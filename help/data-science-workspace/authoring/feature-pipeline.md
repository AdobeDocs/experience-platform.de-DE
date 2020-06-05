---
keywords: Experience Platform;Tutorial;Feature Pipeline;Data Science Workspace;popular topics
solution: Experience Platform
title: Funktionsebenen erstellen
topic: Tutorial
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# Funktionsebenen erstellen

[!DNL Adobe Experience Platform] ermöglicht es Ihnen, benutzerdefinierte Funktionselemente zu erstellen und zu erstellen, um die Funktionstechnik im Maßstab über die Sensei Machine Learning Framework Runtime (im Folgenden &quot;Laufzeit&quot; genannt) durchzuführen.

In diesem Dokument werden die verschiedenen Klassen in einer Feature Pipeline beschrieben und ein schrittweises Lernprogramm zum Erstellen einer benutzerdefinierten Feature Pipeline mit dem [Model Authoring SDK](./sdk.md) in PySpark und Spark bereitgestellt.

## Funktionspipeline-Klassen

In der folgenden Tabelle werden die wichtigsten abstrakten Klassen beschrieben, die Sie erweitern müssen, um eine Feature Pipeline zu erstellen:

| Abstrakte Klasse | Beschreibung |
| -------------- | ----------- |
| DataLoader | Eine DataLoader-Klasse stellt eine Implementierung zum Abrufen von Eingabedaten bereit. |
| DatasetTransformer | Eine DataSetTransformer-Klasse stellt Implementierungen zum Transformieren des Eingabedatasets bereit. Sie können festlegen, dass keine DataSetTransformer-Klasse bereitgestellt und Ihre Funktionstechnik stattdessen in die FeaturePipelineFactory-Klasse implementiert werden soll. |
| FeaturePipelineFactory | Eine FeaturePipelineFactory-Klasse erstellt eine Spark-Pipeline, die aus einer Reihe von Spark-Transformatoren besteht, um die Funktionstechnik durchzuführen. Sie können festlegen, dass keine FeaturePipelineFactory-Klasse bereitgestellt und Ihre Funktionstechnik stattdessen in die DatasetTransformer-Klasse implementiert wird. |
| DataSaver | Eine DataSaver-Klasse stellt die Logik für die Datenspeicherung eines Funktionsdatasets bereit. |

Wenn ein Funktionspipelineauftrag initiiert wird, führt die Laufzeitumgebung zunächst den DataLoader aus, um Eingabedaten als DataFrame zu laden, und ändert dann den DataFrame, indem entweder DataTransformer oder FeaturePipelineFactory oder beide ausgeführt werden. Schließlich wird der sich ergebende Funktionsdatensatz über den DataSaver gespeichert.

Das folgende Flussdiagramm zeigt die Ausführungsreihenfolge der Laufzeitumgebung:

![](../images/authoring/feature-pipeline/FeaturePipeline_Runtime_flow.png)


## Implementieren von Funktionen in Pipeline-Klassen {#implement-your-feature-pipeline-classes}

Die folgenden Abschnitte enthalten Details und Beispiele zur Implementierung der erforderlichen Klassen für eine Feature Pipeline.

### Variablen in der JSON-Konfigurationsdatei definieren {#define-variables-in-the-configuration-json-file}

Die JSON-Konfigurationsdatei besteht aus Schlüssel-Wert-Paaren und dient zum Angeben von Variablen, die später während der Laufzeit definiert werden sollen. Diese Schlüssel-Wert-Paare können Eigenschaften wie den Speicherort des Eingabedatasets, die ID des Ausgabedatasets, die Mandant-ID, Spaltenköpfe usw. definieren.

Das folgende Beispiel zeigt Schlüssel-Wert-Paare, die in einer Konfigurationsdatei gefunden wurden. Erweitern Sie das Beispiel, um Details anzuzeigen:


**Configuration JSON-Beispiel**

