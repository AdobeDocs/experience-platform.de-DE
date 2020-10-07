---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api;spark recipe;read spark;write spark
solution: Experience Platform
title: Zugriff auf Daten mit Spark
topic: tutorial
type: Tutorial
description: Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mit Spark zur Verwendung in Data Science Workspace.
translation-type: tm+mt
source-git-commit: fcb4088ecac76d10b0cb69b04ad55167f5cdac3e
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Zugriff auf Daten mit Spark

Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mit Spark zur Verwendung in Data Science Workspace. Informationen zum Zugriff auf Daten mit JupyterLab-Notebooks finden Sie in der Dokumentation zum Datenzugriff auf [JupyterLab-Notebooks](../jupyterlab/access-notebook-data.md) .

## Erste Schritte

Für die Verwendung [!DNL Spark] sind Leistungsoptimierungen erforderlich, die dem `SparkSession`hinzugefügt werden müssen. Darüber hinaus können Sie auch `configProperties` für spätere Lese- und Schreibvorgänge in Datasets einrichten.

```scala
import com.adobe.platform.ml.config.ConfigProperties
import com.adobe.platform.query.QSOption
import org.apache.spark.sql.{DataFrame, SparkSession}

Class Helper {

 /**
   *
   * @param configProperties - Configuration Properties map
   * @param sparkSession     - SparkSession
   * @return                 - DataFrame which is loaded for training
   */

   def load_dataset(configProperties: ConfigProperties, sparkSession: SparkSession, taskId: String): DataFrame = {
            // Read the configs
            val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Lesen eines Datensatzes

Bei Verwendung von Spark haben Sie Zugriff auf zwei Lesemodi: interaktiv und stapelweise.

Im interaktiven Modus wird eine JDBC-Verbindung (Java Database Connectivity) erstellt [!DNL Query Service] und die Ergebnisse werden über eine reguläre JDBC-Verbindung abgerufen, `ResultSet` die automatisch in eine `DataFrame`übersetzt wird. Dieser Modus funktioniert ähnlich wie die integrierte [!DNL Spark] Methode `spark.read.jdbc()`. Dieser Modus ist nur für kleine Datensätze vorgesehen. Wenn Ihr Datensatz 5 Millionen Zeilen überschreitet, sollten Sie in den Stapelmodus wechseln.

Der Stapelmodus verwendet [!DNL Query Service]den COPY-Befehl, um Parquet-Ergebnismengen an einem freigegebenen Speicherort zu generieren. Diese Parquet-Dateien können dann weiter verarbeitet werden.

Nachfolgend sehen Sie ein Beispiel zum Lesen eines Datensatzes im interaktiven Modus:

```scala
  // Read the configs
    val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "interactive")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
  }
```

Ein Beispiel für das Lesen eines Datensatzes im Stapelmodus ist nachfolgend dargestellt:

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### Spalten aus dem Datensatz AUSWÄHLEN

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT-Klausel

Mit der DISTINCT-Klausel können Sie alle eindeutigen Werte auf Zeilen-/Spaltenebene abrufen und alle Duplikat-Werte aus der Antwort entfernen.

Ein Beispiel für die Verwendung der `distinct()` Funktion ist unten aufgeführt:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WO-Klausel

Das [!DNL Spark] SDK ermöglicht zwei Filtermethoden: Verwenden eines SQL-Ausdrucks oder durch Filtern von Bedingungen.

Nachfolgend sehen Sie ein Beispiel für die Verwendung dieser Filterfunktionen:

#### SQL Ausdruck

```scala
df.where("age > 15")
```

#### Filterbedingungen

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY-Klausel

Die ORDER BY-Klausel ermöglicht es, die empfangenen Ergebnisse in einer bestimmten Reihenfolge (aufsteigend oder absteigend) nach einer bestimmten Spalte zu sortieren. Im [!DNL Spark] SDK erfolgt dies mithilfe der `sort()` Funktion.

Ein Beispiel für die Verwendung der `sort()` Funktion ist unten aufgeführt:

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT-Klausel

Die LIMIT-Klausel ermöglicht es Ihnen, die Anzahl der vom Datensatz erhaltenen Datensätze zu begrenzen.

Ein Beispiel für die Verwendung der `limit()` Funktion ist unten aufgeführt:

```scala
df = df.limit(100)
```

## Schreiben in einen Datensatz

Mithilfe Ihrer `configProperties` Zuordnung können Sie in Experience Platform mit `QSOption`Daten in einen Datensatz schreiben.

```scala
val serviceToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ML_TOKEN", "").toString
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.serviceToken, serviceToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Nächste Schritte

Adobe Experience Platform Data Science Workspace bietet ein Scala-(Spark-)Rezept-Beispiel, das die oben genannten Codebeispiele zum Lesen und Schreiben von Daten verwendet. Wenn Sie mehr darüber erfahren möchten, wie Sie mit Spark auf Ihre Daten zugreifen können, lesen Sie bitte das [Data Science Workspace Scala GitHub Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).