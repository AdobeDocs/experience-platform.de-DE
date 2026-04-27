---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;SQL-Syntax;sql;ctas;CTAS;Tabelle als Auswahl erstellen
solution: Experience Platform
title: SQL-Syntax in Query Service
description: In diesem Dokument wird die vom Abfrage-Service von Adobe Experience Platform unterstützte SQL-Syntax beschrieben.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: f2d81f05c8c19c6f28849fc4dbe9bfa26be64645
workflow-type: tm+mt
source-wordcount: '4737'
ht-degree: 5%

---

# SQL-Syntax in Query Service

Sie können standardmäßige ANSI-SQL für `SELECT` und andere eingeschränkte Befehle im Abfrage-Service von Adobe Experience Platform verwenden. Dieses Dokument behandelt die von [!DNL Query Service] unterstützte SQL-Syntax.

## SELECT queries {#select-queries}

Die folgende Syntax definiert eine `SELECT` Abfrage, die von [!DNL Query Service] unterstützt wird:

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

Im folgenden Abschnitt finden Sie die verfügbaren Optionen für die Schlüsselwörter FROM, GROUP und WITH.

>[!BEGINTABS]

>[!TAB `from_item`]

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

>[!TAB `grouping_element`]

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

>[!TAB `with_query`]

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

>[!ENDTABS]

Die folgenden Unterabschnitte enthalten Details zu zusätzlichen Klauseln, die Sie in Ihren Abfragen verwenden können, sofern sie dem oben beschriebenen Format entsprechen.

### SNAPSHOT-Klausel

Diese Klausel kann verwendet werden, um Daten einer Tabelle basierend auf Momentaufnahme-IDs inkrementell zu lesen. Eine Momentaufnahme-ID ist eine Checkpoint-Markierung, die durch eine Zahl vom Typ „Long“ dargestellt wird. Diese Zahl wird jedes Mal auf eine Data-Lake-Tabelle angewendet, wenn Daten in die Tabelle geschrieben werden. Die `SNAPSHOT`-Klausel hängt sich an die Tabellenbeziehung an, neben der sie verwendet wird.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### Beispiel

```sql
SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT AS OF end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN 'HEAD' AND start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN end_snapshot_id AND 'TAIL';

SELECT * FROM (SELECT id FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id) C;

(SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id) a
  INNER JOIN 
(SELECT * from table_to_be_joined SNAPSHOT AS OF your_chosen_snapshot_id) b 
  ON a.id = b.id;
```

>[!NOTE]
>
>Wenn Sie `HEAD` oder `TAIL` in einer `SNAPSHOT` verwenden, müssen Sie sie in einfache Anführungszeichen setzen (z. B. &quot;HEAD&quot;, „TAIL„). Die Verwendung ohne Anführungszeichen führt zu einem Syntaxfehler.

In der folgenden Tabelle wird die Bedeutung der einzelnen Syntaxoptionen innerhalb der SNAPSHOT-Klausel erläutert.

| Syntax | Bedeutung |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| `SINCE start_snapshot_id` | Liest Daten ausgehend von der angegebenen Snapshot-ID (exklusiv). |
| `AS OF end_snapshot_id` | liest Daten so, wie sie zur angegebenen Momentaufnahme-ID erfasst wurden (einschließlich). |
| `BETWEEN start_snapshot_id AND end_snapshot_id` | Liest Daten zwischen den angegebenen Start- und End-Snapshot-IDs. Es ist exklusiv der `start_snapshot_id` und inklusive der `end_snapshot_id`. |
| `BETWEEN HEAD AND start_snapshot_id` | liest Daten vom Anfang (vor dem ersten Schnappschuss) bis zur angegebenen Start-Schnappschuss-ID (einschließlich). Beachten Sie, dass nur Zeilen in `start_snapshot_id` zurückgegeben werden. |
| `BETWEEN end_snapshot_id AND TAIL` | Liest Daten direkt nach dem angegebenen `end_snapshot_id` bis zum Ende des Datensatzes (ohne Snapshot-ID). This means that if `end_snapshot_id` is the last snapshot in the dataset, the query will return zero rows because there are no snapshots beyond that last snapshot. |
| `SINCE start_snapshot_id INNER JOIN table_to_be_joined AS OF your_chosen_snapshot_id ON table_to_be_queried.id = table_to_be_joined.id` | Reads data starting from the specified snapshot ID from `table_to_be_queried` and joins it with the data from `table_to_be_joined` as it was at `your_chosen_snapshot_id`. The join is based on matching IDs from the ID columns of the two tables being joined. |

A `SNAPSHOT` clause works with a table or table alias but not on top of a subquery or view. A `SNAPSHOT` clause works anywhere a `SELECT` query on a table can be applied.

Also, you can use `HEAD` and `TAIL` as special offset values for snapshot clauses. Using `HEAD` refers to an offset before the first snapshot, while `TAIL` refers to an offset after the last snapshot.

>[!NOTE]
>
>If you are querying between two snapshot IDs, the following two scenarios can occur if the start snapshot is expired and the optional fallback behavior flag (`resolve_fallback_snapshot_on_failure`) is set:
>
>- If the optional fallback behavior flag is set, Query Service chooses the earliest available snapshot, sets it as the start snapshot, and returns the data between the earliest available snapshot and the specified end snapshot. This data is **inclusive** of the earliest available snapshot.

### WHERE clause

By default, matches produced by a `WHERE` clause on a `SELECT` query are case-sensitive. If you want matches to be case-insensitive, you can use the keyword `ILIKE` instead of `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

The logic of the LIKE and ILIKE clauses are explained in the following table:

| Clause | Operator |
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

This query returns customers with names beginning in &quot;A&quot; or &quot;a&quot;.

### JOIN

A `SELECT` query that uses joins has the following syntax:

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION, INTERSECT und EXCEPT

The `UNION`, `INTERSECT`, and `EXCEPT` clauses are used to combine or exclude like rows from two or more tables:

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### CREATE TABLE AS SELECT {#create-table-as-select}

Use the `CREATE TABLE AS SELECT` (CTAS) command to materialize the results of a `SELECT` query into a new table. This is useful for creating transformed datasets, performing aggregations, or previewing feature-engineered data before using it in a model.

If you&#39;re ready to train a model using transformed features, see the [Models documentation](../advanced-statistics/models.md) for guidance on using `CREATE MODEL` with the `TRANSFORM` clause.

You can optionally include a `TRANSFORM` clause to apply one or more feature engineering functions directly within the CTAS statement. Use `TRANSFORM` to inspect the results of your transformation logic before model training.

This syntax applies to both permanent and temporary tables.

```sql
CREATE TABLE table_name 
  [WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE')] 
  [TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)]
