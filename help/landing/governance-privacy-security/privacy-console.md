---
title: Übersicht über die Datenschutzkonsole
description: Erfahren Sie, wie Sie Ihre datenschutzbezogenen Workflows in der Adobe Experience Platform-Benutzeroberfläche überwachen.
feature: Privacy
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 4%

---

# Übersicht über die Datenschutzkonsole

Die [!UICONTROL Datenschutzkonsole] in der Adobe Experience Platform-Benutzeroberfläche bietet eine Dashboard-Ansicht Ihrer datenschutzbezogenen Vorgänge in Platform, einschließlich Arbeitsaufträgen zur Datenhygiene, Anfragen von betroffenen Personen vom Privacy Service und Audit-Protokollen für Platform-Benutzeraktivitäten.

Um auf das Dashboard zuzugreifen, wählen Sie **[!UICONTROL Datenschutzkonsole]** im linken Navigationsbereich aus.

![Bild, das [!UICONTROL Datenschutzkonsole] zeigt, die im linken Navigationsbereich in der Platform-Benutzeroberfläche ausgewählt wird](../images/governance-privacy-security/privacy-console/left-nav.png)

Von hier aus können Sie sich die verfügbaren [Überwachungs-Widgets](#widgets) ansehen, die von der Konsole bereitgestellt werden, oder Sie können eines von mehreren [Handbüchern zu Anwendungsfällen](#use-case-guides) zu den Datenschutzfunktionen von Platform durchsuchen.

## Widgets

[!UICONTROL Datenschutzkonsole] bietet mehrere Widgets zur Überwachung Ihrer Datenschutzvorgänge.

![Bild, das [!UICONTROL Datenschutzkonsole] zeigt, die im linken Navigationsbereich in der Platform-Benutzeroberfläche ausgewählt wird](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Je nach den von Ihrem Unternehmen erworbenen SKUs sind einige der unten genannten Widgets möglicherweise nicht verfügbar.

Die Funktion der einzelnen Widgets wird unten erläutert:

| Widget-Name | Beschreibung |
| --- | --- |
| Status des Arbeitsauftrags zur Datenhygiene | Zeigt die Status der Löschvorgänge von Datensätzen unter [Datenhygiene](../../hygiene/home.md) für den ausgewählten Zeitrahmen an. Verwenden Sie das Dropdown-Menü, um den Zeitrahmen zwischen den letzten 7 Tagen, 14 Tagen und 30 Tagen zu ändern. |
| Aktuelle Arbeitsaufträge zur Datenhygiene | Zeigt die neuesten [Datenhygiene](../../hygiene/home.md) Arbeitsaufträge an, die vom System verarbeitet werden. Verwenden Sie das Dropdown-Menü, um zwischen kürzlich erstellten und kürzlich aktualisierten Arbeitsaufträgen zu wechseln. |
| Häufigste Aktionen | Zeigt die häufigsten Aktionen auf Platform an, die von [Auditprotokollen](./audit-logs/overview.md) für den ausgewählten Zeitraum erfasst werden. Verwenden Sie das Dropdown-Menü, um den Zeitrahmen zwischen den letzten 7 Tagen, 14 Tagen und 30 Tagen zu ändern. |
| Aktivste Benutzer | Zeigt die aktivsten Platform-Benutzer innerhalb Ihrer Organisation an, wie durch [Auditprotokolle](./audit-logs/overview.md) für den ausgewählten Zeitraum erfasst. Verwenden Sie das Dropdown-Menü, um den Zeitrahmen zwischen den letzten 7 Tagen, 14 Tagen und 30 Tagen zu ändern. |
| Anfragen durch betroffene Personen | Zeigt die Anzahl der von der betroffenen Person gesendeten und abgeschlossenen Anfragen bis zum [Privacy Service ](../../privacy-service/home.md) an einem bestimmten Tag. |

{style="table-layout:auto"}

## Handbücher zu Anwendungsfällen

Die Konsole bietet mehrere produktinterne Handbücher, die Ihnen allgemeine Datenschutz-Workflows in Platform vorstellen, einschließlich knapper Anweisungen zum Einrichten einer einfachen Implementierung.

![Bild, das [!UICONTROL Datenschutzkonsole] zeigt, die im linken Navigationsbereich in der Platform-Benutzeroberfläche ausgewählt wird](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Nächste Schritte

Weitere Informationen zu den verschiedenen Platform-Services, die mit Anwendungsfällen für den Datenschutz verknüpft sind, finden Sie in der folgenden Dokumentation:

* [Attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md)
* [Audit-Protokolle](./audit-logs/overview.md)
* [Data Governance](../../data-governance/home.md)
* [Datenhygiene](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
