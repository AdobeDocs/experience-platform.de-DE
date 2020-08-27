---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Erste Schritte mit maschinellem Lernen in Echtzeit
topic: Getting started
description: Im folgenden Dokument werden die erforderlichen Schritte zum Erstellen eines Echtzeit-maschinellen Lernmodells in Adobe Experience Platform beschrieben.
translation-type: tm+mt
source-git-commit: 9ba229195892245d29fb4f17b9f2e5cd6c6ea567
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---


# Erste Schritte mit maschinellem Lernen in Echtzeit (Alpha)

>[!IMPORTANT]
>
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzern zur Verfügung. Diese Funktion ist alphanumerisch und wird noch getestet. Dieses Dokument kann sich ändern.

Um maschinelles Lernen in Echtzeit nutzen zu können, benötigen Sie Zugriff auf eine mit Adobe Experience Platform und [!DNL Data Science Workspace]ausgestattete Organisation. Darüber hinaus benötigen Sie einen vollständigen Datensatz, der für Schulungen und Bewertungen verwendet werden kann.

Die Leitfäden für Echtzeit-Maschinelles Lernen erfordern ein funktionierendes Verständnis von Python 3, [Jupyter-Notebooks](../jupyterlab/overview.md), Datenwissenschaft und maschinellem Lernen.

**Schlüsselbegriffe:**

- **DSL:** Domänenspezifische Sprache.
- **Kante:** Der Dienst für maschinelles Lernen in Echtzeit kann auf Edge-Clustern ausgeführt werden, die näher an Ihren Aktivierungen und Anwendungen liegen.
- **Hub:** Der aktuelle Alpha-Knoten führt den Echtzeit-Evaluierungsdienst für maschinelles Lernen auf dem Adobe Experience Platform Hub aus, während das Experience Edge-Netzwerk in der Entwicklung ist.
- **Knoten:** Ein Knoten ist die grundlegende Einheit, aus der Diagramme gebildet werden. Jeder Knoten führt eine bestimmte Aufgabe durch und kann mithilfe von Links miteinander verkettet werden, um ein Diagramm zu bilden, das eine ML-Pipeline darstellt. Die von einer Node ausgeführte Aufgabe stellt einen Vorgang mit Eingabedaten dar, z. B. eine Transformation von Daten oder Schemas oder eine maschinelle Lerninferenz. Die Node gibt den transformierten oder abgeleiteten Wert an die nächste(n) Node(s) aus.

## Datenbestände in Adobe Experience Platform

Um Beginn beim maschinellen Lernen in Echtzeit zu erhalten, müssen Sie Zugriff auf einen Datensatz haben. Sie haben die Möglichkeit, einen externen Datensatz zu verwenden und ihn in Ihre [!DNL JupyterLab] Umgebung hochzuladen oder einen neuen Datensatz in der Plattform zu erstellen, falls Sie dies noch nicht getan haben.

>[!NOTE]
>
>Wenn Sie bereits über einen Datensatz verfügen, den Sie verwenden möchten, können Sie zu den [nächsten Schritten](#next-steps)überspringen.

### Verwenden eines externen Datensatzes

Weitere Informationen zur Verwendung eines externen Datensatzes, z. B. zum Hochladen von Daten in Ihre [!DNL JupyterLab] Umgebung, finden Sie im Lernprogramm zur [Analyse Ihrer Daten mithilfe von Notebooks](../jupyterlab/analyze-your-data.md#external-data).

### Neuen Datensatz erstellen

Um einen neuen Datensatz für den maschinellen Echtzeitunterricht zu erstellen, benötigen Sie ein Data-Schema für Ihren Datensatz. Als Nächstes müssen Sie Daten mit dem von Ihnen erstellten Schema erfassen. Verwenden Sie die folgenden Lernprogramme, um einen Datensatz zu erstellen und zu füllen für [!DNL Platform]:

- [Erstellen und Ausfüllen eines Datensatzes in der API](../../catalog/datasets/create.md)
- [Erstellen und Ausfüllen eines Datensatzes in der Benutzeroberfläche](../../ingestion/tutorials/ingest-batch-data.md)

## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten für maschinelles Lernen in Echtzeit vorbereitet haben, befolgen Sie den Beginn des Benutzerhandbuchs [für maschinelles Lernen in](./rtml-authoring-notebook.md) Echtzeit, um zu erfahren, wie Sie ein ONNX-Modell erstellen und in den Store für maschinelles Lernen in Echtzeit hochladen können.

