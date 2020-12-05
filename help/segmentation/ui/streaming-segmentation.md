---
keywords: Experience Platform;home;popular topics;streaming segmentation;Segmentation;Segmentation Service;segmentation service;ui guide;
solution: Experience Platform
title: Streaming-Segmentierung
topic: ui guide
description: Streaming-Segmentierung Unter Adobe Experience Platform können Sie Segmentierungen in Echtzeit durchführen und sich dabei auf den Datenreichtum konzentrieren. Mit der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Daten in die Plattform gelangen, was die Planung und Ausführung von Segmentierungsaufträgen erleichtert. Mit dieser Funktion können die meisten Segmentregeln jetzt bewertet werden, wenn die Daten an die Plattform übergeben werden. Dies bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden.
translation-type: tm+mt
source-git-commit: 2bd4b773f7763ca408b55e3b0e2d0bbe9e7b66ba
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---


# Streaming-Segmentierung

>[!NOTE]
>
>Im folgenden Dokument wird erläutert, wie die Streaming-Segmentierung mithilfe der Benutzeroberfläche verwendet wird. Informationen zur Verwendung der Streaming-Segmentierung mit der API finden Sie im Handbuch zur [Streaming-Segmentierungs-API](../api/streaming-segmentation.md).

Die Streaming-Segmentierung für [!DNL Adobe Experience Platform] ermöglicht es Kunden, die Segmentierung in Echtzeit durchzuführen und sich dabei auf den Datenreichtum zu konzentrieren. Mit der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Daten in Streaming übertragen werden, [!DNL Platform]was die Planung und Ausführung von Segmentierungsaufträgen erleichtert. With this capability, most segment rules can now be evaluated as the data is passed into [!DNL Platform], meaning segment membership will be kept up-to-date without running scheduled segmentation jobs.

>[!NOTE]
>
>Streaming-Segmentierung kann nur zur Auswertung von Daten verwendet werden, die in Plattform gestreamt werden. Mit anderen Worten, Daten, die durch die Stapelverarbeitung erfasst werden, werden nicht durch Streaming-Segmentierung ausgewertet und werden zusammen mit dem nächtlich geplanten segmentierten Auftrag ausgewertet.

## Streaming-Segmentierungsarten für Abfragen

>[!NOTE]
>
>Damit Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für das Unternehmen aktivieren. For details on enabling scheduled segmentation, please refer to [the streaming segmentation section in the Segmentation user guide](./overview.md#scheduled-segmentation).

Eine Abfrage wird automatisch mit Streaming-Segmentierung bewertet, wenn sie eines der folgenden Kriterien erfüllt:

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Eingehender Treffer | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Eingehender Treffer innerhalb eines relativen Zeitfensters | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis verweist. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Nur Profil | Eine Segmentdefinition, die nur auf ein Profil-Attribut verweist. |  |
| Eingehender Treffer, der sich auf ein Profil bezieht | Eine Segmentdefinition, die sich auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profil-Attribute bezieht. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Eingehender Treffer, der sich auf ein Profil innerhalb eines relativen Zeitfensters bezieht | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis und ein oder mehrere Profil-Attribute verweist. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Mehrere Ereignis, die auf ein Profil verweisen | Eine Segmentdefinition, die sich **innerhalb der letzten 24 Stunden** auf mehrere Ereignis bezieht und (optional) ein oder mehrere Profil-Attribute besitzt. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

In den folgenden Szenarien wird eine Segmentdefinition für die Streaming-Segmentierung **nicht** aktiviert:

- Die Segmentdefinition umfasst Adobe Audience Manager-Segmente oder -Eigenschaften (AAM).
- Die Segmentdefinition umfasst mehrere Entitäten (Abfragen mit mehreren Entitäten).

Darüber hinaus gelten einige Richtlinien bei der Streaming-Segmentierung:

| Abfragetyp | Leitlinie |
| ---------- | -------- |
| Abfrage mit einem Ereignis | Das Lookback-Fenster unterliegt keinen Einschränkungen. |
| Abfrage mit Ereignis-Verlauf | <ul><li>Das Lookback-Fenster ist auf **einen Tag** beschränkt.</li><li>Zwischen den Ereignissen **muss** eine strikte Bedingung für die zeitliche Reihenfolge bestehen.</li><li>Abfragen mit mindestens einem negierten Ereignis werden unterstützt. Das gesamte Ereignis **kann jedoch keine** Negation sein.</li></ul> |

Wenn eine Segmentdefinition so geändert wird, dass sie die Kriterien für die Streaming-Segmentierung nicht mehr erfüllt, wechselt die Segmentdefinition automatisch von &quot;Streaming&quot;zu &quot;Batch&quot;.

## Details zu Streaming-Segmenten

Nachdem Sie ein Streaming-fähiges Segment erstellt haben, können Sie Details zu diesem Segment zur Ansicht hinzufügen.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Insbesondere werden Details zur Größe der **[!UICONTROL gesamten qualifizierten Audience]** angezeigt. Die **[!UICONTROL Gesamtgröße]** der qualifizierten Audience zeigt die Gesamtanzahl der qualifizierten Audiencen aus der zuletzt ausgeführten Segmentausführung an. Wenn ein Segmentauftrag nicht innerhalb der letzten 24 Stunden abgeschlossen wurde, wird stattdessen die Anzahl der Audiencen einer Schätzung entnommen.

Darunter befindet sich ein Liniendiagramm, das die Anzahl der Segmente anzeigt, die in den letzten 24 Stunden qualifiziert und disqualifiziert wurden. Die Dropdownliste kann angepasst werden, um die letzten 24 Stunden, letzte Woche oder letzten 30 Tage anzuzeigen.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment-graph.png)

Weitere Informationen zur letzten Segmentbewertung finden Sie durch Auswahl der Informationsblase.

![](../images/ui/streaming-segmentation/info-bubble.png)

Weitere Informationen zu Segmentdefinitionen finden Sie im vorherigen Abschnitt zu [Segmentdefinitionsdetails](#segment-details).

## Videodemo zur Streaming-Segmentierung

Das folgende Video soll Ihr Verständnis von Streaming-Segmentierung unterstützen. Es zeigt ein Beispiel für eine Kundenerfahrung, gefolgt von einem kurzen Überblick über die wichtigsten Funktionen der [!DNL Platform] Oberfläche.

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## Nächste Schritte

In diesem Benutzerhandbuch wird erläutert, wie Streaming-fähige Segmentdefinitionen auf Adobe Experience Platform funktionieren und wie Streaming-fähige Segmente überwacht werden.

Weitere Informationen zur Verwendung der Adobe Experience Platform-Benutzeroberfläche finden Sie im Benutzerhandbuch [zur Segmentierung](./overview.md).