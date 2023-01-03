---
keywords: Experience Platform;Profil;Segment;Segmente;Segmentierung;Benutzeroberfläche;UI;Anpassung;Segment-Dashboard;Dashboard
title: Handbuch zum Segmente-Dashboard
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu Segmenten anzeigen können, die Ihre Organisation erstellt hat.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 98%

---

# [!UICONTROL Segmente-Dashboard] {#segment-dashboard}

Die Adobe Experience Platform-Benutzeroberfläche (UI) verfügt über ein Dashboard, über das Sie wichtige Informationen zu Ihren Segmenten anzeigen können. Diese Informationen werden in Form einer täglichen Momentaufnahme erfasst. In diesem Handbuch wird beschrieben, wie Sie in der Benutzeroberfläche auf das Segmente-Dashboard zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Einen Überblick über alle Funktionen des Segmentierungs-Services von Adobe Experience Platform in der Platform-Benutzeroberfläche erhalten Sie im [Handbuch zur Benutzeroberfläche des Segmentierungs-Services](../../segmentation/ui/overview.md).

## Daten im [!UICONTROL Segmente]-Dashboard

Im Segmente-Dashboard wird eine Momentaufnahme der Attributdaten (Datensatzdaten) dargestellt, über die Ihre Organisation im Experience Platform-Profilspeicher verfügt. Die Momentaufnahme enthält keine Ereignisdaten (Zeitreihendaten).

