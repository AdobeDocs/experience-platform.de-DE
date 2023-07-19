---
keywords: Experience Platform; Profil; Zielgruppe; Zielgruppen; Segmentierung; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Zielgruppen-Dashboard; Dashboard
title: Dashboard-Anleitung für Zielgruppen
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu Zielgruppen anzeigen können, die Ihre Organisation erstellt hat.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '2098'
ht-degree: 50%

---

# [!UICONTROL Zielgruppen] Dashboard {#audiences-dashboard}

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu Ihren Zielgruppen anzeigen können, die in einer täglichen Momentaufnahme erfasst werden. In diesem Handbuch wird beschrieben, wie Sie auf die [!UICONTROL Zielgruppen] Dashboard in der Benutzeroberfläche und bietet weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Einen Überblick über alle Funktionen des Segmentierungs-Services von Adobe Experience Platform in der Platform-Benutzeroberfläche erhalten Sie im [Handbuch zur Benutzeroberfläche des Segmentierungs-Services](../../segmentation/ui/overview.md).

## [!UICONTROL Zielgruppen] Dashboard-Daten

Die [!UICONTROL Zielgruppen] Das Dashboard zeigt eine Momentaufnahme der Attributdaten (Datensatzdaten) an, die Ihr Unternehmen im Profilspeicher in Experience Platform hat. Die Momentaufnahme enthält keine Ereignisdaten (Zeitreihendaten).

