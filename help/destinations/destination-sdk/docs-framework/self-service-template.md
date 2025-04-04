---
title: Dokumentationsvorlage für Selbstbedienung // Ersetzen Sie durch den Namen Ihres Ziels
description: Verwenden Sie diese Vorlage, um eine öffentliche Dokumentation für Ihr Ziel im Adobe Experience Platform-Katalog zu erstellen. // Replace with the paragraph in the Overview section
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 33%

---

# Ihre Zielverbindung {#your-destination}

*Wenn Sie diese Vorlage durchlaufen, ersetzen oder löschen Sie alle kursiv gedruckten Absätze (beginnend mit diesem).*

*Aktualisieren Sie zunächst die Metadaten (Titel und Beschreibung) oben auf der Seite. Bitte ignorieren Sie alle Instanzen von UICONTROL auf dieser Seite. Dieses Tag hilft unseren maschinellen Übersetzungsprozessen dabei, die Seite korrekt in die verschiedenen Sprachen zu übersetzen, die wir unterstützen. Wir fügen Ihrer Dokumentation nach dem Absenden Tags hinzu.*

>[!IMPORTANT]
>
>* Füllen Sie alle Abschnitte in dieser Vorlage in der Reihenfolge aus, in der sie in der Vorlage beschrieben sind.
>* Diese Vorlage wird selten aktualisiert, basierend auf dem Partner-Feedback. Bevor Sie mit der Erstellung der Dokumentation für Ihr Ziel beginnen, stellen Sie sicher, dass Sie die [aktuelle Version der Vorlage](../assets/docs-framework/yourdestination-template.zip) heruntergeladen haben.

## Überblick {#overview}

*Geben Sie einen kurzen Überblick über Ihr Unternehmen, einschließlich des Nutzens, den es für Kunden bietet. Fügen Sie einen Link zu Ihrer Startseite der Produktdokumentation für weitere Informationen hinzu.*

>[!IMPORTANT]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom Team *YourDestination* erstellt und verwaltet. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *Link oder E-Mail-Adresse einfügen, über die Sie für Aktualisierungen, z. B. `support@YourDestination.com`, erreichbar sind.*

## Anwendungsszenarien {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das Ziel *YourDestination* verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Adobe Experience Platform-Kundinnen und -Kunden mit diesem Ziel bewältigen können.

### Anwendungsfall #1 {#use-case-1}

*Für mobile Messaging-Plattformen:*

*Eine Plattform für die Vermietung und den Verkauf von Privathaushalten möchte die Android- und iOS-Geräte seiner Kunden per Push über mobile Benachrichtigungen informieren, damit diese wissen, dass es in dem Bereich, in dem sie zuvor nach einer Vermietung gesucht haben, 100 aktualisierte Listen gibt.*

### Anwendungsfall #2 {#use-case-2}

*Für Plattformen in sozialen Netzwerken:*

*Eine Sportbekleidungsmarke möchte Bestandskunden über ihre Social-Media-Konten erreichen. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM in Adobe Experience Platform aufnehmen, Zielgruppen aus ihren eigenen Offline-Daten erstellen und diese Zielgruppen an YourDestination senden, um Anzeigen in den Social-Media-Feeds ihrer Kunden anzuzeigen.*

## Voraussetzungen {#prerequisites}

*Fügen Sie in diesem Abschnitt Informationen zu allen Dingen hinzu, die Kundinnen und Kunden beachten müssen, bevor Sie das Ziel in der Adobe Experience Platform-Benutzeroberfläche einrichten. Dies kann sein über:*

* *muss zu einer Zulassungsliste hinzugefügt werden*
* *Anforderungen für E-Mail-Hashing*
* *Alle Kontospezifikationen auf Ihrer Seite*
* *So erhalten Sie einen API-Schlüssel für die Verbindung mit Ihrer Plattform*

*Sie können einen Link zu Ihrer entsprechenden Dokumentation herstellen, wenn dies für Kunden nützlich wäre.*

## Unterstützte Identitäten {#supported-identities}

*Fügen Sie in diesem Abschnitt Informationen zu den von Ihrem Ziel unterstützten Identitäten hinzu. Die Tabelle wurde mit einigen Standardwerten vorausgefüllt. Löschen Sie die Werte, die nicht auf Ihr Ziel zutreffen, und/oder fügen Sie Werte hinzu, die nicht vorausgefüllt sind.*

*YourDestination* unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| ECID | Experience Cloud ID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weitere Informationen finden Sie im folgenden Dokument [ECID](/help/identity-service/features/ecid.md) . |
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |
| extern_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

