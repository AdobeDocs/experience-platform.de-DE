---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Erste Schritte mit maschinellem Lernen in Echtzeit
topic: Getting started
translation-type: tm+mt
source-git-commit: c9e6eb41e51ad17ad11b9a669ca5e4cf6c899f8b
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# Erste Schritte mit maschinellem Lernen in Echtzeit

>[!IMPORTANT]
>Das maschinelle Lernen in Echtzeit steht noch nicht allen Benutzern zur Verfügung. Diese Funktion ist alphanumerisch und wird noch getestet. Dieses Dokument kann sich ändern.

Um maschinelles Lernen in Echtzeit nutzen zu können, benötigen Sie Zugriff auf eine Organisation mit Adobe Experience Platform und Data Science Workspace. Darüber hinaus benötigen Sie einen Datensatz in Platform.

Die Leitfäden für Echtzeit-Maschinelles Lernen erfordern ein funktionierendes Verständnis von Python 3, [Jupyter-Notebooks](../jupyterlab/overview.md), Datenwissenschaft und maschinellem Lernen.

## Datensätze in Adobe Experience Platform

Für den Beginn mit maschinellem Lernen in Echtzeit benötigen Sie einen ausgefüllten Datensatz in Experience Platform. Sie haben die Möglichkeit, einen externen Datensatz zu verwenden und ihn in Ihre JupyterLab-Umgebung hochzuladen oder einen neuen Datensatz in der Plattform zu erstellen, falls Sie dies noch nicht getan haben.

>[!NOTE]
>Wenn Sie bereits über einen Datensatz verfügen, den Sie verwenden möchten, können Sie die folgenden zwei Schritte überspringen.

### Verwenden eines externen Datensatzes

Weitere Informationen zur Verwendung eines externen Datensatzes, z. B. zum Hochladen von Daten in Ihre JupyterLab-Umgebung, finden Sie im Lernprogramm zur [Analyse Ihrer Daten mithilfe von Notebooks](../jupyterlab/analyze-your-data.md#external-data).

### Erstellen eines neuen Datensatzes

Um einen neuen Datensatz für den maschinellen Echtzeitunterricht zu erstellen, benötigen Sie ein Data-Schema für Ihren Datensatz. Als Nächstes müssen Sie Daten mit dem von Ihnen erstellten Schema erfassen. Verwenden Sie die folgenden Lernprogramme, um einen Datensatz für Plattform zu erstellen und zu füllen:

- [Erstellen und Ausfüllen eines Datensatzes in der API](../../catalog/datasets/create.md)
- [Erstellen und Ausfüllen eines Datensatzes in der Benutzeroberfläche](../../ingestion/tutorials/ingest-batch-data.md)

## Git und Docker

Wenn Sie planen, ein Modell mithilfe des Data Science Workplace-Rezeptarbeitsablaufs zu schulen, sind Git und Docker erforderlich.

>[!NOTE]
>Sie müssen Git und Docker nicht herunterladen, wenn Sie planen, ein Modell mit einem Python-Notebook zu trainieren, oder wenn Sie Ihr eigenes ONNX-Modell verwenden.

- [Anleitung zur Installation von GPS](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Anleitung zur Dockinginstallation](https://docs.docker.com/get-docker/)

## Nächste Schritte

Nachdem Sie Ihre Daten für maschinelles Lernen in Echtzeit vorbereitet haben, befolgen Sie den Beginn in der Übung zum [Training eines Modells](./training-ml-model.md) , um zu erfahren, wie Sie ein ONNX-Modell erstellen und in den Store für maschinelles Lernen in Echtzeit hochladen können.

