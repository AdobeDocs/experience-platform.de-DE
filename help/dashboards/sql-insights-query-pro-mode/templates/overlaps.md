---
title: Erweiterte Zielgruppenüberschneidungen
description: Erfahren Sie, wie Sie mithilfe des Dashboards Erweiterte Zielgruppenüberschneidungen analysieren und datengesteuerte Entscheidungen treffen können. Filtern von Zielgruppen, Vergleichen von Überschneidungen und Exportieren von Einblicken zur Verbesserung von Targeting-Strategien.
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 2%

---

# Erweiterte Zielgruppenüberschneidungen

Erhalten Sie wertvolle Einblicke zur Optimierung Ihrer Zielgruppensegmentierungs- und Targeting-Strategien, indem Sie analysieren, wie sich verschiedene Zielgruppensegmente mit dem Dashboard [!UICONTROL Erweiterte Zielgruppenüberschneidungen] überschneiden. Untersuchen Sie die in der Tabelle aufgeführten Metriken, um Überschneidungen zu erkennen, die Segmentierung zu verfeinern und redundantes Messaging zu reduzieren. Letztlich können Sie diese Einblicke verwenden, um zielgerichtetere Kampagnen und effiziente Marketing-Maßnahmen zu erstellen. In diesem Dashboard können Sie Zielgruppen-Schnittmengen überprüfen, Filter anwenden und eine detaillierte Überschneidungsanalyse durchführen, um datengesteuerte Entscheidungen zu treffen und Interaktionsergebnisse zu verbessern.

## Filtern von Zielgruppen {#filter-audiences}

Um bestimmte Zielgruppen für die Überschneidungsanalyse zu filtern, wählen Sie das Filtersymbol (![Filtersymbol) aus.](../../../images/icons/filter-icon-white.png)), um das Dialogfeld [!UICONTROL Filter] zu öffnen. Von hier aus können Sie Zielgruppen zur Analyse hinzufügen oder aus der Überschneidungsvorlage entfernen.

![Die Ansicht &quot;Erweiterte Zielgruppenüberschneidungen&quot;mit hervorgehobenem Filtersymbol.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-filter-icon.png)

Das Dialogfeld [!UICONTROL Filter] wird angezeigt. Um eine Zielgruppe für die Überschneidungsanalyse auszuwählen, wählen Sie einen Zielgruppennamen aus dem Dropdown-Menü **[!UICONTROL Zielgruppe]** aus. Der Name einer von Ihnen hinzugefügten Zielgruppe wird mit einem -Tag unter dem Dropdown-Menü angezeigt. Nach dem Hinzufügen können Sie das &quot;X&quot;nach ihrem Namen auswählen, um sie zu entfernen. Um alle angewendeten Filter zu entfernen, wählen Sie **[!UICONTROL Alle löschen]** aus.

## Angewandte Filter {#applied-filters}

Sobald ein Filter angewendet wurde ([!UICONTROL Amoxicilin-Segment] im Screenshot-Beispiel), werden die angezeigten Zielgruppendaten eingeschränkt. Alle weiteren Zielgruppen, die Sie hinzufügen möchten, werden neben dem Tag [!UICONTROL Filtern nach] über dem Diagramm [!UICONTROL Erweiterte Zielgruppe überschneidet] angezeigt.

![Das Dashboard &quot;Erweiterte Zielgruppenüberschneidungen&quot;mit hervorgehobenem Filter nach Amoxicilin-Segment.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-applied-filters.png)

## Tabelle &quot;Erweiterte Zielgruppenüberschneidungen&quot; {#advanced-audience-overlaps-table}

Im Hauptabschnitt des Dashboards wird die Tabelle [!UICONTROL Erweiterte Zielgruppenüberschneidungen] angezeigt, die einen detaillierten Vergleich der Zielgruppenüberschneidungen zwischen verschiedenen Segmenten bietet. Die Tabellenspalten lauten wie folgt:

| Spaltenname | Beschreibung |
|------------------------------------|----------------------------------------------------------------------------------------------|
| **[!UICONTROL Source_Segment_Name]** | Die ursprünglich analysierte Zielgruppe (z. B. &quot;Amoxicilin-Segment&quot;). |
| **[!UICONTROL overlap_segment_name]** | Die Zielgruppe, deren Überschneidungen verglichen werden (z. B. &quot;Blutzucker > 100&quot;). |
| **[!UICONTROL Source_segment_audience_count]** | Die Gesamtzahl der Profile der Quell-Audience. |
| **[!UICONTROL overlap_segment_audience_count]** | Die Größe der sich überschneidenden Zielgruppe, die je nach Überschneidung variiert. |
| **[!UICONTROL overlap_Audience_Count]** | Die Größe der tatsächlichen überlappenden Zielgruppe zwischen der Quell- und der Überschneidungszielgruppe. |

{style="table-layout:auto"}

## Exportieren von Insights {#export-insights}

Nachdem Sie die Zielgruppen gefiltert und analysiert haben, können Sie die Daten für weitere Offline-Analysen oder Berichte exportieren. Um Ihre Einblicke zu exportieren, wählen Sie oben rechts in der Tabelle **[!UICONTROL Exportieren]** aus. Das Dialogfeld zum Drucken der PDF wird angezeigt, in dem Sie die Daten als PDF speichern oder drucken können.

![Die Ansicht &quot;Erweiterte Zielgruppenüberschneidungen&quot;mit hervorgehobenem Export.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-export.png)

Um zur Übersicht [!UICONTROL Vorlage] zurückzukehren, wählen Sie **[!UICONTROL Vorlagen]** aus.

![Die Ansicht &quot;Erweiterte Zielgruppenüberschneidungen&quot;mit hervorgehobenen Vorlagen.](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-navigation.png)

## Nächste Schritte

Nach dem Lesen dieses Dokuments haben Sie gelernt, wie Sie Zielgruppenüberschneidungen analysieren und datengesteuerte Entscheidungen mithilfe des Dashboards **[!UICONTROL Erweiterte Zielgruppenüberschneidungen]** treffen können. Um Ihre Zielgruppensegmentierungs- und Targeting-Strategien weiter zu optimieren, sollten Sie andere Data Distiller-Vorlagen nutzen, die wertvolle Einblicke bieten. Weitere Informationen zur weiteren Verbesserung Ihrer Zielgruppeninteraktion und der Segmentierungsbemühungen finden Sie in den Handbüchern [Zielgruppentrends](./trends.md), [Zielgruppenvergleich](./comparison.md) und [Zielgruppenidentitätsüberschneidungen](./identity-overlaps.md) .

