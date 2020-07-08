---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: SQL-Syntax
topic: syntax
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 1%

---


# SQL-Syntax

Abfrage Service bietet die Möglichkeit, ANSI SQL für `SELECT` Anweisungen und andere eingeschränkte Befehle zu verwenden. Dieses Dokument zeigt die SQL-Syntax, die vom Abfrage Service unterstützt wird.

## Definieren einer SELECT-Abfrage

Die folgende Syntax definiert eine vom Abfrage Service unterstützte `SELECT` Abfrage:

```
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

wobei `from_item` eines der folgenden sein kann:

```
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

und `grouping_element` kann eine der folgenden sein:

```
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

und `with_query` ist:

```
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### WO ILIKE-Klausel

Das Schlüsselwort &quot;ILIKE&quot;kann anstelle von &quot;LIKE&quot;verwendet werden, um Übereinstimmungen mit der WHE-Klausel der SELECT-Abfrage vorzunehmen, wobei die Groß-/Kleinschreibung nicht berücksichtigt wird.

```
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

Die Logik der LIKE- und ILIKE-Klauseln lautet wie folgt:
- ```WHERE condition LIKE pattern```entspricht ```~~``` dem Muster
- ```WHERE condition NOT LIKE pattern```entspricht ```!~~``` dem Muster
- ```WHERE condition ILIKE pattern```entspricht ```~~*``` dem Muster
- ```WHERE condition NOT ILIKE pattern```entspricht ```!~~*``` dem Muster


#### Beispiel

```
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

Gibt Kunden zurück, deren Namen mit &quot;A&quot;oder &quot;a&quot;beginnen.

## JOINS

Eine `SELECT` Abfrage mit Joins hat die folgende Syntax:

```
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## VEREINIGUNG, INTERSECT und EXCEPT

Die `UNION`-, `INTERSECT`- und `EXCEPT` -Klauseln werden unterstützt, um gleichartige Zeilen aus zwei oder mehr Tabellen zu kombinieren oder auszuschließen:

```
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## TABELLE ALS AUSWAHL ERSTELLEN

Die folgende Syntax definiert eine `CREATE TABLE AS SELECT` (CTAS-)Abfrage, die vom Abfrage Service unterstützt wird:

```
CREATE TABLE table_name [ WITH (schema='target_schema_title') ] AS (select_query)
```

wobei `target_schema_title` der Titel des XDM-Schemas ist. Verwenden Sie diese Klausel nur, wenn Sie ein vorhandenes XDM-Schema für den neuen Datensatz verwenden möchten, der von der CTAS-Abfrage erstellt wurde.

und `select_query` ist eine `SELECT` Anweisung, deren Syntax oben in diesem Dokument definiert ist.


### Beispiel

```
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

Bitte beachten Sie, dass für eine bestimmte CTAS-Abfrage

1. Die `SELECT` Anweisung muss einen Alias für die Aggregat-Funktionen wie `COUNT`, `SUM`, `MIN`usw. enthalten.
2. Die `SELECT` Anweisung kann mit oder ohne Klammern () angegeben werden.

## IN

Die folgende Syntax definiert eine vom Abfrage Service unterstützte `INSERT INTO` Abfrage:

```
INSERT INTO table_name select_query
```

wobei `select_query` es sich um eine `SELECT` Anweisung handelt, deren Syntax oben in diesem Dokument definiert ist.

### Beispiel

```
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

Bitte beachten Sie, dass für eine bestimmte INSERT-INTO-Abfrage

1. Die `SELECT` Anweisung DARF NICHT in Klammern () gesetzt werden.
2. Das Schema des Ergebnisses der `SELECT` Anweisung muss mit dem in der `INSERT INTO` Anweisung definierten Wert übereinstimmen.

### DROP-TABELLE

Legen Sie eine Tabelle ab und löschen Sie den mit der Tabelle verknüpften Ordner aus dem Dateisystem, wenn es sich nicht um eine EXTERNE Tabelle handelt. Wenn die abzugebende Tabelle nicht vorhanden ist, tritt eine Ausnahme auf.

