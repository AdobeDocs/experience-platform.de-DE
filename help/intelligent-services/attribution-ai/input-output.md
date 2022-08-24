---
keywords: Experience Platform; Erste Schritte; Attribution ai; beliebte Themen; Attribution AI-Eingabe; Attribution AI-Ausgabe;
feature: Attribution AI
title: Eingabe und Ausgabe in Attribution AI
topic-legacy: Input and Output data for Attribution AI
description: Im folgenden Dokument werden die verschiedenen Ein- und Ausgabedaten beschrieben, die in Attribution AI verwendet werden.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: b3c331821e2df17380edbc673066f6b10a06d65f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Eingabe und Ausgabe in [!DNL Attribution AI]

Im folgenden Dokument werden die verschiedenen in [!DNL Attribution AI].

## [!DNL Attribution AI] Eingabedaten

Attribution AI analysiert die folgenden Datensätze, um algorithmische Ergebnisse zu berechnen:

- Adobe Analytics-Datensätze, die die [Analytics-Quell-Connector](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Allgemeine Experience Event (EE)-Datensätze aus dem Adobe Experience Platform-Schema
- Datasets für Consumer Experience Event (CEE)

Sie können jetzt mehrere Datensätze aus verschiedenen Quellen hinzufügen, basierend auf der **Identitätszuordnung** (Feld), wenn jeder Datensatz denselben Identitätstyp (Namespace) wie eine ECID aufweist. Nachdem Sie eine Identität und einen Namespace ausgewählt haben, werden Metriken zur Vollständigkeit der ID-Spalte angezeigt, die das Volumen der zuzuordnenden Daten angeben. Weitere Informationen zum Hinzufügen mehrerer Datensätze finden Sie unter [Attribution AI-Benutzerhandbuch](./user-guide.md#identity).

Die Kanalinformationen werden nicht immer standardmäßig zugeordnet. Wenn der mediaChannel (Feld) in einigen Fällen leer ist, können Sie den Vorgang erst fortsetzen, wenn Sie ein Feld mediaChannel zuordnen, da es sich um eine erforderliche Spalte handelt. Wenn der Kanal im Datensatz erkannt wird, wird er standardmäßig mediaChannel zugeordnet. Die anderen Spalten, z. B. **Medientyp** und **Medienaktion** sind weiterhin optional.

Nachdem Sie das Kanalfeld zugeordnet haben, fahren Sie mit dem Schritt &quot;Ereignisse definieren&quot;fort, in dem Sie Konversionsereignisse und Touchpoint-Ereignisse auswählen und bestimmte Felder aus einzelnen Datensätzen auswählen können.

>[!IMPORTANT]
>
>Der Adobe Analytics-Quell-Connector kann bis zu vier Wochen dauern, bis Daten aufgestockt werden. Wenn Sie kürzlich einen Connector eingerichtet haben, sollten Sie sicherstellen, dass der Datensatz die für Attribution AI erforderliche Mindestlänge von Daten aufweist. Lesen Sie die [historische Daten](#data-requirements) -Abschnitt, um sicherzustellen, dass Sie über genügend Daten verfügen, um präzise algorithmische Ergebnisse zu berechnen.

Weitere Informationen zur Einrichtung der [!DNL Consumer Experience Event] Schema (CEE), siehe [Datenvorbereitung für Intelligent Services](../data-preparation.md) Handbuch. Weitere Informationen zum Zuordnen von Adobe Analytics-Daten finden Sie unter [Analytics-Feldzuordnungen](../../sources/connectors/adobe-applications/analytics.md) Dokumentation.

Nicht alle Spalten im [!DNL Consumer Experience Event] (CEE)-Schema ist für Attribution AI obligatorisch.

Sie können die Touchpoints mit allen unten empfohlenen Feldern im Schema oder im ausgewählten Datensatz konfigurieren.

| Empfohlene Spalten | Benötigt für |
| --- | --- |
| Primäres Identitätsfeld | Touchpoint/Konversion |
| Zeitstempel | Touchpoint/Konversion |
| Kanal._type | Touchpoint |
| Channel.mediaAction | Touchpoint |
| Channel.mediaType | Touchpoint |
| Marketing.trackingCode | Touchpoint |
| Marketing.campaignname | Touchpoint |
| Marketing.campaigngroup | Touchpoint |
| Commerce | Konversion |

In der Regel wird die Attribution für Konversionsspalten wie Bestellung, Käufe und Checkouts unter &quot;Commerce&quot;ausgeführt. Die Spalten für &quot;channel&quot;und &quot;marketing&quot;werden verwendet, um Touchpoints für Attribution AI zu definieren (z. B. `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). Für optimale Ergebnisse und Einblicke wird dringend empfohlen, so viele Konversions- und Touchpoint-Spalten wie möglich einzuschließen. Außerdem sind Sie nicht auf die oben genannten Spalten beschränkt. Sie können alle anderen empfohlenen oder benutzerdefinierten Spalten als Konversions- oder Touchpoint-Definition einbeziehen.

Experience Event (EE)-Datensätze müssen keine Kanal- und Marketing-Mixins enthalten, solange die Kanal- oder Kampagneninformationen, die für die Konfiguration eines Touchpoints relevant sind, in einem der Mixin- oder Durchlauffelder vorhanden sind.

>[!TIP]
>
>Wenn Sie Adobe Analytics-Daten in Ihrem CEE-Schema verwenden, werden die Touchpoint-Informationen für Analytics normalerweise in `channel.typeAtSource` (z. B. `channel.typeAtSource = 'email'`).

## Historische Daten {#data-requirements}

>[!IMPORTANT]
>
> Die für die Funktion von Attribution AI erforderliche Datenmenge lautet wie folgt:
> - Sie müssen Daten für mindestens 3 Monate (90 Tage) bereitstellen, um ein gutes Modell auszuführen.
> - Sie benötigen mindestens 1000 Konversionen.


Attribution AI erfordert historische Daten als Eingabe für das Modelltraining. Die erforderliche Datendauer wird hauptsächlich von zwei Schlüsselfaktoren bestimmt: Schulungsfenster und Rückblickfenster. Die Eingabe mit kürzeren Trainings-Fenstern reagiert empfindlicher auf aktuelle Trends, während längere Schulungsfenster dazu beitragen, stabilere und präzisere Modelle zu erstellen. Es ist wichtig, das Ziel mit historischen Daten zu modellieren, die Ihre Geschäftsziele am besten repräsentieren.

Die [Konfiguration des Schulungsfensters](./user-guide.md#training-window) filtert Konversionsereignisse, die für die Modellschulung auf der Grundlage der Zeit des Vorkommens festgelegt wurden. Derzeit beträgt das Schulungsfenster mindestens 1 Quartal (90 Tage). Die [Lookback-Fenster](./user-guide.md#lookback-window) bietet einen Zeitrahmen, der angibt, wie viele Tage vor den Touchpoints des Konversionsereignisses im Zusammenhang mit diesem Konversionsereignis enthalten sein sollten. Diese beiden Konzepte bestimmen zusammen die Menge der Eingabedaten (gemessen nach Tagen), die für eine Anwendung erforderlich ist.

Standardmäßig definiert Attribution AI das Trainings-Fenster als die letzten 2 Quartale (6 Monate) und das Lookback-Fenster als 56 Tage. Mit anderen Worten: Das Modell berücksichtigt alle definierten Konversionsereignisse, die in den letzten zwei Quartalen aufgetreten sind, und sucht nach allen Touchpoints, die innerhalb von 56 Tagen vor den zugehörigen Konversionsereignissen aufgetreten sind.

**Formel**:

Mindestlänge der erforderlichen Daten = Schulungsfenster + Lookback-Fenster

>[!TIP]
>
> Die Mindestlänge der Daten, die für eine Anwendung mit Standardkonfigurationen erforderlich sind, ist: 2 Quartale (180 Tage) + 56 Tage = 236 Tage.

Beispiel:

- Sie möchten Konversionsereignisse zuordnen, die innerhalb der letzten 90 Tage (3 Monate) stattgefunden haben, und alle Touchpoints verfolgen, die innerhalb von 4 Wochen vor dem Konversionsereignis aufgetreten sind. Die Dauer der Eingabedaten sollte sich über die letzten 90 Tage + 28 Tage (4 Wochen) erstrecken. Das Schulungsfenster beträgt 90 Tage, das Lookback-Fenster 28 Tage und insgesamt 118 Tage.

## Attribution AI der Ausgabedaten

Attribution AI gibt Folgendes aus:

- [Rohe granulare Punktzahl](#raw-granular-scores)
- [Aggregierte Werte](#aggregated-attribution-scores)

**Beispiel für ein Ausgabeschema:**

![](./images/input-output/schema_output.gif)

### Rohe granulare Punktzahl {#raw-granular-scores}

Attribution AI gibt Attributionsbewertungen auf der granularsten Ebene aus, sodass Sie die Bewertungen nach jeder Bewertungsspalte austeilen und würfen können. Um diese Bewertungen in der Benutzeroberfläche anzuzeigen, lesen Sie den Abschnitt unter [Anzeigen von Rohbewertungspfaden](#raw-score-path). Um die Bewertungen mit der API herunterzuladen, besuchen Sie die [Herunterladen von Bewertungen in Attribution AI](./download-scores.md) Dokument.

>[!NOTE]
>
> Sie können jede gewünschte Berichtsspalte aus dem Eingabedatensatz im Ergebnisausgabedatensatz nur dann anzeigen, wenn eine der folgenden Bedingungen erfüllt ist:
> - Die Berichtsspalte ist auf der Konfigurationsseite entweder als Teil der Touchpoint- oder Konversionsdefinitionskonfiguration enthalten.
> - Die Berichtsspalte ist in zusätzliche Score-Datensatzspalten enthalten.


In der folgenden Tabelle sind die Schemafelder in der Beispielausgabe für Rohbewertungen aufgeführt:

| Spaltenname (DataType) | NULL | Beschreibung |
| --- | --- | --- |
| timestamp (DateTime) | False | Der Zeitpunkt, zu dem ein Konversionsereignis oder eine Beobachtung aufgetreten ist. <br> **Beispiel:** 2020-06-09T00:01:51.000 Z |
| identityMap (Map) | True | identityMap des Benutzers ähnlich dem CEE XDM-Format. |
| eventType (String) | True | Der primäre Ereignistyp für diesen Zeitreihensatz. <br> **Beispiel:** &quot;Order&quot;, &quot;Purchase&quot;, &quot;Visit&quot; |
| eventMergeId (String) | True | Eine ID zum Korrelieren oder Zusammenführen mehrerer [!DNL Experience Events] zusammenführen, die im Wesentlichen dasselbe Ereignis sind oder zusammengeführt werden sollten. Dieser sollte vor der Aufnahme vom Datenproduzenten ausgefüllt werden. <br> **Beispiel:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (String) | False | Eine eindeutige Kennung für das Zeitreihenereignis. <br> **Beispiel:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (Object) | False | Der Objektcontainer auf oberster Ebene, der Ihrer zehnten ID entspricht. <br> **Beispiel:** _atsdsnrmmsv2 |
| your_schema_name (Objekt) | False | Ergebniszeile mit Konversionsereignis alle damit verknüpften Touchpoint-Ereignisse und deren Metadaten. <br> **Beispiel:** Attribution AI Scores - Modellname__2020 |
| Segmentierung (Zeichenfolge) | True | Konversionssegment, z. B. Geo-Segmentierung, für die das Modell erstellt wird. Wenn keine Segmente vorhanden sind, ist das Segment mit conversionName identisch. <br> **Beispiel:** ORDER_US |
| conversionName (String) | True | Name der Konversion, die während der Einrichtung konfiguriert wurde. <br> **Beispiel:** Bestellung, Lead, Besuch |
| conversion (Object) | False | Konversionsmetadaten-Spalten. |
| dataSource (String) | True | Globale eindeutige Identifizierung einer Datenquelle. <br> **Beispiel:** Adobe Analytics |
| eventSource (String) | True | Die Quelle, an der das tatsächliche Ereignis aufgetreten ist. <br> **Beispiel:** Adobe.com |
| eventType (String) | True | Der primäre Ereignistyp für diesen Zeitreihensatz. <br> **Beispiel:** Bestellung |
| geo (String) | True | Der geografische Standort, an dem die Konversion bereitgestellt wurde `placeContext.geo.countryCode`. <br> **Beispiel:** USA |
| priceTotal (Double) | True | Durch die Konversion erzielter Umsatz <br> **Beispiel:** 99,9 |
| product (String) | True | Die XDM-ID des Produkts. <br> **Beispiel:** RX 1080 ti |
| productType (String) | True | Der Anzeigename für das Produkt, wie er dem Benutzer für diese Produktansicht angezeigt wird. <br> **Beispiel:** Gpus |
| quantity (Integer) | True | Während der Konvertierung gekaufte Menge. <br> **Beispiel:** 1 1080 ti |
| receivedTimestamp (DateTime) | True | Zeitstempel der Konvertierung erhalten. <br> **Beispiel:** 2020-06-09T00:01:51.000 Z |
| skuId (String) | True | Bestandseinheit (Stock Keeping Unit, SKU), die eindeutige Kennung für ein vom Anbieter definiertes Produkt. <br> **Beispiel:** MJ-03-XS-Black |
| timestamp (DateTime) | True | Zeitstempel der Konvertierung. <br> **Beispiel:** 2020-06-09T00:01:51.000 Z |
| passThrough (Object) | True | Zusätzliche Score-Datensatzspalten, die vom Benutzer beim Konfigurieren des Modells angegeben werden. |
| commerce_order_purchaseCity (String) | True | Zusätzliche Spalte für Datensatz mit Punktzahl . <br> **Beispiel:** city: San Jose |
| customerProfile (Object) | False | Identitätsdetails des Benutzers, der zum Erstellen des Modells verwendet wird. |
| identity (Object) | False | Enthält die Details des Benutzers, der zum Erstellen des Modells verwendet wird, z. B. `id` und `namespace`. |
| id (String) | True | Identitäts-ID des Benutzers, z. B. Cookie-ID, AAID oder MCID usw. <br> **Beispiel:** 17348762725408656344688320891369597404 |
| namespace (String) | True | Identitäts-Namespace, der zum Erstellen der Pfade und damit des Modells verwendet wird. <br> **Beispiel:** aaid |
| touchpointsDetail (Object Array) | True | Die Liste der Touchpoint-Details, die zur Konvertierung führen, die nach | Touchpoint-Vorkommen oder Zeitstempel. |
| touchpointName (String) | True | Name des Touchpoints, der beim Einrichten konfiguriert wurde. <br> **Beispiel:** PAID_SEARCH_CLICK |
| scores (Object) | True | Touchpoint-Beitrag zu dieser Konversion als Ergebnis. Weitere Informationen zu den in diesem Objekt erzeugten Werten finden Sie in der [aggregierte Attributionswerte](#aggregated-attribution-scores) Abschnitt. |
| touchPoint (Object) | True | Touchpoint-Metadaten. Weitere Informationen zu den in diesem Objekt erzeugten Werten finden Sie in der [aggregierte Werte](#aggregated-scores) Abschnitt. |

### Anzeigen von Rohbewertungspfaden (Benutzeroberfläche) {#raw-score-path}

Sie können den Pfad zu Ihren Rohbewertungen in der Benutzeroberfläche anzeigen. Starten durch Auswahl von **[!UICONTROL Schemas]** in der Platform-Benutzeroberfläche suchen und wählen Sie dann Ihr Attributions-KI-Punktschema aus der **[!UICONTROL Durchsuchen]** Registerkarte.

![Schema auswählen](./images/input-output/schemas_browse.png)

Wählen Sie anschließend ein Feld im **[!UICONTROL Struktur]** -Fenster der Benutzeroberfläche, der **[!UICONTROL Feldeigenschaften]** -Registerkarte geöffnet. Within **[!UICONTROL Feldeigenschaften]** ist das Pfadfeld, das Ihren Rohbewertungen zugeordnet ist.

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

Die nachstehende Tabelle ordnet die Attributionsbewertungen den Rohbewertungen zu. Wenn Sie Ihre Rohbewertungen herunterladen möchten, besuchen Sie die [Herunterladen von Bewertungen in Attribution AI](./download-scores.md) Dokumentation.

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
| Touchpoint_scope (String) | Benutzerdefiniert | True | Name des Touchpoints, wie vom Benutzer konfiguriert <br> **Beispiel**: PAID_SEARCH_CLICK |
| product (String) | Benutzerdefiniert | True | Die XDM-Kennung des Produkts. <br> **Beispiel**: CC |
| product_type (String) | Benutzerdefiniert | True | Der Anzeigename für das Produkt, wie er dem Benutzer für diese Produktansicht angezeigt wird. <br> **Beispiel**: Gpus, Laptops |
| geo (String) | Benutzerdefiniert | True | Der geografische Standort, an dem die Konvertierung bereitgestellt wurde (placeContext.geo.countryCode) <br> **Beispiel**: USA |
| event_type (String) | Benutzerdefiniert | True | Der primäre Ereignistyp für diesen Zeitreihensatz <br> **Beispiel**: Gebührenpflichtige Konversion |
| media_type (String) | ENUM | False | Beschreibt, ob der Medientyp gebührenpflichtig, besessen oder verdient ist. <br> **Beispiel**: BEZAHLTE, EIGENTÜMER |
| channel (String) | ENUM | False | Die `channel._type` -Eigenschaft, die verwendet wird, um eine grobe Klassifizierung von Kanälen mit ähnlichen Eigenschaften in [!DNL Consumer Experience Event] XDM. <br> **Beispiel**: SUCHEN |
| action (String) | ENUM | False | Die `mediaAction` -Eigenschaft wird verwendet, um einen Typ der Erlebnisereignis-Medienaktion bereitzustellen. <br> **Beispiel**: KLICKEN |
| campaign_group (String) | Benutzerdefiniert | True | Name der Kampagnengruppe, in der mehrere Kampagnen gruppiert sind, z. B. &#39;50%_DISCOUNT&#39;. <br> **Beispiel**: KOMMERZIELL |
| campaign_name (String) | Benutzerdefiniert | True | Name der Kampagne, die zur Identifizierung der Marketing-Kampagne verwendet wird, z. B. &#39;50%_DISCOUNT_USA&#39; oder &#39;50%_DISCOUNT_ASIA&#39;. <br> **Beispiel**: Erntedankverkauf |

**Referenz zur Rohbewertung (aggregiert)**

Die nachstehende Tabelle ordnet die aggregierten Werte den Rohbewertungen zu. Wenn Sie Ihre Rohbewertungen herunterladen möchten, besuchen Sie die [Herunterladen von Bewertungen in Attribution AI](./download-scores.md) Dokumentation. Um die Rohbewertungspfade über die Benutzeroberfläche anzuzeigen, besuchen Sie den Abschnitt unter [Anzeigen von Rohbewertungspfaden](#raw-score-path) in diesem Dokument.

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

>[!IMPORTANT]
>
> - Attribution AI verwendet nur aktualisierte Daten für Weiterbildung und Scoring. Wenn Sie Daten löschen möchten, verwendet Attribution AI auch nicht die gelöschten Daten.
> - Um die Einhaltung der DSGVO in Attribution AI zu erleichtern, können Sie mit Adobe Experience Platform Privacy Service Protokolle einrichten, um Kundenanfragen beim Zugriff auf und Löschen ihrer Daten im Data Lake, Identity Service und Echtzeit-Kundenprofil zu berücksichtigen.
> - Alle Daten werden im Transit und im Ruhezustand verschlüsselt. Weitere Informationen finden Sie in der Dokumentation . [Datenverschlüsselung](../../../help/landing/governance-privacy-security/encryption.md)


## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten vorbereitet und alle Ihre Anmeldedaten und Schemata eingerichtet haben, führen Sie die folgenden Schritte aus: [Attribution AI-Benutzerhandbuch](./user-guide.md). Dieses Handbuch führt Sie durch die Erstellung einer Instanz für Attribution AI.
