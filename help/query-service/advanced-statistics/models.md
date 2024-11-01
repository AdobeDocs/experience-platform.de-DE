---
title: Modelle
description: Modelllebenszyklusverwaltung mit der Data Distiller SQL-Erweiterung. Erfahren Sie, wie Sie mithilfe von SQL erweiterte statistische Modelle erstellen, trainieren und verwalten, einschließlich wichtiger Prozesse wie Modellversionierung, -auswertung und -vorhersage, um aus Ihren Daten verwertbare Einblicke abzuleiten.
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 1%

---

# Modelle

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Data Distiller-Add-on erworben haben. Weitere Informationen erhalten Sie beim Adobe-Support.

Query Service unterstützt jetzt die Kernprozesse beim Erstellen und Bereitstellen eines Modells. Sie können SQL verwenden, um das Modell mithilfe Ihrer Daten zu trainieren, seine Genauigkeit zu bewerten und dann das Zugmodell anzuwenden, um Prognosen zu neuen Daten zu erstellen. Anschließend können Sie das Modell verwenden, um aus Ihren bisherigen Daten fundierte Entscheidungen über reale Szenarien zu treffen.

Die drei Schritte im Modelllebenszyklus zum Generieren umsetzbarer Einblicke sind:

1. **Training**: Das Modell lernt Muster aus dem bereitgestellten Datensatz. (Modell erstellen oder ersetzen)
2. **Testen/Testen**: Die Leistung des Modells wird mithilfe eines separaten Datensatzes bewertet. (`model_evaluate`)
3. **Prognose**: Das trainierte Modell wird verwendet, um Prognosen zu neuen, nicht sichtbaren Daten zu erstellen.

Verwenden Sie die zur vorhandenen SQL-Grammatik hinzugefügte SQL-Modellerweiterung, um den Lebenszyklus des Modells entsprechend Ihren Geschäftsanforderungen zu verwalten. In diesem Dokument wird die SQL behandelt, die zum Erstellen oder Ersetzen eines Modells, zum Trainieren, Auswerten, gegebenenfalls Neutrainieren und Vorhersagen von Einblicken erforderlich ist.

## Modellerstellung und -schulung {#create-and-train}

Erfahren Sie, wie Sie ein Modell für maschinelles Lernen mit SQL-Befehlen definieren, konfigurieren und trainieren. Die folgende SQL-Anleitung zeigt, wie Sie ein Modell erstellen, Funktionsumwandlungen anwenden und den Trainings-Prozess starten, um sicherzustellen, dass das Modell für die zukünftige Verwendung richtig konfiguriert ist. Die folgenden SQL-Befehle beschreiben verschiedene Optionen für die Modellerstellung und -verwaltung:

- **MODELL ERSTELLEN**: Erstellt und trainiert ein neues Modell in einem angegebenen Datensatz. Wenn bereits ein Modell mit demselben Namen vorhanden ist, gibt dieser Befehl einen Fehler zurück.
- **MODELL ERSTELLEN WENN NICHT VORHANDEN IST**: Erstellt und trainiert ein neues Modell nur dann, wenn ein Modell mit demselben Namen nicht bereits im angegebenen Datensatz vorhanden ist.
- **MODELL ERSTELLEN ODER ERSETZEN**: Erstellt und trainiert ein Modell, wobei die neueste Version eines vorhandenen Modells durch denselben Namen im angegebenen Datensatz ersetzt wird.

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

Um Ihnen zu helfen, die Schlüsselkomponenten und Konfigurationen im Prozess der Modellerstellung und -schulung zu verstehen, erläutern die folgenden Hinweise den Zweck und die Funktion jedes Elements im obigen SQL-Beispiel.

