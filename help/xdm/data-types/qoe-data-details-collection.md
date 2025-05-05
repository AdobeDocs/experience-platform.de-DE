---
title: Datentyp der QoE-Datenerfassung (Quality of Experience)
description: Erfahren Sie mehr über den Datentyp Experience-Datenmodell (XDM) des Datenerfassungstyps QoE (Quality of Experience).
exl-id: d99816d9-e207-434a-9a40-ee9ded46c4d2
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# Datentyp der QoE-Datenerfassung (Quality of Experience)

[!UICONTROL QoE-]: Die Datenerfassung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der detaillierte Metriken zur Erlebnisqualität (QoE) während der Medienwiedergabe bereitstellt. Verwenden Sie den Datentyp [!UICONTROL QoE]Datendetails, um Details wie Bitrateninformationen, Frameraten, Pufferereignisse, ausgelassene Frames usw. zu erfassen. Mediensammlungsfelder erfassen Daten und senden sie zur weiteren Verarbeitung an andere Adobe-Services. Dieser Datentyp ermöglicht die Analyse der Wiedergabequalität und bietet Einblicke in die Streaming-Leistung, das Benutzererlebnis und potenzielle Probleme, die in Wiedergabesitzungen auftreten.

+++Wählen Sie diese Option aus, um den Datentyp QoE-Datendetails anzuzeigen.
![Diagramm zum Datentyp der QoE-Datenerfassung (Quality of Experience).](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Jeder Anzeigename enthält einen Link zu weiteren Informationen zu den Audio- und Videoparametern. Die verknüpften Seiten enthalten Details zu den von Adobe erfassten Video-Anzeigendaten, Implementierungswerten, Netzwerkparametern, Berichten und wichtigen Überlegungen.

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=de#average-bitrate) | `bitrate` | integer | Nein | Der Bitratenwert (in kbps). |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=de#dropped-frames) | `droppedFrames` | integer | Nein | Die Gesamtzahl der bei der Wiedergabe verschobenen Frames. |
| [[!UICONTROL Frames pro Sekunde]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=de#frames-per-second) | `framesPerSecond` | integer | Nein | Die aktuelle Stream-Framerate (in Frames pro Sekunde). |
| [[!UICONTROL Zeit bis zum Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=de#time-to-start-1) | `timeToStart` | integer | Nein | Dauer (in Sekunden) zwischen Laden und Starten des Videos. |

{style="table-layout:auto"}
