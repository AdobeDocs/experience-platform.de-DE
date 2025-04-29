---
title: Modelle
description: Modell-Lebenszyklusverwaltung mit der Data Distiller SQL-Erweiterung. Erfahren Sie, wie Sie erweiterte statistische Modelle mithilfe von SQL erstellen, trainieren und verwalten, einschließlich wichtiger Prozesse wie Modellversionierung, -auswertung und -vorhersage, um aus Ihren Daten umsetzbare Einblicke zu gewinnen.
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 09129d9d19816b4d93b4979305f4ad532e5ffde4
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 1%

---

# Modelle

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Add-on Data Distiller erworben haben. Weitere Informationen erhalten Sie beim Adobe-Support.

Query Service unterstützt jetzt die Kernprozesse des Erstellens und Bereitstellens eines Modells. Sie können SQL verwenden, um das Modell unter Verwendung Ihrer Daten zu trainieren, seine Genauigkeit zu bewerten und dann das trainierte Modell verwenden, um Vorhersagen für neue Daten zu treffen. Anschließend können Sie das Modell verwenden, um aus Ihren früheren Daten zu generalisieren und fundierte Entscheidungen über reale Szenarien zu treffen.

Die drei Schritte im Modell-Lebenszyklus zum Generieren umsetzbarer Einblicke sind:

