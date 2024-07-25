---
title: Erstellen eines globalen Filters
description: Erfahren Sie, wie Sie Ihre Dateneinblicke mit einem benutzerdefinierten, global angewendeten Filter filtern können.
exl-id: a0084039-8809-4883-9f68-c666dcac5881
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# Globalen Filter erstellen {#create-global-filter}

Um einen globalen Filter zu erstellen, wählen Sie zunächst **[!UICONTROL Filter hinzufügen]** aus Ihrer Dashboard-Ansicht und dann **[!UICONTROL Globaler Filter]** aus dem Dropdown-Menü aus.

>[!IMPORTANT]
>
>Stellen Sie sicher, dass Sie Ihre globalen Filter allen Diagrammen zuordnen. Dies ist kein automatischer Prozess. Um einen globalen Filter zu verwenden, müssen Sie einen [Abfrageparameter](../../../../query-service/ui/parameterized-queries.md) in die SQL Ihres Diagramms einbeziehen, den globalen Filter ](#enable-global-filter) im Widget Composer aktivieren und [einen Laufzeitwert auswählen](#select-global-filter) für den Parameter im Dialogfeld &quot;Globaler Filter&quot;. [ Informationen zum Bearbeiten Ihrer SQL-Abfrage, wenn Sie einen Abfrageparameter einbinden müssen, finden Sie im Handbuch query pro .

![Ein benutzerdefiniertes Dashboard mit Filter hinzufügen und seinem Dropdown-Menü hervorgehoben.](../../../images/customizable-insights/add-filter.png)

Sie können die von Ihrer SQL bereitgestellten Einblicke mit benutzerdefinierten globalen Filtern schnell ändern.

Das Dialogfeld [!UICONTROL Globalen Filter erstellen] wird geöffnet. Das Erstellen eines globalen Filters folgt demselben Prozess wie das Erstellen eines Insight mit SQL. Wählen Sie zunächst eine Datenbank (Insights-Datenmodell) aus, die abgefragt werden soll, geben Sie dann Ihre benutzerdefinierte SQL in den Abfrage-Editor ein und wählen Sie schließlich das Ausführungssymbol (![Ausführungssymbol.](/help/images/icons/play.png)).

>[!IMPORTANT]
>
>Sie müssen beim Erstellen eines globalen Filters eine ID und einen Wert angeben. Mit den Beispielwerten können Sie die SQL-Anweisung ausführen und das Diagramm erstellen. Beachten Sie, dass die Beispielwerte, die Sie beim Erstellen Ihrer Anweisung angeben, durch die tatsächlichen Werte ersetzt werden, die Sie für den Datums- oder globalen Filter zur Laufzeit auswählen.

Nach erfolgreicher Ausführung der Abfrage werden die Ergebnisse im Tab Ergebnisse angezeigt. Klicken Sie auf **[!UICONTROL Weiter]**.

![Das Dialogfeld [!UICONTROL Globalen Filter erstellen] mit dem Dropdown-Menü &quot;Datensatz&quot;, dem Ausführungssymbol und Weiter hervorgehoben.](../../../images/customizable-insights/global-filter.png)

Für den letzten Schritt des Workflows zur Erstellung globaler Filter müssen Sie einen Titel für Ihren Filter hinzufügen. Fügen Sie eine Beschriftung zum Textfeld **[!UICONTROL Filterbezeichnung]** hinzu und wählen Sie einen Filtertyp aus der Dropdown-Liste aus.

>[!NOTE]
>
>Derzeit wird nur die Filtertyp [!UICONTROL Kombinationsfeld] unterstützt.

Wählen Sie abschließend **[!UICONTROL Auswählen]** aus, um zur Dashboard-Ansicht zurückzukehren.

![Das Dialogfeld [!UICONTROL Globalen Filter erstellen] mit Auswahl und der Texteingabe für die Filterbeschriftung wurde hervorgehoben.](../../../images/customizable-insights/global-filter-label.png)

## Globalen Filter für jeden Einblick aktivieren {#enable-global-filter}

>[!TIP]
>
>Aktivieren Sie die globalen Filter in jedem Diagramm, das Sie erstellen. Dadurch wird sichergestellt, dass die Werte, die Sie als globaler Filter auswählen, in allen Ihren Diagrammen angezeigt werden.

Nachdem Sie Ihren globalen Filter für Ihr Dashboard erstellt haben, wird der Umschalter für diesen globalen Filter im Widget Composer verfügbar.

![Der Widget Composer mit dem Umschalter Globaler Filter ist hervorgehoben.](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>Stellen Sie sicher, dass der globale Filterparameter in der SQL jedes Insight enthalten ist.

## Globalen Filter auswählen {#select-global-filter}

Um das Dialogfeld [!UICONTROL Filter] zu öffnen, in dem alle Ihre benutzerdefinierten Filter aufgelistet werden, wählen Sie das Filtersymbol (![Ein Filtersymbol) aus.](/help/images/icons/filter.png)) auf der linken Seite Ihres Dashboards. Wählen Sie anschließend eine Option aus dem Dropdown-Menü Ihres globalen Filters und danach **[!UICONTROL Anwenden]** aus, um die Auswirkungen auf Ihre Dashboard-Einblicke anzuwenden.

![Ein benutzerdefiniertes Dashboard mit hervorgehobenem Filterdialogfeld.](../../../images/customizable-insights/custom-filters.png)
