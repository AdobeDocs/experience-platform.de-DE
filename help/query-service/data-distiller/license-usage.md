---
title: Überwachung der Nutzung der Batch Query-Lizenz
description: Die Benutzeroberfläche von Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zur Verwendung der Data Distiller-Lizenz durch Ihr Unternehmen anzeigen können.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: a3a2377a873c0e54ba43a60e28f922e0cb9e9d01
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Überwachen der Nutzung von Batch-Abfragelizenzen {#monitor-license-usage}

Das Dashboard zur Lizenznutzung bietet detaillierte Berichte über die Query Service-Lizenznutzung und -Nutzungsmetriken Ihres Unternehmens für jedes gekaufte Produkt. Weitere Informationen zu den verfügbaren Metriken, die im Dashboard angezeigt werden, finden Sie unter [Dashboard-Handbuch zur Lizenznutzung](../../dashboards/guides/license-usage.md#available-metrics).

Das Dashboard bietet Nutzungsmetriken für jedes gekaufte Produkt, die konsolidierte Verwendung von Metriken in allen Produktions- oder Entwicklungs-Sandboxes und die Nutzungsmetriken aus einer bestimmten Sandbox. Die hier angezeigten Informationen werden während einer täglichen Momentaufnahme Ihrer Platform-Instanz erfasst.

>[!NOTE]
>
>Das Dashboard zur Lizenznutzung ist standardmäßig nicht aktiviert. Benutzern muss die Berechtigung &quot;Dashboard zur Lizenznutzung anzeigen&quot;gewährt werden, damit sie das Dashboard anzeigen können. Anweisungen zum Gewähren von Zugriffsberechtigungen für die Anzeige des Dashboards zur Lizenznutzung finden Sie im Abschnitt [Dashboard-Berechtigungshandbuch](../../dashboards/permissions.md).

## Berechnungsstunden {#compute-hours}

Die [!UICONTROL Berechnungsstunden] -Metrik gilt nur für Kunden mit der Data Distiller-Lizenz für Batch-Abfragen. [!UICONTROL Berechnungsstunden] sind die Zeitwerte, die von den Query Service-Engines benötigt werden, um Daten bei der Ausführung einer Batch-Abfrage zu lesen, zu verarbeiten und in den Data Lake zurückzuschreiben.

>[!NOTE]
>
>**Die Daten sind mit Einschränkungen verfügbar**: Die Daten beginnen am 1. Oktober 2023 ohne Trends.<br>Die **Aufstockung** von Daten aus Ihrem Vertragsbeginn ist eine laufende Arbeit. Es wird voraussichtlich bis Ende des Kalenderjahres verfügbar sein.

![Das Dashboard zur Lizenznutzung mit hervorgehobener Metrik für Berechnungsstunden.](../images/data-distiller/compute-hours.png)

Weitere Informationen zu den für Ihre Organisation basierend auf der erworbenen Lizenz verfügbaren Metriken finden Sie in der [Dashboard-Handbuch zur Lizenznutzung](../../dashboards/guides/license-usage.md).
