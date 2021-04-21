---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;SQL-Syntax;sql;ctas;CTAS;Tabelle erstellen als Auswahl
solution: Experience Platform
title: SQL-Syntax im Abfrage-Dienst
topic-legacy: syntax
description: Dieses Dokument zeigt die SQL-Syntax, die vom Adobe Experience Platform Abfrage Service unterstützt wird.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 14%

---

# SQL-Syntax in Abfrage Service

Der Adobe Experience Platform Abfrage Service bietet die Möglichkeit, ANSI-StandardSQL für `SELECT`-Anweisungen und andere eingeschränkte Befehle zu verwenden. Dieses Dokument behandelt die SQL-Syntax, die von [!DNL Query Service] unterstützt wird.

## AUSWÄHLEN VON Abfragen {#select-queries}

Die folgende Syntax definiert eine `SELECT`-Abfrage, die von [!DNL Query Service] unterstützt wird:

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

wobei `from_item` eine der folgenden Optionen sein kann:

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

Die folgenden Unterabschnitte enthalten Details zu Zusatzklauseln, die Sie in Ihren Abfragen verwenden können, sofern sie dem oben beschriebenen Format entsprechen.

### SNAPSHOT-Klausel

Diese Klausel kann verwendet werden, um Daten auf einer Tabelle basierend auf Snapshot-IDs inkrementell zu lesen. Eine Schnappschuss-ID ist eine Checkpoint-Markierung, die durch eine lange Nummer dargestellt wird, die bei jedem Schreiben der Daten auf eine Daten-Seetabelle angewendet wird. Die `SNAPSHOT`-Klausel hängt sich an die Tabellenbeziehung an, die sie neben verwendet wird.

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

Beachten Sie, dass eine `SNAPSHOT`-Klausel mit einem Tabellen- oder Tabellenalias, jedoch nicht über einer Unter-Abfrage oder Ansicht funktioniert. Eine `SNAPSHOT`-Klausel funktioniert überall dort, wo eine `SELECT`-Abfrage auf einer Tabelle angewendet werden kann.

Zusätzlich können Sie `HEAD` und `TAIL` als spezielle Offset-Werte für Snapshot-Klauseln verwenden. Die Verwendung von `HEAD` bezieht sich auf einen Offset vor dem ersten Schnappschuss, während `TAIL` auf einen Offset nach dem letzten Schnappschuss verweist.

### WO-Klausel

Bei Übereinstimmungen, die mit einer `WHERE`-Klausel auf einer `SELECT`-Abfrage erstellt wurden, wird standardmäßig die Groß-/Kleinschreibung beachtet. Wenn bei Übereinstimmungen nicht zwischen Groß- und Kleinschreibung unterschieden werden soll, können Sie anstelle von `LIKE` den Suchbegriff `ILIKE` verwenden.

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

Eine `SELECT`-Abfrage, die Joins verwendet, hat folgende Syntax:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION, INTERSECT und EXCEPT

Die Klauseln `UNION`, `INTERSECT` und `EXCEPT` werden verwendet, um gleichartige Zeilen aus zwei oder mehr Tabellen zu kombinieren oder auszuschließen:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREATE TABLE AS SELECT

Die folgende Syntax definiert eine `CREATE TABLE AS SELECT` (CTAS)-Abfrage:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

**Parameter**

