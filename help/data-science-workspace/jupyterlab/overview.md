---
keywords: Experience Platform;JupyterLab;Notebooks;Data Science Workspace;beliebte Themen;Jupyterlab
solution: Experience Platform
title: Übersicht über die JupyterLab-Benutzeroberfläche
topic-legacy: Overview
description: JupyterLab ist eine Web-basierte Benutzeroberfläche für Project Jupyter und ist eng in Adobe Experience Platform integriert. Es bietet eine interaktive Entwicklungs-Umgebung für Datenwissenschaftler, die mit Jupyter-Notebooks, Code und Daten arbeiten können. In diesem Dokument erhalten Sie einen Überblick über JupyterLab und die Funktionen sowie Anleitungen zum Durchführen häufiger Aktionen.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1819'
ht-degree: 59%

---

# [!DNL JupyterLab] UI-Übersicht

[!DNL JupyterLab] ist eine Web-basierte Benutzeroberfläche für [Project Jupyter](https://jupyter.org/) und ist eng in Adobe Experience Platform integriert. Es bietet eine interaktive Entwicklungs-Umgebung für Datenwissenschaftler, die mit Jupyter-Notebooks, Code und Daten arbeiten können.

In diesem Dokument erhalten Sie einen Überblick über [!DNL JupyterLab] und die zugehörigen Funktionen sowie Anweisungen zum Durchführen gemeinsamer Aktionen.

## [!DNL JupyterLab] on  [!DNL Experience Platform]

Die JupyterLab-Integration mit Experience Platform wird von Architekturänderungen, Designüberlegungen, benutzerdefinierten Notebook-Erweiterungen, vorinstallierten Bibliotheken und einer Oberfläche im Stil von Adobe begleitet.

In der folgenden Liste werden einige der Funktionen vorgestellt, die bei JupyterLab auf Platform einzigartig sind:

| Funktion | Beschreibung |
| --- | --- |
| **Kernels** | Kernels bieten Notebook- und andere [!DNL JupyterLab] Front-Ends die Möglichkeit, Code in verschiedenen Programmiersprachen auszuführen und einzustellen. [!DNL Experience Platform] bietet zusätzliche Kernel zur Unterstützung der Entwicklung in  [!DNL Python], R, PySpark und  [!DNL Spark]. Weiterführende Informationen finden Sie im Abschnitt [Kernels](#kernels). |
| **Datenzugriff** | Greifen Sie direkt von [!DNL JupyterLab] aus auf vorhandene Datensätze zu, und nutzen Sie die volle Unterstützung für Lese- und Schreibfunktionen. |
| **[!DNL Platform]Dienstintegration** | Integrierte Integrationen ermöglichen es Ihnen, andere [!DNL Platform]-Dienste direkt von [!DNL JupyterLab] aus zu nutzen. Eine vollständige Liste der unterstützten Integrationen finden Sie im Abschnitt zur [Integration mit anderen Platform-Diensten](#service-integration). |
| **Authentifizierung** | Zusätzlich zum <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">nativen Sicherheitsmodell von JupyterLab</a> wird jede Interaktion zwischen Ihrer Anwendung und Experience Platform, einschließlich der Kommunikation zwischen Platform-Diensten, über das <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a> verschlüsselt und authentifiziert. |
| **Entwicklungsbibliotheken** | In [!DNL Experience Platform] stellt [!DNL JupyterLab] vorinstallierte Bibliotheken für [!DNL Python], R und PySpark bereit. Eine vollständige Liste der unterstützten Bibliotheken finden Sie im [Anhang](#supported-libraries). |
| **Bibliotheks-Controller** | Wenn die vorinstallierten Bibliotheken Ihren Anforderungen nicht entsprechen, können zusätzliche Bibliotheken für Python und R installiert und vorübergehend in isolierten Containern gespeichert werden, um die Integrität von [!DNL Platform] zu wahren und die Sicherheit Ihrer Daten zu gewährleisten. Weiterführende Informationen finden Sie im Abschnitt [Kernels](#kernels). |

>[!NOTE]
>
> Zusätzliche Bibliotheken sind nur für die Sitzung verfügbar, in der sie installiert werden. Wenn Sie neue Sitzungen starten, müssen Sie alle zusätzlichen Bibliotheken, die Sie benötigen, neu installieren.

## Integration mit anderen [!DNL Platform]-Diensten {#service-integration}

Normung und Interoperabilität sind Schlüsselkonzepte hinter [!DNL Experience Platform]. Die Integration von [!DNL JupyterLab] auf [!DNL Platform] als eingebettete IDE ermöglicht die Interaktion mit anderen [!DNL Platform]-Diensten, sodass Sie [!DNL Platform] voll ausschöpfen können. Die folgenden [!DNL Platform]-Dienste sind in [!DNL JupyterLab] verfügbar:

* **[!DNL Catalog Service]:** Aufrufen und Erkunden von Datensätzen mit Lese- und Schreibfunktionen.
* **[!DNL Query Service]:** Aufrufen und Erkunden von Datensätzen mit SQL, wodurch sich beim Datenzugriff bei großen Datenmengen der Overhead verringert.
* **[!DNL Sensei ML Framework]:** Modellentwicklung mit der Möglichkeit, Daten zu trainieren und zu bewerten, sowie Rezepterstellung mit einem Klick.
* **[!DNL Experience Data Model (XDM)]:** Normung und Interoperabilität sind Schlüsselkonzepte hinter Adobe Experience Platform. [Erlebnis-Datenmodell (XDM)](https://www.adobe.com/go/xdm-home-en), angetrieben von Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

>[!NOTE]
>
>Einige [!DNL Platform] Dienstintegrationen auf [!DNL JupyterLab] sind auf bestimmte Kernels beschränkt. Weiterführende Informationen finden Sie im Abschnitt [Kernels](#kernels).

## Wichtigste Funktionen und allgemeine Vorgänge

Informationen zu Schlüsselfunktionen von [!DNL JupyterLab] und Anweisungen zur Durchführung gemeinsamer Vorgänge finden Sie in den folgenden Abschnitten:

* [Zugriff auf JupyterLab](#access-jupyterlab)
* [Oberfläche von JupyterLab](#jupyterlab-interface)
* [Code-Zellen](#code-cells)
* [Kernels](#kernels)
* [Kernel-Sitzungen](#kernel-sessions)
* [Starter](#launcher)

### Zugriff auf [!DNL JupyterLab] {#access-jupyterlab}

Wählen Sie unter [Adobe Experience Platform](https://platform.adobe.com) **[!UICONTROL Notebooks]** in der linken Navigationsspalte aus. Warten Sie einige Zeit, bis [!DNL JupyterLab] vollständig initialisiert ist.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] Benutzeroberfläche {#jupyterlab-interface}

Die [!DNL JupyterLab]-Schnittstelle besteht aus einer Menüleiste, einer reduzierbaren linken Seitenleiste und dem Hauptarbeitsbereich mit Registerkarten von Dokumenten und Aktivitäten.

**Menüleiste**

Die Menüleiste oben auf der Oberfläche verfügt über Menüs der obersten Ebene, die in [!DNL JupyterLab] verfügbare Aktionen mit ihren Tastaturbefehlen aufdecken:

* **Datei:** Aktionen im Zusammenhang mit Dateien und Ordnern
* **Bearbeiten:** Aktionen im Zusammenhang mit der Bearbeitung von Dokumenten und anderen Aktivitäten
* **Ansicht:** Aktionen, die das Erscheinungsbild von ändern[!DNL JupyterLab]
* **Ausführen:** Aktionen zum Ausführen von Code in verschiedenen Aktivitäten, wie z. B. Notebooks und Code-Konsolen
* **Kernel:** Aktionen zum Verwalten von Kerneln
* **Registerkarten:** Eine Liste offener Dokumente und Aktivitäten
* **Einstellungen:** Allgemeine Einstellungen und ein Editor für erweiterte Einstellungen
* **Hilfe:**[!DNL JupyterLab] Eine Liste von - und Kernel-Hilfe-Links

**Linke Seitenleiste**

Die linke Seitenleiste enthält anklickbare Registerkarten, die Zugriff auf die folgenden Funktionen bieten:

* **Datei-Browser:** Eine Liste gespeicherter Notebook-Dokumente und -Verzeichnisse
* **Data Explorer:** Durchsuchen, Aufrufen und Erforschen von Datensätzen und Schemas
* **Laufende Kernel und Terminals:** Eine Liste von aktiven Kernel- und Terminal-Sitzungen mit der Möglichkeit zum Beenden
* **Befehle:** Eine Liste mit hilfreichen Befehlen
* **Zellinspektor:** Ein Zelleneditor, der Zugriff auf Tools und Metadaten bietet, die für die Einrichtung eines Notebooks zu Präsentationszwecken nützlich sind
* **Registerkarten:** Eine Liste offener Registerkarten

Wählen Sie eine Registerkarte aus, um deren Funktionen anzuzeigen, oder wählen Sie auf einer erweiterten Registerkarte aus, um die linke Seitenleiste wie unten dargestellt zu reduzieren:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Hauptarbeitsbereich**

Der Hauptarbeitsbereich in [!DNL JupyterLab] ermöglicht es Ihnen, Dokumente und andere Aktivitäten in Registerkartenbedienfelder anzuordnen, die skaliert oder unterteilt werden können. Ziehen Sie eine Registerkarte in die Mitte eines Registerkarten-Panels, um die Registerkarte zu verschieben. Unterteilen Sie ein Panel durch Ziehen einer Registerkarte nach links, rechts, oben oder unten im Panel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### GPU- und Speicherserverkonfiguration in [!DNL Python]/R

Wählen Sie in [!DNL JupyterLab] das Zahnradsymbol in der oberen rechten Ecke aus, um *Notebook-Serverkonfiguration* zu öffnen. Mit dem Schieberegler können Sie die GPU aktivieren und die benötigte Speichermenge zuweisen. Wie viel Arbeitsspeicher Sie zuweisen können, hängt davon ab, wie viel Arbeitsspeicher Ihr Unternehmen bereitgestellt hat. Wählen Sie **[!UICONTROL Konfigurationen aktualisieren]** zum Speichern aus.

>[!NOTE]
>
>Pro Unternehmen wird nur eine GPU für Notebooks bereitgestellt. Wenn die GPU in Gebrauch ist, müssen Sie warten, bis der Benutzer, der die GPU derzeit reserviert hat, sie freigegeben hat. Dies ist möglich, indem Sie sich abmelden oder die GPU für vier oder mehr Stunden im Leerlauf lassen.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Beenden und Neustart [!DNL JupyterLab]

In [!DNL JupyterLab] können Sie Ihre Sitzung beenden, um zu verhindern, dass weitere Ressourcen verwendet werden. Beginn durch Auswahl des **Power-Symbols** ![power-Symbols](../images/jupyterlab/user-guide/power_button.png) und dann **[!UICONTROL Shut Down]** aus dem Popup, das angezeigt wird, um Ihre Sitzung zu beenden. Notebook-Sitzungen enden nach 12 Stunden ohne Aktivität automatisch.

Um [!DNL JupyterLab] neu zu starten, wählen Sie das **Symbol zum Neustart** ![Symbol zum Neustart](../images/jupyterlab/user-guide/restart_button.png), das sich direkt links neben dem Symbol für Strom befindet, und wählen Sie dann **[!UICONTROL Neustart]** aus dem angezeigten Popup aus.

![Jupyterlab beenden](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Code-Zellen {#code-cells}

Code-Zellen sind der Hauptinhalt von Notebooks. Sie enthalten Quell-Code in der Sprache des Kernels vom Notebook und die Ausgabe als Ergebnis der Ausführung der Code-Zelle. Rechts neben jeder Code-Zelle, die die Ausführungsreihenfolge darstellt, wird ein Ausführungszähler angezeigt.

![](../images/jupyterlab/user-guide/code_cell.png)

Häufige Zellaktionen werden nachfolgend beschrieben:

* **Zelle hinzufügen:** Klicken Sie im Notebook-Menü auf das Pluszeichen (**+**), um eine leere Zelle hinzuzufügen. Neue Zellen werden unter der Zelle platziert, mit der derzeit interagiert wird, oder am Ende des Notebooks, wenn keine bestimmte Zelle im Fokus ist.

* **Zelle verschieben:** Platzieren Sie den Cursor rechts neben der Zelle, die Sie verschieben möchten, und ziehen Sie die Zelle dann an eine neue Position. Wenn Sie eine Zelle von einem Notebook in ein anderes verschieben, wird die Zelle zusammen mit ihrem Inhalt repliziert.

* **Zelle ausführen:** Klicken Sie auf den Text der Zelle, die Sie ausführen möchten, und klicken Sie dann auf das **Wiedergabesymbol** (**▶**) im Notebook-Menü. Im Ausführungszähler der Zelle wird ein Sternchen (**\***) angezeigt, wenn der Kernel die Ausführung verarbeitet, und nach Abschluss durch eine Ganzzahl ersetzt.

* **Zelle löschen:** Klicken Sie auf den Text der Zelle, die Sie löschen möchten, und klicken Sie dann auf das Symbol **Schere**.

### Kernels {#kernels}

Notebook-Kernel sind sprachspezifische Rechen-Engines zur Verarbeitung von Notebook-Zellen. Zusätzlich zu [!DNL Python] bietet [!DNL JupyterLab] zusätzliche Sprachunterstützung in R, PySpark und [!DNL Spark] (Scala). Wenn Sie ein Notebook-Dokument öffnen, wird der zugehörige Kernel gestartet. Wenn eine Notebook-Zelle ausgeführt wird, führt der Kernel die Berechnung durch und erzeugt Ergebnisse, die erhebliche CPU- und Arbeitsspeicherressourcen beanspruchen können. Beachten Sie, dass zugewiesener Speicher erst freigegeben wird, wenn der Kernel heruntergefahren wird.

Bestimmte Funktionen und Funktionen sind auf bestimmte Kernels beschränkt, wie in der folgenden Tabelle beschrieben:

| Kernel | Installationsunterstützung für Bibliotheken | [!DNL Platform] Integrationen |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Ja | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Nein | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Kernel-Sitzungen {#kernel-sessions}

Jedes aktive Notebook oder jede aktive Aktivität auf [!DNL JupyterLab] nutzt eine Kernelsitzung. Alle aktiven Sitzungen finden Sie, indem Sie auf der linken Seitenleiste die Registerkarte **Laufende Terminals und Kernel** erweitern. Typ und Zustand des Kernels eines Notebooks finden Sie in der oberen rechten Ecke der Notebook-Oberfläche. In der Abbildung unten ist der zugehörige Kernel des Notebooks **[!DNL Python]3** und der aktuelle Status wird durch einen grauen Kreis rechts dargestellt. Ein leerer Kreis impliziert einen Kernel im Leerlauf, während ein ausgefüllter Kreis einen aktiven Kernel darstellt.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Wenn der Kernel für einen längeren Zeitraum heruntergefahren oder inaktiv ist, dann **Kein Kernel!** mit einem ausgefüllten Kreis angezeigt. Aktivieren Sie einen Kernel, indem Sie auf den Kernel-Status klicken und den entsprechenden Kernel-Typ auswählen, wie unten gezeigt:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Starter {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

Der angepasste *Starter* bietet nützliche Notebook-Vorlagen für die unterstützten Kernels, die Ihnen helfen, mit Ihrer Aufgabe zu beginnen, darunter:

| Vorlage | Beschreibung |
| --- | --- |
| Leer | Eine leere Notebook-Datei. |
| Starter | Ein vorausgefülltes Notebook, das die Datenerfassung anhand von Musterdaten demonstriert. |
| Einzelhandelsumsätze | Ein vorgefülltes Notebook mit dem Vertriebsrezept [für den Einzelhandel](https://docs.adobe.com/content/help/de-DE/experience-platform/data-science-workspace/home.translate.html#!api-specification/markdown/narrative/technical_overview/data_science_workspace_overview/dsw_prebuilt_recipes/retail_sales_recipe/retail_sales_recipe.md), das Beispieldaten verwendet. |
| Recipe Builder | Eine Notebook-Vorlage zum Erstellen eines Rezepts in [!DNL JupyterLab]. Sie ist mit Code und Kommentaren vorausgefüllt, die die Erstellung von Rezepten demonstrieren und beschreiben. Eine ausführliche Vorgehensweise finden Sie im Tutorial [Notebook an Rezept](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en). |
| [!DNL Query Service] | Ein vorausgefülltes Notebook, das die Verwendung von [!DNL Query Service] direkt in [!DNL JupyterLab] mit bereitgestellter Workflows zeigt, die Daten im Maßstab analysieren. |
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
        <th><strong>Rezepturaufbau</strong></th>
        <th><strong>[!DNL Abfrage Service]</strong></th>
        <th><strong>ExperienceEvents</strong></th>
        <th><strong>XDM-Abfragen</strong></th>
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

Weitere Informationen zu den einzelnen unterstützten Notebooks und deren Verwendung finden Sie im [Jupyterlab-Handbuch für den Datenzugriff auf Notebooks](./access-notebook-data.md). Dieser Leitfaden konzentriert sich darauf, wie Sie mit JupyterLab-Notebooks auf Ihre Daten zugreifen können, einschließlich Lesen, Schreiben und Abfragen von Daten. Die Anleitung zum Datenzugriff enthält außerdem Informationen zur maximalen Datenmenge, die von jedem unterstützten Notebook gelesen werden kann.

## Unterstützte Bibliotheken {#supported-libraries}

Für eine Liste unterstützter Pakete in Python, R und PySpark kopieren Sie `!pip list --format=columns` in eine neue Zelle und führen Sie dann die Zelle aus. Eine Liste unterstützter Pakete wird in alphabetischer Reihenfolge gefüllt.

![example](../images/jupyterlab/user-guide/libraries.PNG)
