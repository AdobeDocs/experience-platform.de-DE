---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe-definierte Funktionen
topic: functions
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 81%

---


# Adobe-definierte Funktionen

Adobe-defined functions (ADFs) are prebuilt functions in [!DNL Query Service] that help perform common business related tasks on [!DNL ExperienceEvent] data. Dazu gehören etwa auch Funktionen für Sessionization und Attribution, wie Adobe Analytics sie bietet. Weitere Informationen zu Adobe Analytics und den Konzepten hinter den auf der vorliegenden Website definierten ADFs finden Sie in der [Adobe Analytics-Dokumentation](https://docs.adobe.com/content/help/de-DE/analytics/landing/home.html). This document provides information for Adobe-defined functions available in [!DNL Query Service].

## Window-Funktionen

Ein großer Teil der Business-Logik setzt voraus, die Kontaktpunkte (bzw. „Touchpoints“) zu erfassen, an denen ein Kunde mit Ihrem Unternehmen interagiert, und diese nach dem Zeitpunkt ihres Eintretens zu sortieren. This support is provided by [!DNL Spark] SQL in the form of window functions. Window-Funktionen sind Teil von Standard-SQL und werden von einer Vielzahl anderer SQL-Engines unterstützt.

Eine Window-Funktion aktualisiert eine Aggregation und gibt für jede Zeile in Ihrer sortierten Untergruppe ein einzelnes Element zurück. Die einfachste Aggregationsfunktion lautet `SUM()`. `SUM()` berechnet aus den von Ihnen angegebenen Zeilen die Summe. Wenden Sie `SUM()` stattdessen auf ein Fenster an, wird es in eine Window-Funktion umgewandelt und die kumulative Summe für jede Zeile ausgegeben.

The majority of the [!DNL Spark] SQL helpers are window functions that update each row in your window, with the state of that row added.

### Spezifikation

Syntax: `OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| [partition] | Eine auf einer Spalte oder einem verfügbaren Feld basierende Untergruppe der Zeilen. Beispiel: `PARTITION BY endUserIds._experience.mcid.id` |
| [order] | Eine Spalte oder ein verfügbares Feld zur Sortierung der Zeilen-Untergruppe. Beispiel: `ORDER BY timestamp` |
| [frame] | Eine Untergruppe der Zeilen in einer Partition. Beispiel: `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionization

When you are working with [!DNL ExperienceEvent] data originating from a website, mobile application, interactive voice response system, or any other customer interaction channel it helps if events can be grouped around a related period of activity. In der Regel fußt eine Aktivität auf einer bestimmten Absicht wie der Suche nach einem Produkt, der Zahlung einer Rechnung, dem Abrufen des Kontostandes, dem Ausfüllen eines Formulars etc. Durch diese Gruppierung lassen sich die Ereignisse einfacher zuordnen, wodurch ein Kundenerlebnis in einem breiter gefassten Kontext analysiert werden kann.

Weitere Informationen zur Sessionization in Adobe Analytics finden Sie in der Dokumentation zu [kontextbezogenen Sitzungen](https://docs.adobe.com/content/help/de-DE/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

### Spezifikation

Syntax: `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Feld im Datensatz, das den Zeitstempel angibt. |
| `expirationInSeconds` | Intervall in Sekunden, das den Zeitraum zwischen Ereignissen angibt, der zwischen dem Ende der aktuellen und dem Beginns einer neuen Sitzung liegt. |

| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `timestamp_diff` | Zeit in Sekunden, die zwischen dem aktuellen und dem vorherigen Datensatz liegt. |
| `num` | Eine eindeutige Sitzungsnummer, die bei 1 beginnend den Schlüssel angibt, der unter `PARTITION BY` der Window-Funktion definiert ist. |
| `is_new` | Ein Boolean-Wert, der angibt, ob ein Datensatz der erste einer Sitzung ist. |
| `depth` | Tiefe des aktuellen Datensatzes innerhalb der Sitzung. |

#### Beispiel-Abfrage

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

#### Ergebnisse

```
                id                |       timestamp       |      session       
----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

## Attribution

Für das Verständnis der Faktoren, die sich auf das Kundenerlebnis auswirken, ist es entscheidend, Aktionen von Kunden mit Erfolgen in Relation zu stellen. Die folgenden ADFs unterstützen eine Attribution für die erste und letzte Aktion unter Verwendung verschiedener Einstellungen für die Sitzungsgültigkeit.

Weitere Informationen zur Attribution in Adobe finden Sie im Adobe Analytics-Handbuch unter [Übersicht über Attribution IQ](https://docs.adobe.com/content/help/de-DE/analytics/analyze/analysis-workspace/panels/attribution.html).[!DNL Analytics]

### First-Touch-Attribution

Returns the first touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des Erstkontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage hilft dabei nachzuvollziehen, welche Interaktion zu einer Reihe von Kundenaktionen geführt hat. In the example shown below, the initial tracking code (`em:946426`) in the [!DNL ExperienceEvent] data is attributed 100% (`1.0`) responsibility for the customer actions as it was the first interaction.

### Spezifikation

Syntax: `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Feld im Datensatz, das den Zeitstempel angibt. |
| `channelName` | Ein Anzeigename, der als Beschriftung des zurückgegebenen Objekts dient. |
| `channelValue` | Spalte oder Feld, die bzw. das den Zielkanal für die Abfrage bildet. |


| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Der in der ADF als Beschriftung angegebene `channelName`. |
| `value` | Der Wert aus `channelValue`, der den Erstkontakt im darstellt.[!DNL ExperienceEvent] |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the first touch occured |
| `fraction` | Die Attribution des Erstkontakts, ausgedrückt als anteiliger Wert. |

#### Beispiel-Abfrage

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

#### Ergebnisse

```
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
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

### Last-Touch-Attribution

Returns the last touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage hilft dabei, die letzte Interaktion in einer Reihe von Kundenaktionen nachzuvollziehen. In the example shown below, the tracking code in the returned object is the last interaction in each [!DNL ExperienceEvent] record. Jedem Code wird ein Anteil von 100 % (`1.0`) am Einfluss auf die Kundenaktionen zugeschrieben, da dieser die jeweils letzte Interaktion markiert.

### Spezifikation

Syntax: `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Feld im Datensatz, das den Zeitstempel angibt. |
| `channelName` | Ein Anzeigename, der als Beschriftung des zurückgegebenen Objekts dient. |
| `channelValue` | Spalte oder Feld, die bzw. das den Zielkanal für die Abfrage bildet. |


| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Der in der ADF als Beschriftung angegebene `channelName`. |
| `value` | Der Wert aus `channelValue`, der den letzten Kontakt im darstellt.[!DNL ExperienceEvent] |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the `channelValue` was used |
| `fraction` | Die Attribution des letzten Kontakts, ausgedrückt als anteiliger Wert. |

#### Beispiel-Abfrage

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

#### Ergebnisse

```
                id                 |       timestamp       | trackingcode |                   last_touch                   
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

### First-Touch-Attribution mit bedingter Gültigkeit

Returns the first touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset, expiring after or before a condition. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des Erstkontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

This query is useful if you want to see what interaction led to a series of customer actions within a portion of the [!DNL ExperienceEvent] dataset determined by a condition of your chosing. Im nachfolgenden Beispiel wird ein Kauf (`commerce.purchases.value IS NOT NULL`) an jedem der vier in den Ergebnissen angezeigten Tage (15., 21., 23. und 29. Juli) aufgezeichnet und dem anfänglichen Trackingcode an jedem Tag ein Anteil von 100 % (`1.0`) am Einfluss auf die Kundenaktionen zugeschrieben.

#### Spezifikation

Syntax: `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Feld im Datensatz, das den Zeitstempel angibt. |
| `channelName` | Ein Anzeigename, der als Beschriftung des zurückgegebenen Objekts dient. |
| `channelValue` | Spalte oder Feld, die bzw. das den Zielkanal für die Abfrage bildet. |
| `expCondition` | Die Bedingung, die die Gültigkeit des Kanals bestimmt. |
| `expBefore` | Die Standardeinstellung ist `false`. Ein Boolean-Wert, der angibt, ob der Kanal vor oder nach Eintritt der festgelegten Bedingung abläuft. Wird in erster Linie als Bedingung für den Sitzungsablauf (z. B. `sess.depth = 1, true`) festgelegt, um sicherzustellen, dass nicht der erste Kontakt aus einer vorherigen Sitzung ausgewählt wird. |

| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Der in der ADF als Beschriftung angegebene `channelName`. |
| `value` | Der Wert aus `channelValue`[!DNL ExperienceEvent], der im den Erstkontakt vor der  darstellt.`expCondition` |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the first touch occured |
| `fraction` | Die Attribution des Erstkontakts, ausgedrückt als anteiliger Wert. |

#### Beispiel-Abfrage

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

#### Ergebnisse

```
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
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

### First-Touch-Attribution mit Gültigkeits-Timeout

Returns the first touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset for a specified time period. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des Erstkontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile. Diese Abfrage hilft dabei nachzuvollziehen, welche Interaktion innerhalb eines bestimmten Zeitraums zu einer Kundenaktion geführt hat. Im nachfolgenden Beispiel stellt der für die einzelnen Kundeninteraktionen zurückgegebene Erstkontakt die früheste Interaktion innerhalb der letzten sieben Tage (`expTimeout = 86400 * 7`) dar.

#### Spezifikation

Syntax: `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Feld im Datensatz, das den Zeitstempel angibt. |
| `channelName` | Ein Anzeigename, der als Beschriftung des zurückgegebenen Objekts dient. |
| `channelValue` | Spalte oder Feld, die bzw. das den Zielkanal für die Abfrage bildet. |
| `expTimeout` | Das Zeitfenster (in Sekunden) vor dem Kanal-Ereignis, in dem die Abfrage nach einem Erstkontakt-Ereignis sucht. |

| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Der in der ADF als Beschriftung angegebene `channelName`. |
| `value` | Der Wert aus `channelValue`, der den Erstkontakt innerhalb des `expTimeout`-Intervalls darstellt. |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the first touch occured |
| `fraction` | Die Attribution des Erstkontakts, ausgedrückt als anteiliger Wert. |

#### Beispiel-Abfrage

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, 'Paid First', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### Ergebnisse

```
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### First-Touch-Attribution mit bedingter Gültigkeit

Returns the last touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset, expiring after or before a condition. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile. This query is useful if you want to see the last interaction in a series of customer actions within a portion of the [!DNL ExperienceEvent] dataset determined by a condition of your chosing. Im nachfolgenden Beispiel wird ein Kauf (`commerce.purchases.value IS NOT NULL`) an jedem der vier in den Ergebnissen angezeigten Tage (15., 21., 23. und 29. Juli) festgehalten und dem letzten Trackingcode an jedem Tag ein Anteil von 100 % (`1.0`) am Einfluss auf die Kundenaktionen zugeschrieben.

#### Spezifikation

Syntax: `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Feld im Datensatz, das den Zeitstempel angibt. |
| `channelName` | Ein Anzeigename, der als Beschriftung des zurückgegebenen Objekts dient. |
| `channelValue` | Spalte oder Feld, die bzw. das den Zielkanal für die Abfrage bildet. |
| `expCondition` | Die Bedingung, die die Gültigkeit des Kanals bestimmt. |
| `expBefore` | Die Standardeinstellung ist `false`. Ein Boolean-Wert, der angibt, ob der Kanal vor oder nach Eintritt der festgelegten Bedingung abläuft. Wird in erster Linie für Bedingungen für die Sitzungsgültigkeit (z. B. `sess.depth = 1, true`) festgelegt, um sicherzustellen, dass nicht der letzte Kontakt aus einer vorherigen Sitzung ausgewählt wird. |

| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Der in der ADF als Beschriftung angegebene `channelName`. |
| `value` | Der Wert aus `channelValue`[!DNL ExperienceEvent], der im den letzten Kontakt vor der  darstellt.`expCondition` |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the last touch occured |
| `percentage` | Die Attribution des letzten Kontakts, ausgedrückt als anteiliger Wert. |

#### Beispiel-Abfrage

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

#### Ergebnisse

```
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

### First-Touch-Attribution mit bedingter Gültigkeit

Returns the last touch attribution value and details for a single channel in the target [!DNL ExperienceEvent] dataset for a specified time period. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile. Diese Abfrage hilft dabei, die letzte Interaktion in einem bestimmten Zeitintervall nachzuvollziehen. Im nachfolgenden Beispiel stellt der für die einzelnen Kundeninteraktionen zurückgegebene letzte Kontakt die finale Interaktion innerhalb der darauffolgenden sieben Tage (`expTimeout = 86400 * 7`) dar.

#### Spezifikation

Syntax: `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Feld im Datensatz, das den Zeitstempel angibt. |
| `channelName` | Ein Anzeigename, der als Beschriftung des zurückgegebenen Objekts dient. |
| `channelValue` | Spalte oder Feld, die bzw. das den Zielkanal für die Abfrage bildet. |
| `expTimeout` | Das Zeitfenster (in Sekunden) vor dem Kanal-Ereignis, in dem die Abfrage nach einem Letztkontakt-Ereignis sucht. |

| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Der in der ADF als Beschriftung angegebene `channelName`. |
| `value` | Der Wert aus `channelValue`, der den letzten Kontakt innerhalb des `expTimeout`-Intervalls darstellt. |
| `timestamp` | The timestamp of the [!DNL ExperienceEvent] where the last touch occured |
| `percentage` | Die Attribution des letzten Kontakts, ausgedrückt als anteiliger Wert. |

#### Beispiel-Abfrage

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

#### Ergebnisse

```
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

## Vorheriger/nächster Kontakt

Um ein besseres Bild von Kunden zu gewinnen, ist es wichtig, deren Navigation innerhalb eines Erlebnisses nachvollziehen zu können. Dies liefert eine Verständnis davon, welche Tiefe die Kundeninteraktion aufweist, ob die für ein Erlebnis vorgesehenen Schritte wie gewünscht funktionieren und an welchen Stellen potenzielle Schwierigkeiten das Kundenerlebnis beeinträchtigen. Die folgenden ADFs ermöglichen die Erstellung von Pfadansichten aus „Vorherige“- und „Nächste“-Beziehungen. Sie können Beziehungen für „Vorherige Seite“ und „Nächste Seite“ erstellen oder mehrere Ereignisse durchlaufen, um Pfade zu erstellen.

### Vorheriger Kontakt

Legt den vorherigen Wert eines bestimmten Felds fest, der innerhalb des Fensters eine festgelegte Anzahl von Schritten entfernt ist. Beachten Sie im Beispiel, dass die `WINDOW`-Funktion mit einem Frame von `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` konfiguriert ist, durch das die ADF die aktuelle Zeile sowie alle vor ihr liegenden Zeilen ausgibt.

#### Spezifikation

Syntax: `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `key` | Die Spalte oder das Feld aus dem Ereignis. |
| `shift` | (Optional) Die Anzahl der Ereignisse außerhalb des aktuellen Ereignisses. Der Standardwert ist 1. |
| `ingnoreNulls` | Boolean-Wert, der angibt, ob `key`-Werte mit dem Wert null ignoriert werden sollen. Der Standardwert ist `false`. |


| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `value` | Der auf dem in der ADF verwendeten `key` basierende Wert. |

#### Beispiel-Abfrage

```sql
SELECT endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id, _experience.analytics.session.num
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp ASC
```

#### Ergebnisse

```
                id                 |       timestamp       |                 name                |                    previous_page                    
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

### Nächster Kontakt

Legt den nächsten Wert eines bestimmten Felds fest, der innerhalb des Fensters eine festgelegte Anzahl von Schritten entfernt ist. Beachten Sie im Beispiel, dass die `WINDOW`-Funktion mit einem Frame von `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` konfiguriert ist, durch das die ADF die aktuelle Zeile sowie alle nach ihr liegenden Zeilen ausgibt.

#### Spezifikation

Syntax: `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `key` | Die Spalte oder das Feld aus dem Ereignis. |
| `shift` | (Optional) Die Anzahl der Ereignisse außerhalb des aktuellen Ereignisses. Der Standardwert ist 1. |
| `ingnoreNulls` | Boolean-Wert, der angibt, ob `key`-Werte mit dem Wert null ignoriert werden sollen. Der Standardwert ist `false`. |


| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `value` | Der auf dem in der ADF verwendeten `key` basierende Wert. |

#### Beispiel-Abfrage

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

#### Ergebnisse

```
                id                 |       timestamp       |                name                 |             previous_page             
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

## Zeit zwischen

Mit der „time_between“-Funktion können Sie das Kundenverhalten innerhalb eines Zeitraums vor oder nach dem Eintreten eines Ereignisses untersuchen. So können Sie die zwischen den 7 Tagen nach einer Kampagne oder eines Ereignisses liegenden Ereignisse für eine oder alle Ihre Kunden abrufen.

### Zeit zwischen vorheriger Übereinstimmung

Implementiert eine neue Dimension, die die seit einem bestimmten Vorfall verstrichene Zeit misst.

#### Spezifikation

Syntax: `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Feld für Zeitstempel im Datensatz, der für alle Ereignisse übernommen wird. |
| `eventDefintion` | Ausdruck zur Qualifizierung des vorherigen Ereignisses. |
| `timeUnit` | Einheit der Ausgabe: Tage, Stunden, Minuten und Sekunden. Wird standardmäßig in Sekunden ausgegeben. |

Ausgabe: Gibt einen Zahlenwert zurück, der die Zeiteinheit seit dem Eintreten des vorherigen übereinstimmenden Ereignisses darstellt oder null bleibt, wenn kein übereinstimmendes Ereignis gefunden wurde.

#### Beispiel-Abfrage

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

#### Ergebnisse

```
             page_name             | average_minutes_since_registration 
-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

### Zeit zwischen nächster Übereinstimmung

Implementiert eine neue Dimension, die die Zeit vor dem Eintritt eines bestimmten Ereignisses misst.

#### Spezifikation

Syntax: `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Feld für Zeitstempel im Datensatz, der für alle Ereignisse übernommen wird. |
| `eventDefintion` | Ausdruck zur Qualifizierung des nächsten Ereignisses. |
| `timeUnit` | Einheit der Ausgabe: Tage, Stunden, Minuten und Sekunden. Wird standardmäßig in Sekunden ausgegeben. |

Ausgabe: Gibt einen Zahlenwert zurück, der die Zeiteinheit nach dem nächsten übereinstimmenden Ereignis darstellt oder null bleibt, wenn kein übereinstimmendes Ereignis gefunden wurde.

#### Beispiel-Abfrage

```
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

#### Ergebnisse

```
             page_name             | average_minutes_until_order_confirmation 
-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

## Nächste Schritte

Using the functions described here, you can write queries to access your own [!DNL ExperienceEvent] datasets using [!DNL Query Service]. For more information about authoring queries in [!DNL Query Service], see the documentation on [creating queries](../creating-queries/creating-queries.md).
