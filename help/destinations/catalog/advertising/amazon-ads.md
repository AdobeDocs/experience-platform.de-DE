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

[!DNL Amazon Ads] bietet eine Reihe von Optionen, mit denen Sie Ihre Werbeziele für registrierte Verkäufer, Anbieter, Buchhändler, Kindle Direct Publishing (KDP)-Autoren, App-Entwickler und/oder Agenturen erreichen können.

Die [!DNL Amazon Ads] Integration mit Adobe Experience Platform bietet eine schlüsselfertige Integration für [!DNL Amazon Ads] Produkte, einschließlich Amazon DSP (ADSP) und Amazon Marketing Cloud (AMC).

Mithilfe des [!DNL Amazon Ads]-Ziels in Adobe Experience Platform können Benutzerinnen und Benutzer Advertiser-Zielgruppen für Targeting und Aktivierung in der Amazon-DSP definieren.  Darüber hinaus können Benutzende ihre Daten in [!DNL Amazon Marketing Cloud] hochladen, um die Leistung nach Zielgruppe, von Advertisern bereitgestellten Dimensionen, Zugehörigkeit zu Amazon-Segmenten oder anderen in AMC verfügbaren Signalen zu verstehen. Nach dem Hochladen von Advertiser-Zielgruppen in AMC können Benutzende [!DNL Amazon Marketing Cloud] verwenden, um Zielgruppenmitglieder mithilfe von Amazon-Signalen aus [!DNL Amazon Marketing Cloud] zu ändern, zu verbessern oder an sie anzuhängen.

AMC vereint die einzigartigen Signale aus den von Amazon verwalteten und betriebenen Eigenschaften, die sich über Medien wie Display, Video, Streaming-TV, Audio und gesponserte Anzeigen erstrecken. Benutzerinnen und Benutzer können einfach kuratierte Segmente von Adobe Experience Platform an AMC senden, um das Lernen zu verbessern, z. B. die Markengruppen der Zielgruppen, Lifestyle-Kohorten und Markennamen-Interaktionsmuster. Erweiterte Segmente können dann verwendet werden, um Medienaktivierungen in der Amazon-DSP zu optimieren.

