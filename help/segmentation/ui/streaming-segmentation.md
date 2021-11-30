---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming-Segmentierung; Segmentierung; Segmentierungsdienst; Segmentierungsdienst; Benutzerhandbuch
solution: Experience Platform
title: Handbuch zur Streaming-Segmentierung der Benutzeroberfläche
topic-legacy: ui guide
description: Mit der Streaming-Segmentierung auf Adobe Experience Platform können Sie die Segmentierung nahezu in Echtzeit durchführen und sich dabei auf den Datenreichtum konzentrieren. Mit Streaming-Segmentierung erfolgt jetzt eine Segmentqualifizierung, wenn Daten in Platform landen. So wird die Notwendigkeit verringert, Segmentierungsaufträge zu planen und auszuführen. Mit dieser Funktion können die meisten Segmentregeln jetzt ausgewertet werden, wenn die Daten an Platform übergeben werden. Das bedeutet, dass die Segmentzugehörigkeit ohne Ausführung geplanter Segmentierungsaufträge auf dem neuesten Stand gehalten wird.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 6db0aef66abe11b8ed9f4b8da56875aa296b1a10
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 0%

---

# Streaming-Segmentierung

>[!NOTE]
>
>Im folgenden Dokument wird die Verwendung der Streaming-Segmentierung mithilfe der Benutzeroberfläche beschrieben. Informationen zur Verwendung der Streaming-Segmentierung mithilfe der API finden Sie im Abschnitt [Handbuch zur Streaming-Segmentierungs-API](../api/streaming-segmentation.md).

Streaming-Segmentierung in [!DNL Adobe Experience Platform] ermöglicht es Kunden, die Segmentierung nahezu in Echtzeit durchzuführen und sich dabei auf den Datenreichtum zu konzentrieren. Mit Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Streaming-Daten in [!DNL Platform], wodurch Segmentierungsaufträge einfacher geplant und ausgeführt werden müssen. Mit dieser Funktion können die meisten Segmentregeln jetzt ausgewertet werden, wenn die Daten an [!DNL Platform]bedeutet, dass die Segmentzugehörigkeit auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden.

>[!NOTE]
>
>
>Mit Streaming-Segmentierung ausgewertete Segmente können zwischen idealer und tatsächlicher Mitgliedschaft wechseln, wenn das Segment auf einem anderen Segment basiert, das mithilfe der Batch-Segmentierung ausgewertet wird. Wenn beispielsweise Segment A auf Segment B basiert und Segment B mithilfe der Batch-Segmentierung ausgewertet wird, da Segment B nur alle 24 Stunden aktualisiert wird, entfernt sich Segment A weiter von den tatsächlichen Daten, bis es mit der Aktualisierung Segment B erneut synchronisiert wird.

## Streaming-Segmentierungsabfragetypen {#query-types}

>[!NOTE]
>
>Damit Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für die Organisation aktivieren. Weitere Informationen zur Aktivierung der geplanten Segmentierung finden Sie unter [den Abschnitt zur Streaming-Segmentierung im Benutzerhandbuch zur Segmentierung](./overview.md#scheduled-segmentation).

Eine Abfrage wird automatisch mit Streaming-Segmentierung ausgewertet, wenn sie eines der folgenden Kriterien erfüllt:

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Einzelereignis | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Einzelnes Ereignis innerhalb eines relativen Zeitfensters | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis verweist. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Einzelnes Ereignis mit Zeitfenster | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem Zeitfenster verweist. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Nur Profil | Jede Segmentdefinition, die nur auf ein Profilattribut verweist. |  |
| Einzelnes Ereignis mit einem Profilattribut | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profilattribute verweist. **Hinweis:** Die Abfrage wird sofort ausgewertet, wenn das Ereignis eintritt. Im Fall eines Profilereignisses muss die Integration jedoch 24 Stunden warten. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Einzelnes Ereignis mit einem Profilattribut innerhalb eines relativen Zeitfensters | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis und ein oder mehrere Profilattribute verweist. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segment von Segmenten | Jede Segmentdefinition, die einen oder mehrere Batch- oder Streaming-Segmente enthält. **Hinweis:** Wenn ein Segment von Segmenten verwendet wird, erfolgt eine Profildisqualifizierung **alle 24 Stunden**. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Mehrere Ereignisse mit Profilattribut | Jede Segmentdefinition, die auf mehrere Ereignisse verweist **innerhalb der letzten 24 Stunden** und (optional) ein oder mehrere Profilattribute hat. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Eine Segmentdefinition **not** für Streaming-Segmentierung in den folgenden Szenarien aktiviert werden:

- Die Segmentdefinition umfasst Adobe Audience Manager-Segmente oder -Eigenschaften (AAM).
- Die Segmentdefinition umfasst mehrere Entitäten (Abfragen mit mehreren Entitäten).

Beachten Sie bei der Streaming-Segmentierung die folgenden Richtlinien:

| Abfragetyp | Richtlinie |
| ---------- | -------- |
| Einzelereignisabfrage | Das Lookback-Fenster ist nicht beschränkt. |
| Abfrage mit Ereignisverlauf | <ul><li>Das Lookback-Fenster ist auf **ein Tag**.</li><li>Eine strikte Bedingung für die Zeitreihenfolge **must** zwischen den Ereignissen vorhanden sind.</li><li>Abfragen mit mindestens einem negativen Ereignis werden unterstützt. Das gesamte Ereignis **cannot** eine Negation sein.</li></ul> |

Wenn eine Segmentdefinition geändert wird, sodass sie die Kriterien für Streaming-Segmentierung nicht mehr erfüllt, wird die Segmentdefinition automatisch von &quot;Streaming&quot;zu &quot;Batch&quot;geändert.

Darüber hinaus erfolgt die Aufhebung der Segmentqualifizierung, ähnlich wie bei der Segmentqualifizierung, in Echtzeit. Wenn sich eine Zielgruppe daher nicht mehr für ein Segment qualifiziert, wird sie sofort nicht qualifiziert. Wenn in der Segmentdefinition beispielsweise nach &quot;Alle Benutzer, die in den letzten drei Stunden rote Schuhe gekauft haben&quot;gefragt wird, werden nach drei Stunden alle Profile, die sich ursprünglich für die Segmentdefinition qualifiziert haben, nicht qualifiziert.

## Streaming-Segmentdetails

Nachdem Sie ein Streaming-fähiges Segment erstellt haben, können Sie Details zu diesem Segment anzeigen.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Details zum **[!UICONTROL Gesamtzahl der qualifizierten Zielgruppengröße]** angezeigt. Die **[!UICONTROL Gesamtzahl der qualifizierten Zielgruppengrößen]** zeigt die Gesamtzahl qualifizierter Zielgruppen aus der letzten abgeschlossenen Segmentauftragsausführung an. Wenn ein Segmentauftrag nicht innerhalb der letzten 24 Stunden abgeschlossen wurde, wird die Anzahl der Zielgruppen stattdessen aus einer Schätzung abgeleitet.

Darunter ist ein Kantengraph, der die Anzahl der Segmente anzeigt, die in den letzten 24 Stunden qualifiziert und disqualifiziert wurden. Das Dropdown-Menü kann angepasst werden, um die letzten 24 Stunden, letzte Woche oder letzten 30 Tage anzuzeigen.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Weitere Informationen zur letzten Segmentbewertung finden Sie durch Auswahl der Informationsblase.

![](../images/ui/streaming-segmentation/info-bubble.png)

Weitere Informationen zu Segmentdefinitionen finden Sie im vorherigen Abschnitt unter [Details zur Segmentdefinition](#segment-details).

## Nächste Schritte

In diesem Benutzerhandbuch wird erläutert, wie Streaming-fähige Segmentdefinitionen in Adobe Experience Platform funktionieren und wie Streaming-fähige Segmente überwacht werden.

Weitere Informationen zur Verwendung der Adobe Experience Platform-Benutzeroberfläche finden Sie in der [Benutzerhandbuch zur Segmentierung](./overview.md).

## Anhang

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zur Streaming-Segmentierung:

### Tritt die &quot;Nicht-Qualifizierung&quot;der Streaming-Segmentierung auch in Echtzeit auf?

In den meisten Fällen wird die Qualifizierung der Streaming-Segmentierung in Echtzeit aufgehoben. Streaming-Segmente, die Segmente von Segmenten verwenden, tun dies jedoch **not** in Echtzeit nicht qualifizieren, anstatt die Qualifizierung nach 24 Stunden aufzuheben.

### Auf welche Daten funktioniert Streaming-Segmentierung?

Streaming-Segmentierung funktioniert mit allen Daten, die mit einer Streaming-Quelle erfasst wurden. Segmente, die mit einer Batch-basierten Quelle erfasst werden, werden nächtlich ausgewertet, selbst wenn sie für Streaming-Segmentierung geeignet sind.

### Wie werden Segmente als Batch- oder Streaming-Segmentierung definiert?

Ein Segment wird entweder als Batch- oder Streaming-Segmentierung basierend auf einer Kombination aus Abfragetyp und Ereignisverlaufsdauer definiert. Eine Liste der Segmente, die als Streaming-Segment ausgewertet werden, finden Sie im [Abschnitt zu Streaming-Segmentierungs-Abfragetypen](#query-types).

### Kann ein Benutzer ein Segment als Batch- oder Streaming-Segmentierung definieren?

Zu diesem Zeitpunkt kann der Benutzer nicht definieren, ob ein Segment mithilfe der Batch- oder Streaming-Erfassung ausgewertet wird, da das System automatisch bestimmt, mit welcher Methode das Segment ausgewertet wird.

### Warum steigt die Anzahl der &quot;insgesamt qualifizierten&quot;Segmente weiterhin, während die Zahl unter &quot;Letzte X Tage&quot;im Abschnitt mit den Segmentdetails bei null bleibt?

Die Anzahl der insgesamt qualifizierten Segmente wird aus dem täglichen Segmentierungsauftrag gezogen, der Zielgruppen enthält, die sich sowohl für Batch- als auch für Streaming-Segmente qualifizieren. Dieser Wert wird sowohl für Batch- als auch für Streaming-Segmente angezeigt.

Die Zahl unter &quot;Letzte X Tage&quot; **only** umfasst Zielgruppen, die für Streaming-Segmentierung qualifiziert sind, und **only** erhöht sich, wenn Sie Daten in das System gestreamt haben, und zählt für diese Streaming-Definition. Dieser Wert ist **only** wird für Streaming-Segmente angezeigt. Daher wird dieser Wert **kann** als 0 für Batch-Segmente anzeigen.

Wenn Sie also feststellen, dass die Zahl unter &quot;Letzte X Tage&quot;null ist und das Liniendiagramm ebenfalls null meldet, haben Sie **not** alle Profile in das System gestreamt, die für dieses Segment qualifiziert wären.