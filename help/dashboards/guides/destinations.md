---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Profil-Dashboard; Dashboard
title: Dashboard "Ziele"
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu den aktiven Zielen Ihres Unternehmens anzeigen können.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 41ef7a6e6d3b0ee9afe762b19c8c286ceb361dbb
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 5%

---

#  Ziel-Dashboard

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu den aktiven Zielen Ihres Unternehmens anzeigen können, wie sie in einer täglichen Momentaufnahme erfasst werden. In diesem Handbuch wird beschrieben, wie Sie in der Benutzeroberfläche auf das Ziel-Dashboard zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Metriken.

Eine Übersicht über Ziele sowie einen Katalog aller in Experience Platform verfügbaren Ziele finden Sie in der [Dokumentation zu Zielen](../../destinations/home.md).

##  Dashboard-Zieldaten {#destinations-dashboard-data}

Das Dashboard [!UICONTROL Ziele] zeigt eine Momentaufnahme der Ziele an, die Ihr Unternehmen in Experience Profile aktiviert hat. Der Schnappschuss zeigt die Daten exakt so an, wie sie zum Zeitpunkt der Schnappschussaufnahme aufgetreten sind. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Ziel-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Dashboard &quot;Ziele&quot;durchsuchen

Um in der Benutzeroberfläche von Platform zum Dashboard für Ziele zu navigieren, wählen Sie in der linken Leiste **[!UICONTROL Ziele]** und dann die Registerkarte **[!UICONTROL Übersicht]** aus, um das Dashboard anzuzeigen.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu in Experience Platform ist und noch keine aktiven Ziele hat, sind die Registerkarten [!UICONTROL Ziele] und [!UICONTROL Übersicht] nicht sichtbar. Wenn Sie stattdessen [!UICONTROL Ziele] aus der linken Navigation auswählen, wird die Registerkarte [!UICONTROL Katalog] angezeigt. Weitere Informationen zum Tab [!UICONTROL Katalog] finden Sie im [[!UICONTROL Ziele] Workspace-Handbuch](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### Ändern des Ziel-Dashboards

Sie können das Erscheinungsbild des Ziel-Dashboards ändern, indem Sie **[!UICONTROL Dashboard ändern]** auswählen. Dadurch können Sie Widgets aus dem Dashboard verschieben, hinzufügen und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** zugreifen, um verfügbare Widgets zu untersuchen und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie in der Dokumentation [Dashboards ändern](../customize/modify.md) und [Widget-Bibliothek - Übersicht](../customize/widget-library.md) .

## Standard-Widgets

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Zielen visualisieren können. Sie können auch benutzerdefinierte Widgets erstellen, die für Ihre Organisation freigegeben werden, indem Sie die [!UICONTROL Widget-Bibliothek] verwenden. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst die [Übersicht über die Widget-Bibliothek](../customize/widget-library.md).

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Am häufigsten verwendete Ziele]](#most-used-destinations)
* [[!UICONTROL Kürzlich erstellte Ziele]](#recently-created-destinations)
* [[!UICONTROL Kürzlich aktivierte Segmente]](#recently-activated-segments)

### [!UICONTROL Am häufigsten verwendete Ziele] {#most-used-destinations}

Das Widget **[!UICONTROL Am häufigsten verwendete Ziele]** zeigt die Top-Ziele Ihres Unternehmens nach der Anzahl der zugeordneten Segmente ab dem letzten Schnappschuss an. Dieses Ranking bietet Einblicke, welche Ziele verwendet werden, und zeigt möglicherweise auch diejenigen, die möglicherweise nicht genutzt werden.

Wenn Sie beispielsweise gestern ein Ziel konfiguriert haben, ihm jedoch keine Segmente zugeordnet haben, können Sie sehen, dass das Ziel derzeit nicht genutzt wird.

Die Anzahl der zugeordneten Segmente, die in der Spalte mit der Segmentanzahl angezeigt werden, ist ab der letzten täglichen Momentaufnahme korrekt. Wenn Sie ein neues Segment dem Ziel zuordnen, wird die Anzahl erst aktualisiert, wenn der nächste Schnappschuss erstellt wurde.

Wenn Sie den Namen eines Ziels aus der Liste auswählen, die im Widget angezeigt wird, gelangen Sie zu den Zieldetails, die über den Tab **[!UICONTROL Durchsuchen]** verknüpft sind. Sie können auch **[!UICONTROL Alle anzeigen]** auswählen, um zur Registerkarte **[!UICONTROL Durchsuchen]** zu navigieren, und dann den Namen eines Ziels auswählen, um dessen Details anzuzeigen.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Kürzlich erstellte Ziele] {#recently-created-destinations}

Das Widget **[!UICONTROL Kürzlich erstellte Ziele]** ermöglicht es Ihnen, eine Liste der zuletzt konfigurierten Ziele Ihres Unternehmens anzuzeigen.

Das angezeigte Erstellungsdatum entspricht der letzten täglichen Momentaufnahme. Mit anderen Worten: Wenn Sie ein neues Ziel erstellen, wird es erst nach dem nächsten Schnappschuss in der Liste angezeigt.

Wenn Sie den Namen eines Ziels aus der Liste auswählen, die im Widget angezeigt wird, gelangen Sie zu den Zieldetails, die über den Tab **[!UICONTROL Durchsuchen]** verknüpft sind. Sie können auch **[!UICONTROL Alle anzeigen]** auswählen, um zur Registerkarte **[!UICONTROL Durchsuchen]** zu navigieren, und dann den Namen eines Ziels auswählen, um dessen Details anzuzeigen.

Weitere Informationen zum Konfigurieren bestimmter Zieltypen finden Sie in der [Dokumentation zu Zielen](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Kürzlich aktivierte Segmente] {#recently-activated-segments}

Das Widget **[!UICONTROL Kürzlich aktivierte Segmente]** enthält eine Liste der Segmente, die einem Ziel zuletzt zugeordnet wurden. Diese Liste zeigt, welche Segmente und Ziele aktiv im System verwendet werden, und kann bei der Fehlerbehebung bei fehlerhaften Zuordnungen helfen.

Das angezeigte aktualisierte Datum zeigt an, wann das Segment zuletzt für das Ziel aktiviert wurde, und ist für den letzten täglichen Schnappschuss korrekt. Wenn Sie also ein Segment für das Ziel aktivieren, ändert sich das aktualisierte Datum erst, nachdem der nächste Schnappschuss erstellt wurde.

Wenn Sie den Namen eines Segments aus der im Widget angezeigten Liste auswählen, gelangen Sie zu den Segmentdetails. Sie können auch **[!UICONTROL Alle anzeigen]** auswählen, um zur Registerkarte &quot;Segmentsuche&quot;zu navigieren und dann den Namen eines Segments auszuwählen, um dessen Details anzuzeigen.

Weitere Informationen zum Arbeiten mit Segmenten in Experience Platform finden Sie in der [Segmentation Service - Übersicht](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, das Ziel-Dashboard zu finden und die in den verfügbaren Widgets angezeigten Metriken zu verstehen. Weitere Informationen zum Arbeiten mit Zielen in Experience Platform finden Sie in der [Dokumentation zu Zielen](../../destinations/home.md).
