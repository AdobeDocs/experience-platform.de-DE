---
title: Überwachen der Streaming-Profilaufnahme
description: Erfahren Sie, wie Sie die Aufnahme von Streaming-Profilen mit dem Überwachungs-Dashboard überwachen können
hide: true
hidefromtoc: true
source-git-commit: 2f78b70761ef676fe4ab61b89b6cbb261c99e9ca
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 3%

---

# Überwachen der Streaming-Profilaufnahme

Sie können das Überwachungs-Dashboard in der Adobe Experience Platform-Benutzeroberfläche verwenden, um die Aufnahme von Streaming-Profilen in Ihrer Organisation in Echtzeit zu überwachen. Verwenden Sie diese Funktion, um die Durchsatz-, Latenz- und Datenqualitätsmetriken im Zusammenhang mit Ihren Streaming-Daten transparenter zu gestalten. Darüber hinaus können Sie diese Funktion für proaktive Warnhinweise und den Abruf umsetzbarer Einblicke verwenden, um potenzielle Kapazitätsverletzungen und Probleme bei der Datenaufnahme zu identifizieren.

Lesen Sie das folgende Handbuch, um zu erfahren, wie Sie mit dem Monitoring-Dashboard die Raten und Metriken von Aufnahmen von Streaming-Profilen in Ihrer Organisation überwachen können.

## Das Dashboard zur Aufnahme von Streaming-Profilen

