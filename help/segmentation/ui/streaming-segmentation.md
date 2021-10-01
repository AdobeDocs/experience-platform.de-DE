---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming-Segmentierung; Segmentierung; Segmentierungsdienst; Segmentierungsdienst; Benutzerhandbuch
solution: Experience Platform
title: Handbuch zur Streaming-Segmentierung der Benutzeroberfläche
topic-legacy: ui guide
description: Mit der Streaming-Segmentierung auf Adobe Experience Platform können Sie die Segmentierung nahezu in Echtzeit durchführen und sich dabei auf den Datenreichtum konzentrieren. Mit Streaming-Segmentierung erfolgt jetzt eine Segmentqualifizierung, wenn Daten in Platform landen. So wird die Notwendigkeit verringert, Segmentierungsaufträge zu planen und auszuführen. Mit dieser Funktion können die meisten Segmentregeln jetzt ausgewertet werden, wenn die Daten an Platform übergeben werden. Das bedeutet, dass die Segmentzugehörigkeit ohne Ausführung geplanter Segmentierungsaufträge auf dem neuesten Stand gehalten wird.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: b4a04b52ff9a2b7a36fda58d70a2286fea600ff1
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 1%

---

# Streaming-Segmentierung

>[!NOTE]
>
>Im folgenden Dokument wird die Verwendung der Streaming-Segmentierung mithilfe der Benutzeroberfläche beschrieben. Informationen zur Verwendung von Streaming-Segmentierung mithilfe der API finden Sie im [Streaming-Segmentation-API-Handbuch](../api/streaming-segmentation.md).

Die Streaming-Segmentierung für [!DNL Adobe Experience Platform] ermöglicht es Kunden, die Segmentierung nahezu in Echtzeit durchzuführen, während sie sich auf den Datenreichtum konzentrieren. Mit Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Streaming-Daten in [!DNL Platform] landen. So wird die Notwendigkeit zur Planung und Ausführung von Segmentierungsaufträgen verringert. Mit dieser Funktion können die meisten Segmentregeln jetzt ausgewertet werden, wenn die Daten an [!DNL Platform] übergeben werden. Das bedeutet, dass die Segmentzugehörigkeit ohne Ausführung geplanter Segmentierungsaufträge auf dem neuesten Stand gehalten wird.

>[!NOTE]
>
>Streaming-Segmentierung kann nur zur Auswertung von Daten verwendet werden, die in Platform gestreamt werden. Anders ausgedrückt: Daten, die über die Batch-Erfassung erfasst werden, werden nicht durch Streaming-Segmentierung ausgewertet und zusammen mit dem nächtlich geplanten Segmentauftrag ausgewertet.
>
>Darüber hinaus können Segmente, die mit Streaming-Segmentierung ausgewertet werden, zwischen idealer und tatsächlicher Mitgliedschaft wechseln, wenn das Segment auf einem anderen Segment basiert, das mithilfe der Batch-Segmentierung ausgewertet wird. Wenn beispielsweise Segment A auf Segment B basiert und Segment B mithilfe der Batch-Segmentierung ausgewertet wird, da Segment B nur alle 24 Stunden aktualisiert wird, entfernt sich Segment A weiter von den tatsächlichen Daten, bis es mit der Aktualisierung Segment B erneut synchronisiert wird.

## Streaming-Segmentierungsabfragetypen

