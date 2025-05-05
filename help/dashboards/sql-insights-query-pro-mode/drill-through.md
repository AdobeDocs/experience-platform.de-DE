---
title: Query Pro-Modus - Drill-Through
description: Erfahren Sie, wie Sie von einem beliebigen Diagramm zu einem neuen Dashboard navigieren, um Ihre Daten mithilfe von Drill-Through zu untersuchen.
exl-id: d38550ba-1c56-4b6b-bf96-f21da232ba34
source-git-commit: 5550e757eae95e529d74115df9bbe9b635d25ec8
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Drill-Through {#drill-through}

Drill-Throughs erleichtern die mehrschichtige Datenanalyse, indem sie die Navigation von einem beliebigen Diagramm zu einem neuen Dashboard erleichtern. Diese Funktion erleichtert den Übergang von allgemeinen Übersichten zu detaillierten Berichten bei der Untersuchung von Trends, Kundenverhalten, operativen Indikatoren und mehr. So wird sichergestellt, dass Sie immer über den benötigten Kontext verfügen.

Das System stellt sicher, dass die von Ihnen begonnene Analyse nahtlos über das gesamte Erlebnis hinweg fortgesetzt wird, indem globale Filter und Datumsbereichsfilter automatisch von den Quell-Dashboards an die Ziel-Dashboards übergeben werden. Um die Navigation zwischen verschiedenen Ebenen der Studie zu erleichtern, ermöglicht das System mehrstufige Drill-Throughs.

## Erstellen eines Drill-Throughs {#create-drill-through}

Um einen Drill-Through zu erstellen, wählen Sie zunächst **[!UICONTROL Bearbeiten]** in Ihrer Dashboard-Ansicht aus.

![Ein benutzerdefiniertes Dashboard mit hervorgehobener Option „Bearbeiten“.](../images/sql-insights-query-pro-mode/drill-through.png)

Klicken Sie auf die Auslassungszeichen in dem Diagramm, durch das Sie einen Drilldown durchführen möchten, und wählen Sie dann **[!UICONTROL Bearbeiten]** aus.

![Ein Diagramm mit dem Auslassungsmenü und hervorgehobener Option „Bearbeiten“.](../images/sql-insights-query-pro-mode/drill-through-chart-edit.png)

Verwenden Sie im Bedienfeld [!UICONTROL Eigenschaften] den Umschalter, um **[!UICONTROL Drill-Through aktivieren]** zu aktivieren, und wählen Sie dann über die Dropdown-Liste das **[!UICONTROL Target-Dashboard]** aus. Stellen Sie sicher, dass der Umschalter **[!UICONTROL Filter-Pass-Through]** aktiviert ist, und wählen Sie dann **[!UICONTROL Speichern und schließen]**.

![Bedienfeld „Diagrammeigenschaften“ mit hervorgehobener Option „Drill-Through aktivieren“, „Ziel-Dashboard“ und „Filter-Pass-Through“](../images/sql-insights-query-pro-mode/drill-through-chart-properties.png)

>[!INFO]
>
>Wiederholen Sie die oben hervorgehobenen Schritte für das Ziel-Dashboard, um einen mehrstufigen Drill-Through einzurichten.

## Anzeigen eines Drill-Throughs {#view-drill-through}

Um einen Drill-Through anzuzeigen, wählen Sie in Ihrer Dashboard-Ansicht Auslassungspunkte im Diagramm aus und klicken Sie dann auf **[!UICONTROL Drill-Through]**.

![Ein Diagramm mit dem Menü mit den Auslassungspunkten und hervorgehobenem Drill-Through.](../images/sql-insights-query-pro-mode/drill-through-chart-view.png)

Das Drill-Through-Ziel-Dashboard wird angezeigt. Sie können diesen Schritt wiederholen, wenn Sie mehrstufige Drill-Throughs haben.

![Das Ziel-Dashboard, das mit hervorgehobenem Drill-Through angezeigt wird.](../images/sql-insights-query-pro-mode/drill-through-target-dashboard.png)

>[!NOTE]
>
>Alle im Quell-Dashboard angewendeten Filter werden an das Ziel-Dashboard übergeben. Datumsfilter und globale Filter sind jedoch in untergeordneten Dashboards deaktiviert.

## Entfernen eines Drill-Throughs {#remove-drill-through}

Um einen Drill-Through zu entfernen, wählen Sie zunächst **[!UICONTROL Bearbeiten]** in Ihrer Dashboard-Ansicht aus.

![Ein benutzerdefiniertes Dashboard mit hervorgehobener Option „Bearbeiten“.](../images/sql-insights-query-pro-mode/drill-through.png)

Klicken Sie auf die Auslassungszeichen im Diagramm, durch die Sie einen Drill-down entfernen möchten, und klicken Sie dann auf **[!UICONTROL Bearbeiten]**.

![Ein Diagramm mit dem Auslassungsmenü und hervorgehobener Option „Bearbeiten“.](../images/sql-insights-query-pro-mode/drill-through-chart-edit.png)

Wählen Sie im Bedienfeld [!UICONTROL Eigenschaften] den Umschalter zum Deaktivieren von **[!UICONTROL Drill-Through aktivieren]** aus und klicken Sie dann auf **[!UICONTROL Speichern und schließen]**.

![Bedienfeld „Diagrammeigenschaften“ mit deaktiviertem Umschalter für &quot;[!UICONTROL &#x200B; aktivieren] hervorgehoben.](../images/sql-insights-query-pro-mode/drill-through-disable.png)

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie einen Drill-Through für Ihr Dashboard erstellen. Außerdem erfahren Sie mit dem Handbuch [ Design-Modus , wie Sie Diagramme aus vorhandenen Datenmodellen in der Adobe Experience Platform-Benutzeroberfläche ](../standard-dashboards.md).
