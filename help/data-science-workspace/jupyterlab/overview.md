---
keywords: Experience Platform;JupyterLab;Notebooks;Datenwissenschafts-Arbeitsbereich;beliebte Themen;Jupyterlab
solution: Experience Platform
title: Übersicht über die Benutzeroberfläche von JupyterLab
description: JupyterLab ist eine Web-basierte Benutzeroberfläche für Project Jupyter und ist eng in Adobe Experience Platform integriert. Sie bietet eine interaktive Entwicklungsumgebung für Datenwissenschaftlerinnen und Datenwissenschaftler, die mit Jupyter-Notebooks, -Code und -Daten arbeiten möchten. In diesem Dokument erhalten Sie einen Überblick über JupyterLab und die Funktionen sowie Anleitungen zum Durchführen häufiger Aktionen.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: ht
source-wordcount: '1820'
ht-degree: 100%

---

# [!DNL JupyterLab] Benutzeroberfläche – Übersicht

[!DNL JupyterLab] ist eine Web-basierte Benutzeroberfläche für [Project Jupyter](https://jupyter.org/) und ist eng in Adobe Experience Platform integriert. Sie bietet eine interaktive Entwicklungsumgebung für Datenwissenschaftlerinnen und Datenwissenschaftler, die mit Jupyter-Notebooks, -Code und -Daten arbeiten möchten.

In diesem Dokument erhalten Sie einen Überblick über [!DNL JupyterLab] und seine Funktionen sowie Anweisungen zum Durchführen häufiger Aktionen.

## [!DNL JupyterLab] auf [!DNL Experience Platform]

Die JupyterLab-Integration mit Experience Platform wird von Architekturänderungen, Designüberlegungen, benutzerdefinierten Notebook-Erweiterungen, vorinstallierten Bibliotheken und einer Oberfläche im Stil von Adobe begleitet.

In der folgenden Liste werden einige der Funktionen vorgestellt, die bei JupyterLab auf Platform einzigartig sind:

| Funktion | Beschreibung |
| --- | --- |
| **Kernels** | Kernels bieten Notebook und anderen [!DNL JupyterLab]-Frontends die Möglichkeit, Code in verschiedenen Programmiersprachen auszuführen und zu prüfen. [!DNL Experience Platform] bietet zusätzliche Kernels zur Unterstützung der Entwicklung in [!DNL Python], R, PySpark und [!DNL Spark]. Weiterführende Informationen finden Sie im Abschnitt [Kernels](#kernels). |
| **Datenzugriff** | Auf vorhandene Datensätze kann direkt in [!DNL JupyterLab] zugegriffen werden, bei voller Unterstützung der Lese- und Schreibfunktionen. |
| **[!DNL Platform]-Service-Integration** | Mit nativen Integrationen können Sie andere [!DNL Platform]-Services direkt von [!DNL JupyterLab] aus nutzen. Eine vollständige Liste der unterstützten Integrationen finden Sie im Abschnitt zur [Integration mit anderen Platform-Diensten](#service-integration). |
| **Authentifizierung** | Zusätzlich zum <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">nativen Sicherheitsmodell von JupyterLab</a> wird jede Interaktion zwischen Ihrer Anwendung und Experience Platform, einschließlich der Kommunikation zwischen Platform-Diensten, über das <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a> verschlüsselt und authentifiziert. |
| **Entwicklungsbibliotheken** | In [!DNL Experience Platform] stellt [!DNL JupyterLab] vorinstallierte Bibliotheken für [!DNL Python], R und PySpark zur Verfügung. Eine vollständige Liste der unterstützten Bibliotheken finden Sie im [Anhang](#supported-libraries). |
| **Bibliotheks-Controller** | Wenn die vorinstallierten Bibliotheken Ihren Anforderungen nicht entsprechen, können Sie zusätzliche Bibliotheken für Python und R installieren und vorübergehend in isolierten Containern speichern, um die Integrität von [!DNL Platform] sowie die Sicherheit Ihrer Daten zu wahren. Weiterführende Informationen finden Sie im Abschnitt [Kernels](#kernels). |

>[!NOTE]
>
>Zusätzliche Bibliotheken sind nur für die Sitzung verfügbar, in der sie installiert werden. Wenn Sie neue Sitzungen starten, müssen Sie alle zusätzlichen Bibliotheken, die Sie benötigen, neu installieren.

## Integration in andere [!DNL Platform]-Services {#service-integration}

Standardisierung und Interoperabilität sind Schlüsselkonzepte von [!DNL Experience Platform]. Die Integration von [!DNL JupyterLab] auf [!DNL Platform] als eingebettete IDE ermöglicht es, mit anderen [!DNL Platform]-Services zu interagieren, sodass Sie [!DNL Platform] optimal nutzen können. Folgende [!DNL Platform]-Services sind in [!DNL JupyterLab] verfügbar:

* **[!DNL Catalog Service]:** Aufrufen und Erkunden von Datensätzen mit Lese- und Schreibfunktionen.
* **[!DNL Query Service]:** Greifen Sie auf Datensätze zu und untersuchen Sie sie mithilfe von SQL, was bei großen Datenmengen zu einem geringeren Overhead beim Datenzugriff führt.
* **[!DNL Sensei ML Framework]:** Modellentwicklung mit der Möglichkeit, Daten zu trainieren und zu bewerten, sowie Rezepterstellung mit einem Klick.
* **[!DNL Experience Data Model (XDM)]:** Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. Das von Adobe unterstützte [Experience-Datenmodell (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de) ermöglicht die Standardisierung von Kundenerlebnisdaten und die Definition von Schemata für das Customer Experience Management.

>[!NOTE]
>
>Einige [!DNL Platform]-Service-Integrationen in [!DNL JupyterLab] sind auf bestimmte Kernels beschränkt. Weiterführende Informationen finden Sie im Abschnitt [Kernels](#kernels).

## Wichtigste Funktionen und allgemeine Vorgänge

Informationen zu den wichtigsten Funktionen von [!DNL JupyterLab] und Anweisungen zur Durchführung allgemeiner Vorgänge finden Sie in den folgenden Abschnitten:

* [Zugriff auf JupyterLab](#access-jupyterlab)
* [Oberfläche von JupyterLab](#jupyterlab-interface)
* [Code-Zellen](#code-cells)
* [Kernels](#kernels)
* [Kernel-Sitzungen](#kernel-sessions)
* [Starter](#launcher)

### Zugriff auf [!DNL JupyterLab] {#access-jupyterlab}

Wählen Sie in [Adobe Experience Platform](https://platform.adobe.com) in der linken Navigationsspalte die Option **[!UICONTROL Notebooks]** aus. Warten Sie etwas, bis [!DNL JupyterLab] vollständig initialisiert wurde.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab]-Benutzeroberfläche {#jupyterlab-interface}

Die Benutzeroberfläche von [!DNL JupyterLab] besteht aus einer Menüleiste, einer reduzierbaren linken Seitenleiste und dem Hauptarbeitsbereich mit Registerkarten für Dokumente und Aktivitäten.

**Menüleiste**

Die Menüleiste oben in der Benutzeroberfläche verfügt über Menüs auf oberster Ebene, die die in [!DNL JupyterLab] verfügbaren Aktionen mit ihren Tastaturbefehlen anzeigen:

* **Datei:** Aktionen im Zusammenhang mit Dateien und Ordnern
* **Bearbeiten:** Aktionen im Zusammenhang mit der Bearbeitung von Dokumenten und anderen Aktivitäten
* **Ansicht:** Aktionen, die das Erscheinungsbild von [!DNL JupyterLab] ändern
* **Ausführen:** Aktionen zum Ausführen von Code in verschiedenen Aktivitäten, wie z. B. Notebooks und Code-Konsolen
* **Kernel:** Aktionen zum Verwalten von Kerneln
* **Registerkarten:** Eine Liste offener Dokumente und Aktivitäten
* **Einstellungen:** Allgemeine Einstellungen und ein Editor für erweiterte Einstellungen
* **Hilfe:** Eine Liste von [!DNL JupyterLab]- und Kernel-Hilfe-Links

**Linke Seitenleiste**

Die linke Seitenleiste enthält klickbare Registerkarten, die Zugriff auf folgende Funktionen bieten:

* **Datei-Browser:** Eine Liste gespeicherter Notebook-Dokumente und -Verzeichnisse
* **Data Explorer:** Durchsuchen, Aufrufen und Erforschen von Datensätzen und Schemas
* **Laufende Kernel und Terminals:** Eine Liste von aktiven Kernel- und Terminal-Sitzungen mit der Möglichkeit zum Beenden
* **Befehle:** Eine Liste mit hilfreichen Befehlen
* **Zellinspektor:** Ein Zelleneditor, der Zugriff auf Tools und Metadaten bietet, die für die Einrichtung eines Notebooks zu Präsentationszwecken nützlich sind
* **Registerkarten:** Eine Liste offener Registerkarten

Wählen Sie eine Registerkarte aus, um deren Funktionen anzuzeigen, oder wählen Sie eine erweiterte Registerkarte aus, um die linke Seitenleiste wie unten gezeigt zu reduzieren:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Hauptarbeitsbereich**

Der Hauptarbeitsbereich in [!DNL JupyterLab] ermöglicht es Ihnen, Dokumente und andere Aktivitäten in Registerkarten-Panels anzuordnen, die in der Größe angepasst oder unterteilt werden können. Ziehen Sie eine Registerkarte in die Mitte eines Registerkarten-Panels, um die Registerkarte zu verschieben. Unterteilen Sie ein Panel durch Ziehen einer Registerkarte nach links, rechts, oben oder unten im Panel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### GPU- und Speicher-Server-Konfiguration in [!DNL Python]/R

Wählen Sie in [!DNL JupyterLab] oben rechts das Zahnradsymbol aus, um *Notebook-Server-Konfiguration* zu öffnen. Sie können die GPU-Option umschalten und die benötigte Speichermenge mithilfe des Reglers zuweisen. Wie viel Arbeitsspeicher Sie zuweisen können, hängt davon ab, wie viel Ihre Organisation bereitgestellt hat. Wählen Sie **[!UICONTROL Konfigurationen aktualisieren]** aus, um zu speichern.

>[!NOTE]
>
>Pro Organisation wird nur eine GPU für Notebooks bereitgestellt. Wenn die GPU verwendet wird, müssen Sie warten, bis die Person, die die GPU derzeit reserviert hat, sie freigibt. Dies ist durch Abmelden möglich oder dadurch, dass die GPU vier oder mehr Stunden lang im Leerlauf belassen wird.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Beenden und Neustarten von [!DNL JupyterLab]

In [!DNL JupyterLab] können Sie Ihre Sitzung beenden, um die Verwendung weiterer Ressourcen zu verhindern. Wählen Sie zunächst das **Ein/Aus-Symbol** ![Ein/Aus-Symbol](../images/jupyterlab/user-guide/power_button.png) und dann im angezeigten Popup die Option **[!UICONTROL Herunterfahren]** aus, um Ihre Sitzung zu beenden. Notebook-Sitzungen enden nach 12 Stunden ohne Aktivität automatisch.

Um [!DNL JupyterLab] neu zu starten, wählen Sie das **Neustart-Symbol** ![Neustart-Symbol](../images/jupyterlab/user-guide/restart_button.png) direkt links neben dem Ein/Aus-Symbol und dann im angezeigten Popup die Option **[!UICONTROL Neu starten]** aus.

![Beenden von JupyterLab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Code-Zellen {#code-cells}

Code-Zellen sind der Hauptinhalt von Notebooks. Sie enthalten Quell-Code in der Sprache des Kernels vom Notebook und die Ausgabe als Ergebnis der Ausführung der Code-Zelle. Rechts neben jeder Code-Zelle, die die Ausführungsreihenfolge darstellt, wird ein Ausführungszähler angezeigt.

![](../images/jupyterlab/user-guide/code_cell.png)

Häufige Zellaktionen werden nachfolgend beschrieben:

* **Zelle hinzufügen:** Klicken Sie im Notebook-Menü auf das Pluszeichen (**+**), um eine leere Zelle hinzuzufügen. Neue Zellen werden unter der Zelle platziert, mit der derzeit interagiert wird, oder am Ende des Notebooks, wenn keine bestimmte Zelle im Fokus ist.

* **Zelle verschieben:** Platzieren Sie den Cursor rechts neben der Zelle, die Sie verschieben möchten, und ziehen Sie die Zelle dann an eine neue Position. Wenn Sie eine Zelle von einem Notebook in ein anderes verschieben, wird die Zelle zusammen mit ihrem Inhalt repliziert.

* **Zelle ausführen:** Klicken Sie auf den Text der Zelle, die Sie ausführen möchten, und klicken Sie dann auf das **Wiedergabesymbol** (**▶**) im Notebook-Menü. Im Ausführungszähler der Zelle wird ein Sternchen (**\***) angezeigt, wenn der Kernel die Ausführung verarbeitet, und nach Abschluss durch eine Ganzzahl ersetzt.

* **Zelle löschen:** Klicken Sie auf den Text der Zelle, die Sie löschen möchten, und klicken Sie dann auf das Symbol **Schere**.

### Kernels {#kernels}

Notebook-Kernels sind sprachspezifische Rechen-Engines zur Verarbeitung von Notebook-Zellen. Zusätzlich zu [!DNL Python] bietet [!DNL JupyterLab] Sprachunterstützung für R, PySpark und [!DNL Spark] (Scala). Wenn Sie ein Notebook-Dokument öffnen, wird der zugehörige Kernel gestartet. Wenn eine Notebook-Zelle ausgeführt wird, führt der Kernel die Berechnung durch und erzeugt Ergebnisse, die erhebliche CPU- und Arbeitsspeicherressourcen beanspruchen können. Beachten Sie, dass zugewiesener Arbeitsspeicher erst freigegeben wird, wenn der Kernel heruntergefahren wird.

Bestimmte Funktionen und Funktionen sind auf bestimmte Kernels beschränkt, wie in der folgenden Tabelle beschrieben:

| Kernel | Installationsunterstützung für Bibliotheken | [!DNL Platform]-Integrationen |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Nein | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Kernel-Sitzungen {#kernel-sessions}

Jedes aktive Notebook oder jede Aktivität in [!DNL JupyterLab] verwendet eine Kernel-Sitzung. Alle aktiven Sitzungen finden Sie, indem Sie auf der linken Seitenleiste die Registerkarte **Laufende Terminals und Kernel** erweitern. Typ und Zustand des Kernels eines Notebooks finden Sie in der oberen rechten Ecke der Notebook-Oberfläche. In der Abbildung unten ist der zugehörige Kernel des Notebooks **[!DNL Python]3**, und der aktuelle Status wird durch einen grauen Kreis rechts dargestellt. Ein leerer Kreis impliziert einen Kernel im Leerlauf, während ein ausgefüllter Kreis einen aktiven Kernel darstellt.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Wenn der Kernel heruntergefahren wurde oder über einen längeren Zeitraum inaktiv war, dann erscheint **Kein Kernel!** mit einem ausgefüllten Kreis angezeigt. Aktivieren Sie einen Kernel, indem Sie auf den Kernel-Status klicken und den entsprechenden Kernel-Typ auswählen, wie unten gezeigt:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Starter {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Der angepasste *Starter* bietet nützliche Notebook-Vorlagen für die unterstützten Kernels, die Ihnen helfen, mit Ihrer Aufgabe zu beginnen, darunter:

| Vorlage | Beschreibung |
| --- | --- |
| Leer | Eine leere Notebook-Datei. |
| Starter | Ein vorausgefülltes Notebook, das die Datenerfassung anhand von Musterdaten demonstriert. |
| Einzelhandelsumsätze | Ein vorausgefülltes Notebook mit dem [Rezept für Einzelhandelsumsätze](../pre-built-recipes/retail-sales.md), inklusive Beispieldaten. |
| Recipe Builder | Eine Notebook-Vorlage zum Erstellen eines Rezepts in [!DNL JupyterLab]. Sie ist mit Code und Kommentaren vorausgefüllt, die die Erstellung von Rezepten demonstrieren und beschreiben. Eine ausführliche Vorgehensweise finden Sie im Tutorial [Notebook an Rezept](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/jupyterlab/create-a-model.html?lang=de). |
| [!DNL Query Service] | Ein vorausgefülltes Notebook, das die Verwendung von [!DNL Query Service] direkt in [!DNL JupyterLab] demonstriert, mit Beispiel-Workflows, die Daten im großen Maßstab analysieren. |
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
        <th><strong>[!DNL Query Service]</strong></th>
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

## Nächste Schritte

Weitere Informationen zu den einzelnen unterstützten Notebooks und deren Verwendung finden Sie im Entwicklerhandbuch für den [Datenzugriff über JupyterLab-Notebooks](./access-notebook-data.md). In diesem Handbuch wird beschrieben, wie Sie mit JupyterLab-Notebooks auf Ihre Daten zugreifen können, einschließlich Lesen, Schreiben und Abfragen von Daten. Das Handbuch zum Datenzugriff enthält außerdem Informationen zur maximalen Datenmenge, die von jedem unterstützten Notebook gelesen werden kann.

## Unterstützte Bibliotheken {#supported-libraries}

Für eine Liste der unterstützten Pakete in Python, R und PySpark kopieren Sie `!conda list` und fügen dies in eine neue Zelle ein. Führen Sie dann die Zelle aus. Eine Liste der unterstützten Pakete wird in alphabetischer Reihenfolge aufgefüllt.

![Beispiel](../images/jupyterlab/user-guide/libraries.PNG)

Darüber hinaus werden die folgenden Abhängigkeiten verwendet, aber nicht aufgelistet:
* CUDA 11.2
* CUDNN 8.1

