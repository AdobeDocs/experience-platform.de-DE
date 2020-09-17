---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: JupyterLab-Benutzerhandbuch
topic: Overview
description: JupyterLab ist eine Web-basierte Benutzeroberfläche für Project Jupyter und ist eng in Adobe Experience Platform integriert. Sie bietet eine interaktive Entwicklungsumgebung für Datenwissenschaftler, die mit Jupyter-Notebooks, -Code und -Daten arbeiten möchten. In diesem Dokument erhalten Sie einen Überblick über JupyterLab und die Funktionen sowie Anleitungen zum Durchführen häufiger Aktionen.
translation-type: tm+mt
source-git-commit: d5e7679ac41fd476c77a98920d7f7aeaefacec6d
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 72%

---


# [!DNL JupyterLab] Benutzerhandbuch

[!DNL JupyterLab] ist eine Web-basierte Benutzeroberfläche für [Project Jupyter](https://jupyter.org/) und ist eng in Adobe Experience Platform integriert. Sie bietet eine interaktive Entwicklungsumgebung für Datenwissenschaftler, die mit Jupyter-Notebooks, -Code und -Daten arbeiten möchten.

This document provides an overview of [!DNL JupyterLab] and its features as well as instructions to perform common actions.

## [!DNL JupyterLab] on [!DNL Experience Platform]

Die JupyterLab-Integration mit Experience Platform wird von Architekturänderungen, Designüberlegungen, benutzerdefinierten Notebook-Erweiterungen, vorinstallierten Bibliotheken und einer Oberfläche im Stil von Adobe begleitet.

In der folgenden Liste werden einige der Funktionen vorgestellt, die bei JupyterLab auf Platform einzigartig sind:

| Funktion | Beschreibung |
| --- | --- |
| **Kernels** | Kernels provide notebook and other [!DNL JupyterLab] front-ends the ability to execute and introspect code in different programming languages. [!DNL Experience Platform] bietet zusätzliche Kernel zur Unterstützung der Entwicklung in [!DNL Python], R, PySpark und [!DNL Spark]. Weiterführende Informationen finden Sie im Abschnitt [Kernels](#kernels). |
| **Datenzugriff** | Access existing datasets directly from within [!DNL JupyterLab] with full support for read and write capabilities. |
| **[!DNL Platform]Dienstintegration** | Built-in integrations allows you to utilize other [!DNL Platform] services directly from within [!DNL JupyterLab]. Eine vollständige Liste der unterstützten Integrationen finden Sie im Abschnitt zur [Integration mit anderen Platform-Diensten](#service-integration). |
| **Authentifizierung** | Zusätzlich zum <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">nativen Sicherheitsmodell von JupyterLab</a> wird jede Interaktion zwischen Ihrer Anwendung und Experience Platform, einschließlich der Kommunikation zwischen Platform-Diensten, über das <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a> verschlüsselt und authentifiziert. |
| **Entwicklungsbibliotheken** | In [!DNL Experience Platform]bietet [!DNL JupyterLab] vorinstallierte Bibliotheken für [!DNL Python], R und PySpark. Eine vollständige Liste der unterstützten Bibliotheken finden Sie im [Anhang](#supported-libraries). |
| **Bibliotheks-Controller** | When the the pre-installed libraries are lacking for your needs, additional libraries can be installed for Python and R, and are temporarily stored in isolated containers to maintain the integrity of [!DNL Platform] and keep your data safe. Weiterführende Informationen finden Sie im Abschnitt [Kernels](#kernels). |

>[!NOTE]
>
> Zusätzliche Bibliotheken sind nur für die Sitzung verfügbar, in der sie installiert werden. Wenn Sie neue Sitzungen starten, müssen Sie alle zusätzlichen Bibliotheken, die Sie benötigen, neu installieren.

## Integration with other [!DNL Platform] services {#service-integration}

Standardization and interoperability are key concepts behind [!DNL Experience Platform]. The integration of [!DNL JupyterLab] on [!DNL Platform] as an embedded IDE allows it to interact with other [!DNL Platform] services, enabling you to utilize [!DNL Platform] to its full potential. The following [!DNL Platform] services are available in [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Aufrufen und Erkunden von Datensätzen mit Lese- und Schreibfunktionen.
* **[!DNL Query Service]:** Aufrufen und Erkunden von Datensätzen mit SQL, wodurch sich beim Datenzugriff bei großen Datenmengen der Overhead verringert.
* **[!DNL Sensei ML Framework]:** Modellentwicklung mit der Möglichkeit, Daten zu trainieren und zu bewerten, sowie Rezepterstellung mit einem Klick.
* **[!DNL Experience Data Model (XDM)]:** Normung und Interoperabilität sind Schlüsselkonzepte für Adobe Experience Platform. [Erlebnis-Datenmodell (XDM)](https://www.adobe.com/go/xdm-home-en), angetrieben von Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

>[!NOTE]
>
>Some [!DNL Platform] service integrations on [!DNL JupyterLab] are limited to specific kernels. Weiterführende Informationen finden Sie im Abschnitt [Kernels](#kernels).

## Wichtigste Funktionen und allgemeine Vorgänge

Information regarding key features of [!DNL JupyterLab] and instructions on performing common operations are provided in the sections below:

* [Zugriff auf JupyterLab](#access-jupyterlab)
* [Oberfläche von JupyterLab](#jupyterlab-interface)
* [Code-Zellen](#code-cells)
* [Kernels](#kernels)
* [Kernel-Sitzungen](#kernel-sessions)
* [Starter](#launcher)

### Zugriff auf [!DNL JupyterLab] {#access-jupyterlab}

Wählen Sie in [Adobe Experience Platform](https://platform.adobe.com)in der linken Navigationsspalte **Notebooks** aus. Allow some time for [!DNL JupyterLab] to fully initialize.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] Benutzeroberfläche {#jupyterlab-interface}

The [!DNL JupyterLab] interface consists of a menu bar, a collapsible left sidebar, and the main work area containing tabs of documents and activities.

**Menüleiste**

The menu bar at the top of the interface has top-level menus that expose actions available in [!DNL JupyterLab] with their keyboard shortcuts:

* **Datei:** Aktionen im Zusammenhang mit Dateien und Ordnern
* **Bearbeiten:** Aktionen im Zusammenhang mit der Bearbeitung von Dokumenten und anderen Aktivitäten
* **Ansicht:** Aktionen, die das Erscheinungsbild von ändern[!DNL JupyterLab]
* **Ausführen:** Aktionen zum Ausführen von Code in verschiedenen Aktivitäten, wie z. B. Notebooks und Code-Konsolen
* **Kernel:** Aktionen zum Verwalten von Kerneln
* **Registerkarten:** Eine Liste offener Dokumente und Aktivitäten
* **Einstellungen:** Allgemeine Einstellungen und ein Editor für erweiterte Einstellungen
* **Hilfe:**[!DNL JupyterLab] Eine Liste von - und Kernel-Hilfe-Links

**Linke Seitenleiste**

Die linke Seitenleiste enthält anklickbare Registerkarten, die Zugriff auf folgende Funktionen bieten:

* **Datei-Browser:** Eine Liste gespeicherter Notebook-Dokumente und -Verzeichnisse
* **Data Explorer:** Durchsuchen, Aufrufen und Erforschen von Datensätzen und Schemas
* **Laufende Kernel und Terminals:** Eine Liste von aktiven Kernel- und Terminal-Sitzungen mit der Möglichkeit zum Beenden
* **Befehle:** Eine Liste mit hilfreichen Befehlen
* **Zellinspektor:** Ein Zelleneditor, der Zugriff auf Tools und Metadaten bietet, die für die Einrichtung eines Notebooks zu Präsentationszwecken nützlich sind
* **Registerkarten:** Eine Liste offener Registerkarten

Klicken Sie auf eine Registerkarte, um deren Funktionen anzuzeigen, oder klicken Sie auf eine erweiterte Registerkarte, um die linke Seitenleiste wie unten gezeigt zu reduzieren:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Hauptarbeitsbereich**

The main work area in [!DNL JupyterLab] enables you to arrange documents and other activities into panels of tabs that can be resized or subdivided. Ziehen Sie eine Registerkarte in die Mitte eines Registerkarten-Panels, um die Registerkarte zu verschieben. Unterteilen Sie ein Panel durch Ziehen einer Registerkarte nach links, rechts, oben oder unten im Panel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Code-Zellen {#code-cells}

Code-Zellen sind der Hauptinhalt von Notebooks. Sie enthalten Quell-Code in der Sprache des Kernels vom Notebook und die Ausgabe als Ergebnis der Ausführung der Code-Zelle. Rechts neben jeder Code-Zelle, die die Ausführungsreihenfolge darstellt, wird ein Ausführungszähler angezeigt.

![](../images/jupyterlab/user-guide/code_cell.png)

Häufige Zellaktionen werden nachfolgend beschrieben:

* **Zelle hinzufügen:** Klicken Sie im Notebook-Menü auf das Pluszeichen (**+**), um eine leere Zelle hinzuzufügen. Neue Zellen werden unter der Zelle platziert, mit der derzeit interagiert wird, oder am Ende des Notebooks, wenn keine bestimmte Zelle im Fokus ist.

* **Zelle verschieben:** Platzieren Sie den Cursor rechts neben der Zelle, die Sie verschieben möchten, und ziehen Sie die Zelle dann an eine neue Position. Wenn Sie eine Zelle von einem Notebook in ein anderes verschieben, wird die Zelle zusammen mit ihrem Inhalt repliziert.

* **Zelle ausführen:** Klicken Sie auf den Text der Zelle, die Sie ausführen möchten, und klicken Sie dann auf das **Wiedergabesymbol** (**▶**) im Notebook-Menü. Im Ausführungszähler der Zelle wird ein Sternchen (**\***) angezeigt, wenn der Kernel die Ausführung verarbeitet, und nach Abschluss durch eine Ganzzahl ersetzt.

* **Zelle löschen:** Klicken Sie auf den Text der Zelle, die Sie löschen möchten, und klicken Sie dann auf das Symbol **Schere**.

### Kernels {#kernels}

Notebook-Kernel sind sprachspezifische Rechen-Engines zur Verarbeitung von Notebook-Zellen. In addition to [!DNL Python], [!DNL JupyterLab] provides additional language support in R, PySpark, and [!DNL Spark] (Scala). Wenn Sie ein Notebook-Dokument öffnen, wird der zugehörige Kernel gestartet. Wenn eine Notebook-Zelle ausgeführt wird, führt der Kernel die Berechnung durch und erzeugt Ergebnisse, die erhebliche CPU- und Arbeitsspeicherressourcen beanspruchen können. Beachten Sie, dass zugewiesener Arbeitsspeicher erst freigegeben wird, wenn der Kernel heruntergefahren wird.

Bestimmte Funktionen und Funktionen sind auf bestimmte Kernels beschränkt, wie in der folgenden Tabelle beschrieben:

| Kernel | Installationsunterstützung für Bibliotheken | [!DNL Platform] Integrationen |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Nein | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Kernel-Sitzungen {#kernel-sessions}

Each active notebook or activity on [!DNL JupyterLab] utilizes a kernel session. Alle aktiven Sitzungen finden Sie, indem Sie auf der linken Seitenleiste die Registerkarte **Laufende Terminals und Kernel** erweitern. Typ und Zustand des Kernels eines Notebooks finden Sie in der oberen rechten Ecke der Notebook-Oberfläche. In der Abbildung unten ist der zugehörige Kernel des Notebooks **[!DNL Python]3** und der aktuelle Status wird durch einen grauen Kreis rechts dargestellt. Ein leerer Kreis impliziert einen Kernel im Leerlauf, während ein ausgefüllter Kreis einen aktiven Kernel darstellt.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Wenn der Kernel heruntergefahren wurde oder über einen längeren Zeitraum inaktiv war, dann wird **Kein Kernel!** mit einem ausgefüllten Kreis angezeigt. Aktivieren Sie einen Kernel, indem Sie auf den Kernel-Status klicken und den entsprechenden Kernel-Typ auswählen, wie unten gezeigt:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Starter {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Der angepasste *Starter* bietet nützliche Notebook-Vorlagen für die unterstützten Kernels, die Ihnen helfen, mit Ihrer Aufgabe zu beginnen, darunter:

| Vorlage | Beschreibung |
| --- | --- |
| Leer | Eine leere Notebook-Datei. |
| Starter | Ein vorausgefülltes Notebook, das die Datenerfassung anhand von Musterdaten demonstriert. |
| Einzelhandelsumsätze | A pre-filled notebook featuring the [retail sales recipe](https://docs.adobe.com/content/help/de-DE/experience-platform/data-science-workspace/home.translate.html#!api-specification/markdown/narrative/technical_overview/data_science_workspace_overview/dsw_prebuilt_recipes/retail_sales_recipe/retail_sales_recipe.md) using sample data. |
| Recipe Builder | Eine Notebook-Vorlage zum Erstellen eines Rezepts in [!DNL JupyterLab]. Sie ist mit Code und Kommentaren vorausgefüllt, die die Erstellung von Rezepten demonstrieren und beschreiben. Eine ausführliche Vorgehensweise finden Sie im Tutorial [Notebook an Rezept](https://docs.adobe.com/content/help/de-DE/experience-platform/data-science-workspace/jupyterlab/create-a-recipe.html). |
| [!DNL Query Service] | A pre-filled notebook demonstrating the usage of [!DNL Query Service] directly in [!DNL JupyterLab] with provided sample workflows that analyzes data at scale. |
| ExperienceEvents | Ein vorausgefülltes Notebook, das die Datenerkundung bei Nachwertdaten von Erlebnisereignissen demonstriert und sich auf Funktionen konzentriert, die in der ganzen Datenstruktur einheitlich sind. |
| XDM Queries | Ein vorausgefülltes Notebook, das geschäftliche Beispielabfragen zu Erlebnisereignisdaten veranschaulicht. |
| Aggregation | Ein vorausgefülltes Notebook, das Beispiel-Workflows zur Aggregation großer Datenmengen in kleineren, besser handhabbaren Blöcken veranschaulicht. |
| Clustering | Ein vorausgefülltes Notebook, das die durchgängige Modellierung für maschinellen Lernen mithilfe von Clustering-Algorithmen demonstriert. |

Einige Notebook-Vorlagen sind auf bestimmte Kernels beschränkt. Die Vorlagenverfügbarkeit für jeden Kernel wird in der folgenden Tabelle dargestellt:

<table>
    <tr>
        <td></td>
        <th><strong>Leer</strong></th>
        <th><strong>Starter</strong></th>
        <th><strong>Einzelhandelsumsätze</strong></th>
        <th><strong>Recipe Builder</strong></th>
        <th><strong>[!DNL Abfrage Service]</strong></th>
        <th><strong>ExperienceEvents</strong></th>
        <th><strong>XDM Queries</strong></th>
        <th><strong>Aggregation</strong></th>
        <th><strong>Clustering</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >ja</td>
        <td >ja</td>
        <td >ja</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 ([!DNL Spark] 2.4)</strong></th>
        <td >nein</td>
        <td >ja</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
        <td >ja</td>
        <td >ja</td>
        <td >nein</td>
    </tr>
    <tr>
        <th ><strong>Scala</strong></th>
        <td >ja</td>
        <td >ja</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
        <td >nein</td>
        <td >ja</td>
    </tr>
</table>

Um einen neuen *Starter* zu öffnen, klicken Sie auf **Datei > Neuer Starter**. Alternativ können Sie den **Datei-Browser** in der linken Seitenleiste erweitern und auf das Pluszeichen (**+**) klicken:

![](../images/jupyterlab/user-guide/new_launcher.gif)

### GPU- und Speicherserverkonfiguration in [!DNL Python]/R

Wählen Sie [!DNL JupyterLab] das Zahnradsymbol in der oberen rechten Ecke aus, um die *Notebook-Serverkonfiguration* zu öffnen. Mit dem Schieberegler können Sie die GPU aktivieren und die benötigte Speichermenge zuweisen. Wie viel Arbeitsspeicher Sie zuweisen können, hängt davon ab, wie viel Arbeitsspeicher Ihr Unternehmen bereitgestellt hat. Wählen Sie **[!UICONTROL Zu speichernde Konfigurationen]** aktualisieren.

>[!NOTE]
>
>Pro Unternehmen wird nur eine GPU für Notebooks bereitgestellt. Wenn die GPU in Gebrauch ist, müssen Sie warten, bis der Benutzer, der die GPU derzeit reserviert hat, sie freigegeben hat. Dies ist möglich, indem Sie sich abmelden oder die GPU für vier oder mehr Stunden im Leerlauf lassen.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## Nächste Schritte

Weitere Informationen zu den einzelnen unterstützten Notebooks und deren Verwendung finden Sie im [Jupyterlab-Handbuch für den Datenzugriff](./access-notebook-data.md) auf Notebooks. Dieser Leitfaden konzentriert sich darauf, wie Sie mit JupyterLab-Notebooks auf Ihre Daten zugreifen können, einschließlich Lesen, Schreiben und Abfragen von Daten. Die Anleitung zum Datenzugriff enthält außerdem Informationen zur maximalen Datenmenge, die von jedem unterstützten Notebook gelesen werden kann.

## Unterstützte Bibliotheken {#supported-libraries}

### [!DNL Python] / R

| Bibliothek | Version |
| :------ | :------ |
| notebook | 6.0.0 |
| requests | 2.22.0 |
| plotly | 4.0.0 |
| folium | 0.10.0 |
| ipywidgets | 7.5.1 |
| bokeh | 1.3.1 |
| gensim | 3.7.3 |
| ipyparallel | 0.5.2 |
| jq | 1,6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| pandas | 0.22.0 |
| pandasql | 0.7.3 |
| pillow | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| scipy | 1.3.0 |
| scrapy | 1.3.0 |
| seaborn | 0.9.0 |
| statsmodels | 0.10.1 |
| elastic | 5.1.0.17 |
| ggplot | 0.11.5 |
| py-xgboost | 0,90 |
| opencv | 3.4.1 |
| pyspark | 2.4.3 |
| pytorch | 1.0.1 |
| wxpython | 4.0.6 |
| colorlover | 0.3.0 |
| geopandas | 0.5.1 |
| pyshp | 2.1.0 |
| shapely | 1.6.4 |
| rpy2 | 2.9.4 |
| r-essentials | 3,6 |
| r-arules | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-ggthemes | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| r-leaps | 3,0 |
| r-manipulate | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| r-survival | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| r-quadprog | 1.5_7 |
| r-rjson | 0.2.20 |
| r-forecast | 8,7 |
| r-rsolnp | 1,16 |
| r-reticulate | 1,12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| r-corrplot | 0,84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-randomforest | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| pymongo | 3.8.0 |
| pyarrow | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| fastparquet | 0.3.2 |
| python-snappy | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| graphviz | 2.40.1 |
| python-graphviz | 0.11.1 |
| azure-storage | 0.36.0 |
| [!DNL jupyterlab] | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| mock | 3.0.5 |
| ipympl | 0.3.3 |
| fonts-anacond | 1,0 |
| psycopg2 | 2.8.3 |
| nose | 1.3.7 |
| autovizwidget | 0.12.9 |
| altair | 3.1.0 |
| vega_datasets | 0.7.0 |
| papermill | 1.0.1 |
| sql_magic | 0.0.4 |
| iso3166 | 1,0 |
| nbimporter | 0.3.1 |

### PySpark

| Bibliothek | Version |
| :------ | :------ |
| requests | 2.18.4 |
| gensim | 2.3.0 |
| keras | 2.0.6 |
| nltk | 3.2.4 |
| pandas | 0.20.1 |
| pandasql | 0.7.3 |
| pillow | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| scipy | 0.19.1 |
| scrapy | 1.3.3 |
| statsmodels | 0.8.0 |
| elastic | 4.0.30.44 |
| py-xgboost | 0,60 |
| opencv | 3.1.0 |
| pyarrow | 0.8.0 |
| boto3 | 1.5.18 |
| azure-storage-blob | 1.4.0 |
| [!DNL python] | 3.6.7 |
| mkl-rt | 11,1 |