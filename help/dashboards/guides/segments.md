---
keywords: Experience Platform; Profil; Segment; Segmente; Segmentierung; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Segmentdashboard; Dashboard
title: Dashboard-Anleitung für Segmente
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu Segmenten anzeigen können, die Ihr Unternehmen erstellt hat.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 23df35d7d90b6674b089a842818dba83283a1646
workflow-type: tm+mt
source-wordcount: '2092'
ht-degree: 9%

---

# [!UICONTROL Segment-Dashboard] {#segment-dashboard}

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu Ihren Segmenten anzeigen können, die während einer täglichen Momentaufnahme erfasst werden. In diesem Handbuch wird beschrieben, wie Sie in der Benutzeroberfläche auf das Segment-Dashboard zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Einen Überblick über alle Funktionen des Adobe Experience Platform Segmentation Service in der Benutzeroberfläche von Platform erhalten Sie im [Handbuch zur Benutzeroberfläche des Segmentierungsdienstes](../../segmentation/ui/overview.md).

## [!UICONTROL Segmente] Dashboard-Daten

Das Segment-Dashboard zeigt eine Momentaufnahme der Attributdaten (Datensatzdaten) an, die Ihr Unternehmen im Profilspeicher in der Experience Platform hat. Der Schnappschuss enthält keine Ereignisdaten (Zeitreihendaten).

