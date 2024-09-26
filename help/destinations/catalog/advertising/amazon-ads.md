---
title: Amazon Ads
description: Amazon Ads bietet eine Reihe von Optionen, die Ihnen beim Erreichen Ihrer Werbeziele für Agenturen und/oder registrierte Verkäuferschaft, Anbieterschaft, Buchhändlerinnen und -händler, Entwickelnde von Apps oder Autorinnen bzw. Autoren von Kindle Direct Publishing (KDP) hilft. Die Amazon Ads-Integration mit Adobe Experience Platform bietet eine schlüsselfertige Integration in Amazon Ads-Produkte, einschließlich Amazon DSP (ADSP). Mit dem Amazon Ads-Ziel in Adobe Experience Platform können Benutzerinnen und Benutzer Advertiser-Zielgruppen für Targeting und Aktivierung im Amazon DSP definieren.
last-substantial-update: 2024-09-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 2b84b5106105339ab243a9f4412b47692caedf3c
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 52%

---

# (Beta) Amazon Ads-Verbindung {#amazon-ads}

## Übersicht {#overview}

[!DNL Amazon Ads] bietet registrierten Verkäufern, Buchanbietern, Autoren von Kindle Direct Publishing (KDP), App-Entwicklern und/oder Agenturen eine Reihe von Optionen, mit denen Sie Ihre Werbeziele erreichen können.

Die Integration von [!DNL Amazon Ads] mit Adobe Experience Platform bietet eine Umschalter-Integration in [!DNL Amazon Ads] -Produkte, einschließlich Amazon DSP (ADSP) und Amazon Marketing Cloud (AMC).

Mithilfe des Ziels &quot;[!DNL Amazon Ads]&quot;in Adobe Experience Platform können Benutzer Advertiser-Zielgruppen für Targeting und Aktivierung auf der Amazon-DSP definieren.  Darüber hinaus können Benutzer ihre Daten in [!DNL Amazon Marketing Cloud] hochladen, um die Leistung nach Zielgruppe, vom Advertiser bereitgestellten Dimensionen, Zugehörigkeit zu Amazon-Segmenten oder anderen in AMC verfügbaren Signalen zu verstehen. Nach dem Hochladen von Advertiser-Zielgruppen in AMC können Benutzer [!DNL Amazon Marketing Cloud] verwenden, um mithilfe von Amazon-Signalen in [!DNL Amazon Marketing Cloud] Zielgruppenmitglieder zu ändern, zu verbessern oder anzuhängen.

