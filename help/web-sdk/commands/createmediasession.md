---
title: createMediaSession
description: Erfahren Sie, wie Sie das Web SDK so konfigurieren, dass Mediensitzungen automatisch verwaltet werden
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---


# `createMediaSession`

Die `createMediaSession` -Befehl ist Teil des Web SDK `streamingMedia` -Komponente. Sie können diese Komponente verwenden, um Daten zu Mediensitzungen auf Ihrer Website zu erfassen. Siehe `streamingMedia` [Dokumentation](configure/streamingmedia.md) , um zu erfahren, wie Sie diese Komponente konfigurieren.

Die erfassten Daten können Informationen zu Medienwiedergaben, Pausen, Beendigungen und anderen damit zusammenhängenden Ereignissen enthalten. Nach der Erfassung können Sie diese Daten an senden [Adobe Analytics für Streaming-Medien](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview), um Metriken zu aggregieren. Diese Funktion bietet eine umfassende Lösung zum Verfolgen und Verstehen des Verhaltens der Mediennutzung auf Ihrer Website.

Sie können Mediensitzungen im Web SDK auf zwei Arten erstellen:

* [Automatisch verfolgte Mediensitzungen](#automatic) dem Web SDK erlauben, den Versand von Medien-Ping-Ereignissen an [Adobe Analytics für Streaming-Medien](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview). Die Häufigkeit dieser Pings wird durch die Konfigurationseinstellungen der Variablen [streamingMedia](configure/streamingmedia.md) -Komponente.
* [Manuell verfolgte Mediensitzungen](#manual) mehr Kontrolle über den Versand von Sitzungs-Ping-Ereignissen an [Adobe Analytics für Streaming-Medien](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview). Darüber hinaus können Sie die `sessionID` für Mediensitzungen.

## Erstellen einer automatisch verfolgten Mediensitzung {#automatic}

Um das automatische Tracking einer Mediensitzung zu starten, rufen Sie die `createMediaSession` -Methode mit den unten beschriebenen Optionen verwenden:

```javascript
    alloy("createMediaSession", {
        playerId: "movie-test",
        getPlayerDetails: () => {
            return {
                playhead: document.getElementById("movie-test").currentTime,
                qoeDataDetails: {
                    bitrate: 1000,
                    startupTime: 1000,
                    fps: 30,
                    droppedFrames: 10
                }
            };
        },
        xdm: {
            eventType: "media.sessionStart",
            mediaCollection: {
                sessionDetails: {
                    ...
                }
            }
        }
    });
```

| Eigenschaft | Typ | Erforderlich | Beschreibung |
|---------|----------|---------|---------|
| `playerId` | Zeichenfolge | Ja | Die Player-ID, eine eindeutige ID, die die Mediensitzung darstellt. |
| `getPlayerDetails` | Funktion | Ja | Eine Funktion, die die Player-Details zurückgibt. Diese Rückruffunktion wird vom Web SDK vor jedem Medienereignis für die `playerId` bereitgestellt. |
| `xdm.eventType ` | Objekt | Nein | Der Medien-Ereignistyp. Wenn dies nicht angegeben wird, wird dies automatisch auf `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Das Sitzungsdetailobjekt. Die `sessionDetails` -Objekt sollte die Eigenschaften der Sitzungsdetails enthalten. Siehe [Mediensammlungsschema](../../xdm/data-types/media-collection-details.md) Dokumentation finden Sie weitere Informationen. |


## Erstellen einer manuell verfolgten Mediensitzung {#manual}

Um das manuelle Tracking einer Mediensitzung zu starten, rufen Sie die `createMediaSession` -Methode mit den unten beschriebenen Optionen verwenden:

```javascript
const sessionPromise = alloy("createMediaSession", {
    xdm: {
        eventType: "media.sessionStart",
        mediaCollection: {
            playhead: 0,
            sessionDetails: {
                ...
            },
            qoeDataDetails: {
                bitrate: 1000,
                startupTime: 1000,
                fps: 30,
                droppedFrames: 10
            }
        }
    }
});
```

| Eigenschaft | Typ | Erfordert | Beschreibung |
|---------|----------|---------|---------|
| `xdm.eventType` | Objekt | Nein | Der Medien-Ereignistyp. Wenn nicht angegeben, wird automatisch auf `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Das Sitzungsdetailobjekt. Die `sessionDetails` -Objekt sollte die Eigenschaften der Sitzungsdetails enthalten. Siehe [Mediensammlungsschema](../../xdm/data-types/media-collection-details.md) Dokumentation finden Sie weitere Informationen. |
| `xdm.mediaCollection.playhead` | Ganzzahl | Ja | Die aktuelle Abspielleiste. |
| `xdm.mediaCollection.qoeDataDetails` | Objekt | Nein | Die Qualität der Erlebnisdatendetails. Siehe [Mediensammlungsschema](../../xdm/data-types/media-collection-details.md) Dokumentation finden Sie weitere Informationen. |