Die Attributdaten in der Momentaufnahme zeigen die Daten exakt so an, wie sie zum Zeitpunkt der Momentaufnahme vorgefunden werden. Mit anderen Worten, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten, und die [!UICONTROL Zielgruppen] Das Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Die [!UICONTROL Zielgruppen] Dashboard {#explore}

So navigieren Sie zum [!UICONTROL Zielgruppen] Dashboard in der Platform-Benutzeroberfläche auswählen **[!UICONTROL Zielgruppen]** Wählen Sie in der linken Leiste die **[!UICONTROL Übersicht]** zum Anzeigen des Dashboards.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt wurden, wird die [!UICONTROL Zielgruppen] Das Dashboard ist nicht sichtbar. Stattdessen werden auf der Registerkarte [!UICONTROL Übersicht] Links und Dokumentation angezeigt, die Ihnen bei den ersten Schritten im Zusammenhang mit der Segmentierung helfen können.

![Die [!UICONTROL Zielgruppen] Dashboard [!UICONTROL Übersicht] Registerkarte mit [!UICONTROL Zielgruppen] und [!UICONTROL Übersicht] hervorgehoben.](../images/audiences/dashboard-overview.png)

### Ändern Sie die [!UICONTROL Zielgruppen] Dashboard {#modify}

Sie können das Erscheinungsbild der [!UICONTROL Zielgruppen] Dashboard durch Auswahl von **[!UICONTROL Dashboard ändern]**. Dadurch können Sie Widgets aus dem Dashboard verschieben, hinzufügen und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** zugreifen, um verfügbare Widgets zu erkunden und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie in der Dokumentation zum [Ändern von Dashboards](../customize/modify.md) und zur [Übersicht über die Widget-Bibliothek](../customize/widget-library.md).

### Hinzufügen von Widgets {#add-widget}

Wählen Sie **[!UICONTROL Widget hinzufügen]** aus, um zur Widget-Bibliothek zu navigieren und eine Liste der verfügbaren Widgets anzuzeigen, die Sie Ihrem Dashboard hinzufügen können.

![Die [!UICONTROL Zielgruppen] Dashboard-Übersicht mit [!UICONTROL Widget hinzufügen] hervorgehoben.](../images/audiences/audiences-overview-add-widget.png)

In der Widget-Bibliothek können Sie die Auswahl von Standard- und benutzerdefinierten Zielgruppen-Widgets durchsuchen. Informationen zum Hinzufügen von Widgets finden Sie in der Widget-Bibliothek-Dokumentation zum [Hinzufügen eines Widget](../customize/widget-library.md#add-widgets).

## Auswählen einer Zielgruppe {#select-audience}

Im Dashboard wird automatisch eine Zielgruppe ausgewählt, die angezeigt werden soll. Sie können die Zielgruppe jedoch über das Dropdown-Menü oder die Zielgruppenauswahl ändern.

Um eine andere Zielgruppe auszuwählen, wählen Sie das Dropdown-Menü neben dem Zielgruppennamen aus oder verwenden Sie die Zielgruppenauswahl, um das Dialogfeld für die Zielgruppenauswahl zu öffnen.

>[!IMPORTANT]
>
>In der Liste der auswählbaren Zielgruppen werden nur Zielgruppen angezeigt, deren Profilanzahl über null liegt.

![Die Übersicht über das Audiences-Dashboard mit dem Dropdown-Menü für globale Zielgruppen wurde hervorgehoben.](../images/audiences/change-audience.png)

![Die [!UICONTROL Zielgruppe auswählen] -Dialogfeld, das alle verfügbaren Zielgruppen anzeigt.](../images/audiences/select-audience-dialog.png)

## Widgets und Metriken {#widgets-and-metrics}

Die [!UICONTROL Zielgruppen] Das Dashboard besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihrer ausgewählten Zielgruppe enthalten.

Datum und Uhrzeit der letzten Momentaufnahme werden oben im [!UICONTROL Übersicht] neben dem Zielgruppen-Dropdown-Menü. Alle Widget-Daten sind zum Stand dieses Datums und dieser Uhrzeit korrekt. Der Zeitstempel der Momentaufnahme wird im UTC-Format angegeben, nicht in der Zeitzone der jeweiligen Person oder Organisation.

![Die Registerkarte Übersicht über Zielgruppen mit einem markierten Widget-Zeitstempel.](../images/audiences/widget-timestamp.png)

## Standard-Widgets {#standard-widgets}

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken für Ihre Zielgruppen visualisieren können. In der [!UICONTROL Widget-Bibliothek] können Sie auch benutzerdefinierte Widgets erstellen und für Ihre gesamte Organisation freigeben. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst den Abschnitt [Widget-Bibliothek – Übersicht](../customize/widget-library.md).

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
>abstract="Dieses Widget zeigt die Gesamtzahl der zusammengeführten Profile innerhalb der ausgewählten Zielgruppe an. Diese Zahl hängt von der auf Ihre Daten angewendeten Zusammenführungsrichtlinie ab und ist zum Zeitpunkt der letzten Momentaufnahme korrekt."

Die **[!UICONTROL Zielgruppengröße]** Widget zeigt die Gesamtzahl der zusammengeführten Profile in der ausgewählten Zielgruppe zum Zeitpunkt der Momentaufnahme an. Diese Zahl ist das Ergebnis der Anwendung der Zielgruppen-Zusammenführungsrichtlinie auf Ihre Profildaten, um Profilfragmente zusammenzuführen und für jede Einzelperson in der Zielgruppe ein Profil zu erstellen.

Weitere Informationen zu Fragmenten und zusammengeführten Profilen finden Sie im Abschnitt [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

![Die [!UICONTROL Zielgruppen] Dashboard-Übersicht mit [!UICONTROL Zielgruppengröße] Widget hervorgehoben.](../images/audiences/audience-size.png)

### [!UICONTROL Trend der Audience-Größe] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Trend der Audience-Größe"
>abstract="Dieses Widget liefert Informationen zur Gesamtanzahl der Profile, die den Kriterien **einer beliebigen** Segmentdefinition entsprechen und die während des täglichen Snapshots in den letzten 30 Tagen, 90 Tagen oder 12 Monate erfasst wurden."

Die **[!UICONTROL Zielgruppengrößentrend]** Widget bietet eine Kantengraph-Illustration für die Gesamtzahl der Profile, die sich für **any** Zielgruppe über einen bestimmten Zeitraum. Die Entwicklung der Zielgruppengröße kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Zielgruppengröße wird auf der Y-Achse und die Zeit auf der X-Achse dargestellt.

Dieses Widget enthält auch die automatische [!UICONTROL Untertitel] Funktion, bei der ein Modell für maschinelles Lernen die Grafik- und Zielgruppendaten analysiert und automatisch Untertitel generiert, um die wichtigsten Trends und Ereignisse zu beschreiben. Wählen Sie **[!UICONTROL Beschriftungen]** aus, um das Dialogfeld für automatische Beschriftungen zu öffnen.

![Die [!UICONTROL Zielgruppen] -Übersicht zeigt das Trend-Widget zur Zielgruppengröße an.](../images/audiences/audience-size-trend-captions.png)

Das Dialogfeld für automatische Beschriftungen wird geöffnet und bietet Einblicke in Ihre Daten.

![Das Dialogfeld für automatische Beschriftungen für das Widget „Entwicklung der Zielgruppengröße“.](../images/audiences/audience-size-trend-automatic-captions-dialog.png)

Weiterführende Informationen zur Auswertung von Audiences und zur Qualifizierung und Ausstieg von Profilen finden Sie im Abschnitt [Dokumentation zum Segmentierungsdienst](../../segmentation/home.md).

### [!UICONTROL Trend bei der Änderung der Audience-Größe] {#audience-size-change-trend}

Dieses Widget bietet eine Liniendiagramm, die die Differenz zwischen der Gesamtanzahl der Profile, die sich für eine bestimmte Zielgruppe qualifiziert haben, und den letzten täglichen Momentaufnahmen veranschaulicht. Die für die Analyse ausgewählte Audience wird im Dropdown-Menü Übersicht ausgewählt. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Zielgruppengröße wird auf der Y-Achse und die Zeit auf der X-Achse dargestellt.

![Das Widget „Entwicklung der Veränderung der Zielgruppengröße“](../images/audiences/audience-size-change-trend.png)

### [!UICONTROL Trend der Audience-Größe nach Identität] {#audience-size-trend-by-identity}

Dieses Widget veranschaulicht den Trend zur Zielgruppengröße für eine bestimmte Zielgruppe basierend auf dem Identitätstyp, der im Widget-Dropdown-Menü ausgewählt wird. Die für die Analyse verwendete Audience wird aus der Dropdown-Liste Übersicht ausgewählt. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt.

![Das Widget „Entwicklung der Zielgruppengröße nach Identität“](../images/audiences/audience-size-trend-by-identity.png)

### [!UICONTROL Reihenfolge der Audience-Aktivierung] {#audience-activation-order}

Das Widget [!UICONTROL Reihenfolge der Zielgruppenaktivierung] bietet eine dreispaltige Tabelle, in der der Zielname, die Plattform und das Aktivierungsdatum der Zielgruppe aufgelistet sind. Die Liste ist entsprechend der Aktualität von oben nach unten geordnet und kann bis zu 10 Zeilen enthalten.

![Das Widget „Reihenfolge der Zielgruppenaktivierung“](../images/audiences/audience-activation-order.png)

### [!UICONTROL Zielgruppenüberschneidung] {#audience-overlap}

Dieses Widget verwendet ein Venn-Diagramm, um die Anzahl der Personen zu visualisieren, die den Kriterien für beide Zielgruppen entsprechen. Die zum Vergleich verwendeten Zielgruppen werden aus den Widget-Dropdown-Menüs ausgewählt. Die Gesamtzahl der in der relevanten Segmentdefinition enthaltenen Profile kann durch Bewegen des Mauszeigers über einen Kreis oder die Schnittmenge des Venn-Diagramms angezeigt werden.

Mit diesem Widget können Sie Ihre Segmentierungsstrategie optimieren, indem Sie die Ähnlichkeiten in den Ergebnissen Ihrer Segmentdefinitionen visualisieren.

![Das Widget „Zielgruppenüberschneidung“.](../images/audiences/audience-overlap.png)

### [!UICONTROL Bericht zur Zielgruppenüberschneidung] {#audience-overlap-report}

Dieses Widget enthält eine tabellarische Darstellung der Profilüberlagerungsdaten für eine bestimmte Zielgruppe. Eine Liste mit fünf Zielgruppen, die von den Prozentsätzen der höchsten bis zur niedrigsten Überschneidung sortiert sind, wird für die aus dem Dropdown-Menü am oberen Bildschirmrand ausgewählte Zielgruppe bereitgestellt. Die ausgewählte Audience wird im Abschnitt [!UICONTROL ZIELGRUPPE A NAME] Spalte. Die Analyse der Zielgruppenüberschneidung wird für die zweite Zielgruppe bereitgestellt, die im Abschnitt [!UICONTROL AUDIENCE B NAME] Spalte. Die prozentuale Überschneidung wird in der dritten Spalte auf zwölf Dezimalstellen genau angegeben.

Der Bericht zur Zielgruppenüberschneidung hilft Ihnen beim Erstellen neuer, leistungsstarker Zielgruppen. Durch die Beachtung hoher prozentualer Überschneidungen können Sie Zielgruppen unterdrücken und das Senden derselben Zielgruppe an verschiedene Ziele verhindern. Diese Daten helfen Ihnen auch dabei, verborgene Insights zu entdecken, die bei einer besseren Segmentierung hilfreich sein können. Eine geringe prozentuale Überschneidung hilft, eindeutige Profile zu finden, deren Kontaktierung Sie fortsetzen sollten.

Wählen Sie **[!UICONTROL Mehr anzeigen]** aus, um ein Vollbilddialogfeld zu öffnen, das mehr Daten zu Zielgruppenüberschneidungen enthält.

![Das Widget „Bericht Zielgruppenüberscheidung“ mit hervorgehobener Option „Mehr anzeigen“.](../images/audiences/audience-overlap-report.png)

Das Dialogfeld [!UICONTROL Bericht zur Zielgruppenüberschneidung] wird angezeigt. Dieses Dialogfeld kann bis zu 50 Zeilen mit Analysen zur Zielgruppenüberschneidung enthalten, die in sechs Spalten unterteilt sind. Wählen Sie das Einstellungssymbol (![Das Einstellungssymbol.](../images/audiences/settings-icon.png)) aus, um Spalten aus der Tabelle zu entfernen oder zur Tabelle hinzuzufügen.

![Das Dialogfeld mit dem Bericht zur Zielgruppenüberschneidung.](../images/audiences/audience-overlap-report-dialog.png)

>[!NOTE]
>
>Wählen Sie die Spaltenüberschrift **[!UICONTROL Überschneidung]** aus, um die Rangfolge der Ergebnisse vom höchsten zum niedrigsten bzw. vom niedrigsten zum höchsten zu ändern.

Um den gesamten Bericht im PDF-Format herunterzuladen, wählen Sie das Optionsmenü (**`...`**) und dann **[!UICONTROL Download]** aus.

![Das Dialogfeld mit dem Bericht zur Zielgruppenüberschneidung mit den Auslassungszeichen und der hervorgehobenen Download-Option.](../images/audiences/audience-overlap-report-dialog-download.png)

Wählen Sie eine Zeile aus dem Bericht aus, um ein Venn-Diagramm der Überschneidungsanalyse zu öffnen. Bewegen Sie den Mauszeiger über einen Abschnitt des Venn-Diagramms, um die Profilanzahl in einem Dialogfeld anzuzeigen.

![Das Dialogfeld mit dem Bericht zur Zielgruppenüberschneidung mit einem Venn-Diagramm und einer hervorgehobenen Zeile.](../images/audiences/audience-overlap-report-dialog-venn.png)

Auswählen **[!UICONTROL Schließen]** , um zur [!UICONTROL Zielgruppen] Dashboard.

### [!UICONTROL Identitätsüberschneidung] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Identitätsüberschneidung"
>abstract="Dieses Widget zeigt die Überschneidung von Profilen in der Zielgruppe an, die beide ausgewählten Identitäten enthalten. Die Kreise zeigen die relative Größe jeder Identität an. Die Anzahl der Profile, die beide Namespaces enthalten, wird durch den Überschneidungsbereich der Kreise dargestellt."

Die **[!UICONTROL Identitätsüberschneidung]** -Widget zeigt ein Venn-Diagramm oder ein Set-Diagramm an, das die Überschneidung von Profilen in Ihrer Zielgruppe mit mehreren Identitäten anzeigt.

Verwenden Sie die Dropdown-Menüs im Widget, um die Identitäten auszuwählen, die Sie vergleichen möchten. Die Kreise zeigen die relative Größe jeder ausgewählten Identität an, wobei die Anzahl der Profile, die beide Namespaces enthalten, der Größe des Überschneidungsbereichs der Kreise entspricht.

Wenn ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Identitäten zugeordnet. In dieser Situation ist es wahrscheinlich, dass Ihr Unternehmen über mehrere Profile verfügt, die Fragmente aus mehreren Identitäten enthalten.

Weitere Informationen zu Identitäten finden Sie unter [Dokumentation zu Identity Service](../../identity-service/home.md).

![Die [!UICONTROL Zielgruppen] Dashboard-Übersicht mit hervorgehobenem Widget zur Identitätsüberschneidung.](../images/audiences/identity-overlap.png)

### [!UICONTROL Profile nach Identität] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profile nach Identität"
>abstract="Dieses Widget zeigt die Aufschlüsselung der Identitäten für jedes zusammengeführte Profil in der ausgewählten Zielgruppe an."

Die **[!UICONTROL Profile nach Identität]** -Widget zeigt die Aufschlüsselung der Identitäten für jedes zusammengeführte Profil in Ihrer ausgewählten Zielgruppe an. Die Gesamtzahl der Profile nach Identität kann höher sein als die Gesamtzahl der Profile in der Zielgruppe, da einem Profil mehrere Identitäten zugeordnet sein können. Das heißt, dass die Summe der für jede Identität angezeigten Werte die Gesamtgröße der Zielgruppe übersteigen kann. Dies liegt daran, dass bei der Interaktion eines Kunden mit Ihrer Marke auf mehr als einem Kanal mehrere Identitäten mit diesem einzelnen Kunden verknüpft werden können.

Wählen Sie **[!UICONTROL Beschriftungen]** aus, um das Dialogfeld für automatische Beschriftungen zu öffnen.

![Die [!UICONTROL Zielgruppen] Dashboard-Übersicht mit hervorgehobener Option Profile nach Identitäts-Widget und Beschriftungen.](../images/audiences/profiles-by-identity.png)

Ein maschinelles Lernmodell generiert automatisch Dateneinblicke, indem es die Gesamtverteilung und die Schlüsselaspekte der Daten analysiert.

Weitere Informationen zu Identitäten finden Sie unter [Dokumentation zu Identity Service](../../identity-service/home.md).

### Geplante Aktivierungen {#scheduled-activations}

Das Widget [!UICONTROL Geplante Aktivierungen] bietet eine tabellarische Übersicht über die zuletzt aktivierten Ziele. Die Tabelle enthält die Zielplattform, den Namen Ihres Aktivierungsflusses zu diesem Ziel sowie das Start- und Enddatum der Aktivierung für die ausgewählte Zielgruppe. Wenn für die Aktivierung kein Enddatum angegeben wurde, wird sie als [!UICONTROL Fortaufend] angezeigt. Die Zielgruppe für die Analyse wird oben auf der Seite aus dem Dropdown-Menü ausgewählt.

Mit diesem Widget können Sie auf einen Blick erkennen, wo und wann die Zielgruppe aktiviert wird, und es macht doppelte oder unnötige Aktivierungen transparenter. Diese gesammelten Informationen zeigen auch, wo jegliche Aktivierungen ausgeschlossen wurden.

![Das Widget „Geplante Aktivierungen“.](../images/audiences/scheduled-activations.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, die [!UICONTROL Zielgruppen] und wählen Sie eine Zielgruppe aus, die angezeigt werden soll. Sie sollten auch die Metriken verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Zielgruppen in der Benutzeroberfläche von Experience Platform finden Sie im Abschnitt [Handbuch zur Benutzeroberfläche des Segmentierungsdienstes](../../segmentation/ui/overview.md).