AS (select_query)
```

```sql
CREATE TEMP TABLE table_name 
  [WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE')] 
  [TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)]
AS (select_query)
```

| Parameter | Beschreibung |
| ----- | ----- |
| `schema` | The title of the XDM schema. Use this clause only if you wish to associate the new table with an existing XDM schema. |
| `rowvalidation` | (Optional) Enables row-level validation for each batch ingested into the dataset. Default is true. |
| `label` | (Optional) Use the value `PROFILE` to label the dataset as enabled for Profile ingestion. |
| `transform` | (Optional) Applies feature engineering transformations (such as string indexing, one-hot encoding, or TF-IDF) before materializing  the dataset. This clause is used for previewing transformed features. See [`TRANSFORM` clause documentation](#transform) for more details. |
| `select_query` | A standard `SELECT` statement that defines the dataset. See the [`SELECT` queries section](#select-queries) for more details. |

>[!NOTE]
>
>The `SELECT` statement must include an alias for aggregate functions such as `COUNT`, `SUM`, or `MIN`. You can provide the `SELECT` query with or without parentheses. This applies whether or not the `TRANSFORM` clause is used.

**Beispiele**

A basic example using a `TRANSFORM`clause to preview a few engineered features:

```sql
CREATE TABLE ctas_transform_table_vp14 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review_e2e_DND;
```

A more advanced example with multiple transformation steps:

```sql
CREATE TABLE ctas_transform_table 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

A temporary table example:

```sql
CREATE TEMP TABLE ctas_transform_table 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

#### Limitations and behavior {#limitations-and-behavior}

Keep the following limitations in mind when using the `TRANSFORM` clause with `CREATE TABLE` or `CREATE TEMP TABLE`:

- If any transformation function generates a vector output, it is automatically converted to an array.
- As a result, tables created using `TRANSFORM` cannot be used directly in `CREATE MODEL` statements. You must redefine the transformation logic during model creation to generate the appropriate feature vectors.
- Transformations are only applied during table creation. New data inserted into the table with `INSERT INTO` is **not automatically transformed**. To apply transformations to new data, you must recreate the table using `CREATE TABLE AS SELECT` with the `TRANSFORM` clause.
- This method is intended for previewing and validating transformations at a point in time, not for building reusable transformation pipelines.

>[!NOTE]
>
>Weitere Informationen zu den verfügbaren Transformationsfunktionen und ihren Ausgabetypen finden Sie unter [Ausgabedatentypen für die Funktionstransformation](../advanced-statistics/feature-transformation.md#available-transformations).


### TRANSFORM-Klausel {#transform}

Verwenden Sie die `TRANSFORM`-Klausel, um vor dem Modell-Training oder der Tabellenerstellung eine oder mehrere Feature Engineering-Funktionen auf einen Datensatz anzuwenden. Mit dieser Klausel können Sie die genaue Form Ihrer Eingabefunktionen in der Vorschau anzeigen, überprüfen oder definieren.

Die `TRANSFORM`-Klausel kann in den folgenden Anweisungen verwendet werden:

- `CREATE MODEL`
- `CREATE TABLE`
- `CREATE TEMP TABLE`

Detaillierte Anweisungen zur Verwendung [&#x200B; ERSTELLEN &#x200B;](../advanced-statistics/models.md), einschließlich der Definition von Transformationen, der Festlegung von Modelloptionen und der Konfiguration von Trainingsdaten, finden Sie in der Dokumentation zu Modellen .

Informationen zur Verwendung mit `CREATE TABLE` finden Sie [&#x200B; Abschnitt „CREATE TABLE AS SELECT](#create-table-as-select).

#### MODELLBEISPIEL ERSTELLEN

```sql
CREATE MODEL review_model
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) AS ohe_add_comments,
  tokenizer(comments) AS token_comments,
  stop_words_remover(token_comments, array('and','very','much')) AS stp_token,
  ngram(stp_token, 3) AS ngram_token,
  tf_idf(ngram_token, 20) AS ngram_idf,
  count_vectorizer(stp_token, 13) AS cnt_vec_comments,
  tf_idf(token_comments, 10, 1) AS cmts_idf,
  vector_assembler(array(cmts_idf, viewsgot, ohe_add_comments, ngram_idf, cnt_vec_comments)) AS features
)
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='reviews')
AS SELECT * FROM movie_review_e2e_DND;
```

#### Einschränkungen {#limitations}

Die folgenden Einschränkungen gelten für die Verwendung von `TRANSFORM` mit `CREATE TABLE`. `CREATE TABLE AS SELECT` Abschnitt Einschränkungen und Verhalten finden Sie eine detaillierte Erklärung darüber, wie umgewandelte Daten gespeichert werden, wie Vektorausgaben verarbeitet werden und warum die Ergebnisse nicht direkt in Modell-Trainings-Workflows wiederverwendet werden können.

- Vektorausgaben werden automatisch in Arrays umgewandelt, die nicht direkt in `CREATE MODEL` verwendet werden können.
- Die Umwandlungslogik wird nicht als Metadaten beibehalten und kann nicht stapelweise wiederverwendet werden.

## INSERT INTO

Der `INSERT INTO`-Befehl wird wie folgt definiert:

>[!IMPORTANT]
>
>Der Abfrage-Service unterstützt **nur angehängte Vorgänge** mithilfe der ITAS-Engine. `INSERT INTO` ist der einzige unterstützte Datenmanipulationsbefehl, **Vorgänge** Aktualisieren **und** sind nicht verfügbar. Um Änderungen in Ihren Daten widerzuspiegeln, fügen Sie neue Datensätze ein, die den gewünschten Status darstellen.

```sql
INSERT INTO table_name select_query
```

| Parameter | Beschreibung |
| ----- | ----- |
| `table_name` | Der Name der Tabelle, in die Sie die Abfrage einfügen möchten. |
| `select_query` | Eine `SELECT`. Die Syntax der `SELECT` Abfrage finden Sie im Abschnitt [SELECT-Abfragen](#select-queries). |

**Beispiel**

>[!NOTE]
>
>Das Folgende ist ein fiktives Beispiel und dient lediglich zu Anleitungszwecken.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
>Schließen **nicht** die `SELECT`-Anweisung in Klammern () ein. Außerdem muss das Schema des Ergebnisses der `SELECT`-Anweisung mit dem der in der `INSERT INTO`-Anweisung definierten Tabelle übereinstimmen. Sie können eine `SNAPSHOT`-Klausel bereitstellen, um inkrementelle Deltas in die Zieltabelle zu lesen.

Die meisten Felder in einem echten XDM-Schema werden nicht auf der Stammebene gefunden und SQL erlaubt die Verwendung der Punktnotation nicht. Um mit verschachtelten Feldern ein realistisches Ergebnis zu erzielen, müssen Sie jedes Feld in Ihrem `INSERT INTO` zuordnen.

To `INSERT INTO` nested paths, use the following syntax:

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

The `DROP TABLE` command drops an existing table and deletes the directory associated with the table from the file system if it is not an external table. If the table does not exist, an exception occurs.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| Parameter | Beschreibung |
| ------ | ------ |
| `IF EXISTS` | If this is specified, no exception is thrown if the table does **not** exist. |

## CREATE DATABASE

The `CREATE DATABASE` command creates an Azure Data Lake Storage (ADLS) database.

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## DROP DATABASE

The `DROP DATABASE` command deletes the database from an instance.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| Parameter | Beschreibung |
| ------ | ------ |
| `IF EXISTS` | If this is specified, no exception is thrown if the database does **not** exist. |

## DROP SCHEMA

The `DROP SCHEMA` command drops an existing schema.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| Parameter | Beschreibung |
| ------ | ------ |
| `IF EXISTS` | If this parameter is specified and the schema does **not** exist, no exception is thrown. |
| `RESTRICT` | The default value for the mode. If specified, the schema only drops if it does **not** contain any tables. |
| `CASCADE` | If specified, the schema is dropped along with all the tables present in the schema. |

## CREATE VIEW {#create-view}

An SQL view is a virtual table based on the result-set of an SQL statement. Create a view with the `CREATE VIEW` statement and give it a name. You can then use that name to refer back to the results of the query. This makes it easier to reuse complex queries.

The following syntax defines a `CREATE VIEW` query for a dataset. This dataset can be an ADLS or accelerated store dataset.

```sql
CREATE VIEW view_name AS select_query
```

| Parameter | Beschreibung |
| ------ | ------ |
| `view_name` | The name of view to be created. |
| `select_query` | Eine `SELECT`. Die Syntax der `SELECT` Abfrage finden Sie im Abschnitt [SELECT-Abfragen](#select-queries). |

**Beispiel**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

The following syntax defines a `CREATE VIEW` query which creates a view in the context of a database and schema.

**Beispiel**

```sql
CREATE VIEW db_name.schema_name.view_name AS select_query
CREATE OR REPLACE VIEW db_name.schema_name.view_name AS select_query
```

| Parameter | Beschreibung |
| ------ | ------ |
| `db_name` | Der Name der Datenbank. |
| `schema_name` | Der Name des Schemas. |
| `view_name` | Der Name der zu erstellenden Ansicht. |
| `select_query` | Eine `SELECT`. Die Syntax der `SELECT` Abfrage finden Sie im Abschnitt [SELECT-Abfragen](#select-queries). |

**Beispiel**

```sql
CREATE VIEW <dbV1 AS SELECT color, type FROM Inventory;

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory;
```

## ANSICHTEN ANZEIGEN

Die folgende Abfrage zeigt die Liste der Ansichten.

```sql
SHOW VIEWS;
```

```console
 Db Name  | Schema Name | Name  | Id       |  Dataset Dependencies | Views Dependencies | TYPE