Im Monitoring-Dashboard können Sie drei verschiedene Metrikkategorien für die Streaming-Profilaufnahme verwenden[!UICONTROL &#x200B; „Durchsatz], [!UICONTROL Aufnahme] und [!UICONTROL Latenz].

* **Durchsatz**: Wählen Sie **[!UICONTROL Durchsatz]** aus, um Informationen zur Datenmenge anzuzeigen, die Experience Platform in einem konfigurierten Zeitraum verarbeitet. Beziehen Sie sich auf diese Metrik, um die Effizienz und Kapazität Ihres Systems zu bewerten.
   * **Kapazität**: Die maximale Datenmenge, die Ihre Sandbox unter definierten Bedingungen verarbeiten kann.
   * **Anfragedurchsatz**: Die Rate, mit der Ereignisse vom Aufnahmesystem empfangen werden, gemessen in Ereignissen pro Sekunde.
   * **Verarbeitungsdurchsatz**: Die Rate, mit der das System eingehende Ereignis-Payloads erfolgreich aufnimmt und verarbeitet, gemessen in Ereignissen pro Sekunde.
* **Aufnahme**: Wählen Sie [!UICONTROL Aufnahme] aus, um Informationen zu den Aufnahmevorgängen in Ihrer Sandbox anzuzeigen. Diese Aufnahmevorgänge werden in drei verschiedenen Metriken gemessen:
   * **Erstellte Datensätze**: Die Gesamtzahl der in einem bestimmten Zeitraum erstellten Datensätze. Diese Metrik stellt erfolgreiche Datenaufnahmeprozesse in Ihrer Sandbox dar.
   * **Fehlgeschlagene Datensätze**: Die Gesamtzahl der Datensätze, die aufgrund von Fehlern nicht aufgenommen wurden.
   * **Gelöschte Datensätze**: Die Gesamtzahl der Datensätze, die aufgrund von Verstößen gegen Kapazitätsbeschränkungen gelöscht wurden.
* **Latenz**: Wählen Sie [!UICONTROL Latenz] aus, um Informationen darüber anzuzeigen, wie lange Experience Platform braucht, um innerhalb eines bestimmten Zeitraums auf eine Anfrage zu reagieren oder einen Vorgang abzuschließen.

## Überwachen von Metriken für die Aufnahme von Streaming-Profilen {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="Überwachen der Streaming-Profilaufnahme"
>abstract="Das Monitoring-Dashboard für Streaming-Profile zeigt Informationen über Durchsatz, Aufnahmeraten und Latenz an. Verwenden Sie dieses Dashboard, um die Datenverarbeitungsmetriken anzuzeigen, zu verstehen und zu analysieren. Ihrer Streaming-Profile in Experience Platform."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="Anfragedurchsatz"
>abstract="Diese Metrik stellt die Anzahl der Ereignisse pro Sekunde dar, die in das Aufnahmesystem eintreten."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="Verarbeitungsdurchsatz"
>abstract="Diese Metrik stellt die Anzahl der Ereignisse dar, die vom System jede Sekunde erfolgreich aufgenommen werden."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="P95 Aufnahmelatenz"
>abstract="Diese Metrik misst die 95. Perzentil-Latenz von dem Zeitpunkt an, an dem ein Ereignis in Experience Platform eintrifft, bis zu dem Zeitpunkt, an dem es erfolgreich in den Profilspeicher aufgenommen wurde."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="Maximaler Durchsatz"
>abstract="Diese Metrik stellt die maximale Anzahl eingehender Anfragen pro Sekunde dar, die in die Streaming-Profilaufnahme eintreten."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="Aufgenommene Einträge"
>abstract="Diese Metrik stellt die Gesamtzahl der Datensätze dar, die innerhalb eines konfigurierten Zeitfensters in den Profilspeicher aufgenommen wurden."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="Fehlgeschlagene Einträge"
>abstract="Diese Metrik stellt die Gesamtzahl der Datensätze dar, die innerhalb eines konfigurierten Zeitfensters aufgrund von Fehlern nicht in den Profilspeicher aufgenommen wurden."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="Übersprungene Einträge"
>abstract="Diese Metrik stellt die Gesamtzahl der Datensätze dar, die innerhalb eines konfigurierten Zeitfensters aufgrund von Konfigurations- oder Kapazitätsverstößen verworfen wurden."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="Fehlerdetails"
>abstract="Diese Metrik stellt die Anzahl der aufgrund von Fehlern fehlgeschlagenen Ereignisse dar."
>text="Learn more in documentation"

| Metrik | Beschreibung | Dimensionen | Messhäufigkeit |
| --- | --- | --- | --- |
| Anfragedurchsatz | Diese Metrik stellt die Anzahl der Ereignisse pro Sekunde dar, die in das Aufnahmesystem eintreten. | Sandbox/Datenfluss | Echtzeitüberwachung mit einer Datenaktualisierung alle 60 Sekunden. |
| Verarbeitungsdurchsatz | Diese Metrik stellt die Anzahl der Ereignisse dar, die vom System jede Sekunde erfolgreich aufgenommen werden. | Sandbox/Datenfluss | Echtzeitüberwachung mit einer Datenaktualisierung alle 60 Sekunden. |
| P95 Aufnahmelatenz | Diese Metrik misst die 95. Perzentil-Latenz von dem Zeitpunkt an, an dem ein Ereignis in Experience Platform eintrifft, bis zu dem Zeitpunkt, an dem es erfolgreich in den Profilspeicher aufgenommen wurde. | Sandbox/Datenfluss | Echtzeitüberwachung mit einer Datenaktualisierung alle 60 Sekunden. |
| Maximaler Durchsatz |
| Aufgenommene Einträge | Diese Metrik stellt die Gesamtzahl der Datensätze dar, die innerhalb eines konfigurierten Zeitfensters in den Profilspeicher aufgenommen wurden. | <ul><li>Sandbox/Datenfluss</li><li>Datenflussausführung</li></ul> | <ul><li>Sandbox/Datenfluss: Echtzeit-Überwachung mit einer Datenaktualisierung alle 60 Sekunden.</li><li>Datenflussausführung: in 15 Minuten gruppiert.</li></ul> |
| Fehlgeschlagene Einträge | Diese Metrik stellt die Gesamtzahl der Datensätze dar, die innerhalb eines konfigurierten Zeitfensters aufgrund von Fehlern nicht in den Profilspeicher aufgenommen wurden. | <ul><li>Sandbox/Datenfluss</li><li>Datenflussausführung</li></ul> | <ul><li>Sandbox/Datenfluss: Echtzeit-Überwachung mit einer Datenaktualisierung alle 60 Sekunden.</li><li>Datenflussausführung: in 15 Minuten gruppiert.</li></ul> |
| Übersprungene Einträge | Diese Metrik stellt die Gesamtzahl der Datensätze dar, die innerhalb eines konfigurierten Zeitfensters aufgrund von Konfigurations- oder Kapazitätsverstößen verworfen wurden. | <ul><li>Sandbox/Datenfluss</li><li>Datenflussausführung</li></ul> | <ul><li>Sandbox/Datenfluss: Echtzeit-Überwachung mit einer Datenaktualisierung alle 60 Sekunden.</li><li>Datenflussausführung: in 15 Minuten gruppiert.</li></ul> |
| Fehlerdetails | Diese Metrik stellt die Anzahl der aufgrund von Fehlern fehlgeschlagenen Ereignisse dar. | Datenflussausführung | In einem stündlichen Fenster gruppiert. |

{style="table-layout:auto"}