```
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### Parameter

- `IF EXISTS`: Wenn die Tabelle nicht vorhanden ist, passiert nichts
- `TEMP`: Temporäre Tabelle

## ANSICHT ERSTELLEN

Die folgende Syntax definiert eine vom Abfrage Service unterstützte `CREATE VIEW` Abfrage:

```
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

Wo `view_name` ist der Name der zu erstellenden Ansicht und `select_query` ist eine `SELECT` Anweisung, deren Syntax oben in diesem Dokument definiert ist.

Beispiel:

```
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### DROP-ANSICHT

Die folgende Syntax definiert eine vom Abfrage Service unterstützte `DROP VIEW` Abfrage:

```
DROP VIEW [IF EXISTS] view_name
```

Wo `view_name` ist die Ansicht zu streichen

Beispiel:

```
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Spark SQL-Befehle

### SET

Legen Sie eine Eigenschaft fest, geben Sie den Wert einer vorhandenen Eigenschaft zurück oder alle vorhandenen Eigenschaften werden Liste. Wenn für einen vorhandenen Eigenschaftenschlüssel ein Wert angegeben wird, wird der alte Wert überschrieben.

```
SET property_key [ To | =] property_value
```

Um den Wert für eine Einstellung zurückzugeben, verwenden Sie `SHOW [setting name]`.

## PostgreSQL-Befehle

### BEGINN

Dieser Befehl wird analysiert und der Befehl &quot;Fertig gestellt&quot;wird zurück an den Client gesendet. Das ist dasselbe wie der `START TRANSACTION` Befehl.

```
BEGIN [ TRANSACTION ]
```

#### Parameter

- `TRANSACTION`: Optionale Schlüsselwörter. Listet sie auf, es werden keine Maßnahmen ergriffen.

### SCHLIESSEN

`CLOSE` Gibt die Ressourcen frei, die mit einem geöffneten Cursor verknüpft sind. Nach dem Schließen des Cursors sind keine weiteren Vorgänge zulässig. Ein Cursor sollte geschlossen werden, wenn er nicht mehr benötigt wird.

```
CLOSE { name }
```

#### Parameter

- `name`: der Name eines geöffneten Cursors, der geschlossen werden soll.

### VERPFLICHTEN

In Abfrage Service wird keine Reaktion auf den Commit-Transaktionsanweisung ausgeführt.

```
COMMIT [ WORK | TRANSACTION ]
```

#### Parameter

- `WORK`
- `TRANSACTION`: Optionale Schlüsselwörter. Sie haben keine Wirkung.

### DEALLOCATE

Verwenden Sie diese Option `DEALLOCATE` zum Deklarieren einer zuvor erstellten SQL-Anweisung. Wenn Sie eine vorbereitete Anweisung nicht explizit dezuweisen, wird sie beim Ende der Sitzung dezuordnen.

```
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### Parameter

- `Prepare`: Dieser Suchbegriff wird ignoriert.
- `name`: Der Name der vorbereiteten Anweisung, die dezuordnen soll.
- `ALL`: Alle vorbereiteten Anweisungen dezuordnen.

### DECLARE

`DECLARE` ermöglicht es dem Benutzer, Cursorfunktionen zu erstellen, die verwendet werden können, um eine kleine Anzahl von Zeilen zu einem Zeitpunkt aus einer größeren Abfrage abzurufen. Nachdem der Cursor erstellt wurde, werden Zeilen mit `FETCH`diesem abgerufen.

```
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### Parameter

- `name`: Der Name des zu erstellenden Cursors.
- `WITH HOLD`: Gibt an, dass der Cursor nach der Transaktion, die ihn erfolgreich erstellt hat, weiterhin verwendet werden kann.
- `query`: Ein `SELECT` oder `VALUES` -Befehl, der die vom Cursor zurückzugebenden Zeilen angibt.

### EXECUTE

`EXECUTE` wird verwendet, um eine zuvor vorbereitete Anweisung auszuführen. Da vorbereitete Anweisungen nur für die Dauer einer Sitzung vorhanden sind, muss die vorbereitete Anweisung durch eine `PREPARE` Anweisung erstellt worden sein, die zuvor in der aktuellen Sitzung ausgeführt wurde.

