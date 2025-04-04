---
keywords: Experience Platform;Entwicklerhandbuch;SDK;Modellerstellung;Datenwissenschafts-Workspace;beliebte Themen;Tests
solution: Experience Platform
title: Modellerstellungs-SDK
description: Mit der Modellerstellungs-SDK können Sie benutzerdefinierte Rezepte für maschinelles Lernen und Funktions-Pipelines entwickeln, die in Adobe Experience Platform Data Science Workspace verwendet werden können und implementierbare Vorlagen in PySpark und Scala bereitstellen.
exl-id: c7577f93-a64f-49b7-a76d-71f21d619052
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 62%

---

# Modellerstellungs-SDK

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Mit der Modellerstellungs-SDK können Sie benutzerdefinierte Rezepte für maschinelles Lernen und Feature Pipelines entwickeln, die in [!DNL Adobe Experience Platform] Data Science Workspace verwendet werden können und implementierbare Vorlagen in [!DNL PySpark] und [!DNL Spark (Scala)] bereitstellen.

Dieses Dokument enthält Informationen zu den verschiedenen Klassen, die in der Modellerstellungs-SDK zu finden sind.

## DataLoader {#dataloader}

Die DataLoader-Klasse enthält alles, was zum Abrufen, Filtern und Zurückgeben von rohen Eingabedaten benötigt wird. Beispiele für Eingabedaten sind Daten für Training, Scoring oder Funktionsentwicklung. Datenlader erweitern die abstrakte Klasse `DataLoader` und müssen die abstrakte Methode `load` überschreiben.

**PySpark**

In der folgenden Tabelle werden die abstrakten Methoden einer PySpark-Datenlader-Klasse beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(self, configProperties, spark)</code></p>
                <p>Laden und Zurückgeben von Experience Platform-Daten als Pandas DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>configProperties</code>: Zuordnung von Konfigurationseigenschaften</li>
                    <li><code>spark</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

