---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;adobe-definierte Funktionen;SQL
solution: Experience Platform
title: Adobe-definierte SQL-Funktionen im Abfrage-Dienst
topic-legacy: functions
description: In diesem Dokument finden Sie Informationen zu Adoben-definierten Funktionen, die im Adobe Experience Platform Abfrage Service verfügbar sind.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2913'
ht-degree: 21%

---

# Adobe-definierte SQL-Funktionen im Abfrage-Dienst

Adobe-definierte Funktionen, hierin ADFs genannt, sind vordefinierte Funktionen im Adobe Experience Platform Abfrage Service, die häufig geschäftsbezogene Aufgaben an [!DNL Experience Event]-Daten durchführen. Dazu gehören Funktionen für [Sessionisation](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) und [Attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html) wie in Adobe Analytics.

Dieses Dokument enthält Informationen zu Adoben-definierten Funktionen, die in [!DNL Query Service] verfügbar sind.

## Window-Funktionen {#window-functions}

Ein großer Teil der Business-Logik setzt voraus, die Kontaktpunkte (bzw. „Touchpoints“) zu erfassen, an denen ein Kunde mit Ihrem Unternehmen interagiert, und diese nach dem Zeitpunkt ihres Eintretens zu sortieren. Diese Unterstützung wird von [!DNL Spark] SQL in Form von Fensterfunktionen bereitgestellt. Window-Funktionen sind Teil von Standard-SQL und werden von einer Vielzahl anderer SQL-Engines unterstützt.

Eine Window-Funktion aktualisiert eine Aggregation und gibt für jede Zeile in Ihrer sortierten Untergruppe ein einzelnes Element zurück. Die einfachste Aggregationsfunktion lautet `SUM()`. `SUM()` berechnet aus den von Ihnen angegebenen Zeilen die Summe. Wenden Sie `SUM()` stattdessen auf ein Fenster an, wird es in eine Window-Funktion umgewandelt und die kumulative Summe für jede Zeile ausgegeben.

Die meisten [!DNL Spark] SQL-Helfer sind Fensterfunktionen, die jede Zeile in Ihrem Fenster mit dem Status dieser Zeile aktualisieren.

**Syntax der Abfrage**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `{PARTITION}` | Eine Untergruppe von Zeilen basierend auf einer Spalte oder einem verfügbaren Feld. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Eine Spalte oder ein verfügbares Feld zur Sortierung der Zeilen-Untergruppe. | `ORDER BY timestamp` |
| `{FRAME}` | Eine Untergruppe der Zeilen in einer Partition. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionization

Wenn Sie mit [!DNL Experience Event]-Daten arbeiten, die von einer Website, einer mobilen Anwendung, einem interaktiven Sprachreaktionssystem oder einem anderen Kanal zur Kundeninteraktion stammen, ist es hilfreich, wenn Ereignis um einen bestimmten Zeitraum der Aktivität gruppiert werden können. In der Regel fußt eine Aktivität auf einer bestimmten Absicht wie der Suche nach einem Produkt, der Zahlung einer Rechnung, dem Abrufen des Kontostandes, dem Ausfüllen eines Formulars etc.

Diese Gruppierung bzw. Sitzungsänderung von Daten hilft, die Ereignis zu verknüpfen, um mehr Kontext über das Kundenerlebnis aufzudecken.

Weitere Informationen zur Sitzungsänderung in Adobe Analytics finden Sie in der Dokumentation zu [kontextsensitiven Sitzungen](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html.

**Syntax der Abfrage**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{EXPIRATION_IN_SECONDS}` | Die Anzahl der Sekunden, die zwischen den Ereignissen für die Qualifizierung des Sitzungsende und des Beginns einer neuen Sitzung benötigt werden. |

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

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

**Ergebnisse**

```console
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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `session` angegeben. Die Spalte `session` besteht aus den folgenden Komponenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameter | Beschreibung |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Der Zeitunterschied in Sekunden zwischen dem aktuellen Datensatz und dem vorherigen Datensatz. |
| `{NUM}` | Eine eindeutige Sitzungsnummer, beginnend bei 1, für den Schlüssel, der in der Funktion `PARTITION BY` des Fensters definiert ist. |
| `{IS_NEW}` | Ein boolescher Wert, der bestimmt, ob ein Datensatz der erste einer Sitzung ist. |
| `{DEPTH}` | Die Tiefe des aktuellen Datensatzes innerhalb der Sitzung. |

### SESS_BEGINN_IF

Diese Abfrage gibt den Sitzungsstatus für die aktuelle Zeile basierend auf dem aktuellen Zeitstempel und dem angegebenen Ausdruck zurück und Beginn eine neue Sitzung mit der aktuellen Zeile.

**Syntax der Abfrage**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{TEST_EXPRESSION}` | Ein Ausdruck, mit dem Sie die Datenfelder prüfen möchten. Beispiel: `application.launches > 0`. |

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Ergebnisse**

```console
                id                |       timestamp       | isLaunch |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `session` angegeben. Die Spalte `session` besteht aus den folgenden Komponenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameter | Beschreibung |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Der Zeitunterschied in Sekunden zwischen dem aktuellen Datensatz und dem vorherigen Datensatz. |
| `{NUM}` | Eine eindeutige Sitzungsnummer, beginnend bei 1, für den Schlüssel, der in der Funktion `PARTITION BY` des Fensters definiert ist. |
| `{IS_NEW}` | Ein boolescher Wert, der bestimmt, ob ein Datensatz der erste einer Sitzung ist. |
| `{DEPTH}` | Die Tiefe des aktuellen Datensatzes innerhalb der Sitzung. |

### SESS_END_IF

Diese Abfrage gibt den Sitzungsstatus für die aktuelle Zeile basierend auf dem aktuellen Zeitstempel und dem angegebenen Ausdruck zurück, beendet die aktuelle Sitzung und Beginn eine neue Sitzung für die nächste Zeile.

**Syntax der Abfrage**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{TEST_EXPRESSION}` | Ein Ausdruck, mit dem Sie die Datenfelder prüfen möchten. Beispiel: `application.launches > 0`. |

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**Ergebnisse**

```console
                id                |       timestamp       | isExit   |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `session` angegeben. Die Spalte `session` besteht aus den folgenden Komponenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameter | Beschreibung |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Der Zeitunterschied in Sekunden zwischen dem aktuellen Datensatz und dem vorherigen Datensatz. |
| `{NUM}` | Eine eindeutige Sitzungsnummer, beginnend bei 1, für den Schlüssel, der in der Funktion `PARTITION BY` des Fensters definiert ist. |
| `{IS_NEW}` | Ein boolescher Wert, der bestimmt, ob ein Datensatz der erste einer Sitzung ist. |
| `{DEPTH}` | Die Tiefe des aktuellen Datensatzes innerhalb der Sitzung. |

## Attribution

Die Verknüpfung von Kundenaktionen mit Erfolgen ist ein wichtiger Teil des Verständnisses der Faktoren, die die Kundenerlebnisse beeinflussen. Die folgenden ADFs unterstützen First Touch- und Last Touch-Zuordnungen mit unterschiedlichen Ablaufeinstellungen.

Weitere Informationen zur Zuordnung in Adobe Analytics finden Sie im Handbuch [Übersicht über den Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html) im Bedienfeld [!DNL Analytics] &quot;Zuordnung&quot;.

### First-Touch-Zuordnung

Diese Abfrage gibt den First Touch-Zuordnungswert und Details für einen einzelnen Kanal im Datensatz der Zielgruppe [!DNL Experience Event] zurück. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des Erstkontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage hilft dabei nachzuvollziehen, welche Interaktion zu einer Reihe von Kundenaktionen geführt hat. Im unten gezeigten Beispiel wird dem anfänglichen Rückverfolgungscode (`em:946426`) in den [!DNL Experience Event]-Daten 100 % (`1.0`)-Verantwortung für die Kundenaktionen zugeordnet, da es sich um die erste Interaktion handelte.

**Syntax der Abfrage**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Bezeichnung für das zurückgegebene Objekt. |
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist. |

Eine Erläuterung der Parameter in `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

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

```console
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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `first_touch` angegeben. Die Spalte `first_touch` besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, die als Beschriftung in der ADF eingegeben wurde. |
| `{VALUE}` | Der Wert aus `{CHANNEL_VALUE}`, der den Erstkontakt im darstellt.[!DNL Experience Event] |
| `{TIMESTAMP}` | Der Zeitstempel des [!DNL Experience Event], bei dem der erste Kontakt auftrat. |
| `{FRACTION}` | Die Zuordnung der ersten Berührung, ausgedrückt als Dezimalbruch. |

### Last-Touch-Zuordnung

Diese Abfrage gibt den Last Touch-Zuordnungswert und Details für einen einzelnen Kanal im Datensatz der Zielgruppe [!DNL Experience Event] zurück. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage hilft dabei, die letzte Interaktion in einer Reihe von Kundenaktionen nachzuvollziehen. Im unten gezeigten Beispiel ist der Rückverfolgungscode im zurückgegebenen Objekt die letzte Interaktion in jedem [!DNL Experience Event]-Datensatz. Jeder Code wird 100 % (`1.0`) Verantwortung für die Kundenaktionen zugeordnet, da es sich um die letzte Interaktion handelte.

**Syntax der Abfrage**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Beschriftung des zurückgegebenen Objekts. |
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist. |

Eine Erläuterung der Parameter in `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

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

```console
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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `last_touch` angegeben. Die Spalte `last_touch` besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, die als Beschriftung in der ADF eingegeben wurde. |
| `{VALUE}` | Der Wert aus `{CHANNEL_VALUE}`, der den letzten Kontakt im darstellt.[!DNL Experience Event] |
| `{TIMESTAMP}` | Der Zeitstempel von [!DNL Experience Event], bei dem `channelValue` verwendet wurde. |
| `{FRACTION}` | Die Zuordnung der letzten Berührung, ausgedrückt als Dezimalbruch. |

### First Touch-Zuordnung mit Ablaufbedingung

Diese Abfrage gibt den First Touch-Zuordnungswert und Details für einen einzelnen Kanal im Dataset der Zielgruppe [!DNL Experience Event] zurück, der nach oder vor einer Bedingung abläuft. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des Erstkontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage ist nützlich, wenn Sie sehen möchten, welche Interaktion zu einer Reihe von Kundenaktionen innerhalb eines Teils des [!DNL Experience Event]-Datensatzes geführt hat, der durch eine von Ihnen gewählte Bedingung bestimmt wurde. Im nachfolgenden Beispiel wird ein Kauf (`commerce.purchases.value IS NOT NULL`) an jedem der vier in den Ergebnissen angezeigten Tage (15., 21., 23. und 29. Juli) aufgezeichnet und dem anfänglichen Trackingcode an jedem Tag ein Anteil von 100 % (`1.0`) am Einfluss auf die Kundenaktionen zugeschrieben.

**Syntax der Abfrage**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Bezeichnung für das zurückgegebene Objekt. |
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist. |
| `{EXP_CONDITION}` | Die Bedingung, die den Ablaufzeitpunkt des Kanals bestimmt. |
| `{EXP_BEFORE}` | Ein boolescher Wert, der angibt, ob der Kanal vor oder nach der angegebenen Bedingung `{EXP_CONDITION}` abläuft. Dies ist primär für die Ablaufbedingungen einer Sitzung aktiviert, um sicherzustellen, dass der erste Kontakt nicht aus einer vorherigen Sitzung ausgewählt wurde. Standardmäßig ist dieser Wert auf `false` gesetzt. |

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `first_touch` angegeben. Die Spalte `first_touch` besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, die als Beschriftung in der ADF eingegeben wurde. |
| `{VALUE}` | Der Wert von `CHANNEL_VALUE}`, der die erste Berührung von [!DNL Experience Event] vor dem `{EXP_CONDITION}` ist. |
| `{TIMESTAMP}` | Der Zeitstempel des [!DNL Experience Event], bei dem der erste Kontakt auftrat. |
| `{FRACTION}` | Die Zuordnung der ersten Berührung, ausgedrückt als Dezimalbruch. |

### First Touch-Zuordnung mit Ablauftimeout

Diese Abfrage gibt den First Touch-Zuordnungswert und Details für einen einzelnen Kanal im Dataset der Zielgruppe [!DNL Experience Event] für einen bestimmten Zeitraum zurück. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des Erstkontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage hilft dabei nachzuvollziehen, welche Interaktion innerhalb eines bestimmten Zeitraums zu einer Kundenaktion geführt hat. Im nachfolgenden Beispiel stellt der für die einzelnen Kundeninteraktionen zurückgegebene Erstkontakt die früheste Interaktion innerhalb der letzten sieben Tage (`expTimeout = 86400 * 7`) dar.

**Spezifikation**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Bezeichnung für das zurückgegebene Objekt. |
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist. |
| `{EXP_TIMEOUT}` | Das Zeitfenster vor dem Kanal-Ereignis in Sekunden, in dem die Abfrage nach einem First Touch-Ereignis sucht. |

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

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

**Ergebnisse**

```console
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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `first_touch` angegeben. Die Spalte `first_touch` besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, die als Beschriftung in der ADF eingegeben wurde. |
| `{VALUE}` | Der Wert von `CHANNEL_VALUE}`, der die erste Berührung innerhalb des angegebenen `{EXP_TIMEOUT}`-Intervalls ist. |
| `{TIMESTAMP}` | Der Zeitstempel des [!DNL Experience Event], bei dem der erste Kontakt auftrat. |
| `{FRACTION}` | Die Zuordnung der ersten Berührung, ausgedrückt als Dezimalbruch. |

### Last Touch-Zuordnung mit Ablaufbedingung

Diese Abfrage gibt den Last Touch-Zuordnungswert und Details für einen einzelnen Kanal im Dataset der Zielgruppe [!DNL Experience Event] zurück, der nach oder vor einer Bedingung abläuft. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage ist nützlich, wenn Sie die letzte Interaktion in einer Reihe von Kundenaktionen innerhalb eines Teils des [!DNL Experience Event]-Datensatzes sehen möchten, der durch eine von Ihnen gewählte Bedingung bestimmt wird. Im nachfolgenden Beispiel wird ein Kauf (`commerce.purchases.value IS NOT NULL`) an jedem der vier in den Ergebnissen angezeigten Tage (15., 21., 23. und 29. Juli) festgehalten und dem letzten Trackingcode an jedem Tag ein Anteil von 100 % (`1.0`) am Einfluss auf die Kundenaktionen zugeschrieben.

**Syntax der Abfrage**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Bezeichnung für das zurückgegebene Objekt. |
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das der Kanal für die Zielgruppe für die Abfrage ist. |
| `{EXP_CONDITION}` | Die Bedingung, die den Ablaufzeitpunkt des Kanals bestimmt. |
| `{EXP_BEFORE}` | Ein boolescher Wert, der angibt, ob der Kanal vor oder nach der angegebenen Bedingung `{EXP_CONDITION}` abläuft. Dies ist primär für die Ablaufbedingungen einer Sitzung aktiviert, um sicherzustellen, dass der erste Kontakt nicht aus einer vorherigen Sitzung ausgewählt wurde. Standardmäßig ist dieser Wert auf `false` gesetzt. |

**Abfrage**

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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `last_touch` angegeben. Die Spalte `last_touch` besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, die als Beschriftung in der ADF eingegeben wurde. |
| `{VALUE}` | Der Wert von `{CHANNEL_VALUE}`, der die letzte Berührung von [!DNL Experience Event] vor dem `{EXP_CONDITION}` ist. |
| `{TIMESTAMP}` | Der Zeitstempel des [!DNL Experience Event], bei dem der letzte Kontakt auftrat. |
| `{FRACTION}` | Die Zuordnung der letzten Berührung, ausgedrückt als Dezimalbruch. |

### Last Touch-Zuordnung mit Ablauftimeout

Diese Abfrage gibt den Last Touch-Zuordnungswert und Details für einen einzelnen Kanal im Dataset der Zielgruppe [!DNL Experience Event] für einen bestimmten Zeitraum zurück. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage hilft dabei, die letzte Interaktion in einem bestimmten Zeitintervall nachzuvollziehen. Im nachfolgenden Beispiel stellt der für die einzelnen Kundeninteraktionen zurückgegebene letzte Kontakt die finale Interaktion innerhalb der darauffolgenden sieben Tage (`expTimeout = 86400 * 7`) dar.

**Syntax der Abfrage**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Beschriftung für das zurückgegebene Objekt |
| `{CHANNEL_VALUE}` | Spalte oder Feld, die bzw. das den Zielkanal für die Abfrage bildet. |
| `{EXP_TIMEOUT}` | Das Zeitfenster nach dem Kanal-Ereignis in Sekunden, in dem die Abfrage nach einem Last Touch-Ereignis sucht. |

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `last_touch` angegeben. Die Spalte `last_touch` besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Das `{CHANNEL_NAME}`, als Bezeichnung in der ADF eingegeben. |
| `{VALUE}` | Der Wert aus `{CHANNEL_VALUE}`, der den letzten Kontakt innerhalb des `{EXP_TIMEOUT}`-Intervalls darstellt. |
| `{TIMESTAMP}` | Der Zeitstempel des [!DNL Experience Event], bei dem die letzte Berührung aufgetreten ist |
| `{FRACTION}` | Die Zuordnung der letzten Berührung, ausgedrückt als Dezimalbruch. |

## Pathing

Pfade können verwendet werden, um die Einsatztiefe des Kunden zu verstehen, die beabsichtigten Schritte eines Erlebnisses wie vorgesehen zu überprüfen und potenzielle Schmerzpunkte zu identifizieren, die den Kunden beeinträchtigen.

Die folgenden ADFs unterstützen die Erstellung von Pfade-Ansichten aus ihren vorherigen und nächsten Beziehungen. Sie können sowohl vorherige als auch nächste Seiten erstellen oder mehrere Ereignis durchlaufen, um Pfade zu erstellen.

### Vorherige Seite

Legt den vorherigen Wert eines bestimmten Felds fest, der innerhalb des Fensters eine festgelegte Anzahl von Schritten entfernt ist. Beachten Sie im Beispiel, dass die Funktion `WINDOW` mit einem Frame von `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` konfiguriert ist, wobei ADF die aktuelle Zeile und alle nachfolgenden Zeilen anzeigt.

**Syntax der Abfrage**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{KEY}` | Die Spalte oder das Feld aus dem Ereignis. |
| `{SHIFT}` | (Optional) Die Anzahl der Ereignis außerhalb des aktuellen Ereignisses. Der Standardwert ist 1. |
| `{IGNORE_NULLS}` | (Optional) Ein boolescher Wert, der angibt, ob null `{KEY}`-Werte ignoriert werden sollen. Der Standardwert ist `false`. |

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**Ergebnisse**

```console
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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `previous_page` angegeben. Der Wert in der Spalte `previous_page` basiert auf dem in der ADF verwendeten `{KEY}`.

### Nächste Seite

Legt den nächsten Wert eines bestimmten Felds fest, der innerhalb des Fensters eine festgelegte Anzahl von Schritten entfernt ist. Beachten Sie im Beispiel, dass die Funktion `WINDOW` mit einem Frame von `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` konfiguriert ist, wobei ADF die aktuelle Zeile und alle nachfolgenden Zeilen anzeigt.

**Syntax der Abfrage**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{KEY}` | Die Spalte oder das Feld aus dem Ereignis. |
| `{SHIFT}` | (Optional) Die Anzahl der Ereignis außerhalb des aktuellen Ereignisses. Der Standardwert ist 1. |
| `{IGNORE_NULLS}` | (Optional) Ein boolescher Wert, der angibt, ob null `{KEY}`-Werte ignoriert werden sollen. Der Standardwert ist `false`. |

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**Ergebnisse**

```console
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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `previous_page` angegeben. Der Wert in der Spalte `previous_page` basiert auf dem in der ADF verwendeten `{KEY}`.

## Zeit zwischen

Mit der Zeit-zwischen können Sie das latente Kundenverhalten innerhalb eines bestimmten Zeitraums vor oder nach dem Eintreten eines Ereignisses untersuchen.

### Zeit zwischen vorheriger Übereinstimmung

Diese Abfrage gibt eine Zeiteinheit zurück, die die Zeiteinheit seit der Anzeige des vorherigen übereinstimmenden Ereignisses darstellt. Wenn kein übereinstimmendes Ereignis gefunden wurde, gibt es null zurück.

**Syntax der Abfrage**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Ein Zeitstempelfeld im Datensatz, das auf allen Ereignissen ausgefüllt ist. |
| `{EVENT_DEFINITION}` | Der Ausdruck, um das vorherige Ereignis zu qualifizieren. |
| `{TIME_UNIT}` | Die Ausgabeeinheit. Mögliche Werte sind Tage, Stunden, Minuten und Sekunden. Der Standardwert ist Sekunden. |

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

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

**Ergebnisse**

```console
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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `average_minutes_since_registration` angegeben. Der Wert in der Spalte `average_minutes_since_registration` ist der Zeitunterschied zwischen dem aktuellen und dem vorherigen Ereignis. Die Zeiteinheit wurde zuvor in `{TIME_UNIT}` definiert.

### Zeit zwischen nächster Übereinstimmung

Diese Abfrage gibt eine negative Zahl zurück, die die Zeiteinheit hinter dem nächsten übereinstimmenden Ereignis darstellt. Wenn kein übereinstimmendes Ereignis gefunden wird, wird null zurückgegeben.

**Syntax der Abfrage**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Ein Zeitstempelfeld im Datensatz, das auf allen Ereignissen ausgefüllt ist. |
| `{EVENT_DEFINITION}` | Der Ausdruck, der das nächste Ereignis qualifiziert. |
| `{TIME_UNIT}` | (Optional) Die Einheit der Ausgabe. Mögliche Werte sind Tage, Stunden, Minuten und Sekunden. Der Standardwert ist Sekunden. |

Eine Erläuterung der Parameter innerhalb der Funktion `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

**Abfrage**

```sql
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

**Ergebnisse**

```console
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

Für die angegebene Beispielspalte werden die Abfragen in der Spalte `average_minutes_until_order_confirmation` angegeben. Der Wert in der Spalte `average_minutes_until_order_confirmation` ist der Zeitunterschied zwischen dem aktuellen und dem nächsten Ereignis. Die Zeiteinheit wurde zuvor in `{TIME_UNIT}` definiert.

## Nächste Schritte

Mithilfe der hier beschriebenen Funktionen können Sie Abfragen schreiben, um mit [!DNL Query Service] auf Ihre eigenen [!DNL Experience Event]-Datensätze zuzugreifen. Weitere Informationen zu Authoring-Abfragen in [!DNL Query Service] finden Sie in der Dokumentation zu [Erstellen von Abfragen](../best-practices/writing-queries.md).

## Zusätzliche Ressourcen

Das folgende Video zeigt, wie Abfragen auf der Adobe Experience Platform-Oberfläche und in einem PSQL-Client ausgeführt werden. Darüber hinaus verwendet das Video Beispiele für einzelne Eigenschaften in einem XDM-Objekt, für die Verwendung von Adobe-definierten Funktionen und für die Verwendung von CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
