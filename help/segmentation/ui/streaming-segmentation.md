---
keywords: Experience Platform;home;popular topics;segment evaluation
solution: Experience Platform
title: Streaming-Segmentierung
topic: ui guide
description: Streaming-Segmentierung Unter Adobe Experience Platform können Sie Segmentierungen in Echtzeit durchführen und sich dabei auf den Datenreichtum konzentrieren. Mit der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Daten in die Plattform gelangen, was die Planung und Ausführung von Segmentierungsaufträgen erleichtert. Mit dieser Funktion können die meisten Segmentregeln jetzt bewertet werden, wenn die Daten an die Plattform übergeben werden. Dies bedeutet, dass die Segmentmitgliedschaft auf dem neuesten Stand gehalten wird, ohne dass geplante Segmentierungsaufträge ausgeführt werden.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 2%

---


# Streaming-Segmentierung

>[!NOTE]
>
>Im folgenden Dokument wird erläutert, wie die Streaming-Segmentierung mithilfe der Benutzeroberfläche verwendet wird. Informationen zur Verwendung der Streaming-Segmentierung mit der API finden Sie im Handbuch zur [Streaming-Segmentierungs-API](../api/streaming-segmentation.md).

Die Streaming-Segmentierung für [!DNL Adobe Experience Platform] ermöglicht es Kunden, die Segmentierung in Echtzeit durchzuführen und sich dabei auf den Datenreichtum zu konzentrieren. Mit der Streaming-Segmentierung erfolgt die Segmentqualifizierung jetzt, wenn Daten eingehen, [!DNL Platform]was die Planung und Ausführung von Segmentierungsaufträgen verringert. With this capability, most segment rules can now be evaluated as the data is passed into [!DNL Platform], meaning segment membership will be kept up-to-date without running scheduled segmentation jobs.

## Streaming-Segmentierungsarten für Abfragen

>[!NOTE]
>
>Damit Streaming-Segmentierung funktioniert, müssen Sie die geplante Segmentierung für das Unternehmen aktivieren. For details on enabling scheduled segmentation, please refer to [the streaming segmentation section in the Segmentation user guide](./overview.md#scheduled-segmentation).

Eine Abfrage wird automatisch mit Streaming-Segmentierung bewertet, wenn sie eines der folgenden Kriterien erfüllt:

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Eingehender Treffer | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | ![](../images/ui/streaming-segmentation/incoming-hit.png) |
| Eingehender Treffer innerhalb eines relativen Zeitfensters | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis **innerhalb der letzten sieben Tage** verweist. | ![](../images/ui/streaming-segmentation/relative-hit-success.png) |
| Nur Profil | Eine Segmentdefinition, die nur auf ein Profil-Attribut verweist. |  |
| Eingehender Treffer, der sich auf ein Profil bezieht | Eine Segmentdefinition, die sich auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profil-Attribute bezieht. | ![](../images/ui/streaming-segmentation/profile-hit.png) |
| Eingehender Treffer, der sich auf ein Profil innerhalb eines relativen Zeitfensters bezieht | Eine Segmentdefinition, die sich **innerhalb der letzten sieben Tage** auf ein einzelnes eingehendes Ereignis und ein oder mehrere Profil-Attribute bezieht. | ![](../images/ui/streaming-segmentation/profile-relative-success.png) |
| Mehrere Ereignis, die auf ein Profil verweisen | Jede Segmentdefinition, die sich **innerhalb der letzten 24 Stunden** auf mehrere Ereignis bezieht und (optional) ein oder mehrere Profil-Attribute besitzt. | ![](../images/ui/streaming-segmentation/event-history-success.png) |

Im folgenden Abschnitt werden Segmentdefinitionsbeispiele Liste, die für die Streaming-Segmentierung **nicht** aktiviert werden.

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Eingehender Treffer innerhalb eines relativen Zeitfensters | Wenn sich die Segmentdefinition auf ein eingehendes Ereignis bezieht, das **nicht** innerhalb der **letzten sieben Tage** liegt. Zum Beispiel innerhalb der **letzten zwei Wochen**. | ![](../images/ui/streaming-segmentation/relative-hit-failure.png) |
| Eingehender Treffer, der sich auf ein Profil in einem relativen Fenster bezieht | Die folgenden Optionen unterstützen **keine** Streaming-Segmentierung:<ul><li>Ein eingehendes Ereignis **nicht** innerhalb der **letzten sieben Tage**.</li><li>Eine Segmentdefinition, die [!DNL Adobe Audience Manager (AAM)] Segmente oder Eigenschaften enthält.</li></ul> | ![](../images/ui/streaming-segmentation/profile-relative-failure.png) |
| Mehrere Ereignis, die auf ein Profil verweisen | Die folgenden Optionen unterstützen **keine** Streaming-Segmentierung:<ul><li>Ein Ereignis, das **nicht** innerhalb **der letzten 24 Stunden** auftritt.</li><li>Eine Segmentdefinition, die Segmente oder Eigenschaften von Adobe Audience Manager (AAM) enthält.</li></ul> | ![](../images/ui/streaming-segmentation/event-history-failure.png) |
| Abfragen mit mehreren Entitäten | Abfragen mit mehreren Entitäten werden durch Streaming-Segmentierung insgesamt **nicht** unterstützt. |  |

Darüber hinaus gelten einige Richtlinien für die Streaming-Segmentierung:

| Abfragetyp | Leitlinie |
| ---------- | -------- |
| Abfrage mit einem Ereignis | Das Rückblickfenster ist auf **sieben Tage** begrenzt. |
| Abfrage mit Ereignis-Verlauf | <ul><li>Das Lookback-Fenster ist auf **einen Tag** beschränkt.</li><li>Zwischen den Ereignissen **muss** eine strikte Zeitbestellbedingung bestehen.</li><li>Nur einfache Zeitreihenfolgen (vor und nach) zwischen den Ereignissen sind zulässig.</li><li>Die einzelnen Ereignis **können nicht** negiert werden. Die gesamte Abfrage **kann** jedoch negiert werden.</li></ul> |

## Details zu Streaming-Segmenten

Nachdem Sie ein Streaming-fähiges Segment erstellt haben, können Sie Details zu diesem Segment zur Ansicht hinzufügen.

![](../images/ui/streaming-segmentation/monitoring-streaming-segment.png)

Insbesondere werden Details zur Größe der **[!UICONTROL gesamten qualifizierten Audience]** angezeigt. Wenn ein Auftrag innerhalb der letzten 24 Stunden ausgeführt wurde, wird neben einem Liniendiagramm für die hinzugefügte Audience die **[!UICONTROL Gesamtgröße]** der qualifizierten Audience angezeigt. Andernfalls wird die geschätzte **[!UICONTROL Gesamtgröße]** der Audience neben einer Visualisierungstrends-Linie angezeigt.

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