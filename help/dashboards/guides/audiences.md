---
keywords: Experience Platform; Profil; Zielgruppe; Zielgruppen; Segmentierung; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Zielgruppen-Dashboard; Dashboard
title: Zielgruppen-Dashboard
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu Zielgruppen anzeigen können, die Ihre Organisation erstellt hat.
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: a8b5ed09e8e28075a3a4f37ad30f01c1cc389b9c
workflow-type: tm+mt
source-wordcount: '3132'
ht-degree: 38%

---

# [!UICONTROL Zielgruppen]-Dashboard {#audiences-dashboard}

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu Ihren Zielgruppen anzeigen können, die in einer täglichen Momentaufnahme erfasst werden. In diesem Handbuch wird beschrieben, wie Sie auf das Dashboard [!UICONTROL Zielgruppen] in der Benutzeroberfläche zugreifen und mit ihm arbeiten. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Einen Überblick über alle Funktionen des Segmentierungs-Services von Adobe Experience Platform in der Platform-Benutzeroberfläche erhalten Sie im [Handbuch zur Benutzeroberfläche des Segmentierungs-Services](../../segmentation/ui/overview.md).

## [!UICONTROL Dashboard-Daten der Zielgruppen]

Das Dashboard [!UICONTROL Zielgruppen] zeigt eine Momentaufnahme der Attributdaten (Datensatzdaten) an, die Ihr Unternehmen im Profilspeicher in Experience Platform hat. Die Momentaufnahme enthält keine Ereignisdaten (Zeitreihendaten).

Die Attributdaten in der Momentaufnahme zeigen die Daten exakt so an, wie sie zum Zeitpunkt der Momentaufnahme vorgefunden werden. Mit anderen Worten, der Schnappschuss ist keine Annäherung oder kein Beispiel der Daten und das Dashboard [!UICONTROL Zielgruppen] wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Dashboard [!UICONTROL Zielgruppen] durchsuchen {#explore}

Um in der Platform-Benutzeroberfläche zum Dashboard [!UICONTROL Zielgruppen] zu navigieren, wählen Sie in der linken Leiste die Option **[!UICONTROL Zielgruppen]** und dann die Registerkarte **[!UICONTROL Übersicht]** aus, um das Dashboard anzuzeigen.

>[!NOTE]
>
>Wenn Ihre Organisation erst seit kurzem Platform nutzt und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt hat, ist das Dashboard [!UICONTROL Zielgruppen] nicht sichtbar. Stattdessen werden auf der Registerkarte [!UICONTROL Übersicht] Links und Dokumentation angezeigt, die Ihnen bei den ersten Schritten im Zusammenhang mit der Segmentierung helfen können.

![Die Registerkarte [!UICONTROL Audiences] Dashboard [!UICONTROL Überblick] mit den Registerkarten [!UICONTROL Audiences] und [!UICONTROL Übersicht] wurde hervorgehoben.](../images/audiences/dashboard-overview.png)

### Ändern des Dashboards [!UICONTROL Zielgruppen] {#modify}

Sie können das Erscheinungsbild des Dashboards [!UICONTROL Zielgruppen] ändern, indem Sie die Option **[!UICONTROL Dashboard ändern]** auswählen. Dadurch können Sie Widgets aus dem Dashboard verschieben, hinzufügen und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** zugreifen, um verfügbare Widgets zu erkunden und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie in der Dokumentation zum [Ändern von Dashboards](../customize/modify.md) und zur [Übersicht über die Widget-Bibliothek](../customize/widget-library.md).

### Hinzufügen von Widgets {#add-widget}

Wählen Sie **[!UICONTROL Widget hinzufügen]** aus, um zur Widget-Bibliothek zu navigieren und eine Liste der verfügbaren Widgets anzuzeigen, die Sie Ihrem Dashboard hinzufügen können.

![Die Übersicht über das Dashboard [!UICONTROL Zielgruppen] mit dem Hinweis [!UICONTROL Widget hinzufügen] ist hervorgehoben.](../images/audiences/audiences-overview-add-widget.png)

In der Widget-Bibliothek können Sie die Auswahl von Standard- und benutzerdefinierten Zielgruppen-Widgets durchsuchen. Informationen zum Hinzufügen von Widgets finden Sie in der Widget-Bibliothek-Dokumentation zum [Hinzufügen eines Widget](../customize/widget-library.md#add-widgets).

### SQL anzeigen {#view-sql}

Sie können die SQL anzeigen, die die auf Ihrem Dashboard visualisierten Einblicke generiert, indem Sie den Arbeitsbereich [!UICONTROL Überblick] aktivieren. Sie können sich die SQL Ihrer vorhandenen Einblicke inspirieren lassen, um neue Abfragen zu erstellen, die anhand Ihrer geschäftlichen Anforderungen eindeutige Einblicke aus Platform-Daten gewinnen. Weitere Informationen zu dieser Funktion finden Sie im Handbuch [SQL-Benutzeroberfläche anzeigen](../view-sql.md) .

## Auswählen einer Zielgruppe {#select-audience}

Im Dashboard wird automatisch eine Zielgruppe ausgewählt, die angezeigt werden soll. Sie können die Zielgruppe jedoch über das Dropdown-Menü oder die Zielgruppenauswahl ändern.

Um eine andere Zielgruppe auszuwählen, wählen Sie das Dropdown-Menü neben dem Zielgruppennamen aus oder verwenden Sie die Zielgruppenauswahl, um das Dialogfeld für die Zielgruppenauswahl zu öffnen.

>[!IMPORTANT]
>
>In der Liste der auswählbaren Zielgruppen werden nur Zielgruppen angezeigt, deren Profilanzahl über null liegt.

![Die Übersicht des Zielgruppen-Dashboards mit dem Dropdown-Menü für globale Zielgruppen wurde hervorgehoben.](../images/audiences/change-audience.png)

![Das Dialogfeld [!UICONTROL Zielgruppe auswählen] , in dem alle verfügbaren Zielgruppen angezeigt werden.](../images/audiences/select-audience-dialog.png)

## Widgets und Metriken {#widgets-and-metrics}

Das Dashboard [!UICONTROL Zielgruppen] besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihrer ausgewählten Zielgruppe enthalten.

Datum und Uhrzeit der letzten Momentaufnahme werden oben auf der Registerkarte [!UICONTROL Übersicht] neben dem Zielgruppen-Dropdown-Menü angezeigt. Alle Widget-Daten sind zum Stand dieses Datums und dieser Uhrzeit korrekt. Der Zeitstempel der Momentaufnahme wird im UTC-Format angegeben, nicht in der Zeitzone der jeweiligen Person oder Organisation.

![Die Registerkarte &quot;Zielgruppenübersicht&quot;mit einem markierten Widget-Zeitstempel.](../images/audiences/widget-timestamp.png)

## Standard-Widgets {#default-widgets}

Für alle neuen Instanzen von Adobe Experience Platform wird ein standardmäßiges Widget-Load-out bereitgestellt, in dem die neuesten verfügbaren Einblicke aus Ihren Daten hervorgehoben werden. Die folgenden Widgets werden von Anfang an in Ihrer Segmentansicht vorkonfiguriert. Ausführliche Informationen zum Zweck und zur Funktion der Widgets finden Sie in den jeweiligen Abschnitten.

* [[!UICONTROL Zielgruppen-Größe]](#audience-size)
* [[!UICONTROL Trend bei der Änderung der Zielgruppen-Größe]](#audience-size-change-trend)
* [[!UICONTROL Identitätsüberschneidung]](#identity-overlap)
* [[!UICONTROL Profile nach Identität]](#profiles-by-identity)

>[!NOTE]
>
>Ab dem 26. Juli 2023 wurden die Dashboards [!UICONTROL Profile], [!UICONTROL Zielgruppen] und [!UICONTROL Ziele] Übersicht für alle Benutzer, die ihre Ansichten in den letzten sechs Monaten nicht geändert haben, auf ein neues standardmäßiges Widget-Load-out zurückgesetzt.
>In der Dokumentation in den Abschnitten [Profile](./profiles.md#default-widgets) und [Ziele](./destinations.md#default-widgets) des Standard-Widgets finden Sie Informationen dazu, welche Widgets als Teil der standardmäßigen Widget-Auslastungen enthalten sind. Sie können Ihre Dashboard-Widgets weiterhin wie bisher anpassen.

## Kunden-KI-Widgets {#customer-ai-audiences-widgets}

Customer AI wird verwendet, um für einzelne Profile skaliert benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion zu berechnen. Customer AI analysiert dazu vorhandene Erlebnisereignisdaten von Verbrauchern, um die Tendenzwerte für Abwanderung oder Konversion vorherzusagen **.** Diese hochpräzisen kundenspezifischen Tendenzmodelle ermöglichen eine präzisere Segmentierung und Targeting. Die Einblicke [Verteilung der Bewertungen](#customer-ai-distribution-of-scores) und [Bewertungszusammenfassung](#customer-ai-scoring-summary) zeigen die Aufteilung in Ihrer Zielgruppe. Sie heben hervor, welche Profile die hohe/niedrige/mittlere Tendenz aufweisen und wie sie über Ihre Profilzahlen verteilt sind.

* [[!UICONTROL Kunden-KI – Bewertungszusammenfassung]](#customer-ai-scoring-summary)
* [[!UICONTROL Kunden-KI – Verteilung von Bewertungen]](#customer-ai-distribution-of-scores)

### [!UICONTROL Kunden-KI – Verteilung von Bewertungen] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_distributionOfScores"
>title="Verteilung der Scores"
>abstract="Dieses Widget visualisiert die Verteilung der Gesamtanzahl der Profile anhand ihrer Tendenzwerte in Schritten von fünf Prozent. Die Verteilung der Profilanzahl wird durch das KI-Modell und die ausgewählte Zusammenführungsrichtlinie bestimmt. Sie können das KI-Modell im Dropdown-Menü unter dem Widget-Titel ändern."

Das Widget [!UICONTROL Customer AI-Verteilung der Bewertungen] kategorisiert die Gesamtanzahl der Profile nach ihren Tendenzwerten. Die Verteilung der Profilanzahl wird durch das AI-Modell und die ausgewählte Zusammenführungsrichtlinie bestimmt und dann in fünfprozentigen Schritten visualisiert, die ihre Neigung angeben. Die Anzahl der Profile wird entlang der Y-Achse angegeben und die Tendenzwerte werden entlang der X-Achse angegeben.

>[!NOTE]
>
>Wenn es sich bei der Visualisierung um eine Konversion-Tendenzbewertung handelt, werden die hohen Werte grün und die niedrigen Punkte rot angezeigt. Wenn Sie die Abwanderungsneigung vorhersagen, wird diese gespiegelt, die hohen Werte sind rot und die niedrigen Werte grün. Der mittlere Eimer bleibt gelb, unabhängig vom gewählten Tendenztyp.

Das AI-Modell, das die Tendenzwerte bestimmt, wird aus der Dropdown-Auswahl unter dem Widget-Titel ausgewählt. Das Dropdown-Menü enthält eine Liste aller konfigurierten Customer AI-Modelle. Wählen Sie aus der Liste der verfügbaren Modelle das passende KI-Modell für Ihre Analyse aus. Wenn kein Customer AI-Modell verfügbar ist, werden Sie durch eine Meldung im Widget angewiesen, mindestens ein Customer AI-Modell zu konfigurieren. Außerdem wird ein Hyperlink zur Konfigurationsseite des Customer AI-Modells bereitgestellt. Anweisungen zum Konfigurieren einer Customer AI-Instanz finden Sie in der Dokumentation [.](../../intelligent-services/customer-ai/user-guide/configure.md)

>[!NOTE]
>
>Wählen Sie das Dropdown-Menü direkt unter dem Tab Übersicht aus, um die Zusammenführungsrichtlinie zu ändern, die bestimmt, welche Profile in die Analyse aufgenommen werden. Eine kurze Beschreibung finden Sie im Abschnitt zu [Zusammenführungsrichtlinien](#merge-policies) oder im Abschnitt [Übersicht über Zusammenführungsrichtlinien](../../profile/merge-policies/overview.md) .

Um zur detaillierten Insight-Seite für das ausgewählte Customer AI-Modell zu navigieren, wählen Sie **[!UICONTROL Modelldetails anzeigen]** aus.

![Das Dashboard &quot;Experience Platform-Zielgruppen&quot;mit dem Widget [!UICONTROL Customer AI distribution of scores] und [!UICONTROL View model details] hervorgehoben.](../images/segments/customer-ai-distribution-of-scores.png)

Die Seite mit detaillierten Modelleinblicken wird angezeigt.

![Die Einblicke-Seite für die Kunden-KI.](../images/profiles/customer-ai-insights-page.png)

Weitere Informationen zu Customer AI finden Sie im Leitfaden zur Benutzeroberfläche von [Discovery Insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

### [!UICONTROL Kunden-KI – Bewertungszusammenfassung] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_scoringSummary"
>title="Bewertungszusammenfassung"
>abstract="Dieses Widget zeigt die Gesamtzahl der bewerteten Profile und kategorisiert sie in hohe, mittlere und niedrige Tendenz. Das Ringdiagramm zeigt die proportionale Zusammensetzung der Gesamtprofile über eine hohe, mittlere und niedrige Tendenz hinweg."

Dieses Widget zeigt die Gesamtzahl der bewerteten Profile und kategorisiert sie in Behälter mit hoher, mittlerer und niedriger Neigung als grün, gelb und rot. Ein Ringdiagramm veranschaulicht die proportionale Zusammensetzung der Gesamtprofile zwischen hohen, mittleren und niedrigen Eigenschaften (grün, gelb und rot). Ein Profil ist qualifiziert für eine hohe Tendenz bei über 75, eine mittlere Neigung zwischen 25 und 74 und eine niedrige Tendenz unter 24. Eine Legende zeigt den Farbcode und die Schwellen der Eigenschaften an. Profilzahlen für die Eigenschaften &quot;Hoch&quot;, &quot;Mittel&quot;und &quot;Niedrig&quot;werden in einem Dialogfeld angezeigt, wenn der Cursor den Mauszeiger über den entsprechenden Abschnitt des Ringdiagramms bewegt.

>[!NOTE]
>
>Wenn es sich bei der Visualisierung um eine Konversion-Tendenzbewertung handelt, werden die hohen Werte grün und die niedrigen Punkte rot angezeigt. Wenn Sie die Abwanderungsneigung vorhersagen, wird diese gespiegelt, die hohen Werte sind rot und die niedrigen Werte grün. Der mittlere Eimer bleibt gelb, unabhängig vom gewählten Tendenztyp.

Das Dropdown-Menü unter dem Widget-Titel enthält eine Liste aller konfigurierten Customer AI-Modelle. Wählen Sie aus der Liste der verfügbaren Modelle das passende KI-Modell für Ihre Analyse aus. Wenn kein Customer AI-Modell verfügbar ist, werden Sie durch eine Meldung im Widget angewiesen, mindestens ein Customer AI-Modell zu konfigurieren. Außerdem wird ein Hyperlink zur Konfigurationsseite des Customer AI-Modells bereitgestellt. Detaillierte Anweisungen finden Sie in der Dokumentation zu [Konfigurieren einer Customer AI-Instanz](../../intelligent-services/customer-ai/user-guide/configure.md) .

>[!NOTE]
>
>Die Gesamtzahl der berechneten Profile hängt von der gewählten Zusammenführungsrichtlinie ab. Um die verwendete Zusammenführungsrichtlinie zu ändern, wählen Sie das Dropdown-Menü direkt unter der Registerkarte Übersicht aus. Eine kurze Beschreibung finden Sie im Abschnitt zu [Zusammenführungsrichtlinien](#merge-policies) oder im Abschnitt [Übersicht über Zusammenführungsrichtlinien](../../profile/merge-policies/overview.md) .

![Das Dashboard Experience Platform-Zielgruppen mit dem Widget Customer AI-Bewertungszusammenfassung wurde hervorgehoben.](../images/segments/customer-ai-scoring-summary.png)

Wählen Sie **[!UICONTROL Modelldetails anzeigen]** aus, um zur detaillierten Insight-Seite für das ausgewählte Customer AI-Modell zu navigieren. Weitere Informationen zu Customer AI finden Sie im Leitfaden zur Benutzeroberfläche von [Discovery Insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## Standard-Widgets {#standard-widgets}

Adobe bietet mehrere standardmäßige Widgets, mit denen Sie verschiedene Metriken für Ihre Zielgruppen visualisieren können. In der [!UICONTROL Widget-Bibliothek] können Sie auch benutzerdefinierte Widgets erstellen und für Ihre gesamte Organisation freigeben. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst den Abschnitt [Widget-Bibliothek – Übersicht](../customize/widget-library.md).

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Zielgruppen-Größe]](#audience-size)
* [[!UICONTROL Reihenfolge der Zielgruppen-Aktivierung]](#audience-activation-order)
* [[!UICONTROL Trend der Zielgruppen-Größe]](#audience-size-trend)
* [[!UICONTROL Trend bei der Änderung der Zielgruppen-Größe]](#audience-size-change-trend)
* [[!UICONTROL Trend der Zielgruppen-Größe nach Identität]](#audience-size-trend-by-identity)
* [[!UICONTROL Zielgruppenüberschneidung]](#audience-overlap)
* [[!UICONTROL Bericht zur Zielgruppenüberschneidung]](#audience-overlap-report)
* [[!UICONTROL Identitätsüberschneidung]](#identity-overlap)
* [[!UICONTROL Profile nach Identität]](#profiles-by-identity)
* [[!UICONTROL Geplante Aktivierungen]](#scheduled-activations)

### [!UICONTROL Zielgruppen-Größe] {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesize"
>title="Zielgruppen-Größe"
>abstract="Dieses Widget zeigt die Gesamtzahl der zusammengeführten Profile innerhalb der ausgewählten Zielgruppe an. Diese Zahl hängt von der auf Ihre Daten angewendeten Zusammenführungsrichtlinie ab und ist zum Zeitpunkt der letzten Momentaufnahme korrekt."

Das Widget **[!UICONTROL Zielgruppengröße]** zeigt die Gesamtzahl der zusammengeführten Profile innerhalb der ausgewählten Zielgruppe zum Zeitpunkt der Aufnahme an. Diese Zahl ist das Ergebnis der Anwendung der Zielgruppen-Zusammenführungsrichtlinie auf Ihre Profildaten, um Profilfragmente zusammenzuführen und für jede Einzelperson in der Zielgruppe ein Profil zu erstellen.

Weiterführende Informationen zu Fragmenten und zusammengeführten Profilen finden Sie in der [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md) .

![Die Übersicht über das Dashboard [!UICONTROL Zielgruppen] mit dem Widget [!UICONTROL Zielgruppengröße] ist hervorgehoben.](../images/audiences/audience-size.png)

### [!UICONTROL Trend der Zielgruppen-Größe] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_audiencesizetrend"
>title="Trend der Zielgruppen-Größe"
>abstract="Dieses Widget liefert Informationen zur Gesamtanzahl der Profile, die den Kriterien **einer beliebigen** Segmentdefinition entsprechen und die während des täglichen Snapshots in den letzten 30 Tagen, 90 Tagen oder 12 Monate erfasst wurden."

Das Widget **[!UICONTROL Trend zur Zielgruppengröße]** bietet eine Liniendiagrammdarstellung für die Gesamtanzahl der Profile, die für die **beliebige** -Zielgruppe in einem bestimmten Zeitraum qualifiziert sind. Die Entwicklung der Zielgruppengröße kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Zielgruppengröße wird auf der Y-Achse und die Zeit auf der X-Achse dargestellt.

Dieses Widget enthält auch die automatische Funktion [!UICONTROL Untertitel] , bei der ein Modell für maschinelles Lernen das Diagramm und die Zielgruppendaten analysiert und automatisch Untertitel generiert, um die wichtigsten Trends und wichtigen Ereignisse zu beschreiben. Wählen Sie **[!UICONTROL Beschriftungen]** aus, um das Dialogfeld für automatische Beschriftungen zu öffnen.

![Die Übersicht über [!UICONTROL Zielgruppen] zeigt das Trend-Widget zur Zielgruppengröße an.](../images/audiences/audience-size-trend-captions.png)

Das Dialogfeld für automatische Beschriftungen wird geöffnet und bietet Einblicke in Ihre Daten.

![Das Dialogfeld für automatische Beschriftungen für das Widget „Entwicklung der Zielgruppengröße“.](../images/audiences/audience-size-trend-automatic-captions-dialog.png)

Weitere Informationen zur Auswertung von Zielgruppen und zur Qualifizierung und Ausstieg von Profilen finden Sie in der Dokumentation zum [Segmentation Service](../../segmentation/home.md).

### [!UICONTROL Trend bei der Änderung der Zielgruppen-Größe] {#audience-size-change-trend}

Dieses Widget bietet eine Liniendiagramm, die die Differenz zwischen der Gesamtanzahl der Profile, die sich für eine bestimmte Zielgruppe qualifiziert haben, und den letzten täglichen Momentaufnahmen veranschaulicht. Die für die Analyse ausgewählte Audience wird im Dropdown-Menü Übersicht ausgewählt. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt. Die Zielgruppengröße wird auf der Y-Achse und die Zeit auf der X-Achse dargestellt.

![Das Widget „Entwicklung der Veränderung der Zielgruppengröße“](../images/audiences/audience-size-change-trend.png)

### [!UICONTROL Trend der Zielgruppen-Größe nach Identität] {#audience-size-trend-by-identity}

Dieses Widget veranschaulicht den Trend zur Zielgruppengröße für eine bestimmte Zielgruppe basierend auf dem Identitätstyp, der im Widget-Dropdown-Menü ausgewählt wird. Die für die Analyse verwendete Audience wird aus der Dropdown-Liste Übersicht ausgewählt. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Der Zeitraum wird aus einem Dropdown-Menü im Widget ausgewählt.

![Das Widget „Entwicklung der Zielgruppengröße nach Identität“](../images/audiences/audience-size-trend-by-identity.png)

### [!UICONTROL Reihenfolge der Zielgruppen-Aktivierung] {#audience-activation-order}

Das Widget [!UICONTROL Zielgruppenaktivierungsreihenfolge] enthält eine dreiseitige Tabelle, in der der Zielname, die Plattform und das Aktivierungsdatum der Zielgruppe aufgelistet sind. Die Liste ist entsprechend der Aktualität von oben nach unten geordnet und kann bis zu 10 Zeilen enthalten.

![Das Widget „Reihenfolge der Zielgruppenaktivierung“](../images/audiences/audience-activation-order.png)

### [!UICONTROL Zielgruppenüberschneidung] {#audience-overlap}

Dieses Widget verwendet ein Venn-Diagramm, um die Anzahl der Personen zu visualisieren, die den Kriterien für beide Zielgruppen entsprechen. Die zum Vergleich verwendeten Zielgruppen werden aus den Widget-Dropdown-Menüs ausgewählt. Die Gesamtzahl der in der relevanten Segmentdefinition enthaltenen Profile kann durch Bewegen des Mauszeigers über einen Kreis oder die Schnittmenge des Venn-Diagramms angezeigt werden.

Mit diesem Widget können Sie Ihre Segmentierungsstrategie optimieren, indem Sie die Ähnlichkeiten in den Ergebnissen Ihrer Segmentdefinitionen visualisieren.

![Das Widget „Zielgruppenüberschneidung“.](../images/audiences/audience-overlap.png)

### [!UICONTROL Bericht zur Zielgruppenüberschneidung] {#audience-overlap-report}

Dieses Widget enthält eine tabellarische Darstellung der Profilüberlagerungsdaten für eine bestimmte Zielgruppe. Eine Liste mit fünf Zielgruppen, die von den Prozentsätzen der höchsten bis zur niedrigsten Überschneidung sortiert sind, wird für die aus dem Dropdown-Menü am oberen Bildschirmrand ausgewählte Zielgruppe bereitgestellt. Aus Gründen der Klarheit wird Ihre ausgewählte Zielgruppe in der Spalte [!UICONTROL ZIELGRUPPE A NAME] aufgeführt. Die Analyse der Zielgruppenüberschneidung wird für die zweite Zielgruppe bereitgestellt, die in der Spalte [!UICONTROL ZIELGRUPPE B NAME] aufgeführt ist. Die prozentuale Überschneidung wird in der dritten Spalte auf zwölf Dezimalstellen genau angegeben.

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

Wählen Sie **[!UICONTROL Schließen]** aus, um zum Dashboard [!UICONTROL Zielgruppen] zurückzukehren.

### [!UICONTROL Identitätsüberschneidung] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_identityoverlap"
>title="Identitätsüberschneidung"
>abstract="Dieses Widget zeigt die Überschneidung von Profilen in der Zielgruppe an, die beide ausgewählten Identitäten enthalten. Die Kreise zeigen die relative Größe jeder Identität an. Die Anzahl der Profile, die beide Namespaces enthalten, wird durch den Überschneidungsbereich der Kreise dargestellt."

Das Widget **[!UICONTROL Identitätsüberschneidung]** zeigt ein Venn-Diagramm oder Set-Diagramm an, das die Überschneidung von Profilen in Ihrer Zielgruppe mit mehreren Identitäten anzeigt.

Verwenden Sie die Dropdown-Menüs im Widget, um die Identitäten auszuwählen, die Sie vergleichen möchten. Die Kreise zeigen die relative Größe jeder ausgewählten Identität an, wobei die Anzahl der Profile, die beide Namespaces enthalten, der Größe des Überschneidungsbereichs der Kreise entspricht.

Wenn ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Identitäten zugeordnet. In dieser Situation ist es wahrscheinlich, dass Ihr Unternehmen über mehrere Profile verfügt, die Fragmente aus mehreren Identitäten enthalten.

Weitere Informationen zu Identitäten finden Sie in der Dokumentation zum [Identitätsdienst](../../identity-service/home.md) .

![Die Übersicht über das Dashboard [!UICONTROL Zielgruppen] mit dem Widget zur Identitätsüberschneidung wurde hervorgehoben.](../images/audiences/identity-overlap.png)

### [!UICONTROL Profile nach Identität] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_profilesbyidentity"
>title="Profile nach Identität"
>abstract="Dieses Widget zeigt die Aufschlüsselung der Identitäten für jedes zusammengeführte Profil in der ausgewählten Zielgruppe an."

Das Widget **[!UICONTROL Profile nach Identität]** zeigt die Aufschlüsselung der Identitäten für jedes zusammengeführte Profil in Ihrer ausgewählten Zielgruppe an. Die Gesamtzahl der Profile nach Identität kann höher sein als die Gesamtzahl der Profile in der Zielgruppe, da einem Profil mehrere Identitäten zugeordnet sein können. Das heißt, dass die Summe der für jede Identität angezeigten Werte die Gesamtgröße der Zielgruppe übersteigen kann. Dies liegt daran, dass bei der Interaktion eines Kunden mit Ihrer Marke auf mehr als einem Kanal mehrere Identitäten mit diesem einzelnen Kunden verknüpft werden können.

Wählen Sie **[!UICONTROL Beschriftungen]** aus, um das Dialogfeld für automatische Beschriftungen zu öffnen.

![Die Übersicht über das Dashboard [!UICONTROL Zielgruppen] mit der Option Profile nach Identitäts-Widget und Beschriftungen hervorgehoben.](../images/audiences/profiles-by-identity.png)

Ein maschinelles Lernmodell generiert automatisch Dateneinblicke, indem es die Gesamtverteilung und die Schlüsselaspekte der Daten analysiert.

Weitere Informationen zu Identitäten finden Sie in der Dokumentation zum [Identitätsdienst](../../identity-service/home.md) .

### Geplante Aktivierungen {#scheduled-activations}

Das Widget [!UICONTROL Geplante Aktivierungen] bietet eine tabellarische Übersicht über die zuletzt aktivierten Ziele. Die Tabelle enthält die Zielplattform, den Namen Ihres Aktivierungsflusses zu diesem Ziel sowie das Start- und Enddatum der Aktivierung für die ausgewählte Zielgruppe. Wenn für die Aktivierung kein Enddatum angegeben wurde, wird sie als [!UICONTROL Fortaufend] angezeigt. Die Zielgruppe für die Analyse wird oben auf der Seite aus dem Dropdown-Menü ausgewählt.

Mit diesem Widget können Sie auf einen Blick erkennen, wo und wann die Zielgruppe aktiviert wird, und es macht doppelte oder unnötige Aktivierungen transparenter. Diese gesammelten Informationen zeigen auch, wo jegliche Aktivierungen ausgeschlossen wurden.

![Das Widget „Geplante Aktivierungen“.](../images/audiences/scheduled-activations.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt das Dashboard [!UICONTROL Zielgruppen] finden und eine anzuzeigende Zielgruppe auswählen können. Sie sollten auch die Metriken verstehen, die in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Zielgruppen in der Experience Platform-Benutzeroberfläche finden Sie im Handbuch zur Benutzeroberfläche von [Segmentation Service](../../segmentation/ui/overview.md).
