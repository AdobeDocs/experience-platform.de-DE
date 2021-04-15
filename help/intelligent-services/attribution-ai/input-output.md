---
keywords: Experience Platform;Erste Schritte;Attribution-ai;beliebte Themen;Attribution-ai-Eingabe;Attribution-ai-Ausgabe;
solution: Experience Platform, Intelligent Services
title: Eingabe und Ausgabe in Attribution AI
topic: Eingabe- und Ausgangsdaten für Attribution AI
description: Im folgenden Dokument werden die verschiedenen Ein- und Ausgänge erläutert, die in Attribution AI verwendet werden.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
translation-type: tm+mt
source-git-commit: 2ef2a6431865e8ffdc2abd6cf527249e8b5ca4d0
workflow-type: tm+mt
source-wordcount: '2098'
ht-degree: 4%

---

# Eingabe und Ausgabe in [!DNL Attribution AI]

Im folgenden Dokument werden die verschiedenen Eingabe- und Ausgabedaten umrissen, die in [!DNL Attribution AI] verwendet werden.

## [!DNL Attribution AI] Eingabedaten

[!DNL Attribution AI] verwendet  [!DNL Consumer Experience Event] Daten, um algorithmische Ergebnisse zu berechnen. Weitere Informationen zu [!DNL Consumer Experience Event] finden Sie unter [Daten für die Verwendung in der Intelligent Services-Dokumentation ](../data-preparation.md) vorbereiten.

Nicht alle Spalten im Schema [!DNL Consumer Experience Event] (CEE) sind für Attribution AIS obligatorisch.

>[!NOTE]
>
> Die folgenden 9 Spalten sind obligatorisch, zusätzliche Spalten sind optional, werden jedoch empfohlen/erforderlich, wenn Sie dieselben Daten für andere Adoben wie [!DNL Customer AI] und [!DNL Journey AI] verwenden möchten.

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
| Handel | Konversion  |

Normalerweise wird die Zuordnung auf Konvertierungsspalten wie Bestellung, Einkäufe und Kassengänge unter &quot;commerce&quot;ausgeführt. Die Spalten &quot;Kanal&quot;und &quot;Marketing&quot;werden dringend empfohlen, Touchpoints für gute Einblicke zu definieren. Sie können jedoch jede weitere Spalte zusammen mit den oben genannten Spalten einschließen, um sie als Konversions- oder Touchpoint-Definition zu konfigurieren.

Die folgenden Spalten sind nicht erforderlich, es wird jedoch empfohlen, sie in Ihr CEE-Schema einzubeziehen, wenn die verfügbaren Informationen vorliegen.

**Zusätzliche empfohlene Spalten:**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### Historische Daten {#data-requirements}

>[!IMPORTANT]
>
> Die Mindestdatenmenge, die erforderlich ist, damit Attribution AI funktionieren kann, lautet wie folgt:
> - Sie müssen Daten für mindestens 3 Monate (90 Tage) bereitstellen, um ein gutes Modell auszuführen.
> - Sie benötigen mindestens 1000 Konvertierungen.


Attribution AI erfordert historische Daten als Eingabe für Modellschulungen. Die erforderliche Datendauer wird hauptsächlich von zwei Hauptfaktoren bestimmt: Schulungsfenster und Lookback-Fenster. Die Eingabe mit kürzeren Schulungsfenstern ist anfälliger für aktuelle Trends, während längere Schulungsfenster stabilere und genauere Modelle erzeugen. Es ist wichtig, das Ziel mit historischen Daten zu modellieren, die Ihre Geschäftsziele am besten widerspiegeln.

