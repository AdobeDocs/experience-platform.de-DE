---
title: createMediaSession
description: Erfahren Sie, wie Sie das Web SDK so konfigurieren, dass Mediensitzungen automatisch verwaltet werden
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---

# `createMediaSession`

Der Befehl `createMediaSession` ist Teil der Komponente Web SDK `streamingMedia` . Sie können diese Komponente verwenden, um Daten zu Mediensitzungen auf Ihrer Website zu erfassen. Informationen zum Konfigurieren dieser Komponente finden Sie in der Dokumentation zu `streamingMedia` [Dokumentation](configure/streamingmedia.md) .

Die erfassten Daten können Informationen zu Medienwiedergaben, Pausen, Beendigungen und anderen damit zusammenhängenden Ereignissen enthalten. Nach der Erfassung können Sie diese Daten an [Adobe Analytics für Streaming-Medien](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview) senden, um Metriken zu aggregieren. Diese Funktion bietet eine umfassende Lösung zum Verfolgen und Verstehen des Verhaltens der Mediennutzung auf Ihrer Website.

Sie können Mediensitzungen im Web SDK auf zwei Arten erstellen:

* [Automatisch verfolgte Mediensitzungen](#automatic) ermöglichen es dem Web SDK, den Versand von Medien-Ping-Ereignissen an [Adobe Analytics für Streaming-Medien](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview) zu verwalten. Die Häufigkeit dieser Pings wird durch die Konfigurationseinstellungen der Komponente [streamingMedia](configure/streamingmedia.md) bestimmt.
* [Manuell verfolgte Mediensitzungen](#manual) geben Ihnen mehr Kontrolle über den Versand von Sitzungs-Ping-Ereignissen an [Adobe Analytics für Streaming-Medien](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview). Außerdem können Sie die `sessionID` für Mediensitzungen speichern.

## Erstellen einer automatisch verfolgten Mediensitzung {#automatic}

Um das automatische Tracking einer Mediensitzung zu starten, rufen Sie die Methode `createMediaSession` mit den unten beschriebenen Optionen auf:

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
| `getPlayerDetails` | Funktion | Ja | Eine Funktion, die die Player-Details zurückgibt. Diese Rückruffunktion wird vom Web SDK vor jedem Medienereignis für die bereitgestellte `playerId` aufgerufen. |
| `xdm.eventType ` | Objekt | Nein | Der Medien-Ereignistyp. Wenn dies nicht angegeben wird, wird dies automatisch auf `media.sessionStart` gesetzt. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Das Sitzungsdetailobjekt. Das Objekt `sessionDetails` sollte die Eigenschaften der Sitzungsdetails enthalten. Weitere Informationen finden Sie in der Dokumentation zum [Mediensammlungsschema](../../xdm/data-types/media-collection-details.md) . |


## Erstellen einer manuell verfolgten Mediensitzung {#manual}

Um das manuelle Tracking einer Mediensitzung zu starten, rufen Sie die Methode `createMediaSession` mit den unten beschriebenen Optionen auf:

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
| `xdm.eventType` | Objekt | Nein | Der Medien-Ereignistyp. Wenn nicht angegeben, wird er automatisch auf `media.sessionStart` gesetzt. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Das Sitzungsdetailobjekt. Das Objekt `sessionDetails` sollte die Eigenschaften der Sitzungsdetails enthalten. Weitere Informationen finden Sie in der Dokumentation zum [Mediensammlungsschema](../../xdm/data-types/media-collection-details.md) . |
| `xdm.mediaCollection.playhead` | Ganzzahl | Ja | Die aktuelle Abspielleiste. |
| `xdm.mediaCollection.qoeDataDetails` | Objekt | Nein | Die Qualität der Erlebnisdatendetails. Weitere Informationen finden Sie in der Dokumentation zum [Mediensammlungsschema](../../xdm/data-types/media-collection-details.md) . |
