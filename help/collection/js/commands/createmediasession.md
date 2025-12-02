---
title: createMediaSession
description: Erfahren Sie, wie Sie Web SDK so konfigurieren, dass Mediensitzungen automatisch verwaltet werden
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 7%

---

# `createMediaSession`

Der Befehl `createMediaSession` ist Teil der Web SDK-`streamingMedia`. Sie können diese Komponente verwenden, um Daten zu Mediensitzungen auf Ihrer Website zu erfassen. Informationen zum Konfigurieren dieser Komponente finden `streamingMedia` in der [&#x200B; &#x200B;](configure/streamingmedia.md)Dokumentation).

Die erfassten Daten können Informationen zu Medienwiedergaben, Pausen, Beendigungen und anderen zugehörigen Ereignissen enthalten. Nach der Erfassung können Sie diese Daten zur Aggregation von Metriken an [Adobe Analytics for Streaming Media](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview) senden. Diese Funktion bietet eine umfassende Lösung zum Tracking und zum Verständnis des Medienkonsumverhaltens auf Ihrer Website.

Sie können Mediensitzungen in Web SDK auf zwei Arten erstellen:

* **Automatisch verfolgte Mediensitzungen** ermöglichen es der Web-SDK, den Versand von Medien-Ping-Ereignissen an (Adobe [&#x200B; für Streaming-Medien) &#x200B;](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview) verwalten. Die Häufigkeit dieser Pings wird durch die Konfigurationseinstellungen der Komponente [StreamingMedia](configure/streamingmedia.md) bestimmt.
* **Manuell verfolgte Mediensitzungen** ermöglichen Ihnen mehr Kontrolle über den Versand von Sitzungs-Ping-Ereignissen an [Adobe Analytics für Streaming-Medien](https://experienceleague.adobe.com/de/docs/media-analytics/using/media-overview). Darüber hinaus haben Sie die Möglichkeit, die `sessionID` für Mediensitzungen zu speichern.

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
| `xdm.eventType` | Objekt | Nein | Der Medienereignistyp. Wenn dieses Feld nicht angegeben wird, wird es automatisch auf `media.sessionStart` gesetzt. |
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Enthält Sitzungsdetaileigenschaften. Weitere Informationen finden [&#x200B; unter &#x200B;](/help/xdm/data-types/media-collection-details.md)Mediensammlungsschema“. |

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
| `xdm.mediaCollection.sessionDetails` | Objekt | Ja | Enthält Sitzungsdetaileigenschaften. Weitere Informationen finden [&#x200B; unter &#x200B;](/help/xdm/data-types/media-collection-details.md)Mediensammlungsschema“. |
| `xdm.mediaCollection.playhead` | Ganzzahl | Ja | Der aktuelle Abspielkopf. |
| `xdm.mediaCollection.qoeDataDetails` | Objekt | Nein | Details zur Qualität der Erlebnisdaten. Weitere Informationen finden [&#x200B; in der Dokumentation &#x200B;](/help/xdm/data-types/media-collection-details.md)Mediensammlungsschema“. |

## Erstellen einer Mediensitzung mit der Tag-Erweiterung „Web SDK&quot;

Die diesem Befehl entsprechende Web SDK-Tag-Erweiterung ist der [**[!UICONTROL Session start]**](/help/tags/extensions/client/web-sdk/actions/send-media-event.md#session-start) Ereignistyp innerhalb der Aktion &quot;[!UICONTROL Send media event]&quot;.
