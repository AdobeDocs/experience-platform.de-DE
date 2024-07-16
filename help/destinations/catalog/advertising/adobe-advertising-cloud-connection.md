---
title: Adobe Advertising Cloud DSP-Verbindung
description: Adobe Advertising Cloud DSP ist ein integriertes Ziel für Adobe Real-time Customer Data Platform, mit dem Sie authentifizierte Erstanbieterzielgruppen für zugelassene Advertiser und Benutzer zur Kampagnenaktivierung freigeben können.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 25%

---

# Adobe Advertising Cloud DSP-Verbindung

## Übersicht {#overview}

Mit dem Adobe Advertising Cloud [!DNL Demand-Side Platform] -Ziel (DSP) können Sie authentifizierte Erstanbieterzielgruppen für genehmigte Advertiser und Benutzer freigeben, damit diese für die Kampagnenaktivierung DSP. Weitere Informationen zur Real-Time CDP-Integration mit DSP finden Sie unter [Über die Aktivierung authentifizierter Zielgruppen aus Zielgruppen-Quellen](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Diese Seite wurde vom DSP-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich direkt an den Advertising Cloud-Support unter `adcloud_support@adobe.com`.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das Advertising Cloud DSP-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall für Markenwerbung

Ein Online-Einzelhändler möchte seine Kunden mit hohem Wert über eine Display-Kampagne erneut ansprechen, ohne Cookies für das Targeting zu verwenden. Der Einzelhändler gibt eine Zielgruppe frei, die aus den Hash-E-Mail-IDs seiner hochwertigen Kunden aus seinem Adobe Real-time Customer Data Platform (Real-Time CDP)-Konto besteht, und teilt diese mit seinem DSP Konto. DSP konvertiert dann die Hash-E-Mail-IDs durch eine Partnerschaft zwischen DSP und LiveRamp in authentifizierte [!DNL RampIDs]. Das resultierende [!DNL RampIDs] kann in einer Display-Kampagne verwendet werden, um die Zielgruppe anzusprechen.

### Anwendungsfall der Agentur

Eine Medienagentur mit einem DSP-Konto führt eine Retargeting-Kampagne im Auftrag ihres Kunden, einer Spitzenmarke in der Gastgewerbe. Die Marke möchte im letzten Jahr alle Gäste mit einem neuen Werbeangebot ansprechen. Die Marke hostet alle Gastinformationen in [!DNL Real-Time CDP]. Die Marke kann eine Zielgruppe freigeben, die aus den Hash-E-Mail-IDs ihrer Gäste aus ihrem [!DNL Real-Time CDP] -Konto zum DSP der Medienagentur besteht, um die Gäste durch eine Medienkampagne erneut anzusprechen.

## Voraussetzungen {#prerequisites}

* DSP Einstellungen auf Kontoebene und Kampagnenebene zur Aktivierung der Zielgruppenfreigabe mit [!DNL LiveRamp RampID], wodurch Kundendaten in [!DNL RampIDs] übersetzt werden, um Zielgruppensegmente zu erstellen. Diese Konfiguration wird von Ihrem DSP-Account-Team durchgeführt. [!DNL RampID] ist über eine Partnerschaft zwischen DSP und [!DNL LiveRamp] verfügbar und Sie benötigen keine eigene [!DNL LiveRamp] Mitgliedschaft, um sie zu verwenden.
* Die Experience Cloud-Organisations-ID für das Experience Platform-Konto. Sie finden Ihre ID auf Ihrer [!DNL Real-Time CDP] -Benutzerprofilseite.
* Eine [[!DNL Real-Time CDP] Quelle in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html), um Zielgruppen für die Kampagnenaktivierung zu empfangen. Ihr DSP-Account-Team erstellt die Quelle mithilfe Ihrer Experience Cloud-Organisations-ID.
* Der Quellschlüssel für das DSP- oder Advertiser-Konto, der generiert wird, wenn eine [[!DNL Real-Time CDP] Quelle in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) erstellt wird. Ihr DSP-Account-Team wird diesen Schlüssel für Sie freigeben. Sie verwenden sie innerhalb von Experience Platform, um eine Zielverbindung zum Advertising Cloud DSP-Ziel zu erstellen, wie [unten beschrieben](#authenticate).
* Kundendaten, die aus E-Mails oder gehashten E-Mails bestehen.

## Unterstützte Identitäten {#supported-identities}

Das Adobe Advertising Cloud DSP-Ziel unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Experience Platform unterstützt sowohl einfache als auch SHA256-gehashte E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Transformation anwenden]** , damit Experience Platform die Daten bei Aktivierung automatisch hasst. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

In der folgenden Tabelle finden Sie Informationen zum Zielexporttyp und zur Häufigkeit.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail oder Hash-E-Mail), die im Advertising Cloud DSP-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil auf der Grundlage einer Zielgruppenbewertung im Experience Platform aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [ für Experience Platform. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung zum Ziel herzustellen, befolgen Sie die Anweisungen zum [Erstellen einer Zielverbindung](/help/destinations/ui/connect-destination.md) mithilfe der Experience Platform-Benutzeroberfläche. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um eine Verbindung zum Ziel herzustellen, geben Sie den folgenden Parameter im Abschnitt [!UICONTROL Verbindungstyp] ein und wählen Sie dann **[!UICONTROL Mit Ziel verbinden]**:

* **[!UICONTROL Konto- oder Advertiser-Schlüssel]**: Dieser [!UICONTROL Source-Schlüssel] wird generiert, wenn eine [[!DNL Real-Time CDP] Quelle in der DSP-Benutzeroberfläche erstellt wird.](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) Ihr DSP-Account-Team gibt diesen Schlüssel nach der Erstellung der Quelle für Sie frei.

![Feld &quot;Verbindungstyp&quot;](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

![Zieldetailfelder](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

## Überprüfen des Datenexports {#exported-data}

Um zu überprüfen, ob die Zielgruppe mit Advertising Cloud freigegeben wurde, überprüfen Sie Folgendes:

* Der Datenfluss in Ihrem [!DNL Real-Time CDP] -Ziel ist erfolgreich.

* In DSP ist die Zielgruppe verfügbar, wenn Sie eine Zielgruppe aus [!UICONTROL Zielgruppen] > [!UICONTROL Alle Zielgruppen] oder aus dem Abschnitt [!UICONTROL Zielgruppen-Targeting] der Platzierungseinstellungen erstellen oder bearbeiten. Die Zielgruppe sollte auf der Registerkarte [!UICONTROL Adobe-Segmente] unter dem Ordner [!UICONTROL Real-Time CDP] angezeigt werden.

![Real-Time CDP-Zielgruppen in DSP Zielgruppeneinstellungen](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
