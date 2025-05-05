---
title: QoE (Quality of Experience)-Datendetails-Reporting-Datentyp
description: Erfahren Sie mehr über den Datentyp QoE (Quality of Experience)-Datendetails Reporting-Datentyp Experience-Datenmodell (XDM).
exl-id: 608baa9b-12ca-466c-a962-1401abc0344e
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# QoE-Datentyp (Quality of Experience) - Datendetails

[!UICONTROL QoE-Datendetails] Die Berichterstellung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der detaillierte Metriken zur Erlebnisqualität (QoE) während der Medienwiedergabe bereitstellt. Verwenden Sie den Datentyp [!UICONTROL QoE]Datendetails: Reporting, um Details wie Bitrateninformationen, Frameraten, Pufferereignisse, ausgelassene Frames usw. zu erfassen. Medienberichterstellungsfelder werden von Adobe-Services verwendet, um die von Benutzenden gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten erfasst. Dieser Datentyp ermöglicht die Analyse der Wiedergabequalität und bietet Einblicke in die Streaming-Leistung, das Benutzererlebnis und potenzielle Probleme, die in Wiedergabesitzungen auftreten.

+++Wählen Sie diese Option, um den Datentyp QoE-Datendetails-Reporting anzuzeigen.
![Ein Diagramm zum Datentyp QoE-Datendetails (Quality of Experience) für die Berichterstellung.](../images/data-types/qoe-data-details-reporting.png)
+++

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Video-Anzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Überlegungen.

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|---------------------------------------------------------------------------------------------------|
| [[!UICONTROL Durchschnittliche Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate-1) | `bitrateAverage` | number | Die durchschnittliche Bitrate (in kbps, Ganzzahl). Berechnet als gewichteter Durchschnitt von Bitratenwerten. |
| [[!UICONTROL Bucket mit durchschnittlicher Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrateAverageBucket` | Zeichenfolge | Die durchschnittliche Bitrate (in kbps), kategorisiert in vordefinierten Buckets in 100-kbps-Intervallen. |
| [[!UICONTROL bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | integer | Der Bitratenwert (in kbps). |
| [[!UICONTROL Von Bitratenänderung betroffene Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-change-impacted-streams) | `hasBitrateChangeImpactedStreams` | Boolescher Wert | Gibt an, ob Streams von Bitratenänderungen während der Wiedergabe betroffen waren. |
| [[!UICONTROL Bitratenänderungen]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-changes) | `bitrateChangeCount` | integer | Die Gesamtanzahl der Bitratenänderungen während der Wiedergabe. |
| [[!UICONTROL Pufferereignisse]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-events) | `bufferCount` | integer | Die Anzahl verschiedener Pufferzustände während der Wiedergabe. |
| [[!UICONTROL Vom Puffer betroffene Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-impacted-streams) | `hasBufferImpactedStreams` | Boolescher Wert | Gibt an, ob Streams durch Pufferung während der Wiedergabe beeinträchtigt wurden. |
| [[!UICONTROL Von Dropped Frames betroffene Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frame-impacted-streams) | `hasDroppedFrameImpactedStreams` | Boolescher Wert | Gibt an, ob Streams durch ausgelassene Frames während der Wiedergabe beeinflusst wurden. |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames-1) | `droppedFrames` | integer | Die Gesamtzahl der bei der Wiedergabe verschobenen Frames. |
| [[!UICONTROL Drops vor dem Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#drops-before-start) | `isDroppedBeforeStart` | Boolescher Wert | Gibt an, ob Benutzende das Video vor dem Start beenden, unabhängig von Anzeigen. |
| [[!UICONTROL Von Fehlern betroffene Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#error-impacted-streams) | `hasErrorImpactedStreams` | Boolescher Wert | Zeigt an, ob bei Streams während der Wiedergabe Fehler aufgetreten sind. |
| [[!UICONTROL Fehler]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#errors-%2F-error-events) | `errorCount` | integer | Die Gesamtzahl der bei der Wiedergabe aufgetretenen Fehler. |
| [[!UICONTROL Externe Fehler-IDs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#external-error-ids) | `externalErrors` | Zeichenfolgen-Array | Eindeutige Fehler-IDs aus externen Quellen, z. B. CDN-Fehler. |
| [[!UICONTROL Frames pro Sekunde]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | integer | Die aktuelle Stream-Framerate (in Frames pro Sekunde). |
| [[!UICONTROL Media SDK-Fehler-IDs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#media-sdk-error-ids) | `mediaSdkErrors` | Zeichenfolgen-Array | Eindeutige Fehler-IDs, die von Media SDK während der Wiedergabe generiert wurden. |
| [[!UICONTROL Player SDK-Fehler-IDs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#player-sdk-error-ids) | `playerSdkErrors` | Zeichenfolgen-Array | Eindeutige Fehler-IDs, die vom Player-SDK während der Wiedergabe generiert wurden. |
| [[!UICONTROL Verzögerte &#x200B;]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-events) | `stallCount` | integer | Anzahl der ausstehenden Ereignisse während der Wiedergabe. |
| [[!UICONTROL Betroffene Streams verzögern]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-impacted-streams) | `hasStallImpactedStreams` | Boolescher Wert | Zeigt an, ob Streams während der Wiedergabe angehalten wurden. |
| [[!UICONTROL Zeit bis zum Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | integer | Dauer (in Sekunden) zwischen Laden und Starten des Videos. |
| [[!UICONTROL Gesamtdauer des Puffers]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-buffer-duration-1) | `bufferTime` | integer | Gesamtdauer der Pufferung während der Wiedergabe (in Sekunden). |
| [[!UICONTROL Gesamtdauer der Verzögerung]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-stalling-duration) | `stallTime` | integer | Die Gesamtzeit (in Sekunden), in der die Wiedergabe während der Wiedergabe unterbrochen wurde. |

{style="table-layout:auto"}
