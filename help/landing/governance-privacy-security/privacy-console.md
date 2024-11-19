---
title: Übersicht über die Datenschutzkonsole
description: Erfahren Sie, wie Sie Ihre datenschutzbezogenen Workflows in der Benutzeroberfläche von Adobe Experience Platform überwachen.
feature: Privacy
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 4%

---

# Übersicht über die Datenschutzkonsole

Die Registerkarte [!UICONTROL Datenschutzkonsole] in der Benutzeroberfläche von Adobe Experience Platform bietet eine Dashboard-Ansicht Ihrer datenschutzbezogenen Vorgänge in Platform, einschließlich Arbeitsaufträgen zur Datenhygiene, Anfragen von Datensubjekten von Privacy Service und Prüfprotokollen für Platform-Benutzeraktivitäten.

Um auf das Dashboard zuzugreifen, wählen Sie im linken Navigationsbereich **[!UICONTROL Datenschutzkonsole]** aus.

![Bild mit der Auswahl von [!UICONTROL Datenschutzkonsole] im linken Navigationsbereich der Platform-Benutzeroberfläche](../images/governance-privacy-security/privacy-console/left-nav.png)

Von hier aus können Sie die verfügbaren [Monitoring-Widgets](#widgets) der Konsole lesen oder eine von mehreren [Anwendungsfallhandbüchern](#use-case-guides) der Datenschutzfunktionen von Platform durchsuchen.

## Widgets

[!UICONTROL Datenschutzkonsole] bietet mehrere Widgets zur Überwachung Ihrer Datenschutzvorgänge.

![Bild mit der Auswahl von [!UICONTROL Datenschutzkonsole] im linken Navigationsbereich der Platform-Benutzeroberfläche](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Je nach den SKUs, die Ihr Unternehmen erworben hat, sind einige der unten aufgeführten Widgets möglicherweise nicht verfügbar.

Die Funktion der einzelnen Widgets wird nachfolgend beschrieben:

| Widget-Name | Beschreibung |
| --- | --- |
| Auftragsstatus der Datenhygiene | Zeigt den Status von Löschvorgängen von Datensätzen unter [Datenhygiene](../../hygiene/home.md) für den ausgewählten Zeitraum an. Verwenden Sie das Dropdown-Menü, um den Zeitrahmen zwischen den letzten 7 Tagen, 14 Tagen und 30 Tagen zu ändern. |
| Aktuelle Bestellungen zur Datenhygiene | Zeigt die neuesten [Data Hygiene](../../hygiene/home.md) Arbeitsaufträge an, die vom System verarbeitet werden. Verwenden Sie das Dropdown-Menü, um zwischen kürzlich erstellten Arbeitsaufträgen und kürzlich aktualisierten Arbeitsaufträgen zu wechseln. |
| Häufigste Aktionen | Zeigt die häufigsten Aktionen auf Platform an, die von [Prüfprotokollen](./audit-logs/overview.md) für den ausgewählten Zeitraum erfasst wurden. Verwenden Sie das Dropdown-Menü, um den Zeitrahmen zwischen den letzten 7 Tagen, 14 Tagen und 30 Tagen zu ändern. |
| Aktivste Benutzer | Zeigt die aktivsten Platform-Benutzer in Ihrer Organisation an, die von [Audit-Protokollen](./audit-logs/overview.md) für den ausgewählten Zeitraum erfasst wurden. Verwenden Sie das Dropdown-Menü, um den Zeitrahmen zwischen den letzten 7 Tagen, 14 Tagen und 30 Tagen zu ändern. |
| Anfragen von Datensubjekten | Zeigt die Anzahl der Anfragen von Datensubjekten an, die an einem bestimmten Tag von [Privacy Service](../../privacy-service/home.md) gesendet und abgeschlossen wurden. |

{style="table-layout:auto"}

## Benutzerhandbücher

Die Konsole enthält mehrere produktinterne Anleitungen, die Sie mit allgemeinen Datenschutz-Workflows in Platform vertraut machen, einschließlich kurzer Anweisungen zur Einrichtung einer grundlegenden Implementierung.

![Bild mit der Auswahl von [!UICONTROL Datenschutzkonsole] im linken Navigationsbereich der Platform-Benutzeroberfläche](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Nächste Schritte

Weitere Informationen zu den verschiedenen Platform-Diensten, die mit Datenschutzanwendungsfällen verknüpft sind, finden Sie in der folgenden Dokumentation:

* [Attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md)
* [Audit-Protokolle](./audit-logs/overview.md)
* [Data Governance](../../data-governance/home.md)
* [Datenhygiene](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
