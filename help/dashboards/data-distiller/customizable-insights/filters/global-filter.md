---
title: Erstellen eines globalen Filters
description: Erfahren Sie, wie Sie Ihre Dateneinblicke mit einem benutzerdefinierten, global angewendeten Filter filtern können.
source-git-commit: b95616263d5a6dd26f7fce61d5d0b33c2d470c46
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Globalen Filter erstellen {#create-global-filter}

Um einen globalen Filter zu erstellen, wählen Sie zunächst **[!UICONTROL Filter hinzufügen]** aus Ihrer Dashboard-Ansicht und **[!UICONTROL Globaler Filter]** aus dem Dropdown-Menü aus.

>[!IMPORTANT]
>
>Stellen Sie sicher, dass Sie Ihre globalen Filter allen Diagrammen zuordnen. Dies ist kein automatischer Prozess. Um einen globalen Filter zu verwenden, müssen Sie eine [Abfrageparameter](../../../../query-service/ui/parameterized-queries.md) in der SQL-Anweisung Ihres Diagramms, [Globalen Filter aktivieren](#enable-global-filter) im Widget-Composer und [Laufzeitwert auswählen](#select-global-filter) für den Parameter im Dialogfeld &quot;Globaler Filter&quot;. Informationen zum Bearbeiten Ihrer SQL-Abfrage, wenn Sie einen Abfrageparameter einbinden müssen, finden Sie im Handbuch query pro .

![Ein benutzerdefiniertes Dashboard mit Filter hinzufügen und seinem Dropdown-Menü hervorgehoben.](../../../images/customizable-insights/add-filter.png)

Sie können die von Ihrer SQL bereitgestellten Einblicke mit benutzerdefinierten globalen Filtern schnell ändern.

Die [!UICONTROL Globalen Filter erstellen] wird geöffnet. Das Erstellen eines globalen Filters folgt demselben Prozess wie das Erstellen eines Insight mit SQL. Wählen Sie zunächst eine Datenbank (Insights-Datenmodell) aus, die abgefragt werden soll, geben Sie dann Ihre benutzerdefinierte SQL in den Abfrage-Editor ein und wählen Sie dann das Ausführungssymbol (![Ein Ausführungssymbol.](../../../images/customizable-insights/run-icon.png)).

>[!IMPORTANT]
>
>Sie müssen beim Erstellen eines globalen Filters eine ID und einen Wert angeben. Mit den Beispielwerten können Sie die SQL-Anweisung ausführen und das Diagramm erstellen. Beachten Sie, dass die Beispielwerte, die Sie beim Erstellen Ihrer Anweisung angeben, durch die tatsächlichen Werte ersetzt werden, die Sie für den Datums- oder globalen Filter zur Laufzeit auswählen.

Nach erfolgreicher Ausführung der Abfrage werden die Ergebnisse im Tab Ergebnisse angezeigt. Klicken Sie auf **[!UICONTROL Weiter]**.

![Die [!UICONTROL Erstellen eines Dialogfelds für globale Filter] mit dem Dropdown-Menü Datensatz , dem Ausführungssymbol und Weiter hervorgehoben.](../../../images/customizable-insights/global-filter.png)

Für den letzten Schritt des Workflows zur Erstellung globaler Filter müssen Sie einen Titel für Ihren Filter hinzufügen. Fügen Sie der **[!UICONTROL Filterbezeichnung]** und wählen Sie einen Filtertyp aus dem Dropdown-Feld aus.

>[!NOTE]
>
>Nur die [!UICONTROL Kombinationsfeld] Filtertyp wird derzeit unterstützt.

Wählen Sie abschließend **[!UICONTROL Auswählen]** , um zur Dashboard-Ansicht zurückzukehren.

![Die [!UICONTROL Erstellen eines Dialogfelds für globale Filter] mit Auswahl und der Texteingabe Titel filtern hervorgehoben.](../../../images/customizable-insights/global-filter-label.png)

## Globalen Filter für jeden Einblick aktivieren {#enable-global-filter}

>[!TIP]
>
>Aktivieren Sie die globalen Filter in jedem Diagramm, das Sie erstellen. Dadurch wird sichergestellt, dass die Werte, die Sie als globaler Filter auswählen, in allen Ihren Diagrammen angezeigt werden.

Nachdem Sie Ihren globalen Filter für Ihr Dashboard erstellt haben, wird der Umschalter für diesen globalen Filter im Widget Composer verfügbar.

![Der Widget Composer mit dem Umschalter Globaler Filter markiert.](../../../images/customizable-insights/global-filter-consent.png)

>[!IMPORTANT]
>
>Stellen Sie sicher, dass der globale Filterparameter in der SQL jedes Insight enthalten ist.

## Globalen Filter auswählen {#select-global-filter}

So öffnen Sie die [!UICONTROL Filter] Wählen Sie das Filtersymbol (![Ein Filtersymbol.](../../../images/customizable-insights/filter.png)) auf der linken Seite Ihres Dashboards. Um die Auswirkungen auf Ihre Dashboard-Einblicke anzuwenden, wählen Sie anschließend eine Option aus dem Dropdown-Menü Ihres globalen Filters aus und wählen Sie **[!UICONTROL Anwenden]**.

![Ein benutzerdefiniertes Dashboard mit hervorgehobenem Filterdialogfeld.](../../../images/customizable-insights/custom-filters.png)
