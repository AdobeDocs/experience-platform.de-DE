---
title: Twitter Benutzerdefinierte Zielgruppen-Verbindung
description: Richten Sie Ihre bestehenden Follower und Kunden in Twitter ein und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform erstellten Zielgruppen aktivieren.
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 43%

---

# [!DNL Twitter Custom Audiences]-Verbindung

## Übersicht {#overview}

Sprechen Sie Ihre bestehenden Follower und Kunden auf Twitter an und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform erstellten Zielgruppen aktivieren.

## Voraussetzungen {#prerequisites}

Vor der Konfiguration [!DNL Twitter Custom Audiences] überprüfen Sie unbedingt die folgenden Twitter-Voraussetzungen, die Sie erfüllen müssen.

1. Ihre [!DNL Twitter Ads] müssen für Werbung zugelassen sein. Neu [!DNL Twitter Ads] -Konten sind in den ersten zwei Wochen nach ihrer Erstellung nicht für Werbung geeignet.
2. Ihr Twitter-Benutzerkonto, für das Sie den Zugriff in [!DNL Twitter Audience Manager] muss über die *[!DNL Partner Audience Manager]* Berechtigung aktiviert.

## Unterstützte Identitäten {#supported-identities}

[!DNL Twitter Custom Audiences] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) und Apple ID for Advertisers (IDFA) werden in Adobe Experience Platform unterstützt. Ordnen Sie diese Namespaces und/oder Attribute aus Ihrem Quellschema entsprechend im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) des Zielaktivierungs-Workflows. |
| E-Mail | E-Mail-Adresse(n) des Benutzers | Bitte ordnen Sie in diesem Feld Ihre E-Mail-Adressen mit normalem Text und Ihre SHA256-Hash-E-Mail-Adressen zu. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash. Wenn Sie Ihre Kunden-E-Mail-Adressen vor dem Hochladen in Adobe Experience Platform hash, beachten Sie bitte, dass diese Identitäten mit SHA256 ohne Salz gehasht werden müssen. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs, die im Twitter Custom Audiences-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL Twitter Custom Audiences] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Richten Sie Ihre bestehenden Follower und Kunden in Twitter ein und erstellen Sie relevante Remarketing-Kampagnen, indem Sie Ihre in Adobe Experience Platform as erstellten Zielgruppen aktivieren. [!DNL List Custom Audiences] in Twitter.

## Mit Ziel verbinden {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

1. Suchen Sie die [!DNL Twitter Custom Audiences] Ziel im Zielkatalog auswählen **[!UICONTROL Einrichten]**.
2. Auswählen **[!UICONTROL Mit Ziel verbinden]**.
   ![Bei LinkedIn authentifizieren](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Geben Sie Ihre Twitter-Anmeldedaten ein und wählen Sie **Anmelden**.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="Konto-ID"
>abstract="Ihre Twitter-Werbekonto-ID. Diese ID finden Sie in Ihren Twitter-Werbeeinstellungen."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Konto-ID]**: Ihr [!DNL Twitter Ads] Konto-ID. Diese finden Sie in Ihrer [!DNL Twitter Ads] -Einstellungen.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance – Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

## Zusätzliche Ressourcen {#additional-resources}

Stellen Sie beim Zuordnen von Zielgruppen zu Twitter sicher, dass Sie die folgenden Namensanforderungen für Zielgruppen erfüllen:

1. Stellen Sie für Menschen lesbare Zielgruppen-Mapping-Namen bereit. Es wird empfohlen, denselben Namen zu verwenden, den Sie für die Experience Platform-Segmente verwendet haben.
2. Verwenden Sie keine Sonderzeichen (+ &amp; , % : ; @ / = ? $) in Zielgruppen- und Zielgruppen-Mapping-Namen. Wenn Ihr Experience Platform-Zielgruppenname diese Zeichen enthält, entfernen Sie diese, bevor Sie die Zielgruppe einem Twitter-Ziel zuordnen.

Weitere Informationen über [!DNL List Custom Audiences] in Twitter finden Sie im [Twitter-Dokumentation](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
