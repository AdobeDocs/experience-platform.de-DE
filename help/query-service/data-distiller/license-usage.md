---
title: Überwachung der Nutzung der Batch Query-Lizenz
description: Die Benutzeroberfläche von Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zur Verwendung der Data Distiller-Lizenz durch Ihr Unternehmen anzeigen können.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
hide: true
hidefromtoc: true
source-git-commit: aa209dce9268a15a91db6e3afa7b6066683d76ea
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 15%

---

# (Alpha) Überwachen der Nutzung von Batch-Abfragelizenzen {#monitor-license-usage}

>[!IMPORTANT]
>
>Die Möglichkeit, die Nutzung der Batch-Abfragelizenz über die Benutzeroberfläche zu überwachen, ist noch nicht für alle Benutzer verfügbar. Diese Funktion befindet sich in der Alpha-Phase und wird noch getestet. Dieses Dokument kann sich ändern.

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zur Nutzung der Query Service-Lizenz in Ihrem Unternehmen anzeigen können.

Eine detaillierte Anleitung dazu, wie Sie das Lizenznutzungs-Dashboard in der Benutzeroberfläche aufrufen und nutzen können, sowie Informationen zu den im Dashboard verfügbaren Metriken finden Sie im [Abschnitt zum Lizenznutzungs-Dashboard](../../dashboards/guides/license-usage.md).

Bitte lesen Sie die [Übersicht über Dashboards](../../dashboards/home.md) für eine Zusammenfassung aller Dashboard-Funktionen in Experience Platform.

## Widgets {#widgets}

Das Dashboard zur Lizenznutzung besteht aus Widgets, die schreibgeschützte Metriken anzeigen, die wichtige Informationen zur Lizenzverwendung in Ihrem Unternehmen enthalten. Die sichtbaren Metriken hängen von der spezifischen Lizenzierung Ihres Unternehmens ab.

Wählen Sie ein Optionsfeld aus, um eine Sandbox für die Analyse auszuwählen, und wählen Sie über das Dropdown-Menü einen Zeitraum für die Analyse aus. Die verfügbaren Optionen sind ein Zeitraum von 30 Tagen, 90 Tagen, 12 Monaten, das letzte Jahr, der vollständige Vertragszeitraum oder ein benutzerdefiniertes Datum.

## Berechnungsstunden {#compute-hours}

Die [!UICONTROL Berechnungsstunden] Widget verwendet ein Liniendiagramm, um die Verarbeitungszeit für Batch-Abfragen in Ihrem Unternehmen jeden Tag zu visualisieren. Das Widget zeigt drei Metriken an, die durch eine Zahl oben links im Widget angegeben werden. Sie lauten wie folgt

- [!UICONTROL Aktuell]: Die Gesamtzahl der Berechnungsstunden für den im Dropdown-Menü &quot;Übersicht&quot;ausgewählten Zeitraum. Diese Metrik wird auch im Diagramm durch eine durchgehende Linie angezeigt.
- [!UICONTROL Lizenziert]: Die Gesamtzahl der durch die Lizenzvereinbarung Ihres Unternehmens zulässigen Berechnungsstunden. Diese Metrik wird auch im Diagramm durch eine gepunktete Linie angezeigt.
- [!UICONTROL Nutzung]: Dies ist der Prozentsatz Ihrer Nutzung in Bezug auf die maximalen von Ihrer Lizenz vereinbarten Berechnungsstunden.

>[!IMPORTANT]
>
>Die [!UICONTROL Berechnungsstunden] -Widget gilt nur für Kunden mit der Data Distiller-Lizenz für Batch-Abfragen.

![Das Dashboard zur Lizenznutzung mit hervorgehobenem Widget zur Berechnung der Stunden.](../images/data-distiller/compute-hours.png)