>[!IMPORTANT]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden vom *[!DNL Amazon Ads]*-Team erstellt und gepflegt. Dies ist derzeit ein Beta-Produkt, und die Funktionalität kann sich ändern. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an *`amc-support@amazon.com`.*

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das *[!DNL Amazon Ads]*-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Aktivierung und Zielgruppenbestimmung {#activation-and-targeting}

Durch diese Integration mit Amazon DSP können [!DNL Amazon Ads] Advertiser CDP-Zielgruppen von Adobe Experience Platform an die DSP von Amazon weiterleiten, um Advertiser-Zielgruppen für das Anzeigen-Targeting zu erstellen. Zielgruppen können innerhalb der Amazon-DSP für positives Targeting sowie für negatives Targeting (Unterdrückung) ausgewählt werden. 

### Analyse und Messung {#analytics-and-measurement}

Durch diese Integration mit [!DNL Amazon Marketing Cloud] (AMC) können [!DNL Amazon Ads] Advertiser CDP-Segmente von Adobe Experience Platform Form an AMC weitergeben. Werbetreibende können dann die CDP-Eingaben mit [!DNL Amazon Ads] verbinden und benutzerdefinierte Analysen zu Themen wie Medienwirksamkeit, Zielgruppensegmenten und Kunden-Journey im datenschutzkonformen Format durchführen. Beispielsweise kann ein Werbetreibender eine Liste seiner Bestandskunden hochladen, um die aggregierte Leistung von Werbekampagnen zu verstehen, oder aggregierte Statistiken von Konversionsereignissen auf Amazon, wie das Anzeigen einer Produktdetailseite, das Hinzufügen eines Produkts zu einem Warenkorb oder den Kauf eines Produkts.

### Advertising-Optimierung

Diese Integration mit [!DNL Amazon Marketing Cloud] (AMC) ermöglicht es Werbetreibenden, eigene Kundenlisten hochzuladen und mithilfe von [!DNL Amazon Marketing Cloud] SQL wiederkehrend Überschneidungsanalysen, Unterdrückungen, Ergänzungen oder Optimierungen für Zielgruppen durchzuführen, bevor in der Amazon-DSP eine für die Aktivierung geeignete Zielgruppe für das Targeting erstellt wird.

## Voraussetzungen {#prerequisites}

Um die [!DNL Amazon Ads] mit Adobe Experience Platform verwenden zu können, müssen Benutzende zunächst Zugriff auf ein Amazon DSP Advertiser-Konto oder eine [!DNL Amazon Marketing Cloud]-Instanz haben. Um diese Instanzen bereitzustellen, besuchen Sie die folgende Seite auf der [!DNL Amazon Ads]-Website:

* [Erste Schritte mit Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Erste Schritte mit dem Amazon-Marketing Cloud ](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Unterstützte Identitäten {#supported-identities}

Die *[!DNL Amazon Ads]*-Verbindung unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service//features/namespaces.md). Weitere Informationen zu den von [!DNL Amazon Ads] unterstützten Identitäten finden Sie im [Amazon DSP Support Center](https://advertising.amazon.com/dsp/help/ss/de/audiences#GA6BC9BW52YFXBNE).

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
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

Sie gelangen zur [!DNL Amazon Ads]-Verbindungsschnittstelle, über die Sie zunächst die Advertiser-Konten auswählen, mit denen Sie eine Verbindung herstellen möchten. Bei Verbindungsherstellung werden Sie mit einer neuen Verbindung zurück zu Adobe Experience Platform geleitet, wobei die ID des von Ihnen ausgewählten Advertiser-Kontos angegeben ist. Wählen Sie im Zielkonfigurationsbildschirm das entsprechende Advertiser-Konto aus, um fortzufahren.

* **[!UICONTROL Bearer-Token]**: Füllen Sie das Bearer-Token aus, um sich beim Ziel zu authentifizieren.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Amazon Ads-Verbindung]**: Wählen Sie die ID für das Ziel-[!DNL Amazon Ads] aus, das für das Ziel verwendet wird.

>[!NOTE]
>
>Nach dem Speichern der Zielkonfiguration können Sie die [!DNL Amazon Ads] Advertiser-ID nicht mehr ändern, selbst wenn Sie sich über Ihr Amazon-Konto erneut authentifizieren. Um eine andere [!DNL Amazon Ads] Advertiser-ID zu verwenden, müssen Sie eine neue Zielverbindung erstellen. Werbetreibende, die bereits eine Integration mit ADSP eingerichtet haben, um einen neuen Zielfluss erstellen zu können, wenn ihre Zielgruppen an AMC oder ein anderes ADSP-Konto gesendet werden sollen.

* **[!UICONTROL Advertiser-Region]**: Wählen Sie die gewünschte Region aus, in der Ihr Advertiser gehostet wird. Weitere Informationen zu den von den einzelnen Regionen unterstützten Marktplätzen finden Sie in der [Amazon Ads-Dokumentation](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![Neues Ziel konfigurieren](../../assets/catalog/advertising/amazon_ads_image_4.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Profilen und Zielgruppen für Streaming-Zielgruppen-Exportziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Zuordnen von Attributen und Identitäten {#map}

Die [!DNL Amazon Ads]-Verbindung unterstützt Hash-E-Mail-Adressen und Hash-Telefonnummern zum Abgleichen von Identitäten. Der folgende Screenshot zeigt ein Beispiel für eine Übereinstimmung, die mit der [!DNL Amazon Ads]-Verbindung kompatibel ist:

![Zuordnung von Adobe zu Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Um Hash-E-Mail-Adressen zuzuordnen, wählen Sie den Identity-Namespace von `Email_LC_SHA256` als ein Quellfeld aus.
* Um Hash-Telefonnummern zuzuordnen, wählen Sie den Identity-Namespace von `Phone_SHA256` als ein Quellfeld aus.
* Um ungehashte E-Mail-Adressen oder Telefonnummern zuzuordnen, wählen Sie die entsprechenden Identity-Namespaces als Quellfelder aus und überprüfen Sie die Option `Apply Transformation`, damit Platform die Identitäten bei der Aktivierung hasht.
* *NEU ab der Version vom September 2024*: Amazon Ads erfordert, dass Sie ein Feld mit einem `countryCode` im 2-stelligen ISO-Format zuordnen, um den Prozess der Identitätsauflösung zu erleichtern (z. B.: US, GB, MX, CA usw.). Verbindungen ohne `countryCode` führen zu negativen Auswirkungen auf die Übereinstimmungsraten der Identitäten.

Sie wählen in einer Zielkonfiguration des [!DNL Amazon Ads]-Connectors nur einmal ein bestimmtes Zielfeld aus.  Wenn Sie beispielsweise eine Geschäfts-E-Mail senden, können Sie keine persönliche E-Mail in derselben Zielkonfiguration zuordnen.

Es wird dringend empfohlen, so viele Felder zuzuordnen, wie verfügbar sind. Wenn nur ein Quellattribut verfügbar ist, können Sie ein einzelnes Feld zuordnen. Das [!DNL Amazon Ads]-Ziel verwendet alle zugeordneten Felder für Zuordnungszwecke, was zu höheren Übereinstimmungsraten führt, wenn mehr Felder bereitgestellt werden. Weitere Informationen zu den zulässigen IDs finden Sie auf der [Hilfeseite zu gehashten Zielgruppen von Amazon Ads](https://advertising.amazon.com/dsp/help/ss/de/audiences#GA6BC9BW52YFXBNE).

## Exportierte Daten/Datenexport validieren {#exported-data}

Nach dem Hochladen Ihrer Zielgruppe können Sie mithilfe der folgenden Schritte überprüfen, ob Ihre Zielgruppe korrekt erstellt und hochgeladen wurde:

**Für Amazon DSP**

Navigieren Sie zu **[!UICONTROL Advertiser-ID]** > **[!UICONTROL Zielgruppen]** > **[!UICONTROL Advertiser-Zielgruppen]**. Wenn Ihre Zielgruppe erfolgreich erstellt wurde und die Mindestanzahl an Zielgruppenmitgliedern erreicht, wird der Status von `Active` angezeigt. Weitere Informationen zur Größe und Reichweite Ihrer Zielgruppe finden Sie im Bedienfeld „Prognostizierte Reichweite“ auf der rechten Seite der Benutzeroberfläche von Amazon DSP.

![Validierung der Erstellung von Amazon DSP-Zielgruppen](../../assets/catalog/advertising/amazon_ads_image_3.png)

**Für[!DNL Amazon Marketing Cloud]**

Suchen Sie im linken Schema-Browser Ihre Zielgruppe unter **[!UICONTROL Advertiser hochgeladen]** > **[!UICONTROL aep_audiences]**. Anschließend können Sie Ihre Audience im AMC SQL-Editor mit der folgenden Klausel abfragen:

`select count(user_id) from adobeexperienceplatf_audience_view_000xyz where external_audience_segment_name = '1234567'`

![Validierung der Erstellung von Amazon-Marketing Cloud-Zielgruppen](../../assets/catalog/advertising/amazon_ads_image_5.png)


## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Hilfedokumentation finden Sie in den folgenden [!DNL Amazon Ads]-Hilferessourcen:

* [Hilfezentrum von Amazon DSP](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Änderungsprotokoll {#changelog}

In diesem Abschnitt werden aktualisierte Funktionen und wesentliche Dokumentationsänderungen für diesen Ziel-Connector erfasst.

+++ Änderungsprotokoll anzeigen

| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| Mai 2024 | Funktions- und Dokumentationsaktualisierung | Es wurde die Zuordnungsoption zum Exportieren `countryCode` Parameters in Amazon Ads hinzugefügt. Verwenden Sie `countryCode` im [Zuordnungsschritt](#map) um die Übereinstimmungsraten Ihrer Identitäten mit Amazon zu verbessern. |
| März 2024 | Funktions- und Dokumentationsaktualisierung | Es wurde die Option zum Exportieren von Zielgruppen hinzugefügt, die in [!DNL Amazon Marketing Cloud] (AMC) verwendet werden sollen. |
| Mai 2023 | Funktions- und Dokumentationsaktualisierung | <ul><li>Unterstützung für die Auswahl der Advertiser-Region im [Zielverbindungs-Workflow](#destination-details) hinzugefügt.</li><li>Dokumentation aktualisiert, um das Hinzufügen der Auswahl der Advertiser-Region widerzuspiegeln. Weitere Informationen zum Auswählen der richtigen Advertiser-Region finden Sie in der [Amazon-Dokumentation](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| März 2023 | Erstmalige Veröffentlichung | Ursprüngliche Zielversion und Dokumentation veröffentlicht. |

{style="table-layout:auto"}

+++
