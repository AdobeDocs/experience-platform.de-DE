---
title: Zielgruppen-Identitätsüberschneidungen
description: Erfahren Sie, wie Sie Identitätsüberschneidungen bei Zielgruppen mithilfe des Dashboards Identitätsüberschneidungen bei Zielgruppen analysieren können. Filtern Sie Zielgruppen, geben Sie Zusammenführungsrichtlinien an und untersuchen Sie Identitätsbeziehungen, um datengesteuerte Entscheidungen zu treffen.
exl-id: 355835b8-2a67-40b1-a0e8-6afef01ddc6a
source-git-commit: 5550e757eae95e529d74115df9bbe9b635d25ec8
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 1%

---

# Zielgruppen-Identitätsüberschneidungen

Analysieren Sie Identitätsüberschneidungen für ausgewählte Zielgruppen mit dem Dashboard [!UICONTROL Zielgruppenidentitätsüberschneidungen] . Sie können Einblicke in die Art und Weise nutzen, wie verschiedene Identitäten innerhalb einer Zielgruppe miteinander in Beziehung stehen, um Stitching-Strategien zu optimieren, Redundanz zu reduzieren und die Genauigkeit der Kundensegmentierung zu verbessern. Entwickeln Sie effektive Targeting-Strategien und optimieren Sie die Kundeninteraktionen mit einem verbesserten Verständnis der Überschneidung zwischen Identitätstypen.

## Audiences filtern {#filter-audiences}

Verwenden Sie benutzerdefinierte Filter für die zielgerichtete Analyse bestimmter Zielgruppen und Identitätstypen, um sicherzustellen, dass die präsentierten Daten mit Ihren Analysezielen übereinstimmen. Um Ihre Analyse zu starten, wählen Sie das Filtersymbol (![Das Filtersymbol.](../../../images/icons/filter-icon-white.png)).

![Das Dashboard „Zielgruppenidentität“ überschneidet sich mit dem hervorgehobenen Filtersymbol.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-filter-icon.png)

Das **[!UICONTROL Filter]** wird angezeigt. Wählen Sie in dieser Ansicht die globalen Filter aus, um Ihre Audience, Zusammenführungsrichtlinie und die zu vergleichenden Identitäten zu konfigurieren. Wählen Sie Ihre Einstellungen für die Analyse aus dem Dropdown-Menü jedes Abschnitts aus

1. Wählen Sie eine **[!UICONTROL Zielgruppe]** aus: Wählen Sie das Zielgruppensegment aus, das Sie analysieren möchten (z. B **„Kanada - Alberta**).
2. Geben Sie eine **[!UICONTROL Zusammenführungsrichtlinie]** an: Definieren Sie die Zusammenführungsrichtlinie, die bestimmt, wie Identitäten über die ausgewählte Zielgruppe hinweg kombiniert werden (im Beispiel-Screenshot ist die **Standardzeitbasierte** Richtlinie ausgewählt).
3. Wählen Sie eine **[!UICONTROL Identität A]** und **[!UICONTROL Identität B]** zum Vergleich aus**: Wählen Sie die beiden Identitätstypen aus, die Sie vergleichen möchten. Im Beispiel wird **Identität A** als „crmId“ und **Identität B** als „E-Mail“ ausgewählt.
4. **Datumsbereich festlegen**: Wählen Sie einen vordefinierten Bereich wie „Heute“ oder legen Sie das Start- und Enddatum manuell mithilfe der Kalenderfelder fest.

![Das Dialogfeld „Filter“ im Dashboard „Zielgruppenidentitätsüberschneidungen“.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-filters-dialog.png)

>[!TIP]
>
>Um alle benutzerdefinierten globalen Filter zu löschen, wählen Sie **[!UICONTROL Alle löschen]** im Dialogfeld [!UICONTROL Filter] aus. Um einen einzelnen Filter zu entfernen, wählen Sie [!UICONTROL X] rechts neben dem Filternamen aus.

Nachdem Sie die Filter ausgewählt haben, wählen Sie **[!UICONTROL Anwenden]** aus, um das Dashboard zu aktualisieren.

![Das Dialogfeld „Filter“ im Dashboard „Zielgruppenidentität überschneidet“ mit hervorgehobener Option „Anwenden“.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-apply-filters.png)

## Verfügbare Dashboard-Einblicke {#available-insights}

Das Dashboard **Zielgruppenidentitätsüberschneidungen** bietet mehrere Visualisierungen und tabellarische Daten, die Ihnen dabei helfen, Identitätsüberschneidungen und Trends in Ihrer Zielgruppe zu verstehen.

### Zielgruppen-Identitätsüberschneidungen {#overlaps-table}

Die **[!UICONTROL Audience-Identitätsüberschneidungen]** zeigt Identitätsüberschneidungen basierend auf Ihren ausgewählten Filtern an. Verwenden Sie diese Informationen, um die Überschneidung zwischen verschiedenen Identitätstypen zu bewerten und zu verstehen, wie effektiv Identitäten aufgelöst werden. In der folgenden Tabelle werden die einzelnen Spalten detailliert erläutert:

| Spaltenname | Beschreibung |
|-----------------|-------------------------------|
| **[!UICONTROL Zielgruppenname]** | Der Name der analysierten Zielgruppe. Diese Spalte identifiziert, welches Zielgruppensegment überprüft wird, um sicherzustellen, dass die Insights auf die beabsichtigte Zielgruppe ausgerichtet sind. |
| **[!UICONTROL Identität A]** und **[!UICONTROL Identität B]** | Die zu vergleichenden Identitäten (z. B. `crmId` und `email`). Wenn Sie wissen, welche Identitätstypen verglichen werden, können Sie feststellen, welche Identitätsauflösungsstrategien zur Zielgruppenüberschneidung beitragen, und diese Beziehungen optimieren. |
| **[!UICONTROL Anzahl Überschneidungen]** | Die Anzahl der Profile, in denen beide Identitäten vorhanden sind. Diese Metrik bietet Einblicke in das Ausmaß der Identitätsüberschneidung innerhalb der Zielgruppe. Diese Informationen sind wichtig, um zu bewerten, wie effektiv mehrere Identitäten in einheitliche Profile aufgelöst werden, was wiederum die Targeting- und Personalisierungsstrategien verbessern kann. |
| **[!UICONTROL Anzahl von Identitäten]** | Die Gesamtzahl der Profile in der ausgewählten Zielgruppe, die „Identität **&quot;**. Verwenden Sie diese Informationen, um die Prävalenz des primären Identitätstyps innerhalb der Zielgruppe zu verstehen und ihre Rolle in der Überschneidungsanalyse zu bewerten. |

![Die Tabelle mit Überschneidungen der Zielgruppenidentität im Dashboard für Identitätsüberschneidungen der Zielgruppe.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-chart.png)

### Aufschlüsselung der Identität {#identity-breakdown}

Das **[!UICONTROL Identitätsaufschlüsselung]** Diagramm zeigt die relative Komposition von Identitäten innerhalb der ausgewählten Zielgruppe. Die X-Achse stellt die Gesamtzahl der Identitäten innerhalb der ausgewählten Zielgruppe dar, während die Y-Achse den Namen der zu analysierenden Zielgruppe darstellt. Verwenden Sie diese Visualisierung, um die Prävalenz jedes Identitätstyps zu verstehen und die Auswirkungen Ihrer Identitäts-Management-Strategie zu bewerten. Das Diagramm unterscheidet mithilfe verschiedener Farben zwischen Identitätstypen und bietet einen schnellen Überblick darüber, wie Identitäten über Ihre Zielgruppe verteilt sind.

>[!TIP]
>
>Bewegen Sie den Mauszeiger über die Spalten, um die individuelle Anzahl der Profile für jeden Identitätstyp anzuzeigen.

![Das Diagramm zur Aufschlüsselung der Identität.](../../images/sql-insights-query-pro-mode/templates/identity-breakdown-chart.png)

### Trends bei der Zielgruppenidentität {#audience-identity-trends}

Das Diagramm **[!UICONTROL Trends bei der Zielgruppenidentität]** bietet Einblicke in die Veränderungen der Gesamtzahl der Identitäten im Laufe der Zeit. Die X-Achse stellt den analysierten Datumsbereich dar, während die Y-Achse die Gesamtzahl der Identitäten nach Zielgruppe darstellt. Verwenden Sie diese Metrik, um das Identitätswachstum zu verfolgen, die Stabilität zu bewerten und die Effektivität laufender Identitätsverwaltungs-Maßnahmen zu messen.

>[!TIP]
>
>Bewegen Sie den Mauszeiger über ein Datum im Diagramm, um die Gesamtzahl der Identitäten für die Zielgruppe an einem bestimmten Datum anzuzeigen.

![Diagramm der Identitätstrends der Zielgruppe.](../../images/sql-insights-query-pro-mode/templates/audience-identity-trends-chart.png)

## Exportieren von Einblicken {#export-insights}

Nach der Analyse von Identitätsüberschneidungen können Sie die Daten für die Offline-Analyse oder das Reporting exportieren. Um Ihre Daten zu exportieren **[!UICONTROL wählen Sie]** Exportieren) oben rechts in der Tabelle aus. Das Dialogfeld PDF drucken wird angezeigt, sodass Sie die visualisierten Daten als PDF speichern oder drucken können.

![Das Dashboard „Zielgruppenidentität überschneidet“ mit hervorgehobener Option „Export“.](../../images/sql-insights-query-pro-mode/templates/audience-identity-overlaps-export.png)

Das Dashboard **Zielgruppenidentitätsüberschneidungen** bietet wichtige Einblicke in die Überschneidung verschiedener Identitäten zwischen Ihren ausgewählten Zielgruppen. Durch die Nutzung dieser Einblicke können Sie Strategien zur Identitätszuordnung verfeinern, Redundanz reduzieren und sicherstellen, dass Ihre Zielgruppensegmentierung genauer und effektiver ist.

## Nächste Schritte

Nach dem Lesen dieses Dokuments haben Sie gelernt, wie Sie mithilfe des Dashboards **Zielgruppen-Identitätsüberschneidungen“ wertvolle Einblicke in** Identitätsüberschneidungen für ausgewählte Zielgruppen erhalten. Um Ihr Verständnis von Zielgruppensegmentierung und Identitätsverwaltung weiter zu verbessern, sollten Sie andere Data Distiller-Vorlagen erkunden, die umfassende Einblicke bieten. Weitere Informationen zur weiteren Verbesserung Ihrer Zielgruppenbestimmungs[ und Interaktionsstrategien finden Sie in ](./trends.md) Handbüchern ](./comparison.md)Zielgruppentrends“, [Zielgruppenvergleich und [Erweiterte Zielgruppenüberschneidungen](./overlaps.md).
