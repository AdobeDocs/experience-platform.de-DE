---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentdienst; Segmente; Segmente; mehrere Entitäten; Segmentierung mit mehreren Entitäten; Segmentierung mit mehreren Entitäten; Segmente mit mehreren Entitäten;
solution: Experience Platform
title: Segmentierung mit mehreren Entitäten - Überblick
description: Bei der Segmentierung mit mehreren Entitäten können Sie Profildaten um zusätzliche Daten erweitern, die auf Produkten, Geschäften oder anderen nicht-profilbasierten Klassen beruhen. Sobald eine Verbindung besteht, stehen Daten aus zusätzlichen Klassen zur Verfügung, so als wären sie im Profilschema nativ vorhanden.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 13%

---

# Segmentierung mit mehreren Entitäten - Übersicht

Die Segmentierung mehrerer Entitäten ist eine erweiterte Funktion, die als Teil von Adobe Experience Platform verfügbar ist. [!DNL Segmentation Service]. Mit dieser Funktion können Sie die [!DNL Real-Time Customer Profile] Daten mit zusätzlichen &quot;Nicht-Personen&quot;-Daten (auch als &quot;Dimensionsentitäten&quot;bezeichnet), die Ihr Unternehmen definieren kann, z. B. Daten zu Produkten oder Stores. Die Segmentierung mit mehreren Entitäten bietet Flexibilität bei der Definition von Zielgruppensegmenten basierend auf Daten, die für Ihre individuellen Geschäftsanforderungen relevant sind. Sie kann ohne Expertise auf dem Gebiet der Abfrage von Datenbanken durchgeführt werden. Mit der Segmentierung mit mehreren Entitäten können Sie Ihren Segmenten wichtige Daten hinzufügen, ohne teure Änderungen an Datenströmen vornehmen zu müssen oder auf eine Back-End-Datenzusammenführung zu warten.

## Erste Schritte

Die Segmentierung mehrerer Entitäten erfordert ein Verständnis der verschiedenen Adobe Experience Platform-Dienste, die an der Segmentierung beteiligt sind. Bevor Sie mit diesem Handbuch fortfahren, lesen Sie bitte die folgende Dokumentation:

* [[!DNL Real-Time Customer Profile]](../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus verschiedenen Quellen beruht.
   * [ProfilLimits](../profile/guardrails.md): Best Practices zum Erstellen von Datenmodellen, die von [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ermöglicht Ihnen das Erstellen von Segmenten aus [!DNL Real-Time Customer Profile] Daten.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten ordnet.
   * [Grundlagen der Schemakomposition](../xdm/schema/composition.md#union): Erfahren Sie mehr über Best Practices zum Erstellen von Schemas, die in Experience Platform verwendet werden sollen. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../xdm/schema/best-practices.md) aufgenommen werden.

## Anwendungsfälle

Um den Wert der Segmentierung mit mehreren Entitäten zu veranschaulichen, sollten Sie drei Standardanwendungsfälle für das Marketing berücksichtigen, die die Herausforderungen veranschaulichen, die in den meisten Marketing-Anwendungen auftreten:

### Kombination von Online- und Offline-Kaufdaten

Marketing-Experten, die eine E-Mail-Kampagne erstellen, haben möglicherweise versucht, ein Segment für eine Zielgruppe zu erstellen, indem sie in den letzten drei Monaten die letzten Käufe im Kundenspeicher verwendet haben. Idealerweise würde dieses Segment sowohl den Artikelnamen als auch den Namen des Stores erfordern, in dem der Kauf getätigt wurde. Zuvor bestand die Herausforderung darin, die Store-Kennung aus dem Kaufereignis zu erfassen und sie einem individuellen Kundenprofil zuzuweisen.

### E-Mail-Retargeting für Warenkorbabbruch

Oft ist es komplex, Benutzer zu erstellen und in Segmente zu qualifizieren, die auf den Abbruch des Warenkorbs abzielen. Um zu wissen, welche Produkte in eine personalisierte Retargeting-Kampagne aufgenommen werden sollen, müssen Daten darüber gesammelt werden, welche Produkte von den einzelnen Personen abgebrochen wurden. Diese Daten sind an Commerce-Ereignisse gebunden, bei denen es zuvor schwierig war, Daten zu überwachen und zu extrahieren.

## Erstellen von Segmenten mit mehreren Entitäten

Das Erstellen eines Segments mit mehreren Entitäten erfordert zunächst das Definieren von Beziehungen zwischen Schemas, bevor die [!DNL Segmentation] API oder Segment Builder-Benutzeroberfläche , um die Segmentdefinition zu erstellen.

### Beziehungen definieren

Die Definition von Beziehungen innerhalb der Struktur Ihrer Experience-Datenmodell (XDM)-Schemas ist ein integraler Bestandteil der Segmenterstellung mit mehreren Entitäten. Für Beziehungen muss das Feld im Ziel als primäre Identität dieses Schemas markiert werden. Eine Identität kann nur in Zeichenfolgen markiert werden und nicht in Arrays markiert werden. Darüber hinaus müssen Beziehungen nicht zwingend von eins zu eins sein, da Sie Profile und Erlebnisereignisse mit mehreren Zielen verbinden können.

Die Definition von Beziehungen kann entweder mit der Schema Registry-API oder dem Schema-Editor erfolgen. Ausführliche Anweisungen zum Definieren einer Beziehung zwischen zwei Schemas finden Sie in den folgenden Tutorials:

* [Definieren einer Beziehung zwischen zwei Schemas mithilfe der API](../xdm/tutorials/relationship-api.md)
* [Definieren einer Beziehung zwischen zwei Schemas mithilfe der Schema Editor-Benutzeroberfläche](../xdm/tutorials/relationship-ui.md)

### Erstellen eines Segments mit mehreren Entitäten

Nachdem Sie die erforderlichen XDM-Beziehungen definiert haben, können Sie mit der Erstellung eines Segments mit mehreren Entitäten beginnen. Dies kann entweder über die Segmentation-API oder die Segment Builder-Benutzeroberfläche erfolgen. Weitere Informationen finden Sie in den folgenden Handbüchern:

* [Erstellen eines Segments mithilfe der Segmentation-API](./tutorials/create-a-segment.md)
* [Erstellen eines Segments mithilfe der Benutzeroberfläche von Segment Builder](./ui/overview.md)

## Auswerten und Zugreifen auf Segmente mit mehreren Entitäten

Nachdem Sie ein Segment erstellt haben, können Sie die Segmentergebnisse mithilfe der Segmentation-API auswerten und darauf zugreifen. Die Auswertung eines Segments mit mehreren Entitäten ähnelt der Auswertung eines Standardsegments sehr. Dieser Vorgang kann nur mit der Segmentation-API durchgeführt werden. Eine ausführliche Anleitung zur Verwendung der API für die Auswertung und den Zugriff auf Segmente finden Sie im Abschnitt [Segmenten bewerten und aufrufen](./tutorials/evaluate-a-segment.md) Tutorial.
