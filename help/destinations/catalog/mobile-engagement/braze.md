---
keywords: mobil; einatmen; Messaging;
title: Braze-Verbindung
description: Braze ist eine umfassende Kundeninteraktionsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 9%

---

# [!DNL Braze]-Verbindung

## Übersicht {#overview}

Die [!DNL Braze] Das Ziel hilft beim Senden von Profildaten an [!DNL Braze].

[!DNL Braze] ist eine umfassende Kundeninteraktionsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.

So senden Sie Profildaten an [!DNL Braze], müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die spezifisch für die [!DNL Braze] Ziel:

* [!DNL Adobe Experience Platform] Segmente werden nach [!DNL Braze] unter `AdobeExperiencePlatformSegments` -Attribut.

>[!NOTE]
>
>Beachten Sie beim Senden zusätzlicher benutzerdefinierter Attribute an [!DNL Braze] kann zu einem Anstieg Ihrer [!DNL Braze] Datenpunktverbrauch. Wenden Sie sich an Ihre [!DNL Braze] Kundenbetreuer vor dem Senden zusätzlicher benutzerdefinierter Attribute.

## Anwendungsfälle {#use-cases}

Als Marketing-Experte möchte ich Benutzer in einem Ziel für mobile Interaktionen ansprechen, wobei Segmente in [!DNL Adobe Experience Platform]. Darüber hinaus möchte ich ihnen personalisierte Erlebnisse basierend auf Attributen aus ihren [!DNL Adobe Experience Platform] Profile, sobald Segmente und Profile in [!DNL Adobe Experience Platform].

## Unterstützte Identitäten {#supported-identities}

[!DNL Braze] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten.

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| external_id | Benutzerdefiniert [!DNL Braze] Kennung, die die Zuordnung einer beliebigen Identität unterstützt. | Sie können [identity](../../../identity-service/namespaces.md) der [!DNL Braze] Ziel, solange Sie es dem [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname) und/oder Identitäten, entsprechend Ihrer Feldzuordnung.[!DNL Adobe Experience Platform] Segmente werden nach [!DNL Braze] unter `AdobeExperiencePlatformSegments` -Attribut. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Braze-Konto-Token]**: Dies ist Ihr [!DNL Braze] [!DNL API] Schlüssel. Detaillierte Anweisungen zum Abrufen Ihrer [!DNL API] Schlüssel hier: [REST-API-Schlüssel - Überblick](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, mit dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.
* **[!UICONTROL Endpunktinstanz]**: fragen Sie [!DNL Braze] repräsentativ ist, welche Endpunktinstanz Sie verwenden sollten.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Zuordnungsüberlegungen {#mapping-considerations}

So senden Sie die Zielgruppendaten ordnungsgemäß von [!DNL Adobe Experience Platform] der [!DNL Braze] Ziel, müssen Sie den Schritt zur Feldzuordnung durchlaufen.

Mapping besteht aus der Erstellung einer Verknüpfung zwischen [!DNL Experience Data Model] (XDM)-Schemafelder in Ihrer [!DNL Platform] und ihre entsprechenden Entsprechungen vom Zielort.

So ordnen Sie Ihre XDM-Felder korrekt der [!DNL Braze] Führen Sie die folgenden Schritte aus:

Im [!UICONTROL Zuordnung] Schritt, klicken Sie auf **[!UICONTROL Neues Mapping hinzufügen]**.

![Zielzuordnung löschen](../../assets/catalog/mobile-engagement/braze/mapping.png)

Im [!UICONTROL Quellfeld] klicken Sie auf die Pfeilschaltfläche neben dem leeren Feld.

![Zielquellenzuordnung löschen](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Im [!UICONTROL Quellfeld auswählen] -Fenster können Sie zwischen zwei Kategorien von XDM-Feldern wählen:
* [!UICONTROL Attribute auswählen]: Verwenden Sie diese Option, um ein bestimmtes Feld aus Ihrem XDM-Schema einem [!DNL Braze] -Attribut.

![Quell-Attribut für Zielzuordnung ausblenden](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Identitäts-Namespace auswählen]: Verwenden Sie diese Option, um eine [!DNL Platform] Identitäts-Namespace in eine [!DNL Braze] Namespace.

![Braze Destination Mapping Source Namespace](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Wählen Sie das Quellfeld aus und klicken Sie auf **[!UICONTROL Auswählen]**.

Im [!UICONTROL Zielfeld] klicken Sie auf das Zuordnungssymbol rechts neben dem Feld.

![Zielgruppen-Mapping für Braze](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Im [!UICONTROL Zielgruppenfeld auswählen] -Fenster können Sie zwischen zwei Kategorien von Zielfeldern wählen:
* [!UICONTROL Identitäts-Namespace auswählen]: Verwenden Sie diese Option für die Zuordnung [!DNL Platform] Identitäts-Namespaces zu [!DNL Braze] Identitäts-Namespaces.
* [!UICONTROL Benutzerdefinierte Attribute auswählen]: Verwenden Sie diese Option, um XDM-Attribute benutzerdefinierten Attributen zuzuordnen [!DNL Braze] -Attribute, die Sie in Ihren [!DNL Braze] -Konto. <br> Sie können diese Option auch verwenden, um vorhandene XDM-Attribute in [!DNL Braze]. Sie können beispielsweise eine `lastName` XDM-Attribut zu einem benutzerdefinierten `Last_Name` -Attribut in [!DNL Braze], erstellt die `Last_Name` -Attribut in [!DNL Braze], falls noch nicht vorhanden, und ordnen Sie die `lastName` XDM-Attribut.

![Zielgruppen-Mapping-Felder von Braze Destination](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Wählen Sie Ihr Zielfeld aus und klicken Sie auf **[!UICONTROL Auswählen]**.

Ihr Feld-Mapping sollte jetzt in der Liste angezeigt werden.

![Abschließen der Zielzuordnung verhindern](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die vorherigen Schritte.

## Zuordnungsbeispiel {#mapping-example}

Angenommen, Ihr XDM-Profilschema und Ihr [!DNL Braze] -Instanz enthält die folgenden Attribute und Identitäten:

|  | XDM-Profilschema | [!DNL Braze] Instanz |
|---|---|---|
| Attribute | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identitäten | <ul><li>E-Mail</code></li><li>Google Ad ID (GAID)</code></li><li>Apple ID für Advertiser (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

Die korrekte Zuordnung würde wie folgt aussehen:

![Beispiel für die Braze Destination Mapping](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Exportierte Daten {#exported-data}

So überprüfen Sie, ob die Daten erfolgreich in die [!DNL Braze] Ziel, überprüfen Sie Ihre [!DNL Braze] -Konto. [!DNL Adobe Experience Platform] Segmente werden nach [!DNL Braze] unter `AdobeExperiencePlatformSegments` -Attribut.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](../../../data-governance/home.md).
