---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;von Adobe definierte Funktionen;SQL;
solution: Experience Platform
title: Adobe-definierte SQL-Funktionen im Abfrage-Service
description: Dieses Dokument enthält Informationen zu in Adobe definierten Funktionen, die im Abfrage-Service von Adobe Experience Platform verfügbar sind.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 13%

---

# Adobe-definierte SQL-Funktionen im Abfrage-Service

Adobe-definierte Funktionen, hier als ADFs bezeichnet, sind vordefinierte Funktionen im Abfrage-Service von Adobe Experience Platform, die Sie bei der Durchführung gängiger geschäftsbezogener Aufgaben im Zusammenhang mit [!DNL Experience Event] unterstützen. Dazu gehören Funktionen für [Sessionization](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html?lang=de) und [Attribution](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=de) wie die in Adobe Analytics.

Dieses Dokument enthält Informationen zu in Adobe definierten Funktionen, die in [!DNL Query Service] verfügbar sind.

>[!NOTE]
>
>Die Experience Cloud ID (ECID) wird auch als MCID bezeichnet und weiterhin in Namespaces verwendet.

## Window-Funktionen {#window-functions}

Ein großer Teil der Business-Logik setzt voraus, die Kontaktpunkte (bzw. „Touchpoints“) zu erfassen, an denen ein Kunde mit Ihrem Unternehmen interagiert, und diese nach dem Zeitpunkt ihres Eintretens zu sortieren. Diese Unterstützung wird durch [!DNL Spark] SQL in Form von Fensterfunktionen bereitgestellt. Window-Funktionen sind Teil von Standard-SQL und werden von einer Vielzahl anderer SQL-Engines unterstützt.

Eine Window-Funktion aktualisiert eine Aggregation und gibt für jede Zeile in Ihrer sortierten Teilmenge ein einzelnes Element zurück. Die einfachste Aggregationsfunktion lautet `SUM()`. `SUM()` berechnet aus den von Ihnen angegebenen Zeilen die Summe. Wenden Sie `SUM()` stattdessen auf ein Fenster an, wird es in eine Window-Funktion umgewandelt und die kumulative Summe für jede Zeile ausgegeben.

Der Großteil der [!DNL Spark] SQL-Helper sind Fensterfunktionen, die jede Zeile im Fenster aktualisieren, wobei der Status dieser Zeile hinzugefügt wird.

**Abfragesyntax**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `{PARTITION}` | Eine Untergruppe von Zeilen basierend auf einer Spalte oder einem verfügbaren Feld. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | Eine Spalte oder ein verfügbares Feld, die bzw. das zum Sortieren der Teilmenge oder Zeilen verwendet wird. | `ORDER BY timestamp` |
| `{FRAME}` | Eine Untergruppe der Zeilen in einer Partition. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## Sessionization

Wenn Sie mit [!DNL Experience Event] Daten arbeiten, die von einer Website, einer Mobile App, einem interaktiven Sprachantwortsystem oder einem anderen Kundeninteraktionskanal stammen, ist es hilfreich, wenn Ereignisse um einen damit verbundenen Zeitraum gruppiert werden können. In der Regel verfolgen Sie eine bestimmte Absicht, Ihre Aktivität voranzutreiben, z. B. die Suche nach einem Produkt, die Bezahlung einer Rechnung, die Überprüfung des Kontostands, das Ausfüllen einer Anwendung usw.

Diese Gruppierung oder Sitzungserstellung von Daten hilft bei der Verknüpfung der Ereignisse, um mehr Kontext über das Kundenerlebnis zu erfahren.

Weitere Informationen zur Sitzungserstellung in Adobe Analytics finden Sie in der Dokumentation unter [Kontextabhängige Sitzungen](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html?lang=de).

**Abfragesyntax**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld, das im Datensatz gefunden wurde. |
| `{EXPIRATION_IN_SECONDS}` | Die Anzahl der Sekunden, die zwischen Ereignissen erforderlich sind, um das Ende der aktuellen Sitzung und den Beginn einer neuen Sitzung zu qualifizieren. |

Eine Erläuterung der Parameter innerhalb der `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

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
|----------------------------------+-----------------------+--------------------
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

Für die angegebene Beispielabfrage werden die Ergebnisse in der Spalte `session` angegeben. Die Spalte `session` besteht aus den folgenden Komponenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameter | Beschreibung |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Der Zeitunterschied in Sekunden zwischen dem aktuellen Datensatz und dem vorherigen Datensatz. |
| `{NUM}` | Eine eindeutige Sitzungsnummer, beginnend bei 1, für den Schlüssel, der in der `PARTITION BY` der Fensterfunktion definiert ist. |
| `{IS_NEW}` | Ein boolescher Wert, der angibt, ob ein Datensatz der erste einer Sitzung ist. |
| `{DEPTH}` | Die Tiefe des aktuellen Datensatzes innerhalb der Sitzung. |

### SESS_START_IF

Diese Abfrage gibt den Status der Sitzung für die aktuelle Zeile basierend auf dem aktuellen Zeitstempel und dem gegebenen Ausdruck zurück und startet eine neue Sitzung mit der aktuellen Zeile.

**Abfragesyntax**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld, das im Datensatz gefunden wurde. |
| `{TEST_EXPRESSION}` | Ein Ausdruck, mit dem Sie die Felder der Daten überprüfen möchten. Beispiel: `application.launches > 0`. |

Eine Erläuterung der Parameter innerhalb der `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

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
|----------------------------------+-----------------------+----------+--------------------
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

Für die angegebene Beispielabfrage werden die Ergebnisse in der Spalte `session` angegeben. Die Spalte `session` besteht aus den folgenden Komponenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameter | Beschreibung |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Der Zeitunterschied in Sekunden zwischen dem aktuellen Datensatz und dem vorherigen Datensatz. |
| `{NUM}` | Eine eindeutige Sitzungsnummer, beginnend bei 1, für den Schlüssel, der in der `PARTITION BY` der Fensterfunktion definiert ist. |
| `{IS_NEW}` | Ein boolescher Wert, der angibt, ob ein Datensatz der erste einer Sitzung ist. |
| `{DEPTH}` | Die Tiefe des aktuellen Datensatzes innerhalb der Sitzung. |

### SESS_END_IF

Diese Abfrage gibt den Status der Sitzung für die aktuelle Zeile basierend auf dem aktuellen Zeitstempel und dem angegebenen Ausdruck zurück, beendet die aktuelle Sitzung und startet eine neue Sitzung in der nächsten Zeile.

**Abfragesyntax**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Das Zeitstempelfeld, das im Datensatz gefunden wurde. |
| `{TEST_EXPRESSION}` | Ein Ausdruck, mit dem Sie die Felder der Daten überprüfen möchten. Beispiel: `application.launches > 0`. |

Eine Erläuterung der Parameter innerhalb der `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

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
|----------------------------------+-----------------------+----------+--------------------
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

Für die angegebene Beispielabfrage werden die Ergebnisse in der Spalte `session` angegeben. Die Spalte `session` besteht aus den folgenden Komponenten:

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| Parameter | Beschreibung |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | Der Zeitunterschied in Sekunden zwischen dem aktuellen Datensatz und dem vorherigen Datensatz. |
| `{NUM}` | Eine eindeutige Sitzungsnummer, beginnend bei 1, für den Schlüssel, der in der `PARTITION BY` der Fensterfunktion definiert ist. |
| `{IS_NEW}` | Ein boolescher Wert, der angibt, ob ein Datensatz der erste einer Sitzung ist. |
| `{DEPTH}` | Die Tiefe des aktuellen Datensatzes innerhalb der Sitzung. |


## Pathing

Die Pfade können verwendet werden, um die Interaktionstiefe des Kunden zu verstehen, zu bestätigen, dass die beabsichtigten Schritte eines Erlebnisses wie vorgesehen funktionieren, und potenzielle Probleme zu identifizieren, die sich auf den Kunden auswirken.

Die folgenden ADFs unterstützen die Erstellung von Pfadansichten aus ihren vorherigen und nächsten Beziehungen. Sie können vorherige Seiten und nächste Seiten erstellen oder mehrere Ereignisse durchlaufen, um Pfade zu erstellen.

### Vorherige Seite

Legt den vorherigen Wert eines bestimmten Felds fest, der innerhalb des Fensters eine festgelegte Anzahl von Schritten entfernt ist. Beachten Sie im Beispiel, dass die Funktion `WINDOW` mit einem Frame konfiguriert ist, in dem `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` ADF so eingestellt wird, dass die aktuelle Zeile und alle nachfolgenden Zeilen betrachtet werden.

**Abfragesyntax**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{KEY}` | Die Spalte oder das Feld aus dem Ereignis. |
| `{SHIFT}` | (Optional) Die Anzahl der Ereignisse außerhalb des aktuellen Ereignisses. Standardmäßig ist der Wert 1. |
| `{IGNORE_NULLS}` | (Optional) Ein boolescher Wert, der angibt, ob `{KEY}` Nullwerte ignoriert werden sollen. Standardmäßig ist der Wert `false`. |

Eine Erläuterung der Parameter innerhalb der `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

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
|-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
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

Für die angegebene Beispielabfrage werden die Ergebnisse in der Spalte `previous_page` angegeben. Der Wert in der Spalte `previous_page` basiert auf dem im automatischen Dokumenteinzug verwendeten `{KEY}`.

### Nächste Seite

Legt den nächsten Wert eines bestimmten Felds fest, der innerhalb des Fensters eine festgelegte Anzahl von Schritten entfernt ist. Beachten Sie im Beispiel, dass die Funktion `WINDOW` mit einem Frame konfiguriert ist, in dem `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` ADF so eingestellt wird, dass die aktuelle Zeile und alle nachfolgenden Zeilen betrachtet werden.

**Abfragesyntax**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{KEY}` | Die Spalte oder das Feld aus dem Ereignis. |
| `{SHIFT}` | (Optional) Die Anzahl der Ereignisse außerhalb des aktuellen Ereignisses. Standardmäßig ist der Wert 1. |
| `{IGNORE_NULLS}` | (Optional) Ein boolescher Wert, der angibt, ob `{KEY}` Nullwerte ignoriert werden sollen. Standardmäßig ist der Wert `false`. |

Eine Erläuterung der Parameter innerhalb der `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

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
|-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
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

Für die angegebene Beispielabfrage werden die Ergebnisse in der Spalte `previous_page` angegeben. Der Wert in der Spalte `previous_page` basiert auf dem im automatischen Dokumenteinzug verwendeten `{KEY}`.

## Zeit zwischen

Mithilfe der Zeitspanne zwischen den Ereignissen können Sie das latente Kundenverhalten innerhalb eines bestimmten Zeitraums vor oder nach dem Eintreten eines Ereignisses untersuchen.

### Zeit zwischen vorheriger Übereinstimmung

Diese Abfrage gibt eine Zahl zurück, die die Zeiteinheit darstellt, seit das vorherige übereinstimmende Ereignis gesehen wurde. Wenn kein übereinstimmendes Ereignis gefunden wurde, wird null zurückgegeben.

**Abfragesyntax**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Ein Zeitstempelfeld im Datensatz, das bei allen Ereignissen ausgefüllt wird. |
| `{EVENT_DEFINITION}` | Der Ausdruck, um das vorherige Ereignis zu qualifizieren. |
| `{TIME_UNIT}` | Die Ausgabeeinheit. Mögliche Werte sind Tage, Stunden, Minuten und Sekunden. Standardmäßig ist der Wert Sekunden. |

Eine Erläuterung der Parameter innerhalb der `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

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
|-----------------------------------+------------------------------------
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

Für die angegebene Beispielabfrage werden die Ergebnisse in der Spalte `average_minutes_since_registration` angegeben. Der Wert in der `average_minutes_since_registration` Spalte ist der Zeitunterschied zwischen dem aktuellen und dem vorherigen Ereignis. Die Zeiteinheit wurde zuvor in der `{TIME_UNIT}` definiert.

### Zeit zwischen nächster Übereinstimmung

Diese Abfrage gibt eine negative Zahl zurück, die die Zeiteinheit darstellt, die hinter dem nächsten übereinstimmenden Ereignis liegt. Wenn kein übereinstimmendes Ereignis gefunden wird, wird null zurückgegeben.

**Abfragesyntax**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TIMESTAMP}` | Ein Zeitstempelfeld im Datensatz, das bei allen Ereignissen ausgefüllt wird. |
| `{EVENT_DEFINITION}` | Der Ausdruck, um das nächste Ereignis zu qualifizieren. |
| `{TIME_UNIT}` | (Optional) Die Ausgabeeinheit. Mögliche Werte sind Tage, Stunden, Minuten und Sekunden. Standardmäßig ist der Wert Sekunden. |

Eine Erläuterung der Parameter innerhalb der `OVER()` finden Sie im Abschnitt [Fensterfunktionen](#window-functions).

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
|-----------------------------------+------------------------------------------
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

Für die angegebene Beispielabfrage werden die Ergebnisse in der Spalte `average_minutes_until_order_confirmation` angegeben. Der Wert in der Spalte `average_minutes_until_order_confirmation` ist der Zeitunterschied zwischen dem aktuellen und dem nächsten Ereignis. Die Zeiteinheit wurde zuvor in der `{TIME_UNIT}` definiert.

## Nächste Schritte

Mithilfe der hier beschriebenen Funktionen können Sie Abfragen schreiben, um mithilfe von [!DNL Experience Event] auf Ihre eigenen [!DNL Query Service]-Datensätze zuzugreifen. Weitere Informationen zum Erstellen von Abfragen in [!DNL Query Service] finden Sie in der Dokumentation unter [Erstellen von Abfragen](../best-practices/writing-queries.md).

## Weitere Ressourcen

Im folgenden Video erfahren Sie, wie Sie Abfragen in der Adobe Experience Platform-Benutzeroberfläche und in einem PSQL-Client ausführen. Darüber hinaus verwendet das Video Beispiele für einzelne Eigenschaften in einem XDM-Objekt, für die Verwendung von Adobe-definierten Funktionen und für die Verwendung von CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/33392?captions=ger&quality=12&learn=on)
