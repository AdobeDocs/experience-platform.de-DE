---
keywords: Experience Platform; home; Data Science Workspace; beliebte Themen; Zugriffskontrolle; Sandbox; Intelligence Pack; DSW-Funktionen; DSW-Zugriff; Adobe Experience Platform Intelligence; Intelligence; AEP Intelligence-Paket
solution: Experience Platform
title: Data Science Workspace - Zugriff und Funktionen
description: Im folgenden Dokument werden die Berechtigungen und der Zugriff auf Funktionen von Data Science Workspace beschrieben.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 11%

---

# Zugriff auf und Funktionen von Data Science Workspace

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Im folgenden Dokument werden die Berechtigungen und der Zugriff auf Funktionen von Data Science Workspace beschrieben.

![DSW-Registerkarten](./images/access/platform-tabs.png)

- **Notebooks:** Bietet eine interaktive Entwicklungsumgebung ([JupyterLab](./jupyterlab/overview.md)), um Ihre Daten auf dem Experience Platform zu untersuchen, zu analysieren und zu modellieren.
- **Modelle:** Bietet Tools zum Erstellen, Veröffentlichen und Speichern erweiterter Rezepte und Modelle für maschinelles Lernen. Weitere Informationen finden Sie im Tutorial [Erstellen und Veröffentlichen eines Modells für maschinelles Lernen](./models-recipes/create-publish-model.md) .
- **Dienste:** Enthält sowohl von Adobe bereitgestellte Dienste wie [AI/ML-Dienste](../intelligent-services/home.md) als auch alle benutzerdefinierten Dienste, die Sie mit Data Science Workspace erstellt haben.

Warum wird mir nur die Registerkarte &quot;Dienste&quot;angezeigt?

- Ihr Unternehmen hat möglicherweise nur Berechtigung für Adobe Real-time Customer Data Platform (Real-Time CDP), das den Customer AI AI/ML-Dienst enthält.

Wenn Sie keine der Registerkarten **Data Science** sehen können und die Data Science Workspace-Funktionen nutzen möchten, wenden Sie sich an Ihren Unternehmensadministrator, um zu überprüfen, ob Sie über eine Adobe Experience Platform Intelligence-Lizenz verfügen.

## Data Science Workspace-Verpackung

Data Science Workspace-Funktionen sind im Adobe Experience Platform Intelligence-Paket und im Advanced Intelligence Pack Add-on verfügbar.

In der folgenden Tabelle sind einige der wichtigsten Unterschiede bei den Berechtigungen für Data Science Workspace mit und ohne das Advanced Intelligence Pack-Add-on aufgeführt:

>[!NOTE]
>
>Sie können mehr als ein Erweitertes Intelligence Pack-Add-on lizenzieren. Die erhöhte Kapazität wird zu Ihrer Gesamtberechtigung hinzugefügt. Wenn Sie z. B. 2 Adobe Experience Platform Advanced Intelligence Pack-Addons lizenziert haben, haben Sie Anspruch auf insgesamt 20 gleichzeitige Notebook-Benutzer.

| Data Science Workspace-Berechtigung | Nur Adobe Experience Platform Intelligence-Paket | Adobe Experience Platform Intelligence und Advanced Intelligence Pack-Add-on |
| --- | :---: | :---: |
| Anzahl der unterstützten Notebook-Benutzer. | 5 gleichzeitige Benutzer | First Pack fügt 5 gleichzeitige Benutzer hinzu und zusätzliche Käufe fügen 10 gleichzeitige Benutzer pro Paket hinzu. |
| Ermöglicht integrierte Jupyter Notebooks für die Analyse von Explorationsdaten und die Modellierung. | X (unterstützt R-, Python- und Scala-Bibliotheken) | X (Fügt PySpark- und Spark-ML-Bibliotheken hinzu) |
| Native Integration mit Query Service. Möglichkeit, Datensätze mithilfe von SQL in Notebooks zu untersuchen und zu gestalten. | X | X |
| Zugriff auf vordefinierte Notebook-Vorlagen für Predictive Analytics. | X | X |
| Trainieren und bewerten Sie Modelle manuell mit Jupyter Notebooks. | X | X |
| Stellen Sie Modelle bereit und implementieren Sie sie mit der Möglichkeit, Schulungs- und Unterrichtsvorgänge zu planen. | | X |
| Rezept-Framework zur einfachen Konfiguration, Auswertung, Schulung, Auswertung und Veröffentlichung von Modellen in der Produktion. |  | X |
| Experimentieren und Auswerten benutzeroberflächengesteuerter Modelle. | | X |
| Tief lernende Unterstützung für TensorFlow-Modelle (GPU Compute). | | X |
| Spark-basierter verteilter Compute zum Trainieren und Scores für große Datensätze (10MM + Zeilen). | | X |

## Zugangssteuerung

Die Zugriffskontrolle für Experience Platform wird über die [Adobe Admin Console](https://adminconsole.adobe.com) verwaltet. Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen. Weiterführende Informationen dazu finden Sie unter [Zugangssteuerung – Übersicht](../access-control/home.md).

Um Data Science Workspace verwenden zu können, muss die Berechtigung &quot;Data Science Workspace verwalten&quot;aktiviert sein. In der folgenden Tabelle werden die Auswirkungen der Aktivierung oder Deaktivierung dieser Berechtigung aufgeführt:

| Berechtigung | Aktiviert | Deaktiviert |
|---|---|---|
| Verwalten des Data Science Workspace | Bietet Zugriff auf alle Dienste in Data Science Workspace. | Der API- und UI-Zugriff auf alle Dienste in Data Science Workspace ist deaktiviert. Bei Deaktivierung wird die Auswahl der Seiten **Notebooks**, **Modelle** und **Dienste** verhindert. <li>Der Zugriff auf **Dienste** ist möglicherweise weiterhin über Adobe Real-time Customer Data Platform (Real-Time CDP) verfügbar.</li> |

## Sandbox-Unterstützung

Sandboxes sind virtuelle Partitionen innerhalb einer einzelnen Instanz von Experience Platform. Jede Platform-Instanz unterstützt mehrere Produktions- und Nicht-Produktions-Sandboxes, von denen jede eine eigene Bibliothek mit Platform-Ressourcen unterhält. Mit Nicht-Produktions-Sandboxes können Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen, ohne die Produktions-Sandboxes zu beeinträchtigen. Weiterführende Informationen finden Sie in der [Sandbox-Übersicht](../sandboxes/home.md).

Derzeit gilt für Data Science Workspace die folgende Sandbox-Beschränkung:

- Compute-Ressourcen werden über Produktions- und Nicht-Produktions-Sandboxes hinweg gemeinsam genutzt.

## Nächste Schritte

In diesem Dokument wurden die verschiedenen Zugriffstypen und Funktionen beschrieben, die in Data Science Workspace verfügbar sind.

Um mehr über Data Science Workspace zu erfahren, z. B. einen kompletten täglichen Arbeitsablauf, lesen Sie zunächst die Anleitung zur [Data Science Workspace-exemplarische Vorgehensweise](./walkthrough.md). Weitere allgemeine Informationen finden Sie in der [Übersicht über Data Science Workspace](./home.md).
