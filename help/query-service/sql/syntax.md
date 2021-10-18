---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; SQL-Syntax; SQL; ctas; CTAS; Erstellen einer Tabelle als ausgewählt
solution: Experience Platform
title: SQL-Syntax in Query Service
topic-legacy: syntax
description: Dieses Dokument zeigt die von Adobe Experience Platform Query Service unterstützte SQL-Syntax.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 6f697bb249c50e58f9e8a5821fa71f2d4c9a7aac
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 13%

---

# SQL-Syntax in Query Service

Adobe Experience Platform Query Service bietet die Möglichkeit, Standard-ANSI-SQL für `SELECT`-Anweisungen und andere eingeschränkte Befehle zu verwenden. Dieses Dokument behandelt die von [!DNL Query Service] unterstützte SQL-Syntax.

## Abfragen auswählen {#select-queries}

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

Die folgenden Unterabschnitte enthalten Details zu zusätzlichen Klauseln, die Sie in Ihren Abfragen verwenden können, sofern sie dem oben beschriebenen Format entsprechen.

### SNAPSHOT-Klausel

Diese Klausel kann verwendet werden, um Daten auf einer Tabelle basierend auf Momentaufnahmen-IDs inkrementell zu lesen. Eine Snapshot-ID ist eine Checkpoint-Markierung, die durch eine Long-Typ-Zahl dargestellt wird, die jedes Mal, wenn Daten in eine Data Lake-Tabelle geschrieben werden, auf eine Data Lake-Tabelle angewendet wird. Die `SNAPSHOT`-Klausel hängt sich an die Tabellenbeziehung an, neben der sie verwendet wird.

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

Beachten Sie, dass eine `SNAPSHOT`-Klausel mit einem Tabellen- oder Tabellenalias arbeitet, jedoch nicht über einer Unter-Abfrage oder Ansicht. Eine `SNAPSHOT`-Klausel funktioniert überall dort, wo eine `SELECT`-Abfrage auf einer Tabelle angewendet werden kann.

Darüber hinaus können Sie `HEAD` und `TAIL` als spezielle Offset-Werte für Momentaufnahmen-Klauseln verwenden. Die Verwendung von `HEAD` bezieht sich auf einen Offset vor dem ersten Snapshot, während `TAIL` auf einen Offset nach dem letzten Snapshot verweist.

>[!NOTE]
>
>Wenn Sie zwischen zwei Snapshot-IDs abfragen und der Start-Snapshot abgelaufen ist, können die beiden folgenden Szenarien eintreten, je nachdem, ob das optionale Fallback-Verhalten-Flag (`resolve_fallback_snapshot_on_failure`) gesetzt ist:
>
>- Wenn das optionale Fallback-Verhalten-Flag gesetzt ist, wählt Query Service den frühesten verfügbaren Snapshot aus, legt ihn als Start-Snapshot fest und gibt die Daten zwischen dem frühesten verfügbaren Snapshot und dem angegebenen End-Snapshot zurück. Diese Daten sind **einschließlich** der frühesten verfügbaren Momentaufnahme.
>
>- Wenn das optionale Fallback-Verhalten-Flag nicht gesetzt ist, wird ein Fehler zurückgegeben.


### WHERE-Klausel

Bei Treffern, die von einer `WHERE`-Klausel für eine `SELECT`-Abfrage erzeugt werden, wird standardmäßig zwischen Groß- und Kleinschreibung unterschieden. Wenn Sie möchten, dass Übereinstimmungen nicht zwischen Groß- und Kleinschreibung unterscheiden, können Sie den Suchbegriff `ILIKE` anstelle von `LIKE` verwenden.

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

Eine `SELECT`-Abfrage, die Joins verwendet, hat die folgende Syntax:

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
- `rowvalidation`: (Optional) Gibt an, ob der Benutzer die Überprüfung aller neuen Batches auf Zeilenebene wünscht, die für den neu erstellten Datensatz erfasst werden. Der Standardwert lautet `true`.
- `select_query`: Eine  `SELECT` Anweisung. Die Syntax der `SELECT`-Abfrage finden Sie im Abschnitt [SELECT-Abfragen](#select-queries).

**Beispiel**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>Die `SELECT`-Anweisung muss einen Alias für die Aggregat-Funktionen wie `COUNT`, `SUM`, `MIN` usw. enthalten. Darüber hinaus kann die `SELECT`-Anweisung mit oder ohne Klammern () bereitgestellt werden. Sie können eine `SNAPSHOT`-Klausel bereitstellen, um inkrementelle Deltas in die Zieltabelle zu lesen.

## INSERT INTO

Der Befehl `INSERT INTO` wird wie folgt definiert:

```sql
INSERT INTO table_name select_query
```

**Parameter**

- `table_name`: Der Name der Tabelle, in die die Abfrage eingefügt werden soll.
- `select_query`: Eine  `SELECT` Anweisung. Die Syntax der `SELECT`-Abfrage finden Sie im Abschnitt [SELECT-Abfragen](#select-queries).

**Beispiel**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> Die `SELECT`-Anweisung **darf nicht** in Klammern () stehen. Darüber hinaus muss das Schema des Ergebnisses der `SELECT`-Anweisung mit dem der Tabelle übereinstimmen, die in der `INSERT INTO`-Anweisung definiert ist. Sie können eine `SNAPSHOT`-Klausel bereitstellen, um inkrementelle Deltas in die Zieltabelle zu lesen.

## DROP TABLE

Der Befehl `DROP TABLE` legt eine vorhandene Tabelle ab und löscht das mit der Tabelle verknüpfte Verzeichnis aus dem Dateisystem, wenn es sich nicht um eine externe Tabelle handelt. Wenn die Tabelle nicht vorhanden ist, tritt eine Ausnahme auf.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**Parameter**

- `IF EXISTS`: Wenn dies angegeben ist, wird keine Ausnahme ausgelöst, wenn die Tabelle  **** keine Liste enthält.

## DROP-DATENBANK

Der Befehl `DROP DATABASE` legt eine vorhandene Datenbank ab.

```sql
DROP DATABASE [IF EXISTS] db_name
```

**Parameter**

- `IF EXISTS`: Wenn dies angegeben ist, wird keine Ausnahme ausgelöst, wenn die Datenbank  **** keine Liste enthält.

## DROP-SCHEMA

Der Befehl `DROP SCHEMA` legt ein vorhandenes Schema ab.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

**Parameter**

- `IF EXISTS`: Wenn dies angegeben ist, wird keine Ausnahme ausgelöst, wenn das Schema  **** keine -Liste enthält.

- `RESTRICT`: Standardwert für den Modus. Wenn dies angegeben wird, wird das Schema nur gelöscht, wenn **keine** Tabellen enthält.

- `CASCADE`: Wenn dies angegeben wird, wird das Schema zusammen mit allen im Schema vorhandenen Tabellen abgelegt.

## CREATE VIEW

Die folgende Syntax definiert eine `CREATE VIEW` -Abfrage:

```sql
CREATE VIEW view_name AS select_query
```

**Parameter**

- `view_name`: Der Name der zu erstellenden Ansicht.
- `select_query`: Eine  `SELECT` Anweisung. Die Syntax der `SELECT`-Abfrage finden Sie im Abschnitt [SELECT-Abfragen](#select-queries).

**Beispiel**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## DROP VIEW

Die folgende Syntax definiert eine `DROP VIEW` -Abfrage:

```sql
DROP VIEW [IF EXISTS] view_name
```

**Parameter**

- `IF EXISTS`: Wenn dies angegeben ist, wird keine Ausnahme ausgelöst, wenn die Ansicht  **** keine -Liste enthält.
- `view_name`: Der Name der zu löschenden Ansicht.

**Beispiel**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL-Befehle

Der folgende Unterabschnitt behandelt die von Query Service unterstützten Spark-SQL-Befehle.

### SET

Der Befehl `SET` legt eine Eigenschaft fest und gibt entweder den Wert einer vorhandenen Eigenschaft zurück oder listet alle vorhandenen Eigenschaften auf. Wenn für einen vorhandenen Eigenschaftenschlüssel ein Wert angegeben wird, wird der alte Wert überschrieben.

```sql
SET property_key = property_value
```

**Parameter**

- `property_key`: Der Name der Eigenschaft, die Sie auflisten oder ändern möchten.
- `property_value`: Der Wert, als den die Eigenschaft festgelegt werden soll.

Um den Wert für eine Einstellung zurückzugeben, verwenden Sie `SET [property key]` ohne `property_value`.

## PostgreSQL-Befehle

Die folgenden Unterabschnitte decken die von Query Service unterstützten PostgreSQL-Befehle ab.

### BEGIN

Der Befehl `BEGIN` oder alternativ der Befehl `BEGIN WORK` oder `BEGIN TRANSACTION` löst einen Transaktionsblock aus. Alle Anweisungen, die nach dem Befehl &quot;begin&quot;eingegeben werden, werden in einer einzigen Transaktion ausgeführt, bis ein expliziter COMMIT- oder ROLLBACK-Befehl angegeben wird. Dieser Befehl entspricht `START TRANSACTION`.

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

Mit dem Befehl `DEALLOCATE` können Sie die Zuordnung einer zuvor vorbereiteten SQL-Anweisung aufheben. Wenn Sie die Zuordnung einer vorbereiteten Anweisung nicht explizit aufheben, wird dies am Ende der Sitzung ausgeführt. Weitere Informationen zu vorbereiteten Anweisungen finden Sie im Abschnitt [PREPARE command](#prepare) .

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Wenn `DEALLOCATE name` verwendet wird, stellt `name` den Namen der vorbereiteten Anweisung dar, die aufgehoben werden muss. Wenn `DEALLOCATE ALL` verwendet wird, wird die Zuweisung aller vorbereiteten Anweisungen aufgehoben.

### DECLARE

Mit dem Befehl `DECLARE` kann ein Benutzer einen Cursor erstellen, mit dem eine kleine Anzahl von Zeilen aus einer größeren Abfrage abgerufen werden kann. Nachdem der Cursor erstellt wurde, werden Zeilen mit `FETCH` abgerufen.

```sql
DECLARE name CURSOR FOR query
```

**Parameter**

- `name`: Der Name des zu erstellenden Cursors.
- `query`: Ein `SELECT`- oder `VALUES`-Befehl, der die vom Cursor zurückzugebenden Zeilen angibt.

### EXECUTE

Der Befehl `EXECUTE` wird zum Ausführen einer zuvor vorbereiteten Anweisung verwendet. Da vorbereitete Anweisungen nur für die Dauer einer Sitzung vorhanden sind, muss die vorbereitete Anweisung durch eine `PREPARE`-Anweisung erstellt worden sein, die zuvor in der aktuellen Sitzung ausgeführt wurde. Weitere Informationen zur Verwendung vorbereiteter Anweisungen finden Sie im Abschnitt [`PREPARE` command](#prepare) .

Wenn in der `PREPARE` -Anweisung, mit der die Anweisung erstellt wurde, einige Parameter angegeben wurden, muss ein kompatibler Satz von Parametern an die `EXECUTE` -Anweisung übergeben werden. Wenn diese Parameter nicht übergeben werden, wird ein Fehler erzeugt.

```sql
EXECUTE name [ ( parameter ) ]
```

**Parameter**

- `name`: Der Name der vorbereiteten Anweisung, die ausgeführt werden soll.
- `parameter`: Der tatsächliche Wert eines Parameters für die vorbereitete Anweisung. Hierbei muss es sich um einen Ausdruck handeln, der einen Wert liefert, der mit dem Datentyp dieses Parameters kompatibel ist, der bei der Erstellung der vorbereiteten Anweisung festgelegt wurde.  Wenn mehrere Parameter für die vorbereitete Anweisung vorhanden sind, werden sie durch Kommas getrennt.

### EXPLAIN

Der Befehl `EXPLAIN` zeigt den Ausführungsplan für die angegebene Anweisung an. Der Ausführungsplan zeigt, wie die in der Anweisung referenzierten Tabellen gescannt werden.  Wenn mehrere Tabellen referenziert werden, wird angezeigt, welche Join-Algorithmen verwendet werden, um die erforderlichen Zeilen aus jeder Eingabetabelle zusammenzuführen.

```sql
EXPLAIN option statement
```

Dabei kann `option` einer der folgenden sein:

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**Parameter**

- `ANALYZE`: Wenn die  `option` enthält, werden  `ANALYZE`die Laufzeiten und andere Statistiken angezeigt.
- `FORMAT`: Wenn der  `option` enthält, gibt er  `FORMAT`das Ausgabeformat an, das  `TEXT` oder  `JSON`sein kann. Die Ausgabe ohne Text enthält dieselben Informationen wie das Textausgabeformat, ist jedoch für Programme einfacher zu analysieren. Dieser Parameter ist standardmäßig auf `TEXT` voreingestellt.
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

Mit dem Befehl `PREPARE` können Sie eine vorbereitete Anweisung erstellen. Eine vorbereitete Anweisung ist ein serverseitiges Objekt, das zur Vorlagenbildung für ähnliche SQL-Anweisungen verwendet werden kann.

Vorbereitete Anweisungen können Parameter annehmen, d. h. Werte, die bei der Ausführung in der Anweisung ersetzt werden. Parameter werden nach Position referenziert, indem bei der Verwendung vorbereiteter Anweisungen $1, $2 usw. verwendet werden.

Optional können Sie eine Liste von Parameterdatentypen angeben. Wenn der Datentyp eines Parameters nicht aufgeführt ist, kann der Typ aus dem Kontext abgeleitet werden.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**Parameter**

- `name`: Der Name für die vorbereitete Anweisung.
- `data_type`: Die Datentypen der Parameter der vorbereiteten Anweisung. Wenn der Datentyp eines Parameters nicht aufgeführt ist, kann der Typ aus dem Kontext abgeleitet werden. Wenn Sie mehrere Datentypen hinzufügen müssen, können Sie sie in einer durch Kommas getrennten Liste hinzufügen.

### ROLLBACK

Der Befehl `ROLLBACK` macht die aktuelle Transaktion rückgängig und verwirft alle durch die Transaktion vorgenommenen Aktualisierungen.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECT INTO

Der Befehl `SELECT INTO` erstellt eine neue Tabelle und füllt sie mit Daten, die durch eine Abfrage berechnet wurden. Die Daten werden nicht an den Client zurückgegeben, wie bei einem normalen `SELECT`-Befehl. Die Spalten der neuen Tabelle haben die Namen und Datentypen, die mit den Ausgabespalten des Befehls `SELECT` verknüpft sind.

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

Weitere Informationen zu den standardmäßigen SELECT-Abfrageparametern finden Sie im Abschnitt [SELECT-Abfrage](#select-queries). In diesem Abschnitt werden nur Parameter aufgelistet, die ausschließlich dem Befehl `SELECT INTO` entsprechen.

- `TEMPORARY` oder  `TEMP`: Ein optionaler Parameter. Wenn angegeben, ist die zu erstellende Tabelle eine temporäre Tabelle.
- `UNLOGGED`: Ein optionaler Parameter. Wenn angegeben, ist die Tabelle, die wie erstellt wird, eine nicht protokollierte Tabelle. Weitere Informationen zu nicht protokollierten Tabellen finden Sie in der [PostgreSQL-Dokumentation](https://www.postgresql.org/docs/current/sql-createtable.html).
- `new_table`: Der Name der zu erstellenden Tabelle.

**Beispiel**

Die folgende Abfrage erstellt eine neue Tabelle `films_recent`, die nur aus den letzten Einträgen der Tabelle `films` besteht:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

Der Befehl `SHOW` zeigt die aktuelle Einstellung der Laufzeitparameter an. Diese Variablen können mithilfe der `SET`-Anweisung, durch Bearbeiten der Konfigurationsdatei `postgresql.conf`, durch die Umgebungsvariable `PGOPTIONS` (bei Verwendung von libpq oder einer libpq-basierten Anwendung) oder durch Befehlszeilenflags beim Starten des Postgres-Servers festgelegt werden.

```sql
SHOW name
SHOW ALL
```

**Parameter**

- `name`: Der Name des Laufzeitparameters, zu dem Sie Informationen benötigen. Mögliche Werte für den Laufzeitparameter sind die folgenden Werte:
   - `SERVER_VERSION`: Dieser Parameter zeigt die Versionsnummer des Servers an.
   - `SERVER_ENCODING`: Dieser Parameter zeigt die serverseitige Zeichensatzkodierung an.
   - `LC_COLLATE`: Dieser Parameter zeigt die Gebietsschemaeinstellung der Datenbank für die Sortierung (Textanordnung) an.
   - `LC_CTYPE`: Dieser Parameter zeigt die Gebietsschemaeinstellung der Datenbank für die Zeichenklassifizierung an.
      `IS_SUPERUSER`: Dieser Parameter zeigt an, ob die aktuelle Rolle über Superuser-Berechtigungen verfügt.
- `ALL`: Zeigt die Werte aller Konfigurationsparameter mit Beschreibungen an.

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

Der Befehl `COPY` gibt die Ausgabe einer `SELECT`-Abfrage an einen angegebenen Speicherort aus. Der Benutzer muss Zugriff auf diesen Speicherort haben, damit dieser Befehl erfolgreich ausgeführt werden kann.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**Parameter**

- `query`: Die Abfrage, die Sie kopieren möchten.
- `format_name`: Das Format, in das Sie die Abfrage kopieren möchten. Das `format_name` kann eines von `parquet`, `csv` oder `json` sein. Der Standardwert ist `parquet`.

>[!NOTE]
>
>Der vollständige Ausgabepfad lautet `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>` .

### ALTERSTABELLE

Mit dem Befehl `ALTER TABLE` können Sie Primär- oder Fremdschlüsseleinschränkungen hinzufügen oder ablegen sowie Spalten zur Tabelle hinzufügen.

#### EINSCHRÄNKUNG HINZUFÜGEN ODER ABLEGEN

Die folgenden SQL-Abfragen zeigen Beispiele für das Hinzufügen oder Ablegen von Begrenzungen zu einer Tabelle.

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**Parameter**

- `table_name`: Der Name der Tabelle, die Sie bearbeiten.
- `constraint_name`: Der Name der Einschränkung, die Sie hinzufügen oder löschen möchten.
- `column_name`: Der Name der Spalte, der Sie eine Einschränkung hinzufügen.
- `referenced_table_name`: Der Name der Tabelle, auf die der Fremdschlüssel verweist.
- `primary_column_name`: Der Name der Spalte, auf die der Fremdschlüssel verweist.

>[!NOTE]
>
>Das Tabellenschema sollte eindeutig sein und nicht von mehreren Tabellen gemeinsam genutzt werden. Darüber hinaus ist der Namespace für Primärschlüsseleinschränkungen obligatorisch.

#### SPALTE HINZUFÜGEN

Die folgenden SQL-Abfragen zeigen Beispiele für das Hinzufügen von Spalten zu einer Tabelle.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**Parameter**

- `table_name`: Der Name der Tabelle, die Sie bearbeiten.
- `column_name`: Der Name der Spalte, die Sie hinzufügen möchten.
- `data_type`: Der Datentyp der Spalte, die Sie hinzufügen möchten. Zu den unterstützten Datentypen zählen: bigint, char, string, date, datetime, double, double Precision, integer, smallint, tinyint, varchar.

### PRIMÄRE SCHLÜSSEL ANZEIGEN

Der Befehl `SHOW PRIMARY KEYS` listet alle Primärschlüsseleinschränkungen für die jeweilige Datenbank auf.

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

Der Befehl `SHOW FOREIGN KEYS` listet alle Fremdschlüsseleinschränkungen für die jeweilige Datenbank auf.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
