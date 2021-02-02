---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;SQL-Syntax;sql;ctas;CTAS;Tabelle erstellen als Auswahl
solution: Experience Platform
title: SQL-Syntax
topic: syntax
description: In diesem Dokument finden Sie die von Query Service unterstützte SQL-Syntax.
translation-type: tm+mt
source-git-commit: 14cb1d304fd8aad2ca287f8d66ac6865425db4c5
workflow-type: tm+mt
source-wordcount: '2212'
ht-degree: 84%

---


# SQL-Syntax

[!DNL Query Service]Mit können Sie Standard-ANSI-SQL für `SELECT`-Anweisungen und andere begrenzte Befehle verwenden. Dieses Dokument zeigt die SQL-Syntax, die von [!DNL Query Service] unterstützt wird.

## Definieren einer SELECT-Abfrage

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

wobei `from_item` eines der Folgenden sein kann:

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

und `grouping_element` eines der Folgenden:

```sql
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

und `with_query`:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### SNAPSHOT-Klausel

Diese Klausel kann verwendet werden, um Daten in einer Tabelle inkrementell basierend auf Snapshot-IDs zu lesen. Eine Snapshot-ID ist eine Checkpoint-Markierung, die jedes Mal, wenn Daten in eine Datentabelle geschrieben werden, durch eine Zahl vom Typ &quot;Long&quot;identifiziert wird. Die SNAPSHOT-Klausel fügt sich in die Tabellenbeziehung ein, die sie neben der Tabelle verwendet.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Beispiel

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

Bitte beachten Sie, dass eine SNAPSHOT-Klausel mit einem Tabellen- oder Tabellenalias funktioniert, jedoch nicht über einer Unter-Abfrage oder Ansicht. Eine SNAPHOST-Klausel funktioniert überall dort, wo eine SELECT-Abfrage auf einer Tabelle angewendet werden kann.

### WHERE ILIKE-Klausel

Das Schlüsselwort ILIKE kann anstelle von LIKE verwendet werden, um Übereinstimmungen mit der WHERE-Klausel der SELECT-Abfrage zu finden, ohne die Groß-/Kleinschreibung zu berücksichtigen.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

Hier die Logik der LIKE- und ILIKE-Klauseln:
- ```WHERE condition LIKE pattern```, ```~~``` entspricht pattern
- ```WHERE condition NOT LIKE pattern```, ```!~~``` entspricht pattern
- ```WHERE condition ILIKE pattern```, ```~~*``` entspricht pattern
- ```WHERE condition NOT ILIKE pattern```, ```!~~*``` entspricht pattern


#### Beispiel

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Gibt Kunden zurück, deren Namen mit „A“ oder „a“ beginnen.

## JOINS

Eine `SELECT`-Abfrage mit JOINS hat die folgende Syntax:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## UNION, INTERSECT und EXCEPT

Die `UNION`-, `INTERSECT`- und `EXCEPT`-Klauseln werden unterstützt, um gleichartige Zeilen aus zwei oder mehr Tabellen zu kombinieren oder auszuschließen:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## CREATE TABLE AS SELECT

Die folgende Syntax definiert eine `CREATE TABLE AS SELECT` (CTAS)-Abfrage, die von [!DNL Query Service] unterstützt wird:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

wobei
`target_schema_title` ist der Titel des XDM-Schemas. Verwenden Sie diese Klausel nur, wenn Sie ein vorhandenes XDM-Schema für den neuen Datensatz verwenden möchten, der von CTAS Abfrage erstellt wurde
`rowvalidation` gibt an, ob der Benutzer die Überprüfung auf Zeilenebene aller neuen Stapel, die für den neu erstellten Datensatz erfasst werden, vornehmen möchte. Standardwert ist &quot;true&quot;

und `select_query` ist eine `SELECT`-Anweisung, deren Syntax oben in diesem Dokument definiert ist.


### Beispiel

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

Bitte beachten Sie Folgendes für eine CTAS-Abfrage:

1. Die `SELECT`-Anweisung muss einen Alias für die Aggregat-Funktionen wie `COUNT`, `SUM`, `MIN` usw. enthalten.
2. Die `SELECT`-Anweisung kann mit oder ohne Klammern () angegeben werden.
3. Die `SELECT`-Anweisung kann mit einer SNAPSHOT-Klausel bereitgestellt werden, um inkrementelle Deltas in die Zielgruppe zu lesen.

```sql
CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

