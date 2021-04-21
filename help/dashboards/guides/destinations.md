---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Benutzeroberfläche;Anpassung;Profil-Dashboard;Dashboard
title: Dashboard Ziele
description: Adobe Experience Platform bietet ein Dashboard zur Ansicht wichtiger Informationen über die aktiven Ziele Ihres Unternehmens.
topic-legacy: guide
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---

# (Beta) [!UICONTROL Dashboard Ziele]

>[!IMPORTANT]
>
>Die in diesem Dokument beschriebene Dashboard-Funktion befindet sich derzeit in der Beta-Version und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Die Adobe Experience Platform-Benutzeroberfläche (UI) bietet ein Dashboard, mit dem Sie wichtige Informationen zu den aktiven Zielen Ihres Unternehmens, wie sie in einem täglichen Schnappschuss erfasst werden, Ansichten vornehmen können. In diesem Handbuch wird erläutert, wie Sie auf das Dashboard &quot;Ziele&quot;in der Benutzeroberfläche zugreifen und mit ihm arbeiten können. Außerdem werden weitere Informationen zu den im Dashboard angezeigten Metriken bereitgestellt.

Einen Überblick über die Ziele sowie einen Katalog aller verfügbaren Ziele innerhalb der Experience Platform finden Sie unter [Übersicht über die Ziele](../../destinations/home.md).

## [!UICONTROL Dashboard-Daten ] zu Zielen  {#destinations-dashboard-data}

Das Dashboard [!UICONTROL Ziele] zeigt eine Momentaufnahme der Ziele an, die Ihr Unternehmen in Experience Profil aktiviert hat. Die Daten im Schnappschuss zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem der Schnappschuss erstellt wurde. Das heißt, der Schnappschuss ist keine Näherung oder Stichprobe der Daten, und das Dashboard &quot;Ziele&quot;wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Erstellung des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Das Dashboard Ziele erkunden

Um zum Dashboard &quot;Ziele&quot;in der Benutzeroberfläche &quot;Plattform&quot;zu navigieren, wählen Sie in der linken Leiste **[!UICONTROL Ziele]** aus und klicken Sie dann auf die Registerkarte **[!UICONTROL Übersicht]**, um das Dashboard anzuzeigen.

![](../images/destinations/dashboard-overview.png)

## Verfügbare Widgets

Experience Platform bietet mehrere Widgets, mit denen Sie verschiedene Metriken zu Ihren Zielen visualisieren können. Wählen Sie unten den Namen eines Widget aus, um weitere Informationen zu erhalten:

* [[!UICONTROL Am häufigsten verwendete Ziele]](#most-used-destinations)
* [[!UICONTROL Kürzlich erstellte Ziele]](#recently-created-destinations)
* [[!UICONTROL Kürzlich aktivierte Segmente]](#recently-activated-segments)

### [!UICONTROL Am häufigsten verwendete Ziele] {#most-used-destinations}

Das Widget **[!UICONTROL Am häufigsten verwendete Ziele]** zeigt die wichtigsten Ziele Ihres Unternehmens nach der Anzahl der zugeordneten Segmente ab dem letzten Schnappschuss an. Diese Rangliste bietet einen Einblick, welche Ziele genutzt werden, und zeigt möglicherweise auch diejenigen, die möglicherweise nicht ausreichend genutzt werden.

Wenn Sie beispielsweise gestern ein Ziel konfiguriert haben, ihm aber keine Segmente zugeordnet haben, können Sie sehen, dass das Ziel derzeit nicht genutzt wird.

Die Anzahl der zugeordneten Segmente, die in der Spalte für die Segmentanzahl angezeigt werden, ist ab dem letzten Schnappschuss pro Tag genau. Durch Zuordnen eines neuen Segments zum Ziel wird die Anzahl erst aktualisiert, wenn der nächste Schnappschuss erstellt wurde.

Wenn Sie den Zielnamen aus der Liste wählen, die im Widget angezeigt wird, gelangen Sie zu den Zieldetails, die auf der Registerkarte **[!UICONTROL Durchsuchen]** verknüpft sind. Sie können auch **[!UICONTROL Ansicht All]** auswählen, um zur Registerkarte **[!UICONTROL Durchsuchen]** zu navigieren und dann den Namen eines Ziels auszuwählen, dessen Details Ansicht werden sollen.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Kürzlich erstellte Ziele] {#recently-created-destinations}

Mit dem Widget **[!UICONTROL Kürzlich erstellte Ziele]** können Sie eine Liste der zuletzt konfigurierten Ziele Ihres Unternehmens anzeigen.

Das angezeigte Erstellungsdatum entspricht dem letzten Schnappschuss pro Tag. Wenn Sie also ein neues Ziel erstellen, wird es erst nach dem nächsten Schnappschuss in der Liste angezeigt.

Wenn Sie den Zielnamen aus der Liste wählen, die im Widget angezeigt wird, gelangen Sie zu den Zieldetails, die auf der Registerkarte **[!UICONTROL Durchsuchen]** verknüpft sind. Sie können auch **[!UICONTROL Ansicht All]** auswählen, um zur Registerkarte **[!UICONTROL Durchsuchen]** zu navigieren und dann den Namen eines Ziels auszuwählen, dessen Details Ansicht werden sollen.

Weitere Informationen zum Konfigurieren bestimmter Zieltypen finden Sie in der [Dokumentation zu Zielen](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Kürzlich aktivierte Segmente] {#recently-activated-segments}

Das Widget **[!UICONTROL Kürzlich aktivierte Segmente]** stellt eine Liste der Segmente bereit, die einem Ziel zuletzt zugeordnet wurden. Diese Liste bietet eine Momentaufnahme der aktiven Verwendung von Segmenten und Zielen im System und kann bei der Fehlerbehebung fehlerhafter Zuordnungen helfen.

Das angezeigte aktualisierte Datum zeigt an, wann das Segment zuletzt bis zum Ziel aktiviert wurde, und ist mit dem letzten Schnappschuss pro Tag korrekt. Wenn Sie also ein Segment zum Ziel aktivieren, ändert sich das aktualisierte Datum erst, nachdem der nächste Schnappschuss erstellt wurde.

Wenn Sie den Segmentnamen aus der Liste wählen, die im Widget angezeigt wird, gelangen Sie zu den Segmentdetails. Sie können auch **[!UICONTROL Ansicht All]** auswählen, um zur Registerkarte &quot;Segmentsuche&quot;zu navigieren und dann den Segmentnamen zur Ansicht der Segmentdetails auszuwählen.

Weitere Informationen zum Arbeiten mit Segmenten in der Experience Platform erhalten Sie zunächst im Abschnitt [Übersicht über den Segmentdienst](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Nächste Schritte

Indem Sie diesem Dokument folgen, sollten Sie jetzt in der Lage sein, das Dashboard &quot;Ziele&quot;zu finden und die Metriken zu verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Zielen in der Experience Platform finden Sie in der [Zieldokumentation](../../destinations/home.md).
