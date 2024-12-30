---
title: Modelle
description: Modell-Lebenszyklusverwaltung mit der Data Distiller SQL-Erweiterung. Erfahren Sie, wie Sie erweiterte statistische Modelle mithilfe von SQL erstellen, trainieren und verwalten, einschließlich wichtiger Prozesse wie Modellversionierung, -auswertung und -vorhersage, um aus Ihren Daten umsetzbare Einblicke zu gewinnen.
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 6a61900b19543f110c47e30f4d321d0016b65262
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 1%

---

# Modelle

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Add-on Data Distiller erworben haben. Weitere Informationen erhalten Sie bei Ihrer bzw. Ihrem Adobe-Support-Mitarbeitenden.

Query Service unterstützt jetzt die Kernprozesse des Erstellens und Bereitstellens eines Modells. Sie können SQL verwenden, um das Modell mithilfe Ihrer Daten zu trainieren, seine Genauigkeit zu bewerten und dann ein Trainingsmodell anzuwenden, um Vorhersagen für neue Daten zu treffen. Anschließend können Sie das Modell verwenden, um aus Ihren früheren Daten zu generalisieren und fundierte Entscheidungen über reale Szenarien zu treffen.

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


## Evaluieren von Modellen {#evaluate-model}

Um zuverlässige Ergebnisse zu gewährleisten, bewerten Sie die Genauigkeit und Effektivität des Modells, bevor Sie es für Prognosen mit dem Schlüsselwort `model_evaluate` bereitstellen. Die folgende SQL-Anweisung gibt einen Testdatensatz, bestimmte Spalten und die Modellversion an, um das Modell durch Bewertung seiner Leistung zu testen.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

Die `model_evaluate` Funktion akzeptiert `model-alias` als erstes Argument und eine flexible `SELECT` als zweites Argument. Query Service führt zunächst die `SELECT` aus und ordnet die Ergebnisse der `model_evaluate` Adobe Defined Function (ADF) zu. Das System erwartet, dass die Spaltennamen und Datentypen im Ergebnis der `SELECT`-Anweisung mit denen übereinstimmen, die im Trainings-Schritt verwendet werden. Diese Spaltennamen und Datentypen werden als Testdaten und Kennzeichnungsdaten zur Auswertung behandelt.

>[!IMPORTANT]
>
>Bei der Auswertung (`model_evaluate`) und Vorhersage (`model_predict`) werden die zum Zeitpunkt des Trainings durchgeführten Transformationen verwendet.

## Vorhersagen {#predict}

Verwenden Sie anschließend das Keyword `model_predict` , um das angegebene Modell und die angegebene Version auf einen Datensatz anzuwenden und Prognosen für die ausgewählten Spalten zu generieren. Die folgende SQL-Anweisung zeigt diesen Prozess und zeigt, wie mithilfe des Alias und der Version des Modells Ergebnisse prognostiziert werden können.

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict` akzeptiert als erstes Argument den Modellalias und als zweites Argument eine flexible `SELECT`. Query Service führt zunächst die `SELECT` aus und ordnet die Ergebnisse dem `model_predict` ADF zu. Das System erwartet, dass die Spaltennamen und Datentypen im Ergebnis der `SELECT`-Anweisung mit denen aus dem Trainings-Schritt übereinstimmen. Diese Daten werden dann für die Bewertung und Erstellung von Prognosen verwendet.

>[!IMPORTANT]
>
>Bei der Auswertung (`model_evaluate`) und Vorhersage (`model_predict`) werden die zum Zeitpunkt des Trainings durchgeführten Transformationen verwendet.

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
