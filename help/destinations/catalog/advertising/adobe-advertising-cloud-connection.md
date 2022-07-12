---
title: Adobe Advertising Cloud DSP-Verbindung
description: Adobe Advertising Cloud DSP ist ein integriertes Ziel für die [!DNL Adobe Real-time Customer Data Profile], sodass Sie authentifizierte Erstanbietersegmente für zugelassene Advertiser und Benutzer freigeben können, um Kampagnen zu aktivieren.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 8%

---

# Adobe Advertising Cloud DSP-Verbindung

## Übersicht {#overview}

Mit dem Ziel Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) können Sie authentifizierte First-Party-Segmente mit genehmigten Werbetreibenden und Nutzerinnen und Nutzern für die Kampagnenaktivierung mit DSP teilen. Weitere Informationen zur Integration von Real-Time CDP mit DSP finden Sie unter [Informationen zum Aktivieren authentifizierter Segmente aus Zielgruppen-Quellen](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Diese Seite wurde vom DSP-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich direkt an den Advertising Cloud-Support unter `adcloud_support@adobe.com`.

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das Advertising Cloud DSP-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall für Markenwerbung

Ein Online-Einzelhändler möchte seine Kunden mit hohem Wert über eine Display-Kampagne erneut ansprechen, ohne Cookies für das Targeting zu verwenden. Der Einzelhändler gibt ein Segment frei, das aus den Hash-E-Mail-IDs seiner hochwertigen Kunden aus seiner [!DNL Real-Time CDP] auf sein DSP Konto. DSP konvertiert dann die Hash-E-Mail-IDs in authentifizierte [!DNL RampIDs] durch eine Partnerschaft zwischen DSP und LiveRamp. Das Ergebnis [!DNL RampIDs] kann in einer Display-Kampagne zur Zielgruppenbestimmung verwendet werden.

### Anwendungsfall der Agentur

Eine Medienagentur mit einem DSP-Konto führt eine Retargeting-Kampagne im Auftrag ihres Kunden, einer Spitzenmarke in der Gastgewerbe. Die Marke möchte im letzten Jahr alle Gäste mit einem neuen Werbeangebot ansprechen. Die Marke hostet alle Gastinformationen in [!DNL Real-Time CDP]. Die Marke kann ein Segment freigeben, das aus den Hash-E-Mail-IDs der Gäste aus ihrer [!DNL Real-Time CDP] auf das DSP Konto der Medienagentur zu klicken, um die Gäste durch eine Medienkampagne erneut anzusprechen.

## Voraussetzungen {#prerequisites}

* Einstellungen auf Kontoebene und Kampagnenebene DSP, um die Segmentfreigabe zu ermöglichen [!DNL LiveRamp RampID], wodurch Kundendaten in übersetzt werden [!DNL RampIDs] , um Zielgruppensegmente zu erstellen. Diese Konfiguration wird von Ihrem DSP-Account-Team durchgeführt.
* Die Experience Cloud-Organisations-ID für das Experience Platform-Konto. Ihre Kennung finden Sie in Ihrer [!DNL Real-Time CDP] Benutzerprofilseite.
* A [[!DNL Real-Time CDP] Quelle in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) um Segmente für die Kampagnenaktivierung zu erhalten. Ihr DSP-Kontoteam erstellt die Quelle mithilfe Ihrer Experience Cloud-Organisations-ID.
* Der Quellschlüssel für das DSP Konto oder Advertiser, der bei einem [[!DNL Real-Time CDP] -Quelle wird in DSP erstellt](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Ihr DSP-Account-Team wird diesen Schlüssel für Sie freigeben. Sie verwenden es in Experience Platform, um eine Zielverbindung zum Advertising Cloud DSP-Ziel zu erstellen, wie [erklärt unten](#authenticate).
* Kundendaten, die aus E-Mails oder gehashten E-Mails bestehen.

## Unterstützte Identitäten {#supported-identities}

Das Adobe Advertising Cloud DSP-Ziel unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Weitere Informationen [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Experience Platform unterstützt sowohl einfache als auch SHA256-Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, damit Experience Platform die Daten bei Aktivierung automatisch hasst. |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

In der folgenden Tabelle finden Sie Informationen zum Zielexporttyp und zur Häufigkeit.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (E-Mail oder Hash-E-Mail), die im Advertising Cloud DSP-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Wenn ein Profil in Experience Platform basierend auf der Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions) zur Experience Platform. Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung zum Ziel herzustellen, befolgen Sie die Anweisungen unter [Erstellen einer Zielverbindung](/help/destinations/ui/connect-destination.md) über die Experience Platform-Benutzeroberfläche. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### An Ziel authentifizieren {#authenticate}

Um eine Verbindung zum Ziel herzustellen, geben Sie den folgenden Parameter in der [!UICONTROL Verbindungstyp] und wählen Sie **[!UICONTROL Mit Ziel verbinden]**.:

* **[!UICONTROL Konto- oder Advertiser-Schlüssel]**: Diese [!UICONTROL Quellschlüssel] wird generiert, wenn ein [[!DNL Real-Time CDP] -Quelle wird in der DSP-Benutzeroberfläche erstellt.](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Ihr DSP-Account-Team gibt diesen Schlüssel nach der Erstellung der Quelle für Sie frei.

![Feld Verbindungstyp](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Zieldetails ausfüllen {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, mit dem Sie dieses Ziel in der Zukunft erkennen werden.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen dabei hilft, dieses Ziel in der Zukunft zu identifizieren.

![Zieldetailfelder](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Datenexport überprüfen {#exported-data}

Um sicherzustellen, dass das Datensegment für Advertising Cloud freigegeben wurde, überprüfen Sie Folgendes:

* Der Datenfluss in Ihrer [!DNL Real-Time CDP] Ziel ist erfolgreich.

* In DSP ist das Segment verfügbar, wenn Sie eine Zielgruppe aus [!UICONTROL Zielgruppen] > [!UICONTROL Alle Zielgruppen] oder innerhalb von [!UICONTROL Zielgruppen-Targeting] Abschnitt der Platzierungseinstellungen. Das Segment sollte im [!UICONTROL Adobe-Segmente] Registerkarte unter [!UICONTROL Real-Time CDP] Ordner.

![Real-Time CDP-Segmente in DSP Zielgruppeneinstellungen](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zum [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](/help/data-governance/home.md).
