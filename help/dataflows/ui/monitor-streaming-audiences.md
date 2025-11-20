---
title: Überwachen von Streaming-Zielgruppen
description: Erfahren Sie, wie Sie mit dem Monitoring-Dashboard Zielgruppen überwachen, die mithilfe der Streaming-Segmentierung ausgewertet werden
hide: true
hidefromtoc: true
source-git-commit: 6fe0a36a8f2ac2cb954935ee8fe64432442b6e84
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 9%

---


# Überwachen von Streaming-Zielgruppen

Intro Blurb

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Datenflüsse](../home.md): Datenflüsse stellen Datenaufträge dar, die Informationen über Experience Platform übertragen. Sie werden in verschiedenen -Services konfiguriert, um das Verschieben von Daten von Quell-Connectoren in Zieldatensätze sowie zu Identity Service, Echtzeit-Kundenprofil und Zielen zu erleichtern.
* [Segmentierungs-](../../segmentation/home.md):
* [Kapazitäten](../../landing/license-usage-and-guardrails/capacity.md): In Experience Platform teilen Ihnen die Kapazitäten mit, ob Ihr Unternehmen eine Ihrer Leitplanken überschritten hat, und erhalten Informationen zur Behebung dieser Probleme.

## Überwachen von Metriken für Streaming-Zielgruppen {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="Auswertungsrate"
>abstract="Diese Metrik stellt die Anzahl der pro Sekunde ausgewerteten Datensätze dar."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="P95-Aufnahmelatenz"
>abstract="Diese Metrik misst die 95. Perzentil-Latenz eines Ereignisses, das in Adobe Experience Platform eintrifft, bis zur erfolgreichen Auswertung in der Zielgruppe."
>text="Learn more in documentation"

Die folgende Tabelle enthält detailliertere Informationen zu den Metriken, die für Streaming-Zielgruppen verwendet werden.

| Metrik | Beschreibung | Dimensionen |
| ------ | ----------- | ---------- |
| Auswertungsrate | Die Anzahl der verarbeiteten Zielgruppenauswertungen pro Sekunde. | Sandbox, Datensatz |
| P95-Aufnahmelatenz | Die 95. Perzentil-Latenz der erfolgreichen Ereignisankunft in der Zielgruppe. | Sandbox, Datensatz |
| Empfangene Einträge | Die Gesamtzahl der Datensätze, die von der Streaming-Aufnahme für die Streaming-Segmentierung im ausgewählten Zeitfenster empfangen wurden. | Datensatz |
| Ausgewertete Einträge | Die Gesamtzahl der Datensätze, die **erfolgreich** im ausgewählten Zeitfenster mithilfe der Streaming-Segmentierung ausgewertet wurden. | Datensatz |
| Fehlgeschlagene Einträge | Die Gesamtzahl der Datensätze, die **Auswertung** Streaming-Segmentierung aufgrund von Fehlern im ausgewählten Zeitfenster fehlgeschlagen sind. | Datensatz, Flussausführung |
| Übersprungene Einträge | Die Gesamtzahl der Datensätze, die **Auswertung** Streaming-Segmentierung aufgrund von Fehlern im ausgewählten Zeitfenster übersprungen haben. | Datensatz, Flussausführung |
| Qualifizierte Profile | Die Anzahl der Profile, die sich im ausgewählten Zeitfenster für die Zielgruppe qualifiziert haben. | Sandbox, Zielgruppe |
| Profile disqualifiziert | Die Anzahl der Profile, die sich im ausgewählten Zeitfenster von der Zielgruppe disqualifiziert haben. | Sandbox, Zielgruppe |

{style="table-layout:auto"}

## Verwenden des Monitoring-Dashboards für Streaming-Zielgruppen {#monitoring-dashboard}

Um auf das Überwachungs-Dashboard für Streaming-Zielgruppen zuzugreifen, gehen Sie zur Experience Platform-Benutzeroberfläche, wählen Sie **[!UICONTROL Monitoring]** in der linken Navigationsleiste aus und klicken Sie dann auf **[!UICONTROL Streaming end-to-end]**.

IMAGE

Oben im Dashboard befindet sich die Karte mit der **[!UICONTROL Audiences]** Metrik. Dadurch werden Informationen zur **Auswertungsrate)** Zielgruppen angezeigt.