Die [Schulungsfenster-Konfiguration](./user-guide.md#training-window) Filter-Konvertierungseinstellungen, die für die Modellschulung auf der Grundlage der Ereigniszeit festgelegt sind. Derzeit beträgt das Schulungsfenster mindestens 1 Quartal (90 Tage). Das [Lookback-Fenster](./user-guide.md#lookback-window) bietet einen Zeitraum, der angibt, wie viele Tage vor dem Konversions-Ereignis-Touchpoints im Zusammenhang mit diesem Konversions-Ereignis eingeschlossen werden sollen. Diese beiden Konzepte bestimmen zusammen die Menge der Eingabedaten (gemessen nach Tagen), die für eine Anwendung erforderlich sind.

Standardmäßig definiert Attribution AI das Schulungsfenster als die letzten 2 Quartale (6 Monate) und das Lookback-Fenster als 56 Tage. Anders ausgedrückt, berücksichtigt das Modell alle definierten Konvertierungsmodelle, die in den letzten zwei Quartalen aufgetreten sind, und sucht nach allen Touchpoints, die innerhalb von 56 Tagen vor dem/den zugehörigen Konversions-Ereignissen aufgetreten sind.

**Formel**:

Erforderliche Mindestlänge der Daten = Schulungsfenster + Lookback-Fenster

>[!TIP]
>
> Die Mindestdatenlänge, die für eine Anwendung mit Standardkonfigurationen erforderlich ist, ist: 2 Quartale (180 Tage) + 56 Tage = 236 Tage.

Beispiel :

- Sie möchten Umrechnungs-Ereignis zuordnen, die innerhalb der letzten 90 Tage (3 Monate) aufgetreten sind, und alle Touchpoints verfolgen, die innerhalb von 4 Wochen vor dem Konversions-Ereignis aufgetreten sind. Die Dauer der Eingabedaten sollte sich über die letzten 90 Tage + 28 Tage (4 Wochen) erstrecken. Das Schulungsfenster beträgt 90 Tage und das Lookback-Fenster insgesamt 118 Tage.

## Attribution AI-Ausgabedaten

Attribution AI gibt Folgendes aus:

- [Rohe granulare Punktzahlen](#raw-granular-scores)
- [Aggregierte Ergebnisse](#aggregated-attribution-scores)

**Schema der Ausgabe:**

![](./images/input-output/schema_output.gif)

### Rohe granulare Punktzahlen {#raw-granular-scores}

Attribution AI gibt Zuordnungswerte auf möglichst granularer Ebene aus, sodass Sie die Ergebnisse nach jeder beliebigen Ergebnisspalte ausschneiden und würfeln können. Um diese Werte in der Benutzeroberfläche Ansicht, lesen Sie den Abschnitt [Anzeigen von Rohwertpfaden](#raw-score-path). Um die Punktzahlen mit der API herunterzuladen, besuchen Sie das Dokument [Herunterladen von Punktzahlen in Attribution AI](./download-scores.md).

>[!NOTE]
>
> Sie können alle gewünschten Berichte-Spalten aus dem Eingabedataset im Ergebnisausgabe-Datensatz nur dann anzeigen, wenn einer der folgenden Werte wahr ist:
> - Die Spalte &quot;Berichte&quot;wird auf der Konfigurationsseite entweder als Teil der Touchpoint- oder Konvertierungsdefinitionskonfiguration aufgeführt.
> - Die Spalte &quot;Berichte&quot;ist in den Spalten mit zusätzlichen Ergebnisdatensätzen enthalten.


Die folgende Tabelle zeigt die Schema-Felder in der Rohwertbeispiel-Ausgabe:

| Spaltenname (DataType) | Nullable | Beschreibung |
| --- | --- | --- |
| timestamp (DateTime) | False | Der Zeitpunkt, zu dem ein Konversions-Ereignis oder eine Beobachtung aufgetreten ist. <br> **Beispiel:** 2020-06-09T00:01:51.000Z |
| identityMap (Map) | True | identityMap des Benutzers ähnlich dem CEE XDM-Format. |
| eventType (String) | true | Der primäre Ereignistyp für diesen Zeitreihendatensatz. <br> **Beispiel:** &quot;Bestellung&quot;, &quot;Kauf&quot;, &quot;Besuch&quot; |
| eventMergeId (String) | true | Eine ID, die mehrere [!DNL Experience Events] miteinander korreliert oder zusammenführt, die im Wesentlichen dasselbe Ereignis sind oder zusammengeführt werden sollten. Dieser soll vor der Aufnahme vom Datenhersteller ausgefüllt werden. <br> **Beispiel:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (Zeichenfolge) | False | Eine eindeutige Kennung für das Ereignis der Zeitreihen. <br> **Beispiel:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (Objekt) | False | Der Container des Objekts auf oberster Ebene, der Ihrer Tent-ID entspricht. <br> **Beispiel:** _atsdsnrmmsv2 |
| your_Schema_name (Objekt) | False | Ergebniszeile mit Konversions-Ereignis mit allen damit verknüpften Touchpoint-Ereignissen und deren Metadaten. <br> **Beispiel:** Attribution AI Scores - Modellname__2020 |
| segmentation (Zeichenfolge) | true | Konversionssegment wie die Geo-Segmentierung, auf dem das Modell basiert. Wenn keine Segmente vorhanden sind, ist das Segment mit dem von convertName identisch. <br> **Beispiel:** ORDER_US |
| convertName (String) | true | Name der Konvertierung, die während der Einrichtung konfiguriert wurde. <br> **Beispiel:** Bestellung, Interessent, Besuch |
| Konversion (Objekt) | False | Konvertierungsmetadatenspalten. |
| dataSource (String) | true | Globale eindeutige Identifizierung einer Datenquelle. <br> **Beispiel:** Adobe Analytics |
| eventSource (String) | true | Die Quelle, an der das eigentliche Ereignis aufgetreten ist. <br> **Beispiel:** Adobe.com |
| eventType (String) | true | Der primäre Ereignistyp für diesen Zeitreihendatensatz. <br> **Beispiel:** Reihenfolge |
| geo (Zeichenfolge) | true | Der geografische Ort, an dem die Konvertierung bereitgestellt wurde `placeContext.geo.countryCode`. <br> **Beispiel:** US |
| priceTotal (Dublette) | true | Durch die Umrechnung erzielter Umsatz <br> **Beispiel:** 99.9 |
| product (Zeichenfolge) | true | Die XDM-ID des Produkts. <br> **Beispiel:** RX 1080 ti |
| productType (Zeichenfolge) | true | Der Anzeigename für das Produkt, der dem Benutzer für diese Ansicht angezeigt wird. <br> **Beispiel:** GPUS |
| quantity (Integer) | true | Während der Konvertierung gekaufte Menge <br> **Beispiel:** 1 1080 ti |
| receiveTimestamp (DateTime) | true | Zeitstempel der Konvertierung erhalten. <br> **Beispiel:** 2020-06-09T00:01:51.000Z |
| skuId (Zeichenfolge) | true | Bestandsabwicklungseinheit (SKU), die eindeutige Kennung für ein vom Anbieter definiertes Produkt. <br> **Beispiel:** MJ-03-XS-Black |
| timestamp (DateTime) | true | Zeitstempel der Konversion. <br> **Beispiel:** 2020-06-09T00:01:51.000Z |
| passThrough (Objekt) | true | Zusätzliche Score-Datenset-Spalten, die vom Benutzer beim Konfigurieren des Modells angegeben werden. |
| commerce_order_purchaseCity (Zeichenfolge) | true | Zusätzliche Datensatzspalte für die Punktzahl. <br> **Beispiel:** city: San Jose |
| customerProfile (Objekt) | False | Identitätsdetails des Benutzers, der zum Erstellen des Modells verwendet wird. |
| identity (Objekt) | False | Enthält die Details des Benutzers, der zum Erstellen des Modells verwendet wird, z. B. `id` und `namespace`. |
| id (Zeichenfolge) | true | Identitäts-ID des Benutzers, z. B. Cookie-ID oder AAID oder MCID usw. <br> **Beispiel:** 17348762725408656344688320891369597404 |
| Namensraum (Zeichenfolge) | true | Identitäts-Namensraum, der zum Erstellen der Pfade und damit des Modells verwendet wird. <br> **Beispiel:** aid |
| touchpointsDetail (Object-Array) | true | Die Liste der Touchpoint-Details, die zur nach Touchpoint-Vorkommen oder Zeitstempel sortierten Konvertierung führen. |
| touchpointName (Zeichenfolge) | true | Name des Touchpoints, der während der Einrichtung konfiguriert wurde. <br> **Beispiel:** PAID_SEARCH_CLICK |
| scores (Objekt) | true | Touchpoint-Beitrag zu dieser Konversion als Ergebnis. Weitere Informationen zu den in diesem Objekt erzeugten Ergebnissen finden Sie im Abschnitt [Aggregierte Zuordnungswerte](#aggregated-attribution-scores). |
| touchPoint (Objekt) | true | Touchpoint-Metadaten. Weitere Informationen zu den in diesem Objekt erzeugten Ergebnissen finden Sie im Abschnitt [Aggregierte Werte](#aggregated-scores). |

### Anzeigen von Rohwertpfaden (UI) {#raw-score-path}

Sie können den Pfad zu Ihren Rohwerten in der Benutzeroberfläche Ansicht haben. Beginn durch Auswahl von **[!UICONTROL Schema]** in der Plattform-Benutzeroberfläche suchen und wählen Sie dann Ihr Schema für die Zuordnungs-AI-Ergebnisse aus der Registerkarte **[!UICONTROL Durchsuchen]**.

![Schema auswählen](./images/input-output/schemas_browse.png)

Wählen Sie als Nächstes ein Feld im Fenster **[!UICONTROL Struktur]** der Benutzeroberfläche aus. Die Registerkarte **[!UICONTROL Feldeigenschaften]** wird geöffnet. Innerhalb von **[!UICONTROL Feldeigenschaften]** ist das Pfadfeld, das Ihren Rohwerten zugeordnet ist.

![Schema auswählen](./images/input-output/field_properties.png)


### Aggregierte Zuordnungswerte {#aggregated-attribution-scores}

Aggregierte Punktzahlen können im CSV-Format von der Plattform-Benutzeroberfläche heruntergeladen werden, wenn der Datumsbereich weniger als 30 Tage beträgt.

Attribution AI unterstützt zwei Kategorien von Zuordnungswerten, algorithmische und regelbasierte Werte.

Attribution AI produziert zwei verschiedene Arten von algorithmischen Ergebnissen, inkrementell und beeinflusst. Ein beeinflusster Wert ist der Anteil der Konversion, für die jeder Marketing-Touchpoint verantwortlich ist. Ein inkrementelles Ergebnis ist der Betrag der direkt durch den Marketing-Touchpoint verursachten marginalen Auswirkungen. Der Hauptunterschied zwischen dem inkrementellen Ergebnis und dem beeinflussten Ergebnis besteht darin, dass das inkrementelle Ergebnis den Basiseffekt berücksichtigt. Es wird nicht davon ausgegangen, dass eine Konversion ausschließlich durch die vorherigen Marketing-Touchpoints verursacht wird.

Im Folgenden finden Sie ein Beispiel für die Ausgabe eines Attribution AI-Schemas in der Adobe Experience Platform-Benutzeroberfläche:

![](./images/input-output/schema_screenshot.png)

Die nachstehende Tabelle enthält weitere Details zu den einzelnen Zuordnungswerten:

| Zuordnungswerte | Beschreibung |
| ----- | ----------- |
| Beeinflusst (algorithmisch) | Einflussreiches Ergebnis ist der Anteil der Konversion, für den jeder Marketing-Touchpoint verantwortlich ist. |
| Inkrementell (algorithmisch) | Inkrementelles Ergebnis ist die Höhe des Grenzeffekts, der direkt durch einen Marketing-Touchpoint verursacht wird. |
| Erstkontakt | Regelbasiertes Zuordnungsergebnis, das dem ursprünglichen Touchpoint auf einem Konversionspfad alle Gutschriften zuweist. |
| Letztkontakt | Regelbasierter Zuordnungswert, der dem Touchpoint die Gutschrift zuweist, der der Konversion am nächsten kommt. |
| Linear | Regelbasiertes Zuordnungsergebnis, das jedem Touchpoint auf einem Konversionspfad die gleiche Gutschrift zuweist. |
| U-förmig | Regelbasiertes Zuordnungsergebnis, bei dem 40 % der Gutschrift dem ersten Touchpoint und 40 % der Gutschrift dem letzten Touchpoint zugeordnet werden, während die übrigen 20 % gleichmäßig auf die anderen Touchpoints aufgeteilt werden. |
| Zeitverfall | Regelbasierter Zuordnungswert, bei dem Touchpoints, die näher an der Konversion liegen, mehr gutgeschrieben werden als Touchpoints, die zeitlich weiter von der Konversion entfernt sind. |

**Referenz zur Rohbewertung (Zuordnungswerte)**

Die nachstehende Tabelle ordnet die Zuordnungswerte den Rohwerten zu. Wenn Sie Ihre Rohwerte herunterladen möchten, lesen Sie die Dokumentation [Download-Ergebnisse in Attribution AI](./download-scores.md).

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

Aggregierte Punktzahlen können im CSV-Format von der Plattform-Benutzeroberfläche heruntergeladen werden, wenn der Datumsbereich weniger als 30 Tage beträgt. Die nachstehende Tabelle enthält weitere Informationen zu den einzelnen Aggregat-Spalten.

| Spaltenname | Constraint | Nullable | Beschreibung |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Benutzerdefiniertes und festes Format | False | Ereignis des Kunden im Format JJJJ-MM-TT. <br> **Beispiel**: 2016-05-02 |
| mediatouchpoints_date (DateTime) | Benutzerdefiniertes und festes Format | true | Media Touchpoint Date im Format JJJJ-MM-TT <br> **Beispiel**: 2017-04-21 |
| segment (String) | Berechnet | False | Konversionssegment, z. B. Geo-Segmentierung, auf dem das Modell basiert. Wenn keine Segmente vorhanden sind, ist das Segment identisch mit dem Wert &quot;conversion_scope&quot;. <br> **Beispiel**: ORDER_AMER |
| convert_scope (Zeichenfolge) | Benutzerdefiniert | False | Name der vom Benutzer konfigurierten Konvertierung. <br> **Beispiel**: BESTELLUNG |
| touchpoint_scope (Zeichenfolge) | Benutzerdefiniert | true | Name des Touchpoints, wie vom Benutzer <br> konfiguriert **Beispiel**: PAID_SEARCH_CLICK |
| product (Zeichenfolge) | Benutzerdefiniert | true | Die XDM-ID des Produkts. <br> **Beispiel**: CC |
| product_type (Zeichenfolge) | Benutzerdefiniert | true | Der Anzeigename für das Produkt, der dem Benutzer für diese Ansicht angezeigt wird. <br> **Beispiel**: Gpus, Laptops |
| geo (Zeichenfolge) | Benutzerdefiniert | true | Der geografische Speicherort, an dem die Konvertierung bereitgestellt wurde (placeContext.geo.countryCode) <br> **Beispiel**: US |
| Ereignis_type (Zeichenfolge) | Benutzerdefiniert | true | Der primäre Ereignistyp für diesen Zeitreihendatensatz <br> **Beispiel**: Gebührenpflichtige Konversion |
| media_type (Zeichenfolge) | ENUM | False | Beschreibt, ob der Medientyp bezahlt, im Besitz oder verdient ist. <br> **Beispiel**: BEZAHLTE, EIGENTÜMER |
| Kanal (Zeichenfolge) | ENUM | False | Die `channel._type`-Eigenschaft, mit der eine grobe Klassifizierung von Kanälen mit ähnlichen Eigenschaften in [!DNL Consumer Experience Event] XDM bereitgestellt wird. <br> **Beispiel**: SUCHE |
| action (Zeichenfolge) | ENUM | False | Die `mediaAction`-Eigenschaft wird verwendet, um eine Art von Erlebnis-Ereignis-Medienaktion bereitzustellen. <br> **Beispiel**: KLICKEN |
| Kampagne_Gruppe (Zeichenfolge) | Benutzerdefiniert | true | Name der Kampagne, in der mehrere Kampagnen gruppiert sind, z. B. &quot;50%_DISCOUNT&quot;. <br> **Beispiel**: KOMMERZIELL |
| Kampagne_name (Zeichenfolge) | Benutzerdefiniert | true | Name der Kampagne, die zur Identifizierung der Marketing-Kampagne verwendet wird, z. B. &#39;50%_DISCOUNT_USA&#39; oder &#39;50%_DISCOUNT_ASIA&#39;. <br> **Beispiel**: Erntedankverkauf |

**Referenz zur Rohbewertung (aggregiert)**

Die nachstehende Tabelle ordnet die aggregierten Ergebnisse den Rohwerten zu. Wenn Sie Ihre Rohwerte herunterladen möchten, lesen Sie die Dokumentation [Download-Ergebnisse in Attribution AI](./download-scores.md). Um die Rohwertpfade aus der Benutzeroberfläche Ansicht, besuchen Sie den Abschnitt [Rohwertpfade](#raw-score-path) in diesem Dokument.

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
| Ereignis_type | eventType |
| media_type | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| Aktion | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| Kampagne_group | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| Kampagne_name | _tenantID.your_Schema_name.touchpointsDetail.element.touchpoint.campaignName |


## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten vorbereitet haben und alle Ihre Anmeldedaten und Schema vorhanden sind, führen Sie den Beginn im [Attribution AI Benutzerhandbuch](./user-guide.md) durch. Dieser Leitfaden führt Sie durch das Erstellen einer Instanz für Attribution AI.
