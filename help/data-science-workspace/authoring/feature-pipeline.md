---
keywords: Experience Platform;Tutorial;feature pipeline;Data Science Workspace;popular topics
solution: Adobe Experience Platform Data Science Workspace
title: Erstellen einer Feature-Pipeline
topic: Tutorial
translation-type: tm+mt
source-git-commit: 20e26c874204da75cac7e8d001770702658053f1
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---


# Erstellen einer Feature-Pipeline

>[!IMPORTANT]
> Funktionserweiterungen sind derzeit nur über API verfügbar.

Mit der Adobe Experience Platform können Sie benutzerdefinierte Funktionenpipelines erstellen und erstellen, um die Funktionstechnik im Maßstab über die Sensei Machine Learning Framework Runtime (im Folgenden &quot;Laufzeit&quot; genannt) durchzuführen.

Dieses Dokument beschreibt die verschiedenen Klassen, die in einer Feature-Pipeline gefunden wurden, und bietet eine schrittweise Anleitung zum Erstellen einer benutzerdefinierten Feature-Pipeline mit dem [Model Authoring-SDK](./sdk.md) in PySpark.

Der folgende Arbeitsablauf findet statt, wenn eine Feature-Pipeline ausgeführt wird:

1. Das Rezept lädt den Datensatz in eine Pipeline.
2. Die Merkmalumwandlung erfolgt im Datensatz und wird in die Adobe Experience Platform zurückgeschrieben.
3. Die transformierten Daten werden zur Schulung geladen.
4. Die Feature-Pipeline definiert die Schritte mit dem Verlaufsverstärkungs-Regressor als ausgewähltes Modell.
5. Die Pipeline wird verwendet, um die Schulungsdaten anzupassen und das geschulte Modell wird erstellt.
6. Das Modell wird mit dem Bewertungsdatensatz transformiert.
7. Interessante Spalten der Ausgabe werden dann ausgewählt und mit [!DNL Experience Platform] den zugehörigen Daten gespeichert.

## Erste Schritte

Um ein Rezept in einem Unternehmen auszuführen, ist Folgendes erforderlich:
- Ein Eingabedataset.
- Das Schema des Datensatzes.
- Ein transformiertes Schema und ein leerer Datensatz, der auf diesem Schema basiert.
- Ein Output-Schema und ein leerer Datensatz, der auf diesem Schema basiert.

