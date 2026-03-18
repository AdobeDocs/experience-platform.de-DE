---
title: Adobe Advertising DSP-Verbindung
description: Erfahren Sie, wie Sie authentifizierte und nicht authentifizierte First-Party-Zielgruppen mithilfe mehrerer Identitätstypen für Adobe Advertising Cloud Demand-Side Platform (DSP) freigeben.
feature: Destinations
source-git-commit: 5513e95637c1016caeb6abe699e1807cc234ed40
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 16%

---


# Adobe Advertising DSP-Verbindung

## Überblick {#overview}

Mit dem Ziel Adobe Advertising Cloud Demand-Side Platform (DSP) können Benutzende sowohl authentifizierte als auch nicht authentifizierte First-Party-Zielgruppen mit einem DSP-Konto oder einem bestimmten Advertiser innerhalb eines Kontos teilen.

Mit diesem Ziel können Kundinnen und Kunden Erstanbieter-Zielgruppen für eine oder alle der folgenden IDs freigeben:

* Hash-E-Mail-ID, die zum Targeting in DSP in eine [!DNL LiveRamp RampID] oder [!DNL Unified ID 2.0] (UID2.0) konvertiert wird

* Experience Cloud ID (ECID) und Adobe Advertising-Drittanbieter-Cookies

* Mobile Advertising IDs (MAIDs):

   * [!DNL Google] Advertising IDs (GAIDs) für [!DNL Android] Geräte

   * Kennungen für Advertiser (IDFAs) für [!DNL Apple iOS] Geräte

Diese Verbindung ersetzt die [veraltete Adobe Advertising Cloud DSP-Verbindung](adobe-advertising-cloud-connection-legacy.md) die nur Hash-E-Mail-Adressen unterstützt.

>[!IMPORTANT]
>
>Diese Seite wurde vom Adobe Advertising [!DNL DSP]-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich direkt unter `adcloud_support@adobe.com` an den Advertising Cloud-Support.

## Anwendungsfälle {#use-cases}

Mit diesem Ziel können Werbetreibende ihre Zielgruppe Browser-übergreifend mit Cookies und ohne Cookies erreichen.

Werbetreibende haben die Wahl, Segmente entweder mit authentifizierten First-Party-IDs (wie [!DNL RampID] und [!DNL UID2.0]) oder als nicht authentifizierte IDs (wie Cookies und MAIDs) freizugeben.

## Voraussetzungen {#prerequisites}

* [!DNL RampID activation] Sie [!DNL DSP] Einstellungen auf Konto- und Kampagnenebene, um die Freigabe von Zielgruppen für [!DNL LiveRamp RampID] zu aktivieren. Dadurch werden Kundendaten in [!DNL RampIDs] übersetzt, um Zielgruppensegmente zu erstellen. Diese Konfiguration wird von Ihrem Adobe-Konto-Team durchgeführt. [!DNL RampID] ist über eine Partnerschaft zwischen [!DNL DSP] und [!DNL LiveRamp] verfügbar und Sie benötigen keine eigene [!DNL LiveRamp]-Mitgliedschaft, um sie zu verwenden.