Die Attributdaten in der Momentaufnahme zeigen die Daten exakt so an, wie sie zum Zeitpunkt der Momentaufnahme vorgefunden werden. Das heißt, die Momentaufnahme ist keine Annäherung oder Stichprobe der Daten, und das Segmente-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Erkunden des [!UICONTROL Segmente]-Dashboards {#explore}

Um zum [!UICONTROL Segmente]-Dashboard in der Platform-Benutzeroberfläche zu navigieren, wählen Sie in der linken Leiste die Option **[!UICONTROL Segmente]** und dann die Registerkarte **[!UICONTROL Übersicht]** aus, um das Dashboard anzuzeigen.

>[!NOTE]
>
>Wenn Ihre Organisation Platform erst seit kurzem nutzt und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt hat, ist das [!UICONTROL Segmente]-Dashboard nicht sichtbar. Stattdessen werden auf der Registerkarte [!UICONTROL Übersicht] Links und Dokumentation angezeigt, die Ihnen bei den ersten Schritten im Zusammenhang mit der Segmentierung helfen können.

![Im Tab Übersicht des Segments-Dashboards werden Segmente und Übersicht hervorgehoben.](../images/segments/dashboard-overview.png)

### Ändern des [!UICONTROL Segmente]-Dashboards {#modify}

Sie können das Erscheinungsbild des [!UICONTROL Segmente]-Dashboards durch Auswahl von **[!UICONTROL Dashboard ändern]** ändern. Dadurch können Sie Widgets aus dem Dashboard verschieben, hinzufügen und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** zugreifen, um verfügbare Widgets zu erkunden und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie in der Dokumentation zum [Ändern von Dashboards](../customize/modify.md) und zur [Übersicht über die Widget-Bibliothek](../customize/widget-library.md).

### Hinzufügen von Widgets {#add-widget}

Wählen Sie **[!UICONTROL Widget hinzufügen]** aus, um zur Widget-Bibliothek zu navigieren und eine Liste der verfügbaren Widgets anzuzeigen, die Sie Ihrem Dashboard hinzufügen können.

![Die Registerkarte „Übersicht“ des Segmente-Dashboards mit hervorgehobener Option „Widget hinzufügen“](../images/segments/segments-overview-add-widget.png)

Über die Widget-Bibliothek können Sie die Auswahl von standardmäßigen und benutzerdefinierten Segment-Widgets durchsuchen. Informationen zum [Hinzufügen von Widgets](../customize/widget-library.md#add-widgets) finden Sie in der Dokumentation zur Widget-Bibliothek.

## Auswählen eines Segments

Das Dashboard wählt automatisch ein anzuzeigendes Segment aus. Sie können das Segment jedoch über das Dropdown-Menü oder die Segmentauswahl ändern.

Für die Auswahl eines anderen Segments wählen Sie das Dropdown-Menü neben dem Segmentnamen aus oder verwenden Sie die Segmentauswahl, um das Dialogfeld für die Segmentauswahl zu öffnen.

>[!IMPORTANT]
>
>In der Liste der auswählbaren Segmente werden nur Segmente angezeigt, deren Profilanzahl über null liegt.

![Die Registerkarte „Übersicht“ des Segmente-Dashboards mit hervorgehobenem Dropdown-Menü für globale Segmente](../images/segments/change-segment.png)

![Das Dialogfeld „Segment auswählen“ mit allen verfügbaren Segmenten](../images/segments/select-segment-dialog.png)

## Widgets und Metriken

Das Segmente-Dashboard besteht aus Widgets, bei denen es sich um schreibgeschützte Metriken handelt und die wichtige Informationen zum ausgewählten Segment enthalten.

Datum und Uhrzeit der letzten Momentaufnahme werden oben auf der Registerkarte [!UICONTROL Übersicht] neben dem Dropdown-Menü des Segments angezeigt. Alle Widget-Daten sind zum Stand dieses Datums und dieser Uhrzeit korrekt. Der Zeitstempel der Momentaufnahme wird im UTC-Format angegeben, nicht in der Zeitzone der jeweiligen Person oder Organisation.

![Die Registerkarte „Übersicht“ der Segmente mit einem hervorgehobenem Zeitstempel eines Widgets](../images/segments/widget-timestamp.png)

## Standard-Widgets {#standard-widgets}

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Segmenten visualisieren können. Sie können auch benutzerdefinierte Widgets erstellen, die über die [!UICONTROL Widget-Bibliothek] für Ihre Organisation freigegeben werden können. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst den Abschnitt [Widget-Bibliothek – Übersicht](../customize/widget-library.md).

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Audience-Größe]](#audience-size)
* [[!UICONTROL Reihenfolge der Audience-Aktivierung]](#audience-activation-order)
* [[!UICONTROL Trend der Audience-Größe]](#audience-size-trend)
* [[!UICONTROL Trend bei der Änderung der Audience-Größe]](#audience-size-change-trend)
* [[!UICONTROL Trend der Audience-Größe nach Identität]](#audience-size-trend-by-identity)
* [[!UICONTROL Zielgruppenüberschneidung]](#audience-overlap)
* [[!UICONTROL Bericht zur Zielgruppenüberschneidung]](#audience-overlap-report)
* [[!UICONTROL Identitätsüberschneidung]](#identity-overlap)
* [[!UICONTROL Profile nach Identität]](#profiles-by-identity)
* [[!UICONTROL Geplante Aktivierungen]](#scheduled-activations)

### [!UICONTROL Audience-Größe] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Audience-Größe"
>abstract="Dieses Widget zeigt die Gesamtzahl der zusammengeführten Profile innerhalb des ausgewählten Segments an. Diese Zahl hängt von der auf Ihre Daten angewendeten Zusammenführungsrichtlinie ab und ist zum Zeitpunkt der letzten Momentaufnahme korrekt."

Das Widget **[!UICONTROL Zielgruppengröße]** zeigt die Gesamtzahl der zusammengeführten Profile innerhalb des ausgewählten Segments zum Zeitpunkt der Momentaufnahme an. Diese Zahl ist das Ergebnis der Anwendung der Segmentzusammenführungsrichtlinie auf Ihre Profildaten, um Profilfragmente zu einem einzigen Profil für jede Person im Segment zusammenzuführen.

Weitere Informationen zu Fragmenten und zusammengeführten Profilen finden Sie im Abschnitt [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

![Die Registerkarte „Übersicht“ des Segmente-Dashboards mit hervorgehobenem Widget „Zielgruppengröße“](../images/segments/audience-size.png)

### [!UICONTROL Trend der Audience-Größe] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Trend der Audience-Größe"
>abstract="Dieses Widget liefert Informationen zur Gesamtanzahl der Profile, die den Kriterien **einer beliebigen** Segmentdefinition entsprechen und die während des täglichen Snapshots in den letzten 30 Tagen, 90 Tagen oder 12 Monate erfasst wurden."

Das Widget **[!UICONTROL Entwicklung der Zielgruppengröße]** bietet eine Kantengraph-Illustration für die Gesamtzahl der Profile, die die Kriterien **einer beliebigen** Segmentdefinition über einen bestimmten Zeitraum erfüllen. Die Entwicklung der Zielgruppengröße kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Zielgruppengröße wird auf der Y-Achse und die Zeit auf der X-Achse dargestellt.

Dieses Widget enthält auch die Funktion für automatische [!UICONTROL Beschriftungen], bei der ein maschinelles Lernmodell die Diagramm- und Segmentdaten analysiert und automatisch Beschriftungen generiert, um die wichtigsten Entwicklungen und Ereignisse zu beschreiben. Wählen Sie **[!UICONTROL Beschriftungen]** aus, um das Dialogfeld für automatische Beschriftungen zu öffnen.

![In der Segmentübersicht wird das Widget „Entwicklung der Zielgruppengröße“ angezeigt.](../images/segments/audience-size-trend-captions.png)

Das Dialogfeld für automatische Beschriftungen wird geöffnet und bietet Einblicke in Ihre Daten.

![Das Dialogfeld für automatische Beschriftungen für das Widget „Entwicklung der Zielgruppengröße“.](../images/segments/audience-size-trend-automatic-captions-dialog.png)

Weiterführende Informationen zur Segmentauswertung und dazu, wie Profile für Segmente qualifiziert und daraus entfernt werden, finden Sie in der [Dokumentation zum Segmentierungs-Service](../../segmentation/home.md).

### [!UICONTROL Trend bei der Änderung der Audience-Größe] {#audience-size-change-trend}

Dieses Widget bietet ein Liniendiagramm, das die Differenz der Gesamtzahl der Profile anzeigt, die sich im Zeitraum zwischen den jüngsten täglichen Snapshots für ein bestimmtes Segment qualifiziert haben. Das für die Analyse ausgewählte Segment wird aus dem Dropdown-Menü „Übersicht“ ausgewählt. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Zielgruppengröße wird auf der Y-Achse und die Zeit auf der X-Achse dargestellt.

![Das Widget „Entwicklung der Veränderung der Zielgruppengröße“](../images/segments/audience-size-change-trend.png)

### [!UICONTROL Trend der Audience-Größe nach Identität] {#audience-size-trend-by-identity}

Dieses Widget veranschaulicht die Entwicklung der Zielgruppengröße für ein bestimmtes Segment basierend auf dem Identitätstyp, der im Widget-Dropdown-Menü ausgewählt wurde. Das für die Analyse verwendete Segment wird aus dem Dropdown-Menü „Übersicht“ ausgewählt. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt.

![Das Widget „Entwicklung der Zielgruppengröße nach Identität“](../images/segments/audience-size-trend-by-identity.png)

### [!UICONTROL Reihenfolge der Audience-Aktivierung] {#audience-activation-order}

Das Widget [!UICONTROL Reihenfolge der Zielgruppenaktivierung] bietet eine dreispaltige Tabelle, in der der [!UICONTROL Zielname], die [!UICONTROL Plattform] und das [!UICONTROL Aktivierungsdatum] der Zielgruppe aufgelistet sind. Die Liste ist entsprechend der Aktualität von oben nach unten geordnet und kann bis zu 10 Zeilen enthalten.

![Das Widget „Reihenfolge der Zielgruppenaktivierung“](../images/segments/audience-activation-order.png)

### [!UICONTROL Zielgruppenüberschneidung] {#audience-overlap}

Dieses Widget stellt die Anzahl der Profile aus zwei Segmenten dar, die die Kriterien für beide Segmentdefinitionen erfüllen. Die verwendeten Segmente werden aus den Widget-Dropdown-Menüs ausgewählt. Die Gesamtzahl der in der relevanten Segmentdefinition enthaltenen Profile kann durch Bewegen des Mauszeigers über einen Kreis oder die Schnittmenge des Venn-Diagramms angezeigt werden.

Mit diesem Widget können Sie Ihre Segmentierungsstrategie optimieren, indem Sie die Ähnlichkeiten in den Ergebnissen Ihrer Segmentdefinitionen visualisieren.

![Das Widget „Zielgruppenüberschneidung“.](../images/segments/audience-overlap.png)

### [!UICONTROL Bericht zur Zielgruppenüberschneidung] {#audience-overlap-report}

Dieses Widget stellt die Daten der Zielgruppenüberschneidung für ein bestimmtes Segment als Tabelle dar. Für das Segment, das oben im Bildschirm aus dem Dropdown-Menü ausgewählt wurde, wird eine Liste mit fünf Zielgruppen angezeigt, die vom höchsten bis zum niedrigsten Überschneidungsprozentsatz sortiert sind. Aus Gründen der Übersichtlichkeit wird Ihr ausgewähltes Segment in der Spalte [!UICONTROL Name des Segments A] aufgeführt. Die Analyse der Zielgruppenüberschneidung wird für das zweite Segment bereitgestellt, das in der Spalte [!UICONTROL Name von Segment B] aufgeführt ist. Die prozentuale Überschneidung wird in der dritten Spalte auf zwölf Dezimalstellen genau angegeben.

Der Bericht zur Zielgruppenüberschneidung hilft Ihnen beim Erstellen neuer, hochqualitativer Segmente. Durch die Beachtung hoher prozentualer Überschneidungen können Sie Zielgruppen unterdrücken und das Senden derselben Zielgruppe an verschiedene Ziele verhindern. Diese Daten helfen Ihnen auch dabei, verborgene Insights zu entdecken, die bei einer besseren Segmentierung hilfreich sein können. Eine geringe prozentuale Überschneidung hilft, eindeutige Profile zu finden, deren Kontaktierung Sie fortsetzen sollten.

Wählen Sie **[!UICONTROL Mehr anzeigen]** aus, um ein Vollbilddialogfeld zu öffnen, das mehr Segmentüberschneidungsdaten enthält.

![Das Widget mit dem Zielgruppenüberschneidungsbericht mit hervorgehobener Option „Mehr anzeigen“.](../images/segments/audience-overlap-report.png)

Das Dialogfeld [!UICONTROL Bericht zur Zielgruppenüberschneidung] wird angezeigt. Dieses Dialogfeld kann bis zu 50 Zeilen mit Analysen zur Zielgruppenüberschneidung enthalten, die in sechs Spalten unterteilt sind. Wählen Sie das Einstellungssymbol (![Das Einstellungssymbol.](../images/segments/settings-icon.png)) aus, um Spalten aus der Tabelle zu entfernen oder zur Tabelle hinzuzufügen.

![Das Dialogfeld mit dem Bericht zur Zielgruppenüberschneidung.](../images/segments/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Wählen Sie die Spaltenüberschrift **[!UICONTROL Überschneidung]** aus, um die Rangfolge der Ergebnisse vom höchsten zum niedrigsten bzw. vom niedrigsten zum höchsten zu ändern.

Um den gesamten Bericht im PDF-Format herunterzuladen, wählen Sie das Optionsmenü (**`...`**) und dann **[!UICONTROL Download]** aus.

![Das Dialogfeld mit dem Bericht zur Zielgruppenüberschneidung mit den Auslassungszeichen und der hervorgehobenen Download-Option.](../images/segments/segments-audience-overlap-report-dialog-download.png)

Wählen Sie eine Zeile aus dem Bericht aus, um ein Venn-Diagramm der Überschneidungsanalyse zu öffnen. Bewegen Sie den Mauszeiger über einen Abschnitt des Venn-Diagramms, um die Profilanzahl in einem Dialogfeld anzuzeigen.

![Das Dialogfeld mit dem Bericht zur Zielgruppenüberschneidung mit einem Venn-Diagramm und einer hervorgehobenen Zeile.](../images/segments/audience-overlap-report-dialog-venn.png)

Wählen Sie **[!UICONTROL Schließen]** aus, um zum [!UICONTROL Segmente]-Dashboard zurückzukehren.

### [!UICONTROL Identitätsüberschneidung] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Identitätsüberschneidung"
>abstract="Dieses Widget zeigt die Überschneidung von Profilen in Ihrem Segment ab, die beide ausgewählten Identitäten enthalten. Die Kreise zeigen die relative Größe jeder Identität an. Die Anzahl der Profile, die beide Namespaces enthalten, wird durch den Überschneidungsbereich der Kreise dargestellt."

Das Widget **[!UICONTROL Identitätsüberschneidung]** zeigt ein Venn-Diagramm (oder Mengendiagramm) an, das die Überschneidung von Profilen in Ihrem Segment mit mehreren Identitäten anzeigt.

Verwenden Sie die Dropdown-Menüs im Widget, um die Identitäten auszuwählen, die Sie vergleichen möchten. Die Kreise zeigen die relative Größe jeder ausgewählten Identität an, wobei die Anzahl der Profile, die beide Namespaces enthalten, der Größe des Überschneidungsbereichs der Kreise entspricht.

Wenn ein Kunde mit Ihrer Marke über mehr als einen Kanal interagiert, werden diesem einzelnen Kunden mehrere Identitäten zugeordnet. Daher ist es wahrscheinlich, dass Ihre Organisation über mehrere Profile verfügt, die Fragmente aus mehr als einer Identität enthalten.

Weitere Informationen zu Identitäten finden Sie in der [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

![Die Übersicht des Segmente-Dashboards mit dem hervorgehobenen Widget „Identitätsüberschneidung“.](../images/segments/identity-overlap.png)

### [!UICONTROL Profile nach Identität] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profile nach Identität"
>abstract="Dieses Widget zeigt die Aufschlüsselung der Identitäten für jedes zusammengeführte Profil in Ihrem ausgewählten Segment an."

Das Widget **[!UICONTROL Profile nach Identität]** zeigt die Aufschlüsselung der Identitäten für jedes zusammengeführte Profil in Ihrem ausgewählten Segment an. Die Gesamtzahl der Profile nach Identität kann höher sein als die Gesamtzahl der Profile im Segment, da einem Profil mehrere Identitäten zugeordnet sein können. Das heißt, dass die Summe der für jede Identität angezeigten Werte größer sein kann als die gesamte Zielgruppengröße im Segment, da bei der Interaktion eines Kunden mit Ihrer Marke über mehr als einen Kanal mehrere Identitäten mit diesem einzelnen Kunden verknüpft werden können.

Wählen Sie **[!UICONTROL Beschriftungen]** aus, um den Dialog „Automatische Beschriftungen“ zu öffnen.

![Die Übersicht über das Dashboard &quot;Segmente&quot;mit der Option Profile nach Identitäts-Widget und Beschriftungen hervorgehoben.](../images/segments/profiles-by-identity.png)

Ein maschinelles Lernmodell generiert automatisch Dateneinblicke, indem es die Gesamtverteilung und die Schlüsselaspekte der Daten analysiert.

Weitere Informationen zu Identitäten finden Sie in der [Dokumentation zu Adobe Experience Platform Identity Service](../../identity-service/home.md).

### Geplante Aktivierungen {#scheduled-activations}

Das Widget [!UICONTROL Geplante Aktivierungen] bietet eine tabellarische Übersicht über die zuletzt aktivierten Ziele. Die Tabelle enthält die Zielplattform, den Namen Ihres Aktivierungsflusses zu diesem Ziel sowie das Start- und Enddatum der Aktivierung für das ausgewählte Segment. Wenn für die Aktivierung kein Enddatum angegeben wurde, wird sie als [!UICONTROL Fortaufend] angezeigt. Das zu analysierende Segment wird oben auf der Seite aus dem Dropdown-Menü ausgewählt.

Mit diesem Widget können Sie auf einen Blick erkennen, wo und wann die Zielgruppe aktiviert wird, und es macht doppelte oder unnötige Aktivierungen transparenter. Diese gesammelten Informationen zeigen auch, wo jegliche Aktivierungen ausgeschlossen wurden.

![Das Widget „Geplante Aktivierungen“.](../images/segments/scheduled-activations.png)

## Nächste Schritte

Wenn Sie diesem Dokument gefolgt sind, sollten Sie jetzt in der Lage sein, das Segmente-Dashboard zu finden und ein Segment auszuwählen, das angezeigt werden soll. Sie sollten auch die Metriken verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Segmenten in der Experience Platform-Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche des Segmentierungs-Services](../../segmentation/ui/overview.md).
