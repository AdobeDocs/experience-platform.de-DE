---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Benutzeroberfläche;Benutzeroberfläche;Anpassung;Profil-Dashboard;Dashboard
title: Handbuch zum Ziele-Dashboard
description: Adobe Experience Platform verfügt über ein Dashboard, in dem Sie wichtige Informationen über die aktiven Ziele Ihrer Organisation anzeigen können.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: d9e10271db52f61cdc3e4adc546fe05adadb5a46
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 93%

---

# Dashboard [!UICONTROL Ziele]

Die Benutzeroberfläche von Adobe Experience Platform verfügt über ein Dashboard, in dem Sie wichtige Informationen über die aktiven Ziele Ihres Unternehmens anzeigen können, die in einem täglichen Schnappschuss erfasst wurden. In diesem Handbuch wird beschrieben, wie Sie in der Benutzeroberfläche auf das Ziele-Dashboard zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie weitere Informationen zu den im Dashboard angezeigten Metriken.

Eine Übersicht über Ziele sowie einen Katalog aller in Experience Platform verfügbaren Ziele finden Sie in der [Dokumentation zu Zielen](../../destinations/home.md).

## Daten des [!UICONTROL Ziele]-Dashboards {#destinations-dashboard-data}

Im Dashboard „Ziele“ finden Sie eine Momentaufnahme der Ziele, die Ihre Organisation in Experience Platform aktiviert hat. Die Momentaufnahme zeigt die Daten exakt so an, wie sie zum Zeitpunkt der Momentaufnahme aufgetreten sind. Das heißt, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten, und das Ziele-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme der Momentaufnahme an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn die nächste Momentaufnahme erstellt wird.

## Das [!UICONTROL Ziele]-Dashboard erkunden {#explore}

Um in der Platform-Benutzeroberfläche zum Ziele-Dashboard zu gelangen, wählen Sie **[!UICONTROL Ziele]** in der linken Leiste und dann die Registerkarte **[!UICONTROL Übersicht]** aus.

Datum und Uhrzeit des letzten Schnappschusses werden oben in der [!UICONTROL Übersicht] neben dem Ziel-Dropdown-Menü angezeigt. Alle Widget-Daten sind zum Stand dieses Datums und dieser Uhrzeit korrekt. Der Zeitstempel der Momentaufnahme wird im UTC-Format angegeben, nicht in der Zeitzone der jeweiligen Person oder Organisation.

>[!NOTE]
>
>Wenn Experience Platform neu in Ihrem Unternehmen ist und es noch keine aktiven Ziele hat, sind das Ziele-Dashboard und die Registerkarte [!UICONTROL Übersicht] nicht zu sehen. Wenn Sie [!UICONTROL Ziele] über die linke Navigation auswählen, wird stattdessen die Registerkarte [!UICONTROL Katalog] angezeigt. Weitere Informationen über die Registerkarte [!UICONTROL Katalog] finden Sie im Handbuch zum Arbeitsbereich [[!UICONTROL Ziele]](../../destinations/ui/destinations-workspace.md).

![Die Ziele-Übersicht der Platform-Benutzeroberfläche mit hervorgehobenem aktuellem Schnappschuss.](../images/destinations/snapshot-timestamp.png)

### Das [!UICONTROL Ziele]-Dashboard modifizieren {#modify}

Wählen Sie **[!UICONTROL Dashboard modifzieren]** aus, um das Erscheinungsbild des Ziele-Dashboards zu ändern. Dadurch können Sie Widgets im Dashboard verschieben, hinzufügen und entfernen sowie auf die Widget-Bibliothek zugreifen. In der Widget-Bibliothek können Sie die verfügbaren Widgets durchsuchen und benutzerdefinierte Widgets für Ihre Organisation erstellen.

Weitere Informationen finden Sie in der Dokumentation [Dashboards modifzieren](../customize/modify.md) und [Widget-Bibliothek – Übersicht](../customize/widget-library.md).

### Hinzufügen von Widgets {#add-widget}

Wählen Sie **[!UICONTROL Widget hinzufügen]** aus, um zur Widget-Bibliothek zu navigieren und eine Liste der verfügbaren Widgets anzuzeigen, die Sie Ihrem Dashboard hinzufügen können.

![Die Übersicht über das Dashboard „Ziele“ mit der hervorgehobenen Option „Widget hinzufügen“.](../images/destinations/destinations-overview-add-widget.png)

In der Widget-Bibliothek können Sie die standardmäßigen und benutzerdefinierten Segment-Widgets durchsuchen. Informationen zum Hinzufügen von Widgets finden Sie in der Widget-Bibliothek-Dokumentation zum [Hinzufügen eines Widget](../customize/widget-library.md#add-widgets).

## Standard-Widgets {#standard-widgets}

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Ziel-Metriken visualisieren und die Vollständigkeit der für Ihre Datenanalyse verfügbaren Segmente bewerten können. In der [!UICONTROL Widget-Bibliothek] können Sie auch benutzerdefinierte Widgets erstellen und für Ihre gesamte Organisation freigeben. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst den Abschnitt [Widget-Bibliothek – Übersicht](../customize/widget-library.md).

### Voraussetzungen {#prerequisites}

Bevor Sie mit den Beschreibungen der Standard-Widgets fortfahren, sollten Sie mit den Definitionen der folgenden Schlüsselbegriffe vertraut sein, die in der Dokumentation verwendet werden:

* **Segment:** Ein Segment ist **Regelsätze** , die Attribute und Ereignisdaten enthalten, die eine Reihe von Profilen als Zielgruppe qualifizieren.
* **Zielgruppe**: Eine Zielgruppe ist **Profilgruppe** die die Kriterien einer Segmentdefinition erfüllen.
* **Zugeordnet/Zuordnung**: Beim Daten-Mapping werden Quelldatenfelder den zugehörigen Zielfeldern in einem Ziel zugeordnet.
* **Identität**: Eine Identität ist eine Kennung, die einen einzelnen Kunden eindeutig darstellt, z. B. eine Cookie-ID, Geräte-ID oder E-Mail-ID.
* **Aktivieren**: Activate ist die Aktion, die ein Benutzer durchführt, um ein Segment oder Profile einem Ziel wie Oracle Eloqua, Google oder Salesforce-Marketing Cloud zuzuordnen.

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Am häufigsten verwendete Ziele]](#most-used-destinations)
* [[!UICONTROL Kürzlich erstellte Ziele]](#recently-created-destinations)
* [[!UICONTROL Kürzlich aktivierte Segmente]](#recently-activated-segments)
* [[!UICONTROL Kürzlich aktivierte Segmente nach Ziel]](#recently-activated-segments-by-destination)
* [[!UICONTROL Trend der Audience-Größe]](#audience-size-trend)
* [[!UICONTROL Nicht zugeordnete Segmente nach Identität]](#unmapped-segments-by-identity)
* [[!UICONTROL Zugeordnete Segmente nach Identität]](#mapped-segments-by-identity)
* [[!UICONTROL Häufige Zielgruppen]](#common-audiences)
* [[!UICONTROL Zugeordnete Zielgruppen]](#mapped-audiences)
* [[!UICONTROL Zustand der zugeordneten Zielgruppe]](#mapped-audience-health)
* [[!UICONTROL Anzahl von Zielen]](#destinations-count)
* [[!UICONTROL Zielstatus]](#destination-status)
* [[!UICONTROL Aktive Ziele nach Zielplattform]](#active-destinations-by-destination-platform)
* [[!UICONTROL Aktivierte Audiences für alle Ziele]](#activated-audiences-across-all-destinations)
* [[!UICONTROL Aktivierte Zielgruppen]](#activated-audiences)

### [!UICONTROL Am häufigsten verwendete Ziele] {#most-used-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mostuseddestinations"
>title="Am häufigsten verwendete Ziele"
>abstract="Dieses Widget zeigt die aktivsten Ziele Ihres Unternehmens gemessen an der Anzahl der zugeordneten Segmente an. Diese Zahlen sind zum Zeitpunkt des letzten Schnappschusses korrekt. Diese Rangfolge bietet Einblicke, welche Ziele derzeit am häufigsten verwendet werden, und hebt jene hervor, die möglicherweise nicht ausreichend genutzt werden."

Das Widget **[!UICONTROL Am häufigsten verwendete Ziele]** zeigt die wichtigsten Ziele Ihres Unternehmens nach der Anzahl der zugeordneten Segmente ab dem letzten Schnappschuss an. Diese Rangfolge bietet Einblicke, welche Ziele verwendet werden, und zeigt gleichzeitig, welche möglicherweise nicht genügend genutzt werden.

Wenn Sie beispielsweise gestern ein Ziel konfiguriert haben, ihm jedoch keine Segmente zugeordnet haben, können Sie sehen, dass das Ziel derzeit nicht genutzt wird.

Die Anzahl der zugeordneten Segmente, die in der Spalte mit der Segmentanzahl angezeigt wird, ist zum Zeitpunkt des letzten täglichen Schnappschusses korrekt. Wenn Sie dem Ziel ein neues Segment zuordnen, wird die Anzahl erst aktualisiert, wenn der nächste Schnappschuss erstellt wird.

Wenn Sie den Namen eines Ziels aus der im Widget angezeigten Liste auswählen, gelangen Sie zu denselben Zieldetails, die Sie auch über die Registerkarte **[!UICONTROL Durchsuchen]** aufrufen können. Sie können auch **[!UICONTROL Alle anzeigen]** auswählen, um zur Registerkarte **[!UICONTROL Durchsuchen]** zu navigieren, und dann den Namen eines Ziels auswählen, um dessen Details anzuzeigen.

![Auf der Registerkarte „Übersicht“ im Dashboard „Ziele“ ist das Widget „Am häufigsten verwendete Ziele“ hervorgehoben.](../images/destinations/most-used-destinations.png)

### [!UICONTROL Kürzlich erstellte Ziele] {#recently-created-destinations}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlycreateddestinations"
>title="Kürzlich erstellte Ziele"
>abstract="Dieses Widget zeigt eine Liste der zuletzt konfigurierten Ziele in Ihrer Organisation an."

Das Widget **[!UICONTROL Kürzlich erstellte Ziele]** versetzt Sie in die Lage, eine Liste der zuletzt konfigurierten Ziele Ihrer Organisation anzuzeigen.

Das angezeigte Erstellungsdatum entspricht der letzten täglichen Momentaufnahme. Mit anderen Worten: Wenn Sie ein neues Ziel erstellen, wird es erst nach der nächsten Momentaufnahme in der Liste angezeigt.

Wenn Sie den Namen eines Ziels in der im Widget angezeigten Liste auswählen, gelangen Sie zu den Zieldetails, die über die Registerkarte **[!UICONTROL Durchsuchen]** verknüpft sind. Sie können auch auf **[!UICONTROL Alle anzeigen]** klicken, um zur Registerkarte **[!UICONTROL Durchsuchen]** zu navigieren, und dann den Namen eines Ziels auswählen, um dessen Details anzuzeigen.

Weitere Informationen zum Konfigurieren bestimmter Zieltypen finden Sie in der [Dokumentation zu Zielen](../../destinations/home.md).

![Die Registerkarte „Übersicht“ im Dashboard „Ziele“ mit dem hervorgehobenen Widget „Kürzlich erstellte Ziele“.](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Kürzlich aktivierte Segmente] {#recently-activated-segments}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegments"
>title="Kürzlich aktivierte Segmente"
>abstract="Dieses Widget bietet eine Liste der Segmente, die einem Ziel zuletzt zugeordnet wurden. Diese Liste enthält eine Momentaufnahme der Segmente und Ziele, die aktiv im System verwendet werden, und kann bei der Fehlerbehebung bei fehlerhaften Zuordnungen hilfreich sein."

Das Widget **[!UICONTROL Kürzlich aktivierte Segmente]** stellt eine Liste der Segmente bereit, die einem Ziel zuletzt zugeordnet wurden. Diese Liste enthält eine Momentaufnahme der Segmente und Ziele, die aktiv im System verwendet werden, und kann bei der Fehlerbehebung bei fehlerhaften Zuordnungen hilfreich sein.

Das angezeigte aktualisierte Datum zeigt an, wann das Segment zuletzt für das Ziel aktiviert wurde, und ist für die letzte tägliche Momentaufnahme korrekt. Wenn Sie also ein Segment für das Ziel aktivieren, ändert sich das aktualisierte Datum erst, nachdem die nächste Momentaufnahme erstellt wurde.

Wenn Sie den Namen eines Segments in der im Widget angezeigten Liste auswählen, gelangen Sie zu den Segmentdetails. Sie können auch auf **[!UICONTROL Alle anzeigen]** klicken, um zur Registerkarte zum Durchsuchen von Segmenten zu navigieren und dann den Namen eines Segments auszuwählen, um dessen Details anzuzeigen.

Weitere Informationen zum Arbeiten mit Segmenten in Experience Platform finden Sie in der [Übersicht über den Segmentierungs-Service](../../segmentation/home.md).

![Die Registerkarte „Übersicht“ im Dashboard „Ziele“ mit dem hervorgehobenem Widget „Kürzlich aktivierte Segmente“.](../images/destinations/recently-activated-segments.png)

### [!UICONTROL Kürzlich aktivierte Segmente nach Ziel] {#recently-activated-segments-by-destination}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_recentlyactivatedsegmentsbydestination"
>title="Kürzlich aktivierte Segmente nach Ziel"
>abstract="Dieses Widget zeigt die fünf am häufigsten aktivierten Segmente in absteigender Reihenfolge für das im Dropdown-Menü „Übersicht“ ausgewählte Ziel an."

Das Widget **[!UICONTROL Kürzlich aktivierte Segmente nach Ziel]** zeigt die fünf am häufigsten aktivierten Segmente in absteigender Reihenfolge für das im Dropdown-Menü „Übersicht“ ausgewählte Ziel an. Es ähnelt dem Widget [!UICONTROL Kürzlich aktivierte Segmente], doch gelten die angezeigten Daten **nur** für das ausgewählte Ziel.

Dieses Widget enthält zwei Metriken: den Segmentnamen und das Datum, an dem das Segment zuletzt für das Ziel aktiviert wurde. Die angezeigten Daten sind zum Zeitpunkt der letzten täglichen Momentaufnahme korrekt.

Sie können die Details eines Segments anzeigen, indem Sie den Namen eines Segments in der angezeigten Liste auswählen.

![Das Widget „Kürzlich aktivierte Segmente nach Ziel“.](../images/destinations/recently-activated-segments-by-destination.png)

Weitere Informationen finden Sie im Abschnitt Voraussetzungen für das [verwendete Begriffsdefinitionen](#prerequisites) in dieser Beschreibung.

### [!UICONTROL Trend der Audience-Größe] {#audience-size-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_audiencesizetrend"
>title="Trend der Audience-Größe"
>abstract="Dieses Widget veranschaulicht die Anzahl der im Segment enthaltenen Profile, die täglich an das Zielkonto gesendet werden. Mit dem ersten Dropdown-Menü wird der Zeitraum für die Entwicklung der Zielgruppe angepasst. Im zweiten Dropdown-Menü des Widgets wird das Segment für die Analyse ausgewählt. Das Ziel wird im Dropdown-Menü „Übersicht“ ausgewählt."

Das Widget **[!UICONTROL Entwicklung der Zielgruppengröße]** zeigt die Beziehung der Profilanzahl über einen bestimmten Zeitraum für ein Segment an, das diesem Zielkonto zugeordnet wurde. Im Widget wird mit einem Liniendiagramm die Anzahl der im Segment enthaltenen Profile, die täglich an das Zielkonto gesendet werden, veranschaulicht.

Ein Zeitraum für die Entwicklung der Zielgruppe in den letzten 30 Tagen, 90 Tagen oder 12 Monaten kann über das erste Dropdown-Menü angepasst werden.

Im zweiten Dropdown-Menü werden alle verfügbaren Segmente aufgelistet, die an das im oberen Bereich des Dashboards ausgewählte Zielkonto gesendet werden können.

![Das Widget „Entwicklung der Zielgruppengröße“.](../images/destinations/audience-size-trend.png)

Das Widget **[!UICONTROL Entwicklung der Zielgruppengröße]** enthält oben rechts eine Schaltfläche [!UICONTROL Beschriftungen]. Wählen Sie **[!UICONTROL Beschriftungen]** aus, um den Dialog „Automatische Beschriftungen“ zu öffnen. Ein Modell für maschinelles Lernen generiert automatisch Beschriftungen zur Beschreibung der wichtigsten Trends und Ereignisse, indem Diagramm- und Segmentdaten analysiert werden.

![Das Dialogfeld für automatische Beschriftungen für das Widget „Entwicklung der Zielgruppengröße“.](../images/destinations/audience-size-trend-captions.png)

### [!UICONTROL Nicht zugeordnete Segmente nach Identität] {#unmapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_unmappedsegmentsbyidentity"
>title="Nicht zugeordnete Segmente nach Identität"
>abstract="Dieses Widget listet die fünf häufigsten **nicht zugeordneten** Segmente auf, die nach absteigender Identitätsanzahl für ein bestimmtes Ziel und eine bestimmte Identität angeordnet werden. Die Filter-IDs, die im Dropdown-Menü des Widgets aufgeführt sind, ändern sich je nach dem Zielkonto, das oben auf der Übersichtsseite ausgewählt wurde."

Das Widget **[!UICONTROL Nicht zugeordnete Segmente nach Identität]** listet die fünf häufigsten **nicht zugeordneten** Segmente auf, die nach absteigender Identitätsanzahl für ein bestimmtes Ziel und eine bestimmte Identität angeordnet sind. Es werden Segmente hervorgehoben, die basierend auf der ausgewählten ID dem ausgewählten Zielkonto am besten zugeordnet werden können.

Das Dropdown-Menü „Ziel-ID“ filtert Ihre verfügbaren Segmente. Die im Dropdown-Menü aufgelisteten Filter-IDs ändern sich je nach dem Zielkonto, das oben auf der Übersichtsseite ausgewählt wurde.

Die Spalte „Identitäten“ zählt die Anzahl der im Segment vorhandenen Quell-IDs, die der in der Dropdown-Liste „Widget-ID“ ausgewählten ID zugeordnet werden könnten.

![Das Widget „Nicht zugeordnete Segmente nach Identität“.](../images/destinations/unmapped-segments-by-identity.png)

Weitere Informationen finden Sie im Abschnitt Voraussetzungen für das [verwendete Begriffsdefinitionen](#prerequisites) in dieser Beschreibung.

### [!UICONTROL Zugeordnete Segmente nach Identität] {#mapped-segments-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedsegmentsbyidentity"
>title="Zugeordnete Segmente nach Identität"
>abstract="Dieses Widget listet die fünf häufigsten **zugeordneten** Segmente auf. Die Liste wird in absteigender Reihenfolge nach der Anzahl der in den Segmenten enthaltenen Quell-IDs sortiert. Die zu zählende Ziel-ID wird aus dem Dropdown-Menü unter dem Widget-Titel ausgewählt. Die in der Widget-Dropdown-Liste verfügbaren Ziel-IDs hängen vom oben im Dashboard „Übersicht“ ausgewählten Ziel ab."

Dieses Widget listet die fünf häufigsten **zugeordneten** Segmente auf. Die Liste wird in absteigender Reihenfolge nach der Anzahl der in den Segmenten enthaltenen Quell-IDs sortiert. Die zu zählende Ziel-ID wird aus dem Dropdown-Menü unter dem Widget-Titel ausgewählt. Die Ziel-IDs, die über die Dropdown-Liste im Widget verfügbar sind, ändern sich entsprechend dem Zielkontofilter, der oben im Dashboard „Übersicht“ ausgewählt wird.

![Widget „Zugeordnete Segmente nach Identität“.](../images/destinations/mapped-segments-by-identity.png)

Das Widget **[!UICONTROL Zugeordnete Segmente nach Identität]** zeigt auf einen Blick, wie hoch die Wahrscheinlichkeit der erfolgreichen Zielgruppenbestimmung anhand von Profilen für eine Kampagne im gewählten Ziel ist. Eine effiziente zielgerichtete Kampagne hängt nicht von der Anzahl der an das Ziel gesendeten Profile ab, sondern von der Anzahl der Quell-IDs, die mit großer Wahrscheinlichkeit den Ziel-IDs zugeordnet werden können, um nützliche und verwertbare Daten bereitzustellen.

### Häufige Zielgruppen {#common-audiences}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_commonaudiences"
>title="Häufige Zielgruppen"
>abstract="Dieses Widget bietet eine Liste der fünf wichtigsten Segmente, die für das am oberen Seitenrand ausgewählte Zielkonto aktiviert wurden, sowie das im Widget-Dropdown-Menü ausgewählte Ziel. Die Liste der Segmente wird nach dem Zeitpunkt ihrer Aktivierung geordnet. Das zuletzt aktivierte Segment wird oben angezeigt."

Das Widget **[!UICONTROL Häufige Zielgruppen]** enthält eine Liste der fünf häufigsten Segmente, die für das am oberen Seitenrand ausgewählte Zielkonto aktiviert wurden, sowie das im Dropdown-Menü des Widgets ausgewählte Ziel. Die Liste der Segmente wird nach dem Zeitpunkt ihrer Aktivierung geordnet. Das zuletzt aktivierte Segment wird oben angezeigt.

Die Spalte [!UICONTROL ZIELGRUPPENGRÖSSE] gibt die Gesamtanzahl der Profile eines jeden aufgelisteten Segments an.

![Das Widget „Allgemeine Zielgruppen“.](../images/destinations/common-audiences.png)

### Zugeordnete Zielgruppen {#mapped-audiences}

Das Widget [!UICONTROL Zugeordnete Zielgruppen] zeigt die Gesamtanzahl der zugeordneten Zielgruppen an, die für das am oberen Seitenrand ausgewählte Ziel aktiviert werden können.

Wählen Sie **[!UICONTROL Segmente]** aus, um zur Registerkarte [!UICONTROL Durchsuchen] im Dashboard „Segmente“ zu navigieren. Dieser Arbeitsbereich enthält eine Liste aller Segmentdefinitionen für Ihre Organisation.

![Das Widget „Zugeordnete Zielgruppen“.](../images/destinations/mapped-audiences.png)

### Zustand der zugeordneten Zielgruppe {#mapped-audience-health}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_mappedaudiencehealth"
>title="Zustand der zugeordneten Zielgruppe"
>abstract="Dieses Widget bietet eine Liste von bis zu 20 zugeordneten Segmenten, deren Gesamtprofilanzahl um einen Faktor von mindestens einer Standardabweichung vom 30-Tage-Mittelwert der Zielgruppengröße, die diesem Ziel zugeordnet ist, abweicht. Es bietet eine berechnete Metrik für die Streuung der Zielgruppengrößen vom Mittelwert der letzten 30 Tage. Die Zielgruppengrößen werden absteigend sortiert."

Das Widget bietet eine Liste von bis zu 20 zugeordneten Segmenten, deren Gesamtprofilanzahl ab der letzten täglichen Momentaufnahme um einen Faktor von mindestens einer Standardabweichung vom 30-Tage-Mittelwert der Zielgruppengröße, die diesem Ziel zugeordnet ist, abweicht.

Kurz gesagt, es bietet eine berechnete Metrik für die Streuung der Zielgruppengrößen vom Mittelwert der letzten 30 Tage. Dabei wird verglichen, ob die heutige Zielgruppengröße außerhalb der historischen Standardabweichung liegt, die in den Daten der letzten 30 Tage zu beobachten war.

Alle Zielgruppengrößen im System werden von der größten zur kleinsten Zielgruppengröße sortiert, wie in der Spalte [!UICONTROL NEUESTE GRÖSSE] angegeben.

Wenn die Anzahl der einem Segment zugeordneten Profile außerhalb der Standardabweichung von der durchschnittlichen zugeordneten Profilgröße der letzten 30 Tagen liegt, deutet dies auf eine Anomalie im System hin und sollte untersucht werden.

Wenn ein Segment im Widget [!UICONTROL Zustand der zugeordneten Zielgruppe] stark abweicht, sollten Sie das Diagramm zur Entwicklung der Zielgruppengröße heranziehen und das anomale Segment lokalisieren. Der Trend kann weitere Einblicke in die Konsistenz Ihres Segments bieten.

>[!NOTE]
>
>Die Standardgröße des Widgets „Zustand der zugeordneten Zielgruppen“ kann die Tabelleninformationen überdecken. Ändern Sie die Größe des Widgets, damit die zugeordneten Segmentnamen und Spaltentitel besser lesbar sind. Anleitungen dazu finden Sie in der Dokumentation zum Ändern von Dashboards unter [Größe eines Widgets ändern](../customize/modify.md).

![Das Widget „Zustand der zugeordneten Zielgruppe“.](../images/destinations/mapped-audience-health.png)

### [!UICONTROL Anzahl der Ziele] {#destinations-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_destinations_destinationscount"
>title="Anzahl der Ziele"
>abstract="Dieses Widget gibt die Gesamtzahl der verfügbaren Endpunkte an, an denen eine Zielgruppe im System aktiviert und bereitgestellt werden kann. Diese Zahl umfasst sowohl aktive als auch inaktive Ziele."

Das Widget [!UICONTROL Anzahl der Ziele] gibt die Gesamtzahl der verfügbaren Endpunkte an, an denen eine Zielgruppe im System aktiviert und bereitgestellt werden kann. Diese Zahl umfasst sowohl aktive als auch inaktive Ziele.

Wählen Sie unter der Gesamtzahl die Option **[!UICONTROL Ziele]** aus, um zur Registerkarte zum Durchsuchen von Zielen zu navigieren. Auf dieser Seite werden alle Ziele aufgelistet, mit denen Sie bisher eine Verbindung hergestellt haben.

![Das Widget „Anzahl der Ziele“.](../images/destinations/destinations-count.png)

### [!UICONTROL Zielstatus] {#destination-status}

Das Widget [!UICONTROL Zielstatus] zeigt die Gesamtzahl der aktivierten Ziele als einzelne Metrik an und veranschaulicht in einem Ringdiagramm den proportionalen Unterschied zwischen aktivierten und deaktivierten Zielen.

Die jeweilige Anzahl für aktivierte oder deaktivierte Ziele wird in einem Dialogfeld angezeigt, wenn der Cursor über den entsprechenden Abschnitt des Ringdiagramms bewegt wird.

![Das Widget „Zielstatus“.](../images/destinations/destination-status.png)

### [!UICONTROL Aktive Ziele nach Zielplattform] {#active-destinations-by-destination-platform}

Das Widget bietet eine zweispaltige Tabelle, um eine Liste der aktiven Zielplattformen und die Gesamtzahl der aktiven Ziele für jede Zielplattform anzuzeigen. Die Liste der Zielplattformen ist von der höchsten zur niedrigsten sortiert.

![Das Widget „Aktive Ziele nach Zielplattform“.](../images/destinations/active-destinations-by-destination-platform.png)

### [!UICONTROL Aktivierte Audiences für alle Ziele] {#activated-audiences-across-all-destinations}

Das Widget [!UICONTROL Aktivierte Zielgruppen für alle Ziele] stellt die Gesamtzahl der Zielgruppen bereit, die für alle Ziele in einer einzelnen Metrik aktiviert sind.

>[!NOTE]
>
>Dieses Widget zeigt die Anzahl der Zielgruppen und nicht die Anzahl der Segmente an.

Diese Zahl entspricht der Anzahl beim aktuellen Schnappschuss.

![Das Widget „Aktivierte Zielgruppen für alle Ziele“.](../images/destinations/activated-audiences-across-all-destinations.png)

Wählen Sie **[!UICONTROL Zielgruppen]** aus, um zur Registerkarte [!UICONTROL Durchsuchen] der Ziele zu navigieren. Diese Seite enthält eine Liste aller aktivierten Ziele und zahlreiche relevante Metriken. Weitere Informationen finden Sie in der Dokumentation über die Registerkarte [[!UICONTROL Durchsuchen]](../../destinations/ui/destinations-workspace.md#browse).

Weitere Informationen finden Sie im Abschnitt Voraussetzungen für das [verwendete Begriffsdefinitionen](#prerequisites) in dieser Beschreibung.

### [!UICONTROL Aktivierte Zielgruppen] {#activated-audiences}

Dieses Widget bietet eine einzelne Metrik für die Gesamtzahl der für ein Ziel aktivierten Zielgruppen.

![Das Widget „Aktivierte Zielgruppen“.](../images/destinations/activated-audiences.png)

Wählen Sie **[!UICONTROL Zielgruppen]** aus, um zur Detailseite des Ziel-Dashboards zu navigieren. Die Registerkarte [!UICONTROL Aktivierungsdaten] zeigt eine Liste der Segmente an, die dem Ziel zugeordnet wurden, einschließlich des Anfangs- und Enddatums (falls zutreffend) sowie weiterer relevanter Informationen für den Datenexport, wie Exporttyp, -zeitplan und -frequenz. Um Details zu einem bestimmten Segment anzuzeigen, wählen Sie dessen Namen aus der Liste aus.

![Die Detailseite des Ziel-Dashboards mit der hervorgehobenen Registerkarte „Aktivierungsdaten“.](../images/destinations/activation-data-tab.png)

Dieses Widget hilft Ihnen, den Wert Ihrer Ziele anhand der Anzahl der aktivierten Zielgruppen auf einen Blick zu erfassen. Es bietet auch einfachen Zugriff auf detailliertere Informationen, die für weitere Analysen verwendet werden können.

Weitere Informationen finden Sie im Abschnitt Voraussetzungen für das [verwendete Begriffsdefinitionen](#prerequisites) in dieser Beschreibung.

## Nächste Schritte

Wenn Sie dieses Dokument gelesen haben, sollten Sie jetzt in der Lage sein, das Ziel-Dashboard zu finden und die in den verfügbaren Widgets angezeigten Metriken zu verstehen. Weitere Informationen zum Arbeiten mit Zielen in Experience Platform finden Sie in der [Dokumentation zu Zielen](../../destinations/home.md).
