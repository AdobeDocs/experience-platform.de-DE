---
keywords: Experience Platform; Startseite; Data Science Workspace; beliebte Themen; Zugriffskontrolle; Sandbox; Intelligence Pack; DSW-Funktionen; DSW-Zugriff; Adobe Experience Platform Intelligence; Intelligence; AEP Intelligence-Paket
solution: Experience Platform
title: Zugriff auf Data Science Workspace und Funktionen
topic-legacy: Access and features for data science workspace
description: Im folgenden Dokument werden die Berechtigungen von Data Science Workspace und der Zugriff auf Funktionen beschrieben.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 2ff2721f5420483ddc5caffd1eb0532df729e01b
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 12%

---

# Zugriff auf und Funktionen von Data Science Workspace

Im folgenden Dokument werden die Berechtigungen von Data Science Workspace und der Zugriff auf Funktionen beschrieben.

![DSW-Registerkarten](./images/access/platform-tabs.png)

- **Notebooks:** Bietet eine interaktive Entwicklungsumgebung ([JupyterLab](./jupyterlab/overview.md)), um Ihre Daten in Experience Platform zu untersuchen, zu analysieren und zu modellieren.
- **Modelle:** Bietet Tools zum Erstellen, Veröffentlichen und Speichern erweiterter Rezepte und Modelle für maschinelles Lernen. Weitere Informationen finden Sie unter [Erstellen und Veröffentlichen eines Modells für maschinelles Lernen](./models-recipes/create-publish-model.md) Tutorial.
- **Dienste:** Enthält beide von Adobe bereitgestellten Dienste, z. B. [KI-/ML-Dienste](../intelligent-services/home.md) und alle benutzerdefinierten Dienste, die Sie mit Data Science Workspace erstellt haben.

Warum wird mir nur die Registerkarte &quot;Dienste&quot;angezeigt?

- Ihr Unternehmen hat möglicherweise nur Berechtigung für Real-time Customer Data Platform (RTCDP), das den Customer AI AI/ML-Dienst umfasst.

Wenn Sie keinen der **Datenwissenschaften** Registerkarten ein und möchten die Funktionen von Data Science Workspace nutzen, wenden Sie sich an Ihren Unternehmensadministrator, um zu überprüfen, ob Sie über eine Adobe Experience Platform Intelligence-Lizenz verfügen.

## Data Science Workspace-Verpackung

Data Science Workspace-Funktionen sind im Adobe Experience Platform Intelligence-Paket und im Advanced Intelligence Pack Add-on verfügbar

In der folgenden Tabelle werden einige der wichtigsten Unterschiede für Data Science Workspace-Berechtigungen mit und ohne das Advanced Intelligence Pack-Add-on erläutert:

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
| Stellen Sie Modelle bereit und implementieren Sie sie mit der Möglichkeit, Schulungs- und Unterrichtsvorgänge zu planen. |  | X |
| Rezept-Framework zur einfachen Konfiguration, Auswertung, Schulung, Auswertung und Veröffentlichung von Modellen in der Produktion. |  | X |
| Experimentieren und Auswerten benutzeroberflächengesteuerter Modelle. |  | X |
| Tief lernende Unterstützung für TensorFlow-Modelle (GPU Compute). |  | X |
| Spark-basierter verteilter Compute zum Trainieren und Scores für große Datensätze (10MM + Zeilen). |  | X |

## Zugangssteuerung

Die Zugriffskontrolle für Experience Platform wird über die [Adobe Admin Console](https://adminconsole.adobe.com) verwaltet. Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen. Weiterführende Informationen dazu finden Sie unter [Zugangssteuerung – Übersicht](../access-control/home.md).

Um Data Science Workspace verwenden zu können, muss die Berechtigung &quot;Data Science Workspace verwalten&quot;aktiviert sein. In der folgenden Tabelle werden die Auswirkungen der Aktivierung oder Deaktivierung dieser Berechtigung aufgeführt:

| Berechtigung | Aktiviert | Deaktiviert |
|---|---|---|
| Verwalten des Data Science Workspace | Bietet Zugriff auf alle Dienste in Data Science Workspace. | Der API- und UI-Zugriff auf alle Dienste in Data Science Workspace ist deaktiviert. Während deaktiviert, wählen Sie die **Notebooks**, **Modelle** und **Dienste** -Seiten verhindert werden. <li>Zugriff auf **Dienste** kann weiterhin über Real-time Customer Data Platform (RTCDP) verfügbar sein.</li> |

## Sandbox-Unterstützung

Sandboxes sind virtuelle Partitionen innerhalb einer einzelnen Instanz von Experience Platform. Jede Platform-Instanz unterstützt mehrere Produktions- und Nicht-Produktions-Sandboxes, von denen jede eine eigene Bibliothek mit Platform-Ressourcen unterhält. Mit Nicht-Produktions-Sandboxes können Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen, ohne die Produktions-Sandboxes zu beeinträchtigen. Weiterführende Informationen finden Sie in der [Sandbox-Übersicht](../sandboxes/home.md).

Derzeit gilt für Data Science Workspace die folgende Sandbox-Beschränkung:

- Compute-Ressourcen werden über Produktions- und Nicht-Produktions-Sandboxes hinweg gemeinsam genutzt.

## Nächste Schritte

In diesem Dokument wurden die verschiedenen Arten von Zugriff und Funktionen beschrieben, die in Data Science Workspace verfügbar sind.

Um mehr über Data Science Workspace zu erfahren, z. B. einen vollständigen täglichen Workflow, lesen Sie zunächst den Abschnitt [Anleitung zu Data Science Workspace](./walkthrough.md) Dokumentation. Weitere allgemeine Informationen finden Sie unter [Data Science Workspace - Übersicht](./home.md).
