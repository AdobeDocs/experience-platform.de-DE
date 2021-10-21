---
keywords: Experience Platform;home;beliebte Themen;Segmentierung;Segmentierung;Segmentdienst;Segmente;Segmente;Multientity;Segmentierung mehrerer Entitäten;Segmente;
solution: Experience Platform
title: Übersicht über Segmentierung mehrerer Entitäten
topic-legacy: overview
description: Bei der Segmentierung mit mehreren Entitäten können Sie Profildaten um zusätzliche Daten erweitern, die auf Produkten, Geschäften oder anderen nicht-profilbasierten Klassen beruhen. Sobald eine Verbindung besteht, stehen Daten aus zusätzlichen Klassen zur Verfügung, so als wären sie im Profilschema nativ vorhanden.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: d036ca8c3a378494f776c2bbb05e9d687bd2e201
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 5%

---

# Übersicht zur Segmentierung mehrerer Entitäten

Die Segmentierung mehrerer Entitäten ist eine erweiterte Funktion, die als Teil von Adobe Experience Platform verfügbar ist [!DNL Segmentation Service]. Mit dieser Funktion können Sie [!DNL Real-time Customer Profile] Daten mit zusätzlichen &quot;Nicht-Personen&quot;-Daten (auch als &quot;Dimensionseinheiten&quot; bezeichnet), die von Ihrem Unternehmen definiert werden, z. B. Daten zu Produkten oder Geschäften. Die Segmentierung mehrerer Entitäten bietet Flexibilität bei der Definition von Audiencen-Segmenten auf der Grundlage von Daten, die für Ihre spezifischen geschäftlichen Anforderungen relevant sind, und kann ohne Erfahrung in der Abfrage von Datenbanken durchgeführt werden. Mit der Segmentierung mehrerer Entitäten können Sie wichtige Daten zu Ihren Segmenten hinzufügen, ohne kostspielige Änderungen an den Datenströmen vornehmen zu müssen, oder auf eine Back-End-Datenzusammenführung warten zu müssen.

## Erste Schritte

Die Segmentierung mehrerer Entitäten erfordert ein Verständnis der verschiedenen Adobe Experience Platform-Dienste, die an der Segmentierung beteiligt sind. Bitte lesen Sie die folgende Dokumentation, bevor Sie mit diesem Handbuch fortfahren:

* [[!DNL Real-time Customer Profile]](../profile/home.md): Bietet ein einheitliches Profil für Verbraucher in Echtzeit, basierend auf aggregierten Daten aus mehreren Quellen.
   * [Profil-Guardradien](../profile/guardrails.md): Bewährte Verfahren zum Erstellen von Datenmodellen, unterstützt von [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ermöglicht das Erstellen von Segmenten aus [!DNL Real-time Customer Profile] Daten.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Der standardisierte Rahmen, in dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung von Schemas](../xdm/schema/composition.md#union): Erfahren Sie, wie Sie Schema für die Experience Platform zusammenstellen. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profil und Ereignis gemäß der [Best Practices für die Datenmodellierung](../xdm/schema/best-practices.md).

## Anwendungsfälle

Um den Wert der Segmentierung von mehreren Entitäten zu verdeutlichen, sollten Sie drei standardmäßige Marketing-Anwendungsfälle in Betracht ziehen, die die Herausforderungen veranschaulichen, die sich in den meisten Marketing-Anwendungen stellen:

### Kombination von Online- und Offline-Kaufdaten

Ein Marketingexperte, der eine E-Mail-Kampagne erstellt hat, hat möglicherweise versucht, ein Segment für eine Zielgruppe-Audience zu erstellen, indem er in den letzten drei Monaten die neuesten Einkäufe im Kundengeschäft verwendet hat. Idealerweise würde dieses Segment sowohl den Artikelnamen als auch den Namen des Ladengeschäfts benötigen, in dem der Kauf getätigt wurde. Zuvor hätte die Herausforderung darin bestanden, die Store-ID aus dem Kauf-Ereignis zu erfassen und einem einzelnen KundenProfil zuzuweisen.

### E-Mail-Targeting für Warenkorb-Abbruch

Häufig ist es komplex, Benutzer zu Segmenten zu erstellen und zu qualifizieren, die auf die Warenkorbierung abzielen. Um zu wissen, welche Produkte in eine personalisierte Targeting-Kampagne aufgenommen werden sollen, müssen Daten darüber vorliegen, welche Produkte von den einzelnen Anwendern eingestellt wurden. Diese Daten sind an kommerzielle Ereignis gebunden, die zuvor die Überwachung und Extraktion von Daten erschwert hatten.

## Erstellen von Segmenten mit mehreren Entitäten

Das Erstellen eines Segments mit mehreren Entitäten erfordert zunächst die Definition von Beziehungen zwischen Schemas, bevor die [!DNL Segmentation] API oder Segmentaufbau-Benutzeroberfläche zum Erstellen der Segmentdefinition.

### Beziehungen definieren

Die Definition von Beziehungen innerhalb der Struktur Ihrer Experience Data Model (XDM)-Schema ist ein integraler Bestandteil der Segmenterstellung für mehrere Entitäten. Für Beziehungen muss das Feld im Ziel als primäre Identität des Schemas gekennzeichnet werden. Eine Identität kann nur auf Zeichenfolgen markiert werden und nicht in Arrays markiert werden. Darüber hinaus müssen Beziehungen nicht zwangsläufig ein-/auseinander gehen, da Sie Profil verbinden und Ereignis an mehrere Ziele erleben können.

Die Definition von Beziehungen kann entweder über die Schema-Registry-API oder den Schema-Editor erfolgen. Detaillierte Anweisungen zum Definieren einer Beziehung zwischen zwei Schemas finden Sie in den folgenden Übungen:

* [Definieren einer Beziehung zwischen zwei Schemas mithilfe der API](../xdm/tutorials/relationship-api.md)
* [Definieren einer Beziehung zwischen zwei Schemas mithilfe der Benutzeroberfläche des Schema-Editors](../xdm/tutorials/relationship-ui.md)

### Ein Segment mit mehreren Entitäten erstellen

Sobald Sie die erforderlichen XDM-Beziehungen definiert haben, können Sie mit dem Aufbau eines Segments mit mehreren Entitäten beginnen. Dies kann über die Segmentierungs-API oder die Segmentaufbau-Benutzeroberfläche erfolgen. Weitere Informationen finden Sie in den folgenden Handbüchern:

* [Erstellen eines Segments mithilfe der Segmentierungs-API](./tutorials/create-a-segment.md)
* [Erstellen eines Segments mit der Segmentaufbau-Benutzeroberfläche](./ui/overview.md)

## Segmente für mehrere Entitäten bewerten und darauf zugreifen

Nach dem Erstellen eines Segments können Sie die Segmentergebnisse mithilfe der Segmentierungs-API bewerten und darauf zugreifen. Die Bewertung eines Segments mit mehreren Entitäten ist der Bewertung eines Standardsegments sehr ähnlich. Dieser Prozess kann nur mithilfe der Segmentierungs-API durchgeführt werden. Eine ausführliche Anleitung zur Verwendung der API zum Evaluieren und Zugreifen auf Segmente finden Sie in der [Segmente bewerten und darauf zugreifen](./tutorials/evaluate-a-segment.md) Tutorial.