|----------------------------------------------------------------------------------------------
 qsaccel  | profile_agg | view1 | view_id1 | dwh_dataset1          |                    | DWH
          |             | view2 | view_id2 | adls_dataset          | adls_views         | ADLS
(2 rows)
```

## DROP VIEW

Die folgende Syntax definiert eine `DROP VIEW`:

```sql
DROP VIEW [IF EXISTS] view_name
```

| Parameter | Beschreibung |
| ------ | ------ |
| `IF EXISTS` | Wenn dies angegeben ist, wird keine Ausnahme ausgelöst, wenn die Ansicht **nicht** vorhanden ist. |
| `view_name` | Der Name der zu löschenden Ansicht. |

**Beispiel**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Anonymer Block {#anonymous-block}

Ein anonymer Block besteht aus zwei Abschnitten: dem ausführbaren Abschnitt und dem Abschnitt zur Ausnahmebehandlung. In einem anonymen Block ist der ausführbare Abschnitt obligatorisch. Der Abschnitt zur Ausnahmebehandlung ist jedoch optional.

Das folgende Beispiel zeigt, wie ein Block mit einer oder mehreren Anweisungen erstellt wird, die zusammen ausgeführt werden sollen:

```sql
$$BEGIN
  statementList
[EXCEPTION exceptionHandler]
$$END

exceptionHandler:
      WHEN OTHERS
      THEN statementList

statementList:
    : (statement (';')) +
```

Nachfolgend finden Sie ein Beispiel zur Verwendung des anonymen Blocks.

```sql
$$BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHERS THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
$$END;
```

### Bedingte Anweisungen in einem anonymen Block {#conditional-anonymous-block-statements}

Die IF-THEN-ELSE-Steuerungsstruktur ermöglicht die bedingte Ausführung einer Liste von Anweisungen, wenn eine Bedingung als TRUE ausgewertet wird. Diese Kontrollstruktur ist nur innerhalb eines anonymen Blocks anwendbar. Wenn diese Struktur als eigenständiger Befehl verwendet wird, führt dies zu einem Syntaxfehler (ungültiger Befehl außerhalb des anonymen Blocks).

Der folgende Codeausschnitt zeigt das richtige Format für eine bedingte IF-THEN-ELSE-Anweisung in einem anonymen Block.

```javascript
IF booleanExpression THEN
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSE
   List of statements;
