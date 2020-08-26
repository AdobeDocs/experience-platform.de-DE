---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: JupyterLab-Benutzerhandbuch
topic: Overview
description: JupyterLab ist eine Web-basierte Benutzeroberfläche für Project Jupyter und ist eng in Adobe Experience Platform integriert. Sie bietet eine interaktive Entwicklungsumgebung für Datenwissenschaftler, die mit Jupyter-Notebooks, -Code und -Daten arbeiten möchten.
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 56%

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
* [PySpark/Spark-Ausführungsressource](#execution-resource)
* [Starter](#launcher)

### Access [!DNL JupyterLab] {#access-jupyterlab}

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
| Einzelhandelsumsätze | Ein vorausgefülltes Notebook mit dem <a href="https://docs.adobe.com/content/help/de-DE/experience-platform/data-science-workspace/home.translate.html#!api-specification/markdown/narrative/technical_overview/data_science_workspace_overview/dsw_prebuilt_recipes/retail_sales_recipe/retail_sales_recipe.md" target="_blank">Rezept für Einzelhandelsumsätze</a>, inklusive Beispieldaten. |
| Recipe Builder | Eine Notebook-Vorlage zum Erstellen eines Rezepts in [!DNL JupyterLab]. Sie ist mit Code und Kommentaren vorausgefüllt, die die Erstellung von Rezepten demonstrieren und beschreiben. Eine ausführliche Vorgehensweise finden Sie im Tutorial <a href="https://docs.adobe.com/content/help/de-DE/experience-platform/data-science-workspace/jupyterlab/create-a-recipe.html" target="_blank">Notebook an Rezept</a>. |
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

## Access [!DNL Platform] data using Notebooks

Each supported kernel provides built-in functionalities that allow you to read [!DNL Platform] data from a dataset within a notebook. However, support for paginating data is limited to [!DNL Python] and R notebooks.

### Einschränkungen bei Notebook-Daten

Die folgenden Informationen definieren die maximale Datenmenge, die gelesen werden kann, welche Art von Daten verwendet wurde und den geschätzten Zeitrahmen, in dem die Daten gelesen werden. Für [!DNL Python] und R wurde ein mit 40 GB RAM konfigurierter Notebook-Server für die Benchmarks verwendet. Für PySpark und Scala wurde ein mit 64 GB RAM, 8 Kerne, 2 DBU mit maximal 4 Mitarbeitern konfigurierter Datenbankcluster für die unten beschriebenen Benchmarks verwendet.

Die verwendeten ExperienceEvent-Schema-Daten variierten in der Größe von 1.000 Zeilen bis zu einer Milliarde Zeilen (1B). Beachten Sie, dass für die PySpark- und [!DNL Spark] Metriken ein Datumsbereich von 10 Tagen für die XDM-Daten verwendet wurde.

Die Ad-hoc-Schema-Daten wurden vorab mit [!DNL Query Service] Tabelle als Auswahl erstellen (CTAS) verarbeitet. Diese Daten variierten auch in der Größe von 1.000 Zeilen (1.000) bis zu einer Milliarde (1.000) Zeilen.

#### [!DNL Python] Datenbeschränkungen für Notebooks

**XDM ExperienceEvent-Schema:** Sie sollten maximal 2 Millionen Zeilen (~6,1 GB Daten auf der Festplatte) XDM Daten in weniger als 22 Minuten lesen können. Das Hinzufügen zusätzlicher Zeilen kann zu Fehlern führen.

| Anzahl Zeilen | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Größe auf Festplatte (MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (in Sekunden) | 20.3 | 86.8 | 63 | 659 | 1315 |

**Ad-hoc-Schema:** Sie sollten maximal 5 Millionen Zeilen (~5,6 GB Daten auf der Festplatte) von Nicht-XDM-Daten (Ad-hoc-Daten) in weniger als 14 Minuten lesen können. Das Hinzufügen zusätzlicher Zeilen kann zu Fehlern führen.

| Anzahl Zeilen | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Größe auf Festplatte (in MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (in Sekunden) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### R Datenbeschränkungen für Notebooks

**XDM ExperienceEvent-Schema:** Sie sollten in weniger als 13 Minuten maximal 1 Million Zeilen XDM Daten (3 GB Daten auf Festplatte) lesen können.

| Anzahl Zeilen | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Größe auf Festplatte (MB) | 18.73 | 187.5 | 308 | 3000 |
| R Kernel (in Sekunden) | 14.03 | 69.6 | 86.8 | 775 |

**Ad-hoc-Schema:** Sie sollten in etwa 10 Minuten maximal 3 Millionen Zeilen Ad-hoc-Daten (293 MB Daten auf dem Datenträger) lesen können.

| Anzahl Zeilen | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Größe auf Festplatte (in MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| R SDK (in Sekunden) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### Datenbeschränkungen für PySpark-Notebooks ([!DNL Python] Kernel):

**XDM ExperienceEvent-Schema:** Im interaktiven Modus sollten Sie maximal 5 Millionen Zeilen (~13,42 GB Daten auf Festplatte) XDM Daten in etwa 20 Minuten lesen können. Der interaktive Modus unterstützt nur bis zu 5 Millionen Zeilen. Wenn Sie größere Datensätze lesen möchten, wird empfohlen, in den Stapelmodus zu wechseln. Im Batch-Modus sollten Sie maximal 500 Millionen Zeilen (~1,31 TB Daten auf der Festplatte) XDM Daten in etwa 14 Stunden lesen können.

| Anzahl Zeilen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Größe auf dem Datenträger | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK (interaktiver Modus) | 33 Sek. | 32.4 Sek. | 55.1 Sek. | 253.5 Sek. | 489.2 Sek. | 729.6 Sek. | 1206.8 Sek. | – | – | – | – |
| SDK (Stapelmodus) | 815.8 Sek. | 492.8 Sek. | 379.1 Sek. | 637.4 Sek. | 624.5 Sek. | 869.2 Sek. | 1104.1 Sek. | 1786 Sek. | 5387.2 Sek. | 10624.6 Sek. | 50547 Sek. |

**Ad-hoc-Schema:** Im interaktiven Modus sollten Sie maximal 1 Milliarde Zeilen (~1.05TB Daten auf Festplatte) von Nicht-XDM Daten in weniger als 3 Minuten lesen können. Im Batch-Modus sollten Sie maximal 1 Milliarde Zeilen (~1.05TB Daten auf Festplatte) von Nicht-XDM Daten in etwa 18 Minuten lesen können.

| Anzahl Zeilen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Größe auf Datenträger | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| SDK-Interaktiver Modus (in Sekunden) | 28.2 Sek. | 18.6 Sek. | 20.8 Sek. | 20.9 Sek. | 23.8 Sek. | 21.7 Sek. | 24.7 Sek. | 22 Sek. | 28.4 Sek. | 40 Sek. | 97.4 Sek. | 154.5 Sek. |
| SDK-Stapelmodus (in Sekunden) | 428.8 Sek. | 578.8 Sek. | 641.4 Sek. | 538.5 Sek. | 630.9 Sek. | 467.3 Sek. | 411 Sek. | 675 Sek. | 702 Sek. | 719.2 Sek. | 1022.1 Sek. | 1122.3 Sek. |

#### [!DNL Spark] (Scala-Kernel) Datenbeschränkungen für Notebooks:

**XDM ExperienceEvent-Schema:** Im interaktiven Modus sollten Sie maximal 5 Millionen Zeilen (~13,42 GB Daten auf Festplatte) XDM Daten in etwa 18 Minuten lesen können. Der interaktive Modus unterstützt nur bis zu 5 Millionen Zeilen. Wenn Sie größere Datensätze lesen möchten, wird empfohlen, in den Stapelmodus zu wechseln. Im Batch-Modus sollten Sie maximal 500 Millionen Zeilen (~1,31 TB Daten auf der Festplatte) XDM Daten in etwa 14 Stunden lesen können.

| Anzahl Zeilen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Größe auf Datenträger | 2.93MB | 4.38MB | 29.02 | 2.69 GB   | 5.39 GB   | 8.09 GB   | 13.42 GB   | 26.82 GB   | 134.24 GB   | 268.39 GB   | 1.31TB |
| SDK-Interaktiver Modus (in Sekunden) | 37.9 Sek. | 22.7 Sek. | 45.6 Sek. | 231.7 Sek. | 444.7 Sek. | 660.6 Sek. | 1100 Sek. | – | – | – | – |
| SDK-Stapelmodus (in Sekunden) | 374.4 Sek. | 398.5 Sek. | 527 Sek. | 487.9 Sek. | 588.9 Sek. | 829 Sek. | 939.1 Sek. | 1441 Sek. | 5473.2 Sek. | 10118.8 | 49207.6 |

**Ad-hoc-Schema:** Im interaktiven Modus sollten Sie maximal 1 Milliarde Zeilen (~1.05TB Daten auf Festplatte) von Nicht-XDM Daten in weniger als 3 Minuten lesen können. Im Batch-Modus sollten Sie maximal 1 Milliarde Zeilen (~1.05TB Daten auf Festplatte) von Nicht-XDM Daten in etwa 16 Minuten lesen können.

| Anzahl Zeilen | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Größe auf Datenträger | 1.12MB | 11.24MB | 109.48MB | 2.69 GB   | 2.14 GB   | 3.21 GB   | 5.36 GB   | 10.71 GB   | 53.58 GB   | 107.52 GB   | 535.88 GB   | 1.05TB |
| SDK-Interaktiver Modus (in Sekunden) | 35.7 Sek. | 31 Sek. | 19.5 Sek. | 25.3 Sek. | 23 Sek. | 33.2 Sek. | 25.5 Sek. | 29.2 Sek. | 29.7 Sek. | 36.9 Sek. | 83.5 Sek. | 139 Sek. |
| SDK-Stapelmodus (in Sekunden) | 448.8 Sek. | 459.7 Sek. | 519 Sek. | 475.8 Sek. | 599.9 Sek. | 347.6 Sek. | 407.8 Sek. | 397 Sek. | 518.8 Sek. | 487.9 Sek. | 760.2 Sek. | 975.4 Sek. |

### Read from a dataset in [!DNL Python]/R

[!DNL Python]Mit - und R-Notebooks können Sie Daten beim Zugriff auf Datensätze paginieren. Nachstehend finden Sie Beispiel-Code zum Lesen von Daten mit und ohne Paginierung.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Read from a dataset in [!DNL Python]/R without pagination

Wenn Sie den folgenden Code ausführen, wird der gesamte Datensatz gelesen. Bei erfolgreicher Ausführung werden die Daten als Pandas-Dataframe gespeichert, auf den die Variable `df` verweist.

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

* `{DATASET_ID}`: Die eindeutige Identität des Datensatzes, auf den zugegriffen werden soll.

#### Read from a dataset in [!DNL Python]/R with pagination

Wenn Sie folgenden Code ausführen, werden Daten aus dem angegebenen Datensatz gelesen. Paginierung wird erreicht, indem Daten über die Funktion `limit()` bzw. `offset()` begrenzt und versetzt werden. Datenbegrenzung bezieht sich auf die maximale Anzahl der zu lesenden Datenpunkte, während Versatz auf die Anzahl der Datenpunkte verweist, die vor dem Lesen von Daten übersprungen werden. Wenn der Lesevorgang erfolgreich ausgeführt wird, werden die Daten als Pandas-Dataframe gespeichert, auf den die Variable `df` verweist.

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

* `{DATASET_ID}`: Die eindeutige Identität des Datensatzes, auf den zugegriffen werden soll.

### Read from a dataset in PySpark/[!DNL Spark]/Scala

With an an active PySpark or Scala notebook opened, expand the **Data Explorer** tab from the left sidebar and double click **Datasets** to view a list of available datasets. Right-click on the dataset listing you wish to access and click **Explore Data in Notebook**. Die folgenden Code-Zellen werden generiert:

#### PySpark ([!DNL Spark] 2.4) {#pyspark2.4}

Mit der Einführung von Spark 2.4 wird [`%dataset`](#magic) maßgeschneiderte Magie geliefert.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala ([!DNL Spark] 2.4) {#spark2.4}

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
>
>In Scala können Sie einen Wert deklarieren und `sys.env()` von innen zurückgeben `option`.

### Verwenden von %dataset magic in PySpark 3 ([!DNL Spark] 2.4) Notebooks {#magic}

Mit der Einführung von [!DNL Spark] 2.4 wird `%dataset` benutzerdefinierte Magie zur Verwendung in neuen PySpark 3 ([!DNL Spark] 2.4) Notebooks ([!DNL Python] 3 Kernel) bereitgestellt.

**Nutzung**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Beschreibung**

Ein benutzerdefinierter [!DNL Data Science Workspace] magischer Befehl zum Lesen oder Schreiben eines Datasets aus einem [!DNL Python] Notebook ([!DNL Python] 3 Kernel).

* **{action}**: Der Aktionstyp, der für den Datensatz ausgeführt werden soll. Es stehen zwei Aktionen zur Verfügung: &quot;Lesen&quot;oder &quot;Schreiben&quot;.
* **—datasetId {id}**: Dient zum Bereitstellen der ID des zu lesenden oder zu schreibenden Datensatzes. Dies ist ein erforderliches Argument.
* **—dataFrame {df}**: Das Pandas-Datenblatt. Dies ist ein erforderliches Argument.
   * Wenn die Aktion &quot;gelesen&quot;ist, ist {df} die Variable, in der Ergebnisse des Datensatzlesevorgangs verfügbar sind.
   * Wenn die Aktion &quot;schreiben&quot;lautet, wird dieser Datenraum {df} in den Datensatz geschrieben.
* **—mode (optional)**: Zulässige Parameter sind &quot;batch&quot;und &quot;interaktiv&quot;. Standardmäßig ist der Modus auf &quot;interaktiv&quot;eingestellt. Es wird empfohlen, beim Lesen großer Datenmengen den Stapelmodus zu verwenden.

**Beispiele**

* **Beispiel** lesen: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Beispiel** schreiben: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### Abfragen mit [!DNL Query Service] in [!DNL Python]

[!DNL JupyterLab] auf [!DNL Platform] ermöglicht Ihnen die Verwendung von SQL in einem [!DNL Python] Notebook, um über den <a href="https://docs.adobe.com/content/help/de-DE/experience-platform/query/home.html" target="_blank">Adobe Experience Platform Abfrage Service</a>auf Daten zuzugreifen. Accessing data through [!DNL Query Service] can be useful for dealing with large datasets due to its superior running times. Be advised that querying data using [!DNL Query Service] has a processing time limit of ten minutes.

Before you use [!DNL Query Service] in [!DNL JupyterLab], ensure you have a working understanding of the <a href="https://docs.adobe.com/content/help/de-DE/experience-platform/query/home.html#!api-specification/markdown/narrative/technical_overview/query-service/sql/syntax.md" target="_blank">[!DNL Query Service] SQL syntax</a>.

Querying data using [!DNL Query Service] requires you to provide the name of the target dataset. Sie können die erforderlichen Code-Zellen generieren, indem Sie den gewünschten Datensatz mit dem **Data Explorer** suchen. Klicken Sie mit der rechten Maustaste auf die Datensatzliste und klicken Sie auf **Daten in Notebook abfragen**, um in Ihrem Notebook die beiden folgenden Code-Zellen zu generieren:


In order to utilize [!DNL Query Service] in [!DNL JupyterLab], you must first create a connection between your working [!DNL Python] notebook and [!DNL Query Service]. Dies kann durch Ausführen der ersten generierten Zelle erreicht werden.

```python
qs_connect()
```

In der zweiten generierten Zelle muss die erste Zeile vor der SQL-Abfrage definiert werden. Standardmäßig definiert die generierte Zelle eine optionale Variable (`df0`), mit der die Abfrageergebnisse als Pandas-Dataframe gespeichert werden. <br>Das `-c QS_CONNECTION` Argument ist obligatorisch und weist den Kernel an, die SQL-Abfrage gegen auszuführen [!DNL Query Service]. Eine Liste weiterer Argumente finden Sie im [Anhang](#optional-sql-flags-for-query-service).

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

Python-Variablen können in einer SQL-Abfrage direkt referenziert werden, indem Sie eine im Zeichenfolgenformat formatierte Syntax verwenden und die Variablen in geschweifte Klammern (`{}`) setzen (siehe folgendes Beispiel):

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filter ExperienceEvent data in [!DNL Python]/R

In order to access and filter an ExperienceEvent dataset in a [!DNL Python] or R notebook, you must provide the ID of the dataset (`{DATASET_ID}`) along with the filter rules that define a specific time range using logical operators. Wenn ein Zeitraum definiert ist, wird jede angegebene Paginierung ignoriert und der gesamte Datensatz berücksichtigt.

Eine Liste der Filteroperatoren finden Sie nachfolgend:

* `eq()`: Gleich
* `gt()`: Größer als
* `ge()`: Größer oder gleich
* `lt()`: Niedriger als
* `le()`: Kleiner oder gleich
* `And()`: Logischer UND-Operator
* `Or()`: Logischer ODER-Operator

Die folgenden Zellen filtern einen ExperienceEvent-Datensatz anhand von Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existierten.

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

### ExperienceEvent-Daten in PySpark/ filtern[!DNL Spark]

Accessing and filtering an ExperienceEvent dataset in a PySpark or Scala notebook requires you to provide the dataset identity (`{DATASET_ID}`), your organization&#39;s IMS identity, and the filter rules defining a specific time range. Ein Filterzeitbereich wird mithilfe der Funktion `spark.sql()` definiert, wobei der Funktionsparameter eine SQL-Abfragezeichenfolge ist.

Die folgenden Zellen filtern einen ExperienceEvent-Datensatz anhand von Daten, die ausschließlich zwischen dem 1. Januar 2019 und dem 31. Dezember 2019 existierten.

#### PySpark 3 ([!DNL Spark] 2.4) {#pyspark3-spark2.4}

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

#### Scala ([!DNL Spark] 2.4) {#scala-spark}

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
>
>In Scala können Sie einen Wert deklarieren und `sys.env()` von innen zurückgeben `option`. Dadurch müssen Variablen nicht mehr definiert werden, wenn Sie wissen, dass sie nur einmal verwendet werden. Das folgende Beispiel nimmt `val userToken` das oben stehende Beispiel und deklariert es als Alternative in &quot;in&quot; `option` :
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

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

## Optional SQL flags for [!DNL Query Service] {#optional-sql-flags-for-query-service}

This table outlines the optional SQL flags that can be used for [!DNL Query Service].

| **Markierung** | **Beschreibung** |
| --- | --- |
| `-h`, `--help` | Hilfemeldung anzeigen und beenden. |
| `-n`, `--notify` | Umschaltoption für das Benachrichtigen bei Abfrageergebnissen. |
| `-a`, `--async` | Bei Verwendung dieser Markierung wird die Abfrage asynchron ausgeführt und kann der Kernel freigeben werden, während die Abfrage ausgeführt wird. Seien Sie vorsichtig, wenn Sie Abfrageergebnisse Variablen zuweisen, da sie möglicherweise undefiniert sind, wenn die Abfrage noch nicht abgeschlossen ist. |
| `-d`, `--display` | Die Verwendung dieser Markierung verhindert, dass Ergebnisse angezeigt werden. |

