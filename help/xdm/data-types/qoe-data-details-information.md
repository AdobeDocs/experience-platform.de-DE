---
title: QoE-Datentyp (Qualität des Erlebnisses) Datendetails Datentyp
description: Erfahren Sie mehr über den Datentyp QoE (Quality of Experience) Data Details Information Data Type Experience Data Model (XDM) .
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 6%

---

# QoE-Datentyp (Qualität des Erlebnisses) Datendetails Datentyp

[!UICONTROL Informationen zu QoE-Daten] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der detaillierte Metriken zur Erlebnisqualität (QoE) während der Medienwiedergabe bereitstellt. Verwenden Sie die [!UICONTROL Informationen zu QoE-Daten] Datentyp zum Erfassen von Details wie Bitrateninformationen, Frameraten, Pufferereignissen, Dropped Frames usw. Dieser Datentyp ermöglicht die Analyse der Wiedergabequalität, sodass Einblicke in die Streaming-Leistung, das Benutzererlebnis und potenzielle Probleme während der Wiedergabesitzungen möglich sind.

++ + Wählen Sie diese Option aus, um den Datentyp QoE-Datendetails anzuzeigen.
![Ein Diagramm des Datentyps QoE (Quality of Experience) Data Details Information .](../images/data-types/qoe-data-details-information.png)
+++

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------------------|----------------------------|-----------|--------------------------------------------------------------------------------------------------|
| [!UICONTROL Durchschnittlicher Bitratenbehälter] | `bitrateAverageBucket` | Zeichenfolge | Die durchschnittliche Bitrate (in Kbit/s), die in vordefinierten Behältern mit Intervallen von 100 Kbit/s kategorisiert ist. |
| [!UICONTROL Bitrate] | `bitrate` | integer | Der Bitratenwert (in Kbit/s). |
| [!UICONTROL Durchschnittliche Bitrate] | `bitrateAverage` | number | Die durchschnittliche Bitrate (in Kbit/s, Integer). Wird als gewichteter Durchschnitt der Bitratenwerte berechnet. |
| [!UICONTROL Von Bitratenänderung betroffene Streams] | `hasBitrateChangeImpactedStreams` | boolean | Gibt an, ob Streams während der Wiedergabe von Bitratenänderungen betroffen waren. |
| [!UICONTROL Bitratenänderungen] | `bitrateChangeCount` | integer | Die Gesamtanzahl der Bitratenänderungen während der Wiedergabe. |
| [!UICONTROL Von Dropped Frames betroffene Streams] | `hasDroppedFrameImpactedStreams` | boolean | Gibt an, ob Streams von Dropped Frames während der Wiedergabe beeinflusst wurden. |
| [!UICONTROL Dropped Frames] | `droppedFrames` | integer | Die Gesamtzahl der Frames, die während der Wiedergabe abgelegt wurden. |
| [!UICONTROL Drops vor Start] | `isDroppedBeforeStart` | boolean | Gibt unabhängig von Anzeigen an, ob Benutzer das Video vor dem Start verlassen. |
| [!UICONTROL Bilder pro Sekunde] | `framesPerSecond` | integer | Die aktuelle Stream-Framerate (in Frames pro Sekunde). |
| [!UICONTROL Zeit bis Start] | `timeToStart` | integer | Dauer (in Sekunden) zwischen dem Laden und Starten des Videos. |
| [!UICONTROL Von Puffer betroffene Streams] | `hasBufferImpactedStreams` | boolean | Gibt an, ob die Pufferung während der Wiedergabe Auswirkungen auf Streams hatte. |
| [!UICONTROL Pufferereignisse] | `bufferCount` | integer | Die Anzahl verschiedener Pufferstatus während der Wiedergabe. |
| [!UICONTROL Gesamtpufferdauer] | `bufferTime` | integer | Gesamtdauer der Pufferung während der Wiedergabe (in Sekunden). |
| [!UICONTROL Von Fehlern betroffene Streams] | `hasErrorImpactedStreams` | boolean | Gibt an, ob in Streams während der Wiedergabe Fehler aufgetreten sind. |
| [!UICONTROL Fehler] | `errorCount` | integer | Die Gesamtzahl der Fehler, die während der Wiedergabe aufgetreten sind. |
| [!UICONTROL Von Unterbrechung betroffene Streams] | `hasStallImpactedStreams` | boolean | Gibt an, ob bei Streams während der Wiedergabe eine Unterbrechung aufgetreten ist. |
| [!UICONTROL Unterbrechungsereignisse] | `stallCount` | integer | Die Anzahl der Unterbrechungsereignisse während der Wiedergabe. |
| [!UICONTROL Gesamte Unterbrechungsdauer] | `stallTime` | integer | Die Gesamtdauer (in Sekunden), zu der die Wiedergabe während der Wiedergabe unterbrochen wurde. |
| [!UICONTROL Player-SDK Fehler-IDs] | `playerSdkErrors` | Zeichenfolgen-Array | Vom Player-SDK während der Wiedergabe erzeugte eindeutige Fehler-IDs. |
| [!UICONTROL Externe Fehler-IDs] | `externalErrors` | Zeichenfolgen-Array | Eindeutige Fehler-IDs aus externen Quellen, z. B. CDN-Fehler. |
| [!UICONTROL Medien-SDK Fehler-IDs] | `mediaSdkErrors` | Zeichenfolgen-Array | Vom Media SDK während der Wiedergabe generierte eindeutige Fehler-IDs. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json).

