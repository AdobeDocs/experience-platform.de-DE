---
title: getMediaAnalyticsTracker
description: Erfahren Sie, wie Sie ein Media Analytics-Tracker-Objekt erstellen und zum Verfolgen von Medienereignissen verwenden.
exl-id: ae968da8-7763-4b2a-a716-3014ba0d270d
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---

# `getMediaAnalyticsTracker`

Dieser Web SDK-Befehl ruft einen Media Analytics-Tracker ab. Sie können diesen Befehl verwenden, um eine Objektinstanz zu erstellen, und dann mit denselben APIs wie in der [Media JS Library](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html) Medienereignisse verfolgen.

Der Befehl `getMediaAnalyticsTracker` gibt die veraltete Media Analytics-API zurück.


| Methodenname | Beschreibung | Aufbau |
|-----------------|---|----------------|
| `getInstance` | Erstellt eine Medieninstanz zum Tracking der Wiedergabesitzung. | `Media.getInstance()` |
| `createMediaObject` | Erstellt ein -Objekt, das Medieninformationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | Erstellt ein -Objekt, das Adbreak-Informationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | Erstellt ein -Objekt, das Anzeigeninformationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | Erstellt ein -Objekt, das Kapitelinformationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | Erstellt ein -Objekt, das Statusinformationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createStateObject(name)` |
| `createQoEObject` | Erstellt ein -Objekt, das QoE-Informationen enthält. Gibt ein leeres -Objekt zurück, wenn ungültige Parameter übergeben werden. | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## Instanzmethoden

| Methodenname | Beschreibung | Aufbau |
|---|---|----|
| `trackSessionStart` | Verfolgen Sie die Absicht, die Wiedergabe zu starten. Dadurch wird eine Tracking-Sitzung auf der Media Tracker-Instanz gestartet. | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | Tracking der Medienwiedergabe oder Wiederaufnahme nach einer vorherigen Pause. | `trackerInstance.trackPlay()` |
| `trackPause` | Verfolgen der Medienpause. | `trackerInstance.trackPause()` |
| `trackComplete` | Verfolgen Sie den Abschluss von Medien. Rufen Sie diese Methode nur auf, wenn die Medien vollständig angezeigt wurden. | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | Verfolgen Sie das Ende einer Anzeigesitzung. Rufen Sie diese Methode auch dann auf, wenn der Benutzer das Medium nicht bis zum Abschluss anzeigt. | `trackerInstance.trackSessionEnd()` |
| `trackError` | Verfolgen Sie einen Fehler, der während der Medienwiedergabe aufgetreten ist. | `trackerInstance.trackError("errorId")` |
| `trackEvent` | Verfolgen eines benutzerdefinierten Ereignisses. | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | Aktualisieren Sie die Abspielposition. | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | Aktualisieren Sie die Erlebnisqualität. | `trackerInstance.updateQoEObject(qoe)` |

## Konstanten

| Konstantenname | Beschreibung | Wert |
|-----------------|--|-----------------|
| `MediaType` | Medientyp | `Video`, `Audio` |
| `StreamType` | Stream-Typ | `VOD`, `Live`, `Linear`, `Podcast`, `Audiobook`, `AOD` |
| `VideoMetadataKeys` | Dadurch werden die Standard-Metadatenschlüssel für Video-Streams definiert | `Show`, `Season`, `Episode`, `AssetId`, `Genre`, `FirstAirDate`, `FirstDigitalDate`, `Rating`, `Originator`, `Network`, `ShowType`, `AdLoad`, `MVPD`, `Authorized`, `DayPart`, `Feed`, `StreamFormat` |
| `AudioMetadataKeys` | Dadurch werden die Standard-Metadatenschlüssel für Audio-Streams definiert. | `Artist`, `Album`, `Label`, `Author`, `Station`, `Publisher` |
| `AdMetadataKeys` | Dadurch werden die Standard-Metadatenschlüssel für Anzeigen definiert. | `Advertiser`, `CampaignId`, `CreativeId`, `PlacementId`, `SiteId`, `CreativeUrl` |
| `Event` | Dies definiert den Typ eines Tracking-Ereignisses. | `AdBreakStart`, `AdBreakComplete`, `AdStart`, `AdComplete`, `AdSkip`, `ChapterStart`, `ChapterComplete`, `ChapterSkip`, `SeekStart`, `SeekComplete`, `BufferStart`, `BufferComplete`, `BitrateChange`, `StateStart`, `StateEnd` |
| `PlayerState` | Dadurch werden Standardwerte für das Tracking des Player-Status definiert. | `FullScreen`, `ClosedCaption`, `Mute`, `PictureInPicture`, `InFocus` |
