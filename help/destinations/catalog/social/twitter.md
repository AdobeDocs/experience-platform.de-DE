---
title: Verbindung mit benutzerdefinierten Twitter-Zielgruppen
description: Sprechen Sie Ihre bestehenden Follower und Kunden auf Twitter an und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform erstellten Zielgruppen aktivieren
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 33%

---

# [!DNL Twitter Custom Audiences]-Verbindung

## Überblick {#overview}

Sprechen Sie Ihre bestehenden Follower und Kunden auf Twitter an und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in [!DNL Adobe Experience Platform] erstellten Zielgruppen aktivieren.

## Voraussetzungen {#prerequisites}

Bevor Sie Ihr [!DNL Twitter Custom Audiences]-Ziel konfigurieren, sollten Sie die folgenden Twitter-Voraussetzungen überprüfen, die Sie erfüllen müssen.

1. Ihr [!DNL Twitter Ads] muss für die Werbung infrage kommen. Neue [!DNL Twitter Ads]-Konten sind in den ersten zwei Wochen nach ihrer Erstellung nicht für die Werbung geeignet.
2. Für Ihr Twitter-Benutzerkonto, auf das Sie in [!DNL Twitter Audience Manager] Zugriff haben, muss die *[!DNL Partner Audience Manager]* aktiviert sein.

## Unterstützte Identitäten {#supported-identities}

[!DNL Twitter Custom Audiences] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) und Apple ID for Advertisers (IDFA) werden in [!DNL Adobe Experience Platform] unterstützt. Ordnen Sie diese Namespaces und/oder Attribute aus Ihrem Quellschema im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) des Zielaktivierungs-Workflows entsprechend zu. |
| email | E-Mail-Adresse(n) für den Benutzer | Bitte ordnen Sie Ihre Nur-Text-E-Mail-Adressen und Ihre SHA256-Hash-E-Mail-Adressen diesem Feld zu. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform]. Wenn Sie Ihre Kunden-E-Mail-Adressen hashen, bevor Sie sie in [!DNL Adobe Experience Platform] hochladen, beachten Sie, dass diese Identitäten mit SHA256 ohne Salz gehasht werden müssen. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Nein | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps generiert werden, z. B. [!DNL Adobe Journey Optimizer], </li><li> und mehr. </li></ul> |

{style="table-layout:auto"}



Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}


## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs, die im Ziel „Benutzerdefinierte Twitter-Zielgruppen“ verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Twitter Custom Audiences]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die [!DNL Adobe Experience Platform] Kunden mit diesem Ziel bewältigen können.

### Anwendungsfall 1 {#use-case-1}

Sprechen Sie Ihre bestehenden Follower und Kunden in Twitter an und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in [!DNL Adobe Experience Platform] erstellten Zielgruppen [!DNL List Custom Audiences] in Twitter aktivieren.

## Mit Ziel verbinden {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

1. Suchen Sie das [!DNL Twitter Custom Audiences] im Zielkatalog und wählen Sie **[!UICONTROL Set Up]** aus.
2. Wählen Sie **[!UICONTROL Connect to destination]** aus.
   ![Authentifizierung bei LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Geben Sie Ihre Twitter-Anmeldeinformationen ein und wählen Sie **Anmelden** aus.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="Konto-ID"
>abstract="Ihre Twitter-Werbekonto-ID. Diese ID finden Sie in Ihren Twitter-Werbeeinstellungen."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Account ID]**: Ihre [!DNL Twitter Ads]-Konto-ID. Diese finden Sie in Ihren [!DNL Twitter Ads].

>[!IMPORTANT]
>
>Verwenden Sie keine Sonderzeichen (+ &amp; , % : ; @ / = ? $ \n) in den Namen der Zielgruppe, Beschreibung und Zielgruppenzuordnung angeben. Wenn der Name Ihrer Experience Platform-Zielgruppe diese Zeichen enthält, entfernen Sie sie, bevor Sie die Zielgruppe einem Twitter-Ziel zuordnen.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnungsüberlegungen {#mapping-considerations}

Geben Sie beim Zuordnen von Zielgruppen zu Twitter menschenlesbare Namen für die Zielgruppenzuordnung an. Es wird empfohlen, denselben Namen zu verwenden, den Sie für die Experience Platform-Segmente verwendet haben.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

## Weitere Ressourcen {#additional-resources}

Weitere Informationen zu [!DNL List Custom Audiences] in Twitter finden Sie in der [Twitter-Dokumentation](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
