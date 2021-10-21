---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Benutzerschnittstelle;UI;Anpassung;Profil-Dashboard;Dashboard
title: Ziel-Dashboard
description: Adobe Experience Platform bietet ein Dashboard zur Ansicht wichtiger Informationen über die aktiven Ziele Ihres Unternehmens.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: a920e8aaccb4da6a3aa08f0d420cee0d1944ab9a
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 6%

---

# [!UICONTROL Dashboard „Ziele“]

Die Adobe Experience Platform-Benutzeroberfläche (UI) bietet ein Dashboard zur Ansicht wichtiger Informationen über die aktiven Ziele Ihres Unternehmens, wie sie in einem täglichen Schnappschuss erfasst werden. In diesem Handbuch wird erläutert, wie Sie auf das Dashboard &quot;Ziele&quot;in der Benutzeroberfläche zugreifen und mit diesem arbeiten können, und es werden weitere Informationen zu den im Dashboard angezeigten Metriken bereitgestellt.

Einen Überblick über die Reiseziele sowie einen Katalog aller in der Experience Platform verfügbaren Reiseziele finden Sie unter [Dokumentation zu Zielen](../../destinations/home.md).

## [!UICONTROL Ziele] Dashboard-Daten {#destinations-dashboard-data}

Die [!UICONTROL Ziele] Dashboard zeigt eine Momentaufnahme der Ziele an, die Ihr Unternehmen in der Experience Platform aktiviert hat. Der Schnappschuss zeigt die Daten exakt so an, wie sie zum Zeitpunkt der Schnappschussaufnahme aufgetreten sind. Mit anderen Worten, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Ziel-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Das Dashboard der Reiseziele

Um zum Dashboard &quot;Ziele&quot;in der Platform-UI zu navigieren, wählen Sie **[!UICONTROL Ziele]** in der linken Leiste, und wählen Sie dann die **[!UICONTROL Überblick]** , um das Dashboard anzuzeigen.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu in der Experience Platform ist und noch keine aktiven Ziele hat, [!UICONTROL Ziele] Dashboard und [!UICONTROL Überblick] sind nicht sichtbar. Wählen Sie stattdessen [!UICONTROL Ziele] aus der linken Navigation zeigt die [!UICONTROL Katalog] Tabulator. Weitere Informationen zum Thema [!UICONTROL Katalog] auf der [[!UICONTROL Ziele] Arbeitsbereichsleitfaden](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### Dashboard zum Ändern des Zielorts

Sie können das Erscheinungsbild des Dashboards Ziele ändern, indem Sie **[!UICONTROL Dashboard ändern]**. Dadurch können Sie Widgets aus dem Dashboard verschieben, hinzufügen und entfernen sowie auf **[!UICONTROL Widget-Bibliothek]** , um verfügbare Widgets zu erkunden und benutzerdefinierte Widgets für Ihr Unternehmen zu erstellen.

Siehe [Dashboards ändern](../customize/modify.md) und [Widget-Bibliotheksübersicht](../customize/widget-library.md) Dokumentation, um mehr zu erfahren.

## Standard-Widgets

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken in Bezug auf Ihre Ziele visualisieren können. Sie können benutzerdefinierte Widgets erstellen, die für Ihr Unternehmen freigegeben werden können. Verwenden Sie dazu die [!UICONTROL Widget-Bibliothek]. Weitere Informationen zum Erstellen benutzerdefinierter Widgets erhalten Sie im [Widget-Bibliotheksübersicht](../customize/widget-library.md).

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Bevorzugte Ziele]](#most-used-destinations)
* [[!UICONTROL Kürzlich erstellte Ziele]](#recently-created-destinations)
* [[!UICONTROL Zuletzt aktivierte Segmente]](#recently-activated-segments)

### [!UICONTROL Bevorzugte Ziele] {#most-used-destinations}

Die **[!UICONTROL Bevorzugte Ziele]** Widget zeigt die Top-Ziele Ihres Unternehmens nach Anzahl der zugeordneten Segmente ab dem letzten Schnappschuss an. Diese Rangliste bietet einen Einblick, welche Ziele genutzt werden, und zeigt möglicherweise auch diejenigen, die nicht ausreichend genutzt werden können.

Wenn Sie zum Beispiel gestern ein Ziel konfiguriert haben, diesem aber keine Segmente zugeordnet haben, können Sie sehen, dass das Ziel zurzeit nicht voll ausgelastet ist.

Die Anzahl der zugeordneten Segmente, die in der Segmentzählungsspalte angezeigt werden, ist ab dem letzten täglichen Schnappschuss korrekt. Durch Zuordnen eines neuen Segments zum Ziel wird die Anzahl erst aktualisiert, wenn der nächste Schnappschuss erstellt wurde.

Wenn Sie den Zielgruppennamen aus der im Widget angezeigten Liste auswählen, gelangen Sie zu den Zieldetails, die über den Link **[!UICONTROL Durchsuchen]** Tabulator. Sie können auch **[!UICONTROL Ansicht alle]** um zu **[!UICONTROL Durchsuchen]** und wählen Sie dann den Namen eines Ziels aus, um dessen Details Ansicht.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Kürzlich erstellte Ziele] {#recently-created-destinations}

Die **[!UICONTROL Kürzlich erstellte Ziele]** Widget ermöglicht es Ihnen, eine Liste der zuletzt konfigurierten Ziele Ihres Unternehmens anzuzeigen.

Das angezeigte Erstellungsdatum stimmt mit dem letzten täglichen Schnappschuss überein. Wenn Sie also ein neues Ziel erstellen, wird es erst nach dem nächsten Schnappschuss in der Liste angezeigt.

Wenn Sie den Zielgruppennamen aus der im Widget angezeigten Liste auswählen, gelangen Sie zu den Zieldetails, die über den Link **[!UICONTROL Durchsuchen]** Tabulator. Sie können auch **[!UICONTROL Ansicht alle]** um zu **[!UICONTROL Durchsuchen]** und wählen Sie dann den Namen eines Ziels aus, um dessen Details Ansicht.

Weitere Informationen zur Konfiguration bestimmter Zieltypen finden Sie unter [Dokumentation zu Zielen](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Zuletzt aktivierte Segmente] {#recently-activated-segments}

Die **[!UICONTROL Zuletzt aktivierte Segmente]** -Widget bietet eine Liste der Segmente, die einem Ziel zuletzt zugeordnet wurden. Diese Liste bietet eine Momentaufnahme der aktiven Verwendung von Segmenten und Zielen im System und kann bei der Fehlerbehebung bei fehlerhaften Zuordnungen helfen.

Das angezeigte aktualisierte Datum zeigt das letzte Mal an, dass das Segment am Ziel aktiviert wurde, und stimmt mit dem letzten täglichen Schnappschuss überein. Mit anderen Worten: Wenn Sie ein Segment zum Ziel aktivieren, ändert sich das aktualisierte Datum erst, nachdem der nächste Schnappschuss gemacht wurde.

Wenn Sie den Segmentnamen aus der im Widget angezeigten Liste auswählen, gelangen Sie zu den Segmentdetails. Sie können auch **[!UICONTROL Ansicht alle]** um zur Registerkarte &quot;Segmentsuche&quot;zu navigieren und dann den Segmentnamen auszuwählen, um die Segmentdetails Ansicht.

Weitere Informationen zum Arbeiten mit Segmenten in der Experience Platform erhalten Sie im [Übersicht über Segmentdienste](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie nun in der Lage sein, das Dashboard der Ziele zu finden und die Metriken zu verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Zielen in der Experience Platform finden Sie im [Dokumentation zu Zielen](../../destinations/home.md).
