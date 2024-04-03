---
title: Datenerfassungstyp QoE (Qualität des Erlebnisses)-Datendetails
description: Erfahren Sie mehr über den Datentyp QoE (Quality of Experience) Data Details Data Collection Type Experience Data Model (XDM) .
source-git-commit: e1c94635b691c68de6154d19e974bfdf2e250923
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# QoE-Datentyp (Qualität des Erlebnisses) Datenerfassung

[!UICONTROL QoE-Datendetails] Die Erfassung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der detaillierte Metriken zur Erlebnisqualität (QoE) während der Medienwiedergabe bereitstellt. Verwenden Sie die [!UICONTROL QoE-Datendetails] Sammlungsdatentyp zum Erfassen von Details wie Bitrateninformationen, Frameraten, Pufferereignissen, Dropped Frames usw. Medienerfassungsfelder erfassen Daten und senden sie zur weiteren Verarbeitung an andere Adobe-Dienste. Dieser Datentyp ermöglicht die Analyse der Wiedergabequalität, sodass Einblicke in die Streaming-Leistung, das Benutzererlebnis und potenzielle Probleme während der Wiedergabesitzungen möglich sind.

+++Auswählen , um den Datentyp QoE-Datendetails anzuzeigen.
![Ein Diagramm des Datenerfassungsdatentyps QoE (Qualität des Erlebnisses).](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Videoanzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Aspekten.

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | integer | Nein | Der Bitratenwert (in Kbit/s). |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames) | `droppedFrames` | integer | Nein | Die Gesamtzahl der Frames, die während der Wiedergabe abgelegt wurden. |
| [[!UICONTROL Bilder pro Sekunde]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | integer | Nein | Die aktuelle Stream-Framerate (in Frames pro Sekunde). |
| [[!UICONTROL Zeit bis Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | integer | Nein | Dauer (in Sekunden) zwischen dem Laden und Starten des Videos. |

{style="table-layout:auto"}