## INSERT INTO

Die folgende Syntax definiert eine `INSERT INTO`-Abfrage, die von [!DNL Query Service] unterstützt wird:

```sql
INSERT INTO table_name select_query
```

wobei `select_query` eine `SELECT`-Anweisung ist, deren Syntax oben in diesem Dokument definiert ist.

### Beispiel

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

Bitte beachten Sie Folgendes für eine INSERT INTO-Abfrage:

1. Die `SELECT`-Anweisung DARF NICHT in Klammern () gesetzt werden.
2. Das Schema des Ergebnisses der `SELECT`-Anweisung muss mit dem in der `INSERT INTO`-Anweisung definierten Tabelle übereinstimmen.
3. Die `SELECT`-Anweisung kann mit einer SNAPSHOT-Klausel bereitgestellt werden, um inkrementelle Deltas in die Zielgruppe zu lesen.

```sql
INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

### DROP TABLE

Löscht eine Tabelle und löscht das mit der Tabelle verknüpfte Verzeichnis aus dem Dateisystem, wenn es sich nicht um eine EXTERNE Tabelle handelt. Wenn die zu löschende Tabelle nicht vorhanden ist, tritt ein Fehler (Ausnahmebedingung) auf.

```sql
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### Parameter

- `IF EXISTS`: Wenn die Tabelle nicht vorhanden ist, wird nichts ausgeführt
- `TEMP`: Temporäre Tabelle

## CREATE VIEW

Die folgende Syntax definiert eine `CREATE VIEW`-Abfrage, die von [!DNL Query Service] unterstützt wird:

```sql
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

wobei `view_name` der Name der zu erstellenden Ansicht
und `select_query` eine `SELECT`-Anweisung ist, deren Syntax oben in diesem Dokument definiert ist.

Beispiel:

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### DROP VIEW

Die folgende Syntax definiert eine `DROP VIEW`-Abfrage, die von [!DNL Query Service] unterstützt wird:

```sql
DROP VIEW [IF EXISTS] view_name
```

wobei `view_name` der Name der zu löschenden Ansicht ist

Beispiel:

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL-Befehle

### SET

Legen Sie eine Eigenschaft fest, geben Sie den Wert einer vorhandenen Eigenschaft zurück oder listen Sie alle vorhandenen Eigenschaften auf. Wenn für einen vorhandenen Eigenschaftenschlüssel ein Wert angegeben wird, wird der alte Wert überschrieben.

```sql
SET property_key [ To | =] property_value
```

Um den Wert einer Einstellung zurückzugeben, verwenden Sie `SHOW [setting name]`.

## PostgreSQL-Befehle

### BEGIN

Dieser Befehl wird geparst, und der abgeschlossene Befehl wird an den Client zurückgesendet. Dies entspricht dem `START TRANSACTION`-Befehl.

```sql
BEGIN [ TRANSACTION ]
```

#### Parameter

- `TRANSACTION`: Optionale Schlüsselwörter. Listet sie auf, es werden keine Maßnahmen ergriffen.

### CLOSE

`CLOSE` gibt die Ressourcen frei, die mit einem geöffneten Cursor verknüpft sind. Nach dem Schließen des Cursors sind keine weiteren Vorgänge zulässig. Ein Cursor sollte geschlossen werden, wenn er nicht mehr benötigt wird.

```sql
CLOSE { name }
```

#### Parameter

- `name`: der Name eines geöffneten Cursors, der geschlossen werden soll.

### COMMIT

In [!DNL Query Service] wird keine Aktion als Antwort auf die commit-Anweisung ausgeführt.

```sql
COMMIT [ WORK | TRANSACTION ]
```

#### Parameter

- `WORK`
- `TRANSACTION`: Optionale Schlüsselwörter. Diese haben keine Auswirkungen.

### DEALLOCATE

Verwenden Sie `DEALLOCATE`, um die Zuordnung einer zuvor vorbereiteten SQL-Anweisung aufzuheben. Wenn Sie die Zuordnung einer vorbereiteten Anweisung nicht explizit aufheben, wird dies am Ende der Sitzung ausgeführt.

```sql
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### Parameter

