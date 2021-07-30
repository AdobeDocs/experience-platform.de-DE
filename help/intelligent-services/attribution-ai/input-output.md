---
keywords: Experience Platform; Erste Schritte; Attribution ai; beliebte Themen; Attribution AI-Eingabe; Attribution AI-Ausgabe;
solution: Experience Platform, Intelligent Services
title: Eingabe und Ausgabe in Attribution AI
topic-legacy: Input and Output data for Attribution AI
description: Im folgenden Dokument werden die verschiedenen Ein- und Ausgabedaten beschrieben, die in Attribution AI verwendet werden.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: a49218103669758404a4ddf3f9833b8b2d9b7fc6
workflow-type: tm+mt
source-wordcount: '2230'
ht-degree: 4%

---

# Eingabe und Ausgabe in [!DNL Attribution AI]

Im folgenden Dokument werden die verschiedenen Eingabe- und Ausgabedaten beschrieben, die in [!DNL Attribution AI] verwendet werden.

## [!DNL Attribution AI] Eingabedaten

Attribution AI analysiert einen der folgenden Datensätze, um algorithmische Ergebnisse zu berechnen:

- Datensatz für Kundenerlebnis-Ereignisse (CEE)
- Adobe Analytics-Datensätze, die den [Analytics-Quell-Connector](../../sources/tutorials/ui/create/adobe-applications/analytics.md) verwenden