Wenn in der `PREPARE` Anweisung, mit der die Anweisung erstellt wurde, einige Parameter angegeben wurden, muss ein kompatibler Satz von Parametern an die `EXECUTE` Anweisung übergeben werden, andernfalls wird ein Fehler ausgegeben. Beachten Sie, dass vorbereitete Anweisungen (im Gegensatz zu Funktionen) nicht aufgrund des Typs oder der Anzahl ihrer Parameter überladen werden. Der Name einer vorbereiteten Anweisung muss innerhalb einer Datenbanksitzung eindeutig sein.

```
EXECUTE name [ ( parameter [, ...] ) ]
```

#### Parameter

- `name`: Der Name der vorbereiteten Anweisung, die ausgeführt werden soll.
- `parameter`: Der tatsächliche Wert eines Parameters für die vorbereitete Anweisung. Hierbei muss es sich um einen Ausdruck handeln, der einen Wert liefert, der mit dem Datentyp dieses Parameters kompatibel ist, wie bei der Erstellung der vorbereiteten Anweisung angegeben.

### ERKLÄRUNG

Dieser Befehl zeigt den Ausführungsplan an, den der PostgreSQL-Planer für die angegebene Anweisung generiert. Der Ausführungsplan zeigt, wie die in der Anweisung referenzierten Tabellen gescannt werden — durch einfaches sequenzielles Scannen, Index-Scan usw. — und wenn mehrere Tabellen referenziert werden, welche Verbindungsalgorithmen werden verwendet, um die erforderlichen Zeilen aus jeder Eingabetabelle zusammenzuführen.

Der kritischste Teil der Anzeige sind die geschätzten Anweisungsausführungskosten, was die Schätzung des Planers darüber ist, wie lange es dauert, bis die Anweisung ausgeführt wird (gemessen in Kosteneinheiten, die willkürlich sind, aber üblicherweise bedeuten, dass die Seite abgerufen wird). Es werden zwei Zahlen angezeigt: die Kosten für den Beginn vor der ersten Zeile und die Gesamtkosten für die Rückgabe aller Zeilen. Für die meisten Abfragen sind die Gesamtkosten wichtig, aber in Kontexten wie einer Unterabfrage in EXISTS wählt der Planer die kleinsten Kosten für den Beginn anstelle der kleinsten Gesamtkosten (da der Prüfer ohnehin nach einer Zeile aufhört). Wenn Sie außerdem die Anzahl der Zeilen begrenzen, die mit einer `LIMIT` Klausel zurückgegeben werden sollen, erfolgt eine geeignete Interpolation zwischen den Endpunktkosten, um abzuschätzen, welcher Plan wirklich am billigsten ist.

Die `ANALYZE` Option bewirkt, dass die Anweisung ausgeführt wird, nicht nur geplant. Anschließend werden der Anzeige die tatsächlichen Laufzeitstatistiken hinzugefügt, einschließlich der gesamten verstrichenen Zeit, die innerhalb der einzelnen Planknoten verbracht wurde (in Millisekunden) und der Gesamtzahl der zurückgegebenen Zeilen. Dies ist nützlich, um zu sehen, ob die Schätzungen des Planers der Realität nahe kommen.

```
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### Parameter

- `ANALYZE`: Führen Sie den Befehl aus und zeigen Sie die tatsächlichen Laufzeiten und andere Statistiken an. Dieser Parameter ist standardmäßig auf `FALSE`.
- `FORMAT`: Geben Sie das Ausgabeformat an, das TEXT, XML, JSON oder YAML sein kann. Die Ausgabe ohne Text enthält dieselben Informationen wie das Textausgabeformat, ist jedoch für Programme einfacher zu analysieren. Dieser Parameter ist standardmäßig auf `TEXT`.
- `statement`: Jede `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`oder `CREATE MATERIALIZED VIEW AS` Anweisung, deren Ausführungsplan Sie sehen möchten.

>[!IMPORTANT]
>
>Denken Sie daran, dass die Anweisung tatsächlich ausgeführt wird, wenn die `ANALYZE` Option verwendet wird. Obwohl `EXPLAIN` alle Ausgaben, die eine `SELECT` Rückgabe, verworfen werden, geschehen andere Nebenwirkungen der Anweisung wie gewohnt.

#### Beispiel

So zeigen Sie den Plan für eine einfache Abfrage auf einer Tabelle mit einer einzelnen `integer` Spalte und 10000 Zeilen an:

```
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

