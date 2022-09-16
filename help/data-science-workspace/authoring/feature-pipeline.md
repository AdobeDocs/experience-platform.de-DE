---
keywords: Experience Platform; Tutorial; Feature Pipeline; Data Science Workspace; beliebte Themen
title: Erstellen einer Feature Pipeline mit dem Model Authoring SDK
topic-legacy: tutorial
type: Tutorial
description: Mit Adobe Experience Platform können Sie benutzerdefinierte Funktions-Pipelines erstellen und erstellen, um mithilfe von Sensei Machine Learning Framework Runtime Funktionen bedarfsgerecht zu entwickeln. In diesem Dokument werden die verschiedenen Klassen in einer Feature Pipeline beschrieben und ein schrittweises Tutorial zum Erstellen einer benutzerdefinierten Feature Pipeline mit dem Model Authoring SDK in PySpark bereitgestellt.
exl-id: c2c821d5-7bfb-4667-ace9-9566e6754f98
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 27%

---

# Erstellen einer Funktions-Pipeline mit dem Model Authoring SDK

>[!IMPORTANT]
>
> Feature Pipelines sind derzeit nur über API verfügbar.

Mit Adobe Experience Platform können Sie benutzerdefinierte Funktions-Pipelines erstellen und erstellen, um mithilfe der Sensei Machine Learning Framework Runtime (nachfolgend &quot;Laufzeit&quot;genannt) Funktionen bedarfsgerecht zu entwickeln.

In diesem Dokument werden die verschiedenen Klassen in einer Feature Pipeline beschrieben und ein schrittweises Tutorial zum Erstellen einer benutzerdefinierten Feature Pipeline mit dem [Model Authoring SDK](./sdk.md) in PySpark.

Der folgende Workflow erfolgt bei Ausführung einer Feature Pipeline:

1. Das Rezept lädt den Datensatz in eine Pipeline.
2. Die Merkmalumwandlung erfolgt im Datensatz und wird zurück in Adobe Experience Platform geschrieben.
3. Die umgewandelten Daten werden für das Training geladen.
4. Die Funktions-Pipeline definiert die Bühnen mit dem Gradient Boosting Regressor als ausgewähltes Modell.
5. Die Pipeline wird verwendet, um die Trainings-Daten anzupassen, und das trainierte Modell wird erstellt.
6. Das Modell wird mit dem Scoring-Datensatz transformiert.
7. Interessante Spalten der Ausgabe werden dann ausgewählt und wieder in [!DNL Experience Platform] mit den zugehörigen Daten.

## Erste Schritte

Um ein Rezept in einer Organisation auszuführen, ist Folgendes erforderlich:
- Ein Eingabedatensatz.
- Das Schema des Datensatzes.
- Ein transformiertes Schema und ein leerer Datensatz, der auf diesem Schema basiert.
- Ein Ausgabeschema und ein leerer Datensatz, der auf diesem Schema basiert.

Alle oben genannten Datensätze müssen in die [!DNL Platform] Benutzeroberfläche. Verwenden Sie dazu die bereitgestellte Adobe [Bootstrap-Skript](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap).

## Feature Pipeline-Klassen

In der folgenden Tabelle werden die wichtigsten abstrakten Klassen beschrieben, die Sie erweitern müssen, um eine Funktions-Pipeline zu erstellen:

| Abstrakte Klasse | Beschreibung |
| -------------- | ----------- |
| DataLoader | Eine DataLoader-Klasse stellt eine Implementierung zum Abrufen von Eingabedaten bereit. |
| DatasetTransformer | Eine DatasetTransformer-Klasse stellt Implementierungen zum Transformieren des Eingabedatasets bereit. Sie können festlegen, dass keine DatasetTransformer-Klasse bereitgestellt und Ihre Funktionstechnik stattdessen in die FeaturePipelineFactory-Klasse implementiert werden soll. |
| FeaturePipelineFactory | Eine FeaturePipelineFactory-Klasse erstellt eine Spark-Pipeline, die aus einer Reihe von Spark-Transformatoren besteht, um Funktions-Engineering durchzuführen. Sie können festlegen, dass keine FeaturePipelineFactory-Klasse bereitgestellt und Ihr Funktions-Engineering stattdessen in die DatasetTransformer-Klasse implementiert wird. |
| DataSaver | Eine DataSaver-Klasse stellt die Logik für die Datenspeicherung eines Funktionsdatensatzes bereit. |