1. **Training**: Das Modell lernt Muster aus dem bereitgestellten Datensatz. (Modell erstellen oder ersetzen)
2. **Testen/**: Die Leistung des Modells wird mithilfe eines separaten Datensatzes bewertet. `model_evaluate`)
3. **Prognose**: Das trainierte Modell wird verwendet, um Vorhersagen für neue, nicht angezeigte Daten zu treffen.

Verwenden Sie die zur vorhandenen SQL-Grammatik hinzugefügte SQL-Erweiterung des Modells, um den Modelllebenszyklus entsprechend Ihren Geschäftsanforderungen zu verwalten. In diesem Dokument wird die SQL behandelt, die zum Erstellen oder Ersetzen eines Modells, zum Trainieren, Auswerten, ggf. erneuten Trainieren und Vorhersagen von Insights erforderlich ist.

## Modellerstellung und -training {#create-and-train}

Erfahren Sie, wie Sie ein maschinelles Lernmodell mithilfe von SQL-Befehlen definieren, konfigurieren und trainieren. Die folgende SQL-Anweisung zeigt, wie Sie ein Modell erstellen, Konstruktionstransformationen anwenden und den Trainingsprozess starten, um sicherzustellen, dass das Modell für die zukünftige Verwendung korrekt konfiguriert ist. Die folgenden SQL-Befehle beschreiben verschiedene Optionen für die Modellerstellung und -verwaltung:

- **MODELL ERSTELLEN**: Erstellt ein neues Modell für einen angegebenen Datensatz und trainiert es. Wenn bereits ein Modell mit demselben Namen vorhanden ist, gibt dieser Befehl einen Fehler zurück.
- **MODELL ERSTELLEN, WENN NICHT VORHANDEN**: Erstellt und trainiert ein neues Modell nur, wenn im angegebenen Datensatz noch kein Modell mit demselben Namen vorhanden ist.
- **MODELL ERSTELLEN ODER ERSETZEN**: Erstellt und trainiert ein Modell und ersetzt die neueste Version eines vorhandenen Modells durch denselben Namen im angegebenen Datensatz.

```sql
CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_alias
[TRANSFORM (select_list)]
[OPTIONS(model_option_list)]
[AS {select_query}]
 
model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
                   'LOGISTIC_REG' |
                   'KMEANS' }
  [, MAX_ITER = int64_value ]
 [, LABEL = string_array ]
[, REG_PARAM = float64_value ]
```

**Beispiel**

```sql
CREATE MODEL churn_model
TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features) 
OPTIONS(MODEL_TYPE='linear_reg', LABEL='churn_rate') 
AS
SELECT *
FROM churn_with_rate
ORDER BY period;
```

Um Ihnen dabei zu helfen, die wichtigsten Komponenten und Konfigurationen im Prozess der Modellerstellung und des Trainings zu verstehen, werden in den folgenden Anmerkungen der Zweck und die Funktion der einzelnen Elemente im obigen SQL-Beispiel erläutert.

- `<model_alias>`: Der Modellalias ist ein wiederverwendbarer Name, der dem Modell zugewiesen ist und später referenziert werden kann. Sie müssen Ihrem Modell einen Namen geben.
- `transform`: Die Transform-Klausel wird verwendet, um Feature Engineering-Umwandlungen (z. B. Einmal-Kodierung und Zeichenfolgenindizierung) auf den Datensatz anzuwenden, bevor das Modell trainiert wird. Die letzte Klausel der `TRANSFORM`-Anweisung sollte entweder ein `vector_assembler` mit einer Liste von Spalten sein, aus denen die Funktionen für das Modelltraining bestehen würden, oder ein abgeleiteter Typ des `vector_assembler` (z. B. `max_abs_scaler(feature)`, `standard_scaler(feature)` usw.). Nur die im letzten Abschnitt erwähnten Spalten werden für das Training verwendet. Alle anderen Spalten werden ausgeschlossen, selbst wenn sie in der `SELECT` Abfrage enthalten sind.
- `label = <label-COLUMN>`: Die Bezeichnungsspalte im Trainings-Datensatz, die das Ziel oder das Ergebnis angibt, das das Modell vorhersagen soll.
- `training-dataset`: Mit dieser Syntax werden die Daten ausgewählt, die zum Trainieren des Modells verwendet werden.
- `type = 'LogisticRegression'`: Diese Syntax gibt den Typ des zu verwendenden Algorithmus für maschinelles Lernen an. Zu den Optionen gehören `LinearRegression`, `LogisticRegression` und `KMeans`.
- `options`: Dieses Keyword bietet einen flexiblen Satz von Schlüssel-Wert-Paaren zum Konfigurieren des Modells.
   - `Key model_type`: `model_type = '<supported algorithm>'`: Gibt den Typ des zu verwendenden Algorithmus für maschinelles Lernen an. Zu den unterstützten Optionen gehören `LinearRegression`, `LogisticRegression` und `KMeans`.
   - `Key label`: `label = <label_COLUMN>`: Definiert die Bezeichnungsspalte im Trainings-Datensatz, die das Ziel oder das Ergebnis angibt, das das Modell vorhersagen soll.

Verwenden Sie SQL, um auf den für das Training verwendeten Datensatz zu verweisen.

>[!TIP]
>
>Eine vollständige Referenz zur `TRANSFORM`-Klausel, einschließlich unterstützter Funktionen und der Verwendung in `CREATE MODEL` und `CREATE TABLE`, finden Sie in der [`TRANSFORM`-Klausel in der SQL-Syntaxdokumentation](../sql/syntax.md#transform).

## Modell aktualisieren {#update}

Erfahren Sie, wie Sie ein vorhandenes Modell für maschinelles Lernen aktualisieren können, indem Sie neue technische Funktionstransformationen anwenden und Optionen wie den Algorithmustyp und die Beschriftungsspalte konfigurieren. Bei jeder Aktualisierung wird eine neue Version des Modells erstellt, die ab der letzten Version erhöht wird. Dadurch wird sichergestellt, dass Änderungen nachverfolgt werden und das Modell in zukünftigen Evaluierungs- oder Prognoseschritten wiederverwendet werden kann.

Das folgende Beispiel zeigt die Aktualisierung eines Modells mit neuen Transformationen und Optionen:

```sql
UPDATE MODEL <model_alias> TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features)  OPTIONS(MODEL_TYPE='logistic_reg', LABEL='churn_rate')  AS SELECT * FROM churn_with_rate ORDER BY period;
```

**Beispiel**

Der folgende Befehl hilft Ihnen, den Versionierungsprozess zu verstehen:

```sql
UPDATE MODEL model_vdqbrja OPTIONS(MODEL_TYPE='logistic_reg', LABEL='Survived') AS SELECT * FROM titanic_e2e_dnd;
```

Nach Ausführung dieses Befehls verfügt das Modell über eine neue Version, wie in der folgenden Tabelle dargestellt:

| Aktualisierte Modell-ID | Aktualisiertes Modell | Neue Version |
|--------------------------------------------|---------------|-------------|
| a8f6a254-8f28-42ec-8b26-94edeb4698e8 | model_vdqbrja | 2 |

In den folgenden Anmerkungen werden die wichtigsten Komponenten und Optionen im Workflow für die Modellaktualisierung erläutert.

- `UPDATE model <model_alias>`: Der Befehl update übernimmt die Versionierung und erstellt eine neue Modellversion, die gegenüber der letzten Version erhöht wurde.
- `version`: Ein optionales Keyword, das nur während Aktualisierungen verwendet wird, um explizit anzugeben, dass eine neue Version erstellt werden soll. Wird dies weggelassen, erhöht das System die Version automatisch.

### Anzeigen einer Vorschau und Beibehalten transformierter Funktionen {#preview-transform-output}

Verwenden Sie die `TRANSFORM`-Klausel in `CREATE TABLE`- und `CREATE TEMP TABLE`-Anweisungen, um die Ausgabe von Merkmalstransformationen vor dem Modelltraining in der Vorschau anzuzeigen und beizubehalten. Diese Verbesserung bietet Einblick in die Art und Weise, wie Umwandlungsfunktionen (wie Kodierung, Tokenisierung und Vektor-Assembler) auf Ihren Datensatz angewendet werden.

Durch Materialisierung umgewandelter Daten in eine eigenständige Tabelle können Sie Zwischenelemente untersuchen, die Verarbeitungslogik validieren und die Funktionsqualität sicherstellen, bevor Sie ein Modell erstellen. Dies verbessert die Transparenz in der gesamten Pipeline für maschinelles Lernen und unterstützt eine fundiertere Entscheidungsfindung während der Modellentwicklung.

#### Aufbau {#syntax}

Verwenden Sie die `TRANSFORM`-Klausel in einer `CREATE TABLE`- oder `CREATE TEMP TABLE`-Anweisung, wie unten dargestellt:

```sql
CREATE TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

Oder:

```sql
CREATE TEMP TABLE [IF NOT EXISTS] table_name
[WITH (tableProperties)]
TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)
AS SELECT * FROM source_table;
```

**Beispiel**

Erstellen einer Tabelle mit einfachen Transformationen:

```sql
CREATE TABLE ctas_transform_table
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review;
```

Erstellen einer temporären Tabelle mithilfe zusätzlicher Konstruktionsschritte für Funktionen:

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

Fragen Sie dann die Ausgabe ab:

```sql
SELECT * FROM ctas_transform_table LIMIT 1;
```

#### Wichtige Überlegungen {#considerations}

Diese Funktion verbessert die Transparenz und unterstützt die Funktionsüberprüfung. Es gibt jedoch wichtige Einschränkungen, die zu beachten sind, wenn die `TRANSFORM`-Klausel außerhalb der Modellerstellung verwendet wird.

- **Vektorausgaben**: Wenn die Transformation vektorähnliche Ausgaben erzeugt, werden diese automatisch in Arrays konvertiert.
- **Einschränkung der Wiederverwendung**: Tabellen, die mit `TRANSFORM` erstellt wurden, können nur während der Tabellenerstellung Umwandlungen anwenden. Neue Datenstapel, die mit `INSERT INTO` eingefügt wurden, werden **nicht automatisch transformiert**. Um dieselbe Umwandlungslogik auf neue Daten anzuwenden, müssen Sie die Tabelle mit einer New `CREATE TABLE AS SELECT` (CTAS)-Anweisung neu erstellen.
- **Beschränkung der Wiederverwendung von**: Mit `TRANSFORM` erstellte Tabellen können nicht direkt in `CREATE MODEL` Anweisungen verwendet werden. Sie müssen die `TRANSFORM` bei der Modellerstellung neu definieren. Transformationen, die Vektorausgaben erzeugen, werden beim Modell-Training nicht unterstützt. Weitere Informationen finden Sie unter [Ausgabedatentypen für die Funktionstransformation](./feature-transformation.md#available-transformations).

>[!NOTE]
>
>Diese Funktion ist für die Überprüfung und Validierung konzipiert. Sie ist kein Ersatz für wiederverwendbare Pipeline-Logik. Alle Umwandlungen, die für die Modelleingabe vorgesehen sind, müssen im Schritt zur Modellerstellung explizit neu definiert werden.

## Evaluieren von Modellen {#evaluate-model}

Um zuverlässige Ergebnisse zu gewährleisten, bewerten Sie die Genauigkeit und Effektivität des Modells, bevor Sie es für Prognosen mit dem Schlüsselwort `model_evaluate` bereitstellen. Die folgende SQL-Anweisung gibt einen Testdatensatz, bestimmte Spalten und die Modellversion an, um das Modell durch Bewertung seiner Leistung zu testen.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test_dataset)
```

Die `model_evaluate` Funktion akzeptiert `model-alias` als erstes Argument und eine flexible `SELECT` als zweites Argument. Query Service führt zunächst die `SELECT` aus und ordnet die Ergebnisse der `model_evaluate` Adobe Defined Function (ADF) zu. Das System erwartet, dass die Spaltennamen und Datentypen im Ergebnis der `SELECT`-Anweisung mit denen übereinstimmen, die im Trainings-Schritt verwendet werden. Diese Spaltennamen und Datentypen werden als Testdaten und Kennzeichnungsdaten zur Auswertung behandelt.

>[!IMPORTANT]
>
>Bei der Auswertung (`model_evaluate`) und Vorhersage (`model_predict`) werden die zum Zeitpunkt des Trainings durchgeführten Transformationen verwendet.

## Vorhersagen {#predict}

>[!IMPORTANT]
>
>Die verbesserte Spaltenauswahl und der Alias für `model_predict` werden durch ein Feature Flag gesteuert. Standardmäßig sind Zwischenfelder wie `probability` und `rawPrediction` nicht in der Prognoseausgabe enthalten.\
>Um den Zugriff auf diese Zwischenfelder zu aktivieren, führen Sie den folgenden Befehl aus, bevor Sie `model_predict` ausführen:
>
>`set advanced_statistics_show_hidden_fields=true;`

Verwenden Sie das Keyword `model_predict` , um das angegebene Modell und die angegebene Version auf einen Datensatz anzuwenden und Prognosen zu generieren. Sie können alle Ausgabespalten auswählen, bestimmte Spalten auswählen oder Aliase zuweisen, um die Ausgabeklärheit zu verbessern.

Standardmäßig werden nur Basisspalten und die endgültige Prognose zurückgegeben, es sei denn, das Feature Flag ist aktiviert.

```sql
SELECT * FROM model_predict(model-alias, version-number, SELECT col1, col2 FROM dataset);
```

### Bestimmte Ausgabefelder auswählen {#select-specific-output-fields}

Wenn das Feature Flag aktiviert ist, können Sie eine Teilmenge von Feldern aus der `model_predict` Ausgabe abrufen. Verwenden Sie diese Option, um Zwischenergebnisse wie Prognosewahrscheinlichkeiten, Rohprognosewerte und Basisspalten aus der Eingabeabfrage abzurufen.

**1. Fall: Gibt alle verfügbaren Ausgabefelder zurück**

```sql
SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**2. Fall: Gibt die ausgewählten Spalten zurück**

```sql
SELECT a, b, c, probability, predictionCol FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**3. Fall: Gibt die ausgewählten Spalten mit Aliassen zurück**

```sql
SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

In jedem Fall steuert die äußere `SELECT`, welche Ergebnisfelder zurückgegeben werden. Dazu gehören Basisfelder aus der Eingabeabfrage sowie Prognoseausgaben wie `probability`, `rawPrediction` und `predictionCol`.

### Beibehalten von Prognosen mithilfe von CREATE TABLE oder INSERT INTO

Sie können Prognosen entweder mit „CREATE TABLE AS SELECT“ oder „INSERT INTO SELECT“ beibehalten, einschließlich Prognoseausgaben bei Bedarf.

**Beispiel: Tabelle mit allen Prognoseausgabefeldern erstellen**

```sql
CREATE TABLE scored_data AS SELECT * FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

**Beispiel: Ausgewählte Ausgabefelder mit Aliassen einfügen**

```sql
INSERT INTO scored_data SELECT a, b, c, probability AS p1, predictionCol AS pdc FROM model_predict(modelName, 1, SELECT a, b, c FROM dataset);
```

Dies bietet die Flexibilität, nur die relevanten Prognoseausgabefelder und Basisspalten für nachgelagerte Analysen oder Berichte auszuwählen und beizubehalten.

## Auswerten und Verwalten von Modellen

Verwenden Sie den Befehl `SHOW MODELS` , um alle von Ihnen erstellten verfügbaren Modelle aufzulisten. Verwenden Sie diese Option, um die trainierten Modelle anzuzeigen, die zur Bewertung oder Prognose verfügbar sind. Bei der Abfrage werden die Informationen aus dem Modell-Repository abgerufen, das während der Modellerstellung aktualisiert wird. Zurückgegebene Details sind: Modell-ID, Modellname, Version, Quelldatensatz, Algorithmusdetails, Optionen/Parameter, Erstellungszeit/Aktualisierungszeit und der Benutzer, der das Modell erstellt hat.

```sql
SHOW MODELS;
```

Die Ergebnisse werden in einer ähnlichen Tabelle wie der folgenden angezeigt:

| model-id | model-name | version | source-dataset | type | Optionen | transformieren | Felder | Erstellt | Aktualisiert | Erstellt von |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1,0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`, `ohe_name`, `string_indexer(gender)`, `genderSI` | \[„Name“, „Geschlecht“\] | 14.08.2024 10:30 UHR | 14.08.2024 11:00 UHR | `JohnSnow@adobe.com` |

## Modelle bereinigen und verwalten

Verwenden Sie den Befehl `DROP MODELS` , um die von Ihnen erstellten Modelle aus der Modellregistrierung zu löschen. Sie können damit veraltete, nicht verwendete oder unerwünschte Modelle entfernen. Dadurch werden Ressourcen freigesetzt und sichergestellt, dass nur relevante Modelle gepflegt werden. Sie können auch einen optionalen Modellnamen einfügen, um die Spezifität zu verbessern. Dadurch wird nur das Modell mit der angegebenen Modellversion entfernt.

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, welche SQL-Basissyntax zum Erstellen, Trainieren und Verwalten vertrauenswürdiger Modelle mit Data Distiller erforderlich ist. Erfahren Sie als Nächstes im [Dokument Erweiterte statistische Modelle implementieren](./implement-models/implement-models.md) mehr über die verschiedenen verfügbaren vertrauenswürdigen Modelle und wie Sie sie in Ihren SQL-Workflows effektiv implementieren können. Wenn Sie dies noch nicht getan haben, stellen Sie sicher, dass Sie das Dokument [Feature Engineering](./feature-engineering.md) lesen, um sicherzustellen, dass Ihre Daten für das Modell-Training optimal vorbereitet sind.
