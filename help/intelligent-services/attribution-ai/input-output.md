---
keywords: Experience Platform;getting started;Attribution ai;popular topics;Attribution ai input;Attribution ai output;
solution: Experience Platform
title: Attribution AI input and output
topic: Input and Output data for Attribution AI
description: The following document outlines the different input and outputs utilized in Attribution AI.
translation-type: tm+mt
source-git-commit: 2b51569a4c3dd9863edb6831bd182a7fa9d1d891
workflow-type: tm+mt
source-wordcount: '2075'
ht-degree: 4%

---


# [!DNL Attribution AI] input and output

The following document outlines the different input and outputs utilized in [!DNL Attribution AI].

## [!DNL Attribution AI] input data

[!DNL Attribution AI] verwendet [!DNL Consumer Experience Event] Daten, um algorithmische Ergebnisse zu berechnen. For more details on [!DNL Consumer Experience Event], please refer to the [Prepare data for use in Intelligent Services documentation](../data-preparation.md).

Not all the columns in the [!DNL Consumer Experience Event] (CEE) schema are mandatory for Attribution AI.

>[!NOTE]
>
> Die folgenden 9 Spalten sind obligatorisch, zusätzliche Spalten sind optional, werden aber empfohlen/erforderlich, wenn Sie dieselben Daten für andere Adoben wie [!DNL Customer AI] und [!DNL Journey AI]verwenden möchten.

| Obligatorische Spalten | Benötigt für |
| --- | --- |
| Primär-Identitätsfeld | Touchpoint/Umrechnung |
| Zeitstempel | Touchpoint/Umrechnung |
| Channel._type | Touchpoint |
| Channel.mediaAction | Touchpoint |
| Channel.mediaType | Touchpoint |
| Marketing.trackingCode | Touchpoint |
| Marketing.campaignname | Touchpoint |
| Marketing.campaigngroup | Touchpoint |
| Handel | Konversion |

Normalerweise wird die Zuordnung auf Konvertierungsspalten wie Bestellung, Einkäufe und Kassengänge unter &quot;commerce&quot;ausgeführt. Die Spalten &quot;Kanal&quot;und &quot;Marketing&quot;werden dringend empfohlen, Touchpoints für gute Einblicke zu definieren. Sie können jedoch jede weitere Spalte zusammen mit den oben genannten Spalten einschließen, um sie als Konversions- oder Touchpoint-Definition zu konfigurieren.

Die folgenden Spalten sind nicht erforderlich, es wird jedoch empfohlen, sie in Ihr CEE-Schema einzubeziehen, wenn die verfügbaren Informationen vorliegen.

**Zusätzliche empfohlene Spalten:**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### Historische Daten

>[!IMPORTANT]
>
> Die Mindestdatenmenge, die erforderlich ist, damit Attribution AI funktionieren kann, lautet wie folgt:
> - Sie müssen Daten für mindestens 3 Monate (90 Tage) bereitstellen, um ein gutes Modell auszuführen.
> - Sie benötigen mindestens 1000 Konvertierungen.


Attribution AI erfordert historische Daten als Eingabe für Modellschulungen. Die erforderliche Datendauer wird hauptsächlich von zwei Hauptfaktoren bestimmt: Schulungsfenster und Lookback-Fenster. Die Eingabe mit kürzeren Schulungsfenstern ist anfälliger für aktuelle Trends, während längere Schulungsfenster stabilere und genauere Modelle erzeugen. Es ist wichtig, das Ziel mit historischen Daten zu modellieren, die Ihre Geschäftsziele am besten widerspiegeln.

