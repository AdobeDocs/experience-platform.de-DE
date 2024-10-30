---
title: Zielgruppen-Trends
description: Erfahren Sie, wie Sie Zielgruppenmetriken im Zeitverlauf mithilfe des Dashboards "Zielgruppentrends"verfolgen und analysieren können. Legen Sie Zielgruppenfilter fest, analysieren Sie Größe- und Identitätstrends und exportieren Sie Einblicke für datengesteuerte Entscheidungen.
source-git-commit: 5fc786058a187b161a147a8bd361d19c5f35105d
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 1%

---

# Zielgruppen-Trends

Analysieren Sie, wie sich Ihre Zielgruppen im Laufe der Zeit ändern, mit Visualisierungen wichtiger Zielgruppenmetriken im Dashboard [!UICONTROL Zielgruppentrends]. Dieses Dashboard unterstützt Sie bei der Verfolgung von Trends wie Zielgruppenwachstum, Anzahl der Identitäten und Anzahl einzelner Identitätsprofile und ermöglicht datengesteuerte Entscheidungen. Durch Analyse dieser Metriken können Marketing-Experten Targeting-Strategien optimieren, die Interaktion mit Zielgruppen verbessern und ihre Segmentierungsbemühungen für effektivere Kampagnen verfeinern.

## Filtern von Zielgruppen {#filter-audiences}

Verwenden Sie zum Starten Ihrer Analyse den globalen Filter, um die spezifischen Zielgruppen und den Datumsbereich auszuwählen, den Sie analysieren möchten. Wählen Sie das Filtersymbol (![Filtersymbol) aus.](../../../images/icons/filter-icon-white.png)), um das Dialogfeld **[!UICONTROL Filter]** zu öffnen, in dem Sie Folgendes tun können:

1. **Eine Audience auswählen**: Wählen Sie die Zielgruppe aus, die Sie analysieren möchten (im Screenshot des Beispiels wurde die Audience **Amoxicillin** ausgewählt).
1. **Datumsbereich festlegen**: Wählen Sie einen vordefinierten Bereich aus dem Dropdown-Menü aus oder wählen Sie manuell Start- und Enddatum mithilfe der Kalenderfelder aus.

![Das Dialogfeld &quot;Filter&quot;im Dashboard &quot;Zielgruppentrends&quot;.](../../images/sql-insights-query-pro-mode/templates/audience-trends-filters.png)

Nachdem Sie Ihre Filter festgelegt haben, wählen Sie **[!UICONTROL Anwenden]** aus, um das Dashboard zu aktualisieren. Ihre ausgewählten Filter werden angewendet und es werden gezielte Einblicke in ausgewählte Zielgruppen während eines bestimmten Zeitraums angezeigt. Ihre benutzerdefinierten Filter stellen sicher, dass die Daten für Ihre Analyseziele relevant sind.

![Das Dashboard &quot;Zielgruppentrends&quot;mit angewendetem und hervorgehobenen Amoxicilin-Segmentfilter.](../../images/sql-insights-query-pro-mode/templates/audience-trends-applied-filters.png)

## Verfügbare Zielgruppen-Trend-Diagramme {#available-charts}

Es gibt drei Hauptdiagramme, die Ihnen helfen, Zielgruppenmetriken im Zeitverlauf zu verstehen. Für jedes Diagramm können Sie die Auslassungspunkte (`...`) oben rechts und danach [!UICONTROL Mehr anzeigen] auswählen, um entweder eine Tabellenform der Ergebnisse anzuzeigen oder die Daten als CSV-Datei herunterzuladen, um sie in einer Tabelle anzuzeigen. Weitere Informationen finden Sie im Handbuch [Mehr anzeigen](../view-more.md) .

>[!TIP]
>
>Sie können den Mauszeiger in einem beliebigen Diagramm über ein bestimmtes Datum bewegen, um die Anzahl der einzelnen Profile in einem Dialogfeld anzuzeigen.

### Trends der Zielgruppengröße {#audience-size-trends}

Das Diagramm **[!UICONTROL Trends der Zielgruppengröße]** zeigt die Anzahl der Profile innerhalb der ausgewählten Zielgruppe im Zeitverlauf. Sie hilft dabei, das Wachstum oder die Reduzierung von Zielgruppen zu verfolgen. Sie können dieses Diagramm verwenden, um die Interaktionswirksamkeit zu überwachen und Änderungen in der Zielgruppengröße zu verstehen.

![Das Trend-Diagramm zur Zielgruppengröße.](../../images/sql-insights-query-pro-mode/templates/audience-size-trends-chart.png)

### Trends bei Zielgruppen-Identitäten {#audience-identities-trends}

Das Diagramm **[!UICONTROL Trends bei Zielgruppenidentitäten]** bietet Einblicke in die Gesamtanzahl der Identitäten innerhalb des Zielgruppensegments. Verwenden Sie dieses Diagramm, um zu verstehen, wie eindeutige Identitäten zur Gesamtgröße der Zielgruppe beitragen. Es gibt einen Hinweis auf die Stabilität und Interaktion der Zielgruppe.

![Das Trenddiagramm der Zielgruppenidentitäten.](../../images/sql-insights-query-pro-mode/templates/audience-identities-trends.png)

### Trends der Größe einzelner Identitäts-Zielgruppen {#single-identity-audience-size-trends}

Das Diagramm **[!UICONTROL Trends der Größe einzelner Identitäts-Zielgruppen]** zeigt die Anzahl der Zielgruppenmitglieder mit nur einer Identität. Diese Metrik ist nützlich, um die Zusammensetzung Ihrer Zielgruppe zu verstehen, insbesondere im Hinblick auf die Eindeutigkeit Ihrer Identität, und hilft bei der Messung der Effektivität von Identitätszusammenfügungen.

![Das Trenddiagramm zur Größe einer Einzelidentitäts-Audience.](../../images/sql-insights-query-pro-mode/templates/single-identity-audience-size-trends.png)

## Exportieren von Insights {#export-insights}

Nach Analyse der Metriken und Anwendung relevanter Filter können Sie die Daten für weitere Offline-Analysen oder Berichte exportieren. Wählen Sie dazu oben rechts in der Tabelle **[!UICONTROL Export]** aus. Das Dialogfeld zum Drucken der PDF wird angezeigt. In diesem Dialogfeld können Sie die visualisierten Daten als PDF speichern oder drucken.

![Das Dashboard &quot;Zielgruppentrends&quot;mit hervorgehobenem Export.](../../images/sql-insights-query-pro-mode/templates/audience-trends-export.png)

## Nächste Schritte

Nach dem Lesen dieses Dokuments haben Sie im Dashboard **Zielgruppentrends** gelernt, wie Sie wertvolle Einblicke in das Zielgruppenverhalten im Zeitverlauf erhalten. Weitere Informationen zu anderen Data Distiller-Vorlagen, die Ihnen dabei helfen, fundierte Entscheidungen zu treffen, die Segmentierung zu optimieren und Interaktionsstrategien zu verbessern, finden Sie in den Handbüchern [Zielgruppenvergleich](./comparison.md), [Zielgruppenidentitätsüberschneidungen](./identity-overlaps.md) und [Erweiterte Zielgruppenüberschneidungen](./overlaps.md) .
