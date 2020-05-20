---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Von Adobe definierte Funktionen
topic: functions
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '2190'
ht-degree: 4%

---


# Von Adobe definierte Funktionen

Adobe-definierte Funktionen (ADFs) sind vordefinierte Funktionen im Abfrage Service, mit denen Sie häufige geschäftsbezogene Aufgaben zu ExperienceEvent-Daten durchführen können. Dazu gehören Funktionen für die Sessionierung und Zuordnung, wie sie in Adobe Analytics gefunden werden. Weitere Informationen zu Adobe Analytics und den Konzepten hinter den auf dieser Seite definierten ADFs finden Sie in der Dokumentation [zu](https://docs.adobe.com/content/help/de-DE/analytics/landing/home.html) Adobe Analytics. Dieses Dokument enthält Informationen zu von Adobe definierten Funktionen, die im Abfrage Service verfügbar sind.

## Fensterfunktionen

Der Großteil der Geschäftslogik erfordert das Sammeln der Touchpoints für einen Kunden und deren rechtzeitige Bestellung. Diese Unterstützung wird von Spark SQL in Form von Fensterfunktionen bereitgestellt. Window-Funktionen sind Teil von Standard-SQL und werden von vielen anderen SQL-Engines unterstützt.

Eine Fensterfunktion aktualisiert eine Aggregation und gibt für jede Zeile in Ihrer geordneten Untergruppe ein einzelnes Element zurück. Die grundlegendste Aggregationsfunktion ist `SUM()`. `SUM()` nimmt Ihre Zeilen und gibt Ihnen eine Summe. Wenn Sie stattdessen `SUM()` auf ein Fenster anwenden und es in eine Fensterfunktion umwandeln, erhalten Sie bei jeder Zeile eine kumulative Summe.

Die Mehrzahl der Spark SQL Helfer sind Fensterfunktionen, die jede Zeile in Ihrem Fenster mit dem Status dieser Zeile aktualisieren.

### Spezifikation

Syntax: `OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| [partition] | Eine Untergruppe der Zeilen basierend auf einer Spalte oder einem verfügbaren Feld. Beispiel, `PARTITION BY endUserIds._experience.mcid.id` |
| [bestellen] | Eine Spalte oder ein verfügbares Feld, das bzw. die zur Reihenfolge der Untergruppe/n verwendet wird/werden. Beispiel, `ORDER BY timestamp` |
| [frame] | Eine Untergruppe der Zeilen in einer Partition. Beispiel, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionierung

Wenn Sie mit ExperienceEvent-Daten arbeiten, die von einer Website, mobilen Anwendung, einem interaktiven Voice-Response-System oder einem anderen Kanal zur Kundeninteraktion stammen, ist es hilfreich, wenn Ereignis um einen bestimmten Zeitraum der Aktivität gruppiert werden können. Normalerweise haben Sie eine bestimmte Absicht, Ihre Aktivität zu fördern, wie z.B. die Suche nach einem Produkt, die Zahlung einer Rechnung, die Überprüfung der Kontobilanz, das Ausfüllen einer Anwendung usw. Diese Gruppierung hilft, die Ereignis zuzuordnen, um mehr Kontext über das Kundenerlebnis zu entdecken.

Weitere Informationen zur Sessionierung in Adobe Analytics finden Sie in der Dokumentation zu [kontextsensitiven Sitzungen](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

### Spezifikation

Syntax: `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Im Dataset gefundenes Zeitstempelfeld |
| `expirationInSeconds` | Anzahl der Sekunden, die zwischen den Ereignissen benötigt werden, um das Ende der aktuellen Sitzung und den Beginn einer neuen Sitzung zu qualifizieren |

| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `timestamp_diff` | Zeit in Sekunden zwischen aktuellem Datensatz und vorherigem Datensatz |
| `num` | Eine eindeutige Sitzungsnummer, beginnend bei 1, für den Schlüssel, der in der Funktion `PARTITION BY` des Fensters definiert ist. |
| `is_new` | Ein boolescher Wert, mit dem ermittelt wird, ob ein Datensatz der erste einer Sitzung ist |
| `depth` | Tiefe des aktuellen Datensatzes innerhalb der Sitzung |

#### Abfrage

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

Die Verknüpfung von Kundenaktionen mit Erfolgen ist ein wichtiger Teil des Verständnisses der Faktoren, die das Kundenerlebnis beeinflussen. Die folgenden ADFs unterstützen die Zuordnung &quot;Erste&quot;und &quot;Letzte&quot;mit unterschiedlichen Ablaufeinstellungen.

Weitere Informationen zur Zuordnung in Adobe Analytics finden Sie in der Übersicht über die [Zuordnungs-IQ](https://docs.adobe.com/content/help/de-DE/analytics/analyze/analysis-workspace/panels/attribution.html) im Analytics-Analytics-Handbuch.

### First Touch-Zuordnung

Gibt den First Touch-Zuordnungswert und Details für einen einzelnen Kanal im ExperienceEvent-Datensatz der Zielgruppe zurück. Die Abfrage gibt ein `struct` Objekt mit dem First Touch-Wert, dem Zeitstempel und der Zuordnung für jede für den ausgewählten Kanal zurückgegebene Zeile zurück.

Diese Abfrage ist nützlich, wenn Sie sehen möchten, welche Interaktion zu einer Reihe von Kundenaktionen geführt hat. Im unten gezeigten Beispiel wird dem anfänglichen Rückverfolgungscode (`em:946426`) in den ExperienceEvent-Daten eine 100%ige (`1.0`) Verantwortung für die Kundenaktionen zugewiesen, da es sich um die erste Interaktion handelte.

### Spezifikation

Syntax: `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Im Dataset gefundenes Zeitstempelfeld |
| `channelName` | Ein Anzeigename, der als Beschriftung im zurückgegebenen Objekt verwendet wird |
| `channelValue` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist |


| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Die `channelName` als Bezeichnung in der ADF |
| `value` | Der Wert, aus `channelValue` dem die erste Berührung in ExperienceEvent stammt |
| `timestamp` | Der Zeitstempel des ExperienceEvent, bei dem die erste Berührung erfolgte |
| `fraction` | Die Zuordnung der ersten Berührung, ausgedrückt als Bruchkredit |

#### Abfrage

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

### Last Touch-Zuordnung

Gibt den Last Touch-Zuordnungswert und Details für einen einzelnen Kanal im ExperienceEvent-Datensatz der Zielgruppe zurück. Die Abfrage gibt ein `struct` Objekt mit dem Wert für die letzte Berührung, dem Zeitstempel und der Zuordnung für jede für den ausgewählten Kanal zurückgegebene Zeile zurück.

Diese Abfrage ist nützlich, wenn Sie die letzte Interaktion in einer Reihe von Kundenaktionen sehen möchten. Im unten gezeigten Beispiel ist der Rückverfolgungscode im zurückgegebenen Objekt die letzte Interaktion in jedem ExperienceEvent-Datensatz. Jeder Code wird 100% (`1.0`) Verantwortung für die Kundenaktionen zugeschrieben, da es die letzte Interaktion war.

### Spezifikation

Syntax: `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Im Dataset gefundenes Zeitstempelfeld |
| `channelName` | Ein Anzeigename, der als Beschriftung im zurückgegebenen Objekt verwendet wird |
| `channelValue` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist |


| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Die `channelName` als Bezeichnung in der ADF |
| `value` | Der Wert, aus `channelValue` dem die letzte Berührung in ExperienceEvent stammt |
| `timestamp` | Der Zeitstempel des ExperienceEvent, in dem das `channelValue` Ereignis verwendet wurde |
| `fraction` | Die Zuordnung der letzten Berührung, ausgedrückt als Bruchkredit |

#### Abfrage

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

### First Touch-Zuordnung mit Ablaufbedingung

Gibt den First Touch-Zuordnungswert und Details für einen einzelnen Kanal im ExperienceEvent-Datensatz der Zielgruppe zurück, der nach oder vor einer Bedingung abläuft. Die Abfrage gibt ein `struct` Objekt mit dem First Touch-Wert, dem Zeitstempel und der Zuordnung für jede für den ausgewählten Kanal zurückgegebene Zeile zurück.

Diese Abfrage ist nützlich, wenn Sie sehen möchten, welche Interaktion zu einer Reihe von Kundenaktionen innerhalb eines Teils des ExperienceEvent-Datensatzes geführt hat, der durch eine bestimmte Bedingung Ihrer Wahl bestimmt wurde. Im folgenden Beispiel wird ein Kauf an jedem der vier in den Ergebnissen angezeigten Tage (15. Juli, 21. Juli 23. und 29. Juli) aufgezeichnet (`commerce.purchases.value IS NOT NULL`) und der anfängliche Rückverfolgungscode an jedem Tag wird 100% (`1.0`) Verantwortung für die Kundenaktionen zugewiesen.

#### Spezifikation

Syntax: `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Im Dataset gefundenes Zeitstempelfeld |
| `channelName` | Ein Anzeigename, der als Beschriftung im zurückgegebenen Objekt verwendet wird |
| `channelValue` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist |
| `expCondition` | Die Bedingung, die den Ablaufpunkt des Kanals bestimmt |
| `expBefore` | Die Standardeinstellung ist `false`. Boolescher Wert, der angibt, ob der Kanal vor oder nach Erfüllung der angegebenen Bedingung abläuft. Primär für Sitzungsablaufbedingungen aktiviert (z. B. `sess.depth = 1, true`), um sicherzustellen, dass die erste Berührung nicht aus einer vorherigen Sitzung ausgewählt wird. |

| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Die `channelName` als Bezeichnung in der ADF |
| `value` | Der Wert, aus `channelValue` dem die erste Berührung im ExperienceEvent vor dem `expCondition` |
| `timestamp` | Der Zeitstempel des ExperienceEvent, bei dem die erste Berührung erfolgte |
| `fraction` | Die Zuordnung der ersten Berührung, ausgedrückt als Bruchkredit |

#### Abfrage

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

### First Touch-Zuordnung mit Ablauftimeout

Gibt den First Touch-Zuordnungswert und Details für einen einzelnen Kanal im ExperienceEvent-Datensatz der Zielgruppe für einen bestimmten Zeitraum zurück. Die Abfrage gibt ein `struct` Objekt mit dem First Touch-Wert, dem Zeitstempel und der Zuordnung für jede für den ausgewählten Kanal zurückgegebene Zeile zurück. Diese Abfrage ist hilfreich, wenn Sie sehen möchten, welche Interaktion innerhalb eines bestimmten Zeitraums zu einer Kundenaktion führte. Im unten gezeigten Beispiel ist die erste Berührung, die für jede Kundenaktion zurückgegeben wird, die früheste Interaktion innerhalb der letzten sieben Tage (`expTimeout = 86400 * 7`).

#### Spezifikation

Syntax: `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Im Dataset gefundenes Zeitstempelfeld |
| `channelName` | Ein Anzeigename, der als Beschriftung im zurückgegebenen Objekt verwendet wird |
| `channelValue` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist |
| `expTimeout` | Das Zeitfenster (in Sekunden) vor dem Kanal-Ereignis, in dem die Abfrage nach einem First Touch-Ereignis sucht |

| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Die `channelName` als Bezeichnung in der ADF |
| `value` | Der Wert, von `channelValue` dem die erste Berührung innerhalb des angegebenen `expTimeout` Intervalls ausgeht |
| `timestamp` | Der Zeitstempel des ExperienceEvent, bei dem die erste Berührung erfolgte |
| `fraction` | Die Zuordnung der ersten Berührung, ausgedrückt als Bruchkredit |

#### Abfrage

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

### Last Touch-Zuordnung mit Ablaufbedingung

Gibt den Last Touch-Zuordnungswert und Details für einen einzelnen Kanal im ExperienceEvent-Datensatz der Zielgruppe zurück, der nach oder vor einer Bedingung abläuft. Die Abfrage gibt ein `struct` Objekt mit dem Wert für die letzte Berührung, dem Zeitstempel und der Zuordnung für jede für den ausgewählten Kanal zurückgegebene Zeile zurück. Diese Abfrage ist nützlich, wenn Sie die letzte Interaktion in einer Reihe von Kundenaktionen innerhalb eines Teils des ExperienceEvent-Datensatzes sehen möchten, der durch eine bestimmte Bedingung Ihrer Wahl bestimmt wird. Im folgenden Beispiel wird ein Kauf an jedem der vier in den Ergebnissen angezeigten Tage (15. Juli, 21. Juli 23. und 29. Juli) aufgezeichnet (`commerce.purchases.value IS NOT NULL`) und der letzte Rückverfolgungscode an jedem Tag wird 100% (`1.0`) Verantwortung für die Kundenaktionen zugewiesen.

#### Spezifikation

Syntax: `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Im Dataset gefundenes Zeitstempelfeld |
| `channelName` | Ein Anzeigename, der als Beschriftung im zurückgegebenen Objekt verwendet wird |
| `channelValue` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist |
| `expCondition` | Die Bedingung, die den Ablaufpunkt des Kanals bestimmt |
| `expBefore` | Die Standardeinstellung ist `false`. Boolescher Wert, der angibt, ob der Kanal vor oder nach Erfüllung der angegebenen Bedingung abläuft. Primär für Sitzungsablaufbedingungen aktiviert (z. B. `sess.depth = 1, true`), um sicherzustellen, dass die letzte Berührung nicht aus einer vorherigen Sitzung ausgewählt wird. |

| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Die `channelName` als Bezeichnung in der ADF |
| `value` | Der Wert, aus `channelValue` dem die letzte Berührung im ExperienceEvent vor dem `expCondition` |
| `timestamp` | Der Zeitstempel des ExperienceEvent, bei dem die letzte Berührung aufgetreten ist |
| `percentage` | Die Zuordnung der letzten Berührung, ausgedrückt als Bruchkredit |

#### Abfrage

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

### Last Touch-Zuordnung mit Ablauftimeout

Gibt den Last Touch-Zuordnungswert und Details für einen einzelnen Kanal im ExperienceEvent-Datensatz der Zielgruppe für einen bestimmten Zeitraum zurück. Die Abfrage gibt ein `struct` Objekt mit dem Wert für die letzte Berührung, dem Zeitstempel und der Zuordnung für jede für den ausgewählten Kanal zurückgegebene Zeile zurück. Diese Abfrage ist hilfreich, wenn Sie die letzte Interaktion innerhalb eines bestimmten Zeitintervalls sehen möchten. Im unten gezeigten Beispiel ist die letzte für jede Kundenaktion zurückgegebene Berührung die letzte Interaktion innerhalb der folgenden sieben Tage (`expTimeout = 86400 * 7`).

#### Spezifikation

Syntax: `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Im Dataset gefundenes Zeitstempelfeld |
| `channelName` | Ein Anzeigename, der als Beschriftung im zurückgegebenen Objekt verwendet wird |
| `channelValue` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist |
| `expTimeout` | Das Zeitfenster (in Sekunden) nach dem Kanal-Ereignis, in dem die Abfrage nach einem Last Touch-Ereignis sucht |

| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `name` | Die `channelName` als Bezeichnung in der ADF |
| `value` | Der Wert, aus `channelValue` dem die letzte Berührung innerhalb des angegebenen `expTimeout` Intervalls stammt |
| `timestamp` | Der Zeitstempel des ExperienceEvent, bei dem die letzte Berührung aufgetreten ist |
| `percentage` | Die Zuordnung der letzten Berührung, ausgedrückt als Bruchkredit |

#### Abfrage

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

## Vorherige/nächste Berührung

Es ist wichtig zu verstehen, wie Kunden innerhalb eines Erlebnisses navigieren. Sie können verwendet werden, um die Einsatztiefe des Kunden zu verstehen, die beabsichtigten Schritte eines Erlebnisses wie vorgesehen zu überprüfen und potenzielle Schmerzpunkte zu identifizieren, die den Kunden beeinträchtigen. Die folgenden ADFs unterstützen die Erstellung von Pfadsetzungseinstellungen aus ihren Beziehungen &quot;Zurück&quot;und &quot;Weiter&quot;. Sie können &quot;Vorherige Seite&quot;und &quot;Nächste Seite&quot;erstellen oder mehrere Ereignis durchlaufen, um Pfade zu erstellen.

### Vorherige Berührung

Legt den vorherigen Wert eines bestimmten Felds fest, der innerhalb des Fensters eine bestimmte Anzahl von Schritten entfernt ist. Beachten Sie im Beispiel, dass die `WINDOW` Funktion mit einem Frame konfiguriert ist, in dem die ADF die aktuelle Zeile und alle davor `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` ansieht.

#### Spezifikation

Syntax: `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `key` | Die Spalte oder das Feld aus dem Ereignis. |
| `shift` | (Optional) Die Anzahl der Ereignis außerhalb des aktuellen Ereignisses. Der Standardwert ist 1. |
| `ingnoreNulls` | Boolescher Wert, der angibt, ob Null- `key` Werte ignoriert werden sollen. Der Standardwert ist `false`. |


| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `value` | Der Wert, der auf der im ADF `key` verwendeten |

#### Abfrage

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

### Nächste Berührung

Legt den nächsten Wert eines bestimmten Felds fest, der innerhalb des Fensters eine bestimmte Anzahl von Schritten entfernt ist. Beachten Sie im Beispiel, dass die `WINDOW` Funktion mit einem Frame konfiguriert ist, in dem die ADF die aktuelle Zeile und alle darauf folgenden Zeilen `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` anzeigt.

#### Spezifikation

Syntax: `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `key` | Die Spalte oder das Feld im Ereignis |
| `shift` | (Optional) Die Anzahl der Ereignis außerhalb des aktuellen Ereignisses. Der Standardwert ist 1. |
| `ingnoreNulls` | Boolescher Wert, der angibt, ob Null- `key` Werte ignoriert werden sollen. Der Standardwert ist `false`. |


| Zurückgegebene Objektparameter | Beschreibung |
| ---------------------- | ------------- |
| `value` | Der Wert, der auf der im ADF `key` verwendeten |

#### Abfrage

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

## Zeit dazwischen

Mit der Zeit-zwischen können Sie das latente Kundenverhalten innerhalb eines Zeitraums vor oder nach dem Eintreten eines Ereignisses untersuchen. Sehen Sie sich die Ereignis innerhalb von 7 Tagen nach einer Kampagne oder einem anderen Ereignis für alle Ihre Kunden an.

### Zeit zwischen vorheriger Übereinstimmung

Stellt eine neue Dimension bereit, die die seit einem bestimmten Vorfall verstrichene Zeit misst.

#### Spezifikation

Syntax: `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Zeitstempelfeld im Datensatz, der auf allen Ereignissen ausgefüllt ist. |
| `eventDefintion` | Ausdruck zum Qualifizieren des vorherigen Ereignisses. |
| `timeUnit` | Einheit der Ausgabe: Tage, Stunden, Minuten und Sekunden. Der Standardwert ist Sekunden. |

Ausgabe: Gibt eine Zahl zurück, die die Zeiteinheit seit der Anzeige des vorherigen übereinstimmenden Ereignisses darstellt oder Null bleibt, wenn kein übereinstimmendes Ereignis gefunden wurde.

#### Abfrage

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

### Nächste Übereinstimmung zwischen Datum und Uhrzeit

Stellt eine neue Dimension bereit, die die Zeit misst, bevor ein bestimmtes Ereignis eintritt.

#### Spezifikation

Syntax: `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])` 

| Parameter | Beschreibung |
| --- | --- |
| `timestamp` | Zeitstempelfeld im Datensatz, der auf allen Ereignissen ausgefüllt ist. |
| `eventDefintion` | Ausdruck, um das nächste Ereignis zu qualifizieren. |
| `timeUnit` | Einheit der Ausgabe: Tage, Stunden, Minuten und Sekunden. Der Standardwert ist Sekunden. |

Ausgabe: Gibt eine negative Zahl zurück, die die Zeiteinheit hinter dem nächsten übereinstimmenden Ereignis darstellt, oder bleibt null, wenn kein übereinstimmendes Ereignis gefunden wird.

#### Abfrage

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

Mithilfe der hier beschriebenen Funktionen können Sie Abfragen schreiben, um mithilfe des Abfrage Service auf Ihre eigenen ExperienceEvent-Datensätze zuzugreifen. Weitere Informationen zu Authoring-Abfragen im Abfrage-Dienst finden Sie in der Dokumentation zum [Erstellen von Abfragen](../creating-queries/creating-queries.md).
