---
title: getMediaAnalyticsTracker
description: Erfahren Sie, wie Sie ein Media Analytics-Tracker-Objekt erstellen und es zur Verfolgung von Medienereignissen verwenden.
source-git-commit: 9384c1cc15441199e898d6cc0850e5422253f106
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---


# `getMediaAnalyticsTracker`

Mit diesem Web SDK-Befehl wird ein Media Analytics-Tracker abgerufen. Mit diesem Befehl können Sie eine Objektinstanz erstellen und dann dieselben APIs wie die von der [Media JS-Bibliothek](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html), verfolgen Sie Medienereignisse.

Die `getMediaAnalyticsTracker` gibt die Legacy Media Analytics-API zurück.


| Name der Methode | Beschreibung | Aufbau |
|-----------------|---|----------------|
| `getInstance` | Erstellt eine Medieninstanz zur Verfolgung der Wiedergabesitzung. | `Media.getInstance()` |
| `createMediaObject` | Erstellt ein Objekt, das Medieninformationen enthält. Gibt ein leeres Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | Erstellt ein Objekt, das Informationen zu Werbeunterbrechungen enthält. Gibt ein leeres Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | Erstellt ein Objekt, das Anzeigeninformationen enthält. Gibt ein leeres Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | Erstellt ein Objekt, das Kapitelinformationen enthält. Gibt ein leeres Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | Erstellt ein Objekt, das Statusinformationen enthält. Gibt ein leeres Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createStateObject(name)` |
| `createQoEObject` | Erstellt ein Objekt, das QoE-Informationen enthält. Gibt ein leeres Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## Instanzmethoden

| Name der Methode | Beschreibung | Aufbau |
|---|---|----|
| `trackSessionStart` | Verfolgen Sie die Absicht, die Wiedergabe zu starten. Dadurch wird eine Tracking-Sitzung in der Media-Tracker-Instanz gestartet. | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | Tracking der Wiedergabe oder Wiederaufnahme von Medien nach einer vorherigen Pause | `trackerInstance.trackPlay()` |
| `trackPause` | Verfolgen Sie die Medienpause. | `trackerInstance.trackPause()` |
| `trackComplete` | Verfolgen Sie den Medienabschluss. Rufen Sie diese Methode nur auf, wenn die Medien vollständig angezeigt wurden. | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | Verfolgen Sie das Ende einer Anzeigesitzung. Rufen Sie diese Methode auf, selbst wenn der Benutzer die Medien nicht bis zum Ende anzeigt. | `trackerInstance.trackSessionEnd()` |
| `trackError` | Verfolgen Sie einen Fehler, der während der Medienwiedergabe aufgetreten ist. | `trackerInstance.trackError("errorId")` |
| `trackEvent` | Verfolgen Sie ein benutzerspezifisches Ereignis. | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | Aktualisieren Sie die Position der Abspielleiste. | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | Aktualisieren Sie die Erlebnisqualität. | `trackerInstance.updateQoEObject(qoe)` |

## Konstanten

| Konstantenname | Beschreibung | Wert |
|-----------------|--|-----------------|
| `MediaType` | Medientyp | `Video`, `Audio` |
| `StreamType` | Stream-Typ | `VOD`, `Live`, `Linear`, `Podcast`, `Audiobook`, `AOD` |
| `VideoMetadataKeys` | Dadurch werden Standard-Metadatenschlüssel für Video-Streams definiert | `Show`, `Season`, `Episode`, `AssetId`, `Genre`, `FirstAirDate`, `FirstDigitalDate`, `Rating`, `Originator`, `Network`, `ShowType`, `AdLoad`, `MVPD`, `Authorized`, `DayPart`, `Feed`, `StreamFormat` |
| `AudioMetadataKeys` | Dadurch werden die Standard-Metadatenschlüssel für Audio-Streams definiert. | `Artist`, `Album`, `Label`, `Author`, `Station`, `Publisher` |
| `AdMetadataKeys` | Dadurch werden die Standard-Metadatenschlüssel für Anzeigen definiert. | `Advertiser`, `CampaignId`, `CreativeId`, `PlacementId`, `SiteId`, `CreativeUrl` |
| `Event` | Damit wird der Typ eines Tracking-Ereignisses definiert. | `AdBreakStart`, `AdBreakComplete`, `AdStart`, `AdComplete`, `AdSkip`, `ChapterStart`, `ChapterComplete`, `ChapterSkip`, `SeekStart`, `SeekComplete`, `BufferStart`, `BufferComplete`, `BitrateChange`, `StateStart`, `StateEnd` |
| `PlayerState` | Dadurch werden Standardwerte für das Tracking des Player-Status definiert. | `FullScreen`, `ClosedCaption`, `Mute`, `PictureInPicture`, `InFocus` |
