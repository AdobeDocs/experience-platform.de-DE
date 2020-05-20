---
keywords: Experience Platform;developer guide;SDK;Model authoring;Data Science Workspace;popular topics
solution: Experience Platform
title: SDK-Entwicklerhandbuch
topic: Overview
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---


# SDK-Entwicklerhandbuch

Das Modell Authoring-SDK ermöglicht Ihnen die Entwicklung benutzerdefinierter Rezepte für maschinelles Lernen und Funktionslinien, die in Adobe Experience Platform Data Science Workspace verwendet werden können. Es stellt implementierbare Vorlagen in PySpark und Spark bereit.

Dieses Dokument enthält Informationen zu den verschiedenen Klassen im Model Authoring-SDK.

## DataLoader {#dataloader}

Die DataLoader-Klasse enthält alle Daten zum Abrufen, Filtern und Zurückgeben von Rohdaten. Beispiele für Eingabedaten sind Schulungsdaten, Bewertungsdaten oder Funktionstechniken. Datenlader erweitern die abstrakte Klasse `DataLoader` und müssen die abstrakte Methode überschreiben `load`.

**PySpark**

In der folgenden Tabelle werden die abstrakten Methoden einer PySpark Data Loader-Klasse beschrieben:

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
                <p><code class=" language-undefined">load(self, configProperties, spark)</code></p>
                <p>Plattformdaten als Pandas-Datenrahmen laden und zurückgeben</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften-Map</li>
                    <li><code class=" language-undefined">spark</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