```json
[
    {
        "name": "fp",
        "parameters": [
            {
                "key": "datasetId",
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



Sie können auf die Konfigurations-JSON über jede Klassenmethode zugreifen, die `configProperties` als Parameter definiert wird. Beispiel:

**PySpark**

```python
input_dataset_id = str(configProperties.get("datasetId"))
```

**Spark**

```scala
val input_dataset_id: String = configProperties.get("datasetId")
```


### Vorbereiten der Eingabedaten mit DataLoader {#prepare-the-input-data-with-dataloader}

DataLoader ist für das Abrufen und Filtern von Eingabedaten zuständig. Ihre Implementierung von DataLoader muss die abstrakte Klasse erweitern `DataLoader` und die abstrakte Methode überschreiben `load`.

Im folgenden Beispiel wird ein Platform-Datensatz nach ID abgerufen und als DataFrame zurückgegeben, wobei die DataSet-ID (`datasetId`) eine definierte Eigenschaft in der Konfigurationsdatei ist. Erweitern Sie jedes Beispiel, um Details anzuzeigen:


**PySpark-Beispiel**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    def load(self, configProperties, spark):

        # preliminary checks
        if configProperties is None :
            raise ValueError("configProperties parameter is null")
        if spark is None:
            raise ValueError("spark parameter is null")

        # prepare variables
        dataset_id = str(
            configProperties.get("datasetId"))
        service_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(
            spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
        for arg in ['dataset_id', 'service_token', 'user_token', 'org_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session
        df = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return df
```




**Spark-Beispiel**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

class MyDataLoader extends DataLoader {
    override def load(configProperties: ConfigProperties, sparkSession: SparkSession): DataFrame = {

        // preliminary checks
        require(configProperties != null)
        require(sparkSession != null)

        // prepare variables
        val dataSetId: String = configProperties
            .get("datasetId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(dataSetId, serviceToken, userToken, orgId, apiKey).foreach(
            value => required(value != "")
        )

        // load dataset through Spark session
        var df = sparkSession.read.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .load(dataSetId)
        
        // return as DataFrame
        df
    }
}
```



### Datentransfer mit DataSetTransformer {#transform-a-dataset-with-datasettransformer}

Ein DatasetTransformer stellt die Logik zum Transformieren eines DataFrame-Eingabedaten bereit und gibt einen neuen abgeleiteten DataFrame zurück. Diese Klasse kann implementiert werden, um entweder gemeinsam mit einer FeaturePipelineFactory zu arbeiten, als einzige Funktionstechnikkomponente zu arbeiten, oder Sie können festlegen, dass diese Klasse nicht implementiert wird.

Im folgenden Beispiel wird die DatasetTransformer-Klasse erweitert. Erweitern Sie jedes Beispiel, um Details anzuzeigen:


**PySpark-Beispiel**

```python
# PySpark

from sdk.dataset_transformer import DatasetTransformer

class MyDatasetTransformer(DatasetTransformer):

    def transform(self, configProperties, dataset):
        transformed = dataset

        '''
        Transformations
        '''

        # return new DataFrame
        return transformed
```




**Spark-Beispiel**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DatasetTransformer

class MyDatasetTransformer extends DatasetTransformer {

    override def transform(configProperties: ConfigProperties, dataset: Dataset[_]): Dataset[_] = {
        val transformed = dataset

        /*
        transformations
        */
        
        // return new DataFrame
        transformed
    }
}
```



### Datenfunktionen für Entwickler mit FeaturePipelineFactory {#engineer-data-features-with-featurepipelinefactory}

Mit einer FeaturePipelineFactory können Sie Ihre Funktionstechnik-Logik implementieren, indem Sie eine Reihe von Spark-Transformatoren über eine Spark-Pipeline definieren und verketten. Diese Klasse kann implementiert werden, um entweder mit einem DatasetTransformer zusammenzuarbeiten, als einzige Komponente der Funktionstechnik zu arbeiten, oder Sie können diese Klasse nicht implementieren.

