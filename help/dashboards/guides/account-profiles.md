---
title: Dashboard "Kontoprofile"
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu den B2B-Kontoprofilen Ihres Unternehmens anzeigen können.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: b6811d447f76a671adc98bddef6e760c8be8cd9b
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 4%

---

# Dashboard [!UICONTROL Kontoprofile]

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu Ihren Kontoprofilen anzeigen können, die in einer täglichen Momentaufnahme erfasst werden. In diesem Handbuch wird beschrieben, wie Sie auf das Dashboard [!UICONTROL Kontoprofile] in der Benutzeroberfläche zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Visualisierungen.

Dieses Dokument bietet einen Überblick über die Funktionen des Dashboards [!UICONTROL Kontoprofile] und beschreibt die verfügbaren Standardeinblicke. Umfassende Informationen zu den verfügbaren Funktionen finden Sie im Leitfaden zur Benutzeroberfläche von [[!UICONTROL Kontoprofile]](../../rtcdp/accounts/account-profile-ui-guide.md) .

## Erste Schritte

Sie müssen über die Berechtigung [Adobe Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) verfügen, um auf das Dashboard &quot;B2B [!UICONTROL Kontoprofile]&quot;zuzugreifen.

## Kontoprofildaten {#data}

Das Dashboard [!UICONTROL Kontoprofile] zeigt eine Momentaufnahme Ihrer einheitlichen Kontoinformationen an. Diese Kontoinformationen stammen aus verschiedenen Quellen in Ihren Marketing-Kanälen und den verschiedenen Systemen, die Ihr Unternehmen derzeit zum Speichern von Kundenkontoinformationen verwendet.

