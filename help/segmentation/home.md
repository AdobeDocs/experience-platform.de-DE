---
solution: Experience Platform
title: Segmentierungs-Service – Übersicht
description: Erfahren Sie mehr über den Segmentierungs-Service von Adobe Experience Platform und die Rolle, die dieser im Platform-Ökosystem spielt.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 98%

---

# [!DNL Segmentation Service] – Übersicht

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie anhand von Segmentdefinitionen oder anderen Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen erstellen können. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

Dieses Dokument bietet einen Überblick über [!DNL Segmentation Service] und die Rolle, die er in Adobe Experience Platform spielt.

## Erste Schritte mit [!DNL Segmentation Service]

Sie sollten die folgenden Schlüsselbegriffe verstehen, die in diesem Dokument verwendet werden:

- **Segmentierung**: Die Unterteilung einer großen Personengruppe (z. B. Kunden, Interessenten, Benutzer oder Unternehmen) in kleinere Gruppen, die ähnliche Eigenschaften aufweisen und ähnlich auf Marketing-Strategien reagieren.
- **Zielgruppe**: Eine Sammlung von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese Personensammlung kann entweder von Adobe Experience Platform mithilfe von Segmentdefinitionen (plattformgenerierte Zielgruppe) oder aus externen Quellen (extern generierte Zielgruppe) erstellt werden.
- **Segmentdefinition**: Der Regelsatz, den Adobe Experience Platform verwendet, um wichtige Merkmale oder Verhaltensweisen einer Zielgruppe zu beschreiben.

## Funktionsweise der Segmentierung

Bei der Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die eine Profil-Untergruppe in Ihrem Profilspeicher hat, anhand der eine vermarktbare Personengruppe in Ihrem Kundenstamm ermittelt werden kann. Beispielsweise könnten Sie für eine E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Ihre Schuhe zu kaufen?“ eine Zielgruppe bestehend aus allen Anwendern zusammenstellen, die in den letzten 30 Tagen nach Laufschuhen gesucht, den Kauf jedoch nicht abgeschlossen haben.

Nachdem eine Zielgruppe konzeptionell definiert wurde, wird sie in [!DNL Experience Platform] erstellt. Normalerweise werden Zielgruppen vom Marketer oder der Zielgruppenspezialistin bzw. dem -spezialisten erstellt, in manchen Unternehmen kann diese Tätigkeit aber auch durch die Marketing-Abteilung in Zusammenarbeit mit Datenanalystinnen bzw. -analysten erfolgen. Nach Überprüfung der gesendeten Daten an [!DNL Platform], kann die Datenanalystin bzw. der Datenanalyst die Zielgruppe auf zwei Arten erstellen: entweder durch Erstellen einer Segmentdefinition, durch Auswahl der Felder und Werte, die zum Erstellen der Regeln oder Bedingungen der Zielgruppe verwendet werden, oder durch Zusammenstellen einer Zielgruppe mithilfe der Zielgruppenkomposition.

## Erstellen von Zielgruppen

Zielgruppen können in der Adobe Experience Platform auf zwei verschiedene Arten erstellt werden: entweder direkt als Zielgruppen oder über von der Plattform abgeleitete Segmentdefinitionen.

### Zielgruppenkomposition

Beim direkten Erstellen einer Zielgruppe in Platform können Sie die Zielgruppenkomposition verwenden. Informationen zur Verwendung der Zielgruppenkomposition zur Erstellung einer Zielgruppe finden Sie im [Handbuch zur Zielgruppenkomposition](./ui/audience-composition.md).

### Segmentdefinitionen

Unabhängig davon, ob sie über die API oder über [!DNL Segment Builder] erstellt werden, werden Segmentdefinitionen letztendlich über [!DNL Profile Query Language] (PQL) definiert. Dabei wird die konzeptionelle Segmentdefinition in der Sprache beschrieben, mit der die Profile, die den Kriterien entsprechen, abgerufen werden. Weiterführende Informationen finden Sie in der [Übersicht zur PQL](./pql/overview.md).

Informationen zum Erstellen und Verwenden von Segmenten in [!DNL Segment Builder] (die Benutzeroberflächen-Implementierung von [!DNL Segmentation Service]) finden Sie im [Segment Builder-Handbuch](./ui/overview.md).

Informationen zum Erstellen von Segmentdefinitionen mithilfe der API finden Sie im Tutorial [Erstellen von Segmentdefinitionen mithilfe der API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Bei einer Erweiterung eines Schemas müssen bei allen künftigen Uploads auch die neu hinzugefügten Felder entsprechend aktualisiert werden. Weitere Informationen zum Anpassen von [!DNL Experience Data Model] (XDM) finden Sie im [Tutorial zum Schema-Editor](../xdm/tutorials/create-schema-ui.md).
>
>Wenn für den Datensatz ein Wert der Gültigkeitsdauer von Erlebnisereignissen aktiviert ist, könnte sich dies auf die Zugehörigkeit der erstellten Segmentdefinitionen auswirken. Weiterführende Informationen dazu, wie sich diese Funktion auf die Segmentierung auswirken kann, finden Sie im Handbuch zur [Gültigkeitsdauer von Erlebnisereignissen](../profile/event-expirations.md).

## Bewerten von Zielgruppen {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Auswertungsmethoden"
>abstract="Platform unterstützt derzeit drei Methoden zum Auswerten von Zielgruppen: Streaming-Segmentierung, Batch-Segmentierung und Edge-Segmentierung."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Streaming-Auswertung"
>abstract="Die Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Ihre Zielgruppen infolge von Benutzeraktivität aktualisiert."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=de" text="Auswerten von Ereignissen mit Streaming-Segmentierung nahezu in Echtzeit"

Platform unterstützt derzeit drei Methoden zum Auswerten von Zielgruppen: Streaming-Segmentierung, Batch-Segmentierung und Edge-Segmentierung.

### Streaming-Segmentierung  {#streaming}

Die Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Ihre Zielgruppen infolge von Benutzeraktivität aktualisiert. Nachdem eine Zielgruppe erstellt und gespeichert wurde, wird die Segmentdefinition auf in [!DNL Real-Time Customer Profile] eingehende Daten angewendet. Ergänzungen und Entfernungen der Zielgruppe werden regelmäßig verarbeitet, sodass Ihre Zielgruppe auch weiterhin relevant ist.

Weitere Informationen zur Streaming-Segmentierung finden Sie in der [Dokumentation zur Streaming-Segmentierung](./api/streaming-segmentation.md).

### Batch-Segmentierung {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Batch-Auswertung"
>abstract="Als Alternative zum kontinuierlichen Datenauswahlprozess werden bei der Batch-Segmentierung alle Profildaten gleichzeitig mit Segmentdefinitionen verglichen, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung einer Zielgruppe wird sie gespeichert, sodass Sie sie exportieren und weiterverwenden können."

Als Alternative zum kontinuierlichen Datenauswahlprozess werden bei der Batch-Segmentierung alle Profildaten gleichzeitig mit Segmentdefinitionen verglichen, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung wird die resultierende Zielgruppe gespeichert, sodass Sie sie zur Verwendung exportieren können.

Batch-Zielgruppen werden automatisch alle 24 Stunden ausgewertet. Wenn Sie eine Batch-Zielgruppe auf Anfrage auswerten möchten, können Sie einen Segmentierungsvorgang verwenden. Weitere Informationen zu Segmentierungsvorgängen finden Sie in der [Dokumentation zu Segmentierungsvorgängen](./api/segment-jobs.md).

### Edge-Segmentierung {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Edge-Auswertung"
>abstract="Bei der Edge-Segmentierung werden Segmente in Platform sofort im Edge-Netzwerk ausgewertet, was Anwendungsfälle mit Personalisierung auf derselben Seite und auf der nächsten Seite ermöglicht."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=de" text="Handbuch zur Benutzeroberfläche für Edge-Segmentierung"

Mit der Edge-Segmentierung können Segmente in Platform sofort ausgewertet werden. [im Edge-Netzwerk](../edge/home.md), wodurch Anwendungsfälle für die Personalisierung von derselben Seite und der nächsten Seite aktiviert werden.

Weitere Informationen zur Edge-Segmentierung finden Sie in der [API-Dokumentation](./api/edge-segmentation.md) oder [Benutzeroberflächendokumentation](./ui/edge-segmentation.md).

## Zugriff auf Segmentierungsergebnisse

Wie Sie auf eine exportierte Zielgruppe zugreifen können, erfahren Sie im [Tutorial zur Auswertung von Segmentdefinitionen](./tutorials/evaluate-a-segment.md).

## Segmentdefinitionsmetadaten

Segmentdefinitionsmetadaten ermöglichen die Indizierung für den Fall, dass eine Zielgruppe wiederverwendet und/oder kombiniert werden soll.

Das Zusammenstellen einer Segmentdefinition (entweder über die API oder [!DNL Segment Builder]) erfordert, dass Sie einen Namen und eine Zusammenführungsrichtlinie festlegen.

### Segmentdefinitionsnamen

Wenn Sie eine neue Segmentdefinition erstellen, müssen Sie einen Namen angeben. Der Name der Segmentdefinition wird verwendet, um eine bestimmte Segmentdefinition in der von [!DNL Segmentation Service] erstellten Sammlung zu identifizieren. Segmentdefinitionsnamen sollten daher verständlich, prägnant und eindeutig sein.

>[!NOTE]
>
>Bei der Planung einer Segmentdefinition ist zu beachten, dass Segmentdefinitionen von jeder anderen Segmentdefinition referenziert und mit ihr kombiniert werden können. Erwägen Sie bei der Auswahl eines Namens die Möglichkeit, dass Ihre Segmentdefinition wiederverwendbare Teile enthalten kann.

### Zusammenführungsrichtlinien

Zusammenführungsrichtlinien sind Regeln, die von [!DNL Profile] verwendet werden, um zu bestimmen, wie Daten priorisiert und unter bestimmten Bedingungen zu einer vereinigten Ansicht kombiniert werden.

Wenn keine Zusammenführungsrichtlinie definiert ist, wird die Standard-Zusammenführungsrichtlinie von [!DNL Platform] verwendet. Wenn Sie lieber eine für Ihr Unternehmen spezifische Zusammenführungsrichtlinie verwenden möchten, können Sie eine eigene erstellen und diese als Standard für Ihr Unternehmen festlegen.

Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im [Handbuch zu Zusammenführungsrichtlinien](../profile/api/merge-policies.md).

>[!NOTE]
>
>Die Schätzung der Zielgruppengrößen basiert auf der standardmäßigen Profilzusammenführungsrichtlinie des Unternehmens.

### Andere Segmentdefinitionsmetadaten

Zusätzlich zu Name und Zusammenführungsrichtlinie bietet [!DNL Segment Builder] ein zusätzliches Metadatenfeld zur Beschreibung, in dem Sie den Zweck Ihrer Segmentdefinition zusammenfassen können.

## Erweiterte Segmentierungsfunktionen

Segmentdefinitionen können so konfiguriert werden, dass sie kontinuierlich eine Zielgruppe generieren, indem die [Streaming-Datenaufnahme](../ingestion/streaming-ingestion/overview.md) mit einer der folgenden erweiterten Segmentierungsfunktionen kombiniert wird:
- [Sequenzielle Segmentierung](#sequential)
- [Dynamische Segmentierung](#dynamic)
- [Segmentierung mit mehreren Entitäten](#multi-entity)

Diese erweiterten Funktionen werden in den folgenden Abschnitten ausführlicher erläutert.

### Sequenzielle Segmentierung {#sequential}

Eine standardmäßige Customer Journey ist sequenziell. Mit Adobe Experience Platform können Sie eine geordnete Zielgruppenreihe definieren, die eine Journey widerspiegelt. Dabei werden Sequenzen von Ereignissen unmittelbar bei ihrem Auftreten erfasst. Über die Timeline für visuelle Ereignisse in [!DNL Segment Builder] können Sie Ereignisse in der gewünschten Reihenfolge anordnen.

Ein Beispiel für eine Customer Journey, für die eine sequenzielle Segmentierung erforderlich ist, wäre Produkt ansehen > Produkt hinzufügen > Kasse > Kein Kauf.

### Dynamische Segmentierung {#dynamic}

Mit der dynamischen Segmentierung können die Skalierbarkeitsprobleme gelöst werden, die Marketing-Fachleute beim Erstellen von Zielgruppen für Marketing-Kampagnen üblicherweise haben.

Im Gegensatz zur statischen Segmentierung, bei der Sie jeden möglichen Anwendungsfall explizit und wiederholt erfassen müssen, verwendet die dynamische Segmentierung Variablen, um die Regellogik zu erstellen und Beziehungen dynamisch auszudrücken.

Bei dieser erweiterten Segmentierungsfunktion sollte eine Datenarchitektin oder ein Datenarchitekt mit einer Marketing-Fachkraft zusammenarbeiten, um Kundinnen und Kunden zu identifizieren, die außerhalb ihres Bundesstaates Einkäufe getätigt haben.

Für die statische Segmentierung müssen Sie einzelne Segmente mit einem eindeutigen Attribut für den heimatlichen Bundesstaat definieren, bevor Sie nach Kaufereignissen filtern, die nicht dem heimatlichen Bundesstaat entsprechen. Eine explizite Segmentdefinition dieses Typs würde lauten: „Ich suche nach Personen aus Utah, für die der Bundesstaat des Kaufs nicht Utah ist“. Wenn Sie mit dieser Methode eine Zielgruppe erstellen möchten, müssen Sie für jeden US-Bundesstaat eine Segmentdefinition, also insgesamt 50 Segmente, definieren.

Aufgrund der verschiedenen Kombinationen von Segmentdefinitionen, die sich unweigerlich bei der Skalierung ergeben, wird der manuelle Prozess, der für eine statische Segmentierung erforderlich ist, zeitaufwendiger, was wiederum die Effizienz der Mitarbeiter verringert.

Indem Sie dem Attribut „Bundesstaat des Kaufs“ eine Variable zuweisen, wird Ihre dynamische Segmentdefinition vereinfacht und besagt: „Finde einen Kauf, bei dem der Bundesstaat dieses Kaufs nicht mit dem Heimatstaat der Kundin bzw. des Kunden übereinstimmt“. Auf diese Weise können Sie dann 50 statische Segmente zu einer einzigen dynamischen Segmentdefinition zusammenfassen.

### Segmentierung mit mehreren Entitäten {#multi-entity}

Mit der erweiterten Segmentierungsfunktion für mehrere Entitäten können Sie die Daten von [!DNL Real-Time Customer Profile] mit zusätzlichen Daten erweitern, die auf Produkten, Geschäften oder anderen Nicht-Personen-Entitäten basieren und auch als „Dimensionsentitäten“ bezeichnet werden. Folglich kann [!DNL Segmentation Service] während der Segmentdefinition auf zusätzliche Felder zugreifen, als ob sie nativ im [!DNL Profile]-Datenspeicher enthalten wären. Die Segmentierung mehrerer Entitäten bietet Flexibilität bei der Identifizierung von Zielgruppen anhand von Daten, die für Ihre individuellen Geschäftsanforderungen relevant sind. Weitere Informationen, einschließlich Anwendungsfällen und Workflows, finden Sie im [Handbuch zur Segmentierung mehrerer Entitäten](multi-entity-segmentation.md).

## [!DNL Segmentation Service]-Datentypen

[!DNL Segmentation Service] unterstützt eine Vielzahl von einfachen und komplexen Datentypen. Detaillierte Informationen, einschließlich einer Liste der unterstützten Datentypen, finden Sie im [Handbuch zu unterstützten Datentypen](./data-types.md).

## Nächste Schritte

[!DNL Segmentation Service] bietet einen konsolidierten Workflow zum Erstellen von Zielgruppen aus [!DNL Real-Time Customer Profile]-Daten.

Für weitere Informationen zur Verwendung der Segmentierungsdienst-Benutzeroberfläche lesen Sie bitte den [Überblick über die Segmentierungs-Service-Benutzeroberfläche](./ui/overview.md).

Informationen zum Erstellen von Zielgruppen in der Benutzeroberfläche finden Sie im [Handbuch zur Zielgruppenkomposition](./ui/audience-composition.md). Informationen zum Definieren von Segmentdefinitionen in der Benutzeroberfläche finden Sie im [Segment Builder-Handbuch](./ui/overview.md). Informationen zum Erstellen von Segmentdefinitionen mithilfe der API finden Sie im Tutorial [Erstellen von Segmentdefinitionen mithilfe der API](./tutorials/create-a-segment.md).
