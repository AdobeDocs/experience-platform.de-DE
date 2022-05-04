---
keywords: Experience Platform; Profil; Segment; Segmente; Segmentierung; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Segmentdashboard; Dashboard
title: Segmente-Dashboard
description: 'Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu Segmenten anzeigen können, die Ihr Unternehmen erstellt hat. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: b4cd7bc0d8c038346aacdda7c4c9def12864065c
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 5%

---

# Segmente-Dashboard {#segment-dashboard}

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu Ihren Segmenten anzeigen können, die während einer täglichen Momentaufnahme erfasst werden. In diesem Handbuch wird beschrieben, wie Sie in der Benutzeroberfläche auf das Segment-Dashboard zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Einen Überblick über alle Funktionen des Adobe Experience Platform Segmentation Service in der Benutzeroberfläche von Platform erhalten Sie im [Handbuch zur Benutzeroberfläche des Segmentierungsdienstes](../../segmentation/ui/overview.md).

## Dashboard-Daten des Segments

Das Segment-Dashboard zeigt eine Momentaufnahme der Attributdaten (Datensatzdaten) an, die Ihr Unternehmen im Profilspeicher in der Experience Platform hat. Der Schnappschuss enthält keine Ereignisdaten (Zeitreihendaten).

Die Attributdaten im Snapshot zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem die Momentaufnahme erstellt wurde. Mit anderen Worten, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Segment-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Segmente-Dashboard durchsuchen

So navigieren Sie zum [!UICONTROL Segmente] Dashboard in der Platform-Benutzeroberfläche auswählen **[!UICONTROL Segmente]** Wählen Sie in der linken Leiste die **[!UICONTROL Übersicht]** zum Anzeigen des Dashboards.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt wurden, wird die [!UICONTROL Segmente] Das Dashboard ist nicht sichtbar. Stattdessen wird die [!UICONTROL Übersicht] enthält Links und Dokumentation, die Ihnen bei den ersten Schritten mit der Segmentierung helfen.

![](../images/segments/dashboard-overview.png)

### Ändern der [!UICONTROL Segmente] Dashboard

Sie können das Erscheinungsbild der [!UICONTROL Segmente] Dashboard durch Auswahl von **[!UICONTROL Dashboard ändern]**. Dadurch können Sie Widgets aus dem Dashboard verschieben, hinzufügen und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** , um verfügbare Widgets zu erkunden und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie unter [Ändern von Dashboards](../customize/modify.md) und [Übersicht über die Widget-Bibliothek](../customize/widget-library.md) Dokumentation .

## Segment auswählen

Das Dashboard wählt automatisch ein anzuzeigendes Segment aus. Sie können das Segment jedoch über das Dropdown-Menü oder die Segmentauswahl ändern.

Um ein anderes Segment auszuwählen, wählen Sie das Dropdown-Menü neben dem Segmentnamen aus oder verwenden Sie die Segmentauswahl, um das Dialogfeld für die Segmentauswahl zu öffnen.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widgets und Metriken

Das Segmente-Dashboard besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihrem ausgewählten Segment enthalten.

Das Datum und die Uhrzeit der letzten Aktualisierung eines Widgets zeigen an, wann die letzte Momentaufnahme der Daten erstellt wurde. Datum und Uhrzeit der Momentaufnahme werden in UTC angegeben. Es befindet sich nicht in der Zeitzone des einzelnen Benutzers oder der IMS-Organisation.

![](../images/segments/widget-timestamp.png)