- `Prepare`: Dieses Keyword wird ignoriert.
- `name`: Der Name der vorbereiteten Anweisung, deren Zuordnung aufgehoben werden soll.
- `ALL`: Die Zuordnung aller vorbereiteten Anweisungen wird aufgehoben.

### DECLARE

Mit `DECLARE` kann ein Benutzer Cursor erstellen, mit denen eine kleine Anzahl von Zeilen gleichzeitig aus einer größeren Abfrage abgerufen werden kann. Nachdem der Cursor erstellt wurde, werden Zeilen mit `FETCH` abgerufen.

```sql
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### Parameter

- `name`: Der Name des zu erstellenden Cursors.
- `WITH HOLD`: Gibt an, dass der Cursor weiterhin verwendet werden kann, nachdem die Transaktion, die ihn erstellt hatte, erfolgreich abgeschlossen wurde.
- `query`: Ein `SELECT`- oder `VALUES`-Befehl, der die vom Cursor zurückzugebenden Zeilen angibt.

### EXECUTE

`EXECUTE` wird verwendet, um eine zuvor vorbereitete Anweisung auszuführen. Da vorbereitete Anweisungen nur für die Dauer einer Sitzung vorhanden sind, muss die vorbereitete Anweisung durch eine `PREPARE`-Anweisung erstellt worden sein, die zuvor in der aktuellen Sitzung ausgeführt wurde.

Wenn in der `PREPARE`-Anweisung, mit der die Anweisung erstellt wurde, einige Parameter angegeben wurden, muss ein kompatibler Satz von Parametern an die `EXECUTE`-Anweisung übergeben werden. Andernfalls wird ein Fehler ausgegeben. Beachten Sie, dass vorbereitete Anweisungen (im Gegensatz zu Funktionen) nicht aufgrund des Typs oder der Anzahl ihrer Parameter überladen werden. Der Name einer vorbereiteten Anweisung muss innerhalb einer Datenbanksitzung eindeutig sein.

```sql
EXECUTE name [ ( parameter [, ...] ) ]
```

#### Parameter

- `name`: Der Name der vorbereiteten Anweisung, die ausgeführt werden soll.
- `parameter`: Der tatsächliche Wert eines Parameters für die vorbereitete Anweisung. Hierbei muss es sich um einen Ausdruck handeln, der einen Wert liefert, der mit dem Datentyp dieses Parameters kompatibel ist, der bei der Erstellung der vorbereiteten Anweisung festgelegt wurde.

### EXPLAIN

Dieser Befehl zeigt den Ausführungsplan an, den der PostgreSQL-Planer für die angegebene Anweisung generiert. Der Ausführungsplan zeigt, wie die in der Anweisung referenzierten Tabellen gescannt werden – durch einfaches sequenzielles Scannen, Index-Scannen usw. – und, wenn mehrere Tabellen referenziert werden, welche Join-Algorithmen werden verwendet, um die erforderlichen Zeilen aus jeder Eingabetabelle zusammenzuführen.

Der wichtigste Teil der Anzeige sind die geschätzten Anweisungsausführungskosten. Das ist die Schätzung des Planers, wie lange die Ausführung der Anweisung dauern wird (gemessen in Kosteneinheiten, die frei wählbar sind, aber üblicherweise Abrufe der Festplattenseite bedeuten). Es werden zwei Zahlen angezeigt: die Startkosten, bevor die erste Zeile zurückgegeben werden kann, und die Gesamtkosten für die Rückgabe aller Zeilen. Bei den meisten Abfragen kommt es auf die Gesamtkosten an. In Kontexten wie einer Unterabfrage in EXISTS wählt der Planer jedoch die geringsten Startkosten anstelle der geringsten Gesamtkosten aus (da die Ausführung ohnehin nach einer Zeile anhält). Wenn Sie die Anzahl der Zeilen begrenzen, die mit einer `LIMIT`-Klausel zurückgegeben werden sollen, führt der Planer eine geeignete Interpolation zwischen den Endpunktkosten durch, um abzuschätzen, welcher Plan wirklich der günstigste ist.

Die `ANALYZE`-Option bewirkt, dass die Anweisung ausgeführt und nicht nur geplant wird. Anschließend werden der Anzeige die tatsächlichen Laufzeitstatistiken hinzugefügt, einschließlich der insgesamt verstrichenen Zeit, die innerhalb der einzelnen Planknoten verbracht wurde (in Millisekunden), und der Gesamtzahl der zurückgegebenen Zeilen. Damit können Sie sehen, wie genau die Schätzungen des Planers mit der Realität übereinstimmen.

```sql
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### Parameter