* Zielgruppen-IDs:

   * Für [!DNL RampID] und [!DNL UID2.0] müssen Profile gehashte E-Mail-IDs enthalten.

   * Richten Sie für Cookies einen Cookie-Synchronisierungsprozess mit entweder [!DNL Web SDK] Datenströmen oder dem [!DNL Experience Cloud ID Service] ein. Siehe [Einrichten der ID-Synchronisierung zum Freigeben von Cookies](#cookie-sync) unten.

   * Für Profile mit MAIDs:

      * Fügen Sie für jede GAID den in einer IdentityMap-Spalte `GAID` Wert ein.

      * Fügen Sie für jeden IDFA den in einer IdentityMap-Spalte `IDFA` Wert ein.

* Die Experience Cloud-Organisations-ID für das Experience Platform-Konto. Ihre ID finden Sie auf der Benutzerprofilseite für Adobe Real-Time Customer Data Platform (Real-Time CDP).

* Eine [Real-Time CDP-Quelle in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) zum Empfang von Zielgruppen für die Kampagnenaktivierung. Ihr Adobe-Konto-Team erstellt die Quelle mit Ihrer Experience Cloud-Organisations-ID.

* Der Quellschlüssel für das [!DNL DSP]-Konto oder den Advertiser, der generiert wird, wenn eine [Real-Time CDP-Quelle in erstellt wird [!DNL DSP]](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Ihr [!DNL DSP] Account Team wird diesen Schlüssel mit Ihnen teilen. Sie verwenden sie in Experience Platform, um eine Zielverbindung zum Advertising Cloud DSP-Ziel herzustellen, wie unten beschrieben.

### Einrichten der ID-Synchronisierung zum Freigeben von Cookies {#cookie-sync}

Die ID-Synchronisierung ist eine Voraussetzung für die Freigabe von Drittanbieter-Cookies. Richten Sie einen Cookie-Synchronisierungsprozess mit entweder [!DNL Web SDK] Datenströmen oder der [!DNL Experience Cloud ID Service] ein. Weitere Informationen zur Identitätsverarbeitung für Drittanbieter-Cookies finden Sie unter [Advertising-Ziele, die auf Drittanbieter-Cookie-Integrationen angewiesen sind](/help/destinations/how-destinations-work/identity-handling.md#third-party-cookie-destinations).

**Synchronisierung der Drittanbieter-ID mit[!DNL Web SDK]** aktivieren

Wenn Sie [!DNL Experience Platform Web SDK] verwenden, aktivieren Sie die Synchronisierung von Drittanbieter-IDs in Ihrem Datenstrom, indem Sie die Option [!UICONTROL Third Party ID Sync] in den erweiterten Einstellungen konfigurieren. Anweisungen finden Sie unter [Konfigurieren erweiterter Optionen](/help/datastreams/configure.md#advanced-options) in der Dokumentation zu Datenströmen.

**Aktivieren der Synchronisierung von Drittanbieter-IDs mit dem[!DNL Experience Cloud ID Service]**

Wenn Sie [!DNL Experience Platform] Tags mit dem [!DNL Experience Cloud ID Service] verwenden, konfigurieren Sie die Synchronisierung der Drittanbieter-ID mithilfe der [Experience Cloud ID Service-Erweiterung](/help/tags/extensions/client/id-service/overview.md). Dadurch kann das passende Adobe Advertising-Cookie für die angegebene ECID verfügbar sein, wenn Sie die Zielgruppe in Real-Time CDP aktivieren.

## Unterstützte Identitäten {#supported-identities}

Das Ziel Adobe Advertising Cloud DSP unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben werden. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
| --------------- | ----------- | -------------- |
| `email_lc_sha256` | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Experience Platform unterstützt sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit Experience Platform die Daten bei Aktivierung automatisch hasht. |
| `ECID` | Erstanbieter-Cookie für Experience Cloud | Erforderlich zum Erstellen von Cookie-basierten Segmenten. |
| `Everesttech cookie` | Drittanbieter-Cookie für Adobe Advertising | Erforderlich zum Erstellen von Cookie-basierten Segmenten. |
| `GAID` | [!DNL Android] Geräte-ID | Erforderlich für das Targeting von [!DNL Android]. |
| `IDFA` | [!DNL iOS] Geräte-ID | Erforderlich für das Targeting von [!DNL iOS]. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Ja | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps wie Adobe Journey Optimizer generiert wurden, </li><li> und mehr. </li></ul> |

{style="table-layout:auto"}

Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
| -------------------- | --------- | ----------- | --------- |
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Im Data Lake von Adobe Experience Platform gespeicherte Sammlungen strukturierter Daten. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

In der folgenden Tabelle finden Sie Informationen zum Zielexporttyp und zur Häufigkeit des Exports.

| Element | Typ | Anmerkungen |
| ---- | ---- | ----- |
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den ausgewählten Kennungen. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Wenn ein Profil in Experience Platform auf der Grundlage einer Zielgruppenbewertung aktualisiert wird, sendet der Connector die Aktualisierung nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Experience Platform Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigung[&#x200B; für &#x200B;](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung zum Ziel herzustellen, befolgen Sie die Anweisungen zum [Erstellen einer Zielverbindung](/help/destinations/ui/connect-destination.md) mithilfe der Experience Platform-Benutzeroberfläche. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den folgenden Unterabschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um eine Verbindung zum Ziel herzustellen, geben Sie die folgenden Parameter im Abschnitt [!UICONTROL Connection type] ein und wählen Sie dann **[!UICONTROL Connect to destination]** aus:

* **[!UICONTROL Account or Advertiser Key]**: Dieser [!UICONTROL Source Key] wird generiert, wenn in der Benutzeroberfläche von DSP eine [Real-Time CDP-Quelle erstellt &#x200B;](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Ihr Adobe-Konto-Team teilt diesen Schlüssel mit Ihnen, nachdem es die Quelle erstellt hat.

![Screenshot des Abschnitts „Verbindungstyp“ mit dem Feld „Konto“ oder „Werbekunden-Schlüssel“.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

![Screenshot der Zieldetailfelder mit Eingabe von Name und Beschreibung.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren von Identitäten benötigen Sie die **[!UICONTROL View Identity Graph]** [Zugriffssteuerungsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Sie können die IDs auswählen, die an Adobe Advertising DSP gesendet werden sollen. Standardmäßig sind die Cookie-Kennungen für den Advertiser ausgewählt. Sie können auch [!UICONTROL Hashed Email], [!UICONTROL IDFA] und [!UICONTROL GAID] hinzufügen.

Anweisungen finden Sie unter [Attribute und Identitäten zuordnen](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

![Screenshot des Abschnitts zur Identitätszuordnung mit Cookie-Kennungen, Hash-E-Mail-, IDFA- und GAID-Optionen.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/identity-mapping.png)

## Überprüfen des Datenexports {#exported-data}

Um sicherzustellen, dass die Zielgruppendaten für Advertising Cloud freigegeben wurden, überprüfen Sie Folgendes:

* Der Datenfluss in Ihrem [!DNL Real-Time CDP] Ziel ist erfolgreich.

* In DSP ist die Zielgruppe verfügbar, wenn Sie eine Zielgruppe unter **[!UICONTROL Audiences]** > **[!UICONTROL All Audiences]** oder im Abschnitt **[!UICONTROL Audience Targeting]** der Platzierungseinstellungen erstellen oder bearbeiten. Die Zielgruppe sollte auf der Registerkarte [!UICONTROL Adobe Segments] unter dem Ordner [!UICONTROL Real-Time CDP] angezeigt werden.

![Real-Time CDP-Zielgruppen in den DSP-Zielgruppeneinstellungen](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