END IF
```

**Beispiel**

Im folgenden Beispiel wird `SELECT 200;` ausgeführt.

```sql
$$BEGIN
    SET @V = SELECT 2;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;   

 END$$;
```

Diese Struktur kann mit `raise_error();` verwendet werden, um eine benutzerdefinierte Fehlermeldung zurückzugeben. Der unten gezeigte Code-Block beendet den anonymen Block mit „Benutzerdefinierte Fehlermeldung“.

**Beispiel**

```sql
$$BEGIN
    SET @V = SELECT 5;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT raise_error('custom error message');
    END IF;   

 END$$;
```

#### Verschachtelte IF-Anweisungen

Verschachtelte IF-Anweisungen werden in anonymen Blöcken unterstützt.

**Beispiel**

```sql
$$BEGIN
    SET @V = SELECT 1;
    IF @V = 1 THEN
       SELECT 100;
       IF @V > 0 THEN
         SELECT 1000;
       END IF;   
    END IF;   

 END$$; 
```

#### Ausnahmenblöcke

Exception blocks are supported within anonymous blocks.

**Beispiel**

```sql
$$BEGIN
    SET @V = SELECT 2;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT raise_error(concat('custom-error for v= ', '@V' ));

    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;  
EXCEPTION WHEN OTHERS THEN 
  SELECT 'THERE WAS AN ERROR';    
 END$$;
```

### Auto to JSON {#auto-to-json}

Query Service supports an optional session-level setting to return top-level complex fields from interactive SELECT queries as JSON strings. The `auto_to_json` setting allows for data from complex fields to be returned as JSON then parsed into JSON objects using standard libraries.

SET the feature flag `auto_to_json` to true before executing your SELECT query that contains complex fields.

```sql
set auto_to_json=true; 
```

#### Before setting the `auto_to_json` flag

The following table provides an example query result before the `auto_to_json` setting is applied. The same SELECT query (as seen below) that targets a table with complex fields was used in both scenarios.

```sql
SELECT * FROM TABLE_WITH_COMPLEX_FIELDS LIMIT 2;
```

The results are as follows:

```console
                _id                |                                _experience                                 | application  |                   commerce                   | dataSource |                               device                               |                       endUserIDs                       |                                                                                                environment                                                                                                |                     identityMap                     |                              placeContext                               |   receivedTimestamp   |       timestamp       | userActivityRegion |                                         web                                          | _adcstageforpqs
|-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### After setting the `auto_to_json` flag

The following table demonstrates the difference in results that the `auto_to_json` setting has on the resulting dataset. The same SELECT query was used in both scenarios.

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
|-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### Resolve fallback snapshot on failure {#resolve-fallback-snapshot-on-failure}

The `resolve_fallback_snapshot_on_failure` option is used to resolve the issue of an expired snapshot ID.

Set the `resolve_fallback_snapshot_on_failure` option to true to override a snapshot with a previous snapshot ID.

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
  WHEN OTHERS THEN
    SELECT 'ERROR';
END
$$;
```


## Organisation von Daten-Medienelementen

It is important to logically organize your data assets within the Adobe Experience Platform data lake as they grow. Query Service extends SQL constructs that enable you to logically group data assets within a sandbox. This method of organization allows for the sharing of data assets between schemas without the need to move them physically.

The following SQL constructs using standard SQL syntax are supported for you to logically organize your data.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

See the [logical organization of data assets](../best-practices/organize-data-assets.md) guide for a more detailed explanation on Query Service best practices.

## Tabelle vorhanden

The `table_exists` SQL command is used to confirm whether a table currently exists in the system. Der Befehl gibt einen booleschen Wert zurück: `true`, wenn eine Tabelle **vorhanden** ist, und `false`, wenn **keine** Tabelle vorhanden ist.

By validating whether a table exists before running the statements, the `table_exists` feature simplifies the process of writing an anonymous block to cover both the `CREATE` and `INSERT INTO` use cases.

The following syntax defines the `table_exists` command:

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
WHEN OTHERS THEN SELECT 'ERROR';

END $$; 
```

## Inline {#inline}

The `inline` function separates the elements of an array of structs and generates the values into a table. Es kann nur in der `SELECT` oder einer `LATERAL VIEW` platziert werden.

Die `inline` Funktion **kann** nicht in eine Auswahlliste eingefügt werden, in der andere Generatorfunktionen vorhanden sind.

Standardmäßig werden die erstellten Spalten „col1“, „col2“ usw. genannt. Wenn der Ausdruck `NULL` ist, werden keine Zeilen erstellt.

>[!TIP]
>
>Spaltennamen können mit dem Befehl `RENAME` umbenannt werden.

**Beispiel**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

Das Beispiel gibt Folgendes zurück:

```text
1  a Spark SQL
2  b Spark SQL
```

Dieses zweite Beispiel zeigt außerdem das Konzept und die Anwendung der `inline`. Das Datenmodell für das Beispiel ist in der Abbildung unten dargestellt.

![Ein Schemadiagramm für productListItems.](../images/sql/productListItems.png)

**Beispiel**

```sql
select inline(productListItems) from source_dataset limit 10;
```

Die aus dem `source_dataset` übernommenen Werte werden in die Zieltabelle eingetragen.

| SKU | _experience | Menge | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | („(„(A,pass,b,NULL)„)„) | 5 | 10,5 |
| product-id-5 | („(„(A, pass, B, NULL)„)„) |          |              |
| product-id-2 | („(„(AF, C, D, NULL)„)„) | 6 | 40 |
| product-id-4 | („(„(BM, PASS, NA, NULL)„)„) | 3 | 12 |

## SET

Der Befehl `SET` legt eine Eigenschaft fest und gibt entweder den Wert einer vorhandenen Eigenschaft zurück oder listet alle vorhandenen Eigenschaften auf. Wenn für einen vorhandenen Eigenschaftenschlüssel ein Wert angegeben wird, wird der alte Wert überschrieben.

```sql
SET property_key = property_value
```

