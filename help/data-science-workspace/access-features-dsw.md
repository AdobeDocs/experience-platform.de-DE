---
keywords: Experience Platform;home;Data Science Workspace;popular topics;access control;sandbox;intelligence pack;dsw features;dsw access;Adobe Experience Platform Intelligence;intelligence;aep intelligence package
solution: Experience Platform
title: Zugriff auf den Data Science Workspace und Funktionen
topic: Access and features for data science workspace
description: 'Im folgenden Dokument werden die Berechtigungen und der Zugriff auf Funktionen von Data Science Workspace erläutert. '
translation-type: tm+mt
source-git-commit: 40181fc9b1b08c2e21f806caae76b8af0ec9e5e6
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 14%

---


# Zugriff auf den Data Science Workspace und Funktionen

Im folgenden Dokument werden die Berechtigungen und der Zugriff auf Funktionen von Data Science Workspace erläutert.

![DSW-Register](./images/access/platform-tabs.png)

- **Notebooks:** Bietet eine interaktive Entwicklungs-Umgebung ([JupyterLab](./jupyterlab/overview.md)) zur Untersuchung, Analyse und Modellierung Ihrer Daten auf Experience Platform.
- **Modelle:** Bietet Werkzeuge zum Erstellen, Veröffentlichen und Speichern von erweiterten maschinellen Lernrezepten und -modellen. Weitere Informationen finden Sie im Tutorial zum [Erstellen und Veröffentlichen eines maschinellen Lernmodells](./models-recipes/create-publish-model.md) .
- **Dienste:** Enthält sowohl von der Adobe bereitgestellte Dienste wie [Intelligente Dienste](../intelligent-services/home.md) als auch benutzerdefinierte Dienste, die Sie mit Data Science Workspace erstellt haben.

Warum wird nur die Registerkarte &quot;Dienste&quot;angezeigt?

- Ihr Unternehmen hat möglicherweise nur eine Berechtigung auf die Echtzeit-Kundendatenplattform (RTCDP), die die Intelligent Service Customer AI enthält.

Wenn Sie keine der Registerkarten **Data Science** sehen können und die Data Science Workspace-Funktionen nutzen möchten, wenden Sie sich an Ihren Administrator, um zu prüfen, ob Sie über eine Adobe Experience Platform Intelligence-Lizenz verfügen.

## Adobe Experience Platform Intelligence-Paket-Addon

In der folgenden Tabelle sind einige der wichtigsten Unterschiede für Data Science Workspace mit und ohne das Adobe Experience Platform Intelligence-Paket aufgeführt:

>[!NOTE]
>
>Sie können mehr als ein Intelligence-Paket-Add-On lizenzieren, und die erhöhte Kapazität wird zu Ihrer Gesamtberechtigung hinzugefügt. Wenn Sie z. B. 2 Adobe Experience Platform Intelligence-Paket-Addons lizenziert haben, haben Sie Zugriff auf insgesamt 20 gleichzeitige Notebook-Benutzer.

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] mit Intelligence-Paket-Addon |
| --- | :---: | :---: |
| Anzahl der unterstützten Notebook-Benutzer. | 5 gleichzeitige Benutzer | First Pack fügt 5 gleichzeitige Benutzer und zusätzliche Käufe hinzu, um 10 gleichzeitige Benutzer pro Paket hinzuzufügen. |
| Ermöglicht integrierte Jupyter-Notebooks für die Analyse von Forschungsdaten und das Erstellen von Modellen (R, Python, Scala, PySpark) | X | X |
| Native Integration mit Abfrage Service. Möglichkeit, Datasets mithilfe von SQL in Notebooks zu untersuchen und zu gestalten. | X | X |
| Zugriff auf vordefinierte Notebook-Vorlagen für Prognoseanalysen. | X | X |
| Trainieren und bewerten Sie Modelle mit Jupyter Notebooks. | X | X |
| Stellen Sie Modelle bereit und operalisieren Sie sie mit der Möglichkeit, Schulungen zu planen und Jobs zu untersuchen. |  | X |
| Rezept-Framework zur einfachen Konfiguration, Auswertung, Schulung, Bewertung und Veröffentlichung von Modellen in der Produktion. |  | X |
| Experimentieren und Testen von benutzeroberflächengesteuerten Modellen |  | X |
| Tief-Lernunterstützung für Tensorflow-Modelle (GPU Compute). |  | X |
| Spark-basierte verteilte Berechnung zur Schulung und Bewertung mit großen Datensätzen (10MM + Zeilen). |  | X |

## Zugriffskontrolle

Die Zugriffskontrolle für Experience Platform wird über die [Adobe Admin Console](https://adminconsole.adobe.com) verwaltet. Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen. Weiterführende Informationen dazu finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).

Um Data Science Workspace verwenden zu können, muss die Berechtigung &quot;Data Science Workspace verwalten&quot;aktiviert sein. Die folgende Tabelle zeigt die Auswirkungen, die eine Aktivierung oder Deaktivierung dieser Berechtigung hat:

| Berechtigung | Aktiviert | Deaktiviert |
|---|---|---|
| Verwalten des Data Science Workspace | Bietet Zugriff auf alle Dienste im Data Science Workspace. | API- und UI-Zugriff auf alle Dienste in Data Science Workspace sind deaktiviert. Bei Deaktivierung wird die Auswahl der Seiten **Notebooks**, **Modelle** und **Dienste** verhindert. <li>Der Zugriff auf **Dienste** ist möglicherweise weiterhin über die Echtzeit-Kundendatenplattform (RTCDP) verfügbar.</li> |

## Sandbox-Unterstützung

Sandboxes sind virtuelle Partitionen innerhalb einer einzelnen Instanz von Experience Platform. Jede Plattforminstanz unterstützt eine Produktions-Sandbox und mehrere Nicht-Produktions-Sandboxen, wobei jede eine eigene Bibliothek mit Plattformressourcen unterhält. Mit Nicht-Produktions-Sandboxes können Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen, ohne die Produktions-Sandbox zu beeinträchtigen. For more information on sandboxes, see the [sandboxes overview](../sandboxes/home.md).

Data Science Workspace unterliegt derzeit der folgenden Sandbox-Beschränkung:

- Compute-Ressourcen werden über die Produktions-Sandbox und Nicht-Produktions-Sandboxen freigegeben.

## Nächste Schritte

In diesem Dokument werden die verschiedenen Zugriffstypen und Funktionen im Data Science Workspace beschrieben.

Um mehr über den Data Science Workspace zu erfahren, z. B. einen kompletten täglichen Arbeitsablauf, lesen Sie zunächst die exemplarische [Dokumentation zum](./walkthrough.md) Data Science Workspace. For more general information, visit the [Data Science Workspace overview](./home.md).