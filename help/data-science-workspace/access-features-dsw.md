---
keywords: Experience Platform;Startseite;Data Science Workspace;beliebte Themen;Zugriffssteuerung;Sandbox;Intelligence Pack;DSW-Funktionen;DSW-Zugriff;Adobe Experience Platform Intelligence;Intelligence;AEP-Intelligenzpaket
solution: Experience Platform
title: Zugriff auf und Funktionen von Data Science Workspace
description: Im folgenden Dokument werden die Berechtigungen für Data Science Workspace und der Zugriff auf Funktionen beschrieben.
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

Im folgenden Dokument werden die Berechtigungen für Data Science Workspace und der Zugriff auf Funktionen beschrieben.

![DSW-Register](./images/access/platform-tabs.png)

- **Notebooks:** Bietet eine interaktive Entwicklungsumgebung ([JupyterLab](./jupyterlab/overview.md)) zum Untersuchen, Analysieren und Modellieren Ihrer Daten auf Experience Platform.
- **Modelle:** Stellt Tools bereit, die zum Erstellen, Veröffentlichen und Speichern erweiterter Rezepte und Modelle für maschinelles Lernen verwendet werden. Weitere Informationen finden Sie im Tutorial [Erstellen und Veröffentlichen eines Modells für maschinelles Lernen](./models-recipes/create-publish-model.md) .
- **Services:** Enthält sowohl von Adobe bereitgestellte Services wie [KI-/ML-Services](../intelligent-services/home.md) als auch benutzerdefinierte Services, die Sie mit Data Science Workspace erstellt haben.

Warum wird nur die Registerkarte „Services“ angezeigt?

- Ihr Unternehmen hat möglicherweise nur Anspruch auf Adobe Real-time Customer Data Platform (Real-Time CDP), das den Kunden-KI-/ML-Service umfasst.

Wenn Sie keine der Registerkarten **Datenwissenschaft** sehen können und Data Science Workspace-Funktionen nutzen möchten, wenden Sie sich an Ihren Unternehmensadministrator, um zu überprüfen, ob Sie über eine Adobe Experience Platform Intelligence-Lizenz verfügen.

## Data Science Workspace-Paketierung

Data Science Workspace-Funktionen sind im Adobe Experience Platform Intelligence-Paket und im Add-on „Advanced Intelligence Pack“ verfügbar

In der folgenden Tabelle sind einige der wichtigsten Unterschiede für Data Science Workspace-Berechtigungen mit und ohne das Add-on „Advanced Intelligence Pack“ aufgeführt:

>[!NOTE]
>
>Sie können mehr als ein Add-on für das Advanced Intelligence Pack lizenzieren, und die erhöhte Kapazität wird zu Ihrer Gesamtberechtigung hinzugefügt. Wenn Sie beispielsweise zwei Add-ons für das Adobe Experience Platform Advanced Intelligence Pack lizenziert haben, haben Sie insgesamt Anspruch auf 20 gleichzeitige Notebook-Benutzer.

| Berechtigung für Data Science Workspace | Nur Adobe Experience Platform Intelligence-Paket | Add-on Adobe Experience Platform Intelligence plus Advanced Intelligence Pack |
| --- | :---: | :---: |
| Anzahl der unterstützten Notebook-Benutzer. | 5 gleichzeitige Benutzer | Mit dem ersten Paket werden 5 gleichzeitige Benutzer hinzugefügt und durch zusätzliche Käufe werden 10 gleichzeitige Benutzer pro Paket hinzugefügt. |
| Ermöglicht integrierte Jupyter-Notebooks für die explorative Datenanalyse und Modellerstellung. | X (Unterstützt R-, Python- und Scala-Bibliotheken) | X (fügt PySpark- und Spark-ML-Bibliotheken hinzu) |
| Native Integration mit Query Service. Möglichkeit, Datensätze mithilfe von SQL in Notebooks zu untersuchen und zu gestalten. | X | X |
| Zugriff auf vordefinierte Notebook-Vorlagen für die prädiktive Analyse. | X | X |
| Trainieren und bewerten Sie Modelle manuell mit Jupyter Notebooks. | X | X |
| Stellen Sie Modelle bereit und operationalisieren Sie sie mit der Möglichkeit, Schulungs- und Ableitungsaufträge zu planen. | | X |
| Rezept-Framework zum einfachen Konfigurieren, Auswerten, Trainieren, Bewerten und Veröffentlichen von Modellen in der Produktion. |  | X |
| Benutzeroberflächengesteuertes Experimentieren und Auswerten von Modellen. | | X |
| Deep Learning-Unterstützung für TensorFlow-Modelle (GPU Compute). | | X |
| Spark-basierte verteilte Datenverarbeitung zum Trainieren und Bewerten großer Datensätze (10 MM + Zeilen). | | X |

## Zugangssteuerung

Die Zugriffskontrolle für Experience Platform wird über die [Adobe Admin Console](https://adminconsole.adobe.com) verwaltet. Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen. Weiterführende Informationen dazu finden Sie unter [Zugangssteuerung – Übersicht](../access-control/home.md).

Um Data Science Workspace verwenden zu können, muss die Berechtigung „Data Science Workspace verwalten“ aktiviert sein. In der folgenden Tabelle sind die Auswirkungen der Aktivierung oder Deaktivierung dieser Berechtigung aufgeführt:

| Berechtigung | Aktiviert | Deaktiviert |
|---|---|---|
| Verwalten des Data Science Workspace | Bietet Zugriff auf alle Services in Data Science Workspace. | Der API- und UI-Zugriff auf alle Services in Data Science Workspace ist deaktiviert. Wenn diese Option deaktiviert ist **kann die Auswahl der** Notebooks **, Modelle** und **Services** nicht erfolgen. <li>Der Zugriff auf **Services** ist möglicherweise weiterhin über Adobe Real-time Customer Data Platform (Real-Time CDP) verfügbar.</li> |

## Sandbox-Unterstützung

Sandboxes sind virtuelle Partitionen innerhalb einer einzelnen Instanz von Experience Platform. Jede Platform-Instanz unterstützt mehrere Produktions- und Nicht-Produktions-Sandboxes, von denen jede eine eigene Bibliothek mit Platform-Ressourcen verwaltet. Nicht-Produktions-Sandboxes ermöglichen es Ihnen, Funktionen zu testen, Experimente durchzuführen und benutzerdefinierte Konfigurationen vorzunehmen, ohne dass sich dies auf Ihre Produktions-Sandboxes auswirkt. Weiterführende Informationen finden Sie in der [Sandbox-Übersicht](../sandboxes/home.md).

Derzeit gelten für Data Science Workspace die folgenden Sandbox-Einschränkungen:

- Rechenressourcen werden über die Produktions- und Nicht-Produktions-Sandboxes hinweg gemeinsam genutzt.

## Nächste Schritte

In diesem Dokument wurden die verschiedenen Zugriffsarten und Funktionen beschrieben, die in Data Science Workspace verfügbar sind.

Um mehr über Data Science Workspace zu erfahren, z. B. einen kompletten täglichen Workflow, lesen Sie zunächst die Dokumentation [Data Science Workspace Walkthrough](./walkthrough.md). Weitere allgemeine Informationen finden Sie unter [Übersicht über Data Science Workspace](./home.md).