In der Konfiguration [des](./user-guide.md#training-window) Schulungsfensters werden Ereignis zur Konvertierung für Modellschulungen basierend auf der Häufigkeit des Auftretens Filter. Derzeit beträgt das Schulungsfenster mindestens 1 Quartal (90 Tage). Das [Lookback-Fenster](./user-guide.md#lookback-window) bietet einen Zeitraum, der angibt, wie viele Tage vor dem Konversions-Ereignis-Touchpoints im Zusammenhang mit diesem Konversions-Ereignis eingeschlossen werden sollten. Diese beiden Konzepte bestimmen zusammen die Menge der Eingabedaten (gemessen nach Tagen), die für eine Anwendung erforderlich sind.

Standardmäßig definiert Attribution AI das Schulungsfenster als die letzten 2 Quartale (6 Monate) und das Lookback-Fenster als 56 Tage. Anders ausgedrückt, berücksichtigt das Modell alle definierten Konvertierungsmodelle, die in den letzten zwei Quartalen aufgetreten sind, und sucht nach allen Touchpoints, die innerhalb von 56 Tagen vor dem/den zugehörigen Konversions-Ereignissen aufgetreten sind.

**Formel**:

Erforderliche Mindestlänge der Daten = Schulungsfenster + Lookback-Fenster

>[!TIP]
> Die Mindestdatenlänge, die für eine Anwendung mit Standardkonfigurationen erforderlich ist, ist: 2 Quartale (180 Tage) + 56 Tage = 236 Tage.

Beispiel :

- Sie möchten Umrechnungs-Ereignis zuordnen, die innerhalb der letzten 90 Tage (3 Monate) aufgetreten sind, und alle Touchpoints verfolgen, die innerhalb von 4 Wochen vor dem Konversions-Ereignis aufgetreten sind. Die Dauer der Eingabedaten sollte sich über die letzten 90 Tage + 28 Tage (4 Wochen) erstrecken. Das Schulungsfenster beträgt 90 Tage und das Lookback-Fenster insgesamt 118 Tage.

## Attribution AI output data

Attribution AI gibt Folgendes aus:

- [Rohe granulare Punktzahlen](#raw-granular-scores)
- [Aggregierte Ergebnisse](#aggregated-attribution-scores)

**Example output schema:**

![](./images/input-output/schema_output.gif)

### Raw granular scores {#raw-granular-scores}

Attribution AI outputs attribution scores in the most granular level possible so that you can slice and dice the scores by any score column. To view these scores in the UI, read the section on [viewing raw score paths](#raw-score-path). To download the scores using the API visit the [downloading scores in Attribution AI](./download-scores.md) document.

>[!NOTE]
>
> You are able to see any desired reporting column from the input dataset in the score output dataset only if either of the following are true:
> - The reporting column is included in the configuration page either as part of touchpoint or conversion definition configuration.
> - The reporting column is included in additional score dataset columns.


The following table outlines the schema fields in the raw scores example output:

| Column Name (DataType) | Nullable | Beschreibung |
| --- | --- | --- |
| timestamp (DateTime) | False | The time when an conversion event or observation occurred. <br> **Beispiel:** 2020-06-09T00:01:51.000Z |
| identityMap (Map) | True | identityMap des Benutzers ähnlich dem CEE XDM-Format. |
| eventType (String) | True | The primary event type for this time-series record. <br> **Beispiel:** &quot;Bestellung&quot;, &quot;Kauf&quot;, &quot;Besuch&quot; |
| eventMergeId (String) | True | Eine ID zum Korrelieren oder Zusammenführen mehrerer [!DNL Experience Events] Elemente, die im Wesentlichen dasselbe Ereignis sind oder zusammengeführt werden sollten. Dieser soll vor der Aufnahme vom Datenhersteller ausgefüllt werden. <br> **Beispiel:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (Zeichenfolge) | False | Eine eindeutige Kennung für das Ereignis der Zeitreihen. <br> **Beispiel:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (Objekt) | False | Der Container des Objekts auf oberster Ebene, der Ihrer Tent-ID entspricht. <br> **Beispiel:** _atsdsnrmmsv2 |
| your_Schema_name (Objekt) | False | Ergebniszeile mit Konversions-Ereignis mit allen damit verknüpften Touchpoint-Ereignissen und deren Metadaten. <br> **Beispiel:** Attribution AI Scores - Modellname__2020 |
| segmentation (Zeichenfolge) | True | Konversionssegment wie die Geo-Segmentierung, auf dem das Modell basiert. Wenn keine Segmente vorhanden sind, ist das Segment mit dem von convertName identisch. <br> **Beispiel:** ORDER_US |
| convertName (String) | True | Name der Konvertierung, die während der Einrichtung konfiguriert wurde. <br> **Beispiel:** Bestellung, Interessent, Besuch |
| Konversion (Objekt) | False | Konvertierungsmetadatenspalten. |
| dataSource (String) | True | Globale eindeutige Identifizierung einer Datenquelle. <br> **Beispiel:** Adobe Analytics |
| eventSource (String) | True | Die Quelle, an der das eigentliche Ereignis aufgetreten ist. <br> **Beispiel:** Adobe.com |
| eventType (String) | True | The primary event type for this time-series record. <br> **Beispiel:** Bestellung |
| geo (Zeichenfolge) | True | The geographic location where the conversion was delivered `placeContext.geo.countryCode`. <br> **Beispiel:** US |
| priceTotal (Dublette) | True | Durch die Umrechnung erzielte Einnahmen <br> **Beispiel:** 99,9 |
| product (Zeichenfolge) | True | Die XDM-ID des Produkts. <br> **Beispiel:** RX 1080 ti |
| productType (Zeichenfolge) | True | Der Anzeigename für das Produkt, der dem Benutzer für diese Ansicht angezeigt wird. <br> **Beispiel:** Gpus |
| quantity (Integer) | True | Während der Konvertierung gekaufte Menge <br> **Beispiel:** 1 1080 ti |
| receivedTimestamp (DateTime) | True | Zeitstempel der Konvertierung erhalten. <br> **Example:** 2020-06-09T00:01:51.000Z |
| skuId (String) | True | Stock keeping unit (SKU), the unique identifier for a product defined by the vendor. <br> **Example:** MJ-03-XS-Black |
| timestamp (DateTime) | True | Timestamp of the conversion. <br> **Example:** 2020-06-09T00:01:51.000Z |
| passThrough (Object) | True | Additional Score dataset Columns specified by user while configuring the model. |
| commerce_order_purchaseCity (String) | True | Additional Score dataset Column. <br> **Example:** city : San Jose |
| customerProfile (Object) | False | Identity details of the user used to build the model. |
| identity (Object) | False | Enthält die Details des Benutzers, der zum Erstellen des Modells verwendet wird, z. B. `id` und `namespace`. |
| id (Zeichenfolge) | True | Identitäts-ID des Benutzers, z. B. Cookie-ID oder AAID oder MCID usw. <br> **Beispiel:** 17348762725408656344688320891369597404 |
| namensraum (Zeichenfolge) | True | Identitäts-Namensraum, der zum Erstellen der Pfade und damit des Modells verwendet wird. <br> **Beispiel:** aaid |
| touchpointsDetail (Object-Array) | True | Die Liste der Touchpoint-Details, die zur nach Touchpoint-Vorkommen oder Zeitstempel sortierten Konvertierung führen. |
| touchpointName (Zeichenfolge) | True | Name des Touchpoints, der während der Einrichtung konfiguriert wurde. <br> **Beispiel:** PAID_SEARCH_CLICK |
| scores (Objekt) | True | Touchpoint-Beitrag zu dieser Konversion als Ergebnis. Weitere Informationen zu den in diesem Objekt erzeugten Ergebnissen finden Sie im Abschnitt [Aggregierte Zuordnungswerte](#aggregated-attribution-scores) . |
| touchPoint (Objekt) | True | Touchpoint-Metadaten. Weitere Informationen zu den in diesem Objekt erzeugten Ergebnissen finden Sie im Abschnitt zu [aggregierten Ergebnissen](#aggregated-scores) . |

### Anzeigen von Rohwertpfaden (UI) {#raw-score-path}

Sie können den Pfad zu Ihren Rohwerten in der Benutzeroberfläche Ansicht haben. Beginn durch Auswahl von **[!UICONTROL Schemas]** in der Benutzeroberfläche &quot;Plattform&quot;suchen und wählen Sie dann auf der Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;das Schema für die Zuordnungs-AI-Bewertungen aus.

![Schema auswählen](./images/input-output/schemas_browse.png)

Wählen Sie anschließend im Fenster &quot; *[!UICONTROL Struktur]* &quot;der Benutzeroberfläche ein Feld aus. Die Registerkarte &quot; *[!UICONTROL Feldeigenschaften]* &quot;wird geöffnet. Innerhalb der *[!UICONTROL Feldeigenschaften]* ist das Feld *[!UICONTROL Pfad]* , das Ihren Rohwerten zugeordnet wird.

![Schema auswählen](./images/input-output/field_properties.png)


### Aggregierte Zuordnungswerte {#aggregated-attribution-scores}

Aggregierte Punktzahlen können im CSV-Format von der Plattform-Benutzeroberfläche heruntergeladen werden, wenn der Datumsbereich weniger als 30 Tage beträgt.

Attribution AI unterstützt zwei Kategorien von Zuordnungswerten, algorithmische und regelbasierte Werte.

Attribution AI produziert zwei verschiedene Arten von algorithmischen Ergebnissen, inkrementell und beeinflusst. Ein beeinflusster Wert ist der Anteil der Konversion, für die jeder Marketing-Touchpoint verantwortlich ist. An incremental score is the amount of marginal impact directly caused by the marketing touchpoint. The main difference between the incremental score and the influenced score is that the incremental score takes the baseline effect into account. It does not assume that a conversion is caused purely by the preceding marketing touchpoints.

Here is a quick look at an Attribution AI schema output example from the Adobe Experience Platform UI:

![](./images/input-output/schema_screenshot.png)

See the table below for more details about each of these attribution scores:

| Attribution scores | Beschreibung |
| ----- | ----------- |
| Influenced (algorithmic) | Influenced score is the fraction of the conversion that each marketing touchpoint is responsible for. |
| Incremental (algorithmic) | Incremental score is the amount of marginal impact directly caused by a marketing touchpoint. |
| Erstkontakt | Rule-based attribution score that assigns all credits to the initial touchpoint on a conversion path. |
| Letztkontakt | Rule-based attribution score that assigns all credit to the touchpoint closest to the conversion. |
| Linear | Rule-based attribution score that assigns equal credit to each touchpoint on a conversion path. |
| U-förmig | Rule-based attribution score that assigns 40% of the credit to the first touchpoint and 40% of the credit to the last touchpoint, with the other touchpoints splitting the remaining 20% equally. |
| Zeitverfall | Rule-based attribution score where touchpoints closer to the conversion receive more credit than touchpoints that are farther away in time from the conversion. |

**Referenz zur Rohbewertung (Zuordnungswerte)**

Die nachstehende Tabelle ordnet die Zuordnungswerte den Rohwerten zu. Wenn Sie Ihre Rohwerte herunterladen möchten, finden Sie entsprechende [Downloads in der Attribution AI](./download-scores.md) Dokumentation.

| Zuordnungswerte | Referenzspalte für Rohwerte |
| --- | --- |
| Beeinflusst (algorithmisch) | _tenantID.your_Schema_name.element.touchpoint.algorithmicInfluced |
| Inkrementell (algorithmisch) | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.algorithmicInfluced |
| Erstkontakt | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Letztkontakt | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Linear | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.linear |
| U-förmig | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.uForm |
| Zeitverfall | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Aggregierte Ergebnisse {#aggregated-scores}

Aggregierte Punktzahlen können im CSV-Format von der Plattform-Benutzeroberfläche heruntergeladen werden, wenn der Datumsbereich weniger als 30 Tage beträgt. See the table below for more details about each of these aggregate columns.

| Column Name | Constraint | Nullable | Beschreibung |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | User defined &amp; fixed format | False | Customer Event Date in YYYY-MM-DD format. <br> **Example**: 2016-05-02 |
| mediatouchpoints_date (DateTime) | User defined &amp; fixed format | True | Media Touchpoint Date in YYYY-MM-DD format <br> **Example**: 2017-04-21 |
| segment (String) | Calculated | False | Conversion Segment such as geo segmentation which the model is built against. In case of absence of segments, segment is same as conversion_scope. <br> **Example**: ORDER_AMER |
| conversion_scope (String) | User defined | False | Name of the Conversion as configured by the user. <br> **Example**: ORDER |
| touchpoint_scope (String) | User defined | True | Name of the Touchpoint as configured by the user <br> **Example**: PAID_SEARCH_CLICK |
| product (String) | User defined | True | The XDM identifier of the product. <br> **Example**: CC |
| product_type (Zeichenfolge) | Benutzerdefiniert | True | Der Anzeigename für das Produkt, der dem Benutzer für diese Ansicht angezeigt wird. <br> **Beispiel**: Gpus, Laptops |
| geo (Zeichenfolge) | Benutzerdefiniert | True | The geographic location where the conversion was delivered (placeContext.geo.countryCode) <br> **Beispiel**: US |
| ereignis_type (Zeichenfolge) | Benutzerdefiniert | True | The primary event type for this time-series record <br> **Beispiel**: Gebührenpflichtige Konversion |
| media_type (Zeichenfolge) | ENUM | False | Beschreibt, ob der Medientyp bezahlt, im Besitz oder verdient ist. <br> **Beispiel**: BEZAHLTE, EIGENTÜMER |
| kanal (Zeichenfolge) | ENUM | False | Die `channel._type` Eigenschaft, die verwendet wird, um eine grobe Klassifizierung von Kanälen mit ähnlichen Eigenschaften in [!DNL Consumer Experience Event] XDM bereitzustellen. <br> **Beispiel**: SUCHE |
| action (Zeichenfolge) | ENUM | False | Die `mediaAction` Eigenschaft wird verwendet, um eine Art Erlebnis-Ereignis-Medienaktion bereitzustellen. <br> **Beispiel**: KLICKEN |
| kampagne_Gruppe (Zeichenfolge) | Benutzerdefiniert | True | Name der Kampagne, in der mehrere Kampagnen gruppiert sind, z. B. &quot;50%_DISCOUNT&quot;. <br> **Beispiel**: KOMMERZIELL |
| kampagne_name (Zeichenfolge) | Benutzerdefiniert | True | Name der Kampagne, die zur Identifizierung der Marketing-Kampagne verwendet wird, z. B. &#39;50%_DISCOUNT_USA&#39; oder &#39;50%_DISCOUNT_ASIA&#39;. <br> **Beispiel**: Erntedankverkauf |

**Referenz zur Rohbewertung (aggregiert)**

Die nachstehende Tabelle ordnet die aggregierten Ergebnisse den Rohwerten zu. Wenn Sie Ihre Rohwerte herunterladen möchten, finden Sie entsprechende [Downloads in der Attribution AI](./download-scores.md) Dokumentation. Um die Rohwertpfade in der Benutzeroberfläche Ansicht, besuchen Sie den Abschnitt zum [Anzeigen von Rohwertpfaden](#raw-score-path) in diesem Dokument.

| Spaltenname | Referenzspalte &quot;Rohdaten&quot; |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.timestamp |
| Segment | _tenantID.your_Schema_name.segmentation |
| conversion_scope | _tenantID.your_Schema_name.convertions.conversionName |
| touchpoint_scope | _tenantID.your_Schema_name.touchpointsDetail.element.touchpointName |
| product | _tenantID.your_Schema_name.version.product |
| product_type | _tenantID.your_Schema_name.version.product_type |
| geo | _tenantID.your_Schema_name.conversion.geo |
| ereignis_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| kanal | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| Aktion | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |


## Nächste Schritte {#next-steps}

Once you have prepared your data and have all your credentials and schemas in place, start by following the [Attribution AI user guide](./user-guide.md). This guide walks you through creating an instance for Attribution AI.