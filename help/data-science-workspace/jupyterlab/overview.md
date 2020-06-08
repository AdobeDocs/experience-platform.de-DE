---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: JupyterLab-Benutzerhandbuch
topic: Overview
translation-type: tm+mt
source-git-commit: f2a7300d4ad75e3910abbdf2ecc2946a2dfe553c
workflow-type: tm+mt
source-wordcount: '2773'
ht-degree: 6%

---


# JupyterLab-Benutzerhandbuch

JupyterLab ist eine webbasierte Benutzeroberfläche für <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> und ist fest in [!DNL Adobe Experience Platform]integriert. Es bietet eine interaktive Entwicklungs-Umgebung für Datenwissenschaftler, die mit Jupyter-Notebooks, -Codes und -Daten arbeiten können.

In diesem Dokument erhalten Sie einen Überblick über JupyterLab und seine Funktionen sowie Anleitungen zum Durchführen gemeinsamer Aktionen.

## JupyterLab auf Experience Platform

Die JupyterLab-Integration der Experience Platform wird von Architekturänderungen, Designüberlegungen, benutzerdefinierten Notebook-Erweiterungen, vorinstallierten Bibliotheken und einer Oberfläche zum Thema Adobe begleitet.

In der folgenden Liste werden einige der Funktionen vorgestellt, die für JupyterLab auf Plattform einzigartig sind:

