---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Tutorials für Segmentierung
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren Echtzeit-Kundenprofildaten Zielgruppen generieren können. Diese Segmente werden zentral auf Platform konfiguriert und gepflegt und stehen für jede Adobe-Lösung zur Verfügung.
exl-id: e45de6b5-ff71-4908-ad79-898084763704
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 56%

---

# Tutorials für Segmentierung

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren [!DNL Real-time Customer Profile]-Daten generieren können. Diese Segmente werden zentral konfiguriert und auf [!DNL Platform] gepflegt und sind für jede Adobe leicht zugänglich. Um mehr über die Segmentierung zu erfahren, lesen Sie zunächst die [Segmentation Service – Übersicht](../segmentation/home.md).

## Erstellen einer Segmentdefinition

Eine Segmentdefinition ist der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe verwendet wird. Nach der Konzeption werden die in einer Segmentdefinition beschriebenen Regeln verwendet, um qualifizierte Zielgruppenmitglieder für ein Segment zu bestimmen. Das Entwickeln, Testen, Anzeigen und Speichern einer Segmentdefinition kann über die [!DNL Platform]-Benutzeroberfläche oder -APIs durchgeführt werden. Um eine Segmentdefinition zu erstellen, folgen Sie dem [Tutorial zum Erstellen eines Segment-APIs](../segmentation/tutorials/create-a-segment.md) oder dem [Benutzerhandbuch für die Segmentaufbau-Benutzeroberfläche](../segmentation/ui/overview.md).

## Bewerten eines Segments und Zugriffsergebnisse

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie das Segment entweder durch eine geplante Auswertung oder eine On-Demand-Auswertung bewerten. Die geplante Auswertung (auch als „geplante Segmentierung“ bezeichnet) ermöglicht es Ihnen, einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt zu erstellen, während die On-Demand-Auswertung die Erstellung eines Segmentauftrags zur sofortigen Erstellung der Zielgruppe beinhaltet. Weitere Informationen finden Sie im Tutorial zur [Auswertung und zum Zugriff auf Segmentergebnisse](../segmentation/tutorials/evaluate-a-segment.md).

## Exportieren von Segmentdaten

Für das Exportieren von Segmenten, die [!DNL Profile]-Daten enthalten, ist zunächst [ein Datensatz zu erstellen, in den die Daten exportiert werden.](../segmentation/tutorials/create-dataset-export-segment.md) und anschließend ein neuer Exportauftrag zu starten. Schritte zum Generieren eines Exportauftrags finden Sie im Lernprogramm [zum Auswerten eines Segments](../segmentation/tutorials/evaluate-a-segment.md).

## Konfigurieren von Zusammenführungsrichtlinien

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich einen kompletten Überblick über einzelne Kunden verschaffen können. Beim Zusammenführen dieser Daten sind Zusammenführungsrichtlinien die Regeln, die [!DNL Platform] verwenden, um zu bestimmen, wie die Daten priorisiert werden und welche Daten kombiniert werden, um diese einheitliche Ansicht zu erstellen. Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. Um mit Mergerichtlinien in der [!DNL Platform]-Benutzeroberfläche zu arbeiten, besuchen Sie das [Richtlinien zusammenführen-Benutzerhandbuch](../profile/ui/merge-policies.md). Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API finden Sie im [Entwicklerhandbuch für Zusammenführungsrichtlinien](../profile/api/merge-policies.md).[!DNL Real-time Customer Profile]

## Einhalten der Datennutzungs-Compliance für Segmente

Segmente, die für die Verwendung in [!DNL Real-time Customer Profile] aktiviert sind, enthalten eine Richtlinie-ID zum Zusammenführen innerhalb ihrer Segmentdefinition. Diese Zusammenführungsrichtlinie enthält Informationen darüber, welche Datensätze in das Segment eingeschlossen werden sollen, die wiederum alle entsprechenden Beschriftungen zur Datennutzung enthalten. Spezifische Schritte zum Einhalten der Datennutzungs-Compliance für ein Zielgruppensegment finden Sie im [Tutorial zur Datennutzungs-Compliance für Segmente](../segmentation/tutorials/governance.md).

## Streaming-Segmentierung

Streaming-Segmentierung ist die Möglichkeit, einen Kunden sofort zu bewerten, sobald ein Ereignis in eine bestimmte Segmentgruppe aufgenommen wird. Mit dieser Funktion können die meisten Segmentregeln jetzt bewertet werden, wenn die Daten an Adobe Experience Platform übergeben werden. Dies bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden. Weitere Informationen finden Sie in der [Streaming-Segmentierungs-Übersicht](../segmentation/api/streaming-segmentation.md).

## Segmentierung mit mehreren Entitäten

Die Segmentierung mehrerer Entitäten ist die Möglichkeit, [!DNL Profile]-Daten um zusätzliche Daten zu erweitern, die auf Produktklassen, Stores oder anderen Nicht-Profil-Klassen basieren. Nach der Verbindung stehen Daten aus zusätzlichen Klassen zur Verfügung, als wären sie nativ für das [!DNL Profile]-Schema. Informationen zum Verschieben finden Sie in der [Dokumentation zur Segmentierung mehrerer Entitäten](../segmentation/multi-entity-segmentation.md).