- `<model_alias>`: Der Modellalias ist ein wiederverwendbarer Name, der dem Modell zugewiesen ist und später referenziert werden kann. Sie müssen Ihrem Modell einen Namen geben.
- `transform`: Die Transformationsklausel wird verwendet, um Funktions-Engineering-Transformationen (z. B. einmalige Kodierung und Zeichenfolgenindizierung) auf den Datensatz anzuwenden, bevor das Modell trainiert wird. Der letzte Satz der `TRANSFORM` -Anweisung sollte entweder ein `vector_assembler` mit einer Liste von Spalten sein, aus denen die Funktionen für die Modellschulung bestehen würden, oder ein abgeleiteter Typ des `vector_assembler` (z. B. `max_abs_scaler(feature)`, `standard_scaler(feature)` usw.). Nur die im letzten Satz genannten Spalten werden für die Schulung verwendet. Alle anderen Spalten, auch wenn sie in der `SELECT` -Abfrage enthalten sind, werden ausgeschlossen.
- `label = <label-COLUMN>`: Die Titelspalte im Trainings-Datensatz, die das Ziel oder das Ergebnis angibt, das das Modell vorhersagen soll.
- `training-dataset`: Diese Syntax wählt die Daten aus, die zum Trainieren des Modells verwendet werden.
- `type = 'LogisticRegression'`: Diese Syntax gibt die Art des zu verwendenden maschinellen Lernalgorithmus an. Zu den Optionen gehören `LinearRegression`, `LogisticRegression` und `KMeans`.
- `options`: Dieses Keyword bietet einen flexiblen Satz von Schlüssel-Wert-Paaren zum Konfigurieren des Modells.
   - `Key model_type`: `model_type = '<supported algorithm>'`: Gibt den Typ des zu verwendenden maschinellen Lernalgorithmus an. Zu den unterstützten Optionen gehören `LinearRegression`, `LogisticRegression` und `KMeans`.
   - `Key label`: `label = <label_COLUMN>`: Definiert die Titelspalte im Trainings-Datensatz, die das Ziel oder das Ergebnis angibt, das das Modell vorhersagen möchte.

Verwenden Sie SQL, um auf den für das Training verwendeten Datensatz zu verweisen.

## Modell aktualisieren {#update}

Erfahren Sie, wie Sie ein vorhandenes Modell für maschinelles Lernen aktualisieren können, indem Sie neue Funktionsumwandlungen anwenden und Optionen wie den Algorithmustyp und die Beschriftungsspalte konfigurieren. Die folgende SQL-Anleitung zeigt, wie Sie die Versionsnummer des Modells bei jeder Aktualisierung erhöhen und sicherstellen, dass Änderungen verfolgt werden, damit das Modell in zukünftigen Evaluierungs- oder Prognoseschritten wiederverwendet werden kann.

```sql
UPDATE model <model_alias> transform( one_hot_encoder(NAME) ohe_name, string_indexer(gender) gendersi) options ( type = 'LogisticRegression', label = <label-COLUMN>, ) ASSELECT col1,
       col2,
       col3
FROM   training-dataset.
```

Um Ihnen zu vermitteln, wie Sie Modellversionen verwalten und Umwandlungen effektiv anwenden können, werden in den folgenden Abschnitten die wichtigsten Komponenten und Optionen im Workflow für die Modellaktualisierung erläutert.

- `UPDATE model <model_alias>`: Der Aktualisierungsbefehl verarbeitet die Versionierung und erhöht bei jeder Aktualisierung die Versionsnummer des Modells.
- `version`: Ein optionales Keyword, das nur bei Aktualisierungen zum Erstellen einer neuen Version des Modells verwendet wird.

## Modelle auswerten {#evaluate-model}

Um zuverlässige Ergebnisse zu gewährleisten, bewerten Sie die Genauigkeit und Effektivität des Modells, bevor Sie es für Prognosen mit dem Schlüsselwort `model_evaluate` bereitstellen. Die folgende SQL-Anweisung gibt einen Testdatensatz, bestimmte Spalten und die Version des Modells an, um das Modell durch Bewertung seiner Leistung zu testen.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

Die Funktion `model_evaluate` verwendet `model-alias` als erstes Argument und eine flexible `SELECT` -Anweisung als zweites Argument. Query Service führt zuerst die Anweisung `SELECT` aus und ordnet die Ergebnisse der Adobe Defined Function (ADF) von `model_evaluate` zu. Das System erwartet, dass die Spaltennamen und Datentypen im Ergebnis der `SELECT` -Anweisung mit den im Trainings-Schritt verwendeten übereinstimmen. Diese Spaltennamen und Datentypen werden als Testdaten und Bezeichnungsdaten für die Auswertung behandelt.

>[!IMPORTANT]
>
>Bei der Auswertung (`model_evaluate`) und Vorhersage (`model_predict`) werden die zum Zeitpunkt der Schulung durchgeführten Umwandlungen verwendet.

## Vorhersagen {#predict}

Verwenden Sie als Nächstes das Schlüsselwort `model_predict` , um das angegebene Modell und die angegebene Version auf einen Datensatz anzuwenden und Prognosen für die ausgewählten Spalten zu generieren. Die folgende SQL-Anleitung zeigt diesen Prozess und zeigt, wie Ergebnisse mithilfe des Alias und der Version des Modells prognostiziert werden.

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict` akzeptiert den Modellalias als erstes Argument und eine flexible `SELECT` -Anweisung als zweites Argument. Query Service führt zuerst die Anweisung `SELECT` aus und ordnet die Ergebnisse der ADF `model_predict` zu. Das System erwartet, dass die Spaltennamen und Datentypen im Ergebnis der `SELECT` -Anweisung mit denen des Trainings-Schritts übereinstimmen. Diese Daten werden dann für die Auswertung und Generierung von Prognosen verwendet.

>[!IMPORTANT]
>
>Bei der Auswertung (`model_evaluate`) und Vorhersage (`model_predict`) werden die zum Zeitpunkt der Schulung durchgeführten Umwandlungen verwendet.

## Bewerten und Verwalten Ihrer Modelle

Verwenden Sie den Befehl `SHOW MODELS` , um alle verfügbaren Modelle aufzulisten, die Sie erstellt haben. Verwenden Sie sie, um die trainierten Modelle anzuzeigen, die für die Auswertung oder Vorhersage verfügbar sind. Bei der Abfrage werden die Informationen aus dem Modell-Repository abgerufen, das bei der Modellerstellung aktualisiert wird. Die zurückgegebenen Details sind: Modell-ID, Modellname, Version, Quelldatensatz, Algorithmusdetails, Optionen/Parameter, Erstellungs-/Aktualisierungszeit und der Benutzer, der das Modell erstellt hat.

```sql
SHOW MODELS;
```

Die Ergebnisse werden in einer Tabelle angezeigt, die der folgenden ähnelt:

| model-id | model-name | version | source-dataset | type | options | transformieren | fields | Erstellt | aktualisiert | ERSTELLT VON |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1,0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`, `ohe_name`, `string_indexer(gender)`, `genderSI` | \[&quot;name&quot;, &quot;gender&quot;\] | 2024-08-14 10:30 Uhr | 14.08.2024 11:00 Uhr | `JohnSnow@adobe.com` |

## Ihre Modelle bereinigen und verwalten

Verwenden Sie den Befehl `DROP MODELS` , um die von Ihnen erstellten Modelle aus der Modellregistrierung zu löschen. Sie können damit veraltete, nicht verwendete oder unerwünschte Modelle entfernen. Dadurch werden Ressourcen freigesetzt und sichergestellt, dass nur relevante Modelle beibehalten werden. Sie können auch einen optionalen Modellnamen für eine verbesserte Spezifität einfügen. Dadurch wird nur das Modell mit der bereitgestellten Modellversion entfernt.

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## Nächste Schritte

Nachdem Sie dieses Dokument gelesen haben, verstehen Sie jetzt die grundlegende SQL-Syntax, die zum Erstellen, Trainieren und Verwalten vertrauenswürdiger Modelle mit Data Distiller erforderlich ist. Sehen Sie sich als Nächstes das Dokument [Erweiterte statistische Modelle implementieren](./implement-models/implement-models.md) an, um mehr über die verschiedenen verfügbaren vertrauenswürdigen Modelle zu erfahren und zu erfahren, wie Sie sie effektiv in Ihren SQL-Workflows implementieren können. Wenn Sie dies noch nicht getan haben, überprüfen Sie das Dokument [Funktionsentwicklung](./feature-engineering.md) , um sicherzustellen, dass Ihre Daten optimal auf das Modell-Training vorbereitet sind.
