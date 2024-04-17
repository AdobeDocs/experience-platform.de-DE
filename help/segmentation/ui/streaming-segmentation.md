---
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche für die Streaming-Segmentierung
description: Mit der Streaming-Segmentierung in Adobe Experience Platform können Sie die Segmentierung nahezu in Echtzeit durchführen und sich dabei auf die Relevanz der Daten konzentrieren. Im Rahmen der Streaming-Segmentierung erfolgt jetzt eine Segmentqualifizierung, wenn Daten in Platform aufgenommen werden. So wird die Notwendigkeit verringert, Segmentierungsaufträge zu planen und auszuführen. Mit dieser Funktion können die meisten Segmentregeln jetzt ausgewertet werden, während Daten an Platform übermittelt werden. Das bedeutet, dass die Segmentzugehörigkeit auch ohne Ausführung geplanter Segmentierungsaufträge auf dem neuesten Stand gehalten wird.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: c14c6b8037993b3696b4a99633c80c6ee9679399
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 91%

---

# Streaming-Segmentierung 

>[!NOTE]
>
>Im folgenden Dokument wird die Verwendung der Streaming-Segmentierung mithilfe der Benutzeroberfläche beschrieben. Informationen zur Verwendung der Streaming-Segmentierung mithilfe der API finden Sie im [Handbuch zur API für die Streaming-Segmentierung](../api/streaming-segmentation.md).

Mit der Streaming-Segmentierung in [!DNL Adobe Experience Platform] können Kundinnen und Kunden die Segmentierung nahezu in Echtzeit durchführen und sich dabei auf die Relevanz der Daten konzentrieren. Im Rahmen der Streaming-Segmentierung erfolgt jetzt eine Segmentqualifizierung, wenn Streaming-Daten in [!DNL Platform] aufgenommen werden. So wird die Notwendigkeit verringert, Segmentierungsvorgänge zu planen und auszuführen. Mit dieser Funktion können die meisten Segmentregeln jetzt ausgewertet werden, während Daten an [!DNL Platform] übermittelt werden. Das bedeutet, dass die Segmentzugehörigkeit auch ohne Ausführung geplanter Segmentierungsvorgänge auf dem neuesten Stand gehalten wird.

>[!NOTE]
>
>Die Streaming-Segmentierung funktioniert bei allen Daten, die über eine Streaming-Quelle aufgenommen wurden. Daten, die über eine Batch-basierte Quelle aufgenommen werden, werden jede Nacht ausgewertet, selbst wenn sie zur Streaming-Segmentierung geeignet sind.
>
>Darüber hinaus können Segmente, die mithilfe der Streaming-Segmentierung ausgewertet werden, zwischen idealer und tatsächlicher Zugehörigkeit wechseln, wenn die Segmentdefinition auf einer anderen Segmentdefinition basiert, die durch eine Batch-Segmentierung ausgewertet wird. Wenn beispielsweise Segment A auf Segment B basiert und Segment B mithilfe der Batch-Segmentierung ausgewertet wird, entfernt sich Segment A weiter von den tatsächlichen Daten, bis es mit der Aktualisierung von Segment B erneut synchronisiert wird, da Segment B nur alle 24 Stunden aktualisiert wird.

## Abfragetypen für die Streaming-Segmentierung {#query-types}

>[!NOTE]
>
>Damit die Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für die Organisation aktivieren. Weiterführende Informationen zur Aktivierung der geplanten Segmentierung finden Sie im [Abschnitt zur Streaming-Segmentierung im Segmentierungs-Benutzerhandbuch](./overview.md#scheduled-segmentation).

Eine Abfrage wird automatisch mithilfe der Streaming-Segmentierung ausgewertet, wenn sie eines der folgenden Kriterien erfüllt:

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Einzelnes Ereignis | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | ![Ein Beispiel für ein einzelnes Ereignis wird angezeigt.](../images/ui/streaming-segmentation/incoming-hit.png) |
| Einzelnes Ereignis innerhalb eines relativen Zeitfensters | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis verweist. | ![Ein Beispiel für ein einzelnes Ereignis innerhalb eines relativen Zeitfensters wird angezeigt.](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Einzelnes Ereignis mit einem Zeitfenster | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem Zeitfenster verweist. | ![Ein Beispiel für ein einzelnes Ereignis mit einem Zeitfenster wird angezeigt.](../images/ui/streaming-segmentation/historic-time-window.png) |
| Nur Profil | Jede Segmentdefinition, die nur auf ein Profilattribut verweist. | |
| Einzelnes Ereignis mit einem Profilattribut innerhalb eines relativen Zeitfensters von weniger als 24 Stunden | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem oder mehreren Profilattributen verweist und innerhalb eines relativen Zeitfensters von weniger als 24 Stunden erfolgt. | ![Ein Beispiel für ein einzelnes Ereignis mit einem Profilattribut in einem relativen Zeitfenster wird angezeigt.](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segment von Segmenten | Jede Segmentdefinition, die ein oder mehrere Batch- oder Streaming-Segmente enthält. **Hinweis**: Wenn ein Segment von Segmenten verwendet wird, erfolgt **alle 24 Stunden** eine Profildisqualifizierung. | ![Ein Beispiel für ein Segment von Segmenten wird angezeigt.](../images/ui/streaming-segmentation/two-batches.png) |
| Mehrere Ereignisse mit einem Profilattribut | Jede Segmentdefinition, die **innerhalb der letzten 24 Stunden** auf mehrere Ereignisse verweist und (optional) ein oder mehrere Profilattribute hat. | ![Ein Beispiel für mehrere Ereignisse mit einem Profilattribut wird angezeigt.](../images/ui/streaming-segmentation/event-history-success.png) |

Eine Segmentdefinition wird für die Streaming-Segmentierung in den folgenden Szenarien **nicht** aktiviert:

- Die Segmentdefinition umfasst Segmente oder Merkmale aus Adobe Audience Manager (AAM).
- Die Segmentdefinition umfasst mehrere Entitäten (Abfragen mit mehreren Entitäten).
- Die Segmentdefinition umfasst eine Kombination aus einem einzelnen Ereignis und einem `inSegment`-Ereignis.
   - Wenn die im `inSegment`-Ereignis enthaltene Segmentdefinition jedoch nur ein Profil ist, wird die Segmentdefinition für die Streaming-Segmentierung **aktiviert**.
- Die Segmentdefinition verwendet &quot;Jahr ignorieren&quot;als Teil ihrer Zeitbeschränkungen.

Bitte beachten Sie bei der Streaming-Segmentierung die folgenden Richtlinien:

| Abfragetyp | Richtlinie |
| ---------- | -------- |
| Einzelereignisabfrage | Das Lookback-Fenster ist nicht beschränkt. |
| Abfrage mit Ereignisverlauf | <ul><li>Das Lookback-Fenster ist auf **einen Tag** beschränkt.</li><li>Es **muss** eine strikte Bedingung für die zeitliche Reihenfolge zwischen den Ereignissen vorhanden sein.</li><li>Abfragen mit mindestens einem negierten Ereignis werden unterstützt. Das gesamte Ereignis kann jedoch **keine** Negation sein.</li></ul> |

Wenn eine Segmentdefinition geändert wird, sodass sie die Kriterien für die Streaming-Segmentierung nicht mehr erfüllt, wird die Segmentdefinition automatisch von „Streaming“ zu „Batch“ geändert.

Darüber hinaus erfolgt die Aufhebung der Segmentqualifikation, ähnlich wie die Segmentqualifikation selbst, in Echtzeit. Wenn sich eine Zielgruppe nicht mehr für ein Segment qualifiziert, wird deren Qualifikation daher sofort aufgehoben. Wenn in der Segmentdefinition beispielsweise nach „Alle Benutzenden, die in den letzten drei Stunden rote Schuhe gekauft haben“ gefragt wird, wird die Qualifikation nach drei Stunden für alle Profile, die sich ursprünglich für die Segmentdefinition qualifiziert haben, aufgehoben.

## Details der Segmentdefinition für die Streaming-Segmentierung

Nachdem Sie ein für Streaming aktiviertes Segment erstellt haben, können Sie Details zu diesem Segment anzeigen.

![Die Seite mit den Details zur Segmentdefinition wird angezeigt.](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Insbesondere wird die Metrik **[!UICONTROL Gesamtzahl an Qualifizierten]** angezeigt, die die Gesamtzahl qualifizierter Zielgruppen basierend auf Batch- und Streaming-Auswertungen für dieses Segment umfasst.

Darunter befindet sich ein Liniendiagramm, das die Anzahl der neuen Zielgruppen anzeigt, die in den letzten 24 Stunden mit der Streaming-Auswertungsmethode aktualisiert wurden. Die Dropdown-Liste kann angepasst werden, um die letzten 24 Stunden, die letzte Woche oder die letzten 30 Tage anzuzeigen. Die Metrik **[!UICONTROL Aktualisierte neue Zielgruppe]** basiert auf der Änderung der Größe der Zielgruppe während des ausgewählten Zeitraums, gemäß der Auswertung durch die Streaming-Segmentierung. Diese Metrik umfasst nicht die gesamte qualifizierte Zielgruppe aus der täglichen Batch-Segmentauswertung.

>[!NOTE]
>
>Eine Segmentdefinition gilt als qualifiziert, wenn es von der Statuslosigkeit oder vom Status „beendet“ zum Status „realisiert“ wechselt. Eine Segmentdefinition gilt als nicht qualifiziert, wenn es von realisiert zu beendet wechselt.
>
>Weitere Informationen zu diesen Status finden Sie in der Statustabelle in der [Segmentierungsübersicht](./overview.md#browse).

![Die Karte für Profile im Zeitverlauf wird hervorgehoben und zeigt ein Liniendiagramm der Profile im Zeitverlauf an.](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Weitere Informationen zur letzten Segmentauswertung erhalten Sie, indem Sie die Informationsblase neben **[!UICONTROL Gesamtzahl der Qualifizierten]** anklicken.

![Die Informationsblase für die insgesamt qualifizierten Profile wurde ausgewählt. Dadurch werden Informationen zur letzten Segmentauswertungszeit angezeigt.](../images/ui/streaming-segmentation/info-bubble.png)

Weitere Informationen zu Segmentdefinitionen finden Sie im vorherigen Abschnitt unter [Details zur Segmentdefinition](#segment-details).

## Nächste Schritte

In diesem Benutzerhandbuch wird erläutert, wie für Streaming aktivierte Segmentdefinitionen in Adobe Experience Platform funktionieren und diese überwacht werden können.

Weitere Informationen zur Verwendung der Benutzeroberfläche von Adobe Experience Platform finden Sie im [Benutzerhandbuch zur Segmentierung](./overview.md).

## Anhang

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zur Streaming-Segmentierung:

### Tritt die „Nicht-Qualifizierung“ der Streaming-Segmentierung auch in Echtzeit auf?

In den meisten Fällen geschieht die Aufhebung der Qualifizierung von Streaming-Segmentierungen in Echtzeit. Für Streaming-Segmente, die Segmente von Segmenten verwenden, wird die Qualifizierung jedoch **nicht** in Echtzeit aufgehoben, sondern erst nach 24 Stunden.

### Mit welchen Daten arbeitet die Streaming-Segmentierung?

Die Streaming-Segmentierung funktioniert bei allen Daten, die über eine Streaming-Quelle aufgenommen wurden. Segmente, die mit einer Batch-basierten Quelle erfasst werden, werden jede Nacht ausgewertet, selbst wenn sie für die Streaming-Segmentierung geeignet sind. In das System gestreamte Ereignisse mit einem Zeitstempel, der älter als 24 Stunden ist, werden im nachfolgenden Batch-Vorgang verarbeitet.

### Wie werden Segmente als Batch- oder Streaming-Segmentierung definiert?

Eine Segmentdefinition wird – basierend auf einer Kombination aus Abfragetyp und Ereignisverlaufsdauer – als Batch-, Streaming- oder Edge-Segmentierung definiert. Eine Liste der Segmente, die als Streaming-Segmentdefinitionen ausgewertet werden, finden Sie im [Abschnitt zu Abfragetypen von Streaming-Segmentierungen](#query-types).

Bitte beachten Sie, dass eine Segmentdefinition, die **sowohl** einen `inSegment`-Ausdruck als auch eine direkte Einzelereigniskette enthält, nicht für die Streaming-Segmentierung infrage kommt. Wenn Sie möchten, dass diese Segmentdefinition für die Streaming-Segmentierung qualifiziert wird, sollten Sie die direkte Einzelereigniskette zu einem eigenen Segment machen.

### Warum steigt die Anzahl der „insgesamt qualifizierten“ Segmente weiter an, während die Anzahl unter „Letzte X Tage“ im Abschnitt Segmentdefinitionsdetails bei null bleibt?

Die Anzahl der insgesamt qualifizierten Segmente wird aus dem täglichen Segmentierungsauftrag abgerufen, der Zielgruppen enthält, die sich sowohl für Batch- als auch für Streaming-Segmente qualifizieren. Dieser Wert wird sowohl für Batch- als auch für Streaming-Segmente angezeigt.

Die Zahl unter „Letzte X Tage“ umfasst **nur** Zielgruppen, die für Streaming-Segmentierung qualifiziert sind. Sie erhöht sich **nur** dann, wenn Sie Daten in das System gestreamt haben, und zählt dann für diese Streaming-Definition. Dieser Wert wird **nur** für Streaming-Segmente angezeigt. Daher **kann** dieser Wert für Batch-Segmente als 0 angezeigt werden.

Wenn Sie also feststellen, dass die Zahl unter „Letzte X Tage“ null ist und das Liniendiagramm ebenfalls null zeigt, haben Sie **nicht** alle Profile in das System gestreamt, die für dieses Segment qualifiziert wären.

### Wie lange dauert es, bis eine Segmentdefinition verfügbar ist?

Es dauert bis zu einer Stunde, bis eine Segmentdefinition verfügbar ist.

### Gibt es Einschränkungen beim Streamen von Daten?

Damit Streaming-Daten in der Streaming-Segmentierung verwendet werden können, gibt es **must** Zwischen den eingestreamten Ereignissen muss ein Abstand bestehen. Wenn zu viele Ereignisse innerhalb derselben Sekunde gestreamt werden, behandelt Platform diese Ereignisse als Bot-generierte Daten und sie werden verworfen. Als Best Practice sollten Sie **mindestens** fünf Sekunden zwischen Ereignisdaten, um sicherzustellen, dass die Daten ordnungsgemäß verwendet werden.