- `ANALYZE`: Führen Sie den Befehl aus und zeigen Sie die tatsächlichen Laufzeiten und andere Statistiken an. Dieser Parameter ist standardmäßig auf `FALSE` voreingestellt.
- `FORMAT`: Geben Sie das Ausgabeformat an, das TEXT, XML, JSON oder YAML sein kann. Die Ausgabe ohne Text enthält dieselben Informationen wie das Textausgabeformat, ist jedoch für Programme einfacher zu analysieren. Dieser Parameter ist standardmäßig auf `TEXT` voreingestellt.
- `statement`: Jede `SELECT`-, `INSERT`-, `UPDATE`-, `DELETE`-, `VALUES`-, `EXECUTE`-, `DECLARE`-, `CREATE TABLE AS`- oder `CREATE MATERIALIZED VIEW AS`-Anweisung, deren Ausführungsplan Sie sehen möchten.

>[!IMPORTANT]
>
> Denken Sie daran, dass die Anweisung genau genommen ausgeführt wird, wenn die `ANALYZE`-Option verwendet wird. Obwohl `EXPLAIN` alle Ausgaben verwirft, die `SELECT` zurückgibt, verworfen werden, treten andere Nebenwirkungen der Anweisung wie gewohnt auf.

#### Beispiel

So zeigen Sie den Plan für eine einfache Abfrage in einer Tabelle mit einer einzelnen `integer`-Spalte und 10000 Zeilen an:

```sql
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

`FETCH` ruft Zeilen mit einem zuvor erstellten Cursor ab.

Ein Cursor hat eine verknüpfte Position, die von `FETCH` verwendet wird. Der Cursor kann sich vor der ersten Zeile des Abfrageergebnisses, in einer beliebigen Zeile des Ergebnisses oder nach der letzten Zeile des Ergebnisses befinden. Nach der Erstellung wird ein Cursor vor der ersten Zeile positioniert. Nach dem Abrufen einiger Zeilen wird der Cursor auf der zuletzt abgerufenen Zeile positioniert. Wenn `FETCH` am Ende der verfügbaren Zeilen ausgeführt wird, bleibt der Cursor nach der letzten Zeile positioniert. Wenn keine solche Zeile vorhanden ist, wird ein leeres Ergebnis zurückgegeben und der Cursor wird je nachdem vor der ersten Zeile bzw. nach der letzten Zeile positioniert.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### Parameter

- `num_of_rows`: Eine möglicherweise vorzeichenbehaftete Ganzzahlkonstante, die die Position oder die Anzahl der abzurufenden Zeilen bestimmt.
- `cursor_name`: Name eines geöffneten Cursors.

### PREPARE

`PREPARE` erstellt eine vorbereitete Anweisung. Eine vorbereitete Anweisung ist ein Server-seitiges Objekt, das zur Leistungsoptimierung verwendet werden kann. Wenn die `PREPARE`-Anweisung ausgeführt wird, wird die angegebene Anweisung geparst, analysiert und umgeschrieben. Wenn anschließend ein `EXECUTE`-Befehl ausgegeben wird, wird die vorbereitete Erklärung geplant und ausgeführt. Diese Arbeitsteilung vermeidet sich wiederholende Parse-Analysen, während der Ausführungsplan von den angegebenen spezifischen Parameterwerten abhängt.

Vorbereitete Anweisungen können Parameter beinhalten, d. h. Werte, die bei der Ausführung der Anweisung ersetzt werden. Beziehen Sie sich beim Erstellen der vorbereiteten Anweisung auf Parameter nach Position. Verwenden Sie dazu $1, $2 usw. Eine entsprechende Liste von Parameterdatentypen kann optional angegeben werden. Wenn der Datentyp eines Parameters nicht angegeben ist oder als unbekannt deklariert wird, wird der Typ ggf. aus dem Kontext abgeleitet, in dem der Parameter zuerst referenziert wird. Geben Sie beim Ausführen der Anweisung die tatsächlichen Werte für diese Parameter in der `EXECUTE`-Anweisung an.

Vorbereitete Anweisungen gelten nur für die Dauer der aktuellen Datenbanksitzung. Wenn die Sitzung endet, wird die vorbereitete Anweisung vergessen, sodass sie neu erstellt werden muss, bevor sie erneut verwendet wird. Dies bedeutet auch, dass eine einzelne vorbereitete Anweisung nicht von mehreren gleichzeitigen Datenbank-Clients verwendet werden kann. Jeder Client kann jedoch eine eigene vorbereitete Anweisung erstellen, die verwendet werden soll. Vorbereitete Anweisungen können mithilfe des `DEALLOCATE`-Befehls manuell bereinigt werden.

Vorbereitete Anweisungen haben potenziell den größten Leistungsvorteil, wenn eine einzelne Sitzung zur Ausführung einer großen Anzahl ähnlicher Anweisungen verwendet wird. Der Leistungsunterschied ist besonders dann von Bedeutung, wenn die Anweisungen komplex zu planen oder umzuschreiben sind, wenn die Abfrage beispielsweise mehrere Tabellen umfasst oder mehrere Regeln erfordert. Wenn die Anweisung relativ einfach zu planen und umzuschreiben, aber relativ teuer in der Ausführung ist, ist der Leistungsvorteil von vorbereiteten Anweisungen weniger bemerkbar.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### Parameter

- `name`: Ein beliebiger Name, der dieser vorbereiteten Aussage gegeben wird. Er muss innerhalb einer einzelnen Sitzung eindeutig sein und wird anschließend zum Ausführen oder Deklarieren einer zuvor vorbereiteten Anweisung verwendet.
- `data-type`: Der Datentyp eines Parameters für die vorbereitete Anweisung. Wenn der Datentyp eines bestimmten Parameters nicht angegeben oder als unbekannt angegeben wird, wird er aus dem Kontext abgeleitet, in dem der Parameter zum ersten Mal referenziert wird. Verwenden Sie $ 1, $ 2 usw., um auf die Parameter in der vorbereiteten Anweisung zu verweisen.


### ROLLBACK

`ROLLBACK` setzt die aktuelle Transaktion zurück und bewirkt, dass alle durch die Transaktion vorgenommenen Aktualisierungen verworfen werden.

```sql
ROLLBACK [ WORK ]
```

#### Parameter

- `WORK`

### SELECT INTO

`SELECT INTO` erstellt eine neue Tabelle und füllt sie mit Daten, die von einer Abfrage berechnet wurden. Die Daten werden nicht wie bei einem normalen `SELECT` an den Client zurückgegeben. Die Spalten der neuen Tabelle haben die Namen und Datentypen, die den Ausgabespalten von `SELECT` zugeordnet sind.

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

#### Parameter

- `TEMPORARAY` oder `TEMP`: Wenn angegeben, wird die Tabelle als temporäre Tabelle erstellt.
- `UNLOGGED:`: Wenn angegeben, wird die Tabelle als nicht protokollierte Tabelle erstellt.
- `new_table` Der Name der zu erstellenden Tabelle (optional mit Schema versehen).

#### Beispiel

Erstellen Sie eine neue Tabelle `films_recent`, die nur aus den aktuellen Einträgen der Tabelle `films` besteht:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

`SHOW` zeigt die aktuelle Einstellung der Laufzeitparameter an. Diese Variablen können mithilfe der `SET`-Anweisung, durch Bearbeiten der Konfigurationsdatei postgresql.conf, durch die `PGOPTIONS`-Umgebungsvariable (bei Verwendung von libpq oder einer libpq-basierten Anwendung) oder durch Befehlszeilenflags beim Starten des Postgres-Servers eingestellt werden.

```sql
SHOW name
```

#### Parameter

- `name`:
   - `SERVER_VERSION`: Zeigt die Versionsnummer des Servers an.
   - `SERVER_ENCODING`: Zeigt die Server-seitige Zeichensatzkodierung an. Derzeit kann dieser Parameter angezeigt, aber nicht eingestellt werden, da die Kodierung zum Zeitpunkt der Datenbankerstellung festgelegt wird.
   - `LC_COLLATE`: Zeigt die Gebietsschemaeinstellung der Datenbank für die Sortierung (Textanordnung) an. Derzeit kann dieser Parameter angezeigt, aber nicht eingestellt werden, da die Einstellung zum Zeitpunkt der Datenbankerstellung festgelegt wird.
   - `LC_CTYPE`: Zeigt die Gebietsschemaeinstellung der Datenbank für die Zeichenklassifizierung an. Derzeit kann dieser Parameter angezeigt, aber nicht eingestellt werden, da die Einstellung zum Zeitpunkt der Datenbankerstellung festgelegt wird.
      `IS_SUPERUSER`: Wahr (True), wenn die aktuelle Rolle über Superuser-Berechtigungen verfügt.
- `ALL`: Zeigt die Werte aller Konfigurationsparameter mit Beschreibungen an.

#### Beispiel

Anzeigen der aktuellen Einstellung des Parameters `DateStyle`

```sql
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### START TRANSACTION

Dieser Befehl wird geparst und sendet den abgeschlossenen Befehl zurück an den Client. Dies entspricht dem `BEGIN`-Befehl.

```sql
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```

### KOPIE

Mit diesem Befehl wird die Ausgabe einer beliebigen SELECT-Abfrage an einen angegebenen Speicherort ausgegeben. Der Benutzer muss Zugriff auf diesen Speicherort haben, damit dieser Befehl erfolgreich ausgeführt werden kann.

```sql
COPY  query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']

where 'format_name' is be one of:
    'parquet', 'csv', 'json'

'parquet' is the default format.
```

>[!NOTE]
>
>Der vollständige Ausgabepfad lautet `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`


### ALTER

Mit diesem Befehl können Sie Primär- oder Fremdschlüsseleinschränkungen zur Tabelle hinzufügen oder ablegen.

```sql
Alter TABLE table_name ADD CONSTRAINT Primary key ( column_name )

Alter TABLE table_name ADD CONSTRAINT Foreign key ( column_name ) references referenced_table_name ( primary_column_name )

Alter TABLE table_name ADD CONSTRAINT Foreign key ( column_name ) references referenced_table_name Namespace 'namespace'

Alter TABLE table_name DROP CONSTRAINT Primary key ( column_name )

Alter TABLE table_name DROP CONSTRAINT  Foreign key ( column_name )
```

>[!NOTE]
>Das Schema &quot;Tabelle&quot;sollte eindeutig sein und nicht für mehrere Tabellen freigegeben sein. Darüber hinaus ist der Namensraum obligatorisch.


### PRIMÄR-TASTEN ANZEIGEN

Dieser Befehl Liste alle primären Schlüsseleinschränkungen für die jeweilige Datenbank.

```sql
SHOW PRIMARY KEYS
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```


### AUSLÄNDISCHE TASTEN ANZEIGEN

Dieser Befehl Liste alle Fremdschlüsseleinschränkungen für die jeweilige Datenbank.

```sql
SHOW FOREIGN KEYS
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