*Fügen Sie in diesem Abschnitt Informationen zu den von Ihrem Ziel unterstützten Zielgruppen hinzu. Die Tabelle wurde mit einigen Standardwerten vorausgefüllt. Verwenden Sie die `✓` und `X` Zeichen, um zu markieren, ob Ihr Zielgruppentyp von diesem Ziel unterstützt wird.*

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | X | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

*Behalten Sie in der Tabelle nur die Zeilen bei, die Ihrem Ziel entsprechen. Es sollte eine Zeile für den Exporttyp und eine Zeile für die Exportfrequenz vorhanden sein. Löschen Sie die Werte, die nicht für Ihr Ziel gelten.*

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im Ziel *YourDestination* verwendet werden. |
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder einer Zielgruppe zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Profilattribute auswählen“ im Workflow &quot;[-Aktivierung“ ](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporttyp | **[!UICONTROL Datensatzexport]** | Sie exportieren Rohdatensätze, die nicht nach Zielgruppeninteressen oder Qualifikationen gruppiert oder strukturiert sind. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

*Fügen Sie die Felder hinzu, die Kunden bei der Authentifizierung bei Ihrem Ziel ausfüllen müssen. Diese Felder sind zielspezifisch und hängen von Ihrer Konfiguration in Destination SDK ab. Die Felder Ihres Ziels sind möglicherweise nicht mit den unten aufgeführten Feldern identisch. Bitte fügen Sie auch einen Screenshot ähnlich dem unten gezeigten Beispiel-Screenshot ein.*

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und klicken Sie auf **[!UICONTROL Mit Ziel verbinden]**.

![Beispiel-Screenshot, der zeigt, wie eine Authentifizierung beim Ziel erfolgt](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL Bearer-Token]**: Füllen Sie das Bearer-Token aus, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

*Fügen Sie die Felder hinzu, die Kundinnen und Kunden beim Konfigurieren eines neuen Ziels ausfüllen müssen. Diese Felder sind zielspezifisch und hängen von Ihrer Konfiguration in Destination SDK ab. Die Felder Ihres Ziels sind möglicherweise nicht mit den unten aufgeführten Feldern identisch. Bitte fügen Sie auch einen Screenshot ähnlich dem unten gezeigten Beispiel-Screenshot ein.*

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Beispiel-Screenshot, der zeigt, wie Details für Ihr Ziel ausgefüllt werden](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihre *YourDestination*-Konto-ID.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Zielen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

*Löschen Sie dies entsprechend - Wenn Sie ein neues Streaming-Ziel dokumentieren, behalten Sie den ersten Absatz unten bei. Wenn Sie ein neues dateibasiertes Ziel dokumentieren, behalten Sie den zweiten Absatz bei. Wenn Sie ein Ziel dokumentieren, das Datensätze exportiert, behalten Sie den dritten Absatz bei.*

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

Lesen Sie [ (Beta) Datensätze exportieren ](/help/destinations/ui/export-datasets.md) ausführliche Anweisungen zum Exportieren von Datensätzen an dieses Ziel.

### Zuordnen von Attributen und Identitäten {#map}

*Fügen Sie im Zuordnungsschritt des Aktivierungs-Workflows Informationen zu unterstützten Zuordnungen zwischen Quell- und Zielfeldern hinzu. Ihr Ziel unterstützt möglicherweise den Export von Profilattributen, Identity-Namespaces oder beidem. Einige Felder sind möglicherweise obligatorisch. Zielattribute können vordefiniert oder benutzerdefiniert sein. Rufen Sie die wichtigen Vorbehalte auf und verwenden Sie Beispiele, vorzugsweise mit Screenshots. Zwei Beispiele für Zielseiten, die Sie als Referenz verwenden können, sind:*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Medallien](/help/destinations/catalog/voice/medallia-connector.md#map)*

## Exportierte Daten/Datenexport validieren {#exported-data}

*Fügen Sie einen Absatz darüber hinzu, wie Daten an Ihr Ziel exportiert werden. Dies würde Kundinnen und Kunden dabei helfen, sicherzustellen, dass sie korrekt in Ihr Ziel integriert haben. Sie können beispielsweise eine JSON-Beispieldatei wie die folgende bereitstellen. Oder Sie können Screenshots und Informationen aus der Benutzeroberfläche Ihres Ziels bereitstellen, die zeigen, wie Kundinnen und Kunden erwarten sollten, dass Zielgruppen in der Zielplattform vorkommen.*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

*Sie können weitere Links zu Ihrer Produktdokumentation oder anderen Ressourcen bereitstellen, die Sie für den Erfolg des Kunden als wichtig erachten.*
