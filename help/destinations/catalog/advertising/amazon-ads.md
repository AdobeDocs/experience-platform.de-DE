---
title: Amazon Ads
description: Amazon Ads bietet eine Reihe von Optionen, mit denen Sie Ihre Werbeziele für registrierte Verkäufer, Anbieter, Buchhersteller, Autoren von Kindle Direct Publishing (KDP), App-Entwickler und/oder Agenturen erreichen können. Die Amazon Ads-Integration mit Adobe Experience Platform bietet eine schlüsselfertige Integration in Amazon Ads-Produkte, einschließlich der Amazon DSP (ADSP). Mit dem Amazon Ads-Ziel in Adobe Experience Platform können Benutzer Advertiser-Zielgruppen für Targeting und Aktivierung auf dem Amazon-DSP definieren.
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 732e6d3d53d983f3390941f4694d2c542d882004
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 29%

---


# (Beta) Amazon Ads-Verbindung {#amazon-ads}

## Übersicht {#overview}

Amazon Ads bietet eine Reihe von Optionen, mit denen Sie Ihre Werbeziele für registrierte Verkäufer, Anbieter, Buchhersteller, Autoren von Kindle Direct Publishing (KDP), App-Entwickler und/oder Agenturen erreichen können.

Die Amazon Ads-Integration mit Adobe Experience Platform bietet eine schlüsselfertige Integration in Amazon Ads-Produkte, einschließlich der Amazon DSP (ADSP). Mit dem Amazon Ads-Ziel in Adobe Experience Platform können Benutzer Advertiser-Zielgruppen für Targeting und Aktivierung auf dem Amazon-DSP definieren.

Diese Verbindung unterstützt die Erstellung von Zielgruppen in den folgenden Amazon Marketplace: `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>Diese Dokumentationsseite wurde von der *Amazon Ads* Team. Dies ist derzeit ein Beta-Produkt und die Funktionalität kann sich ändern. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *`amc-support@amazon.com`.*

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die *Amazon Ads* Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Aktivierung und Zielgruppenbestimmung {#activation-and-targeting}

Durch diese Integration mit Amazon DSP können Amazon Ads-Advertiser CDP-Segmente von Adobe Experience Platform an Amazons DSP weiterleiten, um Advertiser-Zielgruppen für das Anzeigen-Targeting zu erstellen. Zielgruppen können innerhalb der Amazon-DSP für positives Targeting sowie für negatives Targeting (Unterdrückung) ausgewählt werden. Darüber hinaus können Advertiser mithilfe von Signalen, die über Amazon Marketing Cloud generiert werden, ihre Advertiser-Zielgruppen optimieren, um Zielgruppenänderungen mit Amazon-DSP zu synchronisieren.

## Voraussetzungen {#prerequisites}

Um die Amazon Ads-Verbindung mit Adobe Experience Platform verwenden zu können, müssen Benutzer zunächst Zugriff auf ein Amazon DSP Advertiser-Konto haben.  Um diese Instanzen bereitzustellen, besuchen Sie die folgende Seite auf der Amazon Ads-Website:

* [Erste Schritte mit Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## Unterstützte Identitäten {#supported-identities}

Die *Amazon Ads* -Verbindung unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/namespaces.md). Weitere Informationen zu den von Amazon Ads unterstützten Identitäten finden Sie unter [Amazon DSP Support Center](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Sowohl einfache als auch SHA256-Hash-Telefonnummern werden von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder andere), die im *Amazon Ads* Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

Sie gelangen zur Amazon Ads-Verbindungsschnittstelle, über die Sie zunächst die Advertiser-Konten auswählen, mit denen Sie eine Verbindung herstellen möchten.  Nach der Verbindung werden Sie mit einer neuen Verbindung zurück zu Adobe Experience Platform geleitet, wobei die ID des von Ihnen ausgewählten Advertiser-Kontos angegeben ist. Wählen Sie im Zielkonfigurationsbildschirm das entsprechende Advertiser-Konto aus, um fortzufahren.

* **[!UICONTROL Trägertoken]**: Füllen Sie das Trägertoken aus, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Amazon Ads Advertiser ID]**: Wählen Sie die ID für das Amazon Ads-Zielkonto aus, das für das Ziel verwendet wird.

Hinweis: Nachdem Sie diese Amazon Ads Advertiser-ID ausgewählt haben, müssen Sie ein neues Ziel erstellen, um dies zu ändern. Wenn Sie die OAuth-Anmeldeinformationen erneut authentifizieren und eine neue Advertiser-ID auswählen, gelten Ihre Änderungen nicht.

![Neues Ziel konfigurieren](../../assets/catalog/advertising/amazon_ads_image_1.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Zugriffssteuerung – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Profilen und Segmenten für Streaming-Segmentexportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Die Amazon Ads-Verbindung unterstützt Hash-E-Mail-Adressen und Hash-Telefonnummern für Identitätsabgleichzwecke.  Der folgende Screenshot zeigt ein Beispiel für eine Übereinstimmung, die mit der Amazon Ads-Verbindung kompatibel ist:

![Zuordnung von Adobe zu Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Um Hash-E-Mail-Adressen zuzuordnen, wählen Sie die `Email_LC_SHA256` Identitäts-Namespace als Quellfeld.
* Um Hash-Telefonnummern zuzuordnen, wählen Sie die `Phone_SHA256` Identitäts-Namespace als Quellfeld.
* Um ungehashte E-Mail-Adressen oder Telefonnummern zuzuordnen, wählen Sie die entsprechenden Identitäts-Namespaces als Quellfelder aus und überprüfen Sie die `Apply Transformation` -Option, damit Platform die Identitäten bei der Aktivierung hasst.

Es wird dringend empfohlen, so viele Felder zuzuordnen, wie verfügbar sind. Wenn nur ein Quellattribut verfügbar ist, können Sie ein einzelnes Feld zuordnen.  Das Amazon Ads-Ziel nutzt alle zugeordneten Felder für Zuordnungszwecke, wodurch höhere Übereinstimmungsraten erzielt werden, wenn mehr Felder bereitgestellt werden. Weitere Informationen zu den zulässigen Kennungen finden Sie im [Hilfeseite zur Amazon Ads-Hash-Zielgruppe](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Export von Daten/Export validieren {#exported-data}

Nach dem Hochladen Ihrer Audience können Sie mithilfe der folgenden Schritte überprüfen, ob Ihre Audience korrekt erstellt und hochgeladen wurde:

**Für Amazon DSP**

Navigieren Sie zu Ihrer Advertiser-ID → Zielgruppen → Advertiser-Zielgruppen. Wenn Ihre Zielgruppe erfolgreich erstellt wurde und die Mindestanzahl an Zielgruppenmitgliedern erreicht, wird der Status von `Active`.  Weitere Informationen zur Größe und Reichweite Ihrer Zielgruppe finden Sie im Bedienfeld &quot;Erwartete Reichweite&quot;auf der rechten Seite der Benutzeroberfläche von Amazon DSP.

![Validierung der Erstellung von Amazon DSP Zielgruppen](../../assets/catalog/advertising/amazon_ads_image_3.png)

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Hilfedokumentation finden Sie in den folgenden Amazon Ads-Hilferessourcen:

* [Amazon DSP Help Center](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
