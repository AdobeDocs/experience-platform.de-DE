---
keywords: Experience Platform; Startseite; beliebte Themen; Datenzugriff; Spark-SDK; Datenzugriffs-API; Funkrezept; Lese-Funken; Schreibfunken
solution: Experience Platform
title: Zugreifen auf Daten mithilfe von Spark in Data Science Workspace
type: Tutorial
description: Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mit Spark zur Verwendung in Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Zugreifen auf Daten mithilfe von Spark in Data Science Workspace

Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mit Spark zur Verwendung in Data Science Workspace. Informationen zum Zugriff auf Daten mit JupyterLab-Notebooks finden Sie im [Datenzugriff auf JupyterLab Notebooks](../jupyterlab/access-notebook-data.md) Dokumentation.

## Erste Schritte

Verwenden [!DNL Spark] erfordert Leistungsoptimierungen, die zum `SparkSession`. Darüber hinaus können Sie auch `configProperties` für später zum Lesen und Schreiben in Datensätze.

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

Der interaktive Modus erstellt eine JDBC-Verbindung (Java Database Connectivity) zu [!DNL Query Service] und erhält Ergebnisse über reguläres JDBC `ResultSet` die automatisch in eine `DataFrame`. Dieser Modus funktioniert ähnlich wie der integrierte [!DNL Spark] method `spark.read.jdbc()`. Dieser Modus ist nur für kleine Datensätze vorgesehen. Wenn Ihr Datensatz 5 Millionen Zeilen überschreitet, wird empfohlen, in den Batch-Modus zu wechseln.

Der Batch-Modus verwendet [!DNL Query Service]den Befehl COPY , um Parquet-Ergebnissätze an einem freigegebenen Speicherort zu generieren. Diese Parquet-Dateien können dann weiter verarbeitet werden.

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

Ein Beispiel für die Verwendung der `distinct()` -Funktion finden Sie unten:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WHERE-Klausel

Die [!DNL Spark] SDK ermöglicht zwei Filtermethoden: Verwenden eines SQL-Ausdrucks oder Filtern durch Bedingungen.

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

Die &quot;ORDER BY&quot;-Klausel ermöglicht die Sortierung der empfangenen Ergebnisse nach einer bestimmten Spalte in einer bestimmten Reihenfolge (aufsteigend oder absteigend). Im [!DNL Spark] SDK: Dies erfolgt durch Verwendung des `sort()` -Funktion.

Ein Beispiel für die Verwendung der `sort()` -Funktion finden Sie unten:

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT-Klausel

Die LIMIT-Klausel ermöglicht es Ihnen, die Anzahl der vom Datensatz empfangenen Datensätze zu begrenzen.

Ein Beispiel für die Verwendung der `limit()` -Funktion finden Sie unten:

```scala
df = df.limit(100)
```

## Schreiben in einen Datensatz

Verwenden der `configProperties` -Zuordnung können Sie in einen Datensatz in Experience Platform schreiben, indem Sie `QSOption`.

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

Adobe Experience Platform Data Science Workspace bietet ein Scala-(Spark-)Rezept-Beispiel, das die oben genannten Codebeispiele zum Lesen und Schreiben von Daten verwendet. Wenn Sie mehr darüber erfahren möchten, wie Sie mit Spark auf Ihre Daten zugreifen können, lesen Sie bitte den Abschnitt [Data Science Workspace Scala GitHub-Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
