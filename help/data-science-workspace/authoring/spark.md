---
keywords: Experience Platform;Startseite;beliebte Themen;Datenzugriff;Spark SDK;Datenzugriffs-API;Spark-Rezept;Spark lesen;Spark schreiben
solution: Experience Platform
title: Zugreifen auf Daten mithilfe von Spark in Data Science Workspace
type: Tutorial
description: Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mithilfe von Spark zur Verwendung in Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Zugreifen auf Daten mithilfe von Spark in Data Science Workspace

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mithilfe von Spark zur Verwendung in Data Science Workspace. Informationen zum Datenzugriff mithilfe von JupyterLab-Notebooks finden Sie in der Dokumentation [Datenzugriff über JupyterLab-Notebooks](../jupyterlab/access-notebook-data.md).

## Erste Schritte

Die Verwendung von [!DNL Spark] erfordert Leistungsoptimierungen, die der `SparkSession` hinzugefügt werden müssen. Darüber hinaus können Sie auch `configProperties` für später zum Lesen und Schreiben in Datensätze einrichten.

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

## Lesen eines Datensatzes

Bei Verwendung von Spark haben Sie Zugriff auf zwei Lesemodi: interaktiv und Batch.

Der interaktive Modus erstellt eine JDBC-Verbindung (Java Database Connectivity) zu [!DNL Query Service] und erhält Ergebnisse über eine reguläre JDBC-`ResultSet`, die automatisch in eine `DataFrame` übersetzt wird. Dieser Modus funktioniert ähnlich wie die integrierte [!DNL Spark]-`spark.read.jdbc()`. Dieser Modus ist nur für kleine Datensätze vorgesehen. Wenn Ihr Datensatz 5 Millionen Zeilen überschreitet, wird empfohlen, in den Batch-Modus zu wechseln.

Im Batch-Modus werden mit dem Befehl KOPIEREN von [!DNL Query Service] Parquet-Ergebnissätze an einem freigegebenen Speicherort generiert. Diese Parquet-Dateien können dann weiter verarbeitet werden.

Ein Beispiel für das Lesen eines Datensatzes im interaktiven Modus finden Sie unten:

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

### Spalten aus dem Datensatz auswählen

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

Die [!DNL Spark] SDK ermöglicht zwei Filtermethoden: Verwenden eines SQL-Ausdrucks oder Filtern nach Bedingungen.

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

Die ORDER BY-Klausel ermöglicht es, die empfangenen Ergebnisse nach einer angegebenen Spalte in einer bestimmten Reihenfolge (aufsteigend oder absteigend) zu sortieren. In der [!DNL Spark] SDK erfolgt dies mithilfe der `sort()`.

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `sort()` :

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT-Klausel

Mit der LIMIT-Klausel können Sie die Anzahl der vom Datensatz empfangenen Datensätze begrenzen.

Nachfolgend finden Sie ein Beispiel für die Verwendung der Funktion `limit()` :

```scala
df = df.limit(100)
```

## Schreiben in einen Datensatz

Mit Ihrer `configProperties` können Sie mit `QSOption` in einen Datensatz auf Experience Platform schreiben.

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

Adobe Experience Platform Data Science Workspace bietet ein Scala (Spark)-Rezeptbeispiel, das die obigen Codebeispiele zum Lesen und Schreiben von Daten verwendet. Weitere Informationen zur Verwendung von Spark für den Zugriff auf Ihre Daten finden Sie im [Data Science Workspace Scala GitHub-Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
