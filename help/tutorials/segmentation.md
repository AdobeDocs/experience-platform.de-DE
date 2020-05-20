---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übungen zur Segmentierung
topic: tutorial
translation-type: tm+mt
source-git-commit: 6705cb699b0785e317a6e437fc8a01ca77266f84
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 8%

---


# Übungen zur Segmentierung

Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren Echtzeit-Daten zum Profil von Kunden generieren können. Diese Segmente werden zentral auf der Plattform konfiguriert und gepflegt und stehen für jede Adobe-Lösung zur Verfügung. Um mehr über die Segmentierung zu erfahren, lesen Sie zunächst die Übersicht über den [Segmentierungsdienst](../segmentation/home.md).

## Erstellen einer Segmentdefinition

Eine Segmentdefinition ist der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe-Audience verwendet wird. Nach der Konzeption werden die in einer Segmentdefinition beschriebenen Regeln verwendet, um qualifizierte Segmentmitglieder für eine Audience zu bestimmen. Die Entwicklung, Prüfung, Vorschau und Speicherung einer Segmentdefinition können über die Plattform-Benutzeroberfläche oder -APIs erfolgen. Um eine Segmentdefinition zu erstellen, führen Sie das [Erstellen eines Segment-API-Tutorials](../segmentation/tutorials/create-a-segment.md) oder das Benutzerhandbuch [für die](../segmentation/ui/overview.md)Segmentaufbau-Benutzeroberfläche aus.

## Bewerten eines Segments und Zugreifen auf Ergebnisse

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie das Segment entweder durch eine geplante Bewertung oder eine On-Demand-Bewertung bewerten. Die geplante Auswertung (auch als &quot;geplante Segmentierung&quot;bezeichnet) ermöglicht es Ihnen, einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt zu erstellen, während die On-Demand-Auswertung die Erstellung eines Segmentauftrags zur sofortigen Erstellung der Audience beinhaltet. Weitere Informationen finden Sie im Tutorial zur [Auswertung und zum Zugriff auf Segmentergebnisse](../segmentation/tutorials/evaluate-a-segment.md).

## Segmentdaten exportieren

Für das Exportieren von Segmenten, die Profil-Daten enthalten, muss zunächst ein Datensatz [erstellt werden, in den die Daten exportiert](../segmentation/tutorials/create-dataset-export-segment.md)werden, und dann ein neuer Exportauftrag initiiert werden. Schritte zum Generieren eines Exportauftrags finden Sie im [Export-API-Lernprogramm](../segmentation/tutorials/export-data.md).

## Zusammenführungsrichtlinien konfigurieren

Mit der Adobe Experience Platform können Sie Daten aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige Ansicht der einzelnen Kunden zu erhalten. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine Übersicht zu schaffen. Mit RESTful-APIs oder der Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen festlegen. Informationen zum Arbeiten mit Zusammenführungsrichtlinien in der Plattform-Benutzeroberfläche finden Sie im [Benutzerhandbuch](../profile/ui/merge-policies.md)zu Zusammenführungsrichtlinien. Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der Echtzeit-Profil-API finden Sie im Entwicklerhandbuch für [Zusammenführungsrichtlinien](../profile/api/merge-policies.md).

## Erzwingen der Datenverwendungskonformität für Segmente

Segmente, die für die Verwendung im Echtzeit-Kundensegment aktiviert sind, enthalten eine Richtlinie-ID zum Zusammenführen innerhalb ihrer Segmentdefinition. Diese Richtlinie zum Zusammenführen enthält Informationen darüber, welche Datensätze in das Segment eingeschlossen werden sollen, die wiederum alle entsprechenden Beschriftungen zur Datenverwendung enthalten. Spezifische Schritte zum Erzwingen der Einhaltung von Datenverwendungsbedingungen für ein Segmentsegment finden Sie im [Tutorial zur Segmentkonformität](../segmentation/tutorials/governance.md).

## (Beta) Streaming-Segmentierung

>[!NOTE]
>Die Streaming-Segmentierung erfolgt in der Beta-Version und steht auf Anfrage zur Verfügung. Die Funktionen und Dokumentation können sich ändern.

Die Streaming-Segmentierung (auch als kontinuierliche Abfrage bezeichnet) ist die Möglichkeit, einen Kunden sofort zu bewerten, sobald ein Ereignis in eine bestimmte Segmentgruppe aufgenommen wird. Mit dieser Funktion können die meisten Segmentregeln jetzt bewertet werden, wenn die Daten an Adobe Experience Platform übergeben werden. Das bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden. Weitere Informationen finden Sie in der Übersicht über die [Streaming-Segmentierung](../segmentation/api/streaming-segmentation.md).

## Segmentierung mehrerer Entitäten

Die Segmentierung mehrerer Entitäten ist die Möglichkeit, Profil-Daten mit zusätzlichen Daten zu erweitern, die auf Produktklassen, Stores oder anderen Nicht-Profil-Klassen basieren. Sobald eine Verbindung besteht, stehen Daten aus zusätzlichen Klassen zur Verfügung, so als wären sie im Profilschema nativ vorhanden. Informationen zum Verschieben finden Sie in der Dokumentation zur Segmentierung [mehrerer Entitäten](../segmentation/multi-entity-segmentation.md).