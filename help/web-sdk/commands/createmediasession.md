---
title: createMediaSession
description: Erfahren Sie, wie Sie Web SDK so konfigurieren, dass Mediensitzungen automatisch verwaltet werden
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---

# `createMediaSession`

Der Befehl `createMediaSession` ist Teil der Web SDK-`streamingMedia`. Sie können diese Komponente verwenden, um Daten zu Mediensitzungen auf Ihrer Website zu erfassen. Informationen zum Konfigurieren dieser Komponente finden [ in der `streamingMedia` ](configure/streamingmedia.md)Dokumentation).

Die erfassten Daten können Informationen zu Medienwiedergaben, Pausen, Beendigungen und anderen zugehörigen Ereignissen enthalten. Nach der Erfassung können Sie diese Daten an [Adobe Analytics für Streaming-Medien](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview) senden, um Metriken zu aggregieren. Diese Funktion bietet eine umfassende Lösung zum Tracking und zum Verständnis des Medienkonsumverhaltens auf Ihrer Website.

Sie können Mediensitzungen in Web SDK auf zwei Arten erstellen:

* [Automatisch verfolgte Mediensitzungen](#automatic) ermöglichen es der Web-SDK, den Versand von Medien-Ping-Ereignissen an [Adobe Analytics für Streaming-Medien zu ](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview). Die Häufigkeit dieser Pings wird durch die Konfigurationseinstellungen der Komponente [StreamingMedia](configure/streamingmedia.md) bestimmt.
* [Manuell verfolgte Mediensitzungen](#manual) ermöglichen Ihnen mehr Kontrolle über den Versand von Sitzungs-Ping-Ereignissen an [Adobe Analytics für Streaming-Medien](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview). Darüber hinaus haben Sie die Möglichkeit, die `sessionID` für Mediensitzungen zu speichern.

## Erstellen einer automatisch verfolgten Mediensitzung {#automatic}

Um das automatische Tracking einer Mediensitzung zu starten, rufen Sie die `createMediaSession`-Methode mit den unten beschriebenen Optionen auf:

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
| `playerId` | Zeichenfolge | Ja | Die Player-ID, eine eindeutige Kennung, die die Mediensitzung darstellt. |
| `getPlayerDetails` | Funktion | Ja | Eine Funktion, die die Player-Details zurückgibt. Diese Rückruffunktion wird von der Web-SDK vor jedem Medienereignis für die angegebene `playerId` aufgerufen. |
| `xdm.eventType ` | Objekt | Nein | Der Medienereignistyp. Wenn dies nicht angegeben wird, wird dies automatisch auf `media.sessionStart` gesetzt. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Das Sitzungsdetailobjekt. Das `sessionDetails`-Objekt sollte die Eigenschaften der Sitzungsdetails enthalten. Weitere Informationen finden [ in der Dokumentation ](../../xdm/data-types/media-collection-details.md)Mediensammlungsschema“. |


## Erstellen einer manuell verfolgten Mediensitzung {#manual}

Um das Tracking einer Mediensitzung manuell zu starten, rufen Sie die `createMediaSession`-Methode mit den unten beschriebenen Optionen auf:

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

| Eigenschaft | Typ | Erforderlich | Beschreibung |
|---------|----------|---------|---------|
| `xdm.eventType` | Objekt | Nein | Der Medienereignistyp. Wenn er nicht angegeben wird, wird er automatisch auf `media.sessionStart` gesetzt. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Das Sitzungsdetailobjekt. Das `sessionDetails`-Objekt sollte die Eigenschaften der Sitzungsdetails enthalten. Weitere Informationen finden [ in der Dokumentation ](../../xdm/data-types/media-collection-details.md)Mediensammlungsschema“. |
| `xdm.mediaCollection.playhead` | Ganzzahl | Ja | Der aktuelle Abspielkopf. |
| `xdm.mediaCollection.qoeDataDetails` | Objekt | Nein | Details zur Qualität der Erlebnisdaten. Weitere Informationen finden [ in der Dokumentation ](../../xdm/data-types/media-collection-details.md)Mediensammlungsschema“. |
