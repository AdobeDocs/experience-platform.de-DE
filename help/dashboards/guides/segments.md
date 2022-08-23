---
keywords: Experience Platform; Profil; Segment; Segmente; Segmentierung; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Segmentdashboard; Dashboard
title: Dashboard-Anleitung für Segmente
description: 'Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu Segmenten anzeigen können, die Ihr Unternehmen erstellt hat. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: e59ba2e83808b460016805997580dc16c4cd369e
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 11%

---

# Segment-Dashboard {#segment-dashboard}

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

Datum und Uhrzeit der letzten Momentaufnahme werden oben im [!UICONTROL Übersicht] neben dem Dropdown-Menü &quot;Segment&quot;ein. Alle Widget-Daten sind ab diesem Datum und dieser Uhrzeit korrekt. Der Zeitstempel der Momentaufnahme wird in UTC bereitgestellt. Es befindet sich nicht in der Zeitzone des einzelnen Benutzers oder der Organisation.

![Die Registerkarte Segmentübersicht mit einem Widget-Zeitstempel hervorgehoben.](../images/segments/widget-timestamp.png)

## Standard-Widgets {#standard-widgets}

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Segmenten visualisieren können. Sie können auch benutzerdefinierte Widgets erstellen, die für Ihre Organisation freigegeben werden, indem Sie die [!UICONTROL Widget-Bibliothek]. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst den Abschnitt [Übersicht über die Widget-Bibliothek](../customize/widget-library.md).

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Zielgruppengröße]](#audience-size)
* [[!UICONTROL Zielgruppenaktivierungs-Reihenfolge]](#audience-activation-order)
* [[!UICONTROL Trend der Zielgruppengröße]](#audience-size-trend)
* [[!UICONTROL Trend bei der Änderung der Zielgruppengröße]](#audience-size-change-trend)
* [[!UICONTROL Trend der Zielgruppengröße nach Identität]](#audience-size-trend-by-identity)
* [[!UICONTROL Zielgruppenüberschneidung]](#audience-overlap)
* [[!UICONTROL Identitätsüberschneidung]](#identity-overlap)
* [[!UICONTROL Profile nach Identität]](#profiles-by-identity)

### [!UICONTROL Zielgruppengröße] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Zielgruppengröße"
>abstract="Dieses Widget zeigt die Gesamtzahl der zusammengeführten Profile innerhalb des ausgewählten Segments an. Diese Zahl hängt von der auf Ihre Daten angewendeten Zusammenführungsrichtlinie ab und ist zum Zeitpunkt der letzten Momentaufnahme korrekt."

Die **[!UICONTROL Zielgruppengröße]** Widget zeigt die Gesamtzahl der zusammengeführten Profile innerhalb des ausgewählten Segments zum Zeitpunkt der Momentaufnahme an. Diese Zahl ist das Ergebnis der Anwendung der Segmentzusammenführungsrichtlinie auf Ihre Profildaten, um Profilfragmente zu einem einzigen Profil für jede Person im Segment zusammenzuführen.

Weitere Informationen zu Fragmenten und zusammengeführten Profilen erhalten Sie im Abschnitt [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

![](../images/segments/audience-size.png)

### [!UICONTROL Trend der Zielgruppengröße] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Trend der Zielgruppengröße"
>abstract="Dieses Widget enthält Informationen zur Gesamtanzahl der Profile, die den Kriterien von **any** Segmentdefinition, die während der täglichen Momentaufnahme für die letzten 30 Tage, 90 Tage oder 12 Monate erfasst wurde."

Die **[!UICONTROL Zielgruppengrößentrend]** Widget bietet eine Kantengraph-Illustration für die Gesamtzahl der Profile, die den Kriterien von **any** Segmentdefinition über einen bestimmten Zeitraum. Der Trend zur Zielgruppengröße kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Zielgruppengröße wird auf der Y-Achse und der Zeit auf der X-Achse dargestellt.

Dieses Widget enthält auch die automatische [!UICONTROL Untertitel] Funktion, bei der ein maschinelles Lernmodell die Diagramm- und Segmentdaten analysiert und automatisch Beschriftungen generiert, um die wichtigsten Trends und Ereignisse zu beschreiben. Auswählen **[!UICONTROL Untertitel]** , um das Dialogfeld mit den automatischen Beschriftungen zu öffnen.

![In der Segmentübersicht wird das Trend-Widget zur Zielgruppengröße angezeigt.](../images/segments/audience-size-trend-captions.png)

Das Dialogfeld für automatische Beschriftungen wird geöffnet und bietet Einblicke in Ihre Daten.

![Das Dialogfeld für automatische Beschriftungen für das Trend-Widget zur Zielgruppengröße.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

Weiterführende Informationen zur Segmentauswertung und zur Qualifizierung und Ausstieg von Profilen finden Sie im Abschnitt [Dokumentation zum Segmentierungsdienst](../../segmentation/home.md).

### [!UICONTROL Trend bei der Änderung der Zielgruppengröße] {#audience-size-change-trend}

Dieses Widget bietet ein Liniendiagramm, das die Differenz der Gesamtzahl der Profile anzeigt, die sich im Zeitraum zwischen den jüngsten täglichen Snapshots für ein bestimmtes Segment qualifiziert haben. Das für die Analyse ausgewählte Segment wird aus der Dropdown-Liste Übersicht ausgewählt. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Zielgruppengröße wird auf der Y-Achse und der Zeit auf der X-Achse dargestellt.

![Das Widget zur Zielgruppengröße ändert den Trend.](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Trend der Zielgruppengröße nach Identität] {#audience-size-trend-by-identity}

Dieses Widget veranschaulicht den Trend zur Zielgruppengröße für ein bestimmtes Segment basierend auf dem Identitätstyp, der im Widget-Dropdown-Menü ausgewählt wurde. Das für die Analyse verwendete Segment wird aus der Dropdown-Liste Übersicht ausgewählt. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt.

![Der Trend zur Zielgruppengröße nach Identitäts-Widget.](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL Zielgruppenaktivierungs-Reihenfolge] {#audience-activation-order}

Die [!UICONTROL Aktivierungsreihenfolge für Zielgruppen] Widget bietet eine Tabelle mit drei Spalten, in der die [!UICONTROL Zielname], die [!UICONTROL platform]und der Aktivierung [!UICONTROL date] der Audience. Die Liste ist von oben nach unten geordnet, entsprechend der Neuigkeit, und kann bis zu 10 Zeilen aufnehmen.

![Das Widget zur Zielgruppenaktivierungsreihenfolge .](../images/segments/audience-activation-order.png)

### [!UICONTROL Zielgruppenüberschneidung] {#audience-overlap}

Dieses Widget stellt die Anzahl der Profile aus zwei Segmenten dar, die die Kriterien für beide Segmentdefinitionen erfüllen. Die zum Vergleich verwendeten Segmente werden aus den Widget-Dropdown-Menüs ausgewählt. Die Gesamtzahl der in der relevanten Segmentdefinition enthaltenen Profile kann durch Bewegen des Mauszeigers über einen Kreis oder die Schnittmenge des Venn-Diagramms angezeigt werden.

Mit diesem Widget können Sie Ihre Segmentierungsstrategie optimieren, indem Sie die Ähnlichkeiten in den Ergebnissen Ihrer Segmentdefinitionen visualisieren.

![Das Widget Zielgruppenüberschneidung .](../images/segments/audience-overlap.png)

<!-- * [[!UICONTROL Audience overlap report]](#audience-overlap-report) -->
<!-- ### [!UICONTROL Audience overlap report] {#audience-overlap-report} -->

<!-- View an ordered list of audiences by Highest or Lowest overlap percentages. -->

<!-- ![The Audience overlap report widget.]() -->

<!-- https://jira.corp.adobe.com/browse/PLAT-125511 -->

### [!UICONTROL Identitätsüberschneidung] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Identitätsüberschneidung"
>abstract="Dieses Widget zeigt die Überschneidung von Profilen in Ihrem Segment, die beide ausgewählte Identitäten enthalten. Die Kreise zeigen die relative Größe jeder Identität an. Die Anzahl der Profile, die beide Namespaces enthalten, wird durch die Überlappung der Kreise dargestellt."

Die **[!UICONTROL Identitätsüberschneidung]** -Widget zeigt ein Venn-Diagramm oder ein Set-Diagramm an, das die Überschneidung von Profilen in Ihrem Segment mit mehreren Identitäten anzeigt.

Verwenden Sie die Dropdown-Menüs im Widget, um die Identitäten auszuwählen, die Sie vergleichen möchten. Die Kreise zeigen die relative Größe jeder ausgewählten Identität an, wobei die Anzahl der Profile, die beide Namespaces enthalten, durch die Größe der Überschneidung zwischen den Kreisen dargestellt wird.

Wenn ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Identitäten zugeordnet. Daher ist es wahrscheinlich, dass Ihr Unternehmen über mehrere Profile verfügt, die Fragmente aus mehr als einer Identität enthalten.

Weitere Informationen zu Identitäten finden Sie unter [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Profile nach Identität] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profile nach Identität"
>abstract="Dieses Widget zeigt die Aufschlüsselung der Identitäten für jedes zusammengeführte Profil in Ihrem ausgewählten Segment an."

Die **[!UICONTROL Profile nach Identität]** Widget zeigt die Aufschlüsselung der Identitäten für jedes zusammengeführte Profil in Ihrem ausgewählten Segment an. Die Gesamtzahl der Profile nach Identität kann höher sein als die Gesamtzahl der Profile im Segment, da einem Profil mehrere Identitäten zugeordnet sein können. Das heißt, dass das Addieren der für jede Identität angezeigten Werte mehr als die gesamte Zielgruppengröße im Segment ausmacht, da bei der Interaktion eines Kunden mit Ihrer Marke auf mehr als einem Kanal mehrere Identitäten mit diesem einzelnen Kunden verknüpft werden können.

Auswählen **[!UICONTROL Untertitel]** , um das Dialogfeld mit den automatischen Beschriftungen zu öffnen.

![Die Profile nach Identitätsbeschriftungen.](../images/segments/profiles-by-identity.png)

Ein maschinelles Lernmodell generiert automatisch Dateneinblicke, indem es die Gesamtverteilung und die Schlüsseldimensionen der Daten analysiert.

Weitere Informationen zu Identitäten finden Sie unter [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, das Segment-Dashboard zu finden und ein anzuzeigendes Segment auszuwählen. Sie sollten auch die Metriken verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Segmenten in der Experience Platform-Benutzeroberfläche finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche des Segmentierungsdienstes](../../segmentation/ui/overview.md).