In der folgenden Tabelle werden die abstrakten Methoden einer [!DNL Spark] Data Loader-Klasse beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>load(configProperties, sparkSession)</code></p>
                <p>Laden und Zurückgeben von Experience Platform-Daten als DataFrame</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Zuordnung von Konfigurationseigenschaften</li>
                    <li><code>sparkSession</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Daten aus einem [!DNL Experience Platform] Datensatz laden {#load-data-from-a-platform-dataset}

Im folgenden Beispiel werden [!DNL Experience Platform] Daten nach ID abgerufen und ein DataFrame zurückgegeben, wobei die Datensatz-ID (`datasetId`) eine definierte Eigenschaft in der Konfigurationsdatei ist.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load_dataset(config_properties, spark, task_id):

        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"
        PLATFORM_SDK_PQS_INTERACTIVE = "interactive"

        # prepare variables
        service_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(spark.sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        dataset_id = str(config_properties.get(task_id))

        # validate variables
        for arg in ['service_token', 'user_token', 'org_id', 'dataset_id', 'api_key']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)

        # load dataset through Spark session

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

        # return as DataFrame
        return pd
```

**Spark (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import java.time.LocalDateTime

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.ml.feature.StringIndexer
import org.apache.spark.sql.expressions.Window
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.{StructType, TimestampType}
import org.apache.spark.sql.{DataFrame, SparkSession}
import org.apache.spark.sql.Column

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
    final val PLATFORM_SDK_PQS_INTERACTIVE: String = "interactive"
    final val PLATFORM_SDK_PQS_BATCH: String = "batch"

    /**
    *
    * @param configProperties - Configuration Properties map
    * @param sparkSession     - SparkSession
    * @return                 - DataFrame which is loaded for training
    */


  def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {

    require(configProperties != null)
    require(sparkSession != null)

    // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString

    val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, PLATFORM_SDK_PQS_INTERACTIVE)
      .option(QSOption.datasetId, dataSetId)
      .load()
    df.show()
    df
    }
}
```

## DataSaver {#datasaver}

Die DataSaver-Klasse enthält alles, was mit dem Speichern von Ausgabedaten zu tun hat, einschließlich Daten für Scoring oder Funktionsentwicklung. Data Saver erweitern die abstrakte Klasse `DataSaver` und müssen die abstrakte Methode `save` überschreiben.

**PySpark**

In der folgenden Tabelle werden die abstrakten Methoden einer [!DNL PySpark] Data Saver-Klasse beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(self, configProperties, dataframe)</code></p>
                <p>Ausgabedaten als DataFrame empfangen und in einem Experience Platform-Datensatz speichern</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>configProperties</code>: Zuordnung von Konfigurationseigenschaften</li>
                    <li><code>dataframe</code>: Daten, die in Form eines DataFrame gespeichert werden sollen</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

In der folgenden Tabelle werden die abstrakten Methoden einer [!DNL Spark] Data Saver-Klasse beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>save(configProperties, dataFrame)</code></p>
                <p>Ausgabedaten als DataFrame empfangen und in einem Experience Platform-Datensatz speichern</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Zuordnung von Konfigurationseigenschaften</li>
                    <li><code>dataFrame</code>: Daten, die in Form eines DataFrame gespeichert werden sollen</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Speichern von Daten in einem [!DNL Experience Platform] {#save-data-to-a-platform-dataset}

Um Daten in einem [!DNL Experience Platform] Datensatz zu speichern, müssen die Eigenschaften entweder bereitgestellt oder in der Konfigurationsdatei definiert werden:

- Eine gültige [!DNL Experience Platform]-Datensatz-ID, unter der Daten gespeichert werden
- Die Mandanten-ID in Ihrer Organisation

In den folgenden Beispielen werden Daten (`prediction`) in einem [!DNL Experience Platform]-Datensatz gespeichert, wobei die Datensatz-ID (`datasetId`) und die Mandanten-ID (`tenantId`) Eigenschaften in der Konfigurationsdatei sind.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType
from pyspark.sql.functions import col, lit, struct
from .helper import *


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to an Experience Platform dataset
    """

    def save(self, config_properties, prediction):

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if config_properties is None:
            raise ValueError("config_properties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")
        
        PLATFORM_SDK_PQS_PACKAGE = "com.adobe.platform.query"

        # prepare variables
        scored_dataset_id = str(config_properties.get("scoringResultsDataSetId"))
        tenant_id = str(config_properties.get("tenant_id"))
        timestamp = "2019-01-01 00:00:00"

        service_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ML_TOKEN"))
        user_token = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_TOKEN"))
        org_id = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_ORG_ID"))
        api_key = str(sparkContext.getConf().get("ML_FRAMEWORK_IMS_CLIENT_ID"))

        # validate variables
       for arg in ['service_token', 'user_token', 'org_id', 'scored_dataset_id', 'api_key', 'tenant_id']:
            if eval(arg) == 'None':
                raise ValueError("%s is empty" % arg)
        
        scored_df = prediction.withColumn("date", col("date").cast(StringType()))
        scored_df = scored_df.withColumn(tenant_id, struct(col("date"), col("store"), col("prediction")))
        scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType()))
        scored_df = scored_df.withColumn("_id", lit("empty"))
        scored_df = scored_df.withColumn("eventType", lit("empty")

        # store data into dataset

        query_options = get_query_options(sparkContext)

        scored_df.select(tenant_id, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE) \
            .option(query_options.userToken(), user_token) \
            .option(query_options.serviceToken(), service_token) \
            .option(query_options.imsOrg(), org_id) \
            .option(query_options.apiKey(), api_key) \
            .option(query_options.datasetId(), scored_dataset_id) \
            .save()
```

**Spark (Scala)**

```scala
// Spark

package com.adobe.platform.ml

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to an Experience Platform dataset
 */

class ScoringDataSaver extends DataSaver {

  final val PLATFORM_SDK_PQS_PACKAGE: String = "com.adobe.platform.query"
  final val PLATFORM_SDK_PQS_BATCH: String = "batch"

  /**
    * Method that saves the scoring data into a dataframe
    * @param configProperties  - Configuration Properties map
    * @param dataFrame         - Dataframe with the scoring results
    */
    
  override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

    require(configProperties != null)
    require(dataFrame != null)

    val predictionColumn = configProperties.get(Constants.PREDICTION_COL).getOrElse(Constants.DEFAULT_PREDICTION)
    val sparkSession = dataFrame.sparkSession

    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val tenantId:String = configProperties.get("tenantId").getOrElse("")
    val timestamp:String = "2019-01-01 00:00:00"

    val scoringResultsDataSetId: String = configProperties.get("scoringResultsDataSetId").getOrElse("")
    import sparkSession.implicits._

    var df = dataFrame.withColumn("date", $"date".cast("String"))

    var scored_df  = df.withColumn(tenantId, struct(df("date"), df("store"), df(predictionColumn)))
    scored_df = scored_df.withColumn("timestamp", lit(timestamp).cast(TimestampType))
    scored_df = scored_df.withColumn("_id", lit("empty"))
    scored_df = scored_df.withColumn("eventType", lit("empty"))

    scored_df.select(tenantId, "_id", "eventType", "timestamp").write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .save()
    }
}
```

## DatasetTransformer {#datasettransformer}

Die DatasetTransformer-Klasse ändert und transformiert die Struktur eines Datensatzes. Für die [!DNL Sensei Machine Learning Runtime] muss diese Komponente nicht definiert sein. Sie wird entsprechend Ihren Anforderungen implementiert.

Im Hinblick auf eine Funktions-Pipeline können DataSet Transformer gemeinsam mit einer Feature-Pipeline-Factory zur Vorbereitung von Daten für die Funktionsentwicklung genutzt werden.

**PySpark**

In der folgenden Tabelle werden die Klassenmethoden einer PySpark-DataSet Transformer-Klasse beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>transform(self, configProperties, dataset)</code></p>
                <p>Nimmt einen Datensatz als Eingabe und gibt einen neuen abgeleiteten Datensatz aus</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>configProperties</code>: Zuordnung von Konfigurationseigenschaften</li>
                    <li><code>dataset</code>: Der Eingabedatensatz für die Transformation</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

In der folgenden Tabelle werden die abstrakten Methoden einer [!DNL Spark] DataSet-Transformatorklasse beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><code>transform(configProperties, dataset)</code></p>
                <p>Nimmt einen Datensatz als Eingabe und gibt einen neuen abgeleiteten Datensatz aus</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Zuordnung von Konfigurationseigenschaften</li>
                    <li><code>dataset</code>: Der Eingabedatensatz für die Transformation</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

Die FeaturePipelineFactory-Klasse enthält Extraktionsalgorithmen für Funktionen und definiert die Phasen einer Funktions-Pipeline von Anfang bis Ende.

**PySpark**

In der folgenden Tabelle werden die Klassenmethoden einer PySpark-FeaturePipelineFactory beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>create_pipeline(self, configProperties)</code></p>
                <p>Spark-Pipeline erstellen und zurückgeben, die eine Reihe von Spark-Transformern enthält</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>configProperties</code>: Zuordnung von Konfigurationseigenschaften</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Parameter-Mapping aus Konfigurationseigenschaften abrufen und zurückgeben</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code>sparkSession</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

In der folgenden Tabelle werden die Klassenmethoden einer [!DNL Spark] FeaturePipelineFactory beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>createPipeline(configProperties)</code></p>
                <p>Pipeline mit einer Reihe von Umwandlern erstellen und zurückgeben</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Zuordnung von Konfigurationseigenschaften</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Parameter-Mapping aus Konfigurationseigenschaften abrufen und zurückgeben</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code>sparkSession</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

Die PipelineFactory-Klasse kapselt Methoden und Definitionen für Modelltraining und -bewertung, bei denen Trainingslogik und Algorithmen in Form einer [!DNL Spark] Pipeline definiert sind.

**PySpark**

Die folgende Tabelle beschreibt die Klassenmethoden einer PySpark-PipelineFactory:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(self, configProperties)</code></p>
                <p>Spark-Pipeline erstellen und zurückgeben, die die Logik und den Algorithmus für das Trainieren und Bewerten von Modellen enthält</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>train(self, configProperties, dataframe)</code></p>
                <p>Benutzerdefinierte Pipeline zurückgeben, die die Logik und den Algorithmus zum Trainieren eines Modells enthält. Diese Methode ist nicht erforderlich, wenn eine Spark-Pipeline verwendet wird</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code>dataframe</code>: Funktionsdatensatz für Trainings-Eingabe</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>score(self, configProperties, dataframe, model)</code></p>
                <p>Mit dem trainierten Modell bewerten und die Ergebnisse zurückgeben</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code>dataframe</code>: Eingabedatensatz für Scoring</li>
                    <li><code>model</code>: Ein trainiertes Modell, das zum Scoring verwendet wird</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Parameter-Mapping aus Konfigurationseigenschaften abrufen und zurückgeben</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code>sparkSession</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

In der folgenden Tabelle werden die Klassenmethoden einer [!DNL Spark] PipelineFactory beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>apply(configProperties)</code></p>
                <p>Pipeline erstellen und zurückgeben, die die Logik und den Algorithmus für das Trainieren und Bewerten von Modellen enthält</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>getParamMap(configProperties, sparkSession)</code></p>
                <p>Parameter-Mapping aus Konfigurationseigenschaften abrufen und zurückgeben</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code>sparkSession</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

Die MLEvaluator-Klasse stellt Methoden zum Definieren von Auswertungsmetriken und zum Festlegen von Trainings- und Testdatensätzen bereit.

**PySpark**

In der folgenden Tabelle werden die Klassenmethoden eines PySpark-MLEvaluator beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(self, configProperties, dataframe)</code></p>
                <p>Teilt den Eingabedatensatz in Trainings- und Testuntergruppen</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code>dataframe</code>: Zu teilender Eingabedatensatz</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Wertet ein trainiertes Modell aus und gibt die Auswertungsergebnisse zurück</p>
            </td>
            <td>
                <ul>
                    <li><code>self</code>: Eigenverweis</li>
                    <li><code>dataframe</code>: Ein DataFrame, bestehend aus Trainings- und Testdaten</li>
                    <li><code>model</code>: Ein trainiertes Modell</li>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark (Scala)**

In der folgenden Tabelle werden die Klassenmethoden eines [!DNL Spark] MLEvaluator beschrieben:

<table>
    <thead>
        <tr>
            <th>Methode und Beschreibung</th>
            <th>Parameter</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>split(configProperties, data)</code></p>
                <p>Teilt den Eingabedatensatz in Trainings- und Testuntergruppen</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code>data</code>: Zu teilender Eingabedatensatz</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code>evaluate(configProperties, model, data)</code></p>
                <p>Wertet ein trainiertes Modell aus und gibt die Auswertungsergebnisse zurück</p>
            </td>
            <td>
                <ul>
                    <li><code>configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code>model</code>: Ein trainiertes Modell</li>
                    <li><code>data</code>: Ein DataFrame, bestehend aus Trainings- und Testdaten</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
