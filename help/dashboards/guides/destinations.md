---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Profil-Dashboard; Dashboard
title: Dashboard "Ziele"
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu den aktiven Zielen Ihres Unternehmens anzeigen können.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 8571d86e1ce9dc894e54fe72dea75b9f8fe84f0b
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 6%

---

# [!UICONTROL Dashboard „Ziele“]

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu den aktiven Zielen Ihres Unternehmens anzeigen können, wie sie in einer täglichen Momentaufnahme erfasst werden. In diesem Handbuch wird beschrieben, wie Sie in der Benutzeroberfläche auf das Ziel-Dashboard zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Metriken.

Eine Übersicht über Ziele sowie einen Katalog aller in der Experience Platform verfügbaren Ziele finden Sie im [Dokumentation zu Zielen](../../destinations/home.md).

## [!UICONTROL Ziele] Dashboard-Daten {#destinations-dashboard-data}

Die [!UICONTROL Ziele] Dashboard zeigt eine Momentaufnahme der Ziele an, die Ihr Unternehmen in Experience Platform aktiviert hat. Der Schnappschuss zeigt die Daten exakt so an, wie sie zum Zeitpunkt der Schnappschussaufnahme aufgetreten sind. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Ziel-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Dashboard &quot;Ziele&quot;durchsuchen

Um in der Platform-Benutzeroberfläche zum Ziel-Dashboard zu navigieren, wählen Sie **[!UICONTROL Ziele]** Wählen Sie in der linken Leiste die **[!UICONTROL Übersicht]** zum Anzeigen des Dashboards.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Experience Platform ist und noch keine aktiven Ziele hat, wird die [!UICONTROL Ziele] Dashboard und [!UICONTROL Übersicht] nicht sichtbar sind. Wählen Sie stattdessen [!UICONTROL Ziele] über die linke Navigation zeigt die [!UICONTROL Katalog] Registerkarte. Weitere Informationen zum [!UICONTROL Katalog] Registerkarte, siehe [[!UICONTROL Ziele] Arbeitsbereichshandbuch](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### Ändern des Ziel-Dashboards

Sie können das Erscheinungsbild des Ziel-Dashboards durch Auswahl von **[!UICONTROL Dashboard ändern]**. Dadurch können Sie Widgets aus dem Dashboard verschieben, hinzufügen und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** , um verfügbare Widgets zu erkunden und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie unter [Ändern von Dashboards](../customize/modify.md) und [Übersicht über Widget-Bibliotheken](../customize/widget-library.md) Dokumentation .

## Standard-Widgets

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Zielen visualisieren können. Sie können auch benutzerdefinierte Widgets erstellen, die für Ihre Organisation freigegeben werden, indem Sie die [!UICONTROL Widget-Bibliothek]. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst den Abschnitt [Übersicht über Widget-Bibliotheken](../customize/widget-library.md).

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Am häufigsten verwendete Ziele]](#most-used-destinations)
* [[!UICONTROL Kürzlich erstellte Ziele]](#recently-created-destinations)
* [[!UICONTROL Kürzlich aktivierte Segmente]](#recently-activated-segments)

### [!UICONTROL Am häufigsten verwendete Ziele] {#most-used-destinations}

Die **[!UICONTROL Am häufigsten verwendete Ziele]** -Widget zeigt die wichtigsten Ziele Ihres Unternehmens nach der Anzahl der zugeordneten Segmente ab dem letzten Schnappschuss an. Dieses Ranking bietet Einblicke, welche Ziele verwendet werden, und zeigt möglicherweise auch diejenigen, die möglicherweise nicht genutzt werden.

Wenn Sie beispielsweise gestern ein Ziel konfiguriert haben, ihm jedoch keine Segmente zugeordnet haben, können Sie sehen, dass das Ziel derzeit nicht genutzt wird.

Die Anzahl der zugeordneten Segmente, die in der Spalte mit der Segmentanzahl angezeigt werden, ist ab der letzten täglichen Momentaufnahme korrekt. Wenn Sie ein neues Segment dem Ziel zuordnen, wird die Anzahl erst aktualisiert, wenn der nächste Schnappschuss erstellt wurde.

Wenn Sie den Namen eines Ziels aus der im Widget angezeigten Liste auswählen, gelangen Sie zu den Zieldetails, die über das **[!UICONTROL Durchsuchen]** Registerkarte. Sie können auch **[!UICONTROL Alle anzeigen]** , um zur **[!UICONTROL Durchsuchen]** und wählen Sie dann den Namen eines Ziels aus, um dessen Details anzuzeigen.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Kürzlich erstellte Ziele] {#recently-created-destinations}

Die **[!UICONTROL Kürzlich erstellte Ziele]** -Widget können Sie eine Liste der zuletzt konfigurierten Ziele Ihres Unternehmens anzeigen.

Das angezeigte Erstellungsdatum entspricht der letzten täglichen Momentaufnahme. Mit anderen Worten: Wenn Sie ein neues Ziel erstellen, wird es erst nach dem nächsten Schnappschuss in der Liste angezeigt.

Wenn Sie den Namen eines Ziels aus der im Widget angezeigten Liste auswählen, gelangen Sie zu den Zieldetails, die über das **[!UICONTROL Durchsuchen]** Registerkarte. Sie können auch **[!UICONTROL Alle anzeigen]** , um zur **[!UICONTROL Durchsuchen]** und wählen Sie dann den Namen eines Ziels aus, um dessen Details anzuzeigen.

Weitere Informationen zum Konfigurieren bestimmter Zieltypen finden Sie unter [Dokumentation zu Zielen](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Kürzlich aktivierte Segmente] {#recently-activated-segments}

Die **[!UICONTROL Kürzlich aktivierte Segmente]** -Widget stellt eine Liste der Segmente bereit, die einem Ziel zuletzt zugeordnet wurden. Diese Liste zeigt, welche Segmente und Ziele aktiv im System verwendet werden, und kann bei der Fehlerbehebung bei fehlerhaften Zuordnungen helfen.

Das angezeigte aktualisierte Datum zeigt an, wann das Segment zuletzt für das Ziel aktiviert wurde, und ist für den letzten täglichen Schnappschuss korrekt. Wenn Sie also ein Segment für das Ziel aktivieren, ändert sich das aktualisierte Datum erst, nachdem der nächste Schnappschuss erstellt wurde.

Wenn Sie den Namen eines Segments aus der im Widget angezeigten Liste auswählen, gelangen Sie zu den Segmentdetails. Sie können auch **[!UICONTROL Alle anzeigen]** , um zur Registerkarte &quot;Segmentsuche&quot;zu navigieren und dann den Namen eines Segments auszuwählen, um dessen Details anzuzeigen.

Weitere Informationen zum Arbeiten mit Segmenten in Experience Platform erhalten Sie im Abschnitt [Übersicht über den Segmentierungsdienst](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, das Ziel-Dashboard zu finden und die in den verfügbaren Widgets angezeigten Metriken zu verstehen. Weitere Informationen zum Arbeiten mit Zielen in Experience Platform finden Sie im Abschnitt [Dokumentation zu Zielen](../../destinations/home.md).
