---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentierung mit mehreren Entitäten
topic: overview
translation-type: tm+mt
source-git-commit: f44e42a4faa3b10f147dbaf929048054ce0bec42
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 65%

---


# Segmentierung mit mehreren Entitäten

Bei der Segmentierung mit mehreren Entitäten können Sie Profildaten um zusätzliche Daten erweitern, die auf Produkten, Geschäften oder anderen nicht-profilbasierten Klassen beruhen. Sobald eine Verbindung besteht, stehen Daten aus zusätzlichen Klassen zur Verfügung, so als wären sie im Profilschema nativ vorhanden.

Um mehr über die Segmentierung mehrerer Entitäten zu erfahren, lesen Sie bitte weiterhin die Dokumentation und ergänzen Sie Ihre Lernerfahrung, indem Sie sich das unten stehende Video ansehen oder die Übersicht über die [Segmentierung](./home.md)erkunden.]

>[!VIDEO](https://video.tv.adobe.com/v/28947?quality=12&learn=on)

## Erste Schritte

Diese Anleitung setzt grundlegende Kenntnisse der verschiedenen Adobe Experience Platform-Diensten voraus, die mit Segmentierung verbunden sind. Bevor Sie mit dieser Anleitung beginnen, lesen Sie bitte die Dokumentation zu folgenden Diensten:

- [Echtzeit-Kundenprofil](../profile/home.md): Bietet ein einheitliches echtzeitbasiertes Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen beruht.
- [Adobe Experience Platform Segmentation Service](./home.md): Ermöglicht Ihnen das Erstellen von Segmenten aus dem Echtzeit-Kundenprofil.
- [Experience-Datenmodell (XDM)](../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.

## So lassen sich XDM-Beziehungen definieren

Die Definition von Beziehungen mit der Struktur Ihrer Experience-Datenmodell (XDM-)Schemas ist ein wichtiger und integraler Bestandteil der Erstellung von Segmenten.

Dieser Vorgang kann entweder mit der Schema Registry-API oder dem Schema-Editor durchgeführt werden. Eine ausführliche Anleitung zur Nutzung der API für das Definieren einer Beziehung zwischen zwei Schemas finden Sie im Tutorial zum [Definieren einer Beziehung zwischen zwei Schemas mithilfe der API](../xdm/tutorials/relationship-api.md). Eine ausführliche Anleitung zur Nutzung des Schema-Editors für das Definieren einer Beziehung zwischen zwei Schemas finden Sie im Tutorial zum [Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors](../xdm/tutorials/relationship-ui.md).

## Erstellen von Segmenten, die XDM-Beziehungen verwenden

Nachdem Sie Ihre XDM-Beziehungen definiert haben, können Sie mit der Segmentierungsdienst-API ein Segment erstellen.

Dieser Vorgang kann entweder mit der Segmentierungs-API oder der Segment Builder-Benutzeroberfläche durchgeführt werden. For a detailed guide on using the API to build a segment, please read [the tutorial on creating a segment using the Segmentation API](./tutorials/create-a-segment.md). Eine ausführliche Anleitung zum Erstellen eines Segments mit dem Segment Builder finden Sie im [Segment Builder-Benutzerhandbuch](./ui/overview.md).

## So lassen sich Segmente für Segmente mit mehreren Entitäten evaluieren und aufrufen

After creating a segment, you can evaluate and access the segment results using the [!DNL Segmentation Service] API. Die Auswertung eines Segments mit mehreren Entitäten ist der Auswertung eines regulären Segments sehr ähnlich.

This process can only be done using the [!DNL Segmentation Service] API. For a detailed guide on using the API to evaluate and access segments, please read the tutorial on [evaluating and accessing segments](./tutorials/evaluate-a-segment.md).