Die Profildaten im Schnappschuss zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem der Schnappschuss erstellt wurde. Mit anderen Worten, der Schnappschuss ist keine Annäherung oder kein Beispiel der Daten, und das Dashboard [!UICONTROL Kontoprofile] wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Dashboard [!UICONTROL Kontoprofile] {#explore}

Um in der Platform-Benutzeroberfläche zum Dashboard [!UICONTROL Kontoprofile] zu navigieren, wählen Sie im linken Navigationsbereich unter [!UICONTROL Konten] die Option **[!UICONTROL Profile]** aus.

![Die Platform-Benutzeroberfläche mit Kontoprofilen im linken Navigationsbereich wurde hervorgehoben und die Registerkarte &quot;Übersicht&quot;wurde angezeigt.](../images/account-profiles/account-profiles-dashboard.png)

Im Dashboard [!UICONTROL Kontoprofile] können Sie entweder [ die in Ihrer Organisation erfassten Kontoprofile durchsuchen](#browse-account-profiles) oder [die Gesamtheit Ihrer Kontoprofildaten mithilfe von Widgets](#standard-widgets) auf einen Blick anzeigen.

### Datumsfilter {#date-filter}

Die Registerkarte [!UICONTROL Übersicht] besteht aus Widgets, die schreibgeschützte Metriken bereitstellen, die wichtige Informationen zu Ihren Kontoprofilen vermitteln. Wählen Sie das Kalendersymbol oder die Daten aus, um den globalen Datumsfilter für Ihre Widgets zu ändern.

>[!IMPORTANT]
>
>Der Datumsbereich, den Sie im Dropdown-Kalender auswählen, wirkt sich auf alle Einblicke mit Ausnahme der beiden prädiktiven Scoring-Widgets ([Verteilung](#predictive-scoring-distribution) und [Einflussfaktoren](#predictive-scoring-top-influential-factors)) aus.

![Die Registerkarte Übersicht über Kontoprofile mit hervorgehobener Datumsauswahl und Filtersymbol.](../images/account-profiles/date-filter.png)

### Konfigurieren des Leads zum Kontoabgleichdienst {#lead-to-account-matching-service}

Wählen Sie **[!UICONTROL Einstellungen]** aus, um den Lead für den Dienst zum Abgleichen von Konten im Dialogfeld [!UICONTROL Kontoeinstellungen] zu konfigurieren. Ausführliche Informationen zum Konfigurieren Ihres Leads für die Kontoübereinstimmung finden Sie im [UI-Handbuch](../../rtcdp/accounts/account-profile-ui-guide.md#configure-lead-to-account-matching). Weiterführende Informationen zum Abgleich von Leads mit Konten finden Sie in der B2B-Dokumentation zu Real-Time CDP im Abschnitt [Lead zum Abgleich von Konten](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) .

![Das Dashboard &quot;Kontoprofile&quot;mit hervorgehobenen Einstellungen.](../images/account-profiles/settings.png)

## Durchsuchen von Account-Profilen {#browse-account-profiles}

Auf der Registerkarte [!UICONTROL Durchsuchen] können Sie die schreibgeschützten Kontoprofile durchsuchen und anzeigen, die in Ihre Organisation aufgenommen wurden. Verwenden Sie eine Konto-ID aus einer verbundenen Unternehmensquelle oder geben Sie Quelldetails direkt ein. In diesem Arbeitsbereich können Sie wichtige Informationen aus dem Kontoprofil sehen, einschließlich Name, Branche, Umsatz und Zielgruppe.

Wählen Sie die [!UICONTROL Profil-ID] aus den Ergebnissen aus, die auf der Registerkarte [!UICONTROL Durchsuchen] angezeigt werden, um die Registerkarte [!UICONTROL Details] für das Kontoprofil zu öffnen.

![Die Registerkarte &quot;Durchsuchen von Kontoprofilen&quot;mit den angezeigten Ergebnissen und der hervorgehobenen Profil-ID.](../images/account-profiles/account-profiles-browse-tab.png)

Die auf der Registerkarte [!UICONTROL Details] angezeigten Kontoprofilinformationen wurden aus mehreren Profilfragmenten zusammengeführt, um eine einzige Ansicht des einzelnen Kontos zu bilden. Weitere Informationen zu den Anzeigefunktionen von Kontoprofilen in der Platform-Benutzeroberfläche finden Sie in der Dokumentation zum Durchsuchen von Kontoprofilen in Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) .[

## Standard-Widgets {#standard-widgets}

Adobe stellt standardmäßige Widgets bereit, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Kontoprofilen visualisieren können.

>[!IMPORTANT]
>
>Wenn Sie keinen Datumsfilter bereitstellen, analysiert das Standardverhalten von Insights Daten, die aus dem Vorjahr bis heute hinzugefügt wurden.

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [Hinzugefügte Kontoprofile](#account-profiles-added)
* [Neue Abschlüsse nach Wirtschaftszweigen](#accounts-by-industry)
* [Neue Konten nach Typ](#accounts-by-type)
* [Neue Möglichkeiten für die Rolle der Person](#opportunities-by-person-role)
* [Neue Einnahmenmöglichkeiten](#opportunities-by-revenue)
* [Neue Möglichkeiten nach Status und Phase](#opportunities-by-status-&-stage)
* [Neue Chancen gewonnen](#opportunities-won)
* [Hinzugefügte Opportunities](#opportunities-added)
* [Verteilung der prädiktiven Bewertung](#predictive-scoring-distribution)
* [Prädiktive Bewertung - wichtigste Einflussfaktoren](#predictive-scoring-top-influential-factors)

### Hinzugefügte Kontoprofile {#account-profiles-added}

Das Widget [!UICONTROL Hinzugefügte Kontoprofile] verwendet ein Liniendiagramm, um die Anzahl der Kontoprofile anzuzeigen, die jeden Tag über einen bestimmten Zeitraum hinzugefügt wurden. Verwenden Sie den globalen Datumsfilter oben im Dashboard, um den Analysezeitraum zu bestimmen. Wenn kein Datumsfilter angegeben wird, werden im Standardverhalten die Kontoprofile aufgelistet, die für das Jahr vor dem aktuellen Datum hinzugefügt wurden. Die Ergebnisse können verwendet werden, um einen Trend bei der Anzahl der hinzugefügten Kontoprofile zu erkennen.

![Das Widget Kontoprofile hinzugefügt.](../images/account-profiles/account-profiles-added.png)

### Neue Abschlüsse nach Wirtschaftszweigen {#accounts-by-industry}

Das Widget [!UICONTROL Neue Konten nach Branche] zeigt die Gesamtanzahl der Konten in einer einzelnen Metrik innerhalb eines Ringdiagramms an. Das Ringdiagramm zeigt die relative Zusammensetzung der verschiedenen Branchen, aus denen diese Summe besteht. Ein farbkodierter Schlüssel bietet eine Aufschlüsselung aller eingeschlossenen Branchen. Einzelne Zahlen für jede Branche werden in einem Dialogfeld angezeigt, wenn der Cursor den Mauszeiger über den entsprechenden Abschnitt des Ringdiagramms bewegt.

![Die neuen Konten nach Branchen-Widget.](../images/account-profiles/new-accounts-by-industry.png)

### Neue Konten nach Typ {#accounts-by-type}

Das Widget [!UICONTROL Neue Konten nach Typ] zeigt die Gesamtanzahl der Konten in einer einzelnen Metrik innerhalb eines Ringdiagramms an. Das Ringdiagramm zeigt die relative Zusammensetzung der verschiedenen Kontotypen, aus denen diese Summe besteht. Ein farbcodierter Schlüssel bietet eine Aufschlüsselung aller enthaltenen Kontotypen. Einzelne Zählungen für jeden Kontotyp werden in einem Dialogfeld angezeigt, wenn der Cursor den Mauszeiger über den entsprechenden Abschnitt des Ringdiagramms bewegt.

![Die neuen Konten nach Typ-Widget.](../images/account-profiles/new-accounts-by-type.png)

### Neue Möglichkeiten für die Rolle der Person {#opportunities-by-person-role}

Das Widget [!UICONTROL Neue Möglichkeiten nach Benutzerrolle] zeigt die Gesamtanzahl Ihrer Möglichkeiten in einer einzelnen Metrik innerhalb eines Ringdiagramms an. Das Ringdiagramm zeigt die relative Zusammensetzung der Rollen, die diese Gesamtzahl von Möglichkeiten ausmachen. Ein farbkodierter Schlüssel bietet eine Aufschlüsselung aller enthaltenen Rollen. Einzelne Zahlen für jede Rolle werden in einem Dialogfeld angezeigt, wenn der Cursor den Mauszeiger über den entsprechenden Abschnitt des Ringdiagramms bewegt.

>[!NOTE]
>
>Der Fehler &quot;[!UICONTROL Keine Daten gefunden]&quot;oder &quot;[!UICONTROL Kann nicht geladen werden]&quot; wird ausgelöst, wenn die &quot;Opportunity-Person&quot;-Bridge-Tabelle in Ihrem Schema nicht verwendet wird. Wenn in Ihrem Insight einer dieser Fehler angezeigt wird, überprüfen Sie Ihr Vereinigungsschema und stellen Sie sicher, dass die Feldergruppe &quot;Chancen - Person&quot;Daten erfasst.

![Das Widget Neue Möglichkeiten nach Rollen für Personen.](../images/account-profiles/new-opportunities-by-person-role.png)

### Neue Einnahmenmöglichkeiten {#opportunities-by-revenue}

Das Widget [!UICONTROL Neue Möglichkeiten nach Umsatz] verwendet ein Balkendiagramm, um den geschätzten Gesamtumsatz zu veranschaulichen, der durch Ihre Möglichkeiten generiert wurde. Das Widget unterstützt bis zu sechs Möglichkeiten.

Um ein Dialogfeld zu sehen, das die spezifische Umsatzsumme für eine Gelegenheit enthält, verwenden Sie den Cursor, um den Mauszeiger über einzelne Balken zu bewegen.

![Das Widget Neue Möglichkeiten nach Umsatz .](../images/account-profiles/new-opportunities-by-revenue.png)

### Neue Möglichkeiten nach Status &amp; Phase {#opportunities-by-status-&-stage}

Dieses Widget verwendet ein Balkendiagramm, um die Anzahl der Möglichkeiten zu veranschaulichen, die in allen Phasen des Marketing-/Verkaufstrichter geöffnet oder geschlossen sind. Das Widget verwendet Farben, um die Stufe der Möglichkeiten zu differenzieren. Ein farbkodierter Schlüssel zeigt die verfügbaren Phasen für Gelegenheiten an.

![Die neuen Möglichkeiten nach Status- und Staging-Widget.](../images/account-profiles/new-opportunities-by-status-&-stage.png)

### Neue Chancen gewonnen {#opportunities-won}

Das Widget [!UICONTROL Neue Möglichkeiten gewonnen] zeigt die Gesamtzahl Ihrer Möglichkeiten an, die erfolgreich in einer einzelnen Metrik innerhalb eines Ringdiagramms abgeschlossen wurden. Das Ringdiagramm veranschaulicht die relative Zusammensetzung der Chancen, die entweder gewonnen werden oder nicht. Ein farbkodierter Schlüssel unterscheidet zwischen erfolgreichen und nicht erfolgreichen Möglichkeiten. Einzelne Zahlen für jede Rolle werden in einem Dialogfeld angezeigt, wenn der Cursor den Mauszeiger über den entsprechenden Abschnitt des Ringdiagramms bewegt.

![Das Widget &quot;Neue Möglichkeiten&quot;wurde gewonnen.](../images/account-profiles/new-opportunities-won.png)

### Hinzugefügte Opportunities {#opportunities-added}

Das Widget [!UICONTROL Hinzugefügte Möglichkeiten] verwendet ein Liniendiagramm, um die Anzahl der Möglichkeiten anzuzeigen, die jeden Tag über einen bestimmten Zeitraum hinzugefügt werden. Verwenden Sie den globalen Datumsfilter oben im Dashboard, um den Analysezeitraum zu bestimmen. Wenn kein Datumsfilter angegeben wird, werden im Standardverhalten die Chancen aufgeführt, die für das Jahr vor dem heutigen hinzugefügt wurden. Die Ergebnisse können dazu dienen, einen Trend bei der Anzahl der hinzugefügten Chancen zu erkennen.

<!-- Link to date filter documentation from Annamalai -->

![Das Widget &quot;Chancen&quot;wurde hinzugefügt.](../images/account-profiles/opportunities-added.png)

### Verteilung der prädiktiven Bewertung {#predictive-scoring-distribution}

Das Widget [!UICONTROL Prädiktive Scoring-Verteilung] zeigt die Verteilung der Punktzahl aller Kontoprofile, damit Sie den Zustand Ihrer Verkaufspipelines auf einen Blick verstehen können. Die Scoring-Daten werden über ein Ringdiagramm und ein Spaltendiagramm übermittelt.

Die Ringdiagramm veranschaulicht den Anteil Ihrer gesamten Kontoprofile an den einzelnen Bereichen mit der hohen, mittleren und niedrigen Kaufneigung. Der Schlüssel enthält weitere Details zu den farbcodierten Abschnitten, einschließlich der Scoring-Bucket-Bereiche und der Anzahl der Kontoprofile in diesem Bereich.

Das Spaltendiagramm bietet eine detailliertere Scoring-Aufschlüsselung. Jede Spalte zeigt die Anzahl der Kontoprofile in jedem der 20 in 5-Punkt-Schritten zusammengefassten Behälter an.

Über das Dropdown-Menü im Widget können Sie das Konto-Scoring-Modell auswählen.

>[!NOTE]
>
>Globale Datumsbereichsfilter gelten nicht für prädiktive Scoring-Einblicke. Prädiktive Scoring-Widgets analysieren Daten basierend auf dem im Dropdown-Menü ausgewählten Konto-Scoring-Modell.

![Das Verteilungs-Widget &quot;Prädiktive Scoring&quot;.](../images/account-profiles/predictive-scoring-distribution.png)

### Prädiktive Bewertung - wichtigste Einflussfaktoren {#predictive-scoring-top-influential-factors}

Das Widget [!UICONTROL Einflussfaktoren für prädiktive Scoring] hilft Ihnen, die wichtigsten Faktoren zu verstehen, die die Ergebnisse für jeden Tendenzbehälter steuern.

Dieses Widget zeigt die wichtigsten Einflussfaktoren für die einzelnen Bereiche mit hoher, mittlerer und niedriger Tendenz. Ein Balken für jeden Einflussfaktor gibt den Prozentsatz der Kontoprofile in diesem Tendenzbehälter an, der den spezifischen Einflussfaktor enthält.

Über das Dropdown-Menü im Widget können Sie das Konto-Scoring-Modell auswählen.

>[!NOTE]
>
>Globale Datumsbereichsfilter gelten nicht für prädiktive Scoring-Einblicke. Prädiktive Scoring-Widgets analysieren Daten basierend auf dem im Dropdown-Menü ausgewählten Konto-Scoring-Modell.

![Das Widget der wichtigsten Einflussfaktoren für die prädiktive Bewertung.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## Datenfehler kann nicht geladen werden {#errors}

Wenn ein Widget &quot;*[!UICONTROL konnte nicht geladen werden&quot;anzeigt. Versuchen Sie es erneut.]* Dies liegt daran, dass für die B2B-Entität keine Daten verfügbar sind. Beispielsweise zeigt das Widget, das unter [!UICONTROL Neue Möglichkeiten nach Benutzerrolle] angezeigt wird, die Meldung &quot;[!UICONTROL Ladeunfähig. Versuchen Sie es erneut.]&quot;, da diese Sandbox keine Opportunitätsdaten enthält.

![Der Fehler Insight kann nicht geladen werden.](../images/account-profiles/unable-to-load.png)

Um das Problem zu beheben, müssen Sie B2B-Entitätsdaten wie *Opportunity person*-Daten in die Sandbox aufnehmen. Nach 48 Stunden werden die Daten in den Widgets angezeigt.

## Nächste Schritte

In diesem Dokument erfahren Sie, wie Sie das Dashboard [!UICONTROL Kontoprofile] finden und welche Metriken in den verfügbaren Widgets angezeigt werden. Weitere Informationen zum Arbeiten mit Kontoprofilen als Teil Ihrer B2B-Daten in der Experience Platform-Benutzeroberfläche finden Sie in der [Übersicht über Kontoprofile](../../rtcdp/accounts/account-profile-overview.md) für Adobe Real-Time CDP, B2B Edition.