AMC führt einzigartige Signale aus allen von Amazon verwalteten und betriebenen Eigenschaften zusammen, die sich über Medien erstrecken, darunter Display-, Video-, Streaming-TV-, Audio- und gesponserte Anzeigen. Benutzer können auf einfache Weise kuratierte Segmente von Adobe Experience Platform an AMC senden, um das Lernen zu verbessern, z. B. in Marketinggruppen, Lifestyle-Kohorten und Markeninteraktionsmuster von Zielgruppen. Erweiterte Segmente können dann zur Optimierung der Medienaktivierung in Amazon DSP verwendet werden.

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite werden vom *[!DNL Amazon Ads]*-Team erstellt und gepflegt. Dies ist derzeit ein Beta-Produkt, und die Funktionalität kann sich ändern. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *`amc-support@amazon.com`.*

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das *[!DNL Amazon Ads]*-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Aktivierung und Zielgruppenbestimmung {#activation-and-targeting}

Durch diese Integration mit Amazon DSP können [!DNL Amazon Ads] Advertiser CDP-Zielgruppen von Adobe Experience Platform an Amazon-DSP weiterleiten, um Advertiser-Zielgruppen für das Anzeigen-Targeting zu erstellen. Zielgruppen können innerhalb der Amazon-DSP für positives Targeting sowie für negatives Targeting (Unterdrückung) ausgewählt werden. 

### Analyse und Messung {#analytics-and-measurement}

Durch diese Integration mit [!DNL Amazon Marketing Cloud] (AMC) können [!DNL Amazon Ads] Advertiser CDP-Segmente aus dem Adobe Experience Platform-Formular an AMC weiterleiten. Werbetreibende können dann die CDP-Eingaben mit [!DNL Amazon Ads] -Signalen verbinden und benutzerdefinierte Analysen zu Themen wie Medienauswirkungen, Zielgruppensegmente und Journey im datenschutzkonformen Format durchführen. Beispielsweise kann ein Werbetreibende eine Liste seiner bestehenden Kunden hochladen, um die Gesamtleistung der Werbekampagnen oder aggregierte Statistiken über Konversionsereignisse auf der Amazon zu verstehen, z. B. die Anzeige einer Produktdetailseite, das Hinzufügen eines Produkts zu einem Warenkorb oder den Kauf eines Produkts.

### Advertising-Optimierung

Durch die Integration von [!DNL Amazon Marketing Cloud] (AMC) können Werbetreibende ihre eigenen Kundenlisten hochladen und mithilfe von [!DNL Amazon Marketing Cloud] SQL Überschneidungsanalysen, Unterdrückungen, Ergänzungen oder Optimierungen für Zielgruppen wiederkehrend durchführen, bevor eine für die Zielgruppenbestimmung geeignete Zielgruppe in Amazon DSP erstellt wird.

## Voraussetzungen {#prerequisites}

Um die [!DNL Amazon Ads] -Verbindung mit Adobe Experience Platform zu verwenden, müssen Benutzer zunächst Zugriff auf ein Amazon DSP Advertiser-Konto oder eine [!DNL Amazon Marketing Cloud] -Instanz haben. Um diese Instanzen bereitzustellen, besuchen Sie die folgende Seite auf der [!DNL Amazon Ads]-Website:

* [Erste Schritte mit Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Erste Schritte mit Amazon Marketing Cloud](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Unterstützte Identitäten {#supported-identities}

Die Verbindung *[!DNL Amazon Ads]* unterstützt die Aktivierung der Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service//features/namespaces.md). Weitere Informationen zu den von [!DNL Amazon Ads] unterstützten Identitäten finden Sie im [Amazon DSP Support Center](https://advertising.amazon.com/dsp/help/ss/de/audiences#GA6BC9BW52YFXBNE).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| phone_sha256 | Telefonnummern, die mit dem SHA256-Algorithmus gehasht wurden | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder sonstiges), die im *[!DNL Amazon Ads]*-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

Sie gelangen zur Oberfläche [!DNL Amazon Ads] , über die Sie zunächst die Advertiser-Konten auswählen, mit denen Sie eine Verbindung herstellen möchten. Bei Verbindungsherstellung werden Sie mit einer neuen Verbindung zurück zu Adobe Experience Platform geleitet, wobei die ID des von Ihnen ausgewählten Advertiser-Kontos angegeben ist. Wählen Sie im Zielkonfigurationsbildschirm das entsprechende Advertiser-Konto aus, um fortzufahren.

* **[!UICONTROL Bearer-Token]**: Füllen Sie das Bearer-Token aus, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Amazon Ads Connection]**: Wählen Sie die ID für das Ziel-Konto [!DNL Amazon Ads] aus, das für das Ziel verwendet wird.

>[!NOTE]
>
>Nach dem Speichern der Zielkonfiguration können Sie die [!DNL Amazon Ads] Advertiser-ID nicht ändern, selbst wenn Sie sich über Ihr Amazon-Konto erneut authentifizieren. Um eine andere [!DNL Amazon Ads] Advertiser-ID zu verwenden, müssen Sie eine neue Zielverbindung erstellen. Werbetreibende, die bereits für eine Integration mit ADSP eingerichtet sind, müssen einen neuen Zielfluss erstellen, wenn sie möchten, dass ihre Zielgruppen an AMC oder ein anderes ADSP-Konto bereitgestellt werden.

* **[!UICONTROL Advertiser-Region]**: Wählen Sie die gewünschte Region aus, in der Ihr Advertiser gehostet wird. Weitere Informationen zu den von den einzelnen Regionen unterstützten Marktplätzen finden Sie in der [Amazon Ads-Dokumentation](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![Neues Ziel konfigurieren](../../assets/catalog/advertising/amazon_ads_image_4.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Die Verbindung [!DNL Amazon Ads] unterstützt Hash-E-Mail-Adresse und Hash-Telefonnummern für Identitätsabgleichzwecke. Der folgende Screenshot zeigt ein Beispiel für die Übereinstimmung, das mit der [!DNL Amazon Ads] -Verbindung kompatibel ist:

![Zuordnung von Adobe zu Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Um Hash-E-Mail-Adressen zuzuordnen, wählen Sie den Identity-Namespace von `Email_LC_SHA256` als ein Quellfeld aus.
* Um Hash-Telefonnummern zuzuordnen, wählen Sie den Identity-Namespace von `Phone_SHA256` als ein Quellfeld aus.
* Um ungehashte E-Mail-Adressen oder Telefonnummern zuzuordnen, wählen Sie die entsprechenden Identity-Namespaces als Quellfelder aus und überprüfen Sie die Option `Apply Transformation`, damit Platform die Identitäten bei der Aktivierung hasht.
* *NEU ab Version September 2024*: Amazon Ads erfordert, dass Sie ein Feld mit einem `countryCode` -Wert im ISO-Format mit zwei Zeichen zuordnen, um den Prozess der Identitätsauflösung zu erleichtern (z. B. USA, GB, MX, CA usw.). Verbindungen ohne `countryCode` -Zuordnungen wirken sich negativ auf die Identitätsübereinstimmungsraten aus.

Sie wählen ein bestimmtes Zielfeld nur einmal in einer Zielkonfiguration des [!DNL Amazon Ads] -Connectors aus.  Wenn Sie beispielsweise eine geschäftliche E-Mail senden, können Sie keine persönliche E-Mail in derselben Zielkonfiguration zuordnen.

Es wird dringend empfohlen, so viele Felder zuzuordnen, wie verfügbar sind. Wenn nur ein Quellattribut verfügbar ist, können Sie ein einzelnes Feld zuordnen. Das Ziel [!DNL Amazon Ads] nutzt alle zugeordneten Felder zu Zuordnungszwecken, um höhere Übereinstimmungsraten zu erzielen, wenn mehr Felder bereitgestellt werden. Weitere Informationen zu den zulässigen IDs finden Sie auf der [Hilfeseite zu gehashten Zielgruppen von Amazon Ads](https://advertising.amazon.com/dsp/help/ss/de/audiences#GA6BC9BW52YFXBNE).

## Exportierte Daten/Datenexport validieren {#exported-data}

Nach dem Hochladen Ihrer Zielgruppe können Sie mithilfe der folgenden Schritte überprüfen, ob Ihre Zielgruppe korrekt erstellt und hochgeladen wurde:

**Für Amazon DSP**

Navigieren Sie zu Ihrer **[!UICONTROL Advertiser-ID]** > **[!UICONTROL Zielgruppen]** > **[!UICONTROL Advertiser-Zielgruppen]**. Wenn Ihre Zielgruppe erfolgreich erstellt wurde und die Mindestanzahl an Zielgruppenmitgliedern erreicht, wird der Status von `Active` angezeigt. Weitere Informationen zur Größe und Reichweite Ihrer Zielgruppe finden Sie im Bedienfeld „Prognostizierte Reichweite“ auf der rechten Seite der Benutzeroberfläche von Amazon DSP.

![Validierung der Erstellung von Amazon DSP-Zielgruppen](../../assets/catalog/advertising/amazon_ads_image_3.png)

**Für[!DNL Amazon Marketing Cloud]**

Suchen Sie im linken Schema-Browser Ihre Zielgruppe unter **[!UICONTROL Advertiser Uploaded]** > **[!UICONTROL aep_audiences]**. Anschließend können Sie Ihre Zielgruppe im AMC SQL-Editor mit der folgenden -Klausel abfragen:

`select count(user_id) from adobeexperienceplatf_audience_view_000xyz where external_audience_segment_name = '1234567'`

![Validierung der Audience-Erstellung für Amazon Marketing Cloud](../../assets/catalog/advertising/amazon_ads_image_5.png)


## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Hilfedokumentation finden Sie in den folgenden [!DNL Amazon Ads] -Hilferessourcen:

* [Hilfezentrum von Amazon DSP](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Änderungsprotokoll {#changelog}

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| Mai 2024 | Funktions- und Dokumentationsaktualisierung | Die Zuordnungsoption zum Exportieren des Parameters `countryCode` in Amazon Ads wurde hinzugefügt. Verwenden Sie `countryCode` im Schritt [Zuordnen](#map) , um Ihre Identitätsübereinstimmungsraten mit Amazon zu verbessern. |
| März 2024 | Funktions- und Dokumentationsaktualisierung | Die Option zum Exportieren von Zielgruppen, die in [!DNL Amazon Marketing Cloud] (AMC) verwendet werden sollen, wurde hinzugefügt. |
| Mai 2023 | Funktions- und Dokumentationsaktualisierung | <ul><li>Unterstützung für die Auswahl der Advertiser-Region im [Zielverbindungs-Workflow](#destination-details) hinzugefügt.</li><li>Dokumentation aktualisiert, um das Hinzufügen der Auswahl der Advertiser-Region widerzuspiegeln. Weitere Informationen zum Auswählen der richtigen Advertiser-Region finden Sie in der [Amazon-Dokumentation](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| März 2023 | Erstmalige Veröffentlichung | Ursprüngliche Zielversion und Dokumentation veröffentlicht. |

{style="table-layout:auto"}

+++
