---
title: Query Pro Mode-Drilldown
description: Erfahren Sie, wie Sie von einem beliebigen Diagramm zu einem neuen Dashboard navigieren, um Ihre Daten mithilfe des Drillthrough-Verfahrens zu untersuchen.
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Durchfahren {#drill-through}

Mithilfe von Drillthroughs können Sie mehrschichtige Datenanalysen durchführen, indem Sie einfach von einem beliebigen Diagramm zu einem neuen Dashboard navigieren. Diese Funktion erleichtert den Übergang von allgemeinen Übersichten zu ausführlichen Berichten bei der Untersuchung von Trends, Kundenverhalten, Betriebsindikatoren und mehr und stellt sicher, dass Sie stets über den benötigten Kontext verfügen.

Das System stellt sicher, dass die Analyse, mit der Sie beginnen, nahtlos während des gesamten Drilldown-Erlebnisses fortgesetzt wird, indem globale Filter und Datumsbereichsfilter automatisch von den Quell-Dashboards an die Ziel-Dashboards übergeben werden. Um die Navigation zwischen verschiedenen Ebenen der Studie zu vereinfachen, ermöglicht das System mehrstufige Drillthroughs.

## Erstellen eines Drilldown-Verfahrens {#create-drill-through}

Um einen Drilldown zu erstellen, wählen Sie zunächst **[!UICONTROL Bearbeiten]** aus Ihrer Dashboard-Ansicht aus.

![Ein benutzerdefiniertes Dashboard mit hervorgehobener Bearbeitung.](../images/sql-insights-query-pro-mode/drill-through.png)

Wählen Sie die Auslassungspunkte im Diagramm aus, die Sie durchsuchen möchten, und wählen Sie dann **[!UICONTROL Bearbeiten]** aus.

![Ein Diagramm, das das Ellipsenmenü mit hervorgehobener Option &quot;Bearbeiten&quot;anzeigt.](../images/sql-insights-query-pro-mode/drill-through-chart-edit.png)

Verwenden Sie im Bedienfeld [!UICONTROL Eigenschaften] den Umschalter, um **[!UICONTROL Drillthrough aktivieren]** zu aktivieren, und wählen Sie dann mithilfe der Dropdown-Liste das **[!UICONTROL Ziel-Dashboard]** aus. Stellen Sie sicher, dass der Umschalter für **[!UICONTROL Durchgang des Filters]** aktiviert ist, und wählen Sie dann **[!UICONTROL Speichern und schließen]**.

![Bedienfeld &quot;Diagrammeigenschaften&quot;mit hervorgehobener Option &quot;Drillthrough aktivieren&quot;, &quot;Ziel-Dashboard&quot;und &quot;Filter-Pass-Through&quot;.](../images/sql-insights-query-pro-mode/drill-through-chart-properties.png)

>[!INFO]
>
>Wiederholen Sie die oben hervorgehobenen Schritte für das Ziel-Dashboard, um einen mehrstufigen Drilldown einzurichten.

## Anzeigen eines Drilldown {#view-drill-through}

Um einen Drilldown anzuzeigen, wählen Sie in der Dashboard-Ansicht die Auslassungszeichen im Diagramm aus und wählen Sie dann **[!UICONTROL Durchsuchen]**.

![Ein Diagramm, das das Ellipsenmenü mit hervorgehobenem Durchlauf anzeigt.](../images/sql-insights-query-pro-mode/drill-through-chart-view.png)

Der Drilldown im Ziel-Dashboard wird angezeigt. Sie können diesen Schritt wiederholen, wenn Sie mehrstufige Drillthroughs haben.

![Das Ziel-Dashboard, das angezeigt wird, während der Durchlauf hervorgehoben ist.](../images/sql-insights-query-pro-mode/drill-through-target-dashboard.png)

>[!NOTE]
>
>Alle im Quell-Dashboard angewendeten Filter werden an das Ziel-Dashboard weitergeleitet. Datumsfilter und globale Filter sind jedoch in untergeordneten Dashboards deaktiviert.

## Einen Drilldown entfernen {#remove-drill-through}

Um einen Drilldown zu entfernen, wählen Sie zunächst **[!UICONTROL Bearbeiten]** aus Ihrer Dashboard-Ansicht aus.

![Ein benutzerdefiniertes Dashboard mit hervorgehobener Bearbeitung.](../images/sql-insights-query-pro-mode/drill-through.png)

Wählen Sie die Auslassungspunkte im Diagramm aus, durch die Sie einen Drilldown entfernen möchten, und wählen Sie dann **[!UICONTROL Bearbeiten]** aus.

![Ein Diagramm, das das Ellipsenmenü mit hervorgehobener Option &quot;Bearbeiten&quot;anzeigt.](../images/sql-insights-query-pro-mode/drill-through-chart-edit.png)

Wählen Sie im Bedienfeld [!UICONTROL Eigenschaften] den Umschalter zum Deaktivieren von **[!UICONTROL Drillthrough aktivieren]** und dann **[!UICONTROL Speichern und schließen]**.

![Bereich für Diagrammeigenschaften mit deaktiviertem Umschalter für [!UICONTROL Drillthrough aktivieren] hervorgehoben.](../images/sql-insights-query-pro-mode/drill-through-disable.png)

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie einen Drilldown für Ihr Dashboard erstellen können. Sie können auch erfahren, wie Sie mit dem Leitfaden für den Designmodus [ Diagramme aus vorhandenen Datenmodellen in der Adobe Experience Platform-Benutzeroberfläche erstellen.](../standard-dashboards.md)
