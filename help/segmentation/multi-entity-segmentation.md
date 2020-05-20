---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentierung mehrerer Entitäten
topic: overview
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 4%

---


# Segmentierung mehrerer Entitäten

Die Segmentierung mehrerer Entitäten ist die Möglichkeit, Profil-Daten mit zusätzlichen Daten zu erweitern, die auf Produktklassen, Stores oder anderen Nicht-Profil-Klassen basieren. Sobald eine Verbindung besteht, stehen Daten aus zusätzlichen Klassen zur Verfügung, so als wären sie im Profilschema nativ vorhanden.

Weitere Informationen zur Segmentierung mehrerer Entitäten finden Sie in der [Segmentierungsübersicht](./home.md).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der verschiedenen Adobe Experience Platform-Dienste, die bei der Verwendung der Segmentierung zum Einsatz kommen. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Echtzeit-Profil](../profile/home.md): Bietet ein einheitliches Verbraucherdatenquellen-Profil in Echtzeit, basierend auf aggregierten Daten aus mehreren Quellen.
- [Adobe Experience Platform Segmentation Service](./home.md): Ermöglicht Ihnen das Erstellen von Segmenten aus dem Echtzeit-Kundensegment.
- [Erlebnisdatenmodell (XDM)](../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.

## Definieren von XDM-Beziehungen

Die Definition von Beziehungen zur Struktur Ihrer Experience Data Model-(XDM-)Schema ist ein wichtiger und integraler Bestandteil der Segmenterstellung.

Dieser Vorgang kann entweder mit der Schema Registry API oder dem Schema Editor durchgeführt werden. Eine ausführliche Anleitung zur Verwendung der API zum Definieren einer Beziehung zwischen zwei Schemas finden Sie im Tutorial zum Definieren einer Beziehung zwischen zwei Schemas mithilfe [der API](../xdm/tutorials/relationship-api.md). Eine ausführliche Anleitung zur Verwendung des Schema-Editors zum Definieren einer Beziehung zwischen zwei Schemas finden Sie [im Tutorial zum Definieren einer Beziehung zwischen zwei Schemas mithilfe des Schema-Editors](../xdm/tutorials/relationship-ui.md).

## So erstellen Sie Segmente, die XDM-Beziehungen verwenden

Nachdem Sie Ihre XDM-Beziehungen definiert haben, können Sie die Echtzeit-Kunden-Profil-APIs verwenden, um ein Segment zu erstellen.

Dieser Vorgang kann entweder mit der Echtzeit-Client-Profil-API oder dem Segmentaufbau durchgeführt werden. Eine ausführliche Anleitung zum Erstellen eines Segments mithilfe der API finden Sie in [der Anleitung zum Erstellen eines Segments mit der Echtzeit-Kunden-Profil-API](./tutorials/create-a-segment.md). Eine ausführliche Anleitung zum Erstellen eines Segments mit dem Segmentaufbau finden Sie im Segment Builder-Benutzerhandbuch [](./ui/overview.md).

## So bewerten Sie Segmente für Segmente mit mehreren Entitäten und greifen darauf zu

Nachdem Sie ein Segment erstellt haben, können Sie die Segmentergebnisse mithilfe der Echtzeit-Kunden-Profil-APIs auswerten und darauf zugreifen. Die Bewertung eines Segments mit mehreren Entitäten ist der Bewertung eines regulären Segments sehr ähnlich.

Dieser Vorgang kann nur mit der Echtzeit-Client-Profil-API durchgeführt werden. Eine ausführliche Anleitung zur Verwendung der API zum Auswerten und Zugreifen auf Segmente finden Sie in [der Anleitung zum Auswerten und Zugreifen auf Segmente](./tutorials/evaluate-a-segment.md).