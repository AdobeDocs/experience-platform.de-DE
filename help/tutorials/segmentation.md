---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Tutorials für Segmentierung
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren Echtzeit-Kundenprofildaten Zielgruppen generieren können. Diese Segmente werden zentral auf Platform konfiguriert und gepflegt und stehen für jede Adobe-Lösung zur Verfügung.
exl-id: e45de6b5-ff71-4908-ad79-898084763704
source-git-commit: 36f64b3a1e75c9badaee29e28408504eabac64fe
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 57%

---

# Tutorials für Segmentierung

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren [!DNL Real-time Customer Profile]-Daten Zielgruppen generieren können. Diese Segmente werden zentral auf [!DNL Platform] konfiguriert und gepflegt und stehen für jede Adobe-Lösung zur Verfügung. Um mehr über die Segmentierung zu erfahren, lesen Sie zunächst die [Segmentation Service – Übersicht](../segmentation/home.md).

## Erstellen einer Segmentdefinition

Eine Segmentdefinition ist der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe verwendet wird. Nach der Konzeption werden die in einer Segmentdefinition beschriebenen Regeln verwendet, um qualifizierte Zielgruppenmitglieder für ein Segment zu bestimmen. Die Entwicklung, Prüfung, Vorschau und Speicherung einer Segmentdefinition können über die [!DNL Platform]-Benutzeroberfläche oder -APIs erfolgen. Um eine Segmentdefinition zu erstellen, folgen Sie dem [Tutorial zum Erstellen eines Segment-APIs](../segmentation/tutorials/create-a-segment.md) oder dem [Benutzerhandbuch für die Segmentaufbau-Benutzeroberfläche](../segmentation/ui/overview.md).

## Bewerten eines Segments und Zugriffsergebnisse

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie das Segment entweder durch eine geplante Auswertung oder eine On-Demand-Auswertung bewerten. Die geplante Auswertung (auch als „geplante Segmentierung“ bezeichnet) ermöglicht es Ihnen, einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt zu erstellen, während die On-Demand-Auswertung die Erstellung eines Segmentauftrags zur sofortigen Erstellung der Zielgruppe beinhaltet. Weitere Informationen finden Sie im Tutorial zur [Auswertung und zum Zugriff auf Segmentergebnisse](../segmentation/tutorials/evaluate-a-segment.md).

## Exportieren von Segmentdaten

Für das Exportieren von Segmenten, die [!DNL Profile]-Daten enthalten, muss zunächst [ein Datensatz erstellt werden, in den die Daten exportiert werden](../segmentation/tutorials/create-dataset-export-segment.md), und dann ein neuer Exportauftrag initiiert werden. Schritte zum Generieren eines Exportauftrags finden Sie im Tutorial zum [Bewerten eines Segments](../segmentation/tutorials/evaluate-a-segment.md).

## Konfigurieren von Zusammenführungsrichtlinien

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich einen kompletten Überblick über einzelne Kunden verschaffen können. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen [!DNL Platform] bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden, um eine einheitliche Ansicht zu schaffen. Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. Um mehr über Zusammenführungsrichtlinien und ihre Rolle in der Experience Platform zu erfahren, lesen Sie zunächst den [Überblick über Zusammenführungsrichtlinien](../profile/merge-policies/overview.md).

## Einhalten der Datennutzungs-Compliance für Segmente

Segmente, die für die Verwendung in [!DNL Real-time Customer Profile] aktiviert sind, enthalten eine Kennung für Zusammenführungsrichtlinien innerhalb ihrer Segmentdefinition. Diese Zusammenführungsrichtlinie enthält Informationen darüber, welche Datensätze in das Segment eingeschlossen werden sollen, die wiederum alle entsprechenden Beschriftungen zur Datennutzung enthalten. Spezifische Schritte zum Einhalten der Datennutzungs-Compliance für ein Zielgruppensegment finden Sie im [Tutorial zur Datennutzungs-Compliance für Segmente](../segmentation/tutorials/governance.md).

## Streaming-Segmentierung

Streaming-Segmentierung ist die Möglichkeit, einen Kunden sofort zu bewerten, sobald ein Ereignis in eine bestimmte Segmentgruppe aufgenommen wird. Mit dieser Funktion können die meisten Segmentregeln jetzt ausgewertet werden, wenn die Daten an Adobe Experience Platform übergeben werden. Das bedeutet, dass die Segmentzugehörigkeit ohne Ausführung geplanter Segmentierungsaufträge auf dem neuesten Stand gehalten wird. Weitere Informationen finden Sie in der [Streaming-Segmentierungs-Übersicht](../segmentation/api/streaming-segmentation.md).

## Segmentierung mit mehreren Entitäten

Bei der Segmentierung mit mehreren Entitäten können Sie [!DNL Profile]-Daten um zusätzliche Daten erweitern, die auf Produkten, Geschäften oder anderen nicht profilbasierten Klassen basieren. Sobald eine Verbindung besteht, stehen Daten aus zusätzlichen Klassen zur Verfügung, so als wären sie im [!DNL Profile]-Schema nativ. Informationen zum Verschieben finden Sie in der [Dokumentation zur Segmentierung mehrerer Entitäten](../segmentation/multi-entity-segmentation.md).
