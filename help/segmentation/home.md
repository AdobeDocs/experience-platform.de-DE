---
solution: Experience Platform
title: Segmentierungs-Service – Übersicht
description: Erfahren Sie mehr über den Segmentierungs-Service von Adobe Experience Platform und die Rolle, die dieser im Platform-Ökosystem spielt.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 93%

---

# [!DNL Segmentation Service] – Übersicht

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihrer [!DNL Real-Time Customer Profile] Daten. Diese Zielgruppen werden zentral konfiguriert und verwaltet in [!DNL Platform]und für jede Adobe leicht zugänglich sind.

Dieses Dokument bietet einen Überblick über [!DNL Segmentation Service] und die Rolle, die er in Adobe Experience Platform spielt.

## Erste Schritte mit [!DNL Segmentation Service]

Sie sollten die folgenden Schlüsselbegriffe verstehen, die in diesem Dokument verwendet werden:

- **Segmentierung**: Die Unterteilung einer großen Personengruppe (z. B. Kunden, Interessenten, Benutzer oder Unternehmen) in kleinere Gruppen, die ähnliche Eigenschaften aufweisen und ähnlich auf Marketing-Strategien reagieren.
- **Zielgruppe**: Eine Sammlung von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese Personensammlung kann entweder von Adobe Experience Platform mithilfe von Segmentdefinitionen (plattformgenerierte Zielgruppe) oder aus externen Quellen (extern generierte Zielgruppe) erstellt werden.
- **Segmentdefinition**: Der Regelsatz, den Adobe Experience Platform verwendet, um die Hauptmerkmale oder das Verhalten einer Zielgruppe zu beschreiben.

## Funktionsweise der Segmentierung

Bei der Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die eine Profil-Untergruppe in Ihrem Profilspeicher hat, anhand der eine vermarktbare Personengruppe in Ihrem Kundenstamm ermittelt werden kann. Beispielsweise könnten Sie für eine E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Ihre Schuhe zu kaufen?“ eine Zielgruppe bestehend aus allen Anwendern zusammenstellen, die in den letzten 30 Tagen nach Laufschuhen gesucht, den Kauf jedoch nicht abgeschlossen haben.

Nachdem ein Segment konzeptionell definiert wurde, wird es in [!DNL Experience Platform] erstellt. Normalerweise werden Segmente vom Marketing- oder Zielgruppenspezialisten erstellt, in manchen Unternehmen kann diese Tätigkeit aber auch durch die Marketing-Abteilung in Zusammenarbeit mit Datenanalysten erfolgen. Nach der Überprüfung der an [!DNL Platform] gesendeten Daten legt der Datenanalyst die Segmentdefinition fest. Dazu wählt er die Felder und Werte aus, die zum Erstellen der Regeln oder Bedingungen des Segments verwendet werden sollen. Dies erfolgt über die Benutzeroberfläche oder die API.

## Erstellen von Segmenten

Unabhängig davon, ob die API oder [!DNL Segment Builder] verwendet wird, werden die Segmente letztlich mithilfe der [!DNL Profile Query Language] (PQL) definiert. Dabei wird die konzeptionelle Segmentdefinition in der Sprache beschrieben, mit der die Profile, die den Kriterien entsprechen, abgerufen werden. Weiterführende Informationen finden Sie in der [Übersicht zur PQL](./pql/overview.md).

Informationen zum Erstellen und Verwenden von Segmenten in [!DNL Segment Builder] (die Benutzeroberflächen-Implementierung von [!DNL Segmentation Service]) finden Sie im [Segment Builder-Handbuch](./ui/overview.md).

Informationen zum Erstellen von Segmentdefinitionen mithilfe der API finden Sie im Tutorial zum [Erstellen von Zielgruppensegmenten mithilfe der API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Bei einer Erweiterung eines Schemas müssen bei allen künftigen Uploads auch die neu hinzugefügten Felder entsprechend aktualisiert werden. Weitere Informationen zum Anpassen von [!DNL Experience Data Model] (XDM) finden Sie im [Tutorial zum Schema-Editor](../xdm/tutorials/create-schema-ui.md).
>
>Wenn für den Datensatz ein Wert der Gültigkeitsdauer von Erlebnisereignissen aktiviert ist, könnte sich dies auf die Zugehörigkeit des erstellten Segments auswirken. Weiterführende Informationen dazu, wie sich diese Funktion auf die Segmentierung auswirken kann, finden Sie im Handbuch zur [Gültigkeitsdauer von Erlebnisereignissen](../profile/event-expirations.md).

## Auswerten von Segmenten {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="Auswertungsmethoden"
>abstract="Platform unterstützt derzeit drei Methoden zum Auswerten von Segmenten: Streaming-Segmentierung, Batch-Segmentierung und Edge-Segmentierung."

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="Streaming-Auswertung"
>abstract="Die Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Ihre Segmente infolge von Benutzeraktivitäten aktualisiert."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=de" text="Auswerten von Ereignissen mit Streaming-Segmentierung nahezu in Echtzeit"

Platform unterstützt derzeit drei Methoden zum Auswerten von Segmenten: Streaming-Segmentierung, Batch-Segmentierung und Edge-Segmentierung.

### Streaming-Segmentierung  {#streaming}

Die Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Ihre Segmente infolge von Benutzeraktivitäten aktualisiert. Nachdem ein Segment erstellt und gespeichert wurde, wird die Segmentdefinition auf in [!DNL Real-Time Customer Profile] eingehende Daten angewendet. Segmenthinzufügungen und -entfernungen werden regelmäßig verarbeitet, um sicherzustellen, dass Ihre Zielgruppe relevant bleibt.

Weitere Informationen zur Streaming-Segmentierung finden Sie in der [Dokumentation zur Streaming-Segmentierung](./api/streaming-segmentation.md).

### Batch-Segmentierung {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="Batch-Auswertung"
>abstract="Als Alternative zum kontinuierlichen Datenauswahlprozess werden bei der Batch-Segmentierung alle Profildaten gleichzeitig mit Segmentdefinitionen verglichen, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung eines Segments wird es gespeichert, sodass Sie es exportieren und weiterverwenden können."

Als Alternative zum kontinuierlichen Datenauswahlprozess werden bei der Batch-Segmentierung alle Profildaten gleichzeitig mit Segmentdefinitionen verglichen, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung eines Segments wird es gespeichert, sodass Sie es exportieren und weiterverwenden können.

Batch-Segmente werden automatisch alle 24 Stunden ausgewertet. Wenn Sie ein Batch-Segment on demand auswerten möchten, können Sie einen Segmentierungsvorgang verwenden. Weitere Informationen zu Segmentierungsvorgängen finden Sie in der [Dokumentation zu Segmentierungsvorgängen](./api/segment-jobs.md).

### Edge-Segmentierung {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="Edge-Auswertung"
>abstract="Bei der Edge-Segmentierung werden Segmente in Platform sofort in Experience Edge ausgewertet, was Anwendungsfälle mit Personalisierung auf derselben Seite und auf der nächsten Seite ermöglicht."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=de" text="Handbuch zur Benutzeroberfläche für Edge-Segmentierung"

Bei der Edge-Segmentierung werden Segmente in Platform sofort [in Experience Edge](../edge/home.md) ausgewertet, was Anwendungsfälle mit Personalisierung auf derselben Seite und auf der nächsten Seite ermöglicht.

Weitere Informationen zur Edge-Segmentierung finden Sie in der [API-Dokumentation](./api/edge-segmentation.md) oder [Benutzeroberflächendokumentation](./ui/edge-segmentation.md).

## Zugriff auf Segmentierungsergebnisse

Informationen darüber, wie Sie auf ein exportiertes Segment zugreifen können, finden Sie im [Tutorial zur Segmentauswertung](./tutorials/evaluate-a-segment.md).

## Segmentmetadaten

Segmentmetadaten ermöglichen die Indizierung für den Fall, dass ein Segment wiederverwendet und/oder kombiniert werden soll.

Zur Erstellung Ihrer Segmente (entweder über die API oder [!DNL Segment Builder]) müssen Sie einen Segmentnamen und eine Zusammenführungsrichtlinie definieren.

### Segmentnamen

Beim Erstellen eines neuen Segments müssen Sie einen Segmentnamen angeben. Der Segmentname wird verwendet, um ein bestimmtes Segment in der von [!DNL Segmentation Service] erstellten Sammlung zu identifizieren. Segmentnamen sollten daher verständlich, prägnant und eindeutig sein.

>[!NOTE]
>
>Beachten Sie bei der Planung eines Segments, dass Segmente durch ein beliebiges anderes Segment referenziert und mit ihm kombiniert werden können. Erwägen Sie bei der Auswahl eines Namens die Möglichkeit, dass Ihr Segment wiederverwendbare Teile enthalten kann.

### Zusammenführungsrichtlinien

Zusammenführungsrichtlinien sind Regeln, die von [!DNL Profile] verwendet werden. um zu bestimmen, wie Daten priorisiert und unter bestimmten Bedingungen zu einer vereinigten Ansicht kombiniert werden.
Wenn keine Zusammenführungsrichtlinie definiert ist, wird die Standard-Zusammenführungsrichtlinie von [!DNL Platform] verwendet. Wenn Sie lieber eine für Ihr Unternehmen spezifische Zusammenführungsrichtlinie verwenden möchten, können Sie eine eigene erstellen und diese als Standard für Ihr Unternehmen festlegen.

Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im [Handbuch zu Zusammenführungsrichtlinien](../profile/api/merge-policies.md).

>[!NOTE]
>
>Die Schätzung der Zielgruppengrößen basiert auf der standardmäßigen Profilzusammenführungsrichtlinie des Unternehmens.

### Andere Segmentmetadaten

Zusätzlich zum Segmentnamen und zur Zusammenführungsrichtlinien besitzt [!DNL Segment Builder] ein zusätzliches Metadatenfeld zur Segmentbeschreibung, in dem Sie den Zweck Ihrer Segmentdefinition angeben können.

## Erweiterte Segmentierungsfunktionen

Segmente können so konfiguriert werden, dass sie kontinuierlich eine Zielgruppe generieren, indem die [Streaming-Datenaufnahme](../ingestion/streaming-ingestion/overview.md) mit einer der folgenden erweiterten Segmentierungsfunktionen kombiniert wird:
- [Sequenzielle Segmentierung](#sequential)
- [Dynamische Segmentierung](#dynamic)
- [Segmentierung mit mehreren Entitäten](#multi-entity)

Diese erweiterten Funktionen werden in den folgenden Abschnitten ausführlicher erläutert.

## Sequenzielle Segmentierung {#sequential}

Eine standardmäßige Customer Journey ist sequenziell. Mit Adobe Experience Platform können Sie eine geordnete Segmentreihe definieren, die eine Journey widerspiegelt. Dabei werden Sequenzen von Ereignissen unmittelbar bei ihrem Auftreten erfasst. Über die Timeline für visuelle Ereignisse in [!DNL Segment Builder] können Sie Ereignisse in der gewünschten Reihenfolge anordnen.

Ein Beispiel für eine Customer Journey, für die eine sequenzielle Segmentierung erforderlich ist, wäre Produkt ansehen > Produkt hinzufügen > Kasse > Kein Kauf.

## Dynamische Segmentierung {#dynamic}

Mit der dynamischen Segmentierung können die Skalierbarkeitsprobleme gelöst werden, die Marketing-Experten beim Erstellen von Segmenten für Marketing-Kampagnen üblicherweise haben.

Im Gegensatz zur statischen Segmentierung, bei der Sie jeden möglichen Anwendungsfall explizit und wiederholt erfassen müssen, verwendet die dynamische Segmentierung Variablen, um die Regellogik zu erstellen und Beziehungen dynamisch auszudrücken.

### Anwendungsfall: Suche nach Kunden, die Käufe außerhalb ihres Bundesstaats tätigen

Bei dieser erweiterten Segmentierungsfunktion sollte ein Datenarchitekt mit einem Marketing-Experten zusammenarbeiten, um Kunden zu identifizieren, die außerhalb ihres Bundesstaats Einkäufe getätigt haben.

**Das Problem**

Für die statische Segmentierung müssen Sie einzelne Segmente mit einem eindeutigen Attribut für den heimatlichen Bundesstaat definieren, bevor Sie nach Kaufereignissen filtern, die nicht dem Bundesland-Status entsprechen. Ein explizites Segment dieses Typs würde lauten: „Ich suche nach Personen aus Utah, deren Kaufstatus nicht Utah ist“. Wenn Sie mit dieser Methode eine Zielgruppe erstellen möchten, müssen Sie für jeden US-Bundesstaat ein Segment, also insgesamt 50 Segmente, definieren.

Aufgrund der verschiedenen Segmentkombinationen, die sich unweigerlich bei der Skalierung ergeben, wird der manuelle Prozess, der für die statische Segmentierung erforderlich ist, zeitaufwendiger, was wiederum die Effizienz der Mitarbeiter verringert.

**Die Lösung**

Indem Sie dem Kaufstatusattribut eine Variable zuweisen, wird Ihr dynamisches Segment vereinfacht: „Finde einen Kauf, bei dem der Status dieses Kaufs nicht mit dem Bundesstaats-Status des Kunden übereinstimmt“. Auf diese Weise können Sie dann 50 statische Segmente zu einem einzigen dynamischen Segment zusammenfassen.

## Segmentierung mit mehreren Entitäten {#multi-entity}

Mit der erweiterten Segmentierungsfunktion für mehrere Entitäten können Sie die Daten von [!DNL Real-Time Customer Profile] mit zusätzlichen Daten erweitern, die auf Produkten, Geschäften oder anderen Nicht-Personen-Entitäten basieren und auch als „Dimensionsentitäten“ bezeichnet werden. Folglich kann [!DNL Segmentation Service] während der Segmentdefinition auf zusätzliche Felder zugreifen, als ob sie nativ im [!DNL Profile]-Datenspeicher enthalten wären. Die Segmentierung mehrerer Entitäten bietet Flexibilität bei der Identifizierung von Zielgruppen anhand von Daten, die für Ihre individuellen Geschäftsanforderungen relevant sind. Weitere Informationen, einschließlich Anwendungsfällen und Workflows, finden Sie im [Handbuch zur Segmentierung mehrerer Entitäten](multi-entity-segmentation.md).

## [!DNL Segmentation Service]-Datentypen

[!DNL Segmentation Service] unterstützt eine Vielzahl von einfachen und komplexen Datentypen. Detaillierte Informationen, einschließlich einer Liste der unterstützten Datentypen, finden Sie im [Handbuch zu unterstützten Datentypen](./data-types.md).

## Nächste Schritte

[!DNL Segmentation Service] bietet einen konsolidierten Workflow zum Erstellen von Segmenten aus [!DNL Real-Time Customer Profile]-Daten. Zusammenfassung:

- [!DNL Segmentation] ist der Prozess der Definition einer Untergruppe von Profilen aus Ihrem Profilspeicher, sodass Sie das Verhalten oder die Attribute Ihrer gewünschten marktfähigen Gruppe charakterisieren können. [!DNL Segmentation Service] ermöglicht diesen Prozess.
- Beachten Sie bei der Planung eines Segments, dass es von einem beliebigen anderen Segment referenziert und mit diesem kombiniert werden kann.
- Ein Segment kann mithilfe von Regeln basierend auf Profildaten, damit verbundenen Zeitreihendaten oder beidem erstellt werden.
- Segmente können entweder bei Bedarf oder kontinuierlich ausgewertet werden. Bei der On-demand-Auswertung werden alle Profildaten gleichzeitig entsprechend den Segmentdefinitionen evaluiert. Wenn Daten kontinuierlich ausgewertet werden, werden Sie unmittelbar mit den Segmentdefinitionen verglichen, wenn sie nach [!DNL Platform] übermittelt werden.

Informationen zum Definieren von Segmenten in der Benutzeroberfläche finden Sie im [Segment Builder-Handbuch](./ui/overview.md). Informationen zum Erstellen von Segmentdefinitionen mithilfe der API finden Sie im Tutorial zum [Erstellen von Segmenten mithilfe der API](./tutorials/create-a-segment.md).