| Parameter | Beschreibung |
| ------ | ------ |
| `property_key` | Der Name der Eigenschaft, die Sie auflisten oder ändern möchten. |
| `property_value` | Der Wert, den die Eigenschaft festlegen soll. |

Um den Wert für eine beliebige Einstellung zurückzugeben, verwenden Sie `SET [property key]` ohne `property_value`.

## [!DNL PostgreSQL]

In den folgenden Unterabschnitten werden die [!DNL PostgreSQL]-Befehle beschrieben, die vom Abfrage-Service unterstützt werden.

### TABELLE ANALYSIEREN {#analyze-table}

Der Befehl `ANALYZE TABLE` führt eine Verteilungsanalyse und statistische Berechnungen für die benannte(n) Tabelle(n) durch. Die Verwendung von `ANALYZE TABLE` hängt davon ab, ob die Datensätze im [beschleunigten Speicher](#compute-statistics-accelerated-store) oder im [Data Lake](#compute-statistics-data-lake) gespeichert werden. Weitere Informationen zur Verwendung finden Sie in den entsprechenden Abschnitten.

#### BERECHNEN VON STATISTIKEN im beschleunigten Speicher {#compute-statistics-accelerated-store}

Der Befehl `ANALYZE TABLE` berechnet Statistiken für eine Tabelle im beschleunigten Speicher. Die Statistiken werden für ausgeführte CTAS- oder ITAS-Abfragen für eine bestimmte Tabelle im beschleunigten Speicher berechnet.

**Beispiel**

```sql
ANALYZE TABLE <original_table_name>
```

Im Folgenden finden Sie eine Liste statistischer Berechnungen, die nach Verwendung des `ANALYZE TABLE`-Befehls verfügbar sind:-

| Berechnete Werte | Beschreibung |
|---|---|
| `field` | Der Name der Spalte in einer Tabelle. |
| `data-type` | Der zulässige Datentyp für jede Spalte. |
| `count` | Die Anzahl der Zeilen, die für dieses Feld einen Wert ungleich null enthalten. |
| `distinct-count` | Die Anzahl der eindeutigen oder eindeutigen Werte für dieses Feld. |
| `missing` | Die Anzahl der Zeilen mit einem Nullwert für dieses Feld. |
| `max` | Der Höchstwert aus der analysierten Tabelle. |
| `min` | Der Mindestwert aus der analysierten Tabelle. |
| `mean` | Der Durchschnittswert der analysierten Tabelle. |
| `stdev` | Die Standardabweichung der analysierten Tabelle. |

#### BERECHNEN VON STATISTIKEN zum Data Lake {#compute-statistics-data-lake}

Sie können jetzt mit dem `COMPUTE STATISTICS` SQL-Befehl Statistiken auf Spaltenebene für [!DNL Azure Data Lake Storage] (ADLS)-Datensätze berechnen. Spaltenstatistiken entweder für den gesamten Datensatz, eine Teilmenge eines Datensatzes, alle Spalten oder eine Teilmenge von Spalten berechnen.

`COMPUTE STATISTICS` erweitert den `ANALYZE TABLE`. Die Befehle `COMPUTE STATISTICS`, `FILTERCONTEXT` und `FOR COLUMNS` werden jedoch in beschleunigten Speichertabellen nicht unterstützt. Diese Erweiterungen für den Befehl `ANALYZE TABLE` werden derzeit nur für ADLS-Tabellen unterstützt.

**Beispiel**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

Der Befehl `FILTER CONTEXT` berechnet Statistiken für eine Teilmenge des Datensatzes basierend auf der bereitgestellten Filterbedingung. Der Befehl `FOR COLUMNS` zielt auf bestimmte Spalten für die Analyse ab.

>[!NOTE]
>
>Die `Statistics ID` und die generierten Statistiken sind nur für jede Sitzung gültig und können nicht über verschiedene PSQL-Sitzungen hinweg aufgerufen werden.<br><br>Einschränkungen:<ul><li>Die Erstellung von Statistiken wird für die Datentypen „Array“ und „Zuordnung“ nicht unterstützt</li><li>Berechnete Statistiken werden **nicht** sitzungsübergreifend beibehalten.</li></ul><br><br>Optionen:<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br>Standardmäßig ist das Flag auf „true“ gesetzt. Wenn Statistiken für einen nicht unterstützten Datentyp angefordert werden, werden daher keine Fehler ausgegeben, sondern Felder mit den nicht unterstützten Datentypen werden im Hintergrund übersprungen.<br>Um Benachrichtigungen zu Fehlern zu aktivieren, wenn Statistiken zu nicht unterstützten Datentypen angefordert werden, verwenden Sie: `SET skip_stats_for_complex_datatypes = false`.

Die Konsolenausgabe wird wie unten dargestellt angezeigt.

```console
|     Statistics ID      |
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

Sie können dann die berechneten Statistiken direkt abfragen, indem Sie auf die `Statistics ID` verweisen. Verwenden Sie die `Statistics ID` oder den Aliasnamen, wie in der folgenden Beispielanweisung gezeigt, um die Ausgabe vollständig anzuzeigen. Weitere Informationen zu dieser Funktion finden Sie in der [Dokumentation zu Aliasnamen](../key-concepts/dataset-statistics.md#alias-name).

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

Verwenden Sie den Befehl `SHOW STATISTICS` , um die Metadaten für alle in der Sitzung generierten temporären Statistiken anzuzeigen. Mithilfe dieses Befehls können Sie den Umfang Ihrer statistischen Analyse verfeinern.

```sql
SHOW STATISTICS;
```

Nachfolgend finden Sie eine Beispielausgabe von SHOW STATISTICS.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
|----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Weitere Informationen finden [&#x200B; in der &#x200B;](../key-concepts/dataset-statistics.md) zu Datensatzstatistiken .

#### TABELLENBEISPIEL {#tablesample}

Der Abfrage-Service von Adobe Experience Platform bietet Beispieldatensätze als Teil der Funktionen zur annähernden Abfrageverarbeitung.

Datensatzbeispiele eignen sich am besten, wenn Sie keine genaue Antwort für einen Aggregatvorgang für einen Datensatz benötigen. Verwenden Sie die `TABLESAMPLE`-Funktion, um effizientere explorative Abfragen für große Datensätze durchzuführen, indem Sie eine annähernde Abfrage ausgeben, um eine ungefähre Antwort zurückzugeben.

Beispieldatensätze werden mit einheitlichen Zufallsproben aus vorhandenen [!DNL Azure Data Lake Storage] (ADLS)-Datensätzen erstellt, wobei nur ein Prozentsatz der Datensätze aus dem Original verwendet wird. Die Datensatzbeispielfunktion erweitert den `ANALYZE TABLE`-Befehl mit den `TABLESAMPLE`- und `SAMPLERATE` SQL-Befehlen.

Im folgenden Beispiel zeigt Zeile 1, wie eine 5 %-Stichprobe der Tabelle berechnet wird. Zeile zwei zeigt, wie eine 5 %-Stichprobe aus einer gefilterten Ansicht der Daten in der Tabelle berechnet wird.

**Beispiel**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

Weitere Informationen finden [&#x200B; in der &#x200B;](../key-concepts/dataset-samples.md) zu Datensatzbeispielen .

### BEGIN

Der `BEGIN`-Befehl oder alternativ der `BEGIN WORK`- oder `BEGIN TRANSACTION`-Befehl initiiert einen Transaktionsblock. Alle Anweisungen, die nach dem Befehl „begin“ eingegeben werden, werden in einer einzigen Transaktion ausgeführt, bis ein expliziter COMMIT- oder ROLLBACK-Befehl gegeben wird. Dieser Befehl entspricht dem Befehl `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### CLOSE

Der Befehl `CLOSE` gibt die Ressourcen frei, die einem geöffneten Cursor zugeordnet sind. Nach dem Schließen des Cursors sind keine weiteren Vorgänge zulässig. Ein Cursor sollte geschlossen werden, wenn er nicht mehr benötigt wird.

```sql
CLOSE name
CLOSE ALL
```

Wenn `CLOSE name` verwendet wird, steht `name` für den Namen eines geöffneten Cursors, der geschlossen werden muss. Wenn `CLOSE ALL` verwendet wird, werden alle offenen Cursor geschlossen.

### DEALLOCATE

Um die Zuordnung einer zuvor vorbereiteten SQL-Anweisung aufzuheben, verwenden Sie den `DEALLOCATE`. Wenn Sie die Zuordnung einer vorbereiteten Anweisung nicht explizit aufgehoben haben, wird die Zuordnung aufgehoben, wenn die Sitzung beendet wird. Weitere Informationen zu vorbereiteten Anweisungen finden Sie im Abschnitt [BEFEHL VORBEREITEN](#prepare).

```sql
DEALLOCATE name
DEALLOCATE ALL
```

Wenn `DEALLOCATE name` verwendet wird, steht `name` für den Namen der vorbereiteten Anweisung, deren Zuordnung aufgehoben werden muss. Wenn `DEALLOCATE ALL` verwendet wird, werden alle vorbereiteten Anweisungen freigegeben.

### DECLARE

Mit dem Befehl `DECLARE` können Benutzer einen Cursor erstellen, mit dem aus einer größeren Abfrage eine kleine Anzahl von Zeilen abgerufen werden kann. Nachdem der Cursor erstellt wurde, werden Zeilen mit `FETCH` abgerufen.

```sql
DECLARE name CURSOR FOR query
```

| Parameter | Beschreibung |
| ------ | ------ |
| `name` | Der Name des zu erstellenden Cursors. |
| `query` | Ein `SELECT`- oder `VALUES`-Befehl, der die vom Cursor zurückzugebenden Zeilen bereitstellt. |

### EXECUTE

Der Befehl `EXECUTE` wird verwendet, um eine zuvor vorbereitete Anweisung auszuführen. Da vorbereitete Anweisungen nur während einer Sitzung vorhanden sind, muss die vorbereitete Anweisung durch eine `PREPARE` Anweisung erstellt worden sein, die zuvor in der aktuellen Sitzung ausgeführt wurde. Weitere Informationen zur Verwendung von vorbereiteten Anweisungen finden Sie im Abschnitt [`PREPARE`Befehl](#prepare).

Wenn die `PREPARE`, die die Anweisung erstellt hat, einige Parameter angegeben hat, muss ein kompatibler Parametersatz an die `EXECUTE` übergeben werden. Wenn diese Parameter nicht übergeben werden, wird ein Fehler ausgelöst.

```sql
EXECUTE name [ ( parameter ) ]
```

| Parameter | Beschreibung |
| ------ | ------ |
| `name` | Der Name der auszuführenden vorbereiteten Anweisung. |
| `parameter` | Der tatsächliche Wert eines Parameters für die vorbereitete Anweisung. Dies muss ein Ausdruck sein, der einen Wert liefert, der mit dem Datentyp dieses Parameters kompatibel ist, der bei der Erstellung der vorbereiteten Anweisung bestimmt wurde. Wenn mehrere Parameter für die vorbereitete Anweisung vorhanden sind, werden sie durch Kommas getrennt. |

### EXPLAIN

Der Befehl `EXPLAIN` zeigt den Ausführungsplan für die angegebene Anweisung an. Der Ausführungsplan zeigt an, wie die von der Anweisung referenzierten Tabellen gescannt werden. Wenn mehrere Tabellen referenziert werden, wird gezeigt, welche Join-Algorithmen verwendet werden, um die erforderlichen Zeilen aus jeder Eingabetabelle zusammenzuführen.

```sql
EXPLAIN statement
```

Um das Format der Antwort zu definieren, verwenden Sie das Schlüsselwort `FORMAT` mit dem Befehl `EXPLAIN` .

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| Parameter | Beschreibung |
| ------ | ------ |
| `FORMAT` | Geben Sie mit dem Befehl `FORMAT` das Ausgabeformat an. Die verfügbaren Optionen sind `TEXT` oder `JSON`. Die Ausgabe ohne Text enthält dieselben Informationen wie das Textausgabeformat, ist jedoch für Programme einfacher zu analysieren. Dieser Parameter ist standardmäßig auf `TEXT` voreingestellt. |
| `statement` | Alle `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS` oder `CREATE MATERIALIZED VIEW AS` Anweisungen, deren Ausführungsplan Sie anzeigen möchten. |

>[!IMPORTANT]
>
>Jede Ausgabe, die eine `SELECT`-Anweisung möglicherweise zurückgibt, wird bei der Ausführung mit dem `EXPLAIN`-Schlüsselwort verworfen. Andere Nebenwirkungen der Anweisung treten wie gewohnt auf.

**Beispiel**

Das folgende Beispiel zeigt den Plan für eine einfache Abfrage in einer Tabelle mit einer einzelnen `integer` und 10000 Zeilen:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
|---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### FETCH

Der Befehl `FETCH` ruft Zeilen mit einem zuvor erstellten Cursor ab.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| Parameter | Beschreibung |
| ------ | ------ |
| `num_of_rows` | Die Anzahl der abzurufenden Zeilen. |
| `cursor_name` | Der Name des Cursors, von dem Sie Informationen abrufen. |

### PREPARE {#prepare}

Mit dem Befehl `PREPARE` können Sie eine vorbereitete Anweisung erstellen. Eine vorbereitete Anweisung ist ein Server-seitiges Objekt, das verwendet werden kann, um ähnliche SQL-Anweisungen in Vorlagen einzufügen.

Vorbereitete Anweisungen können Parameter annehmen. Dabei handelt es sich um Werte, die bei ihrer Ausführung in die Anweisung eingefügt werden. Parameter werden bei Verwendung von vorbereiteten Anweisungen nach Position referenziert (z. B. $1, $2).

Optional können Sie eine Liste von Parameterdatentypen angeben. Wenn der Datentyp eines Parameters nicht aufgeführt ist, kann der Typ aus dem Kontext abgeleitet werden.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| Parameter | Beschreibung |
| ------ | ------ |
| `name` | Der Name der vorbereiteten Anweisung. |
| `data_type` | Die Datentypen der Parameter der vorbereiteten Anweisung. Wenn der Datentyp eines Parameters nicht aufgeführt ist, kann der Typ aus dem Kontext abgeleitet werden. Wenn Sie mehrere Datentypen hinzufügen müssen, können Sie sie in einer kommagetrennten Liste hinzufügen. |

### ROLLBACK

Der Befehl `ROLLBACK` macht die aktuelle Transaktion rückgängig und verwirft alle von der Transaktion vorgenommenen Aktualisierungen.

```sql
ROLLBACK
ROLLBACK WORK
```

### SELECT INTO

Der Befehl `SELECT INTO` erstellt eine neue Tabelle und füllt sie mit Daten, die durch eine Abfrage berechnet werden. Die Daten werden nicht an den Client zurückgegeben, da sie mit einem normalen `SELECT`-Befehl verarbeitet werden. Die Spalten der neuen Tabelle haben die Namen und Datentypen, die mit den Ausgabespalten des `SELECT`-Befehls verknüpft sind.

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

Weitere Informationen zu den standardmäßigen SELECT-Abfrageparametern finden Sie im Abschnitt [SELECT-Abfrage](#select-queries). In diesem Abschnitt werden nur Parameter aufgelistet, die sich ausschließlich auf den `SELECT INTO`-Befehl beziehen.

| Parameter | Beschreibung |
| ------ | ------ |
| `TEMPORARY` oder `TEMP` | Ein optionaler Parameter. If the parameter is specified, the created table is a temporary table. |
| `UNLOGGED` | Ein optionaler Parameter. If the parameter is specified, the created table is an unlogged table. More information about unlogged tables can be found in the [[!DNL PostgreSQL] documentation](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | The name of the table to be created. |

**Beispiel**

The following query creates a new table `films_recent` consisting of only recent entries from the table `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### SHOW

The `SHOW` command displays the current setting of runtime parameters. These variables can be set using the `SET` statement, by editing the `postgresql.conf` configuration file, through the `PGOPTIONS` environmental variable (when using libpq or a libpq-based application), or through command-line flags when starting the Postgres server.

```sql
SHOW name
SHOW ALL
```

| Parameter | Beschreibung |
| ------ | ------ |
| `name` | The name of the runtime parameter you want information about. Possible values for the runtime parameter include the following values:<br>`SERVER_VERSION`: This parameter shows the server&#39;s version number.<br>`SERVER_ENCODING`: This parameter shows the server-side character set encoding.<br>`LC_COLLATE`: This parameter shows the database&#39;s locale setting for collation (text ordering).<br>`LC_CTYPE`: This parameter shows the database&#39;s locale setting for character classification.<br>`IS_SUPERUSER`: This parameter shows if the current role has superuser privileges. |
| `ALL` | Show the values of all configuration parameters with descriptions. |

**Beispiel**

The following query shows the current setting of the parameter `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
|-----------
 ISO, MDY
(1 row)
```

### COPY

The `COPY` command duplicates the output of any `SELECT` query to a specified location. The user must have access to this location for this command to succeed.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| Parameter | Beschreibung |
| ------ | ------ |
| `query` | The query that you want to copy. |
| `format_name` | The format that you want to copy the query in. The `format_name` can be one of `parquet`, `csv`, or `json`. By default, the value is `parquet`. |

>[!NOTE]
>
>The complete output path is `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE {#alter-table}

The `ALTER TABLE` command lets you add or drop primary or foreign key constraints and add columns to the table.

#### ADD or DROP CONSTRAINT

The following SQL queries show examples of adding or dropping constraints to a table. Primary key and foreign key constraints can be added to multiple columns with comma-separated values. Sie können zusammengesetzte Schlüssel erstellen, indem Sie zwei oder mehr Werte für Spaltennamen übergeben, wie in den Beispielen unten dargestellt.

**Definieren von Primärschlüsseln oder zusammengesetzten Schlüsseln**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name1, column_name2 ) NAMESPACE namespace
```

**Definieren einer Beziehung zwischen Tabellen basierend auf einem oder mehreren Schlüsseln**

```sql
ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name1, column_name2 ) REFERENCES referenced_table_name ( primary_column_name1, primary_column_name2 )
```

**Definieren einer Identitätsspalte**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace
```

**Begrenzung/Beziehung/Identität löschen**

```sql
ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name1, column_name2 )

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
>Das Tabellenschema sollte eindeutig sein und nicht von mehreren Tabellen gemeinsam genutzt werden. Außerdem ist der Namespace für den Primärschlüssel, die primäre Identität und Identitätseinschränkungen obligatorisch.

#### Primäre und sekundäre Identitäten hinzufügen oder löschen

Verwenden Sie den `ALTER TABLE`-Befehl, um Begrenzungen für primäre und sekundäre Identitätstabellenspalten hinzuzufügen oder zu löschen.

In den folgenden Beispielen werden eine primäre Identität und eine sekundäre Identität hinzugefügt, indem Einschränkungen hinzugefügt werden.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

Identitäten können auch entfernt werden, indem Einschränkungen entfernt werden, wie im Beispiel unten dargestellt.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

Weitere Informationen finden Sie im Dokument zum [&#x200B; von Identitäten in Ad-hoc-Datensätzen](../data-governance/ad-hoc-schema-identities.md).

#### SPALTE HINZUFÜGEN

Die folgenden SQL-Abfragen zeigen Beispiele für das Hinzufügen von Spalten zu einer Tabelle.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### Unterstützte Datentypen

In der folgenden Tabelle sind die akzeptierten Datentypen für das Hinzufügen von Spalten zu einer Tabelle mit [!DNL Postgres SQL], XDM und dem [!DNL Accelerated Database Recovery] (ADR) in Azure SQL aufgeführt.

| --- | PSQL-Client | XDM | ADR | Beschreibung |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | Ein numerischer Datentyp, mit dem große Ganzzahlen zwischen -9.223.372.036.854.775.807 und 9.223.372.036.854.775.807 in 8 Byte gespeichert werden. |
| 2 | `integer` | `int4` | `integer` | Ein numerischer Datentyp, mit dem Ganzzahlen zwischen -2.147.483.648 und 2.147.483.647 in 4 Bytes gespeichert werden. |
| 3 | `smallint` | `int2` | `smallint` | Ein numerischer Datentyp, mit dem Ganzzahlen zwischen -32.768 und 215-1 32.767 in 2 Byte gespeichert werden. |
| 4 | `tinyint` | `int1` | `tinyint` | Ein numerischer Datentyp, mit dem Ganzzahlen zwischen 0 und 255 in 1 Byte gespeichert werden. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | Ein Datentyp für Zeichen mit variabler Größe. `varchar` ist am besten geeignet, wenn die Größe der Spaltendateneinträge erheblich variiert. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` und `FLOAT` sind gültige Synonyme für `DOUBLE PRECISION`. `double precision` ist ein Gleitkomma-Datentyp. Gleitkommawerte werden in 8 Byte gespeichert. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` ist ein gültiges Synonym für `double precision`.`double precision` ist ein Gleitkomma-Datentyp. Gleitkommawerte werden in 8 Byte gespeichert. |
| 8 | `date` | `date` | `date` | Bei den `date` Datentypen handelt es sich um 4-Byte-gespeicherte Kalenderdatumswerte ohne Zeitstempelinformationen. Der Datumsbereich reicht von 01-01-0001 bis 12-31-9999. |
| 9 | `datetime` | `datetime` | `datetime` | Ein Datentyp, mit dem ein Zeitpunkt gespeichert wird, der als Kalenderdatum und -uhrzeit ausgedrückt wird. `datetime` enthält die Kriterien Jahr, Monat, Tag, Stunde, Sekunde und Bruch. Eine `datetime` kann eine beliebige Teilmenge dieser Zeiteinheiten enthalten, die in dieser Folge verbunden sind, oder sogar nur eine einzige Zeiteinheit umfassen. |
| 10 | `char(len)` | `string` | `char(len)` | Das `char(len)`-Schlüsselwort wird verwendet, um anzugeben, dass das Element ein Zeichen fester Länge ist. |

#### SCHEMA HINZUFÜGEN

Die folgende SQL-Abfrage zeigt ein Beispiel für das Hinzufügen einer Tabelle zu einer Datenbank/einem Schema.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> ADLS-Tabellen und -Ansichten können nicht zu DWH-Datenbanken/Schemata hinzugefügt werden.


#### SCHEMA ENTFERNEN

Die folgende SQL-Abfrage zeigt ein Beispiel für das Entfernen einer Tabelle aus einer Datenbank/einem Schema.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> DWH-Tabellen und -Ansichten können nicht aus physisch verknüpften DWH-Datenbanken/Schemata entfernt werden.


**Parameter**

| Parameter | Beschreibung |
| ------ | ------ |
| `table_name` | Der Name der Tabelle, die Sie bearbeiten. |
| `column_name` | Der Name der Spalte, die Sie hinzufügen möchten. |
| `data_type` | Der Datentyp der Spalte, die Sie hinzufügen möchten. Zu den unterstützten Datentypen gehören: bigint, char, string, date, datetime, double, double Precision, integer, smallint, tinyint, varchar. |

### PRIMÄRE TASTEN ANZEIGEN

Der Befehl `SHOW PRIMARY KEYS` listet alle Einschränkungen für den Primärschlüssel für die angegebene Datenbank auf.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
|------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### FREMDSCHLÜSSEL ANZEIGEN

Der Befehl `SHOW FOREIGN KEYS` listet alle Fremdschlüsseleinschränkungen für die angegebene Datenbank auf.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
|------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### DATENGRUPPEN ANZEIGEN

Der Befehl `SHOW DATAGROUPS` gibt eine Tabelle aller zugehörigen Datenbanken zurück. Für jede Datenbank enthält die Tabelle das Schema, den Gruppentyp, den untergeordneten Typ, den untergeordneten Namen und die untergeordnete ID.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Accelerated Store | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### DATENGRUPPEN FÜR TABELLE ANZEIGEN

Der Befehl `SHOW DATAGROUPS FOR 'table_name'` gibt eine Tabelle aller zugehörigen Datenbanken zurück, die den -Parameter als untergeordneten Parameter enthalten. Für jede Datenbank enthält die Tabelle das Schema, den Gruppentyp, den untergeordneten Typ, den untergeordneten Namen und die untergeordnete ID.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**Parameter**

- `table_name`: Der Name der Tabelle, für die Sie verknüpfte Datenbanken suchen möchten.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
