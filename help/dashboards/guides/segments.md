---
keywords: Experience Platform; Profil; Segment; Segmente; Segmentierung; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Segmentdashboard; Dashboard
title: Segmente-Dashboard
description: 'Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu Segmenten anzeigen können, die Ihr Unternehmen erstellt hat. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 41ef7a6e6d3b0ee9afe762b19c8c286ceb361dbb
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 6%

---

# Segmente-Dashboard {#segment-dashboard}

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu Ihren Segmenten anzeigen können, die während einer täglichen Momentaufnahme erfasst werden. In diesem Handbuch wird beschrieben, wie Sie in der Benutzeroberfläche auf das Segment-Dashboard zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Einen Überblick über alle Adobe Experience Platform Segmentation Service-Funktionen in der Platform-Benutzeroberfläche finden Sie im Handbuch [Segmentation Service UI Guide](../../segmentation/ui/overview.md).

## Dashboard-Daten des Segments

Das Segment-Dashboard zeigt eine Momentaufnahme der Attributdaten (Datensatzdaten) an, die Ihr Unternehmen im Profilspeicher in der Experience Platform hat. Der Schnappschuss enthält keine Ereignisdaten (Zeitreihendaten).

Die Attributdaten im Snapshot zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem die Momentaufnahme erstellt wurde. Mit anderen Worten, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Segment-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Segmente-Dashboard durchsuchen

Um in der Platform-Benutzeroberfläche zum Dashboard [!UICONTROL Segmente] zu navigieren, wählen Sie in der linken Leiste **[!UICONTROL Segmente]** und dann die Registerkarte **[!UICONTROL Übersicht]** aus, um das Dashboard anzuzeigen.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt wurden, ist das Dashboard [!UICONTROL Segmente] nicht sichtbar. Stattdessen zeigt der Tab [!UICONTROL Übersicht] Links und Dokumentation an, die Ihnen bei den ersten Schritten mit der Segmentierung helfen.

![](../images/segments/dashboard-overview.png)

### Ändern des Dashboards [!UICONTROL Segmente]

Sie können das Erscheinungsbild des Dashboards [!UICONTROL Segmente] ändern, indem Sie **[!UICONTROL Dashboard ändern]** auswählen. Dadurch können Sie Widgets aus dem Dashboard verschieben, hinzufügen und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** zugreifen, um verfügbare Widgets zu untersuchen und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie in der Dokumentation [Dashboards ändern](../customize/modify.md) und [Widget-Bibliothek - Übersicht](../customize/widget-library.md) .

## Segment auswählen

Das Dashboard wählt automatisch ein anzuzeigendes Segment aus. Sie können das Segment jedoch über das Dropdown-Menü oder die Segmentauswahl ändern.

Um ein anderes Segment auszuwählen, wählen Sie die Dropdown-Liste neben dem Segmentnamen aus oder öffnen Sie mit der Segmentauswahl das Dialogfeld für die Segmentauswahl.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widgets und Metriken

Das Segmente-Dashboard besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihrem ausgewählten Segment enthalten.

Das Datum und die Uhrzeit der letzten Aktualisierung eines Widgets zeigen an, wann die letzte Momentaufnahme der Daten erstellt wurde. Datum und Uhrzeit der Momentaufnahme werden in UTC angegeben. Es befindet sich nicht in der Zeitzone des einzelnen Benutzers oder der IMS-Organisation.

![](../images/segments/widget-timestamp.png)

## Standard-Widgets

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Segmenten visualisieren können. Sie können auch benutzerdefinierte Widgets erstellen, die für Ihre Organisation freigegeben werden, indem Sie die [!UICONTROL Widget-Bibliothek] verwenden. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst die [Übersicht über die Widget-Bibliothek](../customize/widget-library.md).

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Zielgruppengröße]](#audience-size)
* [[!UICONTROL Zielgruppengrößentrend]](#audience-size-trend)
* [[!UICONTROL Identitätsüberschneidung]](#identity-overlap)
* [[!UICONTROL Profile nach Identität]](#profiles-by-identity)

### [!UICONTROL Zielgruppengröße] {#audience-size}

Das Widget **[!UICONTROL Zielgruppengröße]** zeigt die Gesamtzahl der zusammengeführten Profile innerhalb des ausgewählten Segments zum Zeitpunkt der Momentaufnahme an. Diese Zahl ist das Ergebnis der Anwendung der Segmentzusammenführungsrichtlinie auf Ihre Profildaten, um Profilfragmente zu einem einzigen Profil für jede Person im Segment zusammenzuführen.

Weitere Informationen zu Fragmenten und zusammengeführten Profilen finden Sie in der [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Zielgruppengrößentrend] {#audience-size-trend}

Das Widget **[!UICONTROL Zielgruppengrößentrend]** liefert Informationen zur Gesamtanzahl der Profile im Segment, die während der täglichen Momentaufnahme für die letzten 30 Tage, 90 Tage oder 12 Monate erfasst wurden. Dieses Widget zeigt an, wie sich die Segmentgröße im Laufe der Zeit verändert haben kann, wenn sich neue Profile für das Segment qualifizieren oder es verlassen.

Weiterführende Informationen zur Segmentbewertung und zur Qualifizierung und Ausstieg von Profilen finden Sie in der [Dokumentation zum Segmentation Service](../../segmentation/home.md).

![](../images/segments/audience-size-trend.png)

### [!UICONTROL Identitätsüberschneidung] {#identity-overlap}

Das Widget **[!UICONTROL Identitätsüberschneidung]** zeigt ein Venn-Diagramm oder Set-Diagramm an, das die Überschneidung von Profilen in Ihrem Segment mit mehreren Identitäten anzeigt.

Nachdem Sie die zu vergleichenden Identitäten mithilfe der Dropdown-Menüs im Widget ausgewählt haben, werden Kreise angezeigt, die die relative Größe jeder Identität anzeigen. Die Anzahl der Profile, die beide Namespaces enthalten, wird durch die Größe der Überschneidung zwischen den Kreisen dargestellt.

Wenn ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Identitäten zugeordnet. Daher ist es wahrscheinlich, dass Ihr Unternehmen über mehrere Profile verfügt, die Fragmente aus mehr als einer Identität enthalten.

Weitere Informationen zu Identitäten finden Sie in der Dokumentation zum Adobe Experience Platform Identity Service](../../identity-service/home.md).[

![](../images/segments/identity-overlap.png)

### [!UICONTROL Profile nach Identität] {#profiles-by-identity}

Das Widget **[!UICONTROL Profile nach Identität]** zeigt die Aufschlüsselung der Identitäten für alle zusammengeführten Profile in Ihrem ausgewählten Segment an. Die Gesamtzahl der Profile nach Identität kann höher sein als die Gesamtzahl der Profile im Segment, da einem Profil mehrere Identitäten zugeordnet sein können. Das heißt, dass das Addieren der für jede Identität angezeigten Werte mehr als die gesamte Zielgruppengröße im Segment ausmacht, da bei der Interaktion eines Kunden mit Ihrer Marke auf mehr als einem Kanal mehrere Identitäten mit diesem einzelnen Kunden verknüpft werden können.

Weitere Informationen zu Identitäten finden Sie in der Dokumentation zum Adobe Experience Platform Identity Service](../../identity-service/home.md).[

![](../images/segments/profiles-by-identity.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, das Segment-Dashboard zu finden und ein anzuzeigendes Segment auszuwählen. Sie sollten auch die Metriken verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Segmenten in der Experience Platform-Benutzeroberfläche finden Sie im Handbuch [Segmentation Service UI guide](../../segmentation/ui/overview.md).
