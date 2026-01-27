---
title: Verbindung abgleichen
description: Verwenden Sie das Level-Streaming-Ziel, um Zielgruppen direkt in die UserDB- und Segment-Management-APIs von Level zu aktivieren und das Targeting in Echtzeit zur Entscheidungszeit zu unterstützen.
source-git-commit: d820485fd81efd08d8626f8476338558c4585c20
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 9%

---


# [!DNL Kevel]-Verbindung {#kevel}

## Übersicht {#overview}

[[!DNL Kevel]](https://www.kevel.com/) bietet die KI-fähige Technologie und fachkundige Anleitung, die innovativen Commerce-Führungskräften dabei helfen, in Einzelhandelsmedien zu starten, zu skalieren und erfolgreich zu sein. Die Retail Media Cloud von [!DNL Kevel] ermöglicht zielgerichtete, zuordenbare, anpassbare Anzeigenformate für Onsite- und Offsite-Werbung.

Das [!DNL Kevel] Streaming-Ziel für Adobe Experience Platform ermöglicht es Kunden, Adobe-Zielgruppen direkt in die UserDB- und Segment Management-APIs von [!DNL Kevel] zu aktivieren, um das Targeting in Echtzeit zur Zeit der Anzeigenentscheidung zu unterstützen.

>[!IMPORTANT]
> 
>Wenn Sie Fragen haben oder ein Update zum [!DNL Kevel] oder seiner Dokumentation anfordern möchten, wenden Sie sich per E-Mail an das [!DNL Kevel]-Team unter [support@kevel.com](mailto:support@kevel.com).

## Anwendungsfälle {#use-cases}

Sie können für Ihre Medien-Erlebnisse im Einzelhandel Zielgruppen mit umfangreichem First-Party-Verhalten aktivieren, um relevantere Anzeigen und eine bessere Leistung zu liefern. In Experience Platform erstellen Sie absichtsbasierte Zielgruppen mit hohem Wert, z. B. häufige Kategoriekunden oder Benutzende mit aktuellem Produktinteresse, und synchronisieren diese Mitgliedschaften in Echtzeit mit [!DNL Kevel]. [!DNL Kevel] stellt diese Segmente sofort für die Anzeigenentscheidung zur Verfügung und ermöglicht so ein präzises Targeting für gesponserte Produkte und andere Formate für Such-, Browser- und App-Erlebnisse. Sobald Benutzer die Kriterien erfüllen, können Sie diese Signale nutzen, um relevantere Impressions, ein besseres Targeting sowie eine verbesserte Messung und ROAS zu erzielen.

## Voraussetzungen {#prerequisites}

Um sich auf die Verwendung des [!DNL Kevel] Ziels vorzubereiten, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Sie müssen über ein aktives **[!DNL Kevel]-Netzwerk** API-Zugriff verfügen.
- Sie benötigen einen **[!DNL Kevel]API-Schlüssel** Berechtigungen zum Erstellen von Segmenten und Aktualisieren von UserDB-Datensätzen.
- Sie müssen Identity-Namespaces in Experience Platform konfigurieren, die den Identitäten zugeordnet sind, die Ihre Site oder App während [!DNL Kevel] Anzeigenanfragen sendet (z. B. ECID, GAID, IDFA, Treue-ID usw.).
- Adobe-Kunden sollten nur Identitäten zuordnen, die während Echtzeit-Anzeigenanfragen verwendet werden, da jede Identität zu einem UserDB-Eintrag führt.

## Unterstützte Identitäten {#supported-identities}

Das [!DNL Kevel]-Ziel unterstützt die Aktivierung für jede Identität, die Ihre Anwendung beim Senden von Anzeigenanfragen an [!DNL Kevel] verwenden kann. Sie können bis zu drei Identity-Namespaces zuordnen, um entsprechende UserDB-Einträge zu generieren.

[!DNL Kevel] unterstützt die folgenden Identity-Namespaces von Experience Platform:

| Identity-Namespace | Beschreibung | Typische Verwendung |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | Experience Cloud ID | Wird für die Personalisierung vor Ort und die Adobe-übergreifende Identifizierung verwendet. |
| **GAID** | GOOGLE ADVERTISING ID | Wird für den Traffic von Android-Apps/Geräten verwendet. |
| **IDFA** | APPLE ADVERTISING ID | Wird für den Traffic von iOS-Apps/Geräten verwendet (vorbehaltlich der ATT-Zustimmung). |
| **EXTERNAL_ID** | Externe Kennung (benutzerdefinierte Kennung) | Übergibt proprietäre oder Backend-generierte IDs. |

{style="table-layout:auto"}

### Unterstützung für benutzerdefinierte Identity-Namespaces

Das [!DNL Kevel]-Ziel **akzeptiert auch benutzerdefinierte Namespaces** wie in Ihrer Experience Platform-Implementierung definiert.

Dies bedeutet:

- Sie können **kundenspezifische Identity-Namespaces** zuordnen (z. B.: `loyalty_id`, `gigya_id` oder eine beliebige benutzerdefinierte Identität, die Sie in Identity Service definiert haben).
- Diese Namespaces können `kevel_user_key1`, `kevel_user_key2` oder `kevel_user_key3` wie globale Namespaces zugewiesen werden.
- [!DNL Kevel] generiert **einen UserDB-Eintrag pro Instanz jeder zugeordneten Identität** wodurch für jede Kennung, die Ihr System sendet, ein Abgleich in Echtzeit zur Zeit der Anzeigenentscheidung ermöglicht wird.

### Verhalten bei der Identitätszuordnung

- Sie können **bis zu drei** Identity-Namespaces von Experience Platform den drei Identity-Slots von [!DNL Kevel] zuordnen.
- Für jedes aktivierte Profil erhält [!DNL Kevel] **einen UserDB-Eintrag pro Instanz jeder zugeordneten Identität**.
- Kunden sollten nur Identitäten zuordnen, die sie tatsächlich in Anzeigenanfragen an [!DNL Kevel] senden, um unnötigen UserDB-Speicher zu vermeiden.

![Zuordnungsbeispiel für Ebenenziel](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)

## Unterstützte Zielgruppen {#supported-audiences}

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|-----------------------|-----------|---------------------------------------------------------- |
| Segmentierungs-Service | Ja | Von der Segmentierungs-Engine ausgewertete Adobe-Profil-Zielgruppen. |
| Benutzerdefinierte Uploads | Nein | Derzeit nicht unterstützt. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

| Element | Typ | Anmerkungen |
|------|------|-------|
| Exporttyp | **Segmentexport** | [!DNL Kevel] erhält immer dann eine Aktualisierung, wenn sich ein Profil für eine Zielgruppe qualifiziert oder diese verlässt. |
| Exporthäufigkeit | **Streaming** | Aktualisierungen werden in Echtzeit über das Destination SDK-Streaming-Framework gesendet. |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

Befolgen Sie den standardmäßigen Experience Platform-[Ziel verbinden](../../ui/connect-destination.md)-Workflow.

>[!IMPORTANT]
> 
>Sie müssen über **Ziele anzeigen** und **Ziele verwalten** verfügen.

### Beim Ziel authentifizieren {#authenticate}

Wenn Sie eine Verbindung zu [!DNL Kevel] herstellen, geben Sie das folgende Feld an:

- **Bearer-Token** - Ihr [!DNL Kevel] API-Schlüssel.

![Authentifizierungsoptionen für Level Destination](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### Ausfüllen der Zieldetails {#destination-details}

Konfigurieren Sie nach der Authentifizierung Folgendes:

- **Name** - Eine Bezeichnung zur Identifizierung dieser Zielinstanz.
- **Beschreibung** - Optionaler Text zur Beschreibung dieser Zielinstanz.
- **[!DNL Kevel]Netzwerk-ID** - Ihre [!DNL Kevel] Netzwerkkennung.

![Zieldetails für Level Destination](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)

## Aktivieren von Segmenten für dieses Ziel {#activate}

Um Zielgruppen an [!DNL Kevel] zu senden, folgen Sie dem Workflow in\
[Profile und Segmente für Streaming-Segmentexportziele aktivieren](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Deaktivieren von Zielgruppen {#deactivate}

Wenn eine Zielgruppe in Experience Platform deaktiviert oder aus dem [!DNL Kevel] entfernt wird, sendet Experience Platform keine weiteren Profilqualifikationsaktualisierungen mehr für diese Zielgruppe. Jedes vorhandene Segment, das in [!DNL Kevel] erstellt wurde, bleibt verfügbar und wird nicht automatisch gelöscht.

Wenn das [!DNL Kevel] Segment derzeit in einer aktiven Kampagne verwendet wird, verhindert [!DNL Kevel] das Löschen, um den Live-Versand nicht zu unterbrechen. In diesem Fall führt die Deaktivierung in Experience Platform zu Folgendem:

- Der Experience Platform-Datenfluss stoppt
- Das [!DNL Kevel] Segment existiert weiterhin und kann mit Kampagnen verbunden bleiben, bis es manuell entfernt oder die Kampagne aktualisiert wird

Um das Targeting in [!DNL Kevel] vollständig zu stoppen, stellen Sie sicher, dass das Segment aus allen aktiven Kampagnen im Kampagnen-Management-System von [!DNL Kevel] entfernt wird.

### Zuordnen von Attributen und Identitäten {#map}

[!DNL Kevel] erfordert:

- **Identity-Namespaces** - Bis zu drei Identity-Namespaces, [!DNL Kevel] Identitäts-Slots zugeordnet sind.
- **Segmentzugehörigkeit** - Keine manuelle Zuordnung erforderlich. Experience Platform übergibt automatisch Segmentzugehörigkeitskennungen und Aliase.

Wählen Sie während der Aktivierung die Identity-Namespaces aus, die Sie für [!DNL Kevel] konfiguriert haben. Jede Identität generiert einen eigenen UserDB-Aktualisierungsaufruf.

## Exportierte Daten/Datenexport validieren {#exported-data}

Wenn sich ein Profil für eine Zielgruppe qualifiziert und diese verlässt, sendet Experience Platform eine Streaming-Aktualisierung an [!DNL Kevel].

### Beispiel-Payload von [!DNL Kevel] UserDB empfangen

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345
{
  "segments": [1723, 3344, 9988]
}
```

| Parameter | Beschreibung |
|-----------|-------------|
| **userKey** | Abgeleitet von der zugeordneten Adobe-Identität. |
| **Segmente** | Die Gruppe [!DNL Kevel] Segment-IDs, die den Adobe-Zielgruppen entsprechen, für die das Profil derzeit realisiert wird. |

{style="table-layout:auto"}

### Beispiel für beim Export verwendetes Experience Platform-Profil {#sample-profile}

Beim Aktivieren von Zielgruppen für das [!DNL Kevel]-Ziel sendet Experience Platform Profilfragmente, die sowohl **Segmentqualifikationen** als auch die vom Kunden **Identitäten)** den Identity-Slots von [!DNL Kevel] enthalten.

Nachfolgend finden Sie ein Beispiel für ein exportiertes Profil:

- Mehrere Identity-Namespaces, die `kevel_user_key1`, `kevel_user_key2` und `kevel_user_key3` zugeordnet sind
- Ein einzelnes aktiviertes Segment im `ups` Namespace

```json
{
  "segmentMembership": {
    "ups": {
      "9d161bbb-c785-474a-965b-7d7bc2adf879": {
        "status": "realized",
        "lastQualificationTime": "2025-12-10T21:43:38.541076Z"
      }
    }
  },
  "identityMap": {
    "kevel_user_key1": [
      {
        "id": "ECID-fN1zo"
      },
      {
        "id": "ECID-9Xr2p"
      }
    ],
    "kevel_user_key2": [
      {
        "id": "GAID-4oic4"
      }
    ],
    "kevel_user_key3": [
      {
        "id": "IDFA-nB5fU"
      }
    ]
  }
}
```

#### Interpretation [!DNL Kevel] Profils

Bei der [!DNL Kevel] Zielkonfiguration generiert jede zugeordnete Identität einen eigenen UserDB-Eintrag, d. h., [!DNL Kevel] empfängt:

- Ein Update für `ECID-fN1zo`
- Ein Update für `ECID-9Xr2p`
- Ein Update für `GAID-4oic4`
- Ein Update für `IDFA-nB5fU`

Auf diese Weise kann dieselbe Person zum Zeitpunkt der Entscheidungsfindung mit einer ihrer verfügbaren Identitäten erkannt werden, wobei jede Identität einen identischen Satz von Segmentzugehörigkeiten trägt.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Weitere Ressourcen {#additional-resources}

- [[!DNL Kevel] UserDB-Referenz](https://dev.kevel.com/reference/userdb)
- [[!DNL Kevel] Benutzersegment-Targeting](https://dev.kevel.com/docs/segment-targeting)