Die Attributdaten im Snapshot zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem die Momentaufnahme erstellt wurde. Mit anderen Worten, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten und das Segment-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Die [!UICONTROL Segmente] Dashboard {#explore}

So navigieren Sie zum [!UICONTROL Segmente] Dashboard in der Platform-Benutzeroberfläche auswählen **[!UICONTROL Segmente]** Wählen Sie in der linken Leiste die **[!UICONTROL Übersicht]** zum Anzeigen des Dashboards.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt wurden, wird die [!UICONTROL Segmente] Das Dashboard ist nicht sichtbar. Stattdessen wird die [!UICONTROL Übersicht] enthält Links und Dokumentation, die Ihnen bei den ersten Schritten mit der Segmentierung helfen.

![Die Registerkarte Übersicht des Segmente-Dashboards .](../images/segments/dashboard-overview.png)

### Ändern Sie die [!UICONTROL Segmente] Dashboard {#modify}

Sie können das Erscheinungsbild der [!UICONTROL Segmente] Dashboard durch Auswahl von **[!UICONTROL Dashboard ändern]**. Dadurch können Sie Widgets aus dem Dashboard verschieben, hinzufügen und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** , um verfügbare Widgets zu erkunden und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie unter [Ändern von Dashboards](../customize/modify.md) und [Übersicht über die Widget-Bibliothek](../customize/widget-library.md) Dokumentation .

### Widgets hinzufügen {#add-widget}

Auswählen **[!UICONTROL Widget hinzufügen]** um zur Widget-Bibliothek zu navigieren und eine Liste der verfügbaren Widgets anzuzeigen, die Sie Ihrem Dashboard hinzufügen können.

![Die Übersicht über das Dashboard Segmente mit dem Widget Hinzufügen wurde hervorgehoben.](../images/segments/segments-overview-add-widget.png)

In der Widget-Bibliothek können Sie die Auswahl von standardmäßigen und benutzerdefinierten Segment-Widgets durchsuchen. Informationen zum Hinzufügen von Widgets finden Sie in der Dokumentation zur Widget-Bibliothek . [Widget hinzufügen](../customize/widget-library.md#add-widgets).

## Segment auswählen

Das Dashboard wählt automatisch ein anzuzeigendes Segment aus. Sie können das Segment jedoch über das Dropdown-Menü oder die Segmentauswahl ändern.

Um ein anderes Segment auszuwählen, wählen Sie das Dropdown-Menü neben dem Segmentnamen aus oder verwenden Sie die Segmentauswahl, um das Dialogfeld für die Segmentauswahl zu öffnen.

>[!IMPORTANT]
>
>In der Liste der auswählbaren Segmente werden nur Segmente angezeigt, deren Profilanzahl über null liegt.

![Die Übersicht über das Segmente-Dashboard mit dem Dropdown-Menü für globale Segmente wurde hervorgehoben.](../images/segments/change-segment.png)

![Das Dialogfeld Segment auswählen , in dem alle verfügbaren Segmente angezeigt werden.](../images/segments/select-segment-dialog.png)

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
* [[!UICONTROL Bericht &quot;Zielgruppenüberschneidung&quot;]](#audience-overlap-report)
* [[!UICONTROL Identitätsüberschneidung]](#identity-overlap)
* [[!UICONTROL Profile nach Identität]](#profiles-by-identity)
* [[!UICONTROL Geplante Aktivierungen]](#scheduled-activations)

### [!UICONTROL Zielgruppengröße] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Zielgruppengröße"
>abstract="Dieses Widget zeigt die Gesamtzahl der zusammengeführten Profile innerhalb des ausgewählten Segments an. Diese Zahl hängt von der auf Ihre Daten angewendeten Zusammenführungsrichtlinie ab und ist zum Zeitpunkt der letzten Momentaufnahme korrekt."

Die **[!UICONTROL Zielgruppengröße]** Widget zeigt die Gesamtzahl der zusammengeführten Profile innerhalb des ausgewählten Segments zum Zeitpunkt der Momentaufnahme an. Diese Zahl ist das Ergebnis der Anwendung der Segmentzusammenführungsrichtlinie auf Ihre Profildaten, um Profilfragmente zu einem einzigen Profil für jede Person im Segment zusammenzuführen.

Weitere Informationen zu Fragmenten und zusammengeführten Profilen finden Sie im Abschnitt [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

![Die Übersicht über das Dashboard Segmente mit dem Widget Zielgruppengröße wird hervorgehoben.](../images/segments/audience-size.png)

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

### [!UICONTROL Bericht &quot;Zielgruppenüberschneidung&quot;] {#audience-overlap-report}

Dieses Widget tabellarisiert die Daten zur Zielgruppenüberschneidung für ein bestimmtes Segment. Eine Liste mit fünf Zielgruppen, die von den Prozentsätzen der höchsten bis zur niedrigsten Überschneidung sortiert sind, wird für das Segment bereitgestellt, das oben im Bildschirm aus dem Dropdown-Menü ausgewählt wurde. Aus Gründen der Klarheit wird Ihr ausgewähltes Segment im [!UICONTROL SEGMENT A NAME] Spalte. Die Analyse der Zielgruppenüberschneidung wird für das zweite Segment bereitgestellt, das im [!UICONTROL SEGMENT B NAME] Spalte. Die prozentuale Überschneidung wird in der dritten Spalte genau auf zwölf Dezimalstellen angegeben.

Der Bericht zur Zielgruppenüberschneidung hilft Ihnen beim Erstellen neuer Hochleistungssegmente. Durch die Beobachtung hoher prozentualer Überschneidungen können Sie Zielgruppen unterdrücken und das Senden derselben Zielgruppe an verschiedene Ziele verhindern. Sie helfen Ihnen auch dabei, versteckte Einblicke zu identifizieren, die bei einer besseren Segmentierung hilfreich sein könnten. Eine geringe prozentuale Überschneidung hilft, eindeutige Profile zu finden, die verfolgt werden sollen.

Auswählen **[!UICONTROL Mehr anzeigen]** , um ein Vollbilddialogfeld zu öffnen, das mehr Segmentüberlagerungsdaten enthält.

![Das Berichts-Widget &quot;Zielgruppenüberschneidung&quot;wurde hervorgehoben.](../images/segments/audience-overlap-report.png)

Die [!UICONTROL Bericht &quot;Zielgruppenüberschneidung&quot;] angezeigt. Dieses Dialogfeld kann bis zu 50 Zeilen mit Analysen zur Zielgruppenüberschneidung enthalten, die in sechs Spalten unterteilt sind. Wählen Sie das Einstellungssymbol (![Das Einstellungssymbol.](../images/segments/settings-icon.png)), um Spalten aus der Tabelle zu entfernen oder hinzuzufügen.

![Das Berichtdialogfeld &quot;Zielgruppenüberschneidung&quot;.](../images/segments/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Wählen Sie die **[!UICONTROL Überlappung]** Spaltenüberschrift verwenden, um die Rangfolge der Ergebnisse zwischen der höchsten und der niedrigsten bzw. der niedrigsten der höchsten zu ändern.

Um den gesamten Bericht im PDF-Format herunterzuladen, wählen Sie das Optionsmenü (**`...`**) gefolgt von **[!UICONTROL Download]**.

![Das Berichtdialogfeld Zielgruppenüberschneidung wurde mit den Auslassungszeichen und der Download-Option hervorgehoben.](../images/segments/segments-audience-overlap-report-dialog-download.png)

Wählen Sie eine Zeile aus dem Bericht aus, um ein Venn-Diagramm der Überschneidungsanalyse zu öffnen. Bewegen Sie den Mauszeiger über einen Abschnitt des Venn-Diagramms, um die Profilanzahl in einem Dialogfeld anzuzeigen.

![Das Berichtdialogfeld Zielgruppenüberschneidung wird mit einem Venn-Diagramm und einer hervorgehobenen Zeile angezeigt.](../images/segments/audience-overlap-report-dialog-venn.png)

Auswählen **[!UICONTROL Schließen]** , um zur [!UICONTROL Segmente] Dashboard.

### [!UICONTROL Identitätsüberschneidung] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Identitätsüberschneidung"
>abstract="Dieses Widget zeigt die Überschneidung von Profilen in Ihrem Segment, die beide ausgewählte Identitäten enthalten. Die Kreise zeigen die relative Größe jeder Identität an. Die Anzahl der Profile, die beide Namespaces enthalten, wird durch die Überlappung der Kreise dargestellt."

Die **[!UICONTROL Identitätsüberschneidung]** -Widget zeigt ein Venn-Diagramm oder ein Set-Diagramm an, das die Überschneidung von Profilen in Ihrem Segment mit mehreren Identitäten anzeigt.

Verwenden Sie die Dropdown-Menüs im Widget, um die Identitäten auszuwählen, die Sie vergleichen möchten. Die Kreise zeigen die relative Größe jeder ausgewählten Identität an, wobei die Anzahl der Profile, die beide Namespaces enthalten, durch die Größe der Überschneidung zwischen den Kreisen dargestellt wird.

Wenn ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Identitäten zugeordnet. Daher ist es wahrscheinlich, dass Ihr Unternehmen über mehrere Profile verfügt, die Fragmente aus mehr als einer Identität enthalten.

Weitere Informationen zu Identitäten finden Sie unter [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

![Die Übersicht über das Dashboard &quot;Segmente&quot;mit dem Widget zur Identitätsüberschneidung wurde hervorgehoben.](../images/segments/identity-overlap.png)

### [!UICONTROL Profile nach Identität] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profile nach Identität"
>abstract="Dieses Widget zeigt die Aufschlüsselung der Identitäten für jedes zusammengeführte Profil in Ihrem ausgewählten Segment an."

Die **[!UICONTROL Profile nach Identität]** Widget zeigt die Aufschlüsselung der Identitäten für jedes zusammengeführte Profil in Ihrem ausgewählten Segment an. Die Gesamtzahl der Profile nach Identität kann höher sein als die Gesamtzahl der Profile im Segment, da einem Profil mehrere Identitäten zugeordnet sein können. Das heißt, dass das Addieren der für jede Identität angezeigten Werte mehr als die gesamte Zielgruppengröße im Segment ausmacht, da bei der Interaktion eines Kunden mit Ihrer Marke auf mehr als einem Kanal mehrere Identitäten mit diesem einzelnen Kunden verknüpft werden können.

Auswählen **[!UICONTROL Untertitel]** , um das Dialogfeld mit den automatischen Beschriftungen zu öffnen.

![Das Dialogfeld Profile nach Identitätsbeschriftungen .](../images/segments/profiles-by-identity.png)

Ein maschinelles Lernmodell generiert automatisch Dateneinblicke, indem es die Gesamtverteilung und die Schlüsseldimensionen der Daten analysiert.

Weitere Informationen zu Identitäten finden Sie unter [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

### Geplante Aktivierungen {#scheduled-activations}

Das [!UICONTROL Geplante Aktivierungen]-Widget bietet eine tabellarische Übersicht über die zuletzt aktivierten Ziele. Die Tabelle enthält die Zielplattform, den Namen Ihres Aktivierungsflusses zu diesem Ziel sowie das Start- und Enddatum der Aktivierung für das ausgewählte Segment. Wenn für die Aktivierung kein Enddatum angegeben wurde, wird dies als [!UICONTROL Laufend]. Das zu analysierende Segment wird oben auf der Seite aus dem Dropdown-Menü ausgewählt.

Mit dem Widget können Sie auf einen Blick erkennen, wo und wann die Audience aktiviert wird, und doppelte oder unnötige Aktivierungen transparenter machen. Diese gesammelten Informationen zeigen auch, wo jegliche Aktivierungen ausgeschlossen wurden.

![Das Widget Geplante Aktivierungen .](../images/segments/scheduled-activations.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, das Segment-Dashboard zu finden und ein anzuzeigendes Segment auszuwählen. Sie sollten auch die Metriken verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Segmenten in der Experience Platform-Benutzeroberfläche finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche des Segmentierungsdienstes](../../segmentation/ui/overview.md).