Wenn ein Feature Pipeline-Auftrag initiiert wird, führt Runtime zunächst den DataLoader aus, um Eingabedaten als DataFrame zu laden, und ändert dann den DataFrame, indem entweder DatasetTransformer, FeaturePipelineFactory oder beide ausgeführt werden. Schließlich wird der sich ergebende Funktionsdatensatz über den DataSaver gespeichert.

Das folgende Flussdiagramm zeigt die Ausführungsreihenfolge der Laufzeitumgebung:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implementieren Ihrer Feature Pipeline-Klassen {#implement-your-feature-pipeline-classes}

Die folgenden Abschnitte enthalten Details und Beispiele zur Implementierung der erforderlichen Klassen für eine Feature Pipeline.

### Definieren der Variablen in der JSON-Konfigurationsdatei {#define-variables-in-the-configuration-json-file}

Die JSON-Konfigurationsdatei besteht aus Schlüsselwert-Paaren und dient zum Angeben von Variablen, die später während der Laufzeit definiert werden sollen. Diese Schlüsselwert-Paare können Eigenschaften wie den Speicherort des Eingabedatasets, die ID des Ausgabedatasets, die Mandanten-ID, Spaltenüberschriften usw. definieren.

Das folgende Beispiel zeigt Schlüssel-Wert-Paare, die in einer Konfigurationsdatei gefunden werden:

**Beispiel für JSON-Konfiguration**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "dataset_id",
                "value": "000"
            },
            {
                "key": "featureDatasetId",
                "value": "111"
            },
            {
                "key": "tenantId",
                "value": "_tenantid"
            }
        ]
    }
]
```

Sie können auf die Konfigurations-JSON über jede Klassenmethode zugreifen, die `config_properties` als Parameter definiert. Beispiel:

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

Siehe [pipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) -Datei von Data Science Workspace für ein detaillierteres Konfigurationsbeispiel bereitgestellt.

### Vorbereiten der Eingabedaten mit DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader ist für das Abrufen und Filtern von Eingabedaten zuständig. Ihre Implementierung von DataLoader muss die abstrakte Klasse `DataLoader` erweitern und die abstrakte Methode `load` überschreiben.

Im folgenden Beispiel wird eine [!DNL Platform] Datensatz nach ID und gibt ihn als DataFrame zurück, wobei die Datensatz-ID (`dataset_id`) ist eine definierte Eigenschaft in der Konfigurationsdatei.

**PySpark-Beispiel**

```python
# PySpark

from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
import logging

class MyDataLoader(DataLoader):
    def load_dataset(config_properties, spark, tenant_id, dataset_id):
    PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
    PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

    service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
    user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
    org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
    api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

    dataset_id = str(config_properties.get(dataset_id))

    for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
        if eval(arg) == 'None':
            raise ValueError("%s is empty" % arg)

    query_options = get_query_options(spark.sparkContext)

    pd = spark.read.format(PLATFORM_SDK_PQS_PACKAGE) \
        .option(query_options.userToken(), user_token) \
        .option(query_options.serviceToken(), service_token) \
        .option(query_options.imsOrg(), org_id) \
        .option(query_options.apiKey(), api_key) \
        .option(query_options.mode(), PLATFORM_SDK_PQS_INTERACTIVE) \
        .option(query_options.datasetId(), dataset_id) \
        .load()
    pd.show()

    # Get the distinct values of the dataframe
    pd = pd.distinct()

    # Flatten the data
    if tenant_id in pd.columns:
        pd = pd.select(col(tenant_id + ".*"))

    return pd