In der folgenden Tabelle werden die abstrakten Methoden einer Spark Data Loader-Klasse beschrieben:

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
                <p><code class=" language-undefined">load(configProperties, sparkSession)</code></p>
                <p>Plattformdaten als DataFrame laden und zurückgeben</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften-Map</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Daten aus einem Plattformdataset laden {#load-data-from-a-platform-dataset}

Im folgenden Beispiel werden Plattformdaten nach ID abgerufen und ein DataFrame zurückgegeben, wobei die DataSet-ID (`datasetId`) eine definierte Eigenschaft in der Konfigurationsdatei ist.

**PySpark**

```python
# PySpark

from sdk.data_loader import DataLoader

class MyDataLoader(DataLoader):
    """
    Implementation of DataLoader which loads a DataFrame and prepares data
    """

    def load(self, configProperties, spark):
        """
        Load and return dataset

        :param configProperties:    Configuration properties
        :param spark:               Spark session
        :return:                    DataFrame
        """

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
        pd = spark.read.format("com.adobe.platform.dataset") \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('orgId', org_id) \
            .option('serviceApiKey', api_key) \
            .load(dataset_id)

        # return as DataFrame
        return pd
```

**Spark**

```scala
// Spark

import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.sdk.DataLoader
import org.apache.spark.sql.{DataFrame, SparkSession}

/**
 * Implementation of DataLoader which loads a DataFrame and prepares data
 */
class MyDataLoader extends DataLoader {

    /**
     * @param configProperties  - Configuration properties
     * @param sparkSession      - Spark session
     * @return                  - DataFrame
     */
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

## DataSaver {#datasaver}

Die DataSaver-Klasse kapselt alles, was mit dem Speichern von Ausgabedaten zu tun hat, einschließlich Daten aus der Scoring- oder Funktionstechnik. Datensparer erweitern die abstrakte Klasse `DataSaver` und müssen die abstrakte Methode überschreiben `save`.

**PySpark**

In der folgenden Tabelle werden die abstrakten Methoden einer PySpark Data Saver-Klasse beschrieben:

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
                <p><code class=" language-undefined">save(self, configProperties, dataframe)</code></p>
                <p>Ausgabedaten als DataFrame empfangen und in einem Platform-Datensatz speichern</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften-Map</li>
                    <li><code class=" language-undefined">dataframe</code>: Daten, die in Form eines DataFrame gespeichert werden sollen</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

In der folgenden Tabelle werden die abstrakten Methoden einer Spark Data Saver-Klasse beschrieben:

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
                <p><code class=" language-undefined">save(configProperties, dataFrame)</code></p>
                <p>Ausgabedaten als DataFrame empfangen und in einem Platform-Datensatz speichern</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften-Map</li>
                    <li><code class=" language-undefined">dataFrame</code>: Daten, die in Form eines DataFrame gespeichert werden sollen</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

### Daten in einem Platform-Datensatz speichern {#save-data-to-a-platform-dataset}

Um Daten in einem Platform-Dataset zu speichern, müssen die Eigenschaften entweder bereitgestellt oder in der Konfigurationsdatei definiert werden:

- Eine gültige Plattform-Datensatz-ID, in der Daten gespeichert werden
- Die Mandanten-ID in Ihrer Organisation

Die folgenden Beispiele speichern Daten (`prediction`) in einem Platform-Dataset, wobei die Dataset-ID (`datasetId`) und die Mandant-ID (`tenantId`) Eigenschaften in der Konfigurationsdatei sind.


**PySpark**

```python
# PySpark

from sdk.data_saver import DataSaver
from pyspark.sql.types import StringType, TimestampType


class MyDataSaver(DataSaver):
    """
    Implementation of DataSaver which stores a DataFrame to a Platform dataset
    """

    def save(self, configProperties, prediction):
        """
        Store DataFrame to a Platform dataset

        :param configProperties:    Configuration properties
        :param prediction:          DataFrame to be stored to a Platform dataset
        """

        # Spark context
        sparkContext = prediction._sc

        # preliminary checks
        if configProperties is None:
            raise ValueError("configProperties parameter is null")
        if prediction is None:
            raise ValueError("prediction parameter is null")
        if sparkContext is None:
            raise ValueError("sparkContext parameter is null")

        # prepare variables
        timestamp = "2019-01-01 00:00:00"
        output_dataset_id = str(
            configProperties.get("datasetId"))
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

        # store data into dataset
        prediction.write.format("com.adobe.platform.dataset") \
            .option('orgId', org_id) \
            .option('serviceToken', service_token) \
            .option('userToken', user_token) \
            .option('serviceApiKey', api_key) \
            .save(output_dataset_id)
```




**Spark**

```scala
// Spark

import com.adobe.platform.dataset.DataSetOptions
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.ml.impl.Constants
import com.adobe.platform.ml.sdk.DataSaver
import org.apache.spark.sql.DataFrame
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types.TimestampType

/**
 * Implementation of DataSaver which stores a DataFrame to a Platform dataset
 */
class ScoringDataSaver extends DataSaver {

    /**
     * @param configProperties  - Configuration properties
     * @param dataFrame         - DataFrame to be stored to a Platform dataset
     */
    override def save(configProperties: ConfigProperties, dataFrame: DataFrame): Unit =  {

        // Spark session
        val sparkSession = dataFrame.sparkSession
        import sparkSession.implicits._

        // preliminary checks
        require(configProperties != null)
        require(dataFrame != null)

        // prepare variables
        val predictionColumn = configProperties.get(Constants.PREDICTION_COL)
            .getOrElse(Constants.DEFAULT_PREDICTION)
        val timestamp:String = "2019-01-01 00:00:00"
        val output_dataset_id: String = configProperties
            .get("datasetId").getOrElse("")
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

        // store data into dataset
        dataFrame.write.format("com.adobe.platform.dataset")
            .option(DataSetOptions.orgId, orgId)
            .option(DataSetOptions.serviceToken, serviceToken)
            .option(DataSetOptions.userToken, userToken)
            .option(DataSetOptions.serviceApiKey, apiKey)
            .save(output_dataset_id)
    }
}
```

## DatasetTransformer {#datasettransformer}

Die DatasetTransformer-Klasse ändert und transformiert die Struktur eines Datensatzes. Die Sensei Machine Learning Runtime erfordert keine Definition dieser Komponente und wird entsprechend Ihren Anforderungen implementiert.

Im Hinblick auf eine Feature-Pipeline können DataSet-Transformer gemeinsam mit einer Feature-Pipeline-Fabrik zur Vorbereitung von Daten für die Funktionstechnik eingesetzt werden.

**PySpark**

In der folgenden Tabelle werden die Klassenmethoden einer PySpark-DataSet-Transformer-Klasse beschrieben:

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
                <p><i>abstract</i><br/><code class=" language-undefined">transform(self, configProperties, dataset)</code></p>
                <p>Übernimmt einen Datensatz als Eingabe und Ausgabe eines neuen abgeleiteten Datensatzes</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften-Map</li>
                    <li><code class=" language-undefined">dataset</code>: Das Eingabedataset für die Transformation</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

Die folgende Tabelle beschreibt die abstrakten Methoden einer Spark-DataSet-Transformer-Klasse:

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
                <p><code class=" language-undefined">transform(configProperties, dataset)</code></p>
                <p>Übernimmt einen Datensatz als Eingabe und Ausgabe eines neuen abgeleiteten Datensatzes</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften-Map</li>
                    <li><code class=" language-undefined">dataset</code>: Das Eingabedataset für die Transformation</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## FeaturePipelineFactory {#featurepipelinefactory}

Die FeaturePipelineFactory-Klasse enthält Algorithmen zur Extraktion von Funktionen und definiert die Phasen einer Feature Pipeline von Beginn zu Ende.

**PySpark**

In der folgenden Tabelle werden die Klassenmethoden einer PySpark FeaturePipelineFactory beschrieben:

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
                <p><i>abstract</i><br/><code class=" language-undefined">create_pipeline(self, configProperties)</code></p>
                <p>Erstellen und Zurückgeben einer Spark-Pipeline, die eine Reihe von Spark-Transformers enthält</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften-Map</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Abrufen und Zurückgeben der Parameterzuordnung aus den Konfigurationseigenschaften</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

In der folgenden Tabelle werden die Klassenmethoden einer Spark FeaturePipelineFactory beschrieben:

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
                <p><i>abstract</i><br/><code class=" language-undefined">createPipeline(configProperties)</code></p>
                <p>Erstellen und Zurückgeben einer Pipeline mit einer Reihe von Transformatoren</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften-Map</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Abrufen und Zurückgeben der Parameterzuordnung aus den Konfigurationseigenschaften</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## PipelineFactory {#pipelinefactory}

Die PipelineFactory-Klasse enthält Methoden und Definitionen für Modellschulungen und -bewertungen, wobei Schulungslogik und -algorithmen in Form einer Spark-Pipeline definiert werden.

**PySpark**

Die folgende Tabelle beschreibt die Klassenmethoden einer PySpark PipelineFactory:

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
                <p><i>abstract</i><br/><code class=" language-undefined">apply(self, configProperties)</code></p>
                <p>Erstellen und Zurückgeben einer Spark-Pipeline, die die Logik und den Algorithmus für Modellschulungen und -bewertungen enthält</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">train(self, configProperties, dataframe)</code></p>
                <p>Geben Sie eine benutzerdefinierte Pipeline zurück, die die Logik und den Algorithmus enthält, um ein Modell auszubilden. Diese Methode ist nicht erforderlich, wenn eine Spark-Pipeline verwendet wird</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code class=" language-undefined">dataframe</code>: Funktionsdatensatz für Schulungseingaben</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">score(self, configProperties, dataframe, model)</code></p>
                <p>Ergebnis mit dem geschulten Modell und Rückgabe der Ergebnisse</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code class=" language-undefined">dataframe</code>: Eingabedatensatz für die Bewertung</li>
                    <li><code class=" language-undefined">model</code>: Ein ausgebildetes Modell, das zur Bewertung verwendet wird</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">get_param_map(self, configProperties, sparkSession)</code></p>
                <p>Abrufen und Zurückgeben der Parameterzuordnung aus den Konfigurationseigenschaften</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

In der folgenden Tabelle werden die Klassenmethoden einer Spark PipelineFactory beschrieben:

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
                <p><i>abstract</i><br/><code class=" language-undefined">apply(configProperties)</code></p>
                <p>Erstellen und Zurückgeben einer Pipeline, die die Logik und den Algorithmus für Modellschulungen und -bewertungen enthält</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">getParamMap(configProperties, sparkSession)</code></p>
                <p>Abrufen und Zurückgeben der Parameterzuordnung aus den Konfigurationseigenschaften</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code class=" language-undefined">sparkSession</code>: Spark-Sitzung</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

## MLEvaluator {#mlevaluator}

Die MLEvaluator-Klasse stellt Methoden zum Definieren von Bewertungsmetriken und zum Festlegen von Schulungs- und Testdatasets bereit.

**PySpark**

In der folgenden Tabelle werden die Klassenmethoden eines PySpark MLEvaluators beschrieben:

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
                <p><i>abstract</i><br/><code class=" language-undefined">split(self, configProperties, dataframe)</code></p>
                <p>Teilt den Eingabedatensatz in die Untergruppen "Schulung"und "Test".</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code class=" language-undefined">dataframe</code>: Zu teilendes Eingabedataset</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">evaluate(self, dataframe, model, configProperties)</code></p>
                <p>Wertet ein ausgebildetes Modell aus und gibt die Bewertungsergebnisse zurück</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">self</code>: Eigene Referenz</li>
                    <li><code class=" language-undefined">dataframe</code>: Ein DataFrame, bestehend aus Schulungs- und Testdaten</li>
                    <li><code class=" language-undefined">model</code>: Ein geschultes Modell</li>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>

**Spark**

In der folgenden Tabelle werden die Klassenmethoden eines Spark MLEvaluators beschrieben:

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
                <p><i>abstract</i><br/><code class=" language-undefined">split(configProperties, data)</code></p>
                <p>Teilt den Eingabedatensatz in die Untergruppen "Schulung"und "Test".</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code class=" language-undefined">data</code>: Zu teilendes Eingabedataset</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>
                <p><i>abstract</i><br/><code class=" language-undefined">evaluate(configProperties, model, data)</code></p>
                <p>Wertet ein ausgebildetes Modell aus und gibt die Bewertungsergebnisse zurück</p>
            </td>
            <td>
                <ul>
                    <li><code class=" language-undefined">configProperties</code>: Konfigurationseigenschaften</li>
                    <li><code class=" language-undefined">model</code>: Ein geschultes Modell</li>
                    <li><code class=" language-undefined">data</code>: Ein DataFrame, bestehend aus Schulungs- und Testdaten</li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>