`FETCH` ruft Zeilen mit einem zuvor erstellten Cursor ab.

Ein Cursor hat eine verknüpfte Position, die von `FETCH`verwendet wird. Die Cursorposition kann vor der ersten Zeile des Ergebnisses, in einer beliebigen Zeile des Ergebnisses oder nach der letzten Zeile des Ergebnisses liegen. Nach der Erstellung wird ein Cursor vor der ersten Zeile positioniert. Nach dem Abrufen einiger Zeilen wird der Cursor auf der Zeile positioniert, die zuletzt abgerufen wurde. Wenn der Cursor am Ende der verfügbaren Zeilen `FETCH` ausgeführt wird, wird er nach der letzten Zeile positioniert. Wenn keine solche Zeile vorhanden ist, wird ein leeres Ergebnis zurückgegeben und die Cursor werden vor der ersten Zeile bzw. nach der letzten Zeile positioniert.

```
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### Parameter

- `num_of_rows`: Eine eventuell vorzeichenbehaftete ganzzahlige Konstante, die den Speicherort oder die Anzahl der abzurufenden Zeilen bestimmt.
- `cursor_name`: Name des geöffneten Cursors.

### VORBEREITUNG

`PREPARE` erstellt eine vorbereitete Anweisung. Eine vorbereitete Anweisung ist ein serverseitiges Objekt, das zur Leistungsoptimierung verwendet werden kann. Wenn die `PREPARE` Anweisung ausgeführt wird, wird die angegebene Anweisung analysiert, analysiert und umgeschrieben. Wenn anschließend ein `EXECUTE` Befehl ausgegeben wird, wird die vorbereitete Erklärung geplant und ausgeführt. Diese Arbeitsteilung vermeidet sich wiederholende Parse-Analysen, während der Ausführungsplan von den spezifischen Parameterwerten abhängt.

Zubereitete Anweisungen können Parameter annehmen, Werte, die bei der Ausführung der Anweisung ersetzt werden. Beim Erstellen der vorbereiteten Anweisung beziehen Sie sich auf Parameter nach Position, unter Verwendung von $1, $2 usw. Eine entsprechende Liste von Parameterdatentypen kann optional angegeben werden. Wenn der Datentyp eines Parameters nicht angegeben ist oder als unbekannt deklariert wird, wird der Typ aus dem Kontext abgeleitet, in dem der Parameter zuerst referenziert wird, wenn möglich. Geben Sie beim Ausführen der Anweisung die tatsächlichen Werte für diese Parameter in der `EXECUTE` Anweisung an.

Zubereitete Anweisungen dauern nur für die Dauer der aktuellen Datenbanksitzung. Wenn die Sitzung beendet wird, wird die vorbereitete Anweisung vergessen. Daher muss sie neu erstellt werden, bevor sie erneut verwendet wird. Dies bedeutet auch, dass eine einzelne vorbereitete Anweisung nicht von mehreren gleichzeitigen Datenbankclients verwendet werden kann. Jeder Kunde kann jedoch eine eigene vorbereitete Anweisung erstellen, die verwendet werden soll. Zubereitete Anweisungen können manuell mithilfe des `DEALLOCATE` Befehls bereinigt werden.

Zubereitete Anweisungen haben möglicherweise den größten Leistungsvorteil, wenn eine einzelne Sitzung verwendet wird, um eine große Anzahl ähnlicher Anweisungen auszuführen. Der Leistungsunterschied ist besonders dann von Bedeutung, wenn die Anweisungen komplex zu planen oder umzuschreiben sind, wenn die Abfrage beispielsweise mehrere Tabellen umfasst oder mehrere Regeln erfordert. Wenn die Anweisung relativ einfach zu planen und umzuschreiben, aber relativ teuer auszuführen ist, ist der Leistungsvorteil von vorbereiteten Anweisungen weniger bemerkbar.

```
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### Parameter