Im folgenden Beispiel wird die FeaturePipelieFactory-Klasse erweitert und eine Reihe von Spark-Transformatoren als mehrere Phasen in einer Spark-Pipeline implementiert. Erweitern Sie jedes Beispiel, um Details anzuzeigen:


**PySpark-Beispiel**

```python
# PySpark

from pyspark.ml import Pipeline
from pyspark.ml.feature import HashingTF, Tokenizer
from sdk.feature_pipeline_factory import FeaturePipelineFactory

class MyFeaturePipelineFactory(FeaturePipelineFactory):

    def create_pipeline(self, configProperties):

        # Spark Transformers
        tokenizer = Tokenizer(inputCol="lower_text", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")

        # Chain together Spark Transformers as Spark Pipeline Stages
        pipeline = Pipeline(stages=[tokenizer, hashingTF])

        # return a Spark Pipeline
        return pipeline

    def get_param_map(self, configProperties, sparkSession):
        pass
```




**Spark-Beispiel**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.FeaturePipelineFactory
import org.apache.spark.ml.feature.{HashingTF, Tokenizer}
import org.apache.spark.ml.Pipeline
import org.apache.spark.ml.param.ParamMap
import org.apache.spark.sql.SparkSession

class MyFeaturePipelineFactory(uid:String) extends FeaturePipelineFactory(uid) {
    def this() = this("MyFeaturePipeline")

    override def createPipeline(configProperties: ConfigProperties): Pipeline = {
        
        // Spark Transformers
        val tokenizer = new Tokenizer()
            .setInputCol("lower_text")
            .setOutputCol("words")
        val hashingTF = new HashingTF()
            .setInputCol(tokenizer.getOutputCol())
            .setOutputCol("features")

        // Chain together Spark Transformers as Spark Pipeline Stages
        val pipeline = new Pipeline()
            .setStages(Array(tokenizer, hashingTF))
        
        // return a Spark Pipeline
        pipeline
    }

    override def getParamMap(configProperties: ConfigProperties, sparkSession: SparkSession): ParamMap = {
        val map = new ParamMap()
        map
    }
}
```



### Speichern Sie Ihr Feature DataSet mit DataSaver {#store-your-feature-dataset-with-datasaver}

Der DataSaver ist für das Speichern der sich ergebenden Funktionsdatensätze an einem Speicherort für die Datenspeicherung zuständig. Ihre Implementierung von DataSaver muss die abstrakte Klasse erweitern `DataSaver` und die abstrakte Methode überschreiben `save`.

Im folgenden Beispiel wird die DataSaver-Klasse erweitert, die Daten nach ID in einem Platform-Datensatz speichert, wobei die Dataset-ID (`featureDatasetId`) und die Mandant-ID (`tenantId`) Eigenschaften in der Konfigurationsdatei sind. Erweitern Sie jedes Beispiel, um Details anzuzeigen:


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




**Spark-Beispiel**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

class MyDataSaver extends DataSaver {
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("featureDatasetId").getOrElse("")
        val tenant_id:String = configProperties
            .get("tenantId").getOrElse("")
        val serviceToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
        val userToken: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_TOKEN", "").toString
        val orgId: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
        val apiKey: String = sparkSession.sparkContext.getConf
            .get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

        // validate variables
        List(output_dataset_id, tenant_id, serviceToken, userToken, orgId, apiKey).foreach(
            value => require(value != "")
        )

        // create and prepare DataFrame with valid columns
        import sparkSession.implicits._

        var output_df  = dataFrame.withColumn("date", $"date".cast("String"))
        output_df = output_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
        output_df = output_df.withColumn("_id", lit("empty"))
        output_df = output_df.withColumn("eventType", lit("empty"))

        // store data into dataset
        output_df.select(tenant_id, "_id", "eventType", "timestamp").write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

### Geben Sie Ihre implementierten Klassennamen in der Anwendungsdatei an {#specify-your-implemented-class-names-in-the-application-file}

Nachdem Sie die Klassen in der Feature Pipeline definiert und implementiert haben, müssen Sie die Namen Ihrer Klassen in der Anwendungsdatei angeben.

Die folgenden Beispiele geben implementierte Klassennamen an. Erweitern Sie das Beispiel, um Details anzuzeigen:


**PySpark-Beispiel**

```yaml
# application.yaml

