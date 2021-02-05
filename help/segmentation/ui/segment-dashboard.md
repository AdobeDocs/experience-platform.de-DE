---
keywords: Experience Platform;Profil;Segment;Segmente;Segmentierung;Benutzeroberfläche;UI;Anpassen;SegmentDashboard;Dashboard
title: Segment-Dashboard-UI-Handbuch
description: 'In diesem Handbuch wird das in der Adobe Experience Platform-Benutzeroberfläche verfügbare Segment-Dashboard beschrieben. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---


# (Alpha) Segment-Dashboard {#segment-dashboard}

>[!IMPORTANT]
>
>Die in diesem Dokument beschriebene Dashboard-Funktion ist derzeit alphanumerisch und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Die Adobe Experience Platform-Benutzeroberfläche (UI) bietet ein Dashboard, mit dem Sie wichtige Informationen zu Ihren Segmenten, wie sie in einem täglichen Schnappschuss erfasst werden, Ansichten durchführen können. In diesem Handbuch wird beschrieben, wie Sie auf das Segmentelement in der Benutzeroberfläche zugreifen und mit ihm arbeiten, und es werden weitere Informationen zu den im Dashboard angezeigten Visualisierungen bereitgestellt.

Einen Überblick über alle Adobe Experience Platform-Segmentierungsdienstfunktionen in der Plattform-Benutzeroberfläche finden Sie im Handbuch [Segmentierungsdienst-Benutzeroberfläche](overview.md).

## Segmentdaten Dashboard

Das Dashboard segment zeigt eine Momentaufnahme der Attributdaten (Datensatzdaten) an, die Ihr Unternehmen im in der Experience Platform befindlichen Profil-Store hat. Der Schnappschuss enthält keine Ereignis- (Zeitreihendaten).

Die Attributdaten im Schnappschuss zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem der Schnappschuss erstellt wurde. Das heißt, der Schnappschuss ist keine Näherung oder Stichprobe der Daten und das Segmentelement wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Erstellung des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Segmentanalyse - Dashboard

Um zum Segmentelement in der Plattform-Benutzeroberfläche zu navigieren, wählen Sie in der linken Leiste **[!UICONTROL Segmente]** aus und klicken Sie dann auf die Registerkarte **[!UICONTROL Übersicht]**, um das Dashboard anzuzeigen.

![](../images/ui/segment-dashboard/dashboard-overview.png)

### Segment auswählen

Um ein zu Ansicht Segment im Dashboard auszuwählen, wählen Sie die Dialogfeldauswahl für das Textfeld **[!UICONTROL Segment]** auswählen.

![](../images/ui/segment-dashboard/select-segment.png)

>[!NOTE]
>
>Wenn ein Segment bereits ausgewählt ist, verwenden Sie `X`, um das Segment zuerst zu entfernen, und dann wird die Dialogauswahl angezeigt.
>
>![](../images/ui/segment-dashboard/remove-segment.png)

Das Dialogfeld **[!UICONTROL Segment auswählen]** wird geöffnet, in dem Sie das zu Ansicht Segment auswählen können. Nach Auswahl des gewünschten Segments verwenden Sie **[!UICONTROL Select]**, um zum Dashboard zurückzukehren.

![](../images/ui/segment-dashboard/select-segment-dialog.png)

### Richtlinie zusammenführen

Nach Auswahl eines Segments wird das Textfeld für die Zusammenführungsrichtlinie automatisch mit der für dieses Segment geltenden Richtlinie gefüllt.

Weitere Informationen zum Erstellen von Segmenten in der Experience Platform finden Sie im Handbuch [Segmentaufbau-Benutzeroberfläche](segment-builder.md). Weitere Informationen zu Zusammenführungsrichtlinien erhalten Sie zunächst im [Überblick über das Echtzeit-Profil des Kunden](../../profile/home.md).

![](../images/ui/segment-dashboard/merge-policy.png)

### Widgets und Metriken

Das Segment-Dashboard besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihrem ausgewählten Segment enthalten. Das Datum und die Uhrzeit der letzten Aktualisierung im Widget werden angezeigt, wenn der letzte Schnappschuss der Daten aufgenommen wurde.

![](../images/ui/segment-dashboard/widget-timestamp.png)

## Verfügbare Widgets

Experience Platform bietet mehrere Widgets, mit denen Sie verschiedene Metriken zu Ihrem Segment visualisieren können. Wählen Sie unten den Namen eines Widget aus, um weitere Informationen zu erhalten:

* [[!UICONTROL Segmentgröße]](#segment-size)
* [[!UICONTROL Profile nach Namensraum]](#profiles-by-namespace)

### [!UICONTROL Segmentgröße] {#segment-size}

Das Widget **[!UICONTROL Segmentgröße]** zeigt die Gesamtanzahl der zusammengeführten Profil im ausgewählten Segment zum Zeitpunkt des Snapshots an. Diese Anzahl ist das Ergebnis der Anwendung der Segmentzusammenführungs-Richtlinie auf Ihre Profil-Daten, um Profil-Fragmente zu einem einzigen Profil für jede einzelne Segmentperson zusammenzuführen.

Weitere Informationen zu Fragmenten und zusammengeführten Profilen erhalten Sie zunächst im [Überblick über das Echtzeit-Profil des Kunden](../home.md).

![](../images/ui/segment-dashboard/segment-size.png)

### [!UICONTROL Profile nach Namensraum] {#profiles-by-namespace}

Das Widget **[!UICONTROL Profil nach Namensraum]** zeigt die Aufschlüsselung der Namensraum für alle zusammengeführten Profil im ausgewählten Segment an. Die Gesamtanzahl der Profil nach [!UICONTROL ID-Namensraum] (d. h. addieren Sie die für jeden Namensraum angezeigten Werte) ist in der Regel höher als die Gesamtanzahl der Profil im Segment, da ein Profil mehrere Namensraum damit verknüpft sein könnte. Wenn ein Kunde beispielsweise auf mehr als einem Kanal mit Ihrer Marke interagiert, können mehrere Namensraum mit diesem Kunden verknüpft werden.

Weitere Informationen zu Identitäts-Namensräumen finden Sie in der [Adobe Experience Platform Identity Service-Dokumentation](../../identity-service/home.md).

![](../images/ui/segment-dashboard/profiles-by-namespace.png)

## Zusätzliche Dashboards

Die Plattform-Benutzeroberfläche bietet zusätzliche Dashboards zum Anzeigen von Momentaufnahmen Ihrer Daten in der Experience Platform. Zu diesen Dashboards zählen Echtzeit-Kundendaten und [!UICONTROL Lizenznutzung]. Weitere Informationen zu diesen zusätzlichen Dashboards finden Sie unter den folgenden Links:

* [[!DNL Profile] dashboard](../../profile/ui/profile-dashboard.md)
* [[!UICONTROL License ] usagedashboard](../../landing/license-usage-dashboard.md)

## Nächste Schritte

Indem Sie diesem Dokument folgen, sollten Sie nun in der Lage sein, das Segmentsegment zu suchen und ein Dashboard zur Ansicht auszuwählen. Sie sollten auch die Metriken verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Segmenten in der Benutzeroberfläche der Experience Platform finden Sie im Handbuch [Segmentierungsdienst-Benutzeroberfläche](overview.md).