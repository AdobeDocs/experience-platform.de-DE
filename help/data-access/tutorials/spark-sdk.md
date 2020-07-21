---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Secure Spark Data Access SDK
topic: tutorial
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 1%

---


# Sicheres [!DNL Spark Data Access] SDK

Das Secure [!DNL Spark][!DNL Data Access] SDK ist ein Softwareentwicklungs-Kit, das das Lesen und Schreiben von Datensätzen aus der Adobe Experience Platform ermöglicht.

## Erste Schritte

Sie müssen das [Authentifizierungs](../../tutorials/authentication.md) -Tutorial abgeschlossen haben, um Zugriff auf die Werte zu haben, mit denen das sichere [!DNL Spark] [!DNL Data Access] SDK aufgerufen werden kann:

- `{ACCESS_TOKEN}`
- `{API_KEY}`
- `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. Für die Verwendung des [!DNL Spark] SDK sind der Name und die ID der Sandbox erforderlich, in der der Vorgang ausgeführt wird:

- `{SANDBOX_NAME}`
- `{SANDBOX_ID}`

For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

## Umgebung einrichten

Das [!DNL Spark] SDK erwartet, dass Sie Anmeldeinformationen in Umgebung- oder Datenquellenoptionen angeben.

| Variable | Wert |
| -------- | ----- | 
| `SERVICE_TOKEN` | Ihr Dienstautorisierungstoken. |
| `SERVICE_API_KEY` | Ihr Dienst-API-Schlüssel. Dies ist im Allgemeinen mit Ihrer IMS-Client-ID identisch. |
| `ORG_ID` | Ihr `{IMS_ORG}` ID-Wert. |
| `USER_TOKEN` | Ihr `{ACCESS_TOKEN}` Wert. |

Weitere Konfigurationsparameter sind:

| Variable | Wert |
| -------- | ----- |
| `ENVIRONMENT_NAME` | Die Umgebung, mit der Sie eine Verbindung herstellen möchten. Es kann sich um &quot;dev&quot;, &quot;stage&quot;oder &quot;prod&quot;handeln. |
| `SANDBOX_NAME` | Der Name der Sandbox, mit der Sie eine Verbindung herstellen. |

Alternativ können Sie neben `ENVIRONMENT_NAME`den oben genannten Umgebung auch beliebige Variablen innerhalb `QSOption`einstellen, wie im folgenden Beispiel gezeigt:

```scala
val df = spark.read
    .format("com.adobe.platform.query")
    .option(QSOption.userToken, userToken) // same as env var USER_TOKEN
    .option(QSOption.imsOrg, "69A7534C5808063C0A494234@AdobeOrg") // same as env var ORG_ID
    .option(QSOption.apiKey, "acp_foundation_queryService") // same as env var SERVICE_API_KEY
    .option("mode", "interactive")
    .option("query", "SELECT * FROM csv10000row_xcm_001 LIMIT 10")
    .load()
```

## Installation

Die Verwendung des [!DNL Spark] SDK erfordert Leistungsoptimierungen, die dem `SparkSession`SDK hinzugefügt werden müssen. Sie können sie mit einer der folgenden Methoden anwenden:

Wenden Sie sie direkt auf die aktuelle SparkSession an:

```scala
import com.adobe.platform.query.QSOptimizations
QSOptimizations.apply(spark)
```

Legen Sie die folgende conf vor oder bei der Erstellung von SparkSession fest:

```scala
spark.sql.extensions = com.adobe.platform.query.QSSparkSessionExtensions
```

## Lesen eines Datensatzes

Das [!DNL Spark] SDK unterstützt zwei Lesemodi: interaktiv und stapelweise.

Im interaktiven Modus wird eine JDBC-Verbindung (Java Database Connectivity) erstellt [!DNL Query Service] und die Ergebnisse werden über eine reguläre JDBC-Verbindung abgerufen, `ResultSet` die automatisch in eine `DataFrame`übersetzt wird. Dieser Modus funktioniert ähnlich wie die integrierte [!DNL Spark] Methode `spark.read.jdbc()`. Dieser Modus ist nur für kleine Datensätze vorgesehen und erfordert nur ein Benutzertoken zur Authentifizierung.

Der Stapelmodus verwendet [!DNL Query Service]den COPY-Befehl, um Parquet-Ergebnismengen an einem freigegebenen Speicherort zu generieren. Diese Parquet-Dateien können dann weiter verarbeitet werden. Dieser Modus erfordert sowohl ein Benutzertoken als auch ein Diensttoken mit dem `acp.foundation.catalog.credentials` Gültigkeitsbereich.

Nachfolgend sehen Sie ein Beispiel zum Lesen eines Datensatzes im interaktiven Modus:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "interactive")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
```

Ein Beispiel für das Lesen eines Datensatzes im Stapelmodus ist nachfolgend dargestellt:

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", {IMS_ORG})
      .option("api-key", {SERVICE_API_KEY})
      .option("mode", "batch")
      .option("dataset-id", {DATASET_ID})
      .option("sandbox-name", {SANDBOX_NAME})
      .load()
df.show()
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

Die LIMIT-Klausel ermöglicht es Benutzern, die Anzahl der vom Datensatz erhaltenen Datensätze zu begrenzen.

Ein Beispiel für die Verwendung der `limit()` Funktion ist unten aufgeführt:

```scala
df = df.limit(100)
```

## Schreiben in einen Datensatz

Das [!DNL Spark] SDK unterstützt das Schreiben von Datensätzen. Die Benutzer müssen zunächst einen vorherigen Datensatz abrufen, um in einen neuen Datensatz zu schreiben.

```scala
val df = spark.read
      .format("com.adobe.platform.query")
      .option("user-token", userToken)
      .option("ims-org", "{IMS_ORG}")
      .option("api-key", "{API_KEY}")
      .option("mode", "interactive")
      .option("dataset-id", "{DATASET_ID}")
      .load()

    df.write
      .format("com.adobe.platform.query")
      .option("user-token", {USER_TOKEN})
      .option("service-token", {SERVICE_TOKEN})
      .option("ims-org", "{IMS_ORG_ID})
      .option("api-key", "{API_KEY}")
      .option("create-dataset", "{DATASET_ID}")
      .save()
```