# Name of the implementation of DataLoader abstract class
feature.dataLoader: MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer: MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.pipeline.class: MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver: MyDataSaver
```




**Spark-Beispiel**

```properties
# application.properties

# Name of the implementation of DataLoader abstract class
feature.pipeline.class=MyDataLoader

# Name of the implementation of DatasetTransformer abstract class
feature.dataset.transformer=MyDatasetTransformer

# Name of the implementation of FeaturePipelineFactory abstract class
feature.dataLoader=MyFeaturePipelineFactory

# Name of the implementation of DataSaver abstract class
feature.dataSaver=MyDataSaver
```



## Binäres Artefakt erstellen {#build-the-binary-artifact}

Nachdem Ihre Feature Pipeline-Klassen implementiert wurden, können Sie sie erstellen und in ein binäres Artefakt kompilieren, das dann zur Erstellung einer Feature Pipeline über API-Aufrufe verwendet werden kann.

**PySpark**

Führen Sie zum Erstellen einer PySpark Feature Pipeline das `setup.py` Python-Skript aus, das sich im Stammverzeichnis des Model Authoring-SDK befindet.

>[!NOTE] Zum Erstellen einer PySpark Feature Pipeline müssen Sie Python 3 auf Ihrem Computer installiert haben.

```shell
python3 setup.py bdist_egg
```

Wenn Sie Ihre Feature Pipeline erfolgreich erstellen, wird ein `.egg` Artefakt im `/dist` Verzeichnis generiert. Mit diesem Artefakt wird eine Feature Pipeline erstellt.

**Spark**

Um eine Spark-Feature-Pipeline zu erstellen, führen Sie den folgenden Konsolenbefehl im Stammverzeichnis des Model Authoring-SDK aus:

>[!NOTE] Zum Erstellen einer Pipeline für Spark-Funktionen müssen Sie Scala und sbt auf Ihrem Computer installiert haben.

```shell
mvn clean install
```

Wenn Sie Ihre Feature Pipeline erfolgreich erstellen, wird ein `.jar` Artefakt im `/dist` Verzeichnis generiert. Mit diesem Artefakt wird eine Feature Pipeline erstellt.

## Erstellen einer Feature Pipeline-Engine mit der API {#create-a-feature-pipeline-engine-using-the-api}

Nachdem Sie Ihre Feature Pipeline erstellt und das binäre Artefakt erstellt haben, können Sie eine Feature Pipeline Engine mit der Sensei Machine Learning API [erstellen](../api/engines.md#create-a-feature-pipeline-engine-using-binary-artifacts). Wenn Sie eine Feature Pipeline Engine erfolgreich erstellen, erhalten Sie eine Engine-ID als Teil des Antwortkörpers. Achten Sie darauf, diesen Wert zu speichern, bevor Sie mit den nächsten Schritten fortfahren.

## Nächste Schritte {#next-steps}

[//]: # (Next steps section should refer to tutorials on how to score data using the Feature Pipeline Engine. Update this document once those tutorials are available)

Durch Lesen dieses Dokuments haben Sie eine Feature Pipeline mit dem Model Authoring SDK erstellt, ein binäres Artefakt erstellt und mit dem Artefakt eine Feature Pipeline Engine über einen API-Aufruf erstellt. Sie können jetzt ein Funktionspipelinemodell [](../api/mlinstances.md#create-an-mlinstance) erstellen, indem Sie Ihre neu erstellten Engine- und Beginn-Transformationen verwenden und Datenfunktionen skalierbar extrahieren.