- `name`: Ein willkürlicher Name, der dieser vorbereiteten Aussage gegeben wird. Es muss innerhalb einer einzelnen Sitzung eindeutig sein und wird anschließend zum Ausführen oder Deklarieren einer zuvor vorbereiteten Anweisung verwendet.
- `data-type`: Der Datentyp eines Parameters für die vorbereitete Anweisung. Wenn der Datentyp eines bestimmten Parameters nicht angegeben ist oder als unbekannt angegeben wird, wird er aus dem Kontext abgeleitet, in dem der Parameter zum ersten Mal referenziert wird. Um auf die Parameter in der vorbereiteten Anweisung zu verweisen, verwenden Sie $1, $2 usw.


### ROLLBACK

`ROLLBACK` die aktuelle Transaktion zurücknimmt und alle durch die Transaktion vorgenommenen Aktualisierungen verworfen werden.

```
ROLLBACK [ WORK ]
```

#### Parameter

- `WORK`

### AUSWÄHLEN IN

`SELECT INTO` erstellt eine neue Tabelle und füllt sie mit Daten, die von einer Abfrage berechnet werden. Die Daten werden nicht an den Client zurückgegeben, wie bei einem normalen `SELECT`. Die Spalten der neuen Tabelle haben die Namen und Datentypen, die mit den Ausgabespalten der `SELECT`Tabelle verknüpft sind.

```
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

- `TEMPORARAY` oder `TEMP`: Wenn dies angegeben ist, wird die Tabelle als temporäre Tabelle erstellt.
- `UNLOGGED:` Wenn angegeben, wird die Tabelle als nicht protokollierte Tabelle erstellt.
- `new_table` Der Name der zu erstellenden Tabelle (optional mit Schema versehen).

#### Beispiel

Erstellen Sie eine neue Tabelle, `films_recent` die nur aus aktuellen Einträgen aus der Tabelle besteht `films`:

```
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### ANZEIGEN

`SHOW` zeigt die aktuelle Einstellung der Laufzeitparameter an. Diese Variablen können mithilfe der `SET` Anweisung, durch Bearbeiten der Konfigurationsdatei &quot;postgresql.conf&quot;, durch die `PGOPTIONS` Umgebungsvariable (bei Verwendung von libpq oder einer libpq-basierten Anwendung) oder durch Befehlszeilenflags beim Starten des Postgres-Servers eingestellt werden.

```
SHOW name
```

#### Parameter

- `name`:
   - `SERVER_VERSION`: Zeigt die Versionsnummer des Servers an.
   - `SERVER_ENCODING`: Zeigt die serverseitige Zeichensatzkodierung an. Derzeit kann dieser Parameter angezeigt, aber nicht eingestellt werden, da die Kodierung zum Zeitpunkt der Datenbankerstellung bestimmt wird.
   - `LC_COLLATE`: Zeigt die Spracheinstellung der Datenbank für die Sortierreihenfolge (Textreihenfolge) an. Derzeit kann dieser Parameter angezeigt, aber nicht eingestellt werden, da die Einstellung zum Zeitpunkt der Datenbankerstellung festgelegt wird.
   - `LC_CTYPE`: Zeigt die Spracheinstellung der Datenbank für die Zeichenklassifizierung an. Derzeit kann dieser Parameter angezeigt, aber nicht eingestellt werden, da die Einstellung zum Zeitpunkt der Datenbankerstellung festgelegt wird.
      `IS_SUPERUSER`: True, wenn die aktuelle Rolle über Superuser-Berechtigungen verfügt.
- `ALL`: Zeigen Sie die Werte aller Konfigurationsparameter mit Beschreibungen an.

#### Beispiel

Aktuelle Einstellung des Parameters anzeigen `DateStyle`

```
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### BEGINN-TRANSAKTION

Dieser Befehl wird analysiert und sendet den abgeschlossenen Befehl zurück an den Client. Das ist dasselbe wie der `BEGIN` Befehl.

```
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```
