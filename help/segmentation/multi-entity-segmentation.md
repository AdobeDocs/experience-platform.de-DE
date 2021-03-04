---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierung;Segmentierung;Segmentdienst;Segmente;Multientity;Segmentierung mehrerer Entitäten;Segmente;
solution: Experience Platform
title: Übersicht über die Segmentierung mehrerer Entitäten
topic: Übersicht
description: Bei der Segmentierung mit mehreren Entitäten können Sie Profildaten um zusätzliche Daten erweitern, die auf Produkten, Geschäften oder anderen nicht-profilbasierten Klassen beruhen. Sobald eine Verbindung besteht, stehen Daten aus zusätzlichen Klassen zur Verfügung, so als wären sie im Profilschema nativ vorhanden.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 6%

---


# Übersicht über die Segmentierung mehrerer Entitäten

Die Segmentierung mehrerer Entitäten ist eine erweiterte Funktion, die als Teil von Adobe Experience Platform [!DNL Segmentation Service] verfügbar ist. Mit dieser Funktion können Sie [!DNL Real-time Customer Profile]-Daten um weitere &quot;Nicht-Personen&quot;-Daten erweitern (auch als &quot;Dimensionseinheiten&quot;bezeichnet), die Ihr Unternehmen definieren kann, z. B. Daten zu Produkten oder Stores. Die Segmentierung mehrerer Entitäten bietet Flexibilität bei der Definition von Segmenten auf der Grundlage von Daten, die für Ihre spezifischen Geschäftsanforderungen relevant sind, und kann ohne Kenntnisse in der Datenbankabfrage durchgeführt werden. Mit der Segmentierung mehrerer Entitäten können Sie wichtige Daten zu Ihren Segmenten hinzufügen, ohne dass Sie kostspielige Änderungen an den Datenströmen vornehmen oder auf eine Back-End-Datenzusammenführung warten müssen.

## Erste Schritte

Die Segmentierung mehrerer Entitäten erfordert ein funktionierendes Verständnis der verschiedenen Adobe Experience Platform-Dienste, die an der Segmentierung beteiligt sind. Bevor Sie mit diesem Handbuch fortfahren, lesen Sie bitte die folgende Dokumentation:

* [[!DNL Real-time Customer Profile]](../profile/home.md): Bietet ein einheitliches Verbraucherdatenquellen-Profil in Echtzeit, basierend auf aggregierten Daten aus mehreren Quellen.
   * [Profil-Guardrails](../profile/guardrails.md): Bewährte Verfahren zum Erstellen von Datenmodellen, die von unterstützt werden  [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ermöglicht Ihnen das Erstellen von Segmenten aus  [!DNL Real-time Customer Profile] Daten.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../xdm/schema/composition.md#union) des Schemas: Hier lernen Sie bewährte Verfahren zum Erstellen von Schemas, die in der Experience Platform verwendet werden sollen.

## Anwendungsbeispiele

Um den Wert der Segmentierung mehrerer Entitäten zu veranschaulichen, sollten Sie drei Standardanwendungsfälle für das Marketing erwägen, die die Herausforderungen in den meisten Marketing-Anwendungen illustrieren:

### Kombinieren von Online- und Offline-Kaufdaten

Ein Marketingspezialist, der eine E-Mail-Kampagne erstellt hat, hat möglicherweise versucht, ein Segment für eine Audience der Zielgruppe zu erstellen, indem er in den letzten drei Monaten Käufe im Kundenspeicher verwendet hat. Idealerweise würde dieses Segment sowohl den Artikelnamen als auch den Namen des Geschäfts erfordern, in dem der Kauf getätigt wurde. Zuvor hätte die Herausforderung darin bestehen müssen, die Store-ID aus dem Kauf-Ereignis zu erfassen und sie einem einzelnen Profil zuzuweisen.

### E-Mail-Retargeting für Warenkorbabbruch

Es ist häufig komplex, Benutzer zu erstellen und in Segmente einzustufen, die auf den Abbruch des Einkaufswagens abzielen. Um zu wissen, welche Produkte in eine personalisierte Targeting-Kampagne aufgenommen werden sollen, müssen Daten darüber vorliegen, welche Produkte von den einzelnen Kunden abgeschafft wurden. Diese Daten sind an kommerzielle Ereignis gebunden, die früher Schwierigkeiten hatten, Daten zu überwachen und zu extrahieren.

## Erstellen von Segmenten mit mehreren Entitäten

Zum Erstellen eines Segments mit mehreren Entitäten müssen zunächst Beziehungen zwischen Schemas definiert werden, bevor die API oder die Segmentaufbau-Benutzeroberfläche zum Erstellen der Segmentdefinition verwendet werden.[!DNL Segmentation]

### Beziehungen definieren

Die Definition von Beziehungen innerhalb der Struktur Ihrer Experience Data Model-(XDM-)Schema ist ein integraler Bestandteil der Segmenterstellung für mehrere Entitäten. Bei Beziehungen muss das Feld im Ziel als primäre Identität des Schemas gekennzeichnet werden. Eine Identität kann nur in Zeichenfolgen markiert werden und kann nicht in Arrays markiert werden. Darüber hinaus müssen Beziehungen nicht unbedingt einzeln sein, da Sie Profil und Erlebnis-Ereignis mit mehreren Zielen verbinden können.

Die Definition von Beziehungen kann entweder mit der Schema Registry API oder dem Schema Editor erfolgen. Ausführliche Anweisungen zum Definieren einer Beziehung zwischen zwei Schemas finden Sie in den folgenden Übungen:

* [Definieren einer Beziehung zwischen zwei Schemas mithilfe der API](../xdm/tutorials/relationship-api.md)
* [Definieren einer Beziehung zwischen zwei Schemas mithilfe der Benutzeroberfläche des Schema-Editors](../xdm/tutorials/relationship-ui.md)

### Erstellen eines Segments mit mehreren Entitäten

Nachdem Sie die erforderlichen XDM-Beziehungen definiert haben, können Sie mit der Erstellung eines Segments mit mehreren Entitäten beginnen. Dies kann entweder mit der Segmentierungs-API oder der Segment Builder-Benutzeroberfläche erfolgen. Für weitere Informationen wählen Sie bitte aus den folgenden Handbüchern:

* [Erstellen eines Segments mit der Segmentierungs-API](./tutorials/create-a-segment.md)
* [Erstellen eines Segments mithilfe der Benutzeroberfläche des Segmentaufbaus](./ui/overview.md)

## Bewerten und Zugreifen auf Segmente mit mehreren Entitäten

Nachdem Sie ein Segment erstellt haben, können Sie die Segmentergebnisse mithilfe der Segmentierungs-API bewerten und darauf zugreifen. Die Bewertung eines Segments mit mehreren Entitäten ist der Bewertung eines Standardsegments sehr ähnlich. Dieser Vorgang kann nur mit der Segmentierungs-API durchgeführt werden. Eine ausführliche Anleitung, die zeigt, wie Sie mit der API Segmente bewerten und aufrufen können, finden Sie im Lehrgang [Segmente bewerten und darauf zugreifen](./tutorials/evaluate-a-segment.md).
