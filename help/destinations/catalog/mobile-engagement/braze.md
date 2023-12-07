---
keywords: mobil; braze; messaging;
title: Braze-Verbindung
description: Braze ist eine umfassende Kundeninteraktionsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 34%

---

# [!DNL Braze]-Verbindung

## Übersicht {#overview}

Die [!DNL Braze] Das Ziel hilft beim Senden von Profildaten an [!DNL Braze].

[!DNL Braze] ist eine umfassende Kundeninteraktionsplattform, die relevante und unvergessliche Erlebnisse zwischen Kunden und den Marken, die sie lieben, ermöglicht.

So senden Sie Profildaten an [!DNL Braze], müssen Sie zunächst eine Verbindung zum Ziel herstellen.

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die spezifisch für die [!DNL Braze] Ziel:

* [!DNL Adobe Experience Platform] Zielgruppen werden nach [!DNL Braze] unter `AdobeExperiencePlatformSegments` -Attribut.

>[!NOTE]
>
>Beachten Sie beim Senden zusätzlicher benutzerdefinierter Attribute an [!DNL Braze] kann zu einem Anstieg Ihrer [!DNL Braze] Datenpunktverbrauch. Wenden Sie sich an Ihre [!DNL Braze] Kundenbetreuer vor dem Senden zusätzlicher benutzerdefinierter Attribute.

## Anwendungsfälle {#use-cases}

Marketingexperten möchten mit integrierten Zielgruppen Benutzer in einem mobilen Interaktionsziel ansprechen [!DNL Adobe Experience Platform]. Darüber hinaus möchte ich ihnen personalisierte Erlebnisse basierend auf Attributen aus ihren [!DNL Adobe Experience Platform] Profile, sobald Audiences und Profile in [!DNL Adobe Experience Platform].

## Unterstützte Identitäten {#supported-identities}

[!DNL Braze] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| external_id | Benutzerdefiniert [!DNL Braze] Kennung, die die Zuordnung einer beliebigen Identität unterstützt. | Sie können jede [identity](../../../identity-service/namespaces.md) der [!DNL Braze] Ziel, solange Sie es dem [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname) und/oder Identitäten entsprechend Ihrer Feldzuordnung.[!DNL Adobe Experience Platform] Zielgruppen werden nach [!DNL Braze] unter `AdobeExperiencePlatformSegments` -Attribut. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

* **[!UICONTROL Braze-Konto-Token]**: Dies ist Ihr [!DNL Braze] [!DNL API] Schlüssel. Detaillierte Anweisungen zum Abrufen Ihrer [!DNL API] Schlüssel hier: [REST-API-Schlüssel - Überblick](https://www.braze.com/docs/api/api_key/).

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, mit dem Sie dieses Ziel in Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung ein, mit der Sie dieses Ziel in Zukunft identifizieren können.
* **[!UICONTROL Endpunktinstanz]**: fragen Sie Ihre [!DNL Braze] repräsentativ ist, welche Endpunktinstanz Sie verwenden sollten.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Zuordnungsüberlegungen {#mapping-considerations}

So senden Sie die Zielgruppendaten ordnungsgemäß von [!DNL Adobe Experience Platform] der [!DNL Braze] Ziel, müssen Sie den Schritt zur Feldzuordnung durchlaufen.

Mapping besteht aus der Erstellung einer Verknüpfung zwischen [!DNL Experience Data Model] (XDM)-Schemafelder in Ihrer [!DNL Platform] und ihre entsprechenden Entsprechungen vom Zielort.

Um Ihre XDM-Felder den [!DNL Braze]-Zielfeldern korrekt zuzuordnen, führen Sie die folgenden Schritte aus:

Im [!UICONTROL Zuordnung] Schritt, klicken Sie **[!UICONTROL Neues Mapping hinzufügen]**.

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
| Attribute | <ul><li><code>person.name.firstName</code></li><li><code>person.name.lastName</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>FirstName</code></li><li><code>LastName</code></li><li><code>PhoneNumber</code></li></ul> |
| Identitäten | <ul><li><code>Email</code></li><li><code>Google Ad ID (GAID)</code></li><li><code>Apple ID für Advertiser (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

Die korrekte Zuordnung würde wie folgt aussehen:

![Beispiel für die Braze Destination Mapping](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Braze]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Braze]-Konto. [!DNL Adobe Experience Platform] Zielgruppen werden nach [!DNL Braze] unter `AdobeExperiencePlatformSegments` -Attribut.

## Fehlerbehebung {#troubleshooting}

**Ich habe beim Aktivieren meiner Zielgruppen für dieses Ziel einen Timeout-Fehler erhalten. Was soll ich tun?**

Gelegentlich kann die Aktivierung der Zielgruppe für dieses Ziel zu einem Timeout-Fehler führen. Dieser Fehler wird nicht analysiert, was auf ein Aktivierungsproblem hinweist.

Wenn Sie einen Timeout-Fehler erhalten, überprüfen Sie die Zielgruppengröße in der Zielplattform. Wenn die Zielgruppengröße korrekt ist, funktioniert die Integration erwartungsgemäß.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](../../../data-governance/home.md).
