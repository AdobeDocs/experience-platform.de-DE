---
title: QoE (Quality of Experience)-Datendetails Berichtdatentyp
description: Erfahren Sie mehr über den Datentyp QoE (Quality of Experience) Data Details Reporting Data Type Experience Data Model (XDM) .
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# QoE (Quality of Experience) Datendetails Berichtdatentyp

[!UICONTROL QoE-Datendetails] Die Berichterstellung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der detaillierte Metriken zur Erlebnisqualität (QoE) während der Medienwiedergabe bereitstellt. Verwenden Sie die [!UICONTROL QoE-Datendetails] Berichtdatentyp zum Erfassen von Details wie Bitrateninformationen, Frameraten, Pufferereignissen, Dropped Frames usw. Die Felder für die Medienberichte werden von Adobe-Diensten verwendet, um die von Benutzern gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten verwendet. Dieser Datentyp ermöglicht die Analyse der Wiedergabequalität, sodass Einblicke in die Streaming-Leistung, das Benutzererlebnis und potenzielle Probleme während der Wiedergabesitzungen möglich sind.

++ + Wählen Sie diese Option, um den Datentyp QoE-Datendetails-Berichterstellung anzuzeigen.
![Ein Diagramm des Datentyps QoE (Quality of Experience) Data Details Reporting .](../images/data-types/qoe-data-details-reporting.png)
+++

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Videoanzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Aspekten.

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|---------------------------------------------------------------------------------------------------|
| [[!UICONTROL Durchschnittliche Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate-1) | `bitrateAverage` | number | Die durchschnittliche Bitrate (in Kbit/s, Integer). Wird als gewichteter Durchschnitt der Bitratenwerte berechnet. |
| [[!UICONTROL Durchschnittlicher Bitratenbehälter]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrateAverageBucket` | Zeichenfolge | Die durchschnittliche Bitrate (in Kbit/s), die in vordefinierten Behältern mit Intervallen von 100 Kbit/s kategorisiert ist. |
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | integer | Der Bitratenwert (in Kbit/s). |
| [[!UICONTROL Von Bitratenänderung betroffene Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-change-impacted-streams) | `hasBitrateChangeImpactedStreams` | Boolescher Wert | Gibt an, ob Streams während der Wiedergabe von Bitratenänderungen betroffen waren. |
| [[!UICONTROL Bitratenänderungen]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-changes) | `bitrateChangeCount` | integer | Die Gesamtanzahl der Bitratenänderungen während der Wiedergabe. |
| [[!UICONTROL Pufferereignisse]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-events) | `bufferCount` | integer | Die Anzahl verschiedener Pufferstatus während der Wiedergabe. |
| [[!UICONTROL Von Puffer betroffene Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-impacted-streams) | `hasBufferImpactedStreams` | Boolescher Wert | Gibt an, ob die Pufferung während der Wiedergabe Auswirkungen auf Streams hatte. |
| [[!UICONTROL Von Dropped Frames betroffene Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frame-impacted-streams) | `hasDroppedFrameImpactedStreams` | Boolescher Wert | Gibt an, ob Streams von Dropped Frames während der Wiedergabe beeinflusst wurden. |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames-1) | `droppedFrames` | integer | Die Gesamtzahl der Frames, die während der Wiedergabe abgelegt wurden. |
| [[!UICONTROL Drops vor Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#drops-before-start) | `isDroppedBeforeStart` | Boolescher Wert | Gibt unabhängig von Anzeigen an, ob Benutzer das Video vor dem Start verlassen. |
| [[!UICONTROL Von Fehlern betroffene Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#error-impacted-streams) | `hasErrorImpactedStreams` | Boolescher Wert | Gibt an, ob in Streams während der Wiedergabe Fehler aufgetreten sind. |
| [[!UICONTROL Fehler]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#errors-%2F-error-events) | `errorCount` | integer | Die Gesamtzahl der Fehler, die während der Wiedergabe aufgetreten sind. |
| [[!UICONTROL Externe Fehler-IDs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#external-error-ids) | `externalErrors` | Zeichenfolgen-Array | Eindeutige Fehler-IDs aus externen Quellen, z. B. CDN-Fehler. |
| [[!UICONTROL Bilder pro Sekunde]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | integer | Die aktuelle Stream-Framerate (in Frames pro Sekunde). |
| [[!UICONTROL Medien-SDK Fehler-IDs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#media-sdk-error-ids) | `mediaSdkErrors` | Zeichenfolgen-Array | Vom Media SDK während der Wiedergabe generierte eindeutige Fehler-IDs. |
| [[!UICONTROL Player-SDK Fehler-IDs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#player-sdk-error-ids) | `playerSdkErrors` | Zeichenfolgen-Array | Vom Player-SDK während der Wiedergabe erzeugte eindeutige Fehler-IDs. |
| [[!UICONTROL Unterbrechungsereignisse]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-events) | `stallCount` | integer | Die Anzahl der Unterbrechungsereignisse während der Wiedergabe. |
| [[!UICONTROL Von Unterbrechung betroffene Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-impacted-streams) | `hasStallImpactedStreams` | Boolescher Wert | Gibt an, ob bei Streams während der Wiedergabe eine Unterbrechung aufgetreten ist. |
| [[!UICONTROL Zeit bis Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | integer | Dauer (in Sekunden) zwischen dem Laden und Starten des Videos. |
| [[!UICONTROL Gesamtpufferdauer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-buffer-duration-1) | `bufferTime` | integer | Gesamtdauer der Pufferung während der Wiedergabe (in Sekunden). |
| [[!UICONTROL Gesamte Unterbrechungsdauer]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-stalling-duration) | `stallTime` | integer | Die Gesamtdauer (in Sekunden), zu der die Wiedergabe während der Wiedergabe unterbrochen wurde. |

{style="table-layout:auto"}