- `schema`: Der Titel des XDM-Schemas. Verwenden Sie diese Klausel nur, wenn Sie ein vorhandenes XDM-Schema für den neuen Datensatz verwenden möchten, der von der CTAS-Abfrage erstellt wurde.
- `rowvalidation`: (Optional) Gibt an, ob der Benutzer eine Validierung auf Zeilenebene für alle neuen Stapel wünscht, die für den neu erstellten Datensatz erfasst werden. Der Standardwert lautet `true`.
- `select_query`: Eine  `SELECT` Aussage. Die Syntax der `SELECT`-Abfrage finden Sie im Abschnitt [SELECT-Abfragen](#select-queries).

**Beispiel**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>Die `SELECT`-Anweisung muss einen Alias für die Aggregat-Funktionen wie `COUNT`, `SUM`, `MIN` usw. enthalten. Darüber hinaus kann die `SELECT`-Anweisung mit oder ohne Klammern () bereitgestellt werden. Sie können eine `SNAPSHOT`-Klausel bereitstellen, um inkrementelle Deltas in der Tabelle &quot;Zielgruppe&quot;zu lesen.

## INSERT INTO

Der Befehl `INSERT INTO` wird wie folgt definiert:

```sql
INSERT INTO table_name select_query
```

**Parameter**

- `table_name`: Der Name der Tabelle, in die die Abfrage eingefügt werden soll.
- `select_query`: Eine  `SELECT` Aussage. Die Syntax der `SELECT`-Abfrage finden Sie im Abschnitt [SELECT-Abfragen](#select-queries).

**Beispiel**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> Die `SELECT`-Anweisung **darf nicht** in Klammern () stehen. Darüber hinaus muss das Schema des Ergebnisses der `SELECT`-Anweisung mit dem in der `INSERT INTO`-Anweisung definierten  übereinstimmen. Sie können eine `SNAPSHOT`-Klausel bereitstellen, um inkrementelle Deltas in der Tabelle &quot;Zielgruppe&quot;zu lesen.

## DROP TABLE

Der Befehl `DROP TABLE` legt eine vorhandene Tabelle ab und löscht den mit der Tabelle verknüpften Ordner aus dem Dateisystem, wenn es sich nicht um eine externe Tabelle handelt. Wenn die Tabelle nicht vorhanden ist, tritt eine Ausnahme auf.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**Parameter**

- `IF EXISTS`: Wenn dies angegeben ist, wird keine Ausnahme ausgelöst, wenn die Tabelle  **** nicht vorhanden ist.

## CREATE VIEW

Die folgende Syntax definiert eine `CREATE VIEW`-Abfrage:

```sql
CREATE VIEW view_name AS select_query
```

**Parameter**

- `view_name`: Der Name der zu erstellenden Ansicht.
- `select_query`: Eine  `SELECT` Aussage. Die Syntax der `SELECT`-Abfrage finden Sie im Abschnitt [SELECT-Abfragen](#select-queries).

**Beispiel**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## DROP VIEW

Die folgende Syntax definiert eine `DROP VIEW`-Abfrage:

```sql
DROP VIEW [IF EXISTS] view_name
```

**Parameter**

- `IF EXISTS`: Wenn dieser Wert angegeben ist, wird keine Ausnahme ausgelöst, wenn die Ansicht  **** keine ist.
- `view_name`: Der Name der zu löschenden Ansicht.

**Beispiel**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL-Befehle

Im folgenden Unterabschnitt werden die von Abfrage Service unterstützten Spark-SQL-Befehle beschrieben.

### SET

Der Befehl `SET` legt eine Eigenschaft fest und gibt entweder den Wert einer vorhandenen Eigenschaft zurück oder alle vorhandenen Eigenschaften werden Liste. Wenn für einen vorhandenen Eigenschaftenschlüssel ein Wert angegeben wird, wird der alte Wert überschrieben.

```sql
SET property_key = property_value
```

**Parameter**

- `property_key`: Der Name der Eigenschaft, die Liste oder geändert werden soll.
- `property_value`: Der Wert, als den die Eigenschaft festgelegt werden soll.

Um den Wert für eine Einstellung zurückzugeben, verwenden Sie `SET [property key]` ohne `property_value`.

## PostgreSQL-Befehle

Die folgenden Unterabschnitte decken die von Abfrage Service unterstützten PostgreSQL-Befehle ab.

### BEGIN

Der Befehl `BEGIN` oder alternativ der Befehl `BEGIN WORK` oder `BEGIN TRANSACTION` initiiert einen Transaktionsblock. Alle Anweisungen, die nach dem Befehl &quot;begin&quot;eingegeben werden, werden in einer einzigen Transaktion ausgeführt, bis ein expliziter COMMIT- oder ROLLBACK-Befehl angegeben ist. Dieser Befehl ist identisch mit `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CLOSE

Der Befehl `CLOSE` gibt die Ressourcen frei, die mit einem geöffneten Cursor verknüpft sind. Nach dem Schließen des Cursors sind keine weiteren Vorgänge zulässig. Ein Cursor sollte geschlossen werden, wenn er nicht mehr benötigt wird.

```sql
CLOSE name
CLOSE ALL
```

Wenn `CLOSE name` verwendet wird, stellt `name` den Namen eines geöffneten Cursors dar, der geschlossen werden muss. Wenn `CLOSE ALL` verwendet wird, werden alle geöffneten Cursor geschlossen.

### DEALLOCATE

Mit dem Befehl `DEALLOCATE` können Sie die Zuweisung einer zuvor vorbereiteten SQL-Anweisung aufheben. Wenn Sie die Zuordnung einer vorbereiteten Anweisung nicht explizit aufheben, wird dies am Ende der Sitzung ausgeführt. Weitere Informationen zu vorbereiteten Anweisungen finden Sie im Abschnitt [VORBEREITEN Befehl](#prepare).

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Wenn `DEALLOCATE name` verwendet wird, stellt `name` den Namen der vorbereiteten Anweisung dar, die dezugeordnet werden muss. Wenn `DEALLOCATE ALL` verwendet wird, wird die Zuordnung aller vorbereiteten Anweisungen aufgehoben.

### DECLARE

Mit dem Befehl `DECLARE` können Sie einen Cursor erstellen, mit dem Sie eine kleine Anzahl Zeilen aus einer größeren Abfrage abrufen können. Nachdem der Cursor erstellt wurde, werden Zeilen mit `FETCH` abgerufen.

```sql
DECLARE name CURSOR FOR query
```

**Parameter**

- `name`: Der Name des zu erstellenden Cursors.
- `query`: Ein `SELECT`- oder `VALUES`-Befehl, der die vom Cursor zurückzugebenden Zeilen angibt.

### EXECUTE

Mit dem Befehl `EXECUTE` wird eine zuvor vorbereitete Anweisung ausgeführt. Da vorbereitete Anweisungen nur für die Dauer einer Sitzung vorhanden sind, muss die vorbereitete Anweisung durch eine `PREPARE`-Anweisung erstellt worden sein, die zuvor in der aktuellen Sitzung ausgeführt wurde. Weitere Informationen zur Verwendung vorbereiteter Anweisungen finden Sie im Abschnitt [`PREPARE` command](#prepare).

Wenn die `PREPARE`-Anweisung, mit der die Anweisung erstellt wurde, einige Parameter angegeben hat, muss ein kompatibler Satz von Parametern an die `EXECUTE`-Anweisung übergeben werden. Wenn diese Parameter nicht weitergegeben werden, wird ein Fehler ausgegeben.

```sql
EXECUTE name [ ( parameter ) ]
```

**Parameter**

- `name`: Der Name der vorbereiteten Anweisung, die ausgeführt werden soll.
- `parameter`: Der tatsächliche Wert eines Parameters für die vorbereitete Anweisung. Hierbei muss es sich um einen Ausdruck handeln, der einen Wert liefert, der mit dem Datentyp dieses Parameters kompatibel ist, der bei der Erstellung der vorbereiteten Anweisung festgelegt wurde.  Wenn mehrere Parameter für die vorbereitete Anweisung vorhanden sind, werden diese durch Kommas getrennt.

### EXPLAIN

Der Befehl `EXPLAIN` zeigt den Ausführungsplan für die angegebene Anweisung an. Der Ausführungsplan zeigt an, wie die Tabellen, auf die sich die Anweisung bezieht, gescannt werden.  Wenn mehrere Tabellen referenziert werden, zeigt es, welche Verbindungsalgorithmen verwendet werden, um die erforderlichen Zeilen aus den einzelnen Eingabetabellen zusammenzuführen.

```sql
EXPLAIN option statement
```

Dabei kann `option` einer der folgenden sein:

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**Parameter**

- `ANALYZE`: Wenn der  `option` enthält  `ANALYZE`, werden die Laufzeiten und andere Statistiken angezeigt.
- `FORMAT`: Wenn die Datei  `option` enthält  `FORMAT`, gibt sie das Ausgabeformat an, das sein kann  `TEXT` oder  `JSON`. Die Ausgabe ohne Text enthält dieselben Informationen wie das Textausgabeformat, ist jedoch für Programme einfacher zu analysieren. Dieser Parameter ist standardmäßig auf `TEXT` voreingestellt.
- `statement`: Jede `SELECT`-, `INSERT`-, `UPDATE`-, `DELETE`-, `VALUES`-, `EXECUTE`-, `DECLARE`-, `CREATE TABLE AS`- oder `CREATE MATERIALIZED VIEW AS`-Anweisung, deren Ausführungsplan Sie sehen möchten.

>[!IMPORTANT]
>
> Denken Sie daran, dass die Anweisung genau genommen ausgeführt wird, wenn die `ANALYZE`-Option verwendet wird. Obwohl `EXPLAIN` alle Ausgaben verwirft, die `SELECT` zurückgibt, verworfen werden, treten andere Nebenwirkungen der Anweisung wie gewohnt auf.

**Beispiel**

Das folgende Beispiel zeigt den Plan für eine einfache Abfrage auf einer Tabelle mit einer einzelnen `integer`-Spalte und 10000 Zeilen:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

Der Befehl `FETCH` ruft Zeilen mit einem zuvor erstellten Cursor ab.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**Parameter**

- `num_of_rows`: Die Anzahl der abzurufenden Zeilen.
- `cursor_name`: Der Name des Cursors, aus dem Sie Informationen abrufen.

### PREPARE {#prepare}

Mit dem Befehl `PREPARE` können Sie eine vorbereitete Anweisung erstellen. Eine vorbereitete Anweisung ist ein serverseitiges Objekt, mit dem ähnliche SQL-Anweisungen als Vorlage dienen können.

Zubereitete Anweisungen können Parameter annehmen, bei denen es sich um Werte handelt, die bei der Ausführung in der Anweisung ersetzt werden. Parameter werden nach Position referenziert, unter Verwendung von $1, $2 usw., wenn vorbereitete Anweisungen verwendet werden.

Optional können Sie eine Liste von Parameterdatentypen angeben. Wenn der Datentyp eines Parameters nicht aufgeführt ist, kann der Typ aus dem Kontext abgeleitet werden.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**Parameter**

- `name`: Der Name der vorbereiteten Anweisung.
- `data_type`: Die Datentypen der Parameter der vorbereiteten Anweisung. Wenn der Datentyp eines Parameters nicht aufgeführt ist, kann der Typ aus dem Kontext abgeleitet werden. Wenn Sie mehrere Datentypen hinzufügen müssen, können Sie diese in einer durch Kommas getrennten Liste hinzufügen.

### ROLLBACK

Der Befehl `ROLLBACK` hebt die aktuelle Transaktion auf und verwirft alle durch die Transaktion vorgenommenen Aktualisierungen.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECT INTO

Mit dem Befehl `SELECT INTO` wird eine neue Tabelle erstellt und mit Daten gefüllt, die von einer Abfrage berechnet werden. Die Daten werden nicht an den Client zurückgegeben, wie bei einem normalen Befehl `SELECT`. Die Spalten der neuen Tabelle haben die Namen und Datentypen, die mit den Ausgabespalten des Befehls `SELECT` verknüpft sind.

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

**Parameter**

Weitere Informationen zu den Standardparametern für die SELECT-Abfrage finden Sie im Abschnitt [SELECT-Abfrage](#select-queries). In diesem Abschnitt werden nur Liste-Parameter angegeben, die ausschließlich für den Befehl `SELECT INTO` gelten.

- `TEMPORARY` oder  `TEMP`: Ein optionaler Parameter. Bei Angabe der Tabelle handelt es sich um eine temporäre Tabelle.
- `UNLOGGED`: Ein optionaler Parameter. Bei Angabe der Tabelle, die wie eine nicht angemeldete Tabelle erstellt wird. Weitere Informationen zu nicht protokollierten Tabellen finden Sie in der [PostgreSQL-Dokumentation](https://www.postgresql.org/docs/current/sql-createtable.html).
- `new_table`: Der Name der zu erstellenden Tabelle.

**Beispiel**

Mit der folgenden Abfrage wird eine neue Tabelle `films_recent` erstellt, die nur aus den letzten Einträgen der Tabelle `films` besteht:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

Der Befehl `SHOW` zeigt die aktuelle Einstellung der Laufzeitparameter an. Diese Variablen können mithilfe der Anweisung `SET`, durch Bearbeiten der Konfigurationsdatei `postgresql.conf`, durch die Umgebungsvariable `PGOPTIONS` (bei Verwendung von libpq oder einer libpq-basierten Anwendung) oder durch Befehlszeilenflags beim Starten des Postgres-Servers eingestellt werden.

```sql
SHOW name
SHOW ALL
```

**Parameter**

- `name`: Der Name des Laufzeitparameters, über den Sie Informationen erhalten möchten. Mögliche Werte für den Parameter runtime umfassen die folgenden Werte:
   - `SERVER_VERSION`: Dieser Parameter zeigt die Versionsnummer des Servers an.
   - `SERVER_ENCODING`: Dieser Parameter zeigt die serverseitige Zeichensatzkodierung.
   - `LC_COLLATE`: Dieser Parameter zeigt die Spracheinstellung der Datenbank für die Sortierreihenfolge (Textreihenfolge) an.
   - `LC_CTYPE`: Dieser Parameter zeigt die Spracheinstellung der Datenbank für die Zeichenklassifizierung an.
      `IS_SUPERUSER`: Dieser Parameter zeigt an, ob die aktuelle Rolle über Superuser-Berechtigungen verfügt.
- `ALL`: Zeigt die Werte aller Konfigurationsparameter mit Beschreibungen an.

**Beispiel**

Die folgende Abfrage zeigt die aktuelle Parametereinstellung `DateStyle`.

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

Mit dem Befehl `COPY` wird die Ausgabe einer `SELECT`-Abfrage an einen angegebenen Speicherort ausgeliefert. Der Benutzer muss Zugriff auf diesen Speicherort haben, damit dieser Befehl erfolgreich ausgeführt werden kann.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**Parameter**

- `query`: Die Abfrage, die Sie kopieren möchten.
- `format_name`: Das Format, in das die Abfrage kopiert werden soll. Das `format_name` kann eines von `parquet`, `csv` oder `json` sein. Der Standardwert ist `parquet`.

>[!NOTE]
>
>Der vollständige Ausgabepfad lautet `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTERNATIVTABELLE

Mit dem Befehl `ALTER TABLE` können Sie Primär- oder Fremdschlüsseleinschränkungen hinzufügen oder ablegen sowie Spalten zur Tabelle hinzufügen.

#### hinzufügen- oder DROP-BESCHRÄNKUNG

Die folgenden SQL-Abfragen zeigen Beispiele für das Hinzufügen oder Ablegen von Einschränkungen zu einer Tabelle.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**Parameter**

- `table_name`: Der Name der Tabelle, die Sie bearbeiten.
- `constraint_name`: Der Name der Beschränkung, die hinzugefügt oder gelöscht werden soll.
- `column_name`: Der Name der Spalte, der Sie eine Beschränkung hinzufügen.
- `referenced_table_name`: Der Name der Tabelle, auf die der Fremdschlüssel verweist.
- `primary_column_name`: Der Name der Spalte, auf die der Fremdschlüssel verweist.

>[!NOTE]
>
>Das Schema &quot;Tabelle&quot;sollte eindeutig sein und nicht für mehrere Tabellen freigegeben sein. Darüber hinaus ist der Namensraum für primäre Schlüsseleinschränkungen obligatorisch.

#### hinzufügen SPALTE

Die folgenden SQL-Abfragen zeigen Beispiele zum Hinzufügen von Spalten zu einer Tabelle.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**Parameter**

- `table_name`: Der Name der Tabelle, die Sie bearbeiten.
- `column_name`: Der Name der Spalte, die Sie hinzufügen möchten.
- `data_type`: Der Datentyp der Spalte, die Sie hinzufügen möchten. Folgende Datentypen werden unterstützt: bigint, char, string, date, datetime, Dublette, Genauigkeit der Dublette, integer, smallint, tinyint, varchar.

### PRIMÄR-TASTEN ANZEIGEN

Der Befehl `SHOW PRIMARY KEYS` Liste alle primären Schlüsseleinschränkungen für die jeweilige Datenbank.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### AUSLÄNDISCHE TASTEN ANZEIGEN

Der Befehl `SHOW FOREIGN KEYS` Liste alle Fremdschlüsseleinschränkungen für die jeweilige Datenbank.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