```

### Transformieren eines Datensatzes mit DatasetTransformer {#transform-a-dataset-with-datasettransformer}

Ein DatasetTransformer stellt die Logik zum Transformieren eines Eingangs-DataFrames bereit und gibt einen neuen abgeleiteten DataFrame zurück. Diese Klasse kann implementiert werden, um entweder gemeinsam mit einer FeaturePipelineFactory zu arbeiten, als einzige Funktions-Engineering-Komponente zu arbeiten, oder Sie können festlegen, dass diese Klasse nicht implementiert wird.

Im folgenden Beispiel wird die DatasetTransformer-Klasse erweitert:

**PySpark-Beispiel**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer
from pyspark.ml.feature import StringIndexer
from pyspark.sql.types import IntegerType
from pyspark.sql.functions import unix_timestamp, from_unixtime, to_date, lit, lag, udf, date_format, lower, col, split, explode
from pyspark.sql import Window
from .helper import setupLogger

class MyDatasetTransformer(DatasetTransformer):
    logger = setupLogger(__name__)

    def transform(self, config_properties, dataset):
        tenant_id = str(config_properties.get("tenantId"))

        # Flatten the data
        if tenant_id in dataset.columns:
            self.logger.info("Flatten the data before transformation")
            dataset = dataset.select(col(tenant_id + ".*"))
            dataset.show()

        # Convert isHoliday boolean value to Int
        # Rename the column to holiday and drop isHoliday
        pd = dataset.withColumn("holiday", col("isHoliday").cast(IntegerType())).drop("isHoliday")
        pd.show()

        # Get the week and year from date
        pd = pd.withColumn("week", date_format(to_date("date", "MM/dd/yy"), "w").cast(IntegerType()))
        pd = pd.withColumn("year", date_format(to_date("date", "MM/dd/yy"), "Y").cast(IntegerType()))

        # Convert the date to TimestampType
        pd = pd.withColumn("date", to_date(unix_timestamp(pd["date"], "MM/dd/yy").cast("timestamp")))

        # Convert categorical data
        indexer = StringIndexer(inputCol="storeType", outputCol="storeTypeIndex")
        pd = indexer.fit(pd).transform(pd)

        # Get the WeeklySalesAhead and WeeklySalesLag column values
        window = Window.orderBy("date").partitionBy("store")
        pd = pd.withColumn("weeklySalesLag", lag("weeklySales", 1).over(window)).na.drop(subset=["weeklySalesLag"])
        pd = pd.withColumn("weeklySalesAhead", lag("weeklySales", -1).over(window)).na.drop(subset=["weeklySalesAhead"])
        pd = pd.withColumn("weeklySalesScaled", lag("weeklySalesAhead", -1).over(window)).na.drop(subset=["weeklySalesScaled"])
        pd = pd.withColumn("weeklySalesDiff", (pd['weeklySales'] - pd['weeklySalesLag'])/pd['weeklySalesLag'])

        pd = pd.na.drop()
        self.logger.debug("Transformed dataset count is %s " % pd.count())

        # return transformed dataframe
        return pd
```

### Engineering von Datenfunktionen mit FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

Mit einer FeaturePipelineFactory können Sie Ihre Funktions-Engineering-Logik implementieren, indem Sie eine Reihe von Spark-Transformatoren über eine Spark-Pipeline definieren und verketten. Diese Klasse kann implementiert werden, um entweder mit einem DatasetTransformer zusammenzuarbeiten, als einzige Komponente der Funktions-Engineering-Komponente zu arbeiten, oder Sie können festlegen, dass diese Klasse nicht implementiert wird.

Im folgenden Beispiel wird die FeaturePipelineFactory -Klasse erweitert:

**PySpark-Beispiel**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.regression import GBTRegressor
from pyspark.ml.feature import VectorAssembler

import numpy as np

from sdk.pipeline_factory import PipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def apply(self, config_properties):
        if config_properties is None:
            raise ValueError("config_properties parameter is null")

        tenant_id = str(config_properties.get("tenantId"))
        input_features = str(config_properties.get("ACP_DSW_INPUT_FEATURES"))

        if input_features is None:
            raise ValueError("input_features parameter is null")
        if input_features.startswith(tenant_id):
            input_features = input_features.replace(tenant_id + ".", "")

        learning_rate = float(config_properties.get("learning_rate"))
        n_estimators = int(config_properties.get("n_estimators"))
        max_depth = int(config_properties.get("max_depth"))

        feature_list = list(input_features.split(","))
        feature_list.remove("date")
        feature_list.remove("storeType")

        cols = np.array(feature_list)

        # Gradient-boosted tree estimator
        gbt = GBTRegressor(featuresCol='features', labelCol='weeklySalesAhead', predictionCol='prediction',
                       maxDepth=max_depth, maxBins=n_estimators, stepSize=learning_rate)

        # Assemble the fields to a vector
        assembler = VectorAssembler(inputCols=cols, outputCol="features")

        # Construct the pipeline
        pipeline = Pipeline(stages=[assembler, gbt])

        return pipeline

    def train(self, config_properties, dataframe):
        pass

    def score(self, config_properties, dataframe, model):
        pass

    def getParamMap(self, config_properties, sparkSession):
        return None
```

### Speichern Sie Ihren Funktionsdatensatz mit DataSaver {#store-your-feature-dataset-with-datasaver}

Der DataSaver ist für die Speicherung Ihrer resultierenden Funktionsdatensätze an einem Speicherort verantwortlich. Ihre Implementierung von DataSaver muss die abstrakte Klasse `DataSaver` erweitern und die abstrakte Methode `save` überschreiben.

Im folgenden Beispiel wird die DataSaver-Klasse erweitert, in der Daten in einer [!DNL Platform] Datensatz nach ID, wobei die Datensatz-ID (`featureDatasetId`) und Mandanten-ID (`tenantId`) sind definierte Eigenschaften in der Konfiguration.

**PySpark-Beispiel**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct


class MyDataSaver(DataSaver):
    def save(self, configProperties, data_feature):

        # Spark context
        sparkContext = data_features._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if data_features is None:
            raise ValueError("data_features parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("featureDatasetId"))
        tenant_id = str(
            configProperties.get("tenantId"))
        service_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['output_dataset_id', 'tenant_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # create and prepare DataFrame with valid columns
        output_df = data_features.withColumn("date", col("date").cast(StringType()))
        output_df = output_df.withColumn(tenant_id, struct(col("date"), col("store"), col("features")))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        # store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp") \
            .write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```


### Geben Sie Ihre implementierten Klassennamen in der Anwendungsdatei an {#specify-your-implemented-class-names-in-the-application-file}

Nachdem Sie Ihre Feature Pipeline-Klassen definiert und implementiert haben, müssen Sie die Namen Ihrer Klassen in der YAML-Anwendungsdatei angeben.

Die folgenden Beispiele geben implementierte Klassennamen an:

**PySpark-Beispiel**

```yaml
#Name of the class which contains implementation to get the input data.
feature.dataLoader: InputDataLoaderForFeaturePipeline

#Name of the class which contains implementation to get the transformed data.
feature.dataset.transformer: MyDatasetTransformer

#Name of the class which contains implementation to save the transformed data.
feature.dataSaver: DatasetSaverForTransformedData

#Name of the class which contains implementation to get the training data
training.dataLoader: TrainingDataLoader

#Name of the class which contains pipeline. It should implement PipelineFactory.scala
pipeline.class: TrainPipeline

#Name of the class which contains implementation for evaluation metrics.
evaluator: Evaluator
evaluateModel: True

#Name of the class which contains implementation to get the scoring data.
scoring.dataLoader: ScoringDataLoader

#Name of the class which contains implementation to save the scoring data.
scoring.dataSaver: MyDatasetSaver
```

## Erstellen der Funktions-Pipeline-Engine mit der API {#create-feature-pipeline-engine-api}

Nachdem Sie Ihre Funktions-Pipeline erstellt haben, müssen Sie ein Docker-Bild erstellen, um die Funktions-Pipeline-Endpunkte im [!DNL Sensei Machine Learning] API. Sie benötigen eine Docker-Bild-URL, um die Endpunkte der Feature Pipeline aufrufen zu können.

>[!TIP]
>
>Wenn Sie keine Docker-URL haben, besuchen Sie die [Quelldateien in einem Rezept verpacken](../models-recipes/package-source-files-recipe.md) Tutorial für eine schrittweise Anleitung zum Erstellen einer Docker-Host-URL.

Optional können Sie auch die folgende Postman-Sammlung verwenden, um den Funktions-Pipeline-API-Workflow abzuschließen:

https://www.postman.com/collections/c5fc0d1d5805a5ddd41a

### Erstellen einer Funktions-Pipeline-Engine {#create-engine-api}