>[!IMPORTANT]
>
>Der Adobe Analytics-Quell-Connector kann bis zu vier Wochen dauern, bis Daten aufgestockt werden. Wenn Sie kürzlich einen Connector eingerichtet haben, sollten Sie sicherstellen, dass der Datensatz die für Attribution AI erforderliche Mindestlänge von Daten aufweist. Lesen Sie den Abschnitt [historische Daten](#data-requirements) , um sicherzustellen, dass Sie über genügend Daten verfügen, um genaue algorithmische Werte zu berechnen.

Weitere Informationen zum Einrichten des Schemas [!DNL Consumer Experience Event] (CEE) finden Sie im Handbuch [Intelligent Services data preparing](../data-preparation.md) . Weitere Informationen zur Zuordnung von Adobe Analytics-Daten finden Sie in der Dokumentation [Analytics-Feldzuordnungen](../../sources/connectors/adobe-applications/analytics.md) .

Nicht alle Spalten des Schemas [!DNL Consumer Experience Event] (CEE) sind für Attribution AI obligatorisch.

>[!NOTE]
>
> Die folgenden neun Spalten sind obligatorisch. Zusätzliche Spalten sind optional, werden jedoch empfohlen/erforderlich, wenn Sie dieselben Daten für andere Adobe-Lösungen wie [!DNL Customer AI] und [!DNL Journey AI] verwenden möchten.

| Obligatorische Spalten | Benötigt für |
| --- | --- |
| Primäres Identitätsfeld | Touchpoint/Konversion |
| Zeitstempel | Touchpoint/Konversion |
| Channel._type | Touchpoint |
| Channel.mediaAction | Touchpoint |
| Channel.mediaType | Touchpoint |
| Marketing.trackingCode | Touchpoint |
| Marketing.campaignname | Touchpoint |
| Marketing.campaigngroup | Touchpoint |
| Handel | Konversion |

In der Regel wird die Attribution für Konversionsspalten wie Bestellung, Käufe und Checkouts unter &quot;Commerce&quot;ausgeführt. Die Spalten für &quot;channel&quot;und &quot;marketing&quot;werden verwendet, um Touchpoints für Attribution AI zu definieren (z. B. `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). Für optimale Ergebnisse und Einblicke wird dringend empfohlen, so viele Konversions- und Touchpoint-Spalten wie möglich einzuschließen. Außerdem sind Sie nicht auf die oben genannten Spalten beschränkt. Sie können alle anderen empfohlenen oder benutzerdefinierten Spalten als Konversions- oder Touchpoint-Definition einbeziehen.

>[!TIP]
>
>Wenn Sie Adobe Analytics-Daten in Ihrem CEE-Schema verwenden, werden die Touchpoint-Informationen für Analytics normalerweise in `channel.typeAtSource` gespeichert (z. B. `channel.typeAtSource = 'email'`).

Die folgenden Spalten sind nicht erforderlich. Es wird jedoch empfohlen, sie in Ihr CEE-Schema einzuschließen, wenn Sie über die verfügbaren Informationen verfügen.

**Zusätzliche empfohlene Spalten:**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

## Historische Daten {#data-requirements}

>[!IMPORTANT]
>
> Die für die Funktion von Attribution AI erforderliche Datenmenge lautet wie folgt:
> - Sie müssen Daten für mindestens 3 Monate (90 Tage) bereitstellen, um ein gutes Modell auszuführen.
> - Sie benötigen mindestens 1000 Konversionen.


Attribution AI erfordert historische Daten als Eingabe für das Modelltraining. Die erforderliche Datendauer wird hauptsächlich von zwei Schlüsselfaktoren bestimmt: Schulungsfenster und Rückblickfenster. Die Eingabe mit kürzeren Trainings-Fenstern reagiert empfindlicher auf aktuelle Trends, während längere Schulungsfenster dazu beitragen, stabilere und präzisere Modelle zu erstellen. Es ist wichtig, das Ziel mit historischen Daten zu modellieren, die Ihre Geschäftsziele am besten repräsentieren.

Die [Konfiguration des Trainings-Fensters](./user-guide.md#training-window) filtert Konversionsereignisse, die für die Modellschulung auf der Grundlage der Häufigkeit des Vorkommens festgelegt wurden. Derzeit beträgt das Schulungsfenster mindestens 1 Quartal (90 Tage). Das [Lookback-Fenster](./user-guide.md#lookback-window) bietet einen Zeitrahmen, der angibt, wie viele Tage vor den Touchpoints des Konversionsereignisses im Zusammenhang mit diesem Konversionsereignis eingeschlossen werden sollen. Diese beiden Konzepte bestimmen zusammen die Menge der Eingabedaten (gemessen nach Tagen), die für eine Anwendung erforderlich ist.

Standardmäßig definiert Attribution AI das Trainings-Fenster als die letzten 2 Quartale (6 Monate) und das Lookback-Fenster als 56 Tage. Mit anderen Worten: Das Modell berücksichtigt alle definierten Konversionsereignisse, die in den letzten zwei Quartalen aufgetreten sind, und sucht nach allen Touchpoints, die innerhalb von 56 Tagen vor den zugehörigen Konversionsereignissen aufgetreten sind.

**Formel**:

Mindestlänge der erforderlichen Daten = Schulungsfenster + Lookback-Fenster

>[!TIP]
>
> Die Mindestlänge der Daten, die für eine Anwendung mit Standardkonfigurationen erforderlich sind, ist: 2 Quartale (180 Tage) + 56 Tage = 236 Tage.

Beispiel :

- Sie möchten Konversionsereignisse zuordnen, die innerhalb der letzten 90 Tage (3 Monate) stattgefunden haben, und alle Touchpoints verfolgen, die innerhalb von 4 Wochen vor dem Konversionsereignis aufgetreten sind. Die Dauer der Eingabedaten sollte sich über die letzten 90 Tage + 28 Tage (4 Wochen) erstrecken. Das Schulungsfenster beträgt 90 Tage, das Lookback-Fenster 28 Tage und insgesamt 118 Tage.

## Attribution AI der Ausgabedaten

Attribution AI gibt Folgendes aus:

- [Rohe granulare Punktzahl](#raw-granular-scores)
- [Aggregierte Werte](#aggregated-attribution-scores)

**Beispiel für ein Ausgabeschema:**

![](./images/input-output/schema_output.gif)

### Rohe granulare Punktzahl {#raw-granular-scores}

Attribution AI gibt Attributionsbewertungen auf der detailliertesten Ebene aus, sodass Sie die Bewertungen nach jeder Bewertungsspalte austeilen und würfen können. Um diese Bewertungen in der Benutzeroberfläche anzuzeigen, lesen Sie den Abschnitt [Anzeigen von Rohwertpfaden](#raw-score-path). Um die Bewertungen mit der API herunterzuladen, besuchen Sie das Dokument [Herunterladen von Bewertungen in Attribution AI](./download-scores.md) .

>[!NOTE]
>
> Sie können jede gewünschte Berichtsspalte aus dem Eingabedatensatz im Ergebnisausgabedatensatz nur dann anzeigen, wenn eine der folgenden Bedingungen erfüllt ist:
> - Die Berichtsspalte ist auf der Konfigurationsseite entweder als Teil der Touchpoint- oder Konversionsdefinitionskonfiguration enthalten.
> - Die Berichtsspalte ist in zusätzliche Score-Datensatzspalten enthalten.


In der folgenden Tabelle sind die Schemafelder in der Beispielausgabe für Rohbewertungen aufgeführt:

| Spaltenname (DataType) | NULL | Beschreibung |
| --- | --- | --- |
| timestamp (DateTime) | False | Der Zeitpunkt, zu dem ein Konversionsereignis oder eine Beobachtung aufgetreten ist. <br> **Beispiel:** 2020-06-09T00:01:51.000Z |
| identityMap (Map) | True | identityMap des Benutzers ähnlich dem CEE XDM-Format. |
| eventType (String) | True | Der primäre Ereignistyp für diesen Zeitreihensatz. <br> **Beispiel:** &quot;Bestellung&quot;, &quot;Kauf&quot;, &quot;Besuch&quot; |
| eventMergeId (String) | True | Eine ID zum Korrelieren oder Zusammenführen mehrerer [!DNL Experience Events]-Zeichen, die im Wesentlichen dasselbe Ereignis sind oder zusammengeführt werden sollen. Dieser sollte vor der Aufnahme vom Datenproduzenten ausgefüllt werden. <br> **Beispiel:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (String) | False | Eine eindeutige Kennung für das Zeitreihenereignis. <br> **Beispiel:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (Object) | False | Der oberste Objektcontainer, der Ihrer zehnten ID entspricht. <br> **Beispiel:** _atsdsnrmsv2 |
| your_schema_name (Objekt) | False | Ergebniszeile mit Konversionsereignis alle damit verknüpften Touchpoint-Ereignisse und deren Metadaten. <br> **Beispiel:** Attribution AI Scores - Modellname__2020 |
| Segmentierung (Zeichenfolge) | True | Konversionssegment, z. B. Geo-Segmentierung, für die das Modell erstellt wird. Wenn keine Segmente vorhanden sind, ist das Segment mit conversionName identisch. <br> **Beispiel:** ORDER_US |
| conversionName (String) | True | Name der Konversion, die während der Einrichtung konfiguriert wurde. <br> **Beispiel:** Bestellung, Lead, Besuch |
| conversion (Object) | False | Konversionsmetadaten-Spalten. |
| dataSource (String) | True | Globale eindeutige Identifizierung einer Datenquelle. <br> **Beispiel:** Adobe Analytics |
| eventSource (String) | True | Die Quelle, an der das tatsächliche Ereignis aufgetreten ist. <br> **Beispiel:** Adobe.com |
| eventType (String) | True | Der primäre Ereignistyp für diesen Zeitreihensatz. <br> **Beispiel:** Reihenfolge |
| geo (String) | True | Der geografische Ort, an dem die Konvertierung bereitgestellt wurde `placeContext.geo.countryCode`. <br> **Beispiel:** US |
| priceTotal (Double) | True | Durch die Konversion erzielter Umsatz <br> **Beispiel:** 99.9 |
| product (String) | True | Die XDM-ID des Produkts. <br> **Beispiel:** RX 1080 ti |
| productType (String) | True | Der Anzeigename für das Produkt, wie er dem Benutzer für diese Produktansicht angezeigt wird. <br> **Beispiel:** GPG |
| quantity (Integer) | True | Während der Konvertierung gekaufte Menge. <br> **Beispiel:** 1 1080 ti |
| receivedTimestamp (DateTime) | True | Zeitstempel der Konvertierung erhalten. <br> **Beispiel:** 2020-06-09T00:01:51.000Z |
| skuId (String) | True | Bestandseinheit (Stock Keeping Unit, SKU), die eindeutige Kennung für ein vom Anbieter definiertes Produkt. <br> **Beispiel:** MJ-03-XS-Black |
| timestamp (DateTime) | True | Zeitstempel der Konvertierung. <br> **Beispiel:** 2020-06-09T00:01:51.000Z |
| passThrough (Object) | True | Zusätzliche Score-Datensatzspalten, die vom Benutzer beim Konfigurieren des Modells angegeben werden. |
| commerce_order_purchaseCity (String) | True | Zusätzliche Spalte für Datensatz mit Punktzahl . <br> **Beispiel:** city : San Jose |
| customerProfile (Object) | False | Identitätsdetails des Benutzers, der zum Erstellen des Modells verwendet wird. |
| identity (Object) | False | Enthält die Details des Benutzers, der zum Erstellen des Modells verwendet wird, z. B. `id` und `namespace`. |
| id (String) | True | Identitäts-ID des Benutzers, z. B. Cookie-ID, AAID oder MCID usw. <br> **Beispiel:** 17348762725408656344688320891369597404 |
| namespace (String) | True | Identitäts-Namespace, der zum Erstellen der Pfade und damit des Modells verwendet wird. <br> **Beispiel:** aaid |
| touchpointsDetail (Object Array) | True | Die Liste der Touchpoint-Details, die zur Konvertierung führen, die nach | Touchpoint-Vorkommen oder Zeitstempel. |
| touchpointName (String) | True | Name des Touchpoints, der beim Einrichten konfiguriert wurde. <br> **Beispiel:** PAID_SEARCH_CLICK |
| scores (Object) | True | Touchpoint-Beitrag zu dieser Konversion als Ergebnis. Weitere Informationen zu den in diesem Objekt erzeugten Werten finden Sie im Abschnitt [Aggregierte Attributionswerte](#aggregated-attribution-scores) . |
| touchPoint (Object) | True | Touchpoint-Metadaten. Weitere Informationen zu den in diesem Objekt erzeugten Werten finden Sie im Abschnitt [aggregierte Werte](#aggregated-scores) . |

### Anzeigen von Rohbewertungspfaden (Benutzeroberfläche) {#raw-score-path}

Sie können den Pfad zu Ihren Rohbewertungen in der Benutzeroberfläche anzeigen. Wählen Sie zunächst **[!UICONTROL Schemas]** in der Platform-Benutzeroberfläche aus und suchen Sie dann Ihr Attributions-AI-Punktschema im Tab **[!UICONTROL Durchsuchen]** und wählen Sie es aus.

![Schema auswählen](./images/input-output/schemas_browse.png)

Wählen Sie anschließend ein Feld im Fenster **[!UICONTROL Struktur]** der Benutzeroberfläche aus. Die Registerkarte **[!UICONTROL Feldeigenschaften]** wird geöffnet. Innerhalb von **[!UICONTROL Feldeigenschaften]** ist das Pfadfeld, das Ihren Rohwerten zugeordnet ist.

![Auswählen eines Schemas](./images/input-output/field_properties.png)


### Aggregierte Attributionswerte {#aggregated-attribution-scores}

Aggregierte Bewertungen können über die Platform-Benutzeroberfläche im CSV-Format heruntergeladen werden, wenn der Datumsbereich weniger als 30 Tage beträgt.

Attribution AI unterstützt zwei Kategorien von Attributionsbewertungen: algorithmische und regelbasierte Bewertungen.

Attribution AI erzeugt zwei verschiedene Arten algorithmischer Punktzahlen, inkrementell und beeinflusst. Ein beeinflusst Ergebnis ist der Anteil der Konversion, für den jeder Marketing-Touchpoint verantwortlich ist. Ein inkrementelles Ergebnis ist der Betrag der direkt durch den Marketing-Touchpoint verursachten marginalen Auswirkungen. Der Hauptunterschied zwischen dem inkrementellen Ergebnis und dem beeinflussten Ergebnis besteht darin, dass das inkrementelle Ergebnis den Basiseffekt berücksichtigt. Es wird nicht davon ausgegangen, dass eine Konversion ausschließlich durch die vorherigen Marketing-Touchpoints verursacht wird.

Im Folgenden finden Sie ein Beispiel für die Ausgabe eines Attribution AI-Schemas über die Adobe Experience Platform-Benutzeroberfläche:

![](./images/input-output/schema_screenshot.png)

Weitere Informationen zu den einzelnen Attributionsbewertungen finden Sie in der folgenden Tabelle:

| Attributionsbewertungen | Beschreibung |
| ----- | ----------- |
| Beeinflusst (algorithmisch) | Beeinflusstes Ergebnis ist der Anteil der Konversion, für den jeder Marketing-Touchpoint verantwortlich ist. |
| Inkrementell (algorithmisch) | Das inkrementelle Ergebnis ist der Betrag der direkt durch einen Marketing-Touchpoint verursachten marginalen Auswirkungen. |
| Erstkontakt | Regelbasierte Attributionsbewertung, die alle Gutschriften dem ursprünglichen Touchpoint auf einem Konversionspfad zuweist. |
| Letztkontakt | Regelbasierte Attributionsbewertung, die die gesamte Gutschrift dem Touchpoint zuweist, der der Konversion am nächsten ist. |
| Linear | Regelbasierte Attributionsbewertung, die jedem Touchpoint auf einem Konversionspfad die gleiche Gewichtung zuweist. |
| U-förmig | Regelbasierte Attributionsbewertung, die 40 % des Guthabens dem ersten Touchpoint und 40 % des Guthabens dem letzten Touchpoint zuweist, während die anderen Touchpoints die verbleibenden 20 % gleichmäßig aufteilen. |
| Zeitverfall | Regelbasierte Attributionsbewertung, bei der Touchpoints, die näher an der Konversion liegen, mehr Gewichtung erhalten als Touchpoints, die zeitlich weit von der Konversion entfernt sind. |

**Rohbewertungs-Referenz (Attributionswerte)**

Die nachstehende Tabelle ordnet die Attributionsbewertungen den Rohbewertungen zu. Wenn Sie Ihre Rohbewertungen herunterladen möchten, besuchen Sie die Dokumentation [Herunterladen von Bewertungen in Attribution AI](./download-scores.md) .

| Attributionsbewertungen | Rohwertverweisspalte |
| --- | --- |
| Beeinflusst (algorithmisch) | _tenantID.your_schema_name.element.touchpoint.algorithmicInfluapped |
| Inkrementell (algorithmisch) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInfluapped |
| Erstkontakt | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Letztkontakt | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Linear | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U-förmig | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| Zeitverfall | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Aggregierte Werte {#aggregated-scores}

Aggregierte Bewertungen können über die Platform-Benutzeroberfläche im CSV-Format heruntergeladen werden, wenn der Datumsbereich weniger als 30 Tage beträgt. Weitere Informationen zu den einzelnen Aggregat-Spalten finden Sie in der unten stehenden Tabelle.

| Spaltenname | Einschränkung | NULL | Beschreibung |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Benutzerdefiniertes und festes Format | False | Kundenereignisdatum im Format JJJJ-MM-TT. <br> **Beispiel**: 02.05.2016 |
| mediatouchpoints_date (DateTime) | Benutzerdefiniertes und festes Format | True | Medien-Touchpoint-Datum im Format JJJ-MM-TT <br> **Beispiel**: 21.4.2017 |
| Segment (String) | Berechnet | False | Konversionssegment, z. B. Geo-Segmentierung, für die das Modell erstellt wird. Wenn keine Segmente vorhanden sind, ist das Segment mit conversion_scope identisch. <br> **Beispiel**: ORDER_AMER |
| conversion_scope (String) | Benutzerdefiniert | False | Name der vom Benutzer konfigurierten Konvertierung. <br> **Beispiel**: BESTELLUNG |
| Touchpoint_scope (String) | Benutzerdefiniert | True | Name des Touchpoints, wie vom Benutzer <br> konfiguriert **Beispiel**: PAID_SEARCH_CLICK |
| product (String) | Benutzerdefiniert | True | Die XDM-Kennung des Produkts. <br> **Beispiel**: CC |
| product_type (String) | Benutzerdefiniert | True | Der Anzeigename für das Produkt, wie er dem Benutzer für diese Produktansicht angezeigt wird. <br> **Beispiel**: Gpus, Laptops |
| geo (String) | Benutzerdefiniert | True | Der geografische Standort, an dem die Konvertierung bereitgestellt wurde (placeContext.geo.countryCode) <br> **Beispiel**: USA |
| event_type (String) | Benutzerdefiniert | True | Der primäre Ereignistyp für diesen Zeitreihensatz <br> **Beispiel**: Gebührenpflichtige Konversion |
| media_type (String) | ENUM | False | Beschreibt, ob der Medientyp gebührenpflichtig, besessen oder verdient ist. <br> **Beispiel**: BEZAHLTE, EIGENTÜMER |
| channel (String) | ENUM | False | Die `channel._type`-Eigenschaft, die verwendet wird, um eine grobe Klassifizierung von Kanälen mit ähnlichen Eigenschaften in [!DNL Consumer Experience Event] XDM bereitzustellen. <br> **Beispiel**: SUCHEN |
| action (String) | ENUM | False | Die `mediaAction`-Eigenschaft wird verwendet, um einen Typ von Erlebnisereignis-Medienaktion bereitzustellen. <br> **Beispiel**: KLICKEN |
| campaign_group (String) | Benutzerdefiniert | True | Name der Kampagnengruppe, in der mehrere Kampagnen gruppiert sind, z. B. &#39;50%_DISCOUNT&#39;. <br> **Beispiel**: KOMMERZIELL |
| campaign_name (String) | Benutzerdefiniert | True | Name der Kampagne, die zur Identifizierung der Marketing-Kampagne verwendet wird, z. B. &#39;50%_DISCOUNT_USA&#39; oder &#39;50%_DISCOUNT_ASIA&#39;. <br> **Beispiel**: Erntedankverkauf |

**Referenz zur Rohbewertung (aggregiert)**

Die nachstehende Tabelle ordnet die aggregierten Werte den Rohbewertungen zu. Wenn Sie Ihre Rohbewertungen herunterladen möchten, besuchen Sie die Dokumentation [Herunterladen von Bewertungen in Attribution AI](./download-scores.md) . Um die Rohwertpfade in der Benutzeroberfläche anzuzeigen, besuchen Sie den Abschnitt [Anzeigen von Rohwertpfaden](#raw-score-path) in diesem Dokument.

| Spaltenname | Rohbewertungs-Referenzspalte |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| Segment | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| Touchpoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| product | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| geo | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| Aktion | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |


## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten vorbereitet haben und alle Ihre Anmeldedaten und Schemas vorhanden sind, folgen Sie dem [Attribution AI-Benutzerhandbuch](./user-guide.md). Dieses Handbuch führt Sie durch die Erstellung einer Instanz für Attribution AI.