| Funktion | Beschreibung |
| --- | --- |
| **Kernels** | Kernels bieten Notebook- und andere JupyterLab-Front-Ends die Möglichkeit, Code in verschiedenen Programmiersprachen auszuführen und zu überprüfen. Experience Platform bietet zusätzliche Kernel zur Unterstützung der Entwicklung in Python, R, PySpark und Spark. Weitere Informationen finden Sie im Abschnitt [Kernels](#kernels) . |
| **Datenzugriff** | Greifen Sie direkt von JupyterLab aus auf vorhandene Datensätze zu, und nutzen Sie die volle Unterstützung für Lese- und Schreibfunktionen. |
| **Integration von Plattformdiensten** | Mit integrierten Integrationen können Sie andere Plattformdienste direkt von JupyterLab aus nutzen. Eine vollständige Liste der unterstützten Integrationen finden Sie im Abschnitt zur [Integration mit anderen Plattformdiensten](#service-integration). |
| **Authentifizierung** | Zusätzlich zum integrierten Sicherheitsmodell <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">von</a>JupyterLab wird jede Interaktion zwischen Ihrer Anwendung und Experience Platform, einschließlich der Kommunikation zwischen Plattformservice und -service, über das <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>verschlüsselt und authentifiziert. |
| **Entwicklungsbibliotheken** | In Experience Platform stellt JupyterLab vorinstallierte Bibliotheken für Python, R und PySpark bereit. Eine vollständige Liste der unterstützten Bibliotheken finden Sie im [Anhang](#supported-libraries) . |
| **Bibliothekscontroller** | Wenn die vorinstallierten Bibliotheken Ihren Anforderungen nicht entsprechen, können zusätzliche Bibliotheken für Python und R installiert und vorübergehend in isolierten Containern gespeichert werden, um die Integrität der Plattform zu wahren und die Sicherheit Ihrer Daten zu gewährleisten. Weitere Informationen finden Sie im Abschnitt [Kernels](#kernels) . |

>[!NOTE] Zusätzliche Bibliotheken sind nur für die Sitzung verfügbar, in der sie installiert wurden. Sie müssen alle zusätzlichen Bibliotheken, die Sie benötigen, neu installieren, wenn Sie neue Sitzungen starten.

## Integration mit anderen Plattformdiensten {#service-integration}

Standardisierung und Interoperabilität sind Schlüsselkonzepte der Experience Platform. Die Integration von JupyterLab auf der Plattform als eingebettete IDE ermöglicht es, mit anderen Plattformdiensten zu interagieren, sodass Sie die Plattform optimal nutzen können. Die folgenden Plattformdienste sind in JupyterLab verfügbar:

* **Katalogdienst:** Zugriff auf und Erforschung von Datensätzen mit Lese- und Schreibfunktionen.
* **Abfrage-Dienst:** Zugriff auf und Untersuchung von Datensätzen mit SQL, wodurch der Datenzugriff bei großen Datenmengen kostengünstiger wird.
* **Sensei-ML-Framework:** Modellentwicklung mit der Möglichkeit, Daten zu trainieren und zu bewerten, sowie Rezepterstellung mit einem Klick.

>[!NOTE] Einige Plattformdienstintegrationen auf JupyterLab sind auf bestimmte Kernels beschränkt. Weitere Informationen finden Sie im Abschnitt zu [Kerneln](#kernels) .

## Wichtige Funktionen und allgemeine Vorgänge

Informationen zu den wichtigsten Funktionen von JupyterLab und Anweisungen zur Durchführung gemeinsamer Vorgänge finden Sie in den folgenden Abschnitten:

* [Zugriff auf JupyterLab](#access-jupyterlab)
* [JupyterLab-Schnittstelle](#jupyterlab-interface)
* [Codezellen](#code-cells)
* [Kernels](#kernels)
* [Kernel-Sitzungen](#kernel-sessions)
* [Ausführungsressource PySpark/Spark](#execution-resource)
* [Starter](#launcher)

### Zugriff auf JupyterLab {#access-jupyterlab}

Wählen Sie in [Adobe Experience Platform](https://platform.adobe.com)in der linken Navigationsspalte die Option **Notebooks** . Warten Sie einige Zeit, bis JupyterLab vollständig initialisiert ist.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### JupyterLab-Schnittstelle {#jupyterlab-interface}

Die JupyterLab-Schnittstelle besteht aus einer Menüleiste, einer reduzierbaren linken Seitenleiste und dem Hauptarbeitsbereich mit Registerkarten von Dokumenten und Aktivitäten.

**Menüleiste**

Die Menüleiste oben auf der Oberfläche verfügt über Menüs der obersten Ebene, die die in JupyterLab verfügbaren Aktionen mit ihren Tastaturbefehlen aufdecken:

* **Datei:** Aktionen im Zusammenhang mit Dateien und Ordnern
* **Bearbeiten:** Aktionen im Zusammenhang mit der Bearbeitung von Dokumenten und anderen Aktivitäten
* **Ansicht:** Aktionen, die das Erscheinungsbild von JupyterLab ändern
* **Ausführen:** Aktionen zum Ausführen von Code in verschiedenen Aktivitäten, wie z. B. Notebooks und Codekonsolen
* **Kernel:** Aktionen zum Verwalten von Kerneln
* **Registerkarten:** Eine Liste offener Dokumente und Aktivitäten
* **Einstellungen:** Allgemeine Einstellungen und ein erweiterter Einstellungs-Editor
* **Hilfe:** Eine Liste von JupyterLab- und Kernel-Hilfe-Links

**Linke Seitenleiste**

Die linke Seitenleiste enthält anklickbare Registerkarten, die Zugriff auf die folgenden Funktionen bieten:

* **Dateibrowser:** Eine Liste gespeicherter Notebook-Dokumente und -Ordner
* **Data Explorer:** Durchsuchen, Zugreifen und Erforschen von Datensätzen und Schemas
* **Laufende Kernel und Terminals:** Eine Liste von aktiven Kernel- und Terminalsitzungen mit der Möglichkeit,
* **Befehle:** Eine Liste mit hilfreichen Befehlen
* **Zellinspektor:** Ein Zelleneditor, der Zugriff auf Werkzeuge und Metadaten bietet, die für die Einrichtung eines Notebooks zu Präsentationszwecken nützlich sind
* **Registerkarten:** Eine Liste offener Registerkarten

Klicken Sie auf eine Registerkarte, um deren Funktionen anzuzeigen, oder klicken Sie auf eine erweiterte Registerkarte, um die linke Seitenleiste wie unten gezeigt zu reduzieren:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Hauptarbeitsbereich**

Der Hauptarbeitsbereich in JupyterLab ermöglicht es Ihnen, Dokumente und andere Aktivitäten in Registerkartenbedienfelder anzuordnen, deren Größe angepasst oder unterteilt werden kann. Ziehen Sie eine Registerkarte in die Mitte eines Registerkartenbedienfelds, um die Registerkarte zu migrieren. Unterteilen eines Bedienfelds durch Ziehen einer Registerkarte nach links, rechts, oben oder unten im Bedienfeld:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Codezellen {#code-cells}

Codezellen sind der Hauptinhalt von Notebooks. Sie enthalten Quellcode in der Sprache des zugehörigen Kernels des Notebooks und die Ausgabe als Ergebnis der Ausführung der Codepelle. Rechts neben jeder Codezelle, die die Ausführungsreihenfolge darstellt, wird ein Ausführungszähler angezeigt.

![](../images/jupyterlab/user-guide/code_cell.png)

Häufige Zellaktionen werden nachfolgend beschrieben:

* **Hinzufügen einer Zelle:** Klicken Sie im Menü &quot;Notebook&quot;auf das Pluszeichen (+****), um eine leere Zelle hinzuzufügen. Neue Zellen werden unter der Zelle platziert, mit der derzeit interagiert wird, oder am Ende des Notebooks, wenn keine bestimmte Zelle im Fokus ist.

* **Zelle verschieben:** Platzieren Sie den Cursor rechts neben der Zelle, die Sie verschieben möchten, und ziehen Sie dann die Zelle an eine neue Position. Wenn Sie eine Zelle von einem Notebook auf ein anderes verschieben, wird die Zelle zusammen mit ihrem Inhalt repliziert.

* **Zelle ausführen:** Klicken Sie auf den Text der Zelle, die Sie ausführen möchten, und klicken Sie dann auf das Symbol **play** (**▶**) im Menü Notebook. Ein Sternchen (**\***) wird im Ausführungszähler der Zelle angezeigt, wenn der Kernel die Ausführung verarbeitet, und nach Abschluss wird eine Ganzzahl ersetzt.

* **Löschen einer Zelle:** Klicken Sie auf den Text der Zelle, die Sie löschen möchten, und klicken Sie dann auf das Symbol **Schere** .

### Kernels {#kernels}

Notebook-Kernel sind die sprachspezifischen Computing-Engines zur Verarbeitung von Notebook-Zellen. Zusätzlich zu Python bietet JupyterLab zusätzliche Sprachunterstützung in R, PySpark und Spark (Scala). Wenn Sie ein Notebook-Dokument öffnen, wird der zugehörige Kernel gestartet. Wenn eine Notebook-Zelle ausgeführt wird, führt der Kernel die Berechnung durch und erzeugt Ergebnisse, die erhebliche CPU- und Speicherressourcen beanspruchen können. Beachten Sie, dass zugewiesener Speicher erst freigegeben wird, wenn der Kernel heruntergefahren wird.

Bestimmte Funktionen und Funktionen sind auf bestimmte Kernels beschränkt, wie in der folgenden Tabelle beschrieben:

| Kernel | Bibliotheksinstallationsunterstützung | Plattformintegrationen |
| :----: | :--------------------------: | :-------------------- |
| **Python** | Ja | <ul><li>Sensei-ML-Framework</li><li>Katalogdienst</li><li>Abfrage</li></ul> |
| **R** | Ja | <ul><li>Sensei-ML-Framework</li><li>Katalogdienst</li></ul> |
| **Scala** | Nein | <ul><li>Sensei-ML-Framework</li><li>Katalogdienst</li></ul> |

### Kernel-Sitzungen {#kernel-sessions}

Jedes aktive Notebook oder jede Aktivität auf JupyterLab verwendet eine Kernelsitzung. Alle aktiven Sitzungen finden Sie in der linken Seitenleiste, indem Sie die Registerkarte **Laufende Terminals und Kernel** erweitern. Der Typ und der Zustand des Kernels eines Notebooks können durch Beobachtung der oberen rechten Ecke der Notebook-Oberfläche identifiziert werden. In der Abbildung unten ist der zugehörige Kernel des Notebooks **Python 3** und der aktuelle Status wird durch einen grauen Kreis rechts dargestellt. Ein leerer Kreis impliziert einen Leerlauf und ein ausgefüllter Kreis impliziert einen aktiven Kernel.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Wenn der Kernel über einen längeren Zeitraum heruntergefahren oder inaktiv ist, dann **Kein Kernel!** mit einem ausgefüllten Kreis angezeigt wird. Aktivieren Sie einen Kernel, indem Sie auf den Kernel-Status klicken und den entsprechenden Kernel-Typ auswählen, wie unten gezeigt:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Starter {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Der angepasste *Launcher* bietet nützliche Notebook-Vorlagen für die unterstützten Kernels, die Ihnen helfen, Ihre Aufgabe zu starten, darunter:

| Vorlage | Beschreibung |
| --- | --- |
| Leer | Eine leere Notebook-Datei. |
| Starter | Ein vorausgefülltes Notebook, das die Datenerfassung anhand von Musterdaten demonstriert. |
| Einzelhandel | Ein vorgefülltes Notebook mit dem <a href="https://adobe.ly/2wOgO3L" target="_blank">Einzelhandelsrezept</a> , das Beispieldaten verwendet. |
| Rezepturaufbau | Eine Notebook-Vorlage zum Erstellen eines Rezepts in JupyterLab. Es ist mit Code und Kommentaren vorausgefüllt, die den Rezepterstellungsprozess demonstrieren und beschreiben. Eine ausführliche exemplarische Vorgehensweise finden Sie im <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">Notebook</a> . |
| Abfrage | Ein vorausgefülltes Notebook, das die Verwendung von Abfrage Service direkt in JupyterLab demonstriert, mit Beispieldaten, Workflows die Daten im Maßstab analysieren. |
| XDM-Ereignisse | Ein vorausgefülltes Notebook, das die Datenforschung zu Experience Ereignis-Nachwertdaten demonstriert und sich auf Funktionen konzentriert, die in der Datenstruktur gemeinsam sind. |
| XDM-Abfragen | Ein vorausgefülltes Notebook, das Beispielgeschäftsdaten zu Experience Ereignis-Abfragen zeigt. |
| Aggregation | Ein vorausgefülltes Notebook, das Muster zeigt, Workflows große Datenmengen in kleinere, handhabbare Teile Aggregat. |
| Clustering | Ein vorausgefülltes Notebook, das die durchgängige Modellierung des maschinellen Lernens mithilfe von Clustering-Algorithmen demonstriert. |

Einige Notebook-Vorlagen sind auf bestimmte Kernels beschränkt. Die Vorlagenverfügbarkeit für jeden Kernel wird in der folgenden Tabelle zugeordnet:

<table>
    <tr>
        <td></td>
        <th><strong>Leer</strong></th>
        <th><strong>Starter</strong></th>
        <th><strong>Einzelhandel</strong></th>
        <th><strong>Rezepturaufbau</strong></th>
        <th><strong>Abfrage</strong></th>
        <th><strong>XDM-Ereignisse</strong></th>
        <th><strong>XDM-Abfragen</strong></th>
        <th><strong>Aggregation</strong></th>
        <th><strong>Clustering</strong></th>
    </tr>
    <tr>
        <th><strong>Python</strong></th>
        <td >yes</td>
        <td >yes</td>
        <td >yes</td>
        <td >yes</td>
        <td >yes</td>
        <td >yes</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >yes</td>
        <td >yes</td>
        <td >yes</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 (Spark 2.4)</strong></th>
        <td >no</td>
        <td >yes</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >yes</td>
        <td >yes</td>
        <td >no</td>
    </tr>
    <tr>
        <th ><strong>Scala</strong></th>
        <td >yes</td>
        <td >yes</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >no</td>
        <td >yes</td>
    </tr>
</table>

Um einen neuen *Starter* zu öffnen, klicken Sie auf **Datei > Neuer Starter**. Alternativ können Sie den **Dateibrowser** aus der linken Seitenleiste erweitern und auf das Pluszeichen (**+**) klicken:

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Zugriff auf Plattformdaten mit Notebooks

Jeder unterstützte Kernel bietet integrierte Funktionen, mit denen Sie Plattformdaten aus einem Datensatz in einem Notebook lesen können. Die Unterstützung für die Paginierung von Daten ist jedoch auf Python- und R-Notebooks beschränkt.

### Aus einem Datensatz in Python/R lesen

Mit Python- und R-Notebooks können Sie Daten beim Zugriff auf Datensätze paginieren. Nachstehend finden Sie Beispielcode zum Lesen von Daten mit und ohne Paginierung.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Aus einem Datensatz in Python/R ohne Paginierung lesen

Wenn Sie den folgenden Code ausführen, wird der gesamte Datensatz gelesen. Bei erfolgreicher Ausführung werden die Daten als Pandas-Datenformat gespeichert, auf das die Variable verweist `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`: Die eindeutige Identität des Datensatzes, auf den zugegriffen werden soll

#### Aus einem Datensatz in Python/R mit Paginierung lesen

Wenn Sie den folgenden Code ausführen, werden Daten aus dem angegebenen Datensatz gelesen. Die Paginierung wird erreicht, indem die Daten über die Funktionen `limit()` bzw. über die Funktionen `offset()` verrechnet werden. Die Datenbegrenzung bezieht sich auf die maximale Anzahl der zu lesenden Datenpunkte, während die Verrechnung auf die Anzahl der Datenpunkte verweist, die vor dem Lesen von Daten übersprungen werden sollen. Wenn der Lesevorgang erfolgreich ausgeführt wird, werden die Daten als Pandas-Datenpfad gespeichert, auf den die Variable verweist `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`: Die eindeutige Identität des Datensatzes, auf den zugegriffen werden soll

### Aus einem Datensatz in PySpark/Scala lesen

Wenn ein aktives PySpark- oder Scala-Notebook geöffnet ist, erweitern Sie die Registerkarte **Data Explorer** von der linken Seitenleiste und klicken Sie auf **Datasets** , um eine Liste verfügbarer Datensätze Ansicht. Klicken Sie mit der rechten Maustaste auf den Datensatz, auf den Sie zugreifen möchten, und klicken Sie auf Daten im Notebook **untersuchen**. Die folgenden Codezellen werden generiert:

#### PySpark (Spark 2.4) {#pyspark2.4}

Mit der Einführung von Spark 2.4 wird [`%dataset`](#magic) maßgeschneiderte Magie geliefert.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala (Spark 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>In Scala können Sie einen Wert deklarieren und `sys.env()` von innen zurückgeben `option`.

### Verwenden von %dataset magic in PySpark 3 (Spark 2.4) Notebooks {#magic}

Mit der Einführung von Spark 2.4 wird `%dataset` benutzerdefinierte Magie für den Einsatz in neuen PySpark 3 (Spark 2.4) Notebooks (Python 3 Kernel) geliefert.

**Nutzung**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Beschreibung**

Ein benutzerdefinierter Data Science Workspace magischer Befehl zum Lesen oder Schreiben eines Datensatzes von einem Python-Notebook (Python 3-Kernel).

* **{action}**: Der Aktionstyp, der für den Datensatz ausgeführt werden soll. Es stehen zwei Aktionen zur Verfügung: &quot;Lesen&quot;oder &quot;Schreiben&quot;.
* **—datasetId {id}**: Dient zum Bereitstellen der ID des zu lesenden oder zu schreibenden Datensatzes. Dies ist ein erforderliches Argument.
* **—dataFrame {df}**: Das Pandas-Datenblatt. Dies ist ein erforderliches Argument.
   * Wenn die Aktion &quot;gelesen&quot;ist, ist {df} die Variable, in der Ergebnisse des Datensatzlesevorgangs verfügbar sind.
   * Wenn die Aktion &quot;schreiben&quot;lautet, wird dieser Datenraum {df} in den Datensatz geschrieben.
* **—mode (optional)**: Zulässige Parameter sind &quot;batch&quot;und &quot;interaktiv&quot;. Standardmäßig ist der Modus auf &quot;interaktiv&quot;eingestellt. Es wird empfohlen, beim Lesen großer Datenmengen den Stapelmodus zu verwenden.

**Beispiele**

* **Beispiel** lesen: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Beispiel** schreiben: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### Abfrage von Daten mithilfe des Abfrage Service in Python

Mit JupyterLab on Platform können Sie SQL in einem Python-Notebook verwenden, um über den <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">Adobe Experience Platform Abfrage Service</a>auf Daten zuzugreifen. Der Zugriff auf Daten über den Abfrage Service kann aufgrund der höheren Laufzeiten bei der Bearbeitung großer Datensätze nützlich sein. Beachten Sie, dass die Datenabfrage mit Abfrage Service eine Verarbeitungszeit von 10 Minuten hat.

Bevor Sie den Abfrage Service in JupyterLab verwenden, sollten Sie sich mit der Syntax von <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">Abfrage Service SQL</a>vertraut machen.

Beim Abfragen von Daten mithilfe des Abfrage Service müssen Sie den Namen des Datasets der Zielgruppe angeben. Sie können die erforderlichen Codezellen generieren, indem Sie den gewünschten Datensatz mit dem **Data Explorer** suchen. Klicken Sie mit der rechten Maustaste auf die Datensatzliste und klicken Sie auf **Abfrage Data in Notebook** , um die beiden folgenden Codenzellen in Ihrem Notebook zu generieren:


Um den Abfrage Service in JupyterLab nutzen zu können, müssen Sie zunächst eine Verbindung zwischen Ihrem funktionierenden Python Notebook und dem Abfrage Service herstellen. Dies kann durch Ausführen der ersten generierten Zelle erreicht werden.

```python
qs_connect()
```

In der zweiten generierten Zelle muss die erste Zeile vor der SQL-Abfrage definiert werden. Standardmäßig definiert die generierte Zelle eine optionale Variable (`df0`), mit der die Abfragen als Pandas-Dataframe gespeichert werden. <br>Das `-c QS_CONNECTION` Argument ist obligatorisch und weist den Kernel an, die SQL-Abfrage gegen Abfrage Service auszuführen. Eine Liste weiterer Argumente finden Sie im [Anhang](#optional-sql-flags-for-query-service) .

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python-Variablen können direkt in einer SQL-Abfrage referenziert werden, indem Sie eine im Zeichenfolgenformat formatierte Syntax verwenden und die Variablen in geschweifte Klammern (`{}`) einschließen (siehe folgendes Beispiel):

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtern von ExperienceEvent-Daten in Python/R

Um auf einen ExperienceEvent-Datensatz in einem Python- oder R-Notebook zuzugreifen und ihn zu filtern, müssen Sie die ID des Datensatzes (`{DATASET_ID}`) zusammen mit den Filterregeln angeben, die einen bestimmten Zeitraum mithilfe logischer Operatoren definieren. Wenn ein Zeitraum definiert ist, wird jede angegebene Paginierung ignoriert und der gesamte Datensatz berücksichtigt.

Eine Liste der Filteroperatoren wird nachfolgend beschrieben:

* `eq()`: Gleich
* `gt()`: Größer als
* `ge()`: Größer oder gleich
* `lt()`: Niedriger als
* `le()`: Kleiner oder gleich
* `And()`: Logischer UND-Operator
* `Or()`: Logischer ODER-Operator

Die folgenden Zellen filtern einen ExperienceEvent-Datensatz nach Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existierten.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### Filtern von ExperienceEvent-Daten in PySpark/Spark

Für den Zugriff auf und das Filtern eines ExperienceEvent-Datensatzes in einem PySpark- oder Scala-Notebook müssen Sie die Dataset-Identität (`{DATASET_ID}`), die IMS-Identität Ihres Unternehmens und die Filterregeln, die einen bestimmten Zeitraum definieren, angeben. Ein Filterzeitbereich wird mithilfe der Funktion definiert, `spark.sql()`bei der der Funktionsparameter eine SQL-Abfrage-Zeichenfolge ist.

Die folgenden Zellen filtern einen ExperienceEvent-Datensatz nach Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existierten.

#### PySpark 3 (Spark 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### Scala (Spark 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>In Scala können Sie einen Wert deklarieren und `sys.env()` von innen zurückgeben `option`. Dadurch müssen Variablen nicht mehr definiert werden, wenn Sie wissen, dass sie nur einmal verwendet werden. Das folgende Beispiel nimmt `val userToken` das oben stehende Beispiel und deklariert es als Alternative in &quot;in&quot; `option` :
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

## Unterstützte Bibliotheken {#supported-libraries}

### Python / R

| Bibliothek | Version |
| :------ | :------ |
| Notebook | 6.0.0 |
| Anforderungen | 2.22.0 |
| plotly | 4.0.0 |
| Blattum | 0.10.0 |
| ipywidgets | 7.5.1 |
| bokeh | 1.3.1 |
| Gensim | 3.7.3 |
| ipyparallel | 0.5.2 |
| jq | 1,6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| Pandas | 0.22.0 |
| pandasql | 0.7.3 |
| Kissen | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| Skript | 1.3.0 |
| Scrapie | 1.3.0 |
| seaborn | 0.9.0 |
| statsmodels | 0.10.1 |
| elastisch | 5.1.0.17 |
| ggplot | 0.11.5 |
| py-xgpush | 0.90 |
| opencv | 3.4.1 |
| Pyspark | 2.4.3 |
| Pytorch | 1.0.1 |
| wxpython | 4.0.6 |
| colorlover | 0.3.0 |
| Geopandas | 0.5.1 |
| Pyshp | 2.1.0 |
| formell | 1.6.4 |
| rpy2 | 2.9.4 |
| Grundlagen | 3.6 |
| r-Artikel | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-gthemes | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| Re-Leaps | 3.0 |
| r-manipulieren | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-Überlebenszeit | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| r-Quadprog | 1.5_7 |
| r-rjson | 0.2.20 |
| r-prognose | 8.7 |
| r-rsolnp | 1.16 |
| r-reticulate | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-corplot | 0.84 |
| r-fnn | 1.1.3 |
| r-Schmiermittel | 1.7.4 |
| r-randomforest | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| Pymongo | 3.8.0 |
| pyarrow | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| fastparquet | 0.3.2 |
| Python-Schnappy | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| Azure-Datenspeicherung | 0.36.0 |
| Jupyterlab | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| mock | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
| Nase | 1.3.7 |
| autovizwidget | 0.12.9 |
| Alt | 3.1.0 |
| vega_datasets | 0.7.0 |
| Papierfräser | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1.0 |
| nbimporteur | 0.3.1 |

### PySpark

| Bibliothek | Version |
| :------ | :------ |
| Anforderungen | 2.18.4 |
| Gensim | 2.3.0 |
| keras | 2.0.6 |
| nltk | 3.2.4 |
| Pandas | 0.20.1 |
| pandasql | 0.7.3 |
| Kissen | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| Skript | 0.19.1 |
| Scrapie | 1.3.3 |
| statsmodels | 0.8.0 |
| elastisch | 4.0.30.44 |
| py-xgpush | 0.60 |
| opencv | 3.1.0 |
| pyarrow | 0.8.0 |
| boto3 | 1.5.18 |
| Azure-Datenspeicherung-Blob | 1.4.0 |
| Python | 3.6.7 |
| mkl-rt | 11.1 |

## Optionale SQL-Flags für den Abfrage-Dienst {#optional-sql-flags-for-query-service}

In dieser Tabelle sind die optionalen SQL-Flags aufgeführt, die für den Abfrage Service verwendet werden können.

| **Markierung** | **Beschreibung** |
| --- | --- |
| `-h`, `--help` | Hilfemeldung anzeigen und Beenden. |
| `-n`, `--notify` | Wechsel zur Option zum Benachrichtigen der Abfrage. |
| `-a`, `--async` | Die Verwendung dieses Flag führt die Abfrage asynchron aus und kann den Kernel freigeben, während die Abfrage ausgeführt wird. Seien Sie vorsichtig, wenn Sie Variablen Abfrage-Ergebnisse zuweisen, da sie möglicherweise nicht definiert sind, wenn die Abfrage nicht abgeschlossen ist. |
| `-d`, `--display` | Die Verwendung dieses Flag verhindert, dass Ergebnisse angezeigt werden. |

