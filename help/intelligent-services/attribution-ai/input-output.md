---
keywords: Experience Platform;Erste Schritte;Attributions-KI;beliebte Themen;Attributions-KI-Eingabe;Attributions-KI-Ausgabe;
feature: Attribution AI
title: Eingabe und Ausgabe in Attribution AI
description: Im folgenden Dokument werden die verschiedenen Eingaben und Ausgaben beschrieben, die in Attribution AI verwendet werden.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '2467'
ht-degree: 5%

---

# Ein- und Ausgabe in [!DNL Attribution AI]

Im folgenden Dokument werden die verschiedenen Eingaben und Ausgaben beschrieben, die in [!DNL Attribution AI] verwendet werden.

## [!DNL Attribution AI] Eingabedaten

Attribution AI analysiert die folgenden Datensätze, um algorithmische Scores zu berechnen:

- Adobe Analytics-Datensätze unter Verwendung des [Analytics-Quell-Connectors](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Datensätze von Erlebnisereignissen (EE) im Allgemeinen aus dem Adobe Experience Platform-Schema
- Datensätze für Customer Experience Events (CEE)

Sie können jetzt mehrere Datensätze aus verschiedenen Quellen hinzufügen, die auf der **Identitätszuordnung** (Feld) basieren, wenn jeder Datensatz denselben Identitätstyp (Namespace), z. B. eine ECID, aufweist. Nachdem Sie eine Identität und einen Namespace-ID ausgewählt haben, werden Metriken zur Vollständigkeit der Spalte angezeigt, die das Volumen der zuzuordnenden Daten angeben. Weitere Informationen zum Hinzufügen mehrerer Datensätze finden Sie im [Attribution AI-Benutzerhandbuch](./user-guide.md#identity).

Die Kanalinformationen werden nicht immer standardmäßig zugeordnet. In einigen Fällen können Sie, wenn das Feld mediaChannel (leer) leer ist, erst dann „fortfahren“, wenn Sie ein Feld dem mediaChannel zuordnen, da es sich um eine erforderliche Spalte handelt. Wenn der Kanal im Datensatz erkannt wird, wird er standardmäßig mediaChannel zugeordnet. Die anderen Spalten wie **Medientyp** und **Medienaktion** sind weiterhin optional.

Nachdem Sie das Kanalfeld zugeordnet haben, fahren Sie mit dem Schritt „Ereignisse definieren“ fort, in dem Sie Konversionsereignisse und Touchpoint-Ereignisse auswählen und bestimmte Felder aus einzelnen Datensätzen auswählen können.

>[!IMPORTANT]
>
>Die Aufstockung von Daten durch den Adobe Analytics-Quell-Connector kann bis zu vier Wochen dauern. Wenn Sie kürzlich einen Connector eingerichtet haben, sollten Sie sicherstellen, dass der Datensatz die für Attribution AI erforderliche Mindestlänge von Daten aufweist. Lesen Sie den Abschnitt [Verlaufsdaten](#data-requirements), um sich zu vergewissern, dass Sie über genügend Daten verfügen, um genaue algorithmische Scores zu berechnen.

Weitere Informationen zum Einrichten des [!DNL Consumer Experience Event]-Schemas (CEE) finden Sie im Handbuch [Intelligent Services-](../data-preparation.md)). Weitere Informationen zum Zuordnen von Adobe Analytics-Daten finden Sie in der [Analytics-Feldzuordnungen](../../sources/connectors/adobe-applications/analytics.md).

Nicht alle Spalten im [!DNL Consumer Experience Event] (CEE)-Schema sind für Attribution AI obligatorisch.

Sie können die Touchpoints mithilfe der unten empfohlenen Felder im Schema oder im ausgewählten Datensatz konfigurieren.

| Empfohlene Spalten | Erforderlich für |
| --- | --- |
| Primäres Identitätsfeld | Touchpoint/Konversion |
| Zeitstempel | Touchpoint/Konversion |
| Kanal._type | Kontaktpunkt |
| Channel.mediaAction | Kontaktpunkt |
| Channel.mediaType | Kontaktpunkt |
| Marketing.trackingCode | Kontaktpunkt |
| Marketing.campaignname | Kontaktpunkt |
| Marketing.campaigngroup | Kontaktpunkt |
| Commerce | Konversion |

Normalerweise wird die Attribution in Konversionsspalten wie Bestellung, Käufe und Checkouts unter „Commerce“ ausgeführt. Die Spalten für „Kanal“ und „Marketing“ werden verwendet, um Touchpoints für Attribution AI zu definieren (z. B. `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). Für optimale Ergebnisse und Einblicke wird dringend empfohlen, so viele Konversions- und Touchpoint-Spalten wie möglich einzubeziehen. Darüber hinaus sind Sie nicht auf die obigen Spalten beschränkt. Sie können jede andere empfohlene oder benutzerdefinierte Spalte als Konversions- oder Touchpoint-Definition einbeziehen.

Erlebnisereignis (EE)-Datensätze müssen nicht explizit Kanal- und Marketing-Mixins enthalten, solange die für die Konfiguration eines Touchpoints relevanten Kanal- oder Kampagneninformationen in einem der Mixin- oder Pass-Through-Felder vorhanden sind.

>[!TIP]
>
>Wenn Sie Adobe Analytics-Daten in Ihrem CEE-Schema verwenden, werden die Touchpoint-Informationen für Analytics normalerweise in `channel.typeAtSource` gespeichert (z. B. `channel.typeAtSource = 'email'`).

## Historische Daten {#data-requirements}

>[!IMPORTANT]
>
> Die Mindestmenge an Daten, die für das Funktionieren des Attribution AIS erforderlich ist, beträgt:
> - Sie müssen mindestens 3 Monate (90 Tage) an Daten bereitstellen, um ein gutes Modell auszuführen.
> - Sie benötigen mindestens 1000 Konversionen.

Attribution AI benötigt historische Daten als Eingabe für das Modell-Training. Die benötigte Datendauer wird hauptsächlich durch zwei Schlüsselfaktoren bestimmt: Trainings-Fenster und Lookback-Fenster. Eingaben mit kürzeren Trainings-Fenstern reagieren stärker auf aktuelle Trends, während längere Trainings-Fenster dazu beitragen, stabilere und genauere Modelle zu erstellen. Es ist wichtig, das Ziel mit historischen Daten zu modellieren, die Ihre Geschäftsziele am besten widerspiegeln.

Die [Konfiguration des Trainingsfensters](./user-guide.md#training-window) filtert Konversionsereignisse, die für das Modell-Training einbezogen werden sollen, basierend auf der Intervallzeit. Derzeit ist das Mindestfenster für Schulungen 1 Quartal (90 Tage). Das [Lookback-Fenster](./user-guide.md#lookback-window) stellt einen Zeitrahmen bereit, der angibt, wie viele Tage vor dem Konversionsereignis-Touchpoints, die mit diesem Konversionsereignis verbunden sind, eingeschlossen werden sollen. Diese beiden Konzepte zusammen bestimmen die Menge der Eingabedaten (gemessen durch Tage), die für eine Anwendung erforderlich ist.

Standardmäßig definiert Attribution AI das Schulungsfenster als die letzten 2 Quartale (6 Monate) und das Lookback-Fenster als 56 Tage. Mit anderen Worten, das Modell berücksichtigt alle definierten Konversionsereignisse, die in den letzten 2 Quartalen aufgetreten sind, und sucht nach allen Touchpoints, die innerhalb von 56 Tagen vor dem/den zugehörigen Konversionsereignis(sen) aufgetreten sind.

**Formel**:

Erforderliche Mindestlänge der Daten = Trainings-Fenster + Lookback-Fenster

>[!TIP]
>
> Für eine Anwendung mit Standardkonfigurationen sind mindestens zwei Quartale (180 Tage) + 56 Tage = 236 Tage erforderlich.

Beispiel:

- Sie möchten Konversionsereignisse zuordnen, die in den letzten 90 Tagen (3 Monaten) stattgefunden haben, und alle Touchpoints verfolgen, die innerhalb von 4 Wochen vor dem Konversionsereignis aufgetreten sind. Die Dauer der Eingabedaten sollte sich über die letzten 90 Tage + 28 Tage (4 Wochen) erstrecken. Das Trainings-Fenster beträgt 90 Tage und das Lookback-Fenster 28 Tage mit insgesamt 118 Tagen.

## Attribution AI-Ausgabedaten

Attribution AI gibt Folgendes aus:

- [Granulare Rohwerte](#raw-granular-scores)
- [Aggregierte Scores](#aggregated-attribution-scores)

**Beispiel für Ausgabeschema:**

![](./images/input-output/schema_output.gif)

### Granulare Rohwerte {#raw-granular-scores}

Attribution AI gibt Attributionsbewertungen auf der detailliertesten Ebene aus, sodass Sie die Bewertungen in beliebige Punktspalten aufteilen können. Um diese Bewertungen in der Benutzeroberfläche anzuzeigen, lesen Sie den Abschnitt unter [Anzeigen von Rohwertpfaden](#raw-score-path). Informationen zum Herunterladen der Scores über die API finden Sie [ Dokument „Scores in Attribution AI herunterladen](./download-scores.md).

>[!NOTE]
>
> Sie können jede gewünschte Berichtsspalte aus dem Eingabedatensatz im Score-Ausgabedatensatz nur sehen, wenn eine der folgenden Bedingungen zutrifft:
> - Die Berichtsspalte ist auf der Konfigurationsseite entweder als Teil der Touchpoint- oder Konversionsdefinitionskonfiguration enthalten.
> - Die Berichtsspalte ist in zusätzlichen Bewertungs-Datensatzspalten enthalten.

In der folgenden Tabelle sind die Schemafelder in der Beispielausgabe „Rohbewertungen“ aufgeführt:

| Spaltenname (dataType) | nullable | Beschreibung |
| --- | --- | --- |
| Zeitstempel (DateTime) | False | Der Zeitpunkt, zu dem ein Konversionsereignis oder eine Beobachtung aufgetreten ist. <br> **Beispiel:** 2020-06-09T00:01:51.000Z |
| identityMap (Zuordnung) | True | identityMap des Benutzers ähnlich dem CEE-XDM-Format. |
| eventType (Zeichenfolge) | True | Der primäre Ereignistyp für diesen Zeitreiheneintrag. <br> **Beispiel:** „Bestellung“, „Kauf“, „Besuch“ |
| eventMergeId (Zeichenfolge) | True | Eine ID, um mehrere [!DNL Experience Events] miteinander zu korrelieren oder zusammenzuführen, die im Wesentlichen dasselbe Ereignis sind oder zusammengeführt werden sollen. Dies sollte vom Datenproduzenten vor der Aufnahme ausgefüllt werden. <br> **Beispiel:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (String) | False | Eine eindeutige Kennung für das Zeitreihenereignis. <br> **Beispiel:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (Objekt) | False | Der Objektcontainer der obersten Ebene, der Ihrer Mandanten-ID entspricht. <br> **Beispiel:** _atsdsnrmmsv2 |
| your_schema_name (Objekt) | False | Bewerten Sie die Zeile mit dem Konversionsereignis und allen damit verbundenen Touchpoint-Ereignissen sowie deren Metadaten. <br> **Beispiel:** Attribution AI Scores - Modellname__2020 |
| Segmentierung (Zeichenfolge) | True | Konversionssegmente wie die Geosegmentierung, anhand derer das Modell erstellt wird. Wenn keine Segmente vorhanden sind, ist das Segment dasselbe wie conversionName. <br> **Beispiel:** ORDER_US |
| conversionName (String) | True | Name der Konvertierung, die beim Setup konfiguriert wurde. <br> **Beispiel:**, Lead, Besuch |
| Konversion (Objekt) | False | Konversionsmetadaten-Spalten. |
| dataSource (Zeichenfolge) | True | Globale eindeutige Identifizierung einer Datenquelle. <br> **Beispiel:** Adobe Analytics |
| eventSource (Zeichenfolge) | True | Die Quelle, an der das tatsächliche Ereignis aufgetreten ist. <br> **Beispiel:** Adobe.com |
| eventType (Zeichenfolge) | True | Der primäre Ereignistyp für diesen Zeitreiheneintrag. <br> **example:** order |
| geo (Zeichenfolge) | True | Der geografische Ort, an dem die Konversion bereitgestellt wurde, `placeContext.geo.countryCode`. <br> **Beispiel:** US |
| priceTotal (Doppelt) | True | Durch die <br> erzielter Umsatz **Beispiel:** 99.9 |
| product (Zeichenfolge) | True | Die XDM-Kennung des Produkts selbst. <br> **Beispiel:** RX 1080 ti |
| productType (Zeichenfolge) | True | Der Anzeigename für das Produkt, wie er dem Benutzer für diese Produktansicht präsentiert wird. <br> **Beispiel:** GPUs |
| Menge (Ganzzahl) | True | Bei der Konversion gekaufte Menge <br> **Beispiel:** 1 1080 ti |
| receivedTimestamp (DateTime) | True | Zeitstempel der Konversion empfangen. <br> **Beispiel:** 2020-06-09T00:01:51.000Z |
| skuId (Zeichenfolge) | True | Lagerhaltungseinheit (SKU), die eindeutige Kennung für ein vom Anbieter definiertes Produkt. <br> **Beispiel:** MJ-03-XS-Black |
| Zeitstempel (DateTime) | True | Zeitstempel der Konversion. <br> **Beispiel:** 2020-06-09T00:01:51.000Z |
| passThrough (Objekt) | True | Zusätzliche Bewertungs-Datensatzspalten, die vom Benutzer beim Konfigurieren des Modells angegeben wurden. |
| commerce_order_purchaseCity (Zeichenfolge) | True | Zusätzliche Bewertungs-Datensatzspalte. <br> **Beispiel:** Stadt: San Jose |
| customerProfile (Objekt) | False | Identitätsdetails des Benutzers, der zum Erstellen des Modells verwendet wurde. |
| Identität (Objekt) | False | Enthält die Details des Benutzers, der zum Erstellen des Modells verwendet wird, z. B. `id` und `namespace`. |
| id (String) | True | Identitäts-ID des Benutzers wie Cookie-ID, Adobe Analytics-ID (AAID) oder Experience Cloud-ID (ECID, auch als ECID oder als Besucher-ID bezeichnet) usw. <br> **Beispiel:** 17348762725408656344688320891369597404 |
| namespace (String) | True | Identitäts-Namespace zum Erstellen der Pfade und somit des Modells <br> **Beispiel:** aaid |
| TouchpointsDetail (Objekt-Array) | True | Die Liste der Touchpoint-Details, die zur Konversion führen, sortiert nach | Touchpoint-Vorkommen oder Zeitstempel. |
| TouchpointName (Zeichenfolge) | True | Name des Touchpoints, der bei der Einrichtung konfiguriert wurde. <br> **Beispiel:** PAID_SEARCH_CLICK |
| Scores (Objekt) | True | Touchpoint-Beitrag zu dieser Konversion als Score. Weitere Informationen zu den in diesem Objekt erzielten Scores finden Sie im Abschnitt [aggregierte ](#aggregated-attribution-scores)). |
| TouchPoint (Objekt) | True | Touchpoint-Metadaten. Weitere Informationen zu den in diesem Objekt erzielten Scores finden Sie im Abschnitt [aggregierte Scores](#aggregated-scores). |

### Anzeigen von Rohwertpfaden (Benutzeroberfläche) {#raw-score-path}

Sie können den Pfad zu Ihren Rohwertungen in der Benutzeroberfläche anzeigen. Wählen Sie zunächst **[!UICONTROL Schemas]** in der Platform-Benutzeroberfläche aus und suchen Sie dann auf der Registerkarte **[!UICONTROL Durchsuchen]** nach Ihrem Schema für Attributions-KI-Bewertungen.

![Wählen Sie Ihr Schema](./images/input-output/schemas_browse.png)

Wählen Sie anschließend ein Feld im Fenster **[!UICONTROL Struktur]** der Benutzeroberfläche aus. Die Registerkarte **[!UICONTROL Feldeigenschaften]** wird geöffnet. In **[!UICONTROL Feldeigenschaften]** ist das Pfadfeld, das Ihren Rohwertungen zugeordnet ist.

![Schema auswählen](./images/input-output/field_properties.png)

### Aggregierte Attributionsbewertungen {#aggregated-attribution-scores}

Aggregierte Scores können über die Platform-Benutzeroberfläche im CSV-Format heruntergeladen werden, wenn der Datumsbereich weniger als 30 Tage beträgt.

Attribution AI unterstützt zwei Kategorien von Attributionsbewertungen: algorithmische und regelbasierte.

Attribution AI erzeugt zwei verschiedene Arten von algorithmischen Scores, inkrementelle und beeinflusste. Ein beeinflusster Wert ist der Anteil der Konversion, für den jeder Marketing-Touchpoint verantwortlich ist. Ein inkrementeller Score ist der Betrag der marginalen Auswirkungen, die direkt durch den Marketing-Touchpoint verursacht werden. Der Hauptunterschied zwischen dem inkrementellen Score und dem beeinflussten Score besteht darin, dass der inkrementelle Score den Basiseffekt berücksichtigt. Es wird nicht davon ausgegangen, dass eine Konversion allein durch die vorangehenden Marketing-Touchpoints verursacht wird.

Im Folgenden finden Sie einen kurzen Blick auf ein Beispiel einer Attribution AI-Schemaausgabe in der Adobe Experience Platform-Benutzeroberfläche:

![](./images/input-output/schema_screenshot.png)

Weitere Informationen zu den einzelnen Attributionsbewertungen finden Sie in der folgenden Tabelle:

| Attributionsbewertungen | Beschreibung |
| ----- | ----------- |
| Beeinflusst (algorithmisch) | Der beeinflusste Score ist der Anteil der Konversion, für den jeder Marketing-Touchpoint verantwortlich ist. |
| Inkrementell (algorithmisch) | Der inkrementelle Score ist der Betrag der marginalen Auswirkungen, die direkt durch einen Marketing-Touchpoint verursacht werden. |
| Erstkontakt | Regelbasierter Attributionswert, der alle Credits dem ersten Touchpoint auf einem Konversionspfad zuweist. |
| Letztkontakt | Regelbasierte Attributionsbewertung, die den gesamten Wert dem Touchpoint zuweist, der der Konversion am nächsten ist. |
| Linear | Regelbasierter Attributionswert, der jedem Touchpoint auf einem Konversionspfad den gleichen Wert zuweist. |
| U-förmig | Regelbasierter Attributionswert, der 40 % des Werts dem ersten Touchpoint und 40 % dem letzten Touchpoint zuweist und die restlichen 20 % auf die anderen Touchpoints aufteilt. |
| Zeitabfall | Regelbasierter Attributionswert, bei dem Touchpoints, die näher an der Konversion liegen, mehr Credits erhalten als Touchpoints, die zeitlich weiter von der Konversion entfernt liegen. |

**Referenz zur Rohbewertung (Attributionsbewertungen)**

Die nachstehende Tabelle ordnet die Attributionsbewertungen den Rohbewertungen zu. Wenn Sie Ihre Rohdaten herunterladen möchten, lesen Sie die Dokumentation [Scores in Attribution AI herunterladen](./download-scores.md).

| Attributionsbewertungen | Referenzspalte der Rohbewertung |
| --- | --- |
| Beeinflusst (algorithmisch) | _tenantID.your_schema_name.element.touchpoint.algorithmicInfluected |
| Inkrementell (algorithmisch) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInfluected |
| Erstkontakt | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Letztkontakt | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Linear | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U-förmig | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| Zeitabfall | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Aggregierte Scores {#aggregated-scores}

Aggregierte Scores können über die Platform-Benutzeroberfläche im CSV-Format heruntergeladen werden, wenn der Datumsbereich weniger als 30 Tage beträgt. Weitere Informationen zu den einzelnen Aggregatspalten finden Sie in der nachstehenden Tabelle.

| Spaltenname | Beschränkung | nullable | Beschreibung |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Benutzerdefiniertes und festes Format | False | Kundenereignisdatum im Format JJJJ-MM-TT. <br> **Beispiel**: 02.05.2016 |
| mediaTouchpoints_date (DateTime) | Benutzerdefiniertes und festes Format | True | Medien-Touchpoint-Datum im Format JJJJ-MM-TT <br> **Beispiel**: 21.04.2017 |
| segment (String) | Berechnet | False | Konversionssegment, z. B. Geo-Segmentierung, für die das Modell erstellt wird. Wenn keine Segmente vorhanden sind, ist das Segment dasselbe wie conversion_scope. <br> **Beispiel**: ORDER_AMER |
| conversion_scope (Zeichenfolge) | Benutzerdefiniert | False | Name der Konversion, wie vom Benutzer konfiguriert. <br> **Beispiel**: BESTELLUNG |
| Touchpoint_scope (Zeichenfolge) | Benutzerdefiniert | True | Name des Touchpoints, wie vom Benutzer <br> konfiguriert **Beispiel**: PAID_SEARCH_CLICK |
| product (Zeichenfolge) | Benutzerdefiniert | True | Die XDM-Kennung des Produkts. <br> **Beispiel**: CC |
| product_type (Zeichenfolge) | Benutzerdefiniert | True | Der Anzeigename für das Produkt, wie er dem Benutzer für diese Produktansicht präsentiert wird. <br> **Beispiel**: Grafikprozessoren, Laptops |
| geo (Zeichenfolge) | Benutzerdefiniert | True | Der geografische Ort, an dem die Konversion bereitgestellt wurde (placeContext.geo.countryCode) <br> **Beispiel**: US |
| event_type (Zeichenfolge) | Benutzerdefiniert | True | Der primäre Ereignistyp für diese Zeitreihen-<br> **Beispiel**: Paid Conversion |
| media_type (Zeichenfolge) | AUFZÄHLUNG | False | Beschreibt, ob der Medientyp bezahlt, in Besitz oder verdient ist. <br> **Beispiel**: BEZAHLT, IN BESITZ |
| channel (String) | AUFZÄHLUNG | False | Die `channel._type` -Eigenschaft, die verwendet wird, um eine grobe Klassifizierung von Kanälen mit ähnlichen Eigenschaften in [!DNL Consumer Experience Event] XDM bereitzustellen<br> **Beispiel**: SUCHE |
| Aktion (Zeichenfolge) | AUFZÄHLUNG | False | Die `mediaAction`-Eigenschaft wird verwendet, um einen Typ von Medienaktion für Erlebnisereignisse bereitzustellen. <br> **Beispiel**: KLICKEN SIE AUF |
| campaign_group (Zeichenfolge) | Benutzerdefiniert | True | Name der Kampagnengruppe, in der mehrere Kampagnen gruppiert sind, z. B. „50%_DISCOUNT“. <br> **Beispiel**: KOMMERZIELL |
| campaign_name (Zeichenfolge) | Benutzerdefiniert | True | Name der Kampagne, der zur Identifizierung der Marketing-Kampagne verwendet wird, z. B. „50%_DISCOUNT_USA“ oder „50%_DISCOUNT_ASIA“. <br> **Beispiel**: Thanksgiving Sale |

**Referenz zur Rohbewertung (aggregiert)**

Die folgende Tabelle ordnet die aggregierten Scores den Rohbewertungen zu. Wenn Sie Ihre Rohdaten herunterladen möchten, lesen Sie die Dokumentation [Scores in Attribution AI herunterladen](./download-scores.md). Um die Pfade der Rohwertbewertung in der Benutzeroberfläche anzuzeigen, lesen Sie den Abschnitt [Anzeigen von Rohwertwertpfaden](#raw-score-path) in diesem Dokument.

| Spaltenname | Referenzspalte der Rohbewertung |
| --- | --- |
| customerevents_date | Zeitstempel |
| mediaTouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segmentieren | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| Touchpoint_Scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| Produkt | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| Geo | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| Aktion | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - Das Attribution AI verwendet nur aktualisierte Daten für die Fortbildung und Bewertung. Ebenso verzichtet Kunden-KI auf die Verwendung der gelöschten Daten, wenn Sie eine Löschung von Daten anfordern.
> - Die Attributions-KI nutzt Platform-Datensätze. Um Anfragen zu Verbraucherrechten zu unterstützen, die eine Marke erhalten kann, sollten Marken den Privacy Service von Platform nutzen, damit Privatkundinnen und -kunden Anfragen zum Zugriff und zur Löschung ihrer Daten über den Data Lake, den Identity Service und das Echtzeit-Kundenprofil stellen können.
> - Alle Datensätze, die wir für die Eingabe/Ausgabe von Modellen verwenden, folgen den Platform-Richtlinien. Die Platform-Datenverschlüsselung gilt für Daten in Ruhezeit und während der Übertragung. Weitere Informationen zur Datenverschlüsselung finden [ in der Dokumentation](../../../help/landing/governance-privacy-security/encryption.md)

## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten vorbereitet und alle Ihre Anmeldedaten und Schemata eingerichtet haben, folgen Sie zunächst dem [Attribution AI-Benutzerhandbuch](./user-guide.md). Dieses Handbuch führt Sie durch die Erstellung einer Instanz für Attribution AI.
