---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentierung mit mehreren Entitäten
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 33%

---


# Segmentierung mit mehreren Entitäten

Multi-entity segmentation is the ability to extend [!DNL Profile] data with additional data based on products, stores, or other non-profile classes. Once connected, data from additional classes becomes available as if they were native to the [!DNL Profile] schema.

Um mehr über die Segmentierung mehrerer Entitäten zu erfahren, lesen Sie bitte weiterhin die Dokumentation und ergänzen Sie Ihre Lernerfahrung, indem Sie sich das unten stehende Video ansehen oder die Übersicht über die [Segmentierung](./home.md)erkunden.]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Erste Schritte

Diese Anleitung setzt grundlegende Kenntnisse der verschiedenen Adobe Experience Platform-Diensten voraus, die mit Segmentierung verbunden sind. Bevor Sie mit dieser Anleitung beginnen, lesen Sie bitte die Dokumentation zu folgenden Diensten:

- [!DNL Real-time Customer Profile](../profile/home.md): Bietet ein einheitliches Verbraucherdatenquellen-Profil in Echtzeit, basierend auf aggregierten Daten aus mehreren Quellen.
- [Adobe Experience Platform Segmentation Service](./home.md): Ermöglicht Ihnen das Erstellen von Segmenten aus dem Echtzeit-Kundenprofil.
- [!DNL Experience Data Model (XDM)](../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

## So lassen sich XDM-Beziehungen definieren

Defining relationships with the structure of your [!DNL Experience Data Model] (XDM) schemas is an important and integral part of segment creation.

Dieser Vorgang kann entweder mit der [!DNL Schema Registry] API oder der [!DNL Schema Editor]Methode durchgeführt werden. Eine ausführliche Anleitung zur Nutzung der API für das Definieren einer Beziehung zwischen zwei Schemas finden Sie im Tutorial zum [Definieren einer Beziehung zwischen zwei Schemas mithilfe der API](../xdm/tutorials/relationship-api.md). For a detailed guide on using the [!DNL Schema Editor] to define a relationship between two schemas, please read [the tutorial on defining a relationship between two schemas using the Schema Editor](../xdm/tutorials/relationship-ui.md).

## Erstellen von Segmenten, die XDM-Beziehungen verwenden

Once you have defined your XDM relationships, you can use the [!DNL Segmentation Service] API to build a segment.

Dieser Vorgang kann entweder mit der [!DNL Segmentation] API oder der [!DNL Segment Builder] Benutzeroberfläche durchgeführt werden. For a detailed guide on using the API to build a segment, please read [the tutorial on creating a segment using the Segmentation API](./tutorials/create-a-segment.md). Eine ausführliche Anleitung zum Erstellen eines Segments mit dem Segment Builder finden Sie im [Segment Builder-Benutzerhandbuch](./ui/overview.md).

## So lassen sich Segmente für Segmente mit mehreren Entitäten evaluieren und aufrufen

After creating a segment, you can evaluate and access the segment results using the [!DNL Segmentation Service] API. Die Auswertung eines Segments mit mehreren Entitäten ist der Auswertung eines regulären Segments sehr ähnlich.

This process can only be done using the [!DNL Segmentation Service] API. For a detailed guide on using the API to evaluate and access segments, please read the tutorial on [evaluating and accessing segments](./tutorials/evaluate-a-segment.md).