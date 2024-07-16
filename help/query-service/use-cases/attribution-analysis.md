---
title: Attributionsanalyse
description: In diesem Dokument wird erläutert, wie Sie mithilfe von Query Service eine Marketing-Wirksamkeitsmessmethode erstellen können, die auf dem Marketing-Attributionsmodell des Erstkontakts und Letztkontakts basiert.
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 10%

---

# Attributionsanalyse

Attribution ist ein analytisches Konzept, das bei der Bestimmung der Marketing-Taktiken wie Kanäle, Angebote und Nachrichten hilft, die zu Unternehmensumsätzen oder Konversionen beitragen. Dieses Konzept bewertet die Journey des Verbrauchers (d. h. den Prozess, durch den ein Kunde mit einem Unternehmen interagiert, um ein Ziel zu erreichen), der zu einem Kauf oder einer Akquise auf der Grundlage von Kunden-Touchpoints führt (d. h. jedes Mal, wenn ein Verbraucher mit Ihrer Marke interagiert). Mithilfe der Attributionsanalyse können Marketingexperten den ROI der Kanäle bewerten, die sie mit einem potenziellen Kunden verbinden.

## Erste Schritte

Die SQL-Beispiele in diesem Dokument sind Abfragen, die häufig mit Adobe Analytics-Daten verwendet werden. Dieses Tutorial setzt ein Verständnis der folgenden Komponenten voraus:

* [Adobe Analytics-Quell-Connector für Report Suite-Daten - Übersicht](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [Die Dokumentation zu Analytics-Feldzuordnungen](../../sources/connectors/adobe-applications/mapping/analytics.md) enthält weitere Informationen zur Erfassung und Zuordnung von Analysedaten zur Verwendung mit Query Service.
* [Übersicht über den Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html)
* [Das Handbuch zum Adobe Analytics-Attributionsbedienfeld](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html).

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](../sql/adobe-defined-functions.md#window-functions) . Auch das [Adobe-Marketing- und Commerce-Terminologieglossar](https://business.adobe.com/glossary/index.html) kann nützlich sein.

Für jeden der folgenden Anwendungsfälle wird ein parametrisiertes SQL-Abfragebeispiel als Vorlage bereitgestellt, die Sie anpassen können. Geben Sie Parameter an, wo immer Sie `{ }` in den SQL-Beispielen sehen, die Sie bewerten möchten.

## Ziele

In einem Anwendungsfall für die Attribution werden Adobe Analytics-Daten verwendet, um Kundenaktionen einem erfolgreichen Ergebnis zuzuordnen. Diese Zuordnung ist ein wichtiger Teil des Verständnisses der Faktoren, die die Kundenerlebnisse beeinflussen. Attributionsanalysedaten können verwendet werden, um die Bedeutung des Touchpoints eines Kunden während der Journey eines Kunden zu verstehen.

Die in diesem Dokument enthaltenen Abfragebeispiele unterstützen verschiedene Anwendungsfälle für die Erstkontakt- und Letztkontakt-Attribution mit unterschiedlichen Ablaufeinstellungen. Dieses Handbuch zeigt die folgenden Schlüsselkonzepte:

* Erstkontakt- und Letztkontakt-Attribution.
* Erstkontakt- und Letztkontakt-Attribution mit Ablauftimeout.
* Erstkontakt- und Letztkontakt-Attribution mit Ablaufbedingung.

## Attributionsabfrageparameter {#attribution-query-parameters}

Die nachstehende Tabelle enthält eine Aufschlüsselung der Parameter und ihrer Beschreibungen, die in Zuordnungsabfragen für Erstkontakt und Letztkontakt verwendet werden:

| Parameter | Beschreibung |
|---|---|
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Bezeichnung für das zurückgegebene Objekt. |
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das den Zielkanal für die Abfrage darstellt. |
| `{EXP_TIMEOUT}` | Das Zeitfenster vor dem Kanalereignis in Sekunden, in dem die Abfrage nach einem Erstkontaktereignis sucht. |
| `{EXP_CONDITION}` | Die Bedingung, die den Ablaufpunkt des Kanals bestimmt. |
| `{EXP_BEFORE}` | Ein boolescher Wert, der anzeigt, ob der Kanal vor oder nach der angegebenen Bedingung (`{EXP_CONDITION}`) abläuft. Dies ist in erster Linie für die Ablaufbedingungen einer Sitzung aktiviert, um sicherzustellen, dass der Erstkontakt nicht aus einer vorherigen Sitzung ausgewählt wird. Standardmäßig ist dieser Wert auf `false` gesetzt. |

## Spaltenkomponenten für Abfrageergebnisse {#query-result-column-components}

Die Ergebnisse für die Zuordnungsabfragen werden entweder in der Spalte `first_touch` oder in der Spalte `last_touch` angegeben. Diese Spalten bestehen aus den folgenden Komponenten:

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, die in Azure Data Factory (ADF) als Beschriftung eingegeben wurde. |
| `{VALUE}` | Der Wert aus `{CHANNEL_VALUE}`, der den letzten Kontakt innerhalb des `{EXP_TIMEOUT}`-Intervalls darstellt. |
| `{TIMESTAMP}` | Der Zeitstempel des [!DNL Experience Event] , bei dem der letzte Kontakt aufgetreten ist |
| `{FRACTION}` | Die Attribution des letzten Kontakts, ausgedrückt als Dezimalbruch. |

### Erstkontakt-Attribution {#first-touch}

Die Erstkontakt-Attribution akkreditiert 100 % der Verantwortung für ein erfolgreiches Ergebnis des ersten Kanals, auf den der Verbraucher gestoßen ist. Dieses SQL-Beispiel wird verwendet, um die Interaktion hervorzuheben, die zu einer nachfolgenden Reihe von Kundenaktionen führte.

Die nachstehende Abfrage gibt den Attributionswert des Erstkontakts und Details des Kanals im Ziel-Datensatz [!DNL Experience Event] zurück. Es wird auch ein `struct` -Objekt für den ausgewählten Kanal mit dem Erstkontaktwert, dem Zeitstempel und der Attribution für jede Zeile zurückgegeben.

>[!NOTE]
>
>Die Experience Cloud ID (ECID) wird auch als MCID bezeichnet und wird weiterhin in Namespaces verwendet.

**Abfragesyntax**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

Eine vollständige Liste der potenziell erforderlichen Parameter und deren Beschreibungen finden Sie im Abschnitt [Attributionsabfrageparameter](#attribution-query-parameters).

**Beispielabfrage**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

**Ergebnisse**

In den unten stehenden Ergebnissen wird der anfängliche Trackingcode `em:946426` aus dem Datensatz [!DNL Experience Event] entnommen. Dieser Trackingcode wird zu 100 % (`1.0`) der Verantwortung für die Kundenaktionen zugeordnet, da dies die erste Interaktion war.

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

Eine Aufschlüsselung der in der Spalte `first_touch` angezeigten Ergebnisse finden Sie im Abschnitt [Spaltenkomponenten](#query-result-column-components).

### Letztkontakt-Attribution {#second-touch}

Die Letztkontakt-Attribution akkreditiert 100 % der Verantwortung für ein erfolgreiches Ergebnis des letzten Kanals, auf den der Verbraucher gestoßen ist. In diesem SQL-Beispiel wird die endgültige Interaktion in einer Reihe von Kundenaktionen hervorgehoben.

Die Abfrage gibt den Attributionswert des letzten Kontakts und Details des Kanals im Ziel-Datensatz [!DNL Experience Event] zurück. Es wird auch ein `struct` -Objekt für den ausgewählten Kanal mit dem Wert des letzten Kontakts, dem Zeitstempel und der Attribution für jede Zeile zurückgegeben.

**Abfragesyntax**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

**Beispielabfrage**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Ergebnisse**

In den unten angezeigten Ergebnissen ist der Trackingcode im zurückgegebenen Objekt die letzte Interaktion in jedem [!DNL Experience Event] -Datensatz. Jedem Code wird ein Anteil von 100 % (`1.0`) am Einfluss auf die Aktionen des Kunden zugeschrieben, da dies die letzte Interaktion war.

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

Eine Aufschlüsselung der in der Spalte `last_touch` angezeigten Ergebnisse finden Sie im Abschnitt [Spaltenkomponenten](#query-result-column-components).

### Erstkontakt-Attribution mit bedingter Gültigkeit {#first-touch-attribution-with-expiration-condition}

Mit dieser Abfrage können Sie sehen, welche Interaktion zu einer Reihe von Kundenaktionen innerhalb eines Teils des [!DNL Experience Event] -Datensatzes geführt hat, der durch eine von Ihnen festgelegte Bedingung bestimmt wird.

Die Abfrage gibt den Attributionswert des Erstkontakts und Details für einen einzelnen Kanal im Ziel-Datensatz [!DNL Experience Event] zurück, der nach oder vor einer Bedingung abläuft. Es wird auch ein `struct` -Objekt mit dem Wert des Erstkontakts, dem Zeitstempel und der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile zurückgegeben.

**Abfragesyntax**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Eine vollständige Liste der potenziell erforderlichen Parameter und deren Beschreibungen finden Sie im Abschnitt [Attributionsabfrageparameter](#attribution-query-parameters).

**Beispielabfrage**

Im folgenden Beispiel wird ein Kauf (`commerce.purchases.value IS NOT NULL`) an jedem der vier in den Ergebnissen angezeigten Tage (15., 21., 23. und 29. Juli) aufgezeichnet und dem anfänglichen Trackingcode an jedem Tag ein Anteil von 100 % (`1.0`) am Einfluss auf die Kundenaktionen zugeschrieben.

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Ergebnisse**

```console
                 id               |       timestamp       | trackingCode |                   first_touch                   
----------------------------------+-----------------------+--------------+-------------------------------------------------
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Eine Aufschlüsselung der in der Spalte `first_touch` angezeigten Ergebnisse finden Sie im Abschnitt [Spaltenkomponenten](#query-result-column-components).

### Erstkontakt-Attribution mit Gültigkeits-Timeout {#first-touch-attribution-with-expiration-timeout}

Mit dieser Abfrage wird die Interaktion innerhalb eines ausgewählten Zeitraums ermittelt, die zu einer erfolgreichen Kundenaktion führte.

Die nachstehende Abfrage gibt den Attributionswert des Erstkontakts sowie Details für einen einzelnen Kanal im Ziel-Datensatz [!DNL Experience Event] für einen bestimmten Zeitraum zurück. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des Erstkontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

**Abfragesyntax**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

Eine vollständige Liste der potenziell erforderlichen Parameter und deren Beschreibungen finden Sie im Abschnitt [Attributionsabfrageparameter](#attribution-query-parameters).

**Beispielabfrage**

Im folgenden Beispiel ist der für jede Kundenaktion zurückgegebene Erstkontakt die früheste Interaktion innerhalb der letzten sieben Tage (expTimeout = 86400 * 7).

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Ergebnisse**

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Eine Aufschlüsselung der in der Spalte `first_touch` angezeigten Ergebnisse finden Sie im Abschnitt [Spaltenkomponenten](#query-result-column-components).

### Letztkontakt-Attribution mit bedingter Gültigkeit {#last-touch-attribution-with-expiration-condition}

Mit dieser Abfrage wird die letzte Interaktion in einer Reihe von Kundenaktionen innerhalb eines Teils des [!DNL Experience Event] -Datensatzes ermittelt, der durch eine von Ihnen festgelegte Bedingung bestimmt wird.

Die nachstehende Abfrage gibt den Attributionswert des letzten Kontakts sowie Details für einen einzelnen Kanal im Ziel-Datensatz [!DNL Experience Event] zurück, der nach oder vor einer Bedingung abläuft. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

**Abfragesyntax**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Eine vollständige Liste der potenziell erforderlichen Parameter und deren Beschreibungen finden Sie im Abschnitt [Attributionsabfrageparameter](#attribution-query-parameters).

**Beispielabfrage**

Im folgenden Beispiel wird ein Kauf (`commerce.purchases.value IS NOT NULL`) an jedem der vier in den Ergebnissen angezeigten Tage (15., 21., 23. und 29. Juli) aufgezeichnet und dem letzten Trackingcode an jedem Tag ein Anteil von 100 % (`1.0`) am Einfluss auf die Kundenaktionen zugeschrieben.

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Beispielergebnisse**

```console
                id                 |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+------------------------------------------------
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Eine Aufschlüsselung der in der Spalte `last_touch` angezeigten Ergebnisse finden Sie im Abschnitt [Spaltenkomponenten](#query-result-column-components).

### Letztkontakt-Attribution mit Gültigkeits-Timeout {#last-touch-attribution-with-expiration-timeout}

Mit dieser Abfrage wird die letzte Interaktion innerhalb eines ausgewählten Zeitintervalls ermittelt. Die Abfrage gibt den Attributionswert des letzten Kontakts und Details für einen einzelnen Kanal im Ziel-Datensatz [!DNL Experience Event] für einen bestimmten Zeitraum zurück. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

**Abfragesyntax**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

Eine vollständige Liste der potenziell erforderlichen Parameter und deren Beschreibungen finden Sie im Abschnitt [Attributionsabfrageparameter](#attribution-query-parameters).

**Beispielabfrage**

Im nachfolgenden Beispiel stellt der für die einzelnen Kundeninteraktionen zurückgegebene letzte Kontakt die finale Interaktion innerhalb der darauffolgenden sieben Tage (`expTimeout = 86400 * 7`) dar.

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Ergebnisse**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

Eine Aufschlüsselung der in der Spalte `last_touch` angezeigten Ergebnisse finden Sie im Abschnitt [Spaltenkomponenten](#query-result-column-components).
