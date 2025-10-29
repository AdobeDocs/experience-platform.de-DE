---
title: Adobe Advertising Cloud DSP-Verbindung
description: Adobe Advertising Cloud DSP ist ein integriertes Ziel für Adobe Real-Time Customer Data Platform, mit dem Sie authentifizierte First-Party-Zielgruppen mit genehmigten Werbetreibenden und Nutzerinnen und Nutzern für die Kampagnenaktivierung teilen können.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 22%

---

# Adobe Advertising Cloud DSP-Verbindung

## Überblick {#overview}

Mit dem Ziel Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) können Sie authentifizierte First-Party-Zielgruppen für genehmigte Werbetreibende und Benutzende zur Kampagnenaktivierung mit DSP freigeben. Weitere Informationen zur Integration von Real-Time CDP mit DSP finden Sie unter [Informationen zum Aktivieren authentifizierter Zielgruppen aus Zielgruppenquellen](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Diese Seite wurde vom DSP-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich direkt unter `adcloud_support@adobe.com` an den Advertising Cloud-Support.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das Advertising Cloud DSP-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel bewältigen können.

### Anwendungsfall für Markenwerbung

Ein Online-retailer möchte seine hochwertigen Kunden über eine Anzeigekampagne erneut ansprechen, ohne Cookies für die Zielgruppenbestimmung zu verwenden. Der retailer gibt eine Audience frei, die aus den gehashten E-Mail-IDs seiner hochwertigen Kunden vom Adobe Real-Time Customer Data Platform (Real-Time CDP)-Konto bis zum DSP-Konto besteht. DSP konvertiert dann die gehashten E-Mail-IDs durch eine Partnerschaft zwischen DSP und LiveRamp in authentifizierte [!DNL RampIDs]. Die resultierende [!DNL RampIDs] kann in einer Anzeigekampagne verwendet werden, um die Zielgruppe anzusprechen.

### Anwendungsfall für Agentur

Eine Medienagentur mit DSP-Account führt im Namen ihres Kunden, einer Top-Marke im Gastgewerbe, eine Retargeting-Kampagne durch. Die Marke möchte alle ihre Gäste im letzten Jahr mit einem neuen Werbeangebot erneut ansprechen. Die Marke hostet alle Gastinformationen in [!DNL Real-Time CDP]. Die Marke kann eine Zielgruppe, die aus den gehashten E-Mail-IDs ihrer Gäste aus ihrem [!DNL Real-Time CDP]-Konto besteht, mit dem DSP-Konto der Medienagentur teilen, um die Gäste durch eine Medienkampagne erneut anzusprechen.

## Voraussetzungen {#prerequisites}

* Einstellungen auf Konto- und Kampagnenebene in DSP, um die Freigabe von Zielgruppen für [!DNL LiveRamp RampID] zu aktivieren. Dadurch werden Kundendaten in [!DNL RampIDs] übersetzt, um Zielgruppensegmente zu erstellen. Diese Konfiguration wird von Ihrem DSP-Konto-Team durchgeführt. [!DNL RampID] ist über eine Partnerschaft zwischen DSP und [!DNL LiveRamp] verfügbar und Sie benötigen keine eigene [!DNL LiveRamp]-Mitgliedschaft, um sie zu verwenden.
* Die Experience Cloud-Organisations-ID für das Experience Platform-Konto. Sie finden Ihre ID auf der Seite Ihres [!DNL Real-Time CDP] Benutzerprofils.
* Eine [[!DNL Real-Time CDP] Quelle in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) um Zielgruppen für die Kampagnenaktivierung zu empfangen. Ihr DSP-Konto-Team erstellt die Quelle mit Ihrer Experience Cloud-Organisations-ID.
* Der Quellschlüssel für das DSP-Konto oder den Advertiser, der generiert wird, wenn eine [[!DNL Real-Time CDP] source in DSP erstellt wird](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Ihr DSP-Konto-Team teilt diesen Schlüssel mit Ihnen. Sie verwenden sie in Experience Platform, um eine Zielverbindung zum Advertising Cloud DSP-Ziel herzustellen, wie [ unten erläutert](#authenticate).
* Kundendaten bestehend aus E-Mails oder Hash-E-Mails.

## Unterstützte Identitäten {#supported-identities}

Das Ziel Adobe Advertising Cloud DSP unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Experience Platform unterstützt sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit Experience Platform die Daten bei Aktivierung automatisch hasht. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

In der folgenden Tabelle finden Sie Informationen zum Zielexporttyp und zur Häufigkeit des Exports.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail oder Hash-E-Mail), die im Advertising Cloud DSP-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil in Experience Platform auf der Grundlage einer Zielgruppenbewertung aktualisiert wird, sendet der Connector die Aktualisierung nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Experience Platform Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigung[ für ](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung zum Ziel herzustellen, befolgen Sie die Anweisungen zum [Erstellen einer Zielverbindung](/help/destinations/ui/connect-destination.md) mithilfe der Experience Platform-Benutzeroberfläche. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um eine Verbindung zum Ziel herzustellen, geben Sie den folgenden Parameter im Abschnitt [!UICONTROL Connection type] ein und wählen Sie dann **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Account or Advertiser Key]**: Diese [!UICONTROL Source Key] wird generiert, wenn eine [[!DNL Real-Time CDP] Quelle in der Benutzeroberfläche von DSP erstellt ](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Ihr DSP-Konto-Team teilt diesen Schlüssel mit Ihnen, nachdem es die Quelle erstellt hat.

![Feld Verbindungstyp](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

![Zieldetailfelder](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

## Überprüfen des Datenexports {#exported-data}

Um sicherzustellen, dass die Zielgruppendaten für Advertising Cloud freigegeben wurden, überprüfen Sie Folgendes:

* Der Datenfluss in Ihrem [!DNL Real-Time CDP] Ziel ist erfolgreich.

* In DSP ist die Zielgruppe verfügbar, wenn Sie eine Zielgruppe unter [!UICONTROL Audiences] > [!UICONTROL All Audiences] oder im Abschnitt [!UICONTROL Audience Targeting] der Platzierungseinstellungen erstellen oder bearbeiten. Die Zielgruppe sollte auf der Registerkarte [!UICONTROL Adobe Segments] unter dem Ordner [!UICONTROL Real-Time CDP] angezeigt werden.

![Real-Time CDP-Zielgruppen in den DSP-Zielgruppeneinstellungen](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
