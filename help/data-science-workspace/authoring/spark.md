---
keywords: Experience Platform;home;popular topics;data access;spark sdk;data access api;spark recipe;read spark;write spark
solution: Experience Platform
title: Zugreifen auf Daten mithilfe von Spark in Data Science Workspace
type: Tutorial
description: Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mit Spark zur Verwendung in Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Zugriff auf Daten mithilfe von Spark in Data Science Workspace

Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mit Spark zur Verwendung in Data Science Workspace. Informationen zum Zugriff auf Daten mit JupyterLab-Notebooks finden Sie in der Dokumentation zum Datenzugriff auf JupyterLab-Notebooks ](../jupyterlab/access-notebook-data.md).[

## Erste Schritte

Die Verwendung von [!DNL Spark] erfordert Leistungsoptimierungen, die zum `SparkSession` hinzugefügt werden müssen. Außerdem können Sie `configProperties` für später einrichten, um in Datensätze zu lesen und zu schreiben.

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
            val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
            val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
            val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
            val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

   }
}
```

## Datensatz lesen

Bei Verwendung von Spark haben Sie Zugriff auf zwei Lesemodi: interaktiv und Batch.

Der interaktive Modus erstellt eine Java Database Connectivity (JDBC)-Verbindung zu [!DNL Query Service] und ruft Ergebnisse über eine reguläre JDBC `ResultSet` ab, die automatisch in eine `DataFrame` übersetzt wird. Dieser Modus funktioniert ähnlich wie die integrierte [!DNL Spark]-Methode `spark.read.jdbc()`. Dieser Modus ist nur für kleine Datensätze vorgesehen. Wenn Ihr Datensatz 5 Millionen Zeilen überschreitet, wird empfohlen, in den Batch-Modus zu wechseln.

Der Batch-Modus verwendet den Befehl COPY von [!DNL Query Service] , um Parquet-Ergebnismengen an einem freigegebenen Speicherort zu generieren. Diese Parquet-Dateien können dann weiter verarbeitet werden.

Nachfolgend finden Sie ein Beispiel für das Lesen eines Datensatzes im interaktiven Modus:

```scala
  // Read the configs
    val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
    val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
    val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
    val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString

 val dataSetId: String = configProperties.get(taskId).getOrElse("")

    // Load the dataset
    var df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
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

Ein Beispiel für das Lesen eines Datensatzes im Batch-Modus finden Sie unten:

```scala
val df = sparkSession.read.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.mode, "batch")
      .option(QSOption.datasetId, dataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .load()
    df.show()
    df
```

### Spalten aus Datensatz auswählen

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT-Klausel

Mit der DISTINCT-Klausel können Sie alle eindeutigen Werte auf Zeilen-/Spaltenebene abrufen und alle doppelten Werte aus der Antwort entfernen.

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `distinct()` :

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE-Klausel

Das SDK [!DNL Spark] ermöglicht zwei Filtermethoden: Verwendung eines SQL-Ausdrucks oder Filtern durch Bedingungen.

Nachfolgend finden Sie ein Beispiel für die Verwendung dieser Filterfunktionen:

#### SQL-Ausdruck

```scala
df.where("age > 15")
```

#### Filterbedingungen

```scala
df.where("age" > 15 || "name" = "Steve")
```

### ORDER BY-Klausel

Die &quot;ORDER BY&quot;-Klausel ermöglicht die Sortierung der empfangenen Ergebnisse nach einer bestimmten Spalte in einer bestimmten Reihenfolge (aufsteigend oder absteigend). Im [!DNL Spark] SDK erfolgt dies mithilfe der Funktion `sort()` .

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `sort()` :

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT-Klausel

Die LIMIT-Klausel ermöglicht es Ihnen, die Anzahl der vom Datensatz empfangenen Datensätze zu begrenzen.

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `limit()` :

```scala
df = df.limit(100)
```

## Schreiben in einen Datensatz

Mit Ihrer `configProperties` -Zuordnung können Sie mit `QSOption` in einen Datensatz unter Experience Platform schreiben.

```scala
val userToken: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_TOKEN", "").toString
val orgId: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_ORG_ID", "").toString
val apiKey: String = sparkSession.sparkContext.getConf.get("ML_FRAMEWORK_IMS_CLIENT_ID", "").toString
val sandboxName: String = sparkSession.sparkContext.getConf.get("sandboxName", "").toString 

    df.write.format(PLATFORM_SDK_PQS_PACKAGE)
      .option(QSOption.userToken, userToken)
      .option(QSOption.imsOrg, orgId)
      .option(QSOption.apiKey, apiKey)
      .option(QSOption.datasetId, scoringResultsDataSetId)
      .option(QSOption.sandboxName, sandboxName)
      .save()
```


## Nächste Schritte

Adobe Experience Platform Data Science Workspace bietet ein Scala-(Spark-)Rezept-Beispiel, das die oben genannten Codebeispiele zum Lesen und Schreiben von Daten verwendet. Wenn Sie mehr darüber erfahren möchten, wie Sie mit Spark auf Ihre Daten zugreifen können, lesen Sie bitte das [Data Science Workspace Scala GitHub-Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