>[!NOTE]
>
>Damit Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für die Organisation aktivieren. Weitere Informationen zur Aktivierung der geplanten Segmentierung finden Sie im Abschnitt [Streaming-Segmentierung im Benutzerhandbuch zur Segmentierung](./overview.md#scheduled-segmentation).

Eine Abfrage wird automatisch mit Streaming-Segmentierung ausgewertet, wenn sie eines der folgenden Kriterien erfüllt:

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Eingehender Treffer | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Eingehender Treffer innerhalb eines relativen Zeitfensters | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis verweist. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Eingehender Treffer mit einem Zeitfenster | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem Zeitfenster verweist. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Nur Profil | Jede Segmentdefinition, die nur auf ein Profilattribut verweist. |  |
| Eingehender Treffer, der sich auf ein Profil bezieht | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profilattribute verweist. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Eingehender Treffer, der sich auf ein Profil innerhalb eines relativen Zeitfensters bezieht | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis und ein oder mehrere Profilattribute verweist. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segment von Segmenten | Jede Segmentdefinition, die einen oder mehrere Batch- oder Streaming-Segmente enthält. **Hinweis:** Wenn ein Segment von Segmenten verwendet wird, erfolgt die Profildisqualifizierung  **alle 24 Stunden**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Mehrere Ereignisse, die auf ein Profil verweisen | Jede Segmentdefinition, die auf mehrere Ereignisse **innerhalb der letzten 24 Stunden** verweist und (optional) über ein oder mehrere Profilattribute verfügt. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Eine Segmentdefinition wird **not** für Streaming-Segmentierung in den folgenden Szenarien aktiviert:

- Die Segmentdefinition umfasst Adobe Audience Manager-Segmente oder -Eigenschaften (AAM).
- Die Segmentdefinition umfasst mehrere Entitäten (Abfragen mit mehreren Entitäten).

Darüber hinaus gelten einige Richtlinien für die Streaming-Segmentierung:

| Abfragetyp | Richtlinie |
| ---------- | -------- |
| Einzelereignisabfrage | Das Lookback-Fenster ist nicht beschränkt. |
| Abfrage mit Ereignisverlauf | <ul><li>Das Lookback-Fenster ist auf **einen Tag** beschränkt.</li><li>Zwischen den Ereignissen ist eine strikte Bedingung für die zeitliche Reihenfolge **must** vorhanden.</li><li>Abfragen mit mindestens einem negativen Ereignis werden unterstützt. Das gesamte Ereignis **kann jedoch nicht** eine Negation sein.</li></ul> |

Wenn eine Segmentdefinition geändert wird, sodass sie die Kriterien für Streaming-Segmentierung nicht mehr erfüllt, wird die Segmentdefinition automatisch von &quot;Streaming&quot;zu &quot;Batch&quot;geändert.

## Streaming-Segmentdetails

Nachdem Sie ein Streaming-fähiges Segment erstellt haben, können Sie Details zu diesem Segment anzeigen.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Insbesondere werden Details zur **[!UICONTROL gesamten qualifizierten Zielgruppengröße]** angezeigt. Die **[!UICONTROL Gesamtzahl der qualifizierten Zielgruppengröße]** zeigt die Gesamtzahl der qualifizierten Zielgruppen aus der letzten abgeschlossenen Segmentauftragsausführung an. Wenn ein Segmentauftrag nicht innerhalb der letzten 24 Stunden abgeschlossen wurde, wird die Anzahl der Zielgruppen stattdessen aus einer Schätzung abgeleitet.

Darunter ist ein Kantengraph, der die Anzahl der Segmente anzeigt, die in den letzten 24 Stunden qualifiziert und disqualifiziert wurden. Das Dropdown-Menü kann angepasst werden, um die letzten 24 Stunden, letzte Woche oder letzten 30 Tage anzuzeigen.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Weitere Informationen zur letzten Segmentbewertung finden Sie durch Auswahl der Informationsblase.

![](../images/ui/streaming-segmentation/info-bubble.png)

Weitere Informationen zu Segmentdefinitionen finden Sie im vorherigen Abschnitt unter [Segmentdefinitionsdetails](#segment-details).

## Nächste Schritte

In diesem Benutzerhandbuch wird erläutert, wie Streaming-fähige Segmentdefinitionen in Adobe Experience Platform funktionieren und wie Streaming-fähige Segmente überwacht werden.

Weitere Informationen zur Verwendung der Adobe Experience Platform-Benutzeroberfläche finden Sie im [Benutzerhandbuch zur Segmentierung](./overview.md).
