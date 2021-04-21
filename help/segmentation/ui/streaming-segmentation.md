---
keywords: Experience Platform;Home;beliebte Themen;Streaming-Segmentierung;Segmentierung;Segmentierungsdienst;Segmentierungsdienst;i-Handbuch
solution: Experience Platform
title: Handbuch zur Streaming-Segmentierung
topic-legacy: ui guide
description: Durch Streaming-Segmentierung auf Adobe Experience Platform können Sie die Segmentierung in Echtzeit durchführen und sich dabei auf den Datenreichtum konzentrieren. Mit der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Daten in die Plattform gelangen, was die Planung und Ausführung von Segmentierungsaufträgen erleichtert. Mit dieser Funktion können die meisten Segmentregeln jetzt bewertet werden, wenn die Daten an die Plattform übergeben werden. Dies bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# Streaming-Segmentierung

>[!NOTE]
>
>Im folgenden Dokument wird erläutert, wie die Streaming-Segmentierung mithilfe der Benutzeroberfläche verwendet wird. Informationen zur Verwendung der Streaming-Segmentierung mit der API finden Sie im Handbuch [Streaming-Segmentierungs-API](../api/streaming-segmentation.md).

Die Streaming-Segmentierung für [!DNL Adobe Experience Platform] ermöglicht es Kunden, die Segmentierung in Echtzeit durchzuführen und sich dabei auf den Datenreichtum zu konzentrieren. Bei der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Streaming-Daten in [!DNL Platform] eingehen, was die Planung und Ausführung von Segmentierungsaufträgen erleichtert. Mit dieser Funktion können die meisten Segmentregeln jetzt bewertet werden, wenn die Daten an [!DNL Platform] übergeben werden. Das bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden.

>[!NOTE]
>
>Streaming-Segmentierung kann nur zur Auswertung von Daten verwendet werden, die in Plattform gestreamt werden. Mit anderen Worten, Daten, die durch die Stapelverarbeitung erfasst werden, werden nicht durch Streaming-Segmentierung ausgewertet und werden zusammen mit dem nächtlich geplanten Segmentauftrag ausgewertet.
>
>Darüber hinaus können Segmente, die mit Streaming-Segmentierung ausgewertet werden, zwischen idealer und tatsächlicher Mitgliedschaft wechseln, wenn das Segment auf einem anderen Segment basiert, das mithilfe der Stapelsegmentierung bewertet wird. Beispiel: Wenn Segment A auf Segment B basiert und Segment B mithilfe der Stapelsegmentierung ausgewertet wird, da Segment B nur alle 24 Stunden aktualisiert wird, entfernt sich Segment A weiter von den tatsächlichen Daten, bis es mit der Aktualisierung Segment B erneut synchronisiert wird.

## Streaming-Segmentierungsarten für Abfragen

>[!NOTE]
>
>Damit Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für das Unternehmen aktivieren. Weitere Informationen zum Aktivieren der geplanten Segmentierung finden Sie im Abschnitt [Streaming-Segmentierung im Segmentierungsbenutzerleitfaden](./overview.md#scheduled-segmentation).

Eine Abfrage wird automatisch mit Streaming-Segmentierung bewertet, wenn sie eines der folgenden Kriterien erfüllt:

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Eingehender Treffer | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Eingehender Treffer innerhalb eines relativen Zeitfensters | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis verweist. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Eingehender Treffer mit einem Zeitfenster | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem Zeitfenster verweist. | ![](../images/ui/streaming-segmentation/historic-time-window.png) |
| Nur Profil | Eine Segmentdefinition, die nur auf ein Profil-Attribut verweist. |  |
| Eingehender Treffer, der sich auf ein Profil bezieht | Eine Segmentdefinition, die sich auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profil-Attribute bezieht. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Eingehender Treffer, der sich auf ein Profil innerhalb eines relativen Zeitfensters bezieht | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis und ein oder mehrere Profil-Attribute verweist. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Segment der Segmente | Jede Segmentdefinition, die ein oder mehrere Batch- oder Streaming-Segmente enthält. | ![](../images/ui/streaming-segmentation/two-batches.png) |
| Mehrere Ereignis, die auf ein Profil verweisen | Eine Segmentdefinition, die auf mehrere Ereignis **innerhalb der letzten 24 Stunden** und (optional) verweist, verfügt über ein oder mehrere Profil-Attribute. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Eine Segmentdefinition wird für die Streaming-Segmentierung in den folgenden Szenarien **nicht** aktiviert:

- Die Segmentdefinition umfasst Adobe Audience Manager-Segmente oder -Eigenschaften (AAM).
- Die Segmentdefinition umfasst mehrere Entitäten (Abfragen mit mehreren Entitäten).

Darüber hinaus gelten einige Richtlinien bei der Streaming-Segmentierung:

| Abfragetyp | Leitlinie |
| ---------- | -------- |
| Abfrage mit einem Ereignis | Das Lookback-Fenster unterliegt keinen Einschränkungen. |
| Abfrage mit Ereignis-Verlauf | <ul><li>Das Lookback-Fenster ist auf **einen Tag** beschränkt.</li><li>Zwischen den Ereignissen muss eine strikte Bedingung für die zeitliche Reihenfolge **vorhanden sein.**</li><li>Abfragen mit mindestens einem negierten Ereignis werden unterstützt. Das gesamte Ereignis **kann jedoch keine Negation sein.**</li></ul> |

Wenn eine Segmentdefinition so geändert wird, dass sie die Kriterien für die Streaming-Segmentierung nicht mehr erfüllt, wechselt die Segmentdefinition automatisch von &quot;Streaming&quot;zu &quot;Batch&quot;.

## Details zu Streaming-Segmenten

Nachdem Sie ein Streaming-fähiges Segment erstellt haben, können Sie Details zu diesem Segment zur Ansicht hinzufügen.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Insbesondere werden Details zur Gesamtgröße der qualifizierten Audience **[!UICONTROL angezeigt.]** Die **[!UICONTROL Gesamtgröße der qualifizierten Audience]** zeigt die Gesamtanzahl der qualifizierten Audiencen aus der zuletzt ausgeführten Segmentausführung an. Wenn ein Segmentauftrag nicht innerhalb der letzten 24 Stunden abgeschlossen wurde, wird stattdessen die Anzahl der Audiencen einer Schätzung entnommen.

Darunter befindet sich ein Liniendiagramm, das die Anzahl der Segmente anzeigt, die in den letzten 24 Stunden qualifiziert und disqualifiziert wurden. Die Dropdownliste kann angepasst werden, um die letzten 24 Stunden, letzte Woche oder letzten 30 Tage anzuzeigen.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Weitere Informationen zur letzten Segmentbewertung finden Sie durch Auswahl der Informationsblase.

![](../images/ui/streaming-segmentation/info-bubble.png)

Weitere Informationen zu Segmentdefinitionen finden Sie im vorherigen Abschnitt unter [Segmentdefinitionsdetails](#segment-details).

## Nächste Schritte

In diesem Benutzerhandbuch wird erläutert, wie Streaming-fähige Segmentdefinitionen auf Adobe Experience Platform funktionieren und wie Streaming-fähige Segmente überwacht werden.

Weitere Informationen zur Verwendung der Adobe Experience Platform-Benutzeroberfläche finden Sie im [Segmentierungs-Benutzerhandbuch](./overview.md).
