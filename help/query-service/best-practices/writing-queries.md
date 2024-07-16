---
keywords: Experience Platform; home; beliebte Themen; Query Service; Query Service; Schreiben von Abfragen; Schreiben von Abfragen;
solution: Experience Platform
title: Allgemeine Anleitung für die Ausführung von Abfragen in Query Service
type: Tutorial
description: In diesem Dokument werden wichtige Informationen zum Schreiben von Abfragen in Adobe Experience Platform Query Service beschrieben.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 4%

---

# Allgemeine Anleitung für die Ausführung von Abfragen in [!DNL Query Service]

In diesem Dokument werden wichtige Details zum Schreiben von Abfragen in Adobe Experience Platform [!DNL Query Service] beschrieben.

Ausführliche Informationen zur SQL-Syntax, die in [!DNL Query Service] verwendet wird, finden Sie in der Dokumentation zur [SQL-Syntax](../sql/syntax.md).

## Ausführungsmodelle von Abfragen

Adobe Experience Platform [!DNL Query Service] verfügt über zwei Modelle zur Ausführung von Abfragen: interaktiv und nicht interaktiv. Die interaktive Ausführung wird in Business Intelligence-Tools zur Abfrageentwicklung und Berichterstellung verwendet, während nicht interaktive im Rahmen eines Datenverarbeitungs-Workflows für größere Aufträge und operative Abfragen verwendet werden.

### Ausführung der interaktiven Abfrage

Abfragen können interaktiv ausgeführt werden, indem sie über die [!DNL Query Service] -Benutzeroberfläche oder [über einen verbundenen Client](../clients/overview.md) gesendet werden. Wenn Sie [!DNL Query Service] über einen verbundenen Client ausführen, wird eine aktive Sitzung zwischen dem Client und [!DNL Query Service] ausgeführt, bis entweder die gesendete Abfrage zurückgegeben wird oder eine Zeitüberschreitung auftritt.

Die Ausführung der interaktiven Abfrage weist die folgenden Einschränkungen auf:

| Parameter | Einschränkung |
| --------- | ---------- |
| Zeitüberschreitung der Abfrage | 10 Minuten |
| Maximale zurückgegebene Zeilen | 50.000 |
| Maximale Anzahl gleichzeitiger Abfragen | 5 |

>[!NOTE]
>
>Um die maximale Zeilenbegrenzung zu überschreiben, fügen Sie `LIMIT 0` in Ihre Abfrage ein. Die Abfrage-Zeitüberschreitung von 10 Minuten gilt weiterhin.

Standardmäßig werden die Ergebnisse interaktiver Abfragen an den Client zurückgegeben und **nicht** beibehalten. Damit die Ergebnisse als Datensatz in [!DNL Experience Platform] beibehalten werden können, muss die Abfrage die Syntax `CREATE TABLE AS SELECT` verwenden.

### Nicht-interaktive Abfrageausführung

Abfragen, die über die [!DNL Query Service] -API gesendet werden, werden nicht interaktiv ausgeführt. Nicht interaktive Ausführung bedeutet, dass [!DNL Query Service] den API-Aufruf erhält und die Abfrage in der Reihenfolge ausführt, in der sie empfangen wird. Nicht interaktive Abfragen führen immer dazu, dass entweder ein neuer Datensatz in [!DNL Experience Platform] erstellt wird, um die Ergebnisse zu erhalten, oder dass neue Zeilen in einen vorhandenen Datensatz eingefügt werden.

## Zugreifen auf ein bestimmtes Feld in einem Objekt

Um auf ein Feld innerhalb eines Objekts in Ihrer Abfrage zuzugreifen, können Sie die Punktnotation (`.`) oder die Klammernotation (`[]`) verwenden. Die folgende SQL-Anweisung verwendet die Punktnotation, um das Objekt `endUserIds` bis zum Objekt `mcid` zu durchlaufen.

>[!NOTE]
>
>Die Experience Cloud ID (ECID) wird auch als MCID bezeichnet und wird weiterhin in Namespaces verwendet.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Der Name Ihrer Analysetabelle. |

Die folgende SQL-Anweisung verwendet die Klammer-Notation, um das Objekt `endUserIds` bis zum Objekt `mcid` zu durchlaufen.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Der Name Ihrer Analysetabelle. |

>[!NOTE]
>
>Da jeder Anmerkungstyp die gleichen Ergebnisse zurückgibt, können Sie die gewünschte Option beliebig wählen.

Beide der obigen Beispielabfragen geben anstelle eines einzelnen Werts ein reduziertes Objekt zurück:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

Das zurückgegebene `endUserIds._experience.mcid` -Objekt enthält die entsprechenden Werte für die folgenden Parameter:

- `id`
- `namespace`
- `primary`

Wenn die Spalte nur bis zum Objekt deklariert ist, wird das gesamte Objekt als Zeichenfolge zurückgegeben. Um nur die ID anzuzeigen, verwenden Sie:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Anführungszeichen

Einfache Anführungszeichen, doppelte Anführungszeichen und Backquotes verwenden unterschiedliche Verwendungen in Query Service-Abfragen.

### Einzelne Anführungszeichen

Das einfache Anführungszeichen (`'`) wird zum Erstellen von Textzeichenfolgen verwendet. Beispielsweise kann es in der Anweisung `SELECT` verwendet werden, um einen statischen Textwert im Ergebnis zurückzugeben, und in der `WHERE`-Klausel, um den Inhalt einer Spalte zu bewerten.

Die folgende Abfrage deklariert einen statischen Textwert (`'datasetA'`) für eine Spalte:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Die folgende Abfrage verwendet eine in Anführungszeichen gesetzte Zeichenfolge (`'homepage'`) in ihrer WHERE-Klausel, um Ereignisse für eine bestimmte Seite zurückzugeben.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

### Doppelte Anführungszeichen

Das doppelte Anführungszeichen (`"`) dient zum Deklarieren einer Kennung mit Leerzeichen.

In der folgenden Abfrage werden doppelte Anführungszeichen verwendet, um Werte aus angegebenen Spalten zurückzugeben, wenn eine Spalte einen Leerzeichen in ihrer Kennung enthält:

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>Doppelte Anführungszeichen **können nicht** mit Feldzugriff auf Punktnotation verwendet werden.

### Rücke Anführungszeichen

Das Backquote-Anführungszeichen `` ` `` wird verwendet, um reservierte Spaltennamen **nur** zu maskieren, wenn die Syntax für Punktnotation verwendet wird. Da beispielsweise `order` ein reserviertes Wort in SQL ist, müssen Sie Backquotes verwenden, um auf das Feld `commerce.order` zuzugreifen:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Rücke Anführungszeichen werden auch verwendet, um auf ein Feld zuzugreifen, das mit einer Zahl beginnt. Um beispielsweise auf das Feld `30_day_value` zuzugreifen, müssen Sie die Notation des Backquots verwenden.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Rücke Anführungszeichen sind **nicht** erforderlich, wenn Sie die Klammer-Notation verwenden.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## Anzeigen von Tabelleninformationen

Nachdem Sie eine Verbindung zu Query Service hergestellt haben, können Sie alle verfügbaren Tabellen auf Platform anzeigen, indem Sie entweder die Befehle `\d` oder `SHOW TABLES` verwenden.

### Standardtabellenansicht

Der Befehl `\d` zeigt die standardmäßige Ansicht [!DNL PostgreSQL] für die Auflistung von Tabellen an. Nachfolgend finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Detaillierte Tabellenansicht

Der Befehl `SHOW TABLES` ist ein benutzerdefinierter Befehl, der detailliertere Informationen über die Tabellen bereitstellt. Nachfolgend finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Schemainformationen

Um genauere Informationen über die Schemas in der Tabelle anzuzeigen, können Sie den Befehl `\d {TABLE_NAME}` verwenden, wobei `{TABLE_NAME}` der Name der Tabelle ist, deren Schemadaten Sie anzeigen möchten.

Das folgende Beispiel zeigt die Schemainformationen für die Tabelle `luma_midvalues` , die mit `\d luma_midvalues` angezeigt werden würden:

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Zusätzlich können Sie weitere Informationen zu einer bestimmten Spalte erhalten, indem Sie den Namen der Spalte an den Tabellennamen anhängen. Dies würde im Format `\d {TABLE_NAME}_{COLUMN}` geschrieben.

Das folgende Beispiel zeigt zusätzliche Informationen für die Spalte `web` und wird mithilfe des folgenden Befehls aufgerufen: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Datensätze verknüpfen

Sie können mehrere Datensätze zusammenführen, um Daten aus anderen Datensätzen in Ihre Abfrage aufzunehmen.

Im folgenden Beispiel würden die beiden folgenden Datensätze (`your_analytics_table` und `custom_operating_system_lookup`) hinzugefügt und eine `SELECT` -Anweisung für die 50 wichtigsten Betriebssysteme nach Anzahl der Seitenansichten erstellt.

**Abfrage**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**Ergebnisse**

| OperatingSystem | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979,0 |
| Windows XP | 1669824,0 |
| Windows 8 | 420024,0 |
| Adobe AIR | 315032,0 |
| Windows Vista | 173566,0 |
| Mobile iOS 6.1.3 | 119069,0 |
| Linux | 56516,0 |
| OSX 10.6.8 | 53652,0 |
| Android 4.0.4 | 46167,0 |
| Android 4.0.3 | 31852,0 |
| Windows Server 2003 und XP x64 Edition | 28883,0 |
| Android 4.1.1 | 24336,0 |
| Android 2.3.6 | 15735,0 |
| OSX 10.6 | 13357,0 |
| Windows Phone 7.5 | 11054,0 |
| Android 4.3 | 9221,0 |

## Deduplizierung

Query Service unterstützt die Deduplizierung von Daten oder das Entfernen doppelter Zeilen aus Daten. Weiterführende Informationen zur Deduplizierung finden Sie im [Handbuch zur Query Service-Deduplizierung](../key-concepts/deduplication.md) .

## Zeitzonenberechnungen in Query Service

Query Service standardisiert persistente Daten in Adobe Experience Platform mithilfe des UTC-Zeitstempelformats. Weitere Informationen zur Übersetzung Ihrer Zeitzonenanforderung in und von einem UTC-Zeitstempel finden Sie im Abschnitt [FAQs zum Ändern der Zeitzone von und zu einem UTC-Zeitstempel](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie einige wichtige Aspekte beim Schreiben von Abfragen mit [!DNL Query Service] erläutert. Weitere Informationen zur Verwendung der SQL-Syntax zum Schreiben Ihrer eigenen Abfragen finden Sie in der Dokumentation zur [SQL-Syntax](../sql/syntax.md).

Weitere Beispiele für Abfragen, die in Query Service verwendet werden können, finden Sie in der folgenden Anwendungsfalldokumentation:

- [Analytics-Erkenntnisse](../use-cases/analytics-insights.md)
- [Erstellen eines Trendberichts mit Ereignissen](../use-cases/trended-report-of-events.md)
- [Anzeigen eines Rollup-Berichts eines Besuchers](../use-cases/roll-up-report-of-a-visitor.md)
- [Auflisten der Seitenansichten von Benutzenden](../use-cases/list-visitor-sessions.md)
- [Besucher nach der Anzahl der Seitenansichten auflisten](../use-cases/visitors-by-number-of-page-views.md)
