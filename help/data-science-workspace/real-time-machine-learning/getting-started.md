---
keywords: Experience Platform;Entwicklerhandbuch;Datenwissenschafts-Arbeitsbereich;beliebte Themen;maschinelles Lernen in Echtzeit;
solution: Experience Platform
title: Erste Schritte beim maschinellem Lernen in Echtzeit
description: Im folgenden Dokument werden die Schritte beschrieben, die zum Erstellen eines Modells für maschinelles Lernen in Echtzeit in Adobe Experience Platform erforderlich sind.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 100%

---

# Erste Schritte beim maschinellem Lernen in Echtzeit (Alpha)

>[!IMPORTANT]
>
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzenden zur Verfügung. Diese Funktion befindet sich in der Alpha-Phase und wird noch getestet. Dieses Dokument kann sich ändern.

Um maschinelles Lernen in Echtzeit nutzen zu können, benötigen Sie Zugriff auf eine Organisation mit Adobe Experience Platform und [!DNL Data Science Workspace]. Darüber hinaus benötigen Sie einen vollständigen Datensatz, der zum Trainieren und Bewerten verwendet werden kann.

Die Handbücher für maschinelles Lernen in Echtzeit erfordern ein grundlegendes Verständnis von Python 3, [Jupyter-Notebooks](../jupyterlab/overview.md), Datenwissenschaft und maschinellem Lernen.

**Schlüsselbegriffe:**

- **DSL:** Domain-spezifische Sprache (Domain Specific Language).
- **Edge:** Der Service zur Bewertung für maschinelles Lernen in Echtzeit kann auf Edge-Clustern ausgeführt werden, die näher zu Ihren Aktivierungen und Anwendungen sind.
- **Hub:** Auf der aktuellen Alpha-Version wird der Service zur Bewertung für maschinelles Lernen in Echtzeit auf dem Adobe Experience Platform Hub ausgeführt. Das Experience Edge Network befindet sich in der Entwicklung.
- **Knoten:** Ein Knoten ist die Grundeinheit, aus der Diagramme gebildet werden. Jeder Knoten führt eine bestimmte Aufgabe aus und kann mithilfe von Verknüpfungen mit anderen Knoten verkettet werden, um ein Diagramm zu bilden, das für eine ML-Pipeline steht. Die von einem Knoten ausgeführte Aufgabe stellt einen Vorgang an Eingabedaten dar, beispielsweise eine Umwandlung von Daten oder Schemata oder eine Schlussfolgerung durch maschinelles Lernen. Der Knoten gibt den transformierten oder abgeleiteten Wert an den oder die nächsten Knoten aus.

## Datensätze in Adobe Experience Platform

Um maschinelles Lernen in Echtzeit verwenden zu können, müssen Sie Zugriff auf einen Datensatz haben. Sie haben die Möglichkeit, einen externen Datensatz zu verwenden und ihn in Ihre [!DNL JupyterLab]-Umgebung hochzuladen oder in Platform einen neuen Datensatz zu erstellen, falls Sie dies noch nicht getan haben.

>[!NOTE]
>
>Wenn Sie bereits über einen Datensatz verfügen, den Sie verwenden möchten, können Sie direkt unter [Nächste Schritte](#next-steps) fortfahren.

### Verwenden eines externen Datensatzes

Weitere Informationen zur Verwendung eines externen Datensatzes, z. B. zum Hochladen von Daten in Ihre [!DNL JupyterLab]-Umgebung, finden Sie im Tutorial zum [Analysieren von Daten mithilfe von Notebooks](../jupyterlab/analyze-your-data.md#external-data).

### Erstellen eines neuen Datensatzes

Um einen neuen Datensatz zum maschinellen Lernen in Echtzeit zu erstellen, benötigen Sie ein Datenschema für Ihren Datensatz. Als Nächstes müssen Sie Daten mithilfe des von Ihnen erstellten Schemas aufnehmen. Verwenden Sie die folgenden Tutorials, um einen Datensatz für [!DNL Platform] zu erstellen und aufzufüllen:

- [Erstellen und Auffüllen eines Datensatzes in der API](../../catalog/datasets/create.md)
- [Erstellen und Auffüllen eines Datensatzes in der Benutzeroberfläche](../../ingestion/tutorials/ingest-batch-data.md)

## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten für maschinelles Lernen in Echtzeit vorbereitet haben, folgen Sie zunächst dem [Benutzerhandbuch zum Notebook für maschinelles Lernen in Echtzeit](./rtml-authoring-notebook.md), um zu erfahren, wie Sie ein ONNX-Modell erstellen und in den Modellspeicher für maschinelles Lernen in Echtzeit hochladen.