## Standard-Widgets

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Segmenten visualisieren können. Sie können auch benutzerdefinierte Widgets erstellen, die für Ihre Organisation freigegeben werden, indem Sie die [!UICONTROL Widget-Bibliothek]. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst den Abschnitt [Übersicht über die Widget-Bibliothek](../customize/widget-library.md).

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Zielgruppengröße]](#audience-size)
* [[!UICONTROL Identitätsüberschneidung]](#identity-overlap)
* [[!UICONTROL Profile nach Identität]](#profiles-by-identity)
* [[!UICONTROL Aktivierungsreihenfolge für Zielgruppen]](#audience-activation-order)
* [[!UICONTROL Zielgruppengrößentrend]](#audience-size-trend)
* [[!UICONTROL Trend zur Änderung der Zielgruppengröße]](#audience-size-change-trend)
* [[!UICONTROL Trend zur Zielgruppengröße nach Identität]](#audience-size-trend-by-identity)

### [!UICONTROL Zielgruppengröße] {#audience-size}

Die **[!UICONTROL Zielgruppengröße]** Widget zeigt die Gesamtzahl der zusammengeführten Profile innerhalb des ausgewählten Segments zum Zeitpunkt der Momentaufnahme an. Diese Zahl ist das Ergebnis der Anwendung der Segmentzusammenführungsrichtlinie auf Ihre Profildaten, um Profilfragmente zu einem einzigen Profil für jede Person im Segment zusammenzuführen.

Weitere Informationen zu Fragmenten und zusammengeführten Profilen erhalten Sie im Abschnitt [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Identitätsüberschneidung] {#identity-overlap}

Die **[!UICONTROL Identitätsüberschneidung]** -Widget zeigt ein Venn-Diagramm oder ein Set-Diagramm an, das die Überschneidung von Profilen in Ihrem Segment mit mehreren Identitäten anzeigt.

Nachdem Sie die zu vergleichenden Identitäten mithilfe der Dropdown-Menüs im Widget ausgewählt haben, werden Kreise angezeigt, die die relative Größe jeder Identität anzeigen. Die Anzahl der Profile, die beide Namespaces enthalten, wird durch die Größe der Überschneidung zwischen den Kreisen dargestellt.

Wenn ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Identitäten zugeordnet. Daher ist es wahrscheinlich, dass Ihr Unternehmen über mehrere Profile verfügt, die Fragmente aus mehr als einer Identität enthalten.

Weitere Informationen zu Identitäten finden Sie unter [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Profile nach Identität] {#profiles-by-identity}

Die **[!UICONTROL Profile nach Identität]** -Widget zeigt die Aufschlüsselung der Identitäten über alle zusammengeführten Profile in Ihrem ausgewählten Segment hinweg an. Die Gesamtzahl der Profile nach Identität kann höher sein als die Gesamtzahl der Profile im Segment, da einem Profil mehrere Identitäten zugeordnet sein können. Das heißt, dass das Addieren der für jede Identität angezeigten Werte mehr als die gesamte Zielgruppengröße im Segment ausmacht, da bei der Interaktion eines Kunden mit Ihrer Marke auf mehr als einem Kanal mehrere Identitäten mit diesem einzelnen Kunden verknüpft werden können.

Auswählen **[!UICONTROL Untertitel]** , um das Dialogfeld mit den automatischen Beschriftungen zu öffnen.

![Die Profile nach Identitätsbeschriftungen.](../images/segments/profiles-by-identity.png)

Ein maschinelles Lernmodell generiert automatisch Dateneinblicke, indem es die Gesamtverteilung und die Schlüsseldimensionen der Daten analysiert.

Weitere Informationen zu Identitäten finden Sie unter [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

### [!UICONTROL Aktivierungsreihenfolge für Zielgruppen] {#audience-activation-order}

Die [!UICONTROL Aktivierungsreihenfolge für Zielgruppen] Widget bietet eine Tabelle mit drei Spalten, in der die [!UICONTROL Zielname], die [!UICONTROL platform]und der Aktivierung [!UICONTROL date] der Audience. Die Liste ist von oben nach unten geordnet, entsprechend der Neuigkeit, und kann bis zu 10 Zeilen aufnehmen.

![Das Widget zur Zielgruppenaktivierungsreihenfolge .](../images/segments/audience-activation-order.png)

### [!UICONTROL Zielgruppengrößentrend] {#audience-size-trend}

Die [!UICONTROL Zielgruppengrößentrend] Widget bietet eine Kantengraph-Illustration für die Gesamtzahl der Profile, die den Kriterien von **any** Segmentdefinition über einen bestimmten Zeitraum. Der Trend zur Zielgruppengröße kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Zielgruppengröße wird auf der Y-Achse und der Zeit auf der X-Achse dargestellt.

![Das Trend-Widget zur Zielgruppengröße .](../images/segments/audience-size-trend.png)

### [!UICONTROL Trend zur Änderung der Zielgruppengröße] {#audience-size-change-trend}

Dieses Widget bietet eine Liniendiagramm, die die Differenz in der Gesamtzahl der Profile anzeigt, die sich für ein bestimmtes Segment zwischen den letzten täglichen Momentaufnahmen qualifiziert haben. Das für die Analyse ausgewählte Segment wird aus der Dropdown-Liste Übersicht ausgewählt. Der Zeitraum der Trendanalyse kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Zielgruppengröße wird auf der Y-Achse und der Zeit auf der X-Achse dargestellt.

![Das Widget zur Zielgruppengröße ändert den Trend.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Trend zur Zielgruppengröße nach Identität] {#audience-size-trend-by-identity}

Dieses Widget veranschaulicht den Trend zur Zielgruppengröße für ein bestimmtes Segment basierend auf dem Identitätstyp, der im Widget-Dropdown-Menü ausgewählt wurde. Das für die Analyse verwendete Segment wird aus der Dropdown-Liste Übersicht ausgewählt. Der Zeitraum der Trendanalyse kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt.

![Der Trend zur Zielgruppengröße nach Identitäts-Widget.](../images/segments/audience-size-trend-by-identity.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, das Segment-Dashboard zu finden und ein anzuzeigendes Segment auszuwählen. Sie sollten auch die Metriken verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Segmenten in der Experience Platform-Benutzeroberfläche finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche des Segmentierungsdienstes](../../segmentation/ui/overview.md).
