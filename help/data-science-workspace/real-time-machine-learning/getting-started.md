---
keywords: Experience Platform; Entwicklerhandbuch; Data Science Workspace; beliebte Themen; Echtzeit-maschinelles Lernen
solution: Experience Platform
title: Erste Schritte mit maschinellem Lernen in Echtzeit
topic-legacy: Getting started
description: Im folgenden Dokument werden die Schritte beschrieben, die zum Erstellen eines Modells für maschinelles Lernen in Echtzeit in Adobe Experience Platform erforderlich sind.
exl-id: 90a1c580-f6e7-4517-aa1e-da5092fbc4a2
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Erste Schritte mit maschinellem Lernen in Echtzeit (Alpha)

>[!IMPORTANT]
>
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzern zur Verfügung. Diese Funktion befindet sich in der Alpha-Phase und wird noch getestet. Dieses Dokument kann sich ändern.

Um maschinelles Lernen in Echtzeit nutzen zu können, benötigen Sie Zugriff auf eine mit Adobe Experience Platform und [!DNL Data Science Workspace] bereitgestellte Organisation. Darüber hinaus benötigen Sie einen vollständigen Datensatz, der für Schulungen und Auswertungen verwendet werden kann.

Die Handbücher für maschinelles Lernen in Echtzeit erfordern ein grundlegendes Verständnis von Python 3, [Jupyter Notebooks](../jupyterlab/overview.md), Datenwissenschaft und maschinellem Lernen.

**Schlüsselbegriffe:**

- **DSL:** Domänenspezifische Sprache.
- **Edge:**  Der Scoring-Dienst für maschinelles Lernen in Echtzeit kann auf Edge-Clustern ausgeführt werden, die näher an Ihren Aktivierungen und Anwendungen liegen.
- **Hub:** Das aktuelle Alpha führt den Scoring-Dienst für maschinelles Lernen in Echtzeit auf dem Adobe Experience Platform Hub aus, während sich das Experience Edge-Netzwerk in der Entwicklung befindet.
- **Knoten:** Ein Knoten ist die grundlegende Einheit, aus der Diagramme gebildet werden. Jeder Knoten führt eine bestimmte Aufgabe aus und kann mithilfe von Links miteinander verkettet werden, um ein Diagramm zu bilden, das eine ML-Pipeline darstellt. Die von einem Knoten ausgeführte Aufgabe stellt einen Vorgang für Eingabedaten dar, z. B. eine Transformation von Daten oder Schemas oder eine Inferenz für maschinelles Lernen. Der Knoten gibt den umgewandelten oder abgeleiteten Wert an die nächsten Knoten aus.

## Datensätze in Adobe Experience Platform

Um maschinelles Lernen in Echtzeit verwenden zu können, müssen Sie Zugriff auf einen Datensatz haben. Sie können einen externen Datensatz verwenden und ihn in Ihre [!DNL JupyterLab]-Umgebung hochladen oder, falls noch nicht geschehen, einen neuen Datensatz in Platform erstellen.

>[!NOTE]
>
>Wenn Sie bereits über einen Datensatz verfügen, den Sie verwenden möchten, können Sie zu [Nächste Schritte](#next-steps) überspringen.

### Externen Datensatz verwenden

Weitere Informationen zur Verwendung eines externen Datensatzes, z. B. zum Hochladen von Daten in Ihre [!DNL JupyterLab]-Umgebung, finden Sie im Tutorial zum Analysieren Ihrer Daten mit Notebooks](../jupyterlab/analyze-your-data.md#external-data).[

### Neuen Datensatz erstellen

Um einen neuen Datensatz zur Verwendung im Echtzeit-maschinellen Lernen zu erstellen, benötigen Sie ein Datenschema für Ihren Datensatz. Als Nächstes müssen Sie Daten mithilfe des von Ihnen erstellten Schemas erfassen. Verwenden Sie die folgenden Tutorials, um einen Datensatz für [!DNL Platform] zu erstellen und zu füllen:

- [Erstellen und Ausfüllen eines Datensatzes in der API](../../catalog/datasets/create.md)
- [Erstellen und Ausfüllen eines Datensatzes in der Benutzeroberfläche](../../ingestion/tutorials/ingest-batch-data.md)

## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten für maschinelles Lernen in Echtzeit vorbereitet haben, folgen Sie dem [Handbuch für Notebook-Benutzer für maschinelles Lernen in Echtzeit](./rtml-authoring-notebook.md), um zu erfahren, wie Sie ein ONNX-Modell erstellen und in den Modellspeicher für maschinelles Lernen in Echtzeit hochladen.
