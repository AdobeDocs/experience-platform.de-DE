---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Adobe-definierte Funktionen; SQL;
solution: Experience Platform
title: Adobe-definierte SQL-Funktionen in Query Service
topic-legacy: functions
description: Dieses Dokument enthält Informationen zu den in Adobe Experience Platform Query Service verfügbaren Adobe-definierten Funktionen.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: 63b6236a7e3689afb2ebaa763349b3102697424e
workflow-type: tm+mt
source-wordcount: '2913'
ht-degree: 22%

---

# Adobe-definierte SQL-Funktionen in Query Service

Adobe-definierte Funktionen, hier ADFs genannt, sind vordefinierte Funktionen in Adobe Experience Platform Query Service, mit denen gängige geschäftsbezogene Aufgaben für [!DNL Experience Event] Daten. Dazu gehören Funktionen für [Sessionization](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) und [Attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=de) wie in Adobe Analytics.

Dieses Dokument enthält Informationen zu den in der Adobe definierten Funktionen. [!DNL Query Service].

## Window-Funktionen {#window-functions}

Ein großer Teil der Business-Logik setzt voraus, die Kontaktpunkte (bzw. „Touchpoints“) zu erfassen, an denen ein Kunde mit Ihrem Unternehmen interagiert, und diese nach dem Zeitpunkt ihres Eintretens zu sortieren. Diese Unterstützung wird von [!DNL Spark] SQL in Form von Fensterfunktionen. Window-Funktionen sind Teil von Standard-SQL und werden von einer Vielzahl anderer SQL-Engines unterstützt.

Eine Window-Funktion aktualisiert eine Aggregation und gibt für jede Zeile in Ihrer sortierten Untergruppe ein einzelnes Element zurück. Die einfachste Aggregationsfunktion lautet `SUM()`. `SUM()` berechnet aus den von Ihnen angegebenen Zeilen die Summe. Wenden Sie `SUM()` stattdessen auf ein Fenster an, wird es in eine Window-Funktion umgewandelt und die kumulative Summe für jede Zeile ausgegeben.

Die Mehrheit der [!DNL Spark] SQL-Helfer sind Window-Funktionen, die jede Zeile in Ihrem Fenster aktualisieren, wobei der Status dieser Zeile hinzugefügt wird.

**Abfragesyntax**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `{PARTITION}` | Eine auf einer Spalte oder einem verfügbaren Feld basierende Untergruppe von Zeilen. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Eine Spalte oder ein verfügbares Feld zur Sortierung der Zeilen-Untergruppe. | `ORDER BY timestamp` |
| `{FRAME}` | Eine Untergruppe der Zeilen in einer Partition. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionization

Wenn Sie mit [!DNL Experience Event] Daten aus einer Website, Mobile App, einem interaktiven Sprachreaktionssystem oder einem anderen Kanal zur Kundeninteraktion helfen Ihnen dabei, Ereignisse nach einem bestimmten Aktivitätszeitraum zu gruppieren. In der Regel fußt eine Aktivität auf einer bestimmten Absicht wie der Suche nach einem Produkt, der Zahlung einer Rechnung, dem Abrufen des Kontostandes, dem Ausfüllen eines Formulars etc.

Diese Gruppierung oder Sitzungserstellung von Daten hilft bei der Zuordnung der Ereignisse, um mehr Kontext über das Kundenerlebnis zu finden.

Weitere Informationen zur Sitzungserstellung in Adobe Analytics finden Sie in der Dokumentation unter [kontextbezogene Sitzungen](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

**Abfragesyntax**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{EXPIRATION_IN_SECONDS}` | Die Anzahl der Sekunden, die zwischen Ereignissen erforderlich sind, um das Ende der aktuellen Sitzung und den Beginn einer neuen Sitzung zu qualifizieren. |

Eine Erläuterung der Parameter innerhalb der `OVER()` -Funktion finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `session` Spalte. Die `session` -Spalte besteht aus den folgenden Komponenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameter | Beschreibung |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Die Zeitdifferenz in Sekunden zwischen dem aktuellen und dem vorherigen Datensatz. |
| `{NUM}` | Eine eindeutige Sitzungsnummer, beginnend bei 1, für den Schlüssel, der in der Variablen `PARTITION BY` der Window-Funktion. |
| `{IS_NEW}` | Ein boolescher Wert, der angibt, ob ein Datensatz der erste einer Sitzung ist. |
| `{DEPTH}` | Die Tiefe des aktuellen Datensatzes innerhalb der Sitzung. |

### SESS_START_IF

Diese Abfrage gibt den Sitzungsstatus für die aktuelle Zeile basierend auf dem aktuellen Zeitstempel und dem angegebenen Ausdruck zurück und startet eine neue Sitzung mit der aktuellen Zeile.

**Abfragesyntax**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{TEST_EXPRESSION}` | Ein Ausdruck, mit dem Sie die Datenfelder überprüfen möchten. Beispiel: `application.launches > 0`. |

Eine Erläuterung der Parameter innerhalb der `OVER()` -Funktion finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `session` Spalte. Die `session` -Spalte besteht aus den folgenden Komponenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameter | Beschreibung |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Die Zeitdifferenz in Sekunden zwischen dem aktuellen und dem vorherigen Datensatz. |
| `{NUM}` | Eine eindeutige Sitzungsnummer, beginnend bei 1, für den Schlüssel, der in der Variablen `PARTITION BY` der Window-Funktion. |
| `{IS_NEW}` | Ein boolescher Wert, der angibt, ob ein Datensatz der erste einer Sitzung ist. |
| `{DEPTH}` | Die Tiefe des aktuellen Datensatzes innerhalb der Sitzung. |

### SESS_END_IF

Diese Abfrage gibt den Sitzungsstatus für die aktuelle Zeile basierend auf dem aktuellen Zeitstempel und dem angegebenen Ausdruck zurück, beendet die aktuelle Sitzung und startet in der nächsten Zeile eine neue Sitzung.

**Abfragesyntax**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{TEST_EXPRESSION}` | Ein Ausdruck, mit dem Sie die Datenfelder überprüfen möchten. Beispiel: `application.launches > 0`. |

Eine Erläuterung der Parameter innerhalb der `OVER()` -Funktion finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `session` Spalte. Die `session` -Spalte besteht aus den folgenden Komponenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameter | Beschreibung |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Die Zeitdifferenz in Sekunden zwischen dem aktuellen und dem vorherigen Datensatz. |
| `{NUM}` | Eine eindeutige Sitzungsnummer, beginnend bei 1, für den Schlüssel, der in der Variablen `PARTITION BY` der Window-Funktion. |
| `{IS_NEW}` | Ein boolescher Wert, der angibt, ob ein Datensatz der erste einer Sitzung ist. |
| `{DEPTH}` | Die Tiefe des aktuellen Datensatzes innerhalb der Sitzung. |

## Attribution

Die Zuordnung von Kundenaktionen zum Erfolg ist ein wichtiger Teil des Verständnisses der Faktoren, die Kundenerlebnisse beeinflussen. Die folgenden ADFs unterstützen die Erstkontakt- und Letztkontakt-Attribution mit unterschiedlichen Ablaufeinstellungen.

Weitere Informationen zur Attribution in Adobe Analytics finden Sie unter [Übersicht über Attribution IQ](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html) im [!DNL Analytics] Handbuch zum Attributionsbedienfeld.

### Erstkontakt-Attribution

Diese Abfrage gibt den Attributionswert des Erstkontakts und Details für einen einzelnen Kanal in der Zielgruppe zurück. [!DNL Experience Event] Datensatz. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des Erstkontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage hilft dabei nachzuvollziehen, welche Interaktion zu einer Reihe von Kundenaktionen geführt hat. Im folgenden Beispiel wird der ursprüngliche Trackingcode (`em:946426`) im [!DNL Experience Event] Daten werden zu 100 % (`1.0`) die Verantwortung für die Kundenaktionen übernehmen, da dies die erste Interaktion war.

**Abfragesyntax**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Bezeichnung für das zurückgegebene Objekt. |
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das den Zielkanal für die Abfrage darstellt. |

Eine Erläuterung der Parameter in `OVER()` finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `first_touch` Spalte. Die `first_touch` -Spalte besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, der in der ADF als Titel eingetragen wurde. |
| `{VALUE}` | Der Wert aus `{CHANNEL_VALUE}`, der den Erstkontakt im darstellt.[!DNL Experience Event] |
| `{TIMESTAMP}` | Der Zeitstempel der [!DNL Experience Event] wobei der Erstkontakt erfolgte. |
| `{FRACTION}` | Die Attribution des Erstkontakts, ausgedrückt als Dezimalbruch. |

### Letztkontakt-Attribution

Diese Abfrage gibt den Attributionswert des letzten Kontakts und Details für einen einzelnen Kanal in der Zielgruppe zurück. [!DNL Experience Event] Datensatz. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage hilft dabei, die letzte Interaktion in einer Reihe von Kundenaktionen nachzuvollziehen. Im folgenden Beispiel stellt der Trackingcode im zurückgegebenen Objekt die letzte Interaktion in jeder [!DNL Experience Event] aufzeichnen. Jedem Code werden 100 % (`1.0`) Verantwortung für die Kundenaktionen, da dies die letzte Interaktion war.

**Abfragesyntax**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Bezeichnung des zurückgegebenen Objekts. |
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das den Zielkanal für die Abfrage darstellt. |

Eine Erläuterung der Parameter in `OVER()` finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `last_touch` Spalte. Die `last_touch` -Spalte besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, der in der ADF als Titel eingetragen wurde. |
| `{VALUE}` | Der Wert aus `{CHANNEL_VALUE}`, der den letzten Kontakt im darstellt.[!DNL Experience Event] |
| `{TIMESTAMP}` | Der Zeitstempel der [!DNL Experience Event] wobei `channelValue` verwendet wurde. |
| `{FRACTION}` | Die Attribution des letzten Kontakts, ausgedrückt als Dezimalbruch. |

### Erstkontakt-Attribution mit Ablaufbedingung

Diese Abfrage gibt den Attributionswert des Erstkontakts und Details für einen einzelnen Kanal in der Zielgruppe zurück. [!DNL Experience Event] Datensatz, der nach oder vor einer Bedingung abläuft. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des Erstkontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage ist nützlich, wenn Sie sehen möchten, welche Interaktion zu einer Reihe von Kundenaktionen innerhalb eines Teils der [!DNL Experience Event] Datensatz, der durch eine von Ihnen ausgewählte Bedingung bestimmt wird. Im nachfolgenden Beispiel wird ein Kauf (`commerce.purchases.value IS NOT NULL`) an jedem der vier in den Ergebnissen angezeigten Tage (15., 21., 23. und 29. Juli) aufgezeichnet und dem anfänglichen Trackingcode an jedem Tag ein Anteil von 100 % (`1.0`) am Einfluss auf die Kundenaktionen zugeschrieben.

**Abfragesyntax**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Bezeichnung für das zurückgegebene Objekt. |
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das den Zielkanal für die Abfrage darstellt. |
| `{EXP_CONDITION}` | Die Bedingung, die den Ablaufpunkt des Kanals bestimmt. |
| `{EXP_BEFORE}` | Ein boolescher Wert, der anzeigt, ob der Kanal vor oder nach der angegebenen Bedingung abläuft, `{EXP_CONDITION}`, wird erfüllt. Dies ist in erster Linie für die Ablaufbedingungen einer Sitzung aktiviert, um sicherzustellen, dass der Erstkontakt nicht aus einer vorherigen Sitzung ausgewählt wird. Standardmäßig ist dieser Wert auf `false` gesetzt. |

Eine Erläuterung der Parameter innerhalb der `OVER()` -Funktion finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `first_touch` Spalte. Die `first_touch` -Spalte besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, der in der ADF als Titel eingetragen wurde. |
| `{VALUE}` | Der Wert aus `CHANNEL_VALUE}` Dies ist der erste Kontakt in der [!DNL Experience Event], bevor `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | Der Zeitstempel der [!DNL Experience Event] wobei der Erstkontakt erfolgte. |
| `{FRACTION}` | Die Attribution des Erstkontakts, ausgedrückt als Dezimalbruch. |

### Erstkontakt-Attribution mit Ablauftimeout

Diese Abfrage gibt den Attributionswert des Erstkontakts und Details für einen einzelnen Kanal in der Zielgruppe zurück. [!DNL Experience Event] Datensatz für einen bestimmten Zeitraum. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des Erstkontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

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
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das den Zielkanal für die Abfrage darstellt. |
| `{EXP_TIMEOUT}` | Das Zeitfenster vor dem Kanalereignis in Sekunden, in dem die Abfrage nach einem Erstkontaktereignis sucht. |

Eine Erläuterung der Parameter innerhalb der `OVER()` -Funktion finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `first_touch` Spalte. Die `first_touch` -Spalte besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, der in der ADF als Titel eingetragen wurde. |
| `{VALUE}` | Der Wert aus `CHANNEL_VALUE}` Dies ist der Erstkontakt innerhalb des angegebenen `{EXP_TIMEOUT}` Intervall. |
| `{TIMESTAMP}` | Der Zeitstempel der [!DNL Experience Event] wobei der Erstkontakt erfolgte. |
| `{FRACTION}` | Die Attribution des Erstkontakts, ausgedrückt als Dezimalbruch. |

### Letztkontakt-Attribution mit Ablaufbedingung

Diese Abfrage gibt den Attributionswert des letzten Kontakts und Details für einen einzelnen Kanal in der Zielgruppe zurück. [!DNL Experience Event] Datensatz, der nach oder vor einer Bedingung abläuft. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage ist nützlich, wenn Sie die letzte Interaktion in einer Reihe von Kundenaktionen innerhalb eines Teils der [!DNL Experience Event] Datensatz, der durch eine von Ihnen ausgewählte Bedingung bestimmt wird. Im nachfolgenden Beispiel wird ein Kauf (`commerce.purchases.value IS NOT NULL`) an jedem der vier in den Ergebnissen angezeigten Tage (15., 21., 23. und 29. Juli) festgehalten und dem letzten Trackingcode an jedem Tag ein Anteil von 100 % (`1.0`) am Einfluss auf die Kundenaktionen zugeschrieben.

**Abfragesyntax**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld im Datensatz. |
| `{CHANNEL_NAME}` | Die Bezeichnung für das zurückgegebene Objekt. |
| `{CHANNEL_VALUE}` | Die Spalte oder das Feld, die bzw. das den Zielkanal für die Abfrage darstellt. |
| `{EXP_CONDITION}` | Die Bedingung, die den Ablaufpunkt des Kanals bestimmt. |
| `{EXP_BEFORE}` | Ein boolescher Wert, der anzeigt, ob der Kanal vor oder nach der angegebenen Bedingung abläuft, `{EXP_CONDITION}`, wird erfüllt. Dies ist in erster Linie für die Ablaufbedingungen einer Sitzung aktiviert, um sicherzustellen, dass der Erstkontakt nicht aus einer vorherigen Sitzung ausgewählt wird. Standardmäßig ist dieser Wert auf `false` gesetzt. |

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `last_touch` Spalte. Die `last_touch` -Spalte besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, der in der ADF als Titel eingetragen wurde. |
| `{VALUE}` | Der Wert aus `{CHANNEL_VALUE}` Dies ist der letzte Kontakt im [!DNL Experience Event], bevor `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | Der Zeitstempel der [!DNL Experience Event] wobei der letzte Kontakt aufgetreten ist. |
| `{FRACTION}` | Die Attribution des letzten Kontakts, ausgedrückt als Dezimalbruch. |

### Letztkontakt-Attribution mit Ablauftimeout

Diese Abfrage gibt den Attributionswert des letzten Kontakts und Details für einen einzelnen Kanal in der Zielgruppe zurück. [!DNL Experience Event] Datensatz für einen bestimmten Zeitraum. Die Abfrage liefert ein `struct`-Objekt mit dem Wert des letzten Kontakts, dem Zeitstempel sowie der Attribution für jede für den ausgewählten Kanal zurückgegebene Zeile.

Diese Abfrage hilft dabei, die letzte Interaktion in einem bestimmten Zeitintervall nachzuvollziehen. Im nachfolgenden Beispiel stellt der für die einzelnen Kundeninteraktionen zurückgegebene letzte Kontakt die finale Interaktion innerhalb der darauffolgenden sieben Tage (`expTimeout = 86400 * 7`) dar.

**Abfragesyntax**

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
| `{EXP_TIMEOUT}` | Das Zeitfenster, in dem die Abfrage nach einem Letztkontakt-Ereignis sucht (in Sekunden), nach dem das Kanalereignis eintritt. |

Eine Erläuterung der Parameter innerhalb der `OVER()` -Funktion finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `last_touch` Spalte. Die `last_touch` -Spalte besteht aus den folgenden Komponenten:

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| Parameter | Beschreibung |
| ---------- | ----------- |
| `{NAME}` | Die `{CHANNEL_NAME}`, der in der ADF als Titel eingetragen wurde. |
| `{VALUE}` | Der Wert aus `{CHANNEL_VALUE}`, der den letzten Kontakt innerhalb des `{EXP_TIMEOUT}`-Intervalls darstellt. |
| `{TIMESTAMP}` | Der Zeitstempel der [!DNL Experience Event] wo der letzte Kontakt aufgetreten ist |
| `{FRACTION}` | Die Attribution des letzten Kontakts, ausgedrückt als Dezimalbruch. |

## Pathing

Pfade können verwendet werden, um die Interaktionstiefe des Kunden zu verstehen, die beabsichtigten Schritte eines Erlebnisses wie geplant zu bestätigen und potenzielle Schmerzpunkte zu identifizieren, die sich auf den Kunden auswirken.

Die folgenden ADFs unterstützen die Erstellung von Pfadansichten aus ihren vorherigen und nächsten Beziehungen. Sie können vorherige und nächste Seiten erstellen oder mehrere Ereignisse durchlaufen, um Pfade zu erstellen.

### Vorherige Seite

Legt den vorherigen Wert eines bestimmten Felds fest, der innerhalb des Fensters eine festgelegte Anzahl von Schritten entfernt ist. Beachten Sie im Beispiel, dass die Variable `WINDOW` -Funktion mit einem Frame von `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` die ADF so einstellen, dass sie sich die aktuelle Zeile und alle nachfolgenden Zeilen ansieht.

**Abfragesyntax**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{KEY}` | Die Spalte oder das Feld aus dem Ereignis. |
| `{SHIFT}` | (Optional) Die Anzahl der Ereignisse außerhalb des aktuellen Ereignisses. Der Standardwert ist 1. |
| `{IGNORE_NULLS}` | (Optional) Ein boolescher Wert, der angibt, ob null `{KEY}` -Werte ignoriert werden. Standardmäßig lautet der Wert `false`. |

Eine Erläuterung der Parameter innerhalb der `OVER()` -Funktion finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `previous_page` Spalte. Der Wert innerhalb der `previous_page` basiert auf der `{KEY}` wird in der ADF verwendet.

### Nächste Seite

Legt den nächsten Wert eines bestimmten Felds fest, der innerhalb des Fensters eine festgelegte Anzahl von Schritten entfernt ist. Beachten Sie im Beispiel, dass die Variable `WINDOW` -Funktion mit einem Frame von `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` die ADF so einstellen, dass sie sich die aktuelle Zeile und alle nachfolgenden Zeilen ansieht.

**Abfragesyntax**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{KEY}` | Die Spalte oder das Feld aus dem Ereignis. |
| `{SHIFT}` | (Optional) Die Anzahl der Ereignisse außerhalb des aktuellen Ereignisses. Der Standardwert ist 1. |
| `{IGNORE_NULLS}` | (Optional) Ein boolescher Wert, der angibt, ob null `{KEY}` -Werte ignoriert werden. Standardmäßig lautet der Wert `false`. |

Eine Erläuterung der Parameter innerhalb der `OVER()` -Funktion finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `previous_page` Spalte. Der Wert innerhalb der `previous_page` basiert auf der `{KEY}` wird in der ADF verwendet.

## Zeit zwischen

Mit der Zeit-zwischen können Sie das latente Kundenverhalten innerhalb eines bestimmten Zeitraums vor oder nach dem Eintreten eines Ereignisses untersuchen.

### Zeit zwischen vorheriger Übereinstimmung

Diese Abfrage gibt eine Zahl zurück, die die Zeiteinheit seit der Anzeige des vorherigen übereinstimmenden Ereignisses darstellt. Wenn kein übereinstimmendes Ereignis gefunden wurde, wird null zurückgegeben.

**Abfragesyntax**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Ein Zeitstempelfeld im Datensatz, das bei allen Ereignissen aufgefüllt ist. |
| `{EVENT_DEFINITION}` | Der Ausdruck, der das vorherige Ereignis qualifizieren soll. |
| `{TIME_UNIT}` | Die Einheit der Ausgabe. Mögliche Werte sind Tage, Stunden, Minuten und Sekunden. Standardmäßig beträgt der Wert Sekunden. |

Eine Erläuterung der Parameter innerhalb der `OVER()` -Funktion finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `average_minutes_since_registration` Spalte. Der Wert innerhalb der `average_minutes_since_registration` ist die Zeitdifferenz zwischen dem aktuellen und vorherigen Ereignis. Die Zeiteinheit wurde zuvor in der Variablen `{TIME_UNIT}`.

### Zeit zwischen nächster Übereinstimmung

Diese Abfrage gibt eine negative Zahl zurück, die die Zeiteinheit hinter dem nächsten übereinstimmenden Ereignis darstellt. Wenn kein übereinstimmendes Ereignis gefunden wird, wird null zurückgegeben.

**Abfragesyntax**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Ein Zeitstempelfeld im Datensatz, das bei allen Ereignissen aufgefüllt ist. |
| `{EVENT_DEFINITION}` | Der Ausdruck, der das nächste Ereignis qualifizieren soll. |
| `{TIME_UNIT}` | (Optional) Die AusgabEinheit. Mögliche Werte sind Tage, Stunden, Minuten und Sekunden. Standardmäßig beträgt der Wert Sekunden. |

Eine Erläuterung der Parameter innerhalb der `OVER()` -Funktion finden Sie im Abschnitt [Bereich für Fensterfunktionen](#window-functions).

**Beispielabfrage**

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

Die Ergebnisse der angegebenen Beispielabfrage werden im `average_minutes_until_order_confirmation` Spalte. Der Wert innerhalb der `average_minutes_until_order_confirmation` ist die Zeitdifferenz zwischen dem aktuellen und dem nächsten Ereignis. Die Zeiteinheit wurde zuvor in der Variablen `{TIME_UNIT}`.

## Nächste Schritte

Mithilfe der hier beschriebenen Funktionen können Sie Abfragen erstellen, um auf Ihre [!DNL Experience Event] Datensätze mit [!DNL Query Service]. Weitere Informationen zu Authoring-Abfragen finden Sie unter [!DNL Query Service], siehe die Dokumentation unter [Abfragen erstellen](../best-practices/writing-queries.md).

## Weitere Ressourcen

Im folgenden Video erfahren Sie, wie Sie Abfragen in der Adobe Experience Platform-Benutzeroberfläche und in einem PSQL-Client ausführen. Darüber hinaus werden im Video auch Beispiele für einzelne Eigenschaften in einem XDM-Objekt verwendet, Adobe-definierte Funktionen verwendet und CREATE TABLE AS SELECT (CTAS) verwendet.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
