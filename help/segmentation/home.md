---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentdienst; Segment; Segment; Segmente; Segmente
solution: Experience Platform
title: Übersicht über den Segmentierungsdienst
topic-legacy: overview
description: Erfahren Sie mehr über den Segmentierungsdienst von Adobe Experience Platform und die Rolle, die dieser im Platform-Ökosystem spielt.
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 3130d9731a53c01fb7bc15265e044191ceae47f6
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 8%

---

# [!DNL Segmentation Service] – Übersicht

Adobe Experience Platform [!DNL Segmentation Service] bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Zielgruppen aus Ihren [!DNL Real-time Customer Profile] Daten. Diese Segmente werden zentral konfiguriert und verwaltet in [!DNL Platform]und für jede Adobe leicht zugänglich sind.

Dieses Dokument bietet einen Überblick über [!DNL Segmentation Service] und die Rolle, die sie in Adobe Experience Platform spielt.

## Erste Schritte mit [!DNL Segmentation Service]

Es ist wichtig, die folgenden Schlüsselbegriffe zu verstehen, die in diesem Dokument verwendet werden:

- **Segmentierung**: Die Unterteilung einer großen Gruppe von Einzelanwendern (z. B. Kunden, Interessenten, Benutzer oder Organisationen) in kleinere Gruppen, die ähnliche Eigenschaften aufweisen und ähnlich auf Marketing-Strategien reagieren.
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe verwendet wird. Nach der Konzeption werden die in einer Segmentdefinition beschriebenen Regeln verwendet, um qualifizierte Zielgruppenmitglieder für ein Segment zu bestimmen.
- **Audience**: Der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

## Funktionsweise der Segmentierung

Bei Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die von einer Untergruppe von Profilen in Ihrem Profilspeicher geteilt werden, sodass Sie eine vermarktbare Gruppe von Personen aus Ihrem Kundenstamm ermitteln können. In einer E-Mail-Kampagne mit dem Namen „Haben Sie vergessen, Schuhe zu kaufen?“ wollen Sie möglicherweise eine Zielgruppe aller Anwender auswählen, die in den letzten 30 Tagen nach Laufschuhen gesucht haben, den Kauf jedoch nicht abgeschlossen haben.

Sobald ein Segment konzeptionell definiert wurde, wird es in [!DNL Experience Platform]. In der Regel werden Segmente vom Marketing- oder Zielgruppenspezialisten erstellt, obwohl einige Unternehmen es vorziehen, dass sie in Zusammenarbeit mit ihren Datenanalysten von ihrer Marketing-Abteilung erstellt werden. Nach Überprüfung der gesendeten Daten an [!DNL Platform], erstellt der Datenanalyst die Segmentdefinition, indem er auswählt, welche Felder und Werte zum Erstellen der Regeln oder Bedingungen des Segments verwendet werden. Dies erfolgt über die Benutzeroberfläche oder die API.

## Segmente erstellen

Ob mit der API oder mit der [!DNL Segment Builder], werden Segmente letztendlich mithilfe von [!DNL Profile Query Language] (PQL). Hier wird die Definition des konzeptionellen Segments in der Sprache beschrieben, die zum Abrufen von Profilen erstellt wurde, die den Kriterien entsprechen. Weitere Informationen finden Sie unter [PQL-Übersicht](./pql/overview.md).

Informationen zum Erstellen und Verwenden von Segmenten finden Sie im Abschnitt [!DNL Segment Builder] (Implementierung der Benutzeroberfläche von [!DNL Segmentation Service]), siehe [Segment Builder-Handbuch](./ui/overview.md).

Informationen zum Erstellen von Segmentdefinitionen mithilfe der API finden Sie im Tutorial zu [Erstellen von Zielgruppensegmenten mithilfe der API](./tutorials/create-a-segment.md).

>[!NOTE]
>
>Bei einer Erweiterung eines Schemas müssen alle zukünftigen Uploads neu hinzugefügte Felder entsprechend aktualisiert werden. Weitere Informationen zum Anpassen [!DNL Experience Data Model] (XDM), besuchen Sie die [Tutorial zum Schema Editor](../xdm/tutorials/create-schema-ui.md).
>
>Wenn die Time-to-Live (TTL) für den Datensatz aktiviert ist, könnte sich dies auf die Mitgliedschaft des erstellten Segments auswirken. Weiterführende Informationen zu TTL und deren Auswirkungen auf die Segmentierung finden Sie im Abschnitt [TTL-Handbuch für den Profildienst](../profile/apply-ttl.md).

## Segmente bewerten

Platform unterstützt derzeit drei Methoden zum Auswerten von Segmenten: Streaming-Segmentierung, Batch-Segmentierung und Kantensegmentierung.

### Streaming-Segmentierung

Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Ihre Segmente als Reaktion auf Benutzeraktivitäten aktualisiert. Nachdem ein Segment erstellt und gespeichert wurde, wird die Segmentdefinition auf eingehende Daten angewendet auf [!DNL Real-time Customer Profile]. Segmentzufügungen und -entfernungen werden regelmäßig verarbeitet, um sicherzustellen, dass Ihre Zielgruppe relevant bleibt.

Weitere Informationen zur Streaming-Segmentierung finden Sie in der [Dokumentation zur Streaming-Segmentierung](./api/streaming-segmentation.md).

### Batch-Segmentierung

Als Alternative zu einem laufenden Datenauswahlprozess verschiebt die Batch-Segmentierung alle Profildaten gleichzeitig durch Segmentdefinitionen, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung wird dieses Segment gespeichert, sodass Sie es zur Verwendung exportieren können.

Batch-Segmente werden automatisch alle 24 Stunden ausgewertet. Wenn Sie ein Batch-Segment bei Bedarf auswerten möchten, können Sie einen Segmentauftrag verwenden. Weitere Informationen zu Segmentaufträgen finden Sie im Abschnitt [Dokumentation zu Segmentaufträgen](./api/segment-jobs.md).

### Edge-Segmentierung

Bei der Edge-Segmentierung können Segmente in Platform sofort in Experience Edge ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

Weitere Informationen zur Kantensegmentierung finden Sie in der [API-Dokumentation](./api/edge-segmentation.md) oder [Benutzeroberflächendokumentation](./ui/edge-segmentation.md).

## Zugriff auf Segmentierungsergebnisse

Informationen zum Zugriff auf ein exportiertes Segment finden Sie unter [Tutorial zur Segmentbewertung](./tutorials/evaluate-a-segment.md).

## Segmentmetadaten

Segmentmetadaten erleichtern die Indizierung für den Fall, dass eines Ihrer Segmente wiederverwendet und/oder kombiniert werden soll.

Erstellen Ihrer Segmente (entweder über die API oder [!DNL Segment Builder]) erfordert, dass Sie einen Segmentnamen und eine Zusammenführungsrichtlinie definieren.

### Segmentnamen

Beim Erstellen eines neuen Segments müssen Sie einen Segmentnamen angeben. Der Segmentname wird verwendet, um ein bestimmtes Segment aus der von [!DNL Segmentation Service]. Segmentnamen sollten daher beschreibend, kurz und eindeutig sein.

>[!NOTE]
>
>Beachten Sie bei der Planung eines Segments, dass Segmente aus einem beliebigen anderen Segment referenziert und mit ihm kombiniert werden können. Erwägen Sie bei der Auswahl eines Namens die Möglichkeit, dass Ihr Segment wiederverwendbare Teile enthalten kann.

### Zusammenführungsrichtlinien

Zusammenführungsrichtlinien sind Regeln, die von [!DNL Profile] um zu bestimmen, wie Daten priorisiert und unter bestimmten Bedingungen zu einer einheitlichen Ansicht kombiniert werden.
Wenn keine Zusammenführungsrichtlinie definiert ist, wird die Standardeinstellung [!DNL Platform] Die Zusammenführungsrichtlinie wird verwendet. Wenn Sie lieber eine für Ihre Organisation spezifische Zusammenführungsrichtlinie verwenden möchten, können Sie eine eigene erstellen und diese als Standard für Ihre Organisation markieren.

Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im [Leitfaden zu Zusammenführungsrichtlinien](../profile/api/merge-policies.md).

>[!NOTE]
>
>Die Schätzung der Zielgruppengrößen basiert auf der standardmäßigen Profilzusammenführungsrichtlinie des Unternehmens.

### Andere Segmentmetadaten

Zusätzlich zu den Segmentnamen- und Zusammenführungsrichtlinien gilt Folgendes: [!DNL Segment Builder] bietet Ihnen ein zusätzliches Metadatenfeld &quot;Segmentbeschreibung&quot;, in dem Sie den Zweck Ihrer Segmentdefinition zusammenfassen können.

## Erweiterte Segmentierungsfunktionen

Segmente können so konfiguriert werden, dass sie kontinuierlich eine Zielgruppe generieren, indem sie [Streaming-Datenerfassung](../ingestion/streaming-ingestion/overview.md) mit einer der folgenden erweiterten Segmentierungsfunktionen:
- [Sequenzielle Segmentierung](#sequential)
- [Dynamische Segmentierung](#dynamic)
- [Segmentierung mit mehreren Entitäten](#multi-entity)

Diese erweiterten Funktionen werden in den folgenden Abschnitten ausführlicher erläutert.

## Sequenzielle Segmentierung {#sequential}

Eine Standardbenutzer-Journey ist sequenziell. Mit Adobe Experience Platform können Sie eine geordnete Segmentreihe definieren, um diese Journey widerzuspiegeln und somit Ereignissequenzen zu erfassen. Sie können Ereignisse in der gewünschten Reihenfolge anordnen, indem Sie die Timeline für visuelle Ereignisse in der [!DNL Segment Builder].

Ein Beispiel für eine Journey eines Kunden, für das eine sequenzielle Segmentierung erforderlich wäre, wäre Produktansicht > Produktangebot > Checkout > Kein Kauf.

## Dynamische Segmentierung {#dynamic}

Die dynamische Segmentierung löst die Skalierbarkeitsprobleme, die Marketingexperten beim Erstellen von Segmenten für Marketing-Kampagnen traditionell haben.

Im Gegensatz zur statischen Segmentierung, bei der Sie jeden möglichen Anwendungsfall explizit und wiederholt erfassen müssen, verwendet die dynamische Segmentierung Variablen, um die Regellogik zu erstellen und Beziehungen dynamisch auszudrücken.

### Anwendungsfall: Suchen nach Kunden, die Käufe außerhalb ihres Heimatlandes tätigen

Um den Wert dieser erweiterten Segmentierungsfunktion zu veranschaulichen, sollten Sie einen Datenarchitekten erwägen, der mit einem Marketing-Experten zusammenarbeitet, um Kunden zu identifizieren, die außerhalb ihres Heimatstaates Einkäufe getätigt haben.

**Das Problem**

Für die statische Segmentierung müssen Sie einzelne Segmente mit einem eindeutigen Stammstatusattribut definieren, bevor Sie nach Kaufereignissen filtern, die nicht dem Startstatus entsprechen. Ein explizites Segment dieses Typs würde lauten: &quot;Ich suche nach Personen aus Utah, deren Kaufstatus nicht Utah ist&quot;. Wenn Sie mit dieser Methode eine Zielgruppe erstellen, müssen Sie für jeden US-Bundesstaat ein Segment für insgesamt 50 Segmente definieren.

Aufgrund der verschiedenen Segmentkombinationen, die sich unweigerlich bei der Skalierung ergeben, wird der manuelle Prozess, der für die statische Segmentierung erforderlich ist, zeitaufwendiger, wodurch sich Ihre Gesamteffizienz verringert.

**Die Lösung**

Indem Sie dem Kaufstatusattribut eine Variable zuweisen, vereinfacht sich Ihr dynamisches Segment, &quot;einen Kauf zu finden, bei dem der Status dieses Kaufs nicht mit dem Herkunftsstatus des Kunden übereinstimmt&quot;. Auf diese Weise können Sie dann 50 statische Segmente zu einem einzigen dynamischen Segment zusammenfassen.

## Segmentierung mit mehreren Entitäten {#multi-entity}

Mit der erweiterten Segmentierungsfunktion für mehrere Entitäten können Sie [!DNL Real-time Customer Profile] Daten mit zusätzlichen Daten, die auf Produkten, Geschäften oder anderen Nicht-Personen-Entitäten basieren, die auch als &quot;Dimensionsentitäten&quot;bezeichnet werden. Daher [!DNL Segmentation Service] kann während der Segmentdefinition auf zusätzliche Felder zugreifen, als ob sie nativ für [!DNL Profile] Datenspeicher. Die Segmentierung mehrerer Entitäten bietet Flexibilität bei der Identifizierung von Zielgruppen anhand von Daten, die für Ihre individuellen Geschäftsanforderungen relevant sind. Weitere Informationen, einschließlich Anwendungsfällen und Workflows, finden Sie im Abschnitt [Handbuch zur Segmentierung mehrerer Entitäten](multi-entity-segmentation.md).

## [!DNL Segmentation Service] Datentypen

[!DNL Segmentation Service] unterstützt eine Vielzahl von primitiven und komplexen Datentypen. Detaillierte Informationen, einschließlich einer Liste der unterstützten Datentypen, finden Sie im Abschnitt [Handbuch zu unterstützten Datentypen](./data-types.md).

## Nächste Schritte

[!DNL Segmentation Service] bietet einen konsolidierten Workflow zum Erstellen von Segmenten aus [!DNL Real-time Customer Profile] Daten. Zusammenfassung:

- [!DNL Segmentation] ist der Prozess der Definition einer Teilmenge von Profilen aus Ihrem Profilspeicher, sodass Sie das Verhalten oder die Attribute einer gewünschten marktfähigen Gruppe charakterisieren können. [!DNL Segmentation Service] ermöglicht diesen Prozess.
- Beachten Sie bei der Planung eines Segments, dass ein Segment aus einem beliebigen anderen Segment referenziert und mit diesem kombiniert werden kann.
- Ein Segment kann aus Regeln basierend auf Profildaten, verwandten Zeitreihendaten oder beidem erstellt werden.
- Segmente können entweder bei Bedarf oder kontinuierlich ausgewertet werden. Bei der bedarfsgerechten Auswertung werden alle Profildaten gleichzeitig durch die Segmentdefinitionen weitergeleitet. Wenn Daten kontinuierlich ausgewertet werden, werden sie durch die Segmentdefinitionen nach [!DNL Platform].

Informationen zum Definieren von Segmenten in der Benutzeroberfläche finden Sie unter [Segment Builder-Handbuch](./ui/overview.md). Informationen zum Erstellen von Segmentdefinitionen mithilfe der API finden Sie im Tutorial zu [Erstellen von Segmenten mithilfe der API](./tutorials/create-a-segment.md).