Sobald Sie Ihren Docker-Image-Speicherort haben, können Sie [Erstellen einer Funktions-Pipeline-Engine](../api/engines.md#feature-pipeline-docker) mithilfe der [!DNL Sensei Machine Learning] API durch Ausführen einer POST zu `/engines`. Durch das erfolgreiche Erstellen einer Feature Pipeline-Engine erhalten Sie eine eindeutige Engine-Kennung (`id`). Achten Sie darauf, diesen Wert zu speichern, bevor Sie fortfahren.

### Erstellen einer MLInstance {#create-mlinstance}

Verwenden von neu erstellten `engineID`, müssen Sie [Erstellen einer MLIstance](../api/mlinstances.md#create-an-mlinstance) , indem Sie eine POST-Anfrage an die `/mlInstance` -Endpunkt. Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details der neu erstellten MLInstance einschließlich ihrer eindeutigen Kennung (`id`), die im nächsten API-Aufruf verwendet wird.

### Erstellen eines Experiments {#create-experiment}

Als Nächstes müssen Sie [Erstellen eines Experiments](../api/experiments.md#create-an-experiment). Um ein Experiment zu erstellen, benötigen Sie eine eindeutige MLIstance-Kennung (`id`) und stellen Sie eine POST-Anfrage an die `/experiment` -Endpunkt. Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details des neu erstellten Experiments einschließlich der eindeutigen Kennung (`id`), die im nächsten API-Aufruf verwendet wird.

### Geben Sie die Pipeline-Aufgabe für die Experimentablauf-Funktion an {#specify-feature-pipeline-task}

Nach dem Erstellen eines Experiments müssen Sie den Modus des Experiments in `featurePipeline`. Um den Modus zu ändern, nehmen Sie eine zusätzliche POST zu [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) mit `EXPERIMENT_ID` und im Versand `{ "mode":"featurePipeline"}` um einen Funktions-Pipeline-Experimentablauf anzugeben.

Stellen Sie nach dem Abschluss eine GET-Anfrage an `/experiments/{EXPERIMENT_ID}` nach [den Experimentstatus abrufen](../api/experiments.md#retrieve-specific) und warten Sie, bis der Experimentstatus aktualisiert wurde.

### Festlegen der Trainings-Aufgabe für die Experimentausführung {#training}

Als Nächstes müssen Sie [die Aufgabe für die Schulungsausführung festlegen](../api/experiments.md#experiment-training-scoring). Nehmen Sie eine POST vor zu `experiments/{EXPERIMENT_ID}/runs` und legen Sie im Hauptteil den Modus auf `train` und senden Sie eine Reihe von Aufgaben, die Ihre Trainings-Parameter enthalten. Eine erfolgreiche Antwort gibt eine Payload zurück, die die Details des angeforderten Experiments enthält.

Stellen Sie nach dem Abschluss eine GET-Anfrage an `/experiments/{EXPERIMENT_ID}` nach [den Experimentstatus abrufen](../api/experiments.md#retrieve-specific) und warten Sie, bis der Experimentstatus aktualisiert wurde.

### Festlegen der Scoring-Aufgabe für Experimentabläufe {#scoring}

>[!NOTE]
>
> Um diesen Schritt abzuschließen, muss Ihrem Experiment mindestens ein erfolgreicher Trainings-Lauf zugeordnet sein.

Nach einem erfolgreichen Trainings-Lauf müssen Sie [Scoring-Lauf-Aufgabe angeben](../api/experiments.md#experiment-training-scoring). Nehmen Sie eine POST vor zu `experiments/{EXPERIMENT_ID}/runs` und legen Sie im Hauptteil die `mode` auf &quot;score&quot;gesetzt. Dadurch wird Ihr Auswertungs-Experimentablauf gestartet.

Stellen Sie nach dem Abschluss eine GET-Anfrage an `/experiments/{EXPERIMENT_ID}` nach [den Experimentstatus abrufen](../api/experiments.md#retrieve-specific) und warten Sie, bis der Experimentstatus aktualisiert wurde.

Sobald die Auswertung abgeschlossen ist, sollte Ihre Feature Pipeline betriebsbereit sein.

## Nächste Schritte {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

Durch Lesen dieses Dokuments haben Sie eine Funktions-Pipeline mit dem Model Authoring SDK erstellt, ein Docker-Bild erstellt und die Docker-Bild-URL verwendet, um ein Feature-Pipeline-Modell mithilfe der [!DNL Sensei Machine Learning] API. Sie sind jetzt bereit, mit der Transformation von Datensätzen und dem Extrahieren von Datenfunktionen im Maßstab mit dem [[!DNL Sensei Machine Learning API]](../api/getting-started.md).
