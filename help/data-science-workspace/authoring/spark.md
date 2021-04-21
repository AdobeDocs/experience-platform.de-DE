---
keywords: Experience Platform;Home;beliebte Themen;Datenzugriff;Funkk SDK;Datenzugriffs-API;Funkrezept;Lese-Funken;Schreibfunk
solution: Experience Platform
title: Zugriff auf Daten mithilfe von Spark in Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mit Spark zur Verwendung in Data Science Workspace.
exl-id: 9bffb52d-1c16-4899-b455-ce570d76d3b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Zugriff auf Daten mithilfe von Spark in Data Science Workspace

Das folgende Dokument enthält Beispiele für den Zugriff auf Daten mit Spark zur Verwendung in Data Science Workspace. Informationen zum Zugriff auf Daten mit JupyterLab-Notebooks finden Sie in der Dokumentation [JupyterLab-Notebook-Datenzugriff](../jupyterlab/access-notebook-data.md).

## Erste Schritte

Die Verwendung von [!DNL Spark] erfordert Leistungsoptimierungen, die dem `SparkSession` hinzugefügt werden müssen. Zusätzlich können Sie `configProperties` auch für später einrichten, um in Datasets zu lesen und zu schreiben.

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

Bei Verwendung von Spark haben Sie Zugriff auf zwei Lesemodi: interaktiv und stapelweise.

Der interaktive Modus erstellt eine JDBC-Verbindung (Java Database Connectivity) zu [!DNL Query Service] und ruft Ergebnisse über eine reguläre JDBC `ResultSet` ab, die automatisch in ein `DataFrame` übersetzt wird. Dieser Modus funktioniert ähnlich wie die integrierte [!DNL Spark]-Methode `spark.read.jdbc()`. Dieser Modus ist nur für kleine Datensätze vorgesehen. Wenn Ihr Datensatz 5 Millionen Zeilen überschreitet, sollten Sie in den Stapelmodus wechseln.

Der Stapelmodus verwendet den COPY-Befehl von [!DNL Query Service], um Ergebnissätze aus Parquet an einem freigegebenen Speicherort zu generieren. Diese Parquet-Dateien können dann weiter verarbeitet werden.

Nachfolgend sehen Sie ein Beispiel zum Lesen eines Datensatzes im interaktiven Modus:

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

Ein Beispiel für das Lesen eines Datensatzes im Stapelmodus ist nachfolgend dargestellt:

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

### Spalten aus dem Datensatz AUSWÄHLEN

```scala
df = df.select("column-a", "column-b").show()
```

### DISTINCT-Klausel

Mit der DISTINCT-Klausel können Sie alle eindeutigen Werte auf Zeilen-/Spaltenebene abrufen und alle Duplikat-Werte aus der Antwort entfernen.

Ein Beispiel für die Verwendung der Funktion `distinct()` ist unten aufgeführt:

```scala
df = df.select("column-a", "column-b").distinct().show()
```

### WO-Klausel

Das SDK [!DNL Spark] ermöglicht zwei Methoden zum Filtern: Verwenden eines SQL-Ausdrucks oder durch Filtern von Bedingungen.

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

Die ORDER BY-Klausel ermöglicht es, die empfangenen Ergebnisse in einer bestimmten Reihenfolge (aufsteigend oder absteigend) nach einer bestimmten Spalte zu sortieren. Im SDK [!DNL Spark] erfolgt dies mithilfe der Funktion `sort()`.

Ein Beispiel für die Verwendung der Funktion `sort()` ist unten aufgeführt:

```scala
df = df.sort($"column1", $"column2".desc)
```

### LIMIT-Klausel

Die LIMIT-Klausel ermöglicht es Ihnen, die Anzahl der vom Datensatz erhaltenen Datensätze zu begrenzen.

Ein Beispiel für die Verwendung der Funktion `limit()` ist unten aufgeführt:

```scala
df = df.limit(100)
```

## Schreiben in einen Datensatz

Mit Ihrer `configProperties`-Zuordnung können Sie mit `QSOption` in einen Datensatz in Experience Platform schreiben.

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

Adobe Experience Platform Data Science Workspace bietet ein Scala-(Spark-)Rezept-Beispiel, das die oben genannten Codebeispiele zum Lesen und Schreiben von Daten verwendet. Wenn Sie mehr darüber erfahren möchten, wie Sie mit Spark auf Ihre Daten zugreifen können, lesen Sie bitte das [Data Science Workspace Scala GitHub Repository](https://github.com/adobe/experience-platform-dsw-reference/tree/master/recipes/scala).
