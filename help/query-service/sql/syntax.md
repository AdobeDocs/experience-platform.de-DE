---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; SQL-Syntax; SQL; ctas; CTAS; Erstellen einer Tabelle als ausgewählt
solution: Experience Platform
title: SQL-Syntax in Query Service
description: Dieses Dokument zeigt die von Adobe Experience Platform Query Service unterstützte SQL-Syntax.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: b94536be6e92354e237b99d36af13adf5a49afa7
workflow-type: tm+mt
source-wordcount: '3863'
ht-degree: 9%

---

# SQL-Syntax in Query Service

Adobe Experience Platform Query Service bietet die Möglichkeit, standardmäßige ANSI-SQL für `SELECT` -Anweisungen und anderen eingeschränkten Befehlen. In diesem Dokument wird die von [!DNL Query Service].

## Abfragen auswählen {#select-queries}

Die folgende Syntax definiert eine `SELECT` Abfrage unterstützt von [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

where `from_item` kann eine der folgenden Optionen sein:

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
[ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
```

```sql
with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

und `grouping_element` kann eine der folgenden Optionen sein:

```sql
( )
```

```sql
expression
```

```sql
( expression [, ...] )
```

```sql
ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
CUBE ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
GROUPING SETS ( grouping_element [, ...] )
```

und `with_query`:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

Die folgenden Unterabschnitte enthalten Details zu zusätzlichen Klauseln, die Sie in Ihren Abfragen verwenden können, sofern sie dem oben beschriebenen Format entsprechen.

### SNAPSHOT-Klausel

Diese Klausel kann verwendet werden, um Daten auf einer Tabelle basierend auf Momentaufnahmen-IDs inkrementell zu lesen. Eine Snapshot-ID ist eine Checkpoint-Markierung, die durch eine Long-Typ-Zahl dargestellt wird, die jedes Mal, wenn Daten in eine Data Lake-Tabelle geschrieben werden, auf eine Data Lake-Tabelle angewendet wird. Die `SNAPSHOT` -Klausel hängt sich an die Tabellenbeziehung an, neben der sie verwendet wird.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Beispiel

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM Customers SNAPSHOT BETWEEN HEAD AND 123;

SELECT * FROM Customers SNAPSHOT BETWEEN 345 AND TAIL;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

Bitte beachten Sie, dass eine `SNAPSHOT` -Klausel funktioniert mit einem Tabellen- oder Tabellenalias, jedoch nicht über einer Unter-Abfrage oder Ansicht. A `SNAPSHOT` -Klausel funktioniert überall in einer `SELECT` -Abfrage auf eine Tabelle angewendet werden.

Darüber hinaus können Sie `HEAD` und `TAIL` als spezielle Offset-Werte für Momentaufnahmen-Klauseln. Verwenden `HEAD` bezieht sich auf einen Offset vor dem ersten Snapshot, während `TAIL` bezieht sich auf einen Versatz nach dem letzten Schnappschuss.

>[!NOTE]
>
>Wenn Sie zwischen zwei Snapshot-IDs abfragen und der Start-Snapshot abgelaufen ist, können die beiden folgenden Szenarien eintreten, je nachdem, ob das optionale Fallback-Verhalten-Flag (`resolve_fallback_snapshot_on_failure`) festgelegt ist:
>
>- Wenn das optionale Fallback-Verhalten-Flag gesetzt ist, wählt Query Service den frühesten verfügbaren Snapshot aus, legt ihn als Start-Snapshot fest und gibt die Daten zwischen dem frühesten verfügbaren Snapshot und dem angegebenen End-Snapshot zurück. Diese Daten sind **inklusive** der frühesten verfügbaren Momentaufnahme.
>
>- Wenn das optionale Fallback-Verhalten-Flag nicht gesetzt ist, wird ein Fehler zurückgegeben.

### WHERE-Klausel

Standardmäßig werden Übereinstimmungen von einem `WHERE` einer `SELECT` -Abfrage muss zwischen Groß- und Kleinschreibung unterschieden werden. Wenn bei Treffern nicht zwischen Groß- und Kleinschreibung unterschieden werden soll, können Sie den Suchbegriff `ILIKE` anstelle von `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

Die Logik der LIKE- und ILIKE-Klauseln wird in der folgenden Tabelle erläutert:

| Klausel | Operator |
| ------ | -------- |
| `WHERE condition LIKE pattern` | `~~` |
| `WHERE condition NOT LIKE pattern` | `!~~` |
| `WHERE condition ILIKE pattern` | `~~*` |
| `WHERE condition NOT ILIKE pattern` | `!~~*` |

**Beispiel**

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Diese Abfrage gibt Kunden zurück, deren Namen mit &quot;A&quot;oder &quot;a&quot;beginnen.

### JOIN

A `SELECT` -Abfrage, die Joins verwendet, hat die folgende Syntax:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION, INTERSECT und EXCEPT

Die `UNION`, `INTERSECT`, und `EXCEPT` -Klauseln werden verwendet, um gleichartige Zeilen aus zwei oder mehr Tabellen zu kombinieren oder auszuschließen:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREATE TABLE AS SELECT {#create-table-as-select}

Die folgende Syntax definiert eine `CREATE TABLE AS SELECT` (CTAS)-Abfrage:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE') ] AS (select_query)
```

| Parameter | Beschreibung |
| ----- | ----- |
| `schema` | Der Titel des XDM-Schemas. Verwenden Sie diese Klausel nur, wenn Sie ein vorhandenes XDM-Schema für den neuen Datensatz verwenden möchten, der von der CTAS-Abfrage erstellt wurde. |
| `rowvalidation` | (Optional) Gibt an, ob der Benutzer die Überprüfung aller neuen Batches auf Zeilenebene wünscht, die für den neu erstellten Datensatz erfasst werden. Der Standardwert lautet `true`. |
| `label` | Wenn Sie einen Datensatz mit einer CTAS-Abfrage erstellen, verwenden Sie diese Bezeichnung mit dem Wert von `profile` , um Ihren Datensatz als für das Profil aktiviert zu kennzeichnen. Das bedeutet, dass Ihr Datensatz bei der Erstellung automatisch für das Profil markiert wird. Weitere Informationen zur Verwendung von `label`. |
| `select_query` | A `SELECT` -Anweisung. Die Syntax der `SELECT` -Abfrage finden Sie im Abschnitt [Abschnitt &quot;Abfragen auswählen&quot;](#select-queries). |

**Beispiel**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title', label='PROFILE') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>Die `SELECT`-Anweisung muss einen Alias für die Aggregat-Funktionen wie `COUNT`, `SUM`, `MIN` usw. enthalten. Darüber hinaus wird die `SELECT` -Anweisung kann mit oder ohne Klammern () bereitgestellt werden. Sie können eine `SNAPSHOT` -Klausel, um inkrementelle Deltas in die Zieltabelle zu lesen.

## INSERT INTO

Die `INSERT INTO` -Befehl wird wie folgt definiert:

```sql
INSERT INTO table_name select_query
```

| Parameter | Beschreibung |
| ----- | ----- |
| `table_name` | Der Name der Tabelle, in die die Abfrage eingefügt werden soll. |
| `select_query` | A `SELECT` -Anweisung. Die Syntax der `SELECT` -Abfrage finden Sie im Abschnitt [Abschnitt &quot;Abfragen auswählen&quot;](#select-queries). |

**Beispiel**

>[!NOTE]
>
>Im Folgenden finden Sie ein hilfreiches Beispiel und nur zu Anleitungszwecken.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> Die `SELECT` statement **darf nicht** in Klammern (). Außerdem wird das Schema des Ergebnisses der `SELECT` -Anweisung muss mit der in der `INSERT INTO` -Anweisung. Sie können eine `SNAPSHOT` -Klausel, um inkrementelle Deltas in die Zieltabelle zu lesen.

Die meisten Felder in einem echten XDM-Schema befinden sich nicht auf der Stammebene und SQL lässt die Verwendung der Punktnotation nicht zu. Um mithilfe verschachtelter Felder ein realistisches Ergebnis zu erzielen, müssen Sie jedes Feld in Ihrem `INSERT INTO` Pfad.

nach `INSERT INTO` verschachtelte Pfade verwenden die folgende Syntax:

```sql
INSERT INTO [dataset]
SELECT struct([source field1] as [target field in schema],
[source field2] as [target field in schema],
[source field3] as [target field in schema]) [tenant name]
FROM [dataset]
```

**Beispiel**

```sql
INSERT INTO Customers SELECT struct(SupplierName as Supplier, City as SupplierCity, Country as SupplierCountry) _Adobe FROM OnlineCustomers;
```

## DROP TABLE

Die `DROP TABLE` löscht eine vorhandene Tabelle und löscht den mit der Tabelle verknüpften Ordner aus dem Dateisystem, wenn es sich nicht um eine externe Tabelle handelt. Wenn die Tabelle nicht vorhanden ist, tritt eine Ausnahme auf.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Parameter | Beschreibung |
| ------ | ------ |
| `IF EXISTS` | Wenn dies angegeben ist, wird keine Ausnahme ausgelöst, wenn die Tabelle **not** existieren. |

## DATENBANK ERSTELLEN

Die `CREATE DATABASE` -Befehl erstellt eine ADLS-Datenbank.

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## DROP-DATENBANK

Die `DROP DATABASE` löscht die Datenbank aus einer Instanz.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Parameter | Beschreibung |
| ------ | ------ |
| `IF EXISTS` | Wenn dies angegeben ist, wird keine Ausnahme ausgelöst, wenn die Datenbank **not** existieren. |

## DROP-SCHEMA

Die `DROP SCHEMA` -Befehl entfernt ein vorhandenes Schema.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Parameter | Beschreibung |
| ------ | ------ |
| `IF EXISTS` | Wenn dies angegeben ist, wird keine Ausnahme ausgelöst, wenn das Schema **not** existieren. |
| `RESTRICT` | Standardwert für den Modus. Wenn dies angegeben wird, wird das Schema nur gelöscht, wenn es **nicht** enthält alle Tabellen. |
| `CASCADE` | Wenn dies angegeben wird, wird das Schema zusammen mit allen im Schema vorhandenen Tabellen abgelegt. |

## CREATE VIEW

Die folgende Syntax definiert eine `CREATE VIEW` Abfrage:

```sql
CREATE VIEW view_name AS select_query
```

| Parameter | Beschreibung |
| ------ | ------ |
| `view_name` | Der Name der zu erstellenden Ansicht. |
| `select_query` | A `SELECT` -Anweisung. Die Syntax der `SELECT` -Abfrage finden Sie im Abschnitt [Abschnitt &quot;Abfragen auswählen&quot;](#select-queries). |

**Beispiel**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## DROP VIEW

Die folgende Syntax definiert eine `DROP VIEW` Abfrage:

```sql
DROP VIEW [IF EXISTS] view_name
```

| Parameter | Beschreibung |
| ------ | ------ |
| `IF EXISTS` | Wenn dies angegeben ist, wird keine Ausnahme ausgelöst, wenn die Ansicht dies tut **not** existieren. |
| `view_name` | Der Name der zu löschenden Ansicht. |

**Beispiel**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Anonymer Block

Ein anonymer Block besteht aus zwei Abschnitten: ausführbare Dateien und Abschnitte zur Bearbeitung von Ausnahmen. In einem anonymen Baustein ist der Abschnitt &quot;Ausführbare Datei&quot;obligatorisch. Der Abschnitt zur Ausnahmebehandlung ist jedoch optional.

Das folgende Beispiel zeigt, wie ein Block mit einer oder mehreren Anweisungen erstellt wird, die zusammen ausgeführt werden sollen:

```sql
$$BEGIN
  statementList
[EXCEPTION exceptionHandler]
$$END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

Nachfolgend finden Sie ein Beispiel für die Verwendung eines anonymen Blocks.

```sql
$$BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
$$END;
```

### Automatisch in JSON {#auto-to-json}

Query Service unterstützt eine optionale Einstellung auf Sitzungsebene, um komplexe Felder der obersten Ebene aus interaktiven SELECT-Abfragen als JSON-Zeichenfolgen zurückzugeben. Die `auto_to_json` -Einstellung ermöglicht die Rückgabe von Daten aus komplexen Feldern als JSON und die anschließende Analyse in JSON-Objekten mithilfe von Standardbibliotheken.

Feature Flag setzen `auto_to_json` auf &quot;true&quot;gesetzt, bevor Sie Ihre SELECT-Abfrage mit komplexen Feldern ausführen.

```sql
set auto_to_json=true; 
```

#### Bevor Sie die `auto_to_json` Markierung

Die folgende Tabelle enthält ein Beispielabfrageergebnis vor dem `auto_to_json` -Einstellung angewendet wird. In beiden Szenarien wurde dieselbe SELECT-Abfrage (wie unten dargestellt) verwendet, die auf eine Tabelle mit komplexen Feldern ausgerichtet ist.

```sql
SELECT * FROM TABLE_WITH_COMPLEX_FIELDS LIMIT 2;
```

Die Ergebnisse lauten wie folgt:

```console
                _id                |                                _experience                                 | application  |                   commerce                   | dataSource |                               device                               |                       endUserIDs                       |                                                                                                environment                                                                                                |                     identityMap                     |                              placeContext                               |   receivedTimestamp   |       timestamp       | userActivityRegion |                                         web                                          | _adcstageforpqs
-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### Nachdem Sie die `auto_to_json` Markierung

Die folgende Tabelle zeigt den Unterschied in den Ergebnissen, die die Variable `auto_to_json` hat auf den resultierenden Datensatz Einfluss. Dieselbe SELECT-Abfrage wurde in beiden Szenarien verwendet.

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### Fallback-Momentaufnahme bei Fehler beheben {#resolve-fallback-snapshot-on-failure}

Die `resolve_fallback_snapshot_on_failure` -Option wird verwendet, um das Problem einer abgelaufenen Snapshot-ID zu beheben. Momentaufnahmen-Metadaten laufen nach zwei Tagen ab und ein abgelaufener Schnappschuss kann die Logik eines Skripts ungültig machen. Dies kann bei der Verwendung anonymer Bausteine ein Problem darstellen.

Legen Sie die `resolve_fallback_snapshot_on_failure` auf &quot;true&quot;, um einen Schnappschuss mit einer vorherigen Momentaufnahme-ID zu überschreiben.

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

Die folgende Codezeile überschreibt die `@from_snapshot_id` mit der frühesten verfügbaren `snapshot_id` aus Metadaten.

```sql
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);

Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```


## Organisation von Daten-Medienelementen

Es ist wichtig, Ihre Daten-Assets beim Wachstum im Adobe Experience Platform Data Lake logisch zu organisieren. Query Service erweitert SQL-Konstrukte, mit denen Sie Daten-Assets logisch in einer Sandbox gruppieren können. Diese Organisationsmethode ermöglicht die Freigabe von Daten-Assets zwischen Schemas, ohne dass diese physisch verschoben werden müssen.

Die folgenden SQL-Konstrukte mit SQL-Standardsyntax werden zur logischen Organisation Ihrer Daten unterstützt.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Siehe Handbuch unter [Logische Organisation von Datenelementen](../best-practices/organize-data-assets.md) für eine detaillierte Erläuterung der Best Practices für Query Service.

## Tabelle vorhanden

Die `table_exists` Der SQL-Befehl wird verwendet, um zu überprüfen, ob eine Tabelle im System vorhanden ist oder nicht. Der Befehl gibt einen booleschen Wert zurück: `true`, wenn eine Tabelle **vorhanden** ist, und `false`, wenn **keine** Tabelle vorhanden ist.

Wenn Sie überprüfen, ob eine Tabelle vorhanden ist, bevor Sie die Anweisungen ausführen, wird die `table_exists` -Funktion vereinfacht das Schreiben eines anonymen Blocks, um beide `CREATE` und `INSERT INTO` Anwendungsbeispiele.

Die folgende Syntax definiert die `table_exists` command:

```SQL
$$
BEGIN

#Set mytableexist to true if the table already exists.
SET @mytableexist = SELECT table_exists('target_table_name');

#Create the table if it does not already exist (this is a one time operation).
CREATE TABLE IF NOT EXISTS target_table_name AS
  SELECT *
  FROM   profile_dim_date limit 10;

#Insert data only if the table already exists. Check if @mytableexist = 'true'
 INSERT INTO target_table_name           (
                     select *
                     from   profile_dim_date
                     WHERE  @mytableexist = 'true' limit 20
              ) ;
EXCEPTION
WHEN other THEN SELECT 'ERROR';

END $$; 
```

## Inline {#inline}

Die `inline` -Funktion trennt die Elemente eines Arrays von Strukturen und generiert die Werte in einer Tabelle. Sie kann nur im `SELECT` Liste oder `LATERAL VIEW`.

Die `inline` function **cannot** in einer Auswahlliste platziert werden, in der andere Generatorfunktionen vorhanden sind.

Standardmäßig werden die erzeugten Spalten &quot;col1&quot;, &quot;col2&quot;usw. genannt. Wenn der Ausdruck `NULL` dann werden keine Zeilen erzeugt.

>[!TIP]
>
>Spaltennamen können mithilfe der `RENAME` Befehl.

**Beispiel**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

Das Beispiel gibt Folgendes zurück:

```text
1  a Spark SQL
2  b Spark SQL
```

Dieses zweite Beispiel veranschaulicht außerdem das Konzept und die Anwendung des `inline` -Funktion. Das Datenmodell für das Beispiel ist in der Abbildung unten dargestellt.

![Ein Schemadiagramm für productListItems.](../images/sql/productListItems.png)

**Beispiel**

```sql
select inline(productListItems) from source_dataset limit 10;
```

Die Werte, die aus dem `source_dataset` werden zum Ausfüllen der Zieltabelle verwendet.

| SKU | _experience  | quantity | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;)&quot;)&quot;) | 5 | 10.5 |
| product-id-5 | (&quot;(&quot;(&quot;(&quot;(A, pass, B, NULL)&quot;)&quot;)&quot;)&quot;) |          |              |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D, NULL)&quot;)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(BM, pass, NA, NULL)&quot;)&quot;)&quot;) | 3 | 12 |

## [!DNL Spark] SQL-Befehle

Der folgende Unterabschnitt behandelt die von Query Service unterstützten Spark-SQL-Befehle.

### SET

Die `SET` gibt eine Eigenschaft ein und gibt entweder den Wert einer vorhandenen Eigenschaft zurück oder listet alle vorhandenen Eigenschaften auf. Wenn für einen vorhandenen Eigenschaftenschlüssel ein Wert angegeben wird, wird der alte Wert überschrieben.

```sql
SET property_key = property_value
```

| Parameter | Beschreibung |
| ------ | ------ |
| `property_key` | Der Name der Eigenschaft, die Sie auflisten oder ändern möchten. |
| `property_value` | Der Wert, als den die Eigenschaft festgelegt werden soll. |

Um den Wert für eine Einstellung zurückzugeben, verwenden Sie `SET [property key]` ohne `property_value`.

## [!DNL PostgreSQL] commands

Die folgenden Unterabschnitte decken die [!DNL PostgreSQL] von Query Service unterstützte Befehle.

### ANALYSETABELLE {#analyze-table}

Die `ANALYZE TABLE` -Befehl führt eine Verteilungsanalyse und statistische Berechnungen für die benannte(n) Tabelle(n) durch. Die Verwendung von `ANALYZE TABLE` variiert, je nachdem, ob die Datensätze auf der [beschleunigter Speicher](#compute-statistics-accelerated-store) oder [Datensee](#compute-statistics-data-lake). Weitere Informationen zur Verwendung finden Sie in den entsprechenden Abschnitten.

#### COMPUTE STATISTICS on the Accelerated Store {#compute-statistics-accelerated-store}

Die `ANALYZE TABLE` berechnet Statistiken für eine Tabelle im beschleunigten Speicher. Die Statistiken werden anhand der ausgeführten CTAS- oder ITAS-Abfragen für eine bestimmte Tabelle im beschleunigten Speicher berechnet.

**Beispiel**

```sql
ANALYZE TABLE <original_table_name>
```

Im Folgenden finden Sie eine Liste statistischer Berechnungen, die nach Verwendung der Variablen `ANALYZE TABLE` command:-

| Berechnete Werte | Beschreibung |
|---|---|
| `field` | Der Name der Spalte in einer Tabelle. |
| `data-type` | Der zulässige Datentyp für jede Spalte. |
| `count` | Die Anzahl der Zeilen, die einen Wert ungleich null für dieses Feld enthalten. |
| `distinct-count` | Die Anzahl der eindeutigen oder eindeutigen Werte für dieses Feld. |
| `missing` | Die Anzahl der Zeilen, die einen Nullwert für dieses Feld haben. |
| `max` | Der Maximalwert aus der analysierten Tabelle. |
| `min` | Der Mindestwert aus der analysierten Tabelle. |
| `mean` | Der Durchschnittswert der analysierten Tabelle. |
| `stdev` | Die Standardabweichung der analysierten Tabelle. |

#### COMPUTE STATISTIKEN auf dem Data Lake {#compute-statistics-data-lake}

Sie können nun Statistiken auf Spaltenebene berechnen über [!DNL Azure Data Lake Storage] (ADLS)-Datensätzen mit der `COMPUTE STATISTICS` SQL-Befehl. Berechnen Sie Spaltenstatistiken für den gesamten Datensatz, eine Untergruppe eines Datensatzes, alle Spalten oder eine Untergruppe von Spalten.

`COMPUTE STATISTICS` erweitert die `ANALYZE TABLE` Befehl. Die Variable `COMPUTE STATISTICS`, `FILTERCONTEXT`, und `FOR COLUMNS` -Befehle werden für beschleunigte Store-Tabellen nicht unterstützt. Diese Erweiterungen für den Befehl `ANALYZE TABLE` werden derzeit nur für ADLS-Tabellen unterstützt.

**Beispiel**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

Die `FILTER CONTEXT` berechnet basierend auf der bereitgestellten Filterbedingung Statistiken über eine Teilmenge des Datensatzes. Die `FOR COLUMNS` -Befehl dient zur Bestimmung bestimmter Spalten für die Analyse.

>[!NOTE]
>
>Die `Statistics ID` und die generierten Statistiken gelten nur für jede Sitzung und können nicht über verschiedene PSQL-Sitzungen hinweg aufgerufen werden.<br><br>Einschränkungen:<ul><li>Die Erstellung von Statistiken wird für Array- oder Zuordnungsdatentypen nicht unterstützt</li><li>Berechnete Statistiken sind **not** über mehrere Sitzungen hinweg beibehalten.</li></ul><br><br>Optionen:<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br>Standardmäßig ist diese Markierung auf „true“ eingestellt. Wenn daher Statistiken für einen Datentyp angefordert werden, der nicht unterstützt wird, wird kein Fehler ausgegeben, es werden jedoch Felder mit den nicht unterstützten Datentypen still übersprungen.<br>Um Benachrichtigungen zu Fehlern zu aktivieren, wenn Statistiken zu nicht unterstützten Datentypen angefordert werden, verwenden Sie: `SET skip_stats_for_complex_datatypes = false`.

Die Konsolenausgabe wird wie unten dargestellt angezeigt.

```console
|     Statistics ID      | 
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

Sie können die berechneten Statistiken dann direkt abfragen, indem Sie auf die `Statistics ID`. Die folgende Beispielanweisung ermöglicht es Ihnen, die Ausgabe vollständig anzuzeigen, wenn sie mit der `Statistics ID` oder den Aliasnamen. Weitere Informationen zu dieser Funktion finden Sie unter [Alias-Namensdokumentation](../essential-concepts/dataset-statistics.md#alias-name).

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

Verwenden Sie die `SHOW STATISTICS` -Befehl, um die Metadaten für alle temporären Statistiken anzuzeigen, die in der Sitzung generiert wurden. Mithilfe dieses Befehls können Sie den Umfang Ihrer statistischen Analyse verfeinern.

```sql
SHOW STATISTICS;
```

Nachfolgend finden Sie ein Beispiel für die Ausgabe SHOW STATISTICS.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Siehe [Dokumentation zu Datensatzstatistiken](../essential-concepts/dataset-statistics.md) für weitere Informationen.

#### TABLESAMPEL {#tablesample}

Der Abfrage-Service von Adobe Experience Platform bietet Beispieldatensätze als Teil der Funktionen zur annähernden Abfrageverarbeitung.
Beispiele für Datensätze werden am besten verwendet, wenn Sie keine genaue Antwort für einen Aggregat-Vorgang über einen Datensatz benötigen. Mit dieser Funktion können Sie effizientere Explorationsabfragen zu großen Datensätzen durchführen, indem Sie eine ungefähre Abfrage senden, um eine ungefähre Antwort zurückzugeben.

Beispieldatensätze werden mit einheitlichen Zufallsproben aus vorhandenen [!DNL Azure Data Lake Storage] (ADLS)-Datensätze, bei denen nur ein Prozentsatz der Datensätze aus dem Original verwendet wird. Die Datensatzbeispielfunktion erweitert die `ANALYZE TABLE` mit dem Befehl `TABLESAMPLE` und `SAMPLERATE` SQL-Befehle.

In den Beispielen unten zeigt Zeile eins, wie eine 5 %-Probe der Tabelle berechnet wird. Zeile zwei zeigt, wie ein 5 %-Sample aus einer gefilterten Ansicht der Daten in der Tabelle berechnet wird.

**Beispiel**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

Siehe [Dokumentation zu Datensatzbeispielen](../essential-concepts/dataset-samples.md) für weitere Informationen.

### BEGIN

Die `BEGIN` -Befehl oder alternativ der `BEGIN WORK` oder `BEGIN TRANSACTION` -Befehl, startet einen Transaktionsblock. Alle Anweisungen, die nach dem Befehl &quot;begin&quot;eingegeben werden, werden in einer einzigen Transaktion ausgeführt, bis ein expliziter COMMIT- oder ROLLBACK-Befehl angegeben wird. Dieser Befehl entspricht dem `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CLOSE

Die `CLOSE` gibt die Ressourcen frei, die mit einem geöffneten Cursor verknüpft sind. Nach dem Schließen des Cursors sind keine weiteren Vorgänge zulässig. Ein Cursor sollte geschlossen werden, wenn er nicht mehr benötigt wird.

```sql
CLOSE name
CLOSE ALL
```

Wenn `CLOSE name` verwendet wird, `name` stellt den Namen eines geöffneten Cursors dar, der geschlossen werden muss. Wenn `CLOSE ALL` verwendet wird, werden alle geöffneten Cursor geschlossen.

### DEALLOCATE

Die `DEALLOCATE` -Befehl können Sie die Zuordnung einer zuvor vorbereiteten SQL-Anweisung aufheben. Wenn Sie die Zuordnung einer vorbereiteten Anweisung nicht explizit aufheben, wird dies am Ende der Sitzung ausgeführt. Weitere Informationen zu vorbereiteten Anweisungen finden Sie im [VORBEREITEN, Befehl](#prepare) Abschnitt.

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Wenn `DEALLOCATE name` verwendet wird, `name` stellt den Namen der vorbereiteten Anweisung dar, die aufgehoben werden muss. Wenn `DEALLOCATE ALL` verwendet wird, wird die Zuweisung aller vorbereiteten Anweisungen aufgehoben.

### DECLARE

Die `DECLARE` -Befehl ermöglicht es einem Benutzer, einen Cursor zu erstellen, mit dem eine kleine Anzahl von Zeilen aus einer größeren Abfrage abgerufen werden kann. Nachdem der Cursor erstellt wurde, werden Zeilen mit `FETCH` abgerufen.

```sql
DECLARE name CURSOR FOR query
```

| Parameter | Beschreibung |
| ------ | ------ |
| `name` | Der Name des zu erstellenden Cursors. |
| `query` | Ein `SELECT`- oder `VALUES`-Befehl, der die vom Cursor zurückzugebenden Zeilen angibt. |

### EXECUTE

Die `EXECUTE` -Befehl wird zum Ausführen einer zuvor vorbereiteten Anweisung verwendet. Da vorbereitete Anweisungen nur für die Dauer einer Sitzung vorhanden sind, muss die vorbereitete Anweisung von einer `PREPARE` -Anweisung, die zuvor in der aktuellen Sitzung ausgeführt wurde. Weitere Informationen zur Verwendung vorbereiteter Anweisungen finden Sie im [`PREPARE` command](#prepare) Abschnitt.

Wenn die Variable `PREPARE` -Anweisung, die die Anweisung erstellt hat, die einige Parameter angegeben hat, muss ein kompatibler Satz von Parametern an `EXECUTE` -Anweisung. Wenn diese Parameter nicht übergeben werden, wird ein Fehler erzeugt.

```sql
EXECUTE name [ ( parameter ) ]
```

| Parameter | Beschreibung |
| ------ | ------ |
| `name` | Der Name der vorbereiteten Anweisung, die ausgeführt werden soll. |
| `parameter` | Der tatsächliche Wert eines Parameters für die vorbereitete Anweisung. Hierbei muss es sich um einen Ausdruck handeln, der einen Wert liefert, der mit dem Datentyp dieses Parameters kompatibel ist, der bei der Erstellung der vorbereiteten Anweisung festgelegt wurde.  Wenn mehrere Parameter für die vorbereitete Anweisung vorhanden sind, werden sie durch Kommas getrennt. |

### EXPLAIN

Die `EXPLAIN` zeigt den Ausführungsplan für die angegebene Anweisung an. Der Ausführungsplan zeigt, wie die in der Anweisung referenzierten Tabellen gescannt werden.  Wenn mehrere Tabellen referenziert werden, wird angezeigt, welche Join-Algorithmen verwendet werden, um die erforderlichen Zeilen aus jeder Eingabetabelle zusammenzuführen.

```sql
EXPLAIN statement
```

Verwenden Sie die `FORMAT` mit dem Keyword `EXPLAIN` -Befehl, um das Format der Antwort zu definieren.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Parameter | Beschreibung |
| ------ | ------ |
| `FORMAT` | Verwenden Sie die `FORMAT` -Befehl, um das Ausgabeformat anzugeben. Die verfügbaren Optionen sind `TEXT` oder `JSON`. Die Ausgabe ohne Text enthält dieselben Informationen wie das Textausgabeformat, ist jedoch für Programme einfacher zu analysieren. Dieser Parameter ist standardmäßig auf `TEXT` voreingestellt. |
| `statement` | Jede `SELECT`-, `INSERT`-, `UPDATE`-, `DELETE`-, `VALUES`-, `EXECUTE`-, `DECLARE`-, `CREATE TABLE AS`- oder `CREATE MATERIALIZED VIEW AS`-Anweisung, deren Ausführungsplan Sie sehen möchten. |

>[!IMPORTANT]
>
>Jede Ausgabe, die `SELECT` -Anweisung wird möglicherweise zurückgegeben, wenn sie mit der `EXPLAIN` Keyword. Andere Nebenwirkungen der Anweisung treten wie gewohnt auf.

**Beispiel**

Das folgende Beispiel zeigt den Plan für eine einfache Abfrage einer Tabelle mit einer einzigen `integer` Spalte und 10000 Zeilen:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### FETCH

Die `FETCH` -Befehl ruft Zeilen mit einem zuvor erstellten Cursor ab.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Parameter | Beschreibung |
| ------ | ------ |
| `num_of_rows` | Die Anzahl der abzurufenden Zeilen. |
| `cursor_name` | Der Name des Cursors, aus dem Sie Informationen abrufen. |

### PREPARE {#prepare}

Die `PREPARE` -Befehl können Sie eine vorbereitete Anweisung erstellen. Eine vorbereitete Anweisung ist ein serverseitiges Objekt, das zur Vorlagenbildung für ähnliche SQL-Anweisungen verwendet werden kann.

Vorbereitete Anweisungen können Parameter annehmen, d. h. Werte, die bei der Ausführung in der Anweisung ersetzt werden. Parameter werden nach Position referenziert, indem bei der Verwendung vorbereiteter Anweisungen $1, $2 usw. verwendet werden.

Optional können Sie eine Liste von Parameterdatentypen angeben. Wenn der Datentyp eines Parameters nicht aufgeführt ist, kann der Typ aus dem Kontext abgeleitet werden.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Parameter | Beschreibung |
| ------ | ------ |
| `name` | Der Name für die vorbereitete Anweisung. |
| `data_type` | Die Datentypen der Parameter der vorbereiteten Anweisung. Wenn der Datentyp eines Parameters nicht aufgeführt ist, kann der Typ aus dem Kontext abgeleitet werden. Wenn Sie mehrere Datentypen hinzufügen müssen, können Sie sie in einer durch Kommas getrennten Liste hinzufügen. |

### ROLLBACK

Die `ROLLBACK` -Befehl löscht die aktuelle Transaktion und verwirft alle durch die Transaktion vorgenommenen Aktualisierungen.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECT INTO

Die `SELECT INTO` erstellt eine neue Tabelle und füllt sie mit Daten, die durch eine Abfrage berechnet wurden. Die Daten werden nicht wie bei einem normalen `SELECT` Befehl. Die Spalten der neuen Tabelle haben die Namen und Datentypen, die mit den Ausgabespalten der `SELECT` Befehl.

```sql
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
    * | expression [ [ AS ] output_name ] [, ...]
    INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] new_table
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY expression [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
    [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
    [ FOR { UPDATE | SHARE } [ OF table_name [, ...] ] [ NOWAIT ] [...] ]
```

Weitere Informationen zu den standardmäßigen SELECT-Abfrageparametern finden Sie im [Abfrageabschnitt auswählen](#select-queries). In diesem Abschnitt werden nur Parameter aufgelistet, die ausschließlich für die `SELECT INTO` Befehl.

| Parameter | Beschreibung |
| ------ | ------ |
| `TEMPORARY` oder `TEMP` | Ein optionaler Parameter. Wenn angegeben, ist die zu erstellende Tabelle eine temporäre Tabelle. |
| `UNLOGGED` | Ein optionaler Parameter. Wenn angegeben, ist die Tabelle, die wie erstellt wird, eine nicht protokollierte Tabelle. Weitere Informationen zu nicht protokollierten Tabellen finden Sie im [[!DNL PostgreSQL] Dokumentation](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | Der Name der zu erstellenden Tabelle. |

**Beispiel**

Die folgende Abfrage erstellt eine neue Tabelle `films_recent` aus nur aktuellen Einträgen der Tabelle `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

Die `SHOW` zeigt die aktuelle Einstellung der Laufzeitparameter an. Diese Variablen können mithilfe der Variablen `SET` Anweisung, indem Sie die `postgresql.conf` Konfigurationsdatei über die `PGOPTIONS` Umgebungsvariable (bei Verwendung von libpq oder einer libpq-basierten Anwendung) oder durch Befehlszeilenflags beim Starten des Postgres-Servers.

```sql
SHOW name
SHOW ALL
```

| Parameter | Beschreibung |
| ------ | ------ |
| `name` | Der Name des Laufzeitparameters, zu dem Sie Informationen benötigen. Mögliche Werte für den Laufzeitparameter sind die folgenden Werte:<br>`SERVER_VERSION`: Dieser Parameter zeigt die Versionsnummer des Servers an.<br>`SERVER_ENCODING`: Dieser Parameter zeigt die serverseitige Zeichensatzkodierung an.<br>`LC_COLLATE`: Dieser Parameter zeigt die Gebietsschemaeinstellung der Datenbank für die Sortierung (Textanordnung) an.<br>`LC_CTYPE`: Dieser Parameter zeigt die Gebietsschemaeinstellung der Datenbank für die Zeichenklassifizierung an.<br>`IS_SUPERUSER`: Dieser Parameter zeigt an, ob die aktuelle Rolle über Superuser-Berechtigungen verfügt. |
| `ALL` | Zeigt die Werte aller Konfigurationsparameter mit Beschreibungen an. |

**Beispiel**

Die folgende Abfrage zeigt die aktuelle Einstellung des Parameters `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### KOPIE

Die `COPY` -Befehl dupliziert die Ausgabe eines `SELECT` an einen bestimmten Ort abrufen. Der Benutzer muss Zugriff auf diesen Speicherort haben, damit dieser Befehl erfolgreich ausgeführt werden kann.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Parameter | Beschreibung |
| ------ | ------ |
| `query` | Die Abfrage, die Sie kopieren möchten. |
| `format_name` | Das Format, in das die Abfrage kopiert werden soll. Die `format_name` kann eines von `parquet`, `csv`oder `json`. Standardmäßig ist der Wert `parquet`. |

>[!NOTE]
>
>Der vollständige Ausgabepfad `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTERSTABELLE {#alter-table}

Die `ALTER TABLE` -Befehl können Sie Primär- oder Fremdschlüsseleinschränkungen hinzufügen oder ablegen sowie Spalten zur Tabelle hinzufügen.


#### EINSCHRÄNKUNG HINZUFÜGEN ODER ABLEGEN

Die folgenden SQL-Abfragen zeigen Beispiele für das Hinzufügen oder Ablegen von Begrenzungen zu einer Tabelle.

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY IDENTITY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT IDENTITY ( column_name )
```

| Parameter | Beschreibung |
| ------ | ------ |
| `table_name` | Der Name der Tabelle, die Sie bearbeiten. |
| `column_name` | Der Name der Spalte, der Sie eine Einschränkung hinzufügen. |
| `referenced_table_name` | Der Name der Tabelle, auf die der Fremdschlüssel verweist. |
| `primary_column_name` | Der Name der Spalte, auf die der Fremdschlüssel verweist. |


>[!NOTE]
>
>Das Tabellenschema sollte eindeutig sein und nicht von mehreren Tabellen gemeinsam genutzt werden. Darüber hinaus ist der Namespace für Primärschlüssel, primäre Identität und Identitätseinschränkungen obligatorisch.

#### Primäre und sekundäre Identitäten hinzufügen oder löschen

Die `ALTER TABLE` -Befehl können Sie über SQL direkt Begrenzungen für primäre und sekundäre Identitätstabelle-Spalten hinzufügen oder löschen.

Die folgenden Beispiele fügen eine primäre Identität und eine sekundäre Identität hinzu, indem Einschränkungen hinzugefügt werden.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

Identitäten können auch durch Ablegen von Einschränkungen entfernt werden, wie im folgenden Beispiel gezeigt.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

Siehe Dokument unter [Festlegen von Identitäten in Ad-hoc-Datensätzen](../data-governance/ad-hoc-schema-identities.md) für detailliertere Informationen.

#### SPALTE HINZUFÜGEN

Die folgenden SQL-Abfragen zeigen Beispiele für das Hinzufügen von Spalten zu einer Tabelle.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Unterstützte Datentypen

In der folgenden Tabelle sind die zulässigen Datentypen für das Hinzufügen von Spalten zu einer Tabelle mit [!DNL Postgres SQL], XDM und die [!DNL Accelerated Database Recovery] (ADR) in Azure SQL.

| --- | PSQL-Client | XDM | ADR | Beschreibung |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | Ein numerischer Datentyp zum Speichern großer Ganzzahlen zwischen -9.223.372.036.854.775.807 und 9.223.372.036.854.775.807 in 8 Byte. |
| 2 | `integer` | `int4` | `integer` | Ein numerischer Datentyp zum Speichern von Ganzzahlen zwischen -2.147.483.648 und 2.147.483.647 in 4 Byte. |
| 3 | `smallint` | `int2` | `smallint` | Ein numerischer Datentyp zum Speichern von Ganzzahlen zwischen -32.768 und 215-1 32.767 in 2 Byte. |
| 4 | `tinyint` | `int1` | `tinyint` | Ein numerischer Datentyp zum Speichern von Ganzzahlen zwischen 0 und 255 in 1 Byte. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | Ein Datentyp mit Zeichen, der variablengroß ist. `varchar` wird am besten verwendet, wenn die Größe der Spaltendateneinträge erheblich variiert. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` und `FLOAT` sind gültige Synonyme für `DOUBLE PRECISION`. `double precision` ist ein Gleitkomma-Datentyp. Gleitkommawerte werden in 8 Byte gespeichert. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` ist ein gültiges Synonym für `double precision`.`double precision` ist ein Gleitkomma-Datentyp. Gleitkommawerte werden in 8 Byte gespeichert. |
| 8 | `date` | `date` | `date` | Die `date` -Datentyp sind 4-Byte-gespeicherte Kalenderdatumswerte ohne Zeitstempelinformationen. Der Datumsbereich reicht vom 01-01-0001 bis zum 12-31-999. |
| 9 | `datetime` | `datetime` | `datetime` | Ein Datentyp, mit dem ein als Kalenderdatum und -zeit ausgedrückter Zeitpunkt gespeichert wird. `datetime` umfasst die Zähler für: Jahr, Monat, Tag, Stunde, Sekunde und Fraktion. A `datetime` Die Deklaration kann eine Teilmenge dieser Zeiteinheiten enthalten, die in dieser Sequenz zusammengefügt sind, oder sogar nur eine Zeiteinheit umfassen. |
| 10 | `char(len)` | `string` | `char(len)` | Die `char(len)` -Keyword wird verwendet, um anzugeben, dass es sich bei dem Element um ein Zeichen mit fester Länge handelt. |

#### SCHEMA HINZUFÜGEN

Die folgende SQL-Abfrage zeigt ein Beispiel für das Hinzufügen einer Tabelle zu einer Datenbank/einem Schema.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> ADLS-Tabellen und -Ansichten können nicht zu DWH-Datenbanken/-Schemata hinzugefügt werden.


#### SCHEMA ENTFERNEN

Die folgende SQL-Abfrage zeigt ein Beispiel für das Entfernen einer Tabelle aus einer Datenbank/einem Schema.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> DWH-Tabellen und -Ansichten können nicht aus physisch verknüpften DWH-Datenbanken/-Schemata entfernt werden.


**Parameter**

| Parameter | Beschreibung |
| ------ | ------ |
| `table_name` | Der Name der Tabelle, die Sie bearbeiten. |
| `column_name` | Der Name der Spalte, die Sie hinzufügen möchten. |
| `data_type` | Der Datentyp der Spalte, die Sie hinzufügen möchten. Zu den unterstützten Datentypen gehören: bigint, char, string, date, datetime, double, double Precision, integer, smallint, tinyint, varchar. |

### PRIMÄRE SCHLÜSSEL ANZEIGEN

Die `SHOW PRIMARY KEYS` führt alle Primärschlüsseleinschränkungen für die jeweilige Datenbank auf.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### AUSLÄNDLICHE SCHLÜSSEL ANZEIGEN

Die `SHOW FOREIGN KEYS` führt alle Fremdschlüsseleinschränkungen für die jeweilige Datenbank auf.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### DATAGROUPS ANZEIGEN

Die `SHOW DATAGROUPS` gibt eine Tabelle aller zugehörigen Datenbanken zurück. Die Tabelle enthält für jede Datenbank Schema, Gruppentyp, untergeordneten Typ, untergeordneten Namen und untergeordnete ID.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Data Warehouse Table | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### DATENAGROUPS FÜR Tabelle ANZEIGEN

Die `SHOW DATAGROUPS FOR` Der Befehl &#39;table_name&#39; gibt eine Tabelle aller zugehörigen Datenbanken zurück, die den Parameter als untergeordnetes Element enthalten. Die Tabelle enthält für jede Datenbank Schema, Gruppentyp, untergeordneten Typ, untergeordneten Namen und untergeordnete ID.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parameter**

- `table_name`: Der Name der Tabelle, für die Sie verknüpfte Datenbanken suchen möchten.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