Alle oben genannten Datensätze müssen in die [!DNL Platform] Benutzeroberfläche hochgeladen werden. Verwenden Sie dazu das von Adobe bereitgestellte [Bootstrap-Skript](https://github.com/adobe/experience-platform-dsw-reference/tree/master/bootstrap).

## Funktionsbereitstellungsklassen

Die folgende Tabelle beschreibt die wichtigsten abstrakten Klassen, die Sie erweitern müssen, um eine Feature-Pipeline zu erstellen:

| Abstrakte Klasse | Beschreibung |
| -------------- | ----------- |
| DataLoader | Eine DataLoader-Klasse stellt eine Implementierung zum Abrufen von Eingabedaten bereit. |
| DatasetTransformer | Eine DataSetTransformer-Klasse stellt Implementierungen zum Transformieren des Eingabedatasets bereit. Sie können festlegen, dass keine DataSetTransformer-Klasse bereitgestellt und Ihre Funktionstechnik stattdessen in die FeaturePipelineFactory-Klasse implementiert werden soll. |
| FeaturePipelineFactory | Eine FeaturePipelineFactory-Klasse erstellt eine Spark-Pipeline, die aus einer Reihe von Spark-Transformatoren besteht, um die Funktionstechnik durchzuführen. Sie können festlegen, dass keine FeaturePipelineFactory-Klasse bereitgestellt und Ihre Funktionstechnik stattdessen in die DatasetTransformer-Klasse implementiert wird. |
| DataSaver | Eine DataSaver-Klasse stellt die Logik für die Datenspeicherung eines Funktionsdatasets bereit. |

Wenn ein Funktionspipelineauftrag initiiert wird, führt die Laufzeitumgebung zunächst den DataLoader aus, um Eingabedaten als DataFrame zu laden, und ändert dann den DataFrame, indem entweder DataTransformer, FeaturePipelineFactory oder beides ausgeführt wird. Schließlich wird der sich ergebende Funktionsdatensatz über den DataSaver gespeichert.

Das folgende Flussdiagramm zeigt die Ausführungsreihenfolge der Laufzeitumgebung:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implementieren von Funktionen in Pipeline-Klassen {#implement-your-feature-pipeline-classes}

Die folgenden Abschnitte enthalten Details und Beispiele zur Implementierung der erforderlichen Klassen für eine Feature Pipeline.

### Variablen in der JSON-Konfigurationsdatei definieren {#define-variables-in-the-configuration-json-file}

Die JSON-Konfigurationsdatei besteht aus Schlüssel-Wert-Paaren und dient zum Angeben von Variablen, die später während der Laufzeit definiert werden sollen. Diese Schlüssel-Wert-Paare können Eigenschaften wie den Speicherort des Eingabedatasets, die ID des Ausgabedatasets, die Mandant-ID, Spaltenköpfe usw. definieren.

Das folgende Beispiel zeigt Schlüssel/Wert-Paare, die in einer Konfigurationsdatei gefunden wurden:

**Configuration JSON-Beispiel**

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

Sie können auf die Konfigurations-JSON über jede Klassenmethode zugreifen, die `config_properties` als Parameter definiert wird. Beispiel:

**PySpark**

```python
dataset_id = str(config_properties.get(dataset_id))
```

Ein detaillierteres Konfigurationsbeispiel finden Sie in der Datei &quot; [ipipipeline.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/feature_pipeline_recipes/pyspark/pipeline.json) &quot;von Data Science Workspace.

### Vorbereiten der Eingabedaten mit DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader ist für das Abrufen und Filtern von Eingabedaten zuständig. Ihre Implementierung von DataLoader muss die abstrakte Klasse erweitern `DataLoader` und die abstrakte Methode überschreiben `load`.

Im folgenden Beispiel wird ein [!DNL Platform] Datensatz nach ID abgerufen und als DataFrame zurückgegeben, wobei die DataSet-ID (`dataset_id`) eine definierte Eigenschaft in der Konfigurationsdatei ist.

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

### Datentransfer mit DataSetTransformer {#transform-a-dataset-with-datasettransformer}

Ein DatasetTransformer stellt die Logik zum Transformieren eines DataFrame-Eingabedaten bereit und gibt einen neuen abgeleiteten DataFrame zurück. Diese Klasse kann implementiert werden, um entweder gemeinsam mit einer FeaturePipelineFactory zu arbeiten, als einzige Funktionstechnikkomponente zu arbeiten, oder Sie können festlegen, dass diese Klasse nicht implementiert wird.

Im folgenden Beispiel wird die DataSetTransformer-Klasse erweitert:


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

### Datenfunktionen für Entwickler mit FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

Mit einer FeaturePipelineFactory können Sie Ihre Funktionstechnik-Logik implementieren, indem Sie eine Reihe von Spark-Transformatoren über eine Spark-Pipeline definieren und verketten. Diese Klasse kann implementiert werden, um entweder mit einem DatasetTransformer zusammenzuarbeiten, als einzige Komponente der Funktionstechnik zu arbeiten, oder Sie können diese Klasse nicht implementieren.

Im folgenden Beispiel wird die FeaturePipelineFactory-Klasse erweitert:

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

### Speichern Sie Ihr Feature DataSet mit DataSaver {#store-your-feature-dataset-with-datasaver}

Der DataSaver ist für das Speichern der sich ergebenden Funktionsdatensätze an einem Speicherort für die Datenspeicherung zuständig. Ihre Implementierung von DataSaver muss die abstrakte Klasse erweitern `DataSaver` und die abstrakte Methode überschreiben `save`.

Im folgenden Beispiel wird die DataSaver-Klasse erweitert, in der Daten nach ID in einem [!DNL Platform] Datensatz gespeichert werden, wobei die DataSet-ID (`featureDatasetId`) und die Mandant-ID (`tenantId`) Eigenschaften in der Konfiguration sind.

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

Nachdem Sie die Klassen für Ihre Funktionen definiert und implementiert haben, müssen Sie die Namen Ihrer Klassen in der YAML-Anwendungsdatei angeben.

In den folgenden Beispielen werden implementierte Klassennamen angegeben:

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

## Erstellen Sie Ihre Feature Pipeline-Engine mit der API {#create-feature-pipeline-engine-api}

Nachdem Sie Ihre Feature-Pipeline erstellt haben, müssen Sie ein Docker-Bild erstellen, um die Feature-Pipeline-Endpunkte in der Sensei Machine Learning API aufzurufen. Sie benötigen eine Docker-Bild-URL, um die Feature-Pipeline-Endpunkte aufzurufen.

>[!TIP]
>Wenn Sie keine Docker-URL haben, besuchen Sie die Quelldateien des [Pakets in einem Rezept](../models-recipes/package-source-files-recipe.md) -Lernprogramm, um eine schrittweise Anleitung zum Erstellen einer Docker-Host-URL zu erhalten.

Optional können Sie auch die folgende Postman-Sammlung verwenden, um den Workflow der Feature Pipeline-API abzuschließen:

https://www.getpostman.com/collections/c5fc0d1d5805a5ddd41a

### Erstellen einer Feature-Pipeline-Engine {#create-engine-api}

Sobald Sie Ihren Docker-Bildspeicherort haben, können Sie eine Feature-Pipeline-Engine [mit der Sensei Machine Learning API](../api/engines.md#feature-pipeline-docker) erstellen, indem Sie einen POST-Test zu `/engines`erstellen. Durch die erfolgreiche Erstellung einer Feature Pipeline-Engine erhalten Sie eine eindeutige Engine-ID (`id`). Achten Sie darauf, diesen Wert zu speichern, bevor Sie fortfahren.

### Erstellen einer MLInstanz {#create-mlinstance}

Mit der neu erstellten `engineID`Funktion müssen Sie eine MLIstance [erstellen, indem Sie eine POST-Anforderung an den](../api/mlinstances.md#create-an-mlinstance) `/mlInstance` Endpunkt senden. Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die die Details der neu erstellten MLInstanz einschließlich ihrer eindeutigen Kennung (`id`) enthält, die im nächsten API-Aufruf verwendet wird.

### Experiment erstellen {#create-experiment}

Als Nächstes müssen Sie ein Experiment [erstellen](../api/experiments.md#create-an-experiment). Um ein Experiment zu erstellen, müssen Sie Ihren MLIstance eindeutigen Bezeichner (`id`) haben und eine POST-Anforderung an den `/experiment` Endpunkt stellen. Eine erfolgreiche Antwort gibt eine Nutzlast zurück, die die Details des neu erstellten Experiments einschließlich der eindeutigen Kennung (`id`) enthält, die im nächsten API-Aufruf verwendet wird.

### Aufgabe der Pipelines für die Experimentausführungsfunktion angeben {#specify-feature-pipeline-task}

Nach dem Erstellen eines Experiments müssen Sie den Modus des Experiments in `featurePipeline`ändern. Um den Modus zu ändern, führen Sie einen zusätzlichen POST-Test an [`experiments/{EXPERIMENT_ID}/runs`](../api/experiments.md#experiment-training-scoring) Ihren und im Körper senden, um eine Funktion Pipelinement-Ausführung `EXPERIMENT_ID` `{ "mode":"featurePipeline"}` anzugeben.

Nach Abschluss des Tests müssen Sie eine GET-Anforderung stellen, `/experiments/{EXPERIMENT_ID}` um den Experimentstatus [](../api/experiments.md#retrieve-specific) abzurufen, und warten, bis der Experimentstatus aktualisiert wurde.

### Festlegen der Aufgabe für die Testausführung {#training}

Als Nächstes müssen Sie die Aufgabe [für die Schulungsausführung](../api/experiments.md#experiment-training-scoring)angeben. Erstellen Sie einen POST-Test, um `experiments/{EXPERIMENT_ID}/runs` und im Körper legen Sie den Modus auf `train` und senden Sie ein Array von Aufgaben, die Ihre Schulungsparameter enthalten. Eine erfolgreiche Antwort gibt eine Nutzlast mit den Details des angeforderten Experiments zurück.

Nach Abschluss des Tests müssen Sie eine GET-Anforderung stellen, `/experiments/{EXPERIMENT_ID}` um den Experimentstatus [](../api/experiments.md#retrieve-specific) abzurufen, und warten, bis der Experimentstatus aktualisiert wurde.

### Festlegen der Aufgabe für die Auswertung von Experimenten {#scoring}

>[!NOTE]
> Um diesen Schritt abzuschließen, müssen Sie mindestens einen erfolgreichen Schulungslauf mit Ihrem Experiment verknüpfen.

Nach einem erfolgreichen Schulungslauf müssen Sie die [Aufgabe](../api/experiments.md#experiment-training-scoring)für die Bewertungsausführung angeben. Erstellen Sie einen POST auf `experiments/{EXPERIMENT_ID}/runs` und setzen Sie das `mode` Attribut auf &quot;score&quot;. Dies Beginn die Ausführung Ihres Bewertungsexperiments.

Nach Abschluss des Tests müssen Sie eine GET-Anforderung stellen, `/experiments/{EXPERIMENT_ID}` um den Experimentstatus [](../api/experiments.md#retrieve-specific) abzurufen, und warten, bis der Experimentstatus aktualisiert wurde.

Sobald die Bewertung abgeschlossen ist, sollte Ihre Feature-Pipeline betriebsbereit sein.

## Nächste Schritte {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the feature pipeline Engine. Update this document once those tutorials are available)

Durch Lesen dieses Dokuments haben Sie mithilfe des Model Authoring-SDK eine Feature-Pipeline erstellt, ein Docker-Bild erstellt und mit der Docker-Bild-URL ein Feature-Pipeline-Modell mithilfe der Sensei Machine Learning API erstellt. Sie sind jetzt bereit, mit der Transformation von Datensätzen und der Extrahierung von Datenfunktionen im Maßstab mit der [Sensei Machine Learning API](../api/getting-started.md)fortzufahren.