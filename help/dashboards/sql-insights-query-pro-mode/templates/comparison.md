---
title: Zielgruppenvergleich
description: Erfahren Sie, wie Sie Schlüsselmetriken zwischen verschiedenen Zielgruppen mithilfe des Dashboards "Zielgruppenvergleich"vergleichen. Festlegen von Zielgruppenfiltern, Analysieren von Trends und Exportieren von Einblicken für datengesteuerte Entscheidungen
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# Zielgruppenvergleich

Das Dashboard [!UICONTROL Zielgruppenvergleich] vergleicht wichtige Zielgruppenmetriken in einer parallelen Ansicht. In diesem Dashboard können Sie verschiedene Aktionen durchführen, um zwei Zielgruppen zu vergleichen und Schlüsselmetriken zwischen ihnen zu analysieren. Anschließend können Sie datengesteuerte Entscheidungen in Bezug auf Zielgruppensegmentierung und Zielgruppenstrategien treffen.

## Festlegen von Zielgruppenvergleichen {#set-audience-comparisons}

Um aussagekräftigere Einblicke und Vergleiche zu ermöglichen, verwenden Sie die Systemfilter, um die Zielgruppensegmente und den Zeitrahmen, den Sie analysieren möchten, präzise anzusprechen. Wählen Sie das Filtersymbol (![Filtersymbol) aus.](../../../images/icons/filter-icon-white.png)), um zwei verschiedene Zielgruppen ([!UICONTROL Zielgruppe A] und [!UICONTROL Zielgruppe B]) auszuwählen und bestimmte Parameter zum Vergleich festzulegen.

![Das Dialogfeld &quot;Filter&quot;im Dashboard &quot;Zielgruppenvergleich&quot;.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-filters.png)

Das Dialogfeld [!UICONTROL Filter] wird angezeigt. Um die erste zu analysierende Zielgruppe auszuwählen, wählen Sie das Dropdown-Menü **[!UICONTROL Zielgruppe A auswählen]** aus. In diesem Beispiel wurde `California Patients` als Zielgruppe A ausgewählt. Diese Zielgruppe wird nach Anwendung des Filters auf der linken Seite des Vergleichs angezeigt.

Wählen Sie anschließend eine zweite Zielgruppe aus, die mit [!UICONTROL Zielgruppe A] aus dem Dropdown-Menü **[!UICONTROL Zielgruppe B auswählen]** verglichen werden soll. In diesem Bild wurde [!UICONTROL Benutzer, die E-Mail zugestimmt wurden] als [!UICONTROL Zielgruppe B] ausgewählt. Diese Zielgruppe wird nach Anwendung des Filters auf der rechten Seite des Dashboards [!UICONTROL Zielgruppenvergleich] angezeigt.

### Datumsbereiche anpassen {#adjust-date-ranges}

Sie können Ihre Daten auch nach bestimmten Zeiträumen filtern, um zu sehen, wie diese Zielgruppen funktionieren oder sich über einen benutzerdefinierten Datumsbereich ändern. Um einen Zeitraum für die Filterung der Zielgruppendaten nach einem bestimmten Zeitraum festzulegen, wählen Sie das Start- und das Enddatum aus den Kalenderfeldern aus.

Das Dialogfeld gibt auch an, wie viele Filter angewendet werden (im Screenshot unten werden zwei Filter verwendet: Zielgruppe A und Zielgruppe B und heute als Datumsbereich). Um alle angewendeten Filter zu entfernen, wählen Sie **[!UICONTROL Alle löschen]** aus.

Nachdem Sie die Zielgruppen und den Datumsbereich festgelegt haben, wählen Sie **[!UICONTROL Anwenden]** aus, um das Dashboard [!UICONTROL Zielgruppenvergleich] zu aktualisieren.

![Das Dialogfeld &quot;Filter&quot;im Dashboard &quot;Zielgruppenvergleich&quot;mit hervorgehobenem Anwenden.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-filters-apply.png)

Das Dashboard zeigt nun die Vergleichstabellen für jede Zielgruppe nebeneinander an.

![Das Dashboard für den Zielgruppenvergleich mit mehreren Diagrammen, in denen die Metriken für jede Zielgruppe verglichen werden.](../../images/sql-insights-query-pro-mode/templates/audience-comparison-dashboard.png)

## Verfügbare Zielgruppen-Vergleichstabellen {#available-charts}

<!-- Potentially could expand this section to include images of each widget.  -->

Das Dashboard bietet verschiedene Diagramme zum Vergleichen von Einblicken:

- [[!UICONTROL Zielgruppengröße]](../../guides/audiences.md#audience-size): Verfolgen Sie einfach die Größe der einzelnen Zielgruppen basierend auf der Anzahl der darin enthaltenen Profile. Diese Metrik hilft Ihnen, die Skala der beiden Zielgruppen zu verstehen, die Sie vergleichen.
- [!UICONTROL Aufschlüsselung der Zielgruppenidentität]: Ein Tortendiagramm bietet eine Aufschlüsselung der relativen Zusammensetzung der Identitäten innerhalb der einzelnen Zielgruppen. Sie können die Anzahl der Identitäten insgesamt anzeigen und untersuchen, wie verschiedene Kennungen (wie E-Mail oder CRM-ID) zu dieser Summe beitragen. Dieses Diagramm hilft Ihnen, die Zusammensetzung der einzelnen Zielgruppen basierend auf Identitätstypen zu verstehen. Bewegen Sie den Mauszeiger über einen Abschnitt des Tortendiagramms, um eine genaue Anzahl von Identitäten anzuzeigen.
- [[!UICONTROL Trend zur Zielgruppengröße]](../../guides/audiences.md#audience-size-trend): Dieses Diagramm stellt die Trends der Größe im Zeitverlauf für die ausgewählte Zielgruppe dar. Verwenden Sie diese Diagramme, um zu visualisieren, wie sich die Größe der einzelnen Zielgruppen über einen ausgewählten Zeitraum verändert hat. Spitzen und Tiefen geben die Phasen des Wachstums oder der Verringerung der Anzahl der Profile an.
- [[!UICONTROL Trend zur Änderung der Zielgruppengröße]](../../guides/audiences.md#audience-size-change-trend): Dieses Diagramm zeigt die Trends zur Größenänderung für die ausgewählte Zielgruppe an. Sie visualisiert, wie stark die Zielgruppengröße im Laufe der Zeit zugenommen oder abgenommen hat, und ermöglicht es Ihnen, signifikante Veränderungen oder Trends in der Zielgruppenpopulation zu identifizieren.

>[!NOTE]
>
>Die Diagramme [!UICONTROL Trend der Zielgruppengröße] und [!UICONTROL Trend zur Änderung der Zielgruppengröße] helfen Ihnen beim Tracking und Vergleichen der absoluten Größe und der Größenschwankungen zwischen zwei Zielgruppen über einen bestimmten Zeitraum. Diese Informationen erleichtern das Verständnis von Mustern und Faktoren, die Änderungen der Zielgruppe beeinflussen.

## Exportieren von Einblicken {#export-insights}

Nachdem Sie die Filter angewendet und die Zielgruppen analysiert haben, können Sie die Daten für weitere Offline-Analyse- oder Berichtszwecke exportieren. Um Ihre Einblicke zu exportieren, wählen Sie oben rechts in der Tabelle **[!UICONTROL Exportieren]** aus. Das Dialogfeld zum Drucken der PDF wird angezeigt. In diesem Dialogfeld können Sie die in der Tabelle angezeigten Daten als PDF speichern oder drucken.

Wählen Sie **[!UICONTROL Vorlagen]** aus, um zur Übersicht [!UICONTROL Vorlage] zurückzukehren.

![Die Ansicht &quot;Erweiterte Zielgruppenüberschneidungen&quot;mit hervorgehobenen Vorlagen.](../../images/sql-insights-query-pro-mode/templates/navigation.png)

## Nächste Schritte

Nach dem Lesen dieses Dokuments haben Sie gelernt, wie Sie Schlüsselmetriken zwischen verschiedenen Zielgruppen mithilfe des Dashboards **Zielgruppenvergleich** vergleichen können. Um Ihre Zielgruppensegmentierungs- und Targeting-Strategien weiter zu verbessern, erkunden Sie andere Data Distiller-Vorlagen, die zusätzliche Einblicke bieten. Weitere Informationen dazu, wie Sie Ihre Entscheidungsprozesse weiter verbessern und Interaktionsbemühungen optimieren können, finden Sie in den Handbüchern [Audience Trends](./trends.md), [Überschneidungen bei der Zielgruppenidentität](./identity-overlaps.md) und [Erweiterte Zielgruppenüberschneidungen](./overlaps.md) .

