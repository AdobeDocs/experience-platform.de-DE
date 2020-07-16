---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutorials für Segmentierung
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 55%

---


# Tutorials für Segmentierung

Adobe Experience Platform [!DNL Segmentation Service] provides a user interface and RESTful API that allows you to build segments and generate audiences from your [!DNL Real-time Customer Profile] data. These segments are centrally configured and maintained on [!DNL Platform], and are readily accessible by any Adobe solution. Um mehr über die Segmentierung zu erfahren, lesen Sie zunächst die [Segmentierungsdienst-Übersicht](../segmentation/home.md).

## Erstellen einer Segmentdefinition

Eine Segmentdefinition ist der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe verwendet wird. Nach der Konzeption werden die in einer Segmentdefinition beschriebenen Regeln verwendet, um qualifizierte Zielgruppenmitglieder für ein Segment zu bestimmen. The developing, testing, previewing, and saving of a segment definition can be done using the [!DNL Platform] user interface or APIs. Um eine Segmentdefinition zu erstellen, folgen Sie dem [Tutorial zum Erstellen eines Segment-APIs](../segmentation/tutorials/create-a-segment.md) oder dem [Benutzerhandbuch für die Segmentaufbau-Benutzeroberfläche](../segmentation/ui/overview.md).

## Bewerten eines Segments und Zugriffsergebnisse

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie das Segment entweder durch eine geplante Auswertung oder eine On-Demand-Auswertung bewerten. Die geplante Auswertung (auch als „geplante Segmentierung“ bezeichnet) ermöglicht es Ihnen, einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt zu erstellen, während die On-Demand-Auswertung die Erstellung eines Segmentauftrags zur sofortigen Erstellung der Zielgruppe beinhaltet. Weitere Informationen finden Sie im Tutorial zur [Auswertung und zum Zugriff auf Segmentergebnisse](../segmentation/tutorials/evaluate-a-segment.md).

## Exportieren von Segmentdaten

Exporting segments containing [!DNL Profile] data requires first [creating a dataset into which the data will be exported](../segmentation/tutorials/create-dataset-export-segment.md), then initiating a new export job. Schritte zum Generieren eines Exportauftrags finden Sie im [Export-API-Tutorial](../segmentation/tutorials/export-data.md).

## Konfigurieren von Zusammenführungsrichtlinien

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich einen kompletten Überblick über einzelne Kunden verschaffen können. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view. Mithilfe von RESTful-APIs oder der Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, bestehende Richtlinien verwalten und eine für Ihr Unternehmen als Standard verwendete Zusammenführungsrichtlinie einrichten. To work with merge policies in the [!DNL Platform] UI, visit the [merge policies user guide](../profile/ui/merge-policies.md). To work with merge policies using the [!DNL Real-time Customer Profile] API, see the [merge policies developer guide](../profile/api/merge-policies.md).

## Einhalten der Datennutzungs-Compliance für Segmente

Segments that are enabled for use in [!DNL Real-time Customer Profile] contain a merge policy ID within their segment definition. Diese Zusammenführungsrichtlinie gibt an, welche Datensätze in das Segment aufgenommen werden, für die wiederum über ihre Beschriftungen definiert ist, wie die in ihnen enthaltenen Daten genutzt werden dürfen. Eine schrittweise Anleitung dazu, wie Sie Compliance-Vorgaben zur Datennutzung für ein Zielgruppensegment durchsetzen, finden Sie in diesem [Tutorial](../segmentation/tutorials/governance.md).

## Streaming-Segmentierung

Streaming-Segmentierung ist die Möglichkeit, einen Kunden sofort zu bewerten, sobald ein Ereignis in eine bestimmte Segmentgruppe aufgenommen wird. Mit dieser Funktion können die meisten Segmentregeln jetzt bewertet werden, wenn die Daten an die Adobe Experience Platform übergeben werden. Dies bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden. Weitere Informationen finden Sie in der [Streaming-Segmentierungs-Übersicht](../segmentation/api/streaming-segmentation.md).

## Segmentierung mehrerer Entitäten

Multi-entity segmentation is the ability to extend [!DNL Profile] data with additional data based on products, stores, or other non-profile classes. Once connected, data from additional classes becomes available as if they were native to the [!DNL Profile] schema. Informationen zum Verschieben finden Sie in der [Dokumentation zur Segmentierung mehrerer Entitäten](../segmentation/multi-entity-segmentation.md).