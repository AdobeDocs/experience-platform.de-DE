---
title: sendMediaEvent
description: Erfahren Sie, wie Sie mit dem Befehl sendMediaEvent Mediensitzungen in Web SDK verfolgen können.
exl-id: a38626fd-4810-40a0-8893-e98136634fac
source-git-commit: 877e12f1d53bb4a8d7c2564490d4e8f3e9e34e34
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# `sendMediaEvent`

Der Befehl `sendMediaEvent` ist Teil der Web SDK-`streamingMedia`. Sie können diese Komponente verwenden, um Daten zu Mediensitzungen auf Ihrer Website zu erfassen. Informationen zum Konfigurieren dieser Komponente finden [ in der `streamingMedia` ](configure/streamingmedia.md)Dokumentation).

Verwenden Sie den `sendMediaEvent`-Befehl, um Medienwiedergaben, Pausen, Abschlüsse, Aktualisierungen des Player-Status und andere zugehörige Ereignisse zu verfolgen.

Web SDK kann Medienereignisse je nach Typ des Medien-Sitzungs-Trackings verarbeiten:

* **Ereignisverarbeitung für automatisch verfolgte Sitzungen**. In diesem Modus müssen Sie die `sessionID` nicht an das Medienereignis oder den Abspielkopfwert übergeben. Die Web-SDK übernimmt dies für Sie basierend auf der angegebenen Player-ID und der `getPlayerDetails` Rückruffunktion, die beim Starten der Mediensitzung bereitgestellt wurde.
* **Ereignisverarbeitung für manuell verfolgte Sitzungen**. In diesem Modus müssen Sie die `sessionID` zusammen mit dem Abspielkopfwert (ganzzahliger Wert) an das Medienereignis übergeben. Bei Bedarf können Sie auch Details zur Erlebnisqualität weitergeben.

## Verarbeiten von Medienereignissen nach Typ {#handle-by-type}

Wählen Sie die folgenden Registerkarten aus, um Beispiele für die Verarbeitung von Ereignistypen für jeden Ereignistyp und jede Sitzungsverfolgungsmethode anzuzeigen (automatisch oder manuell).


### Play {#play}

Der `media.play` Ereignistyp wird verwendet, um zu verfolgen, wann die Medienwiedergabe beginnt. Dieses Ereignis sollte gesendet werden, wenn der Player von einem anderen Status aus den Status „Playing“ (Wiedergabe) wechselt. Andere Zustände, von denen der Player zu „Playing“ (Wiedergabe) wechselt, sind „Buffering“ (Pufferung), die Wiederaufnahme von „Paused“ (angehalten), die Wiederherstellung des Players nach einem Fehler oder die automatische Wiedergabe.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.play",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Aussetzen {#pause}

Der `media.pauseStart` Ereignistyp wird verwendet, um zu verfolgen, wann eine Medienwiedergabe angehalten wurde. Dieses Ereignis sollte gesendet werden, wenn der Benutzer auf &quot;**[!UICONTROL &quot;]**. Es gibt keinen Resume-Ereignistyp. Ein Lebenslauf wird abgeleitet, wenn Sie nach einem `media.pauseStart` ein `media.play` senden.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.pauseStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Fehler {#error}

Der `media.error`-Ereignistyp wird verwendet, um zu verfolgen, wann während der Medienwiedergabe ein Fehler auftritt. Dieses Ereignis sollte bei einem Fehler gesendet werden.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.error",
        mediaCollection: {
            errorDetails: {
                name: "network-error",
                source: "player"
            }
        }
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.error",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                errorDetails: {
                    name: "network-error",
                    source: "player"
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Start der Werbeunterbrechung {#ad-break-start}

Der `media.adBreakStart` Ereignistyp wird verwendet, um den Beginn einer Werbeunterbrechung zu verfolgen. Dieses Ereignis sollte gesendet werden, wenn eine Werbeunterbrechung beginnt.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakStart",
        mediaCollection: {
            advertisingPodDetails: {
                friendlyName: "Mid-roll",
                offset: 0,
                index: 1
            }
        }
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                advertisingPodDetails: {
                    friendlyName: "Mid-roll",
                    offset: 0,
                    index: 1
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Werbeunterbrechung abgeschlossen {#ad-break-complete}

Der `media.adBreakComplete` Ereignistyp wird verwendet, um zu verfolgen, wann eine Werbeunterbrechung abgeschlossen ist. Dieses Ereignis sollte gesendet werden, wenn eine Werbeunterbrechung abgeschlossen ist.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Anzeigenstart {#ad-start}

Der `media.adStart` Ereignistyp wird verwendet, um den Beginn einer Anzeige zu verfolgen. Dieses Ereignis sollte beim Start einer Anzeige gesendet werden.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            advertisingDetails: {
                friendlyName: "Ad 1",
                name: "/uri-reference/001",
                length: 10,
                advertiser: "Adobe Marketing",
                campaignID: "Adobe Analytics",
                creativeID: "creativeID",
                creativeURL: "https://creativeurl.com",
                placementID: "placementID",
                siteID: "siteID",
                podPosition: 11,
                playerName: "HTML5 player"
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
            sessionID,
            advertisingDetails: {
              friendlyName: "Ad 1",
              name: "/uri-reference/001",
              length: 10,
              advertiser: "Adobe Marketing",
              campaignID: "Adobe Analytics",
              creativeID: "creativeID",
              creativeURL: "https://creativeurl.com",
              placementID: "placementID",
              siteID: "siteID",
              podPosition: 11,
              playerName: "HTML5 player"
            },
            customMetadata: [
              {
                name: "myCustomValue3",
                value: "c3"
              },
              {
                name: "myCustomValue2",
                value: "c2"
              },
              {
                name: "myCustomValue1",
                value: "c1"
              }]
        }
        }
    });
});
```

>[!ENDTABS]


### Hinzufügen abgeschlossen {#ad-complete}

Der `media.adComplete` Ereignistyp wird verwendet, um zu verfolgen, wann eine Anzeige abgeschlossen ist. Dieses Ereignis sollte gesendet werden, wenn eine Anzeige abgeschlossen ist.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Überspringen einer Anzeige {#ad-skip}

Der `media.adSkip` Ereignistyp wird verwendet, um zu verfolgen, wann eine Anzeige übersprungen wird. Dieses Ereignis sollte gesendet werden, wenn eine Anzeige übersprungen wird.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Kapitelstart {#chapter-start}

Der `media.chapterStart` Ereignistyp wird verwendet, um den Beginn eines Kapitels zu verfolgen. Dieses Ereignis sollte gesendet werden, wenn ein Kapitel beginnt.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterStart",
        mediaCollection: {
            chapterDetails: {
                friendlyName: "Chapter 1",
                position: 1,
                length: 10,
                index: 1,
                offset: 0
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                chapterDetails: {
                    friendlyName: "Chapter 1",
                    position: 1,
                    length: 10,
                    index: 1,
                    offset: 0
                },
                customMetadata: [{
                        name: "myCustomValue3",
                        value: "c3"
                    },
                    {
                        name: "myCustomValue2",
                        value: "c2"
                    },
                    {
                        name: "myCustomValue1",
                        value: "c1"
                    }
                ]
            }
        }
    });
});
```

>[!ENDTABS]


### Kapitel abgeschlossen {#chapter-complete}

Der `media.chapterComplete` Ereignistyp wird verwendet, um zu verfolgen, wann ein Kapitel abgeschlossen ist. Dieses Ereignis sollte gesendet werden, wenn ein Kapitel abgeschlossen ist.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Kapitelübersprung {#chapter-skip}

Der `media.chapterSkip` Ereignistyp wird verwendet, um zu verfolgen, wann ein Kapitel übersprungen wird. Dieses Ereignis sollte gesendet werden, wenn ein Kapitel übersprungen wird.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Start der Pufferung {#buffer-start}

Der `media.bufferStart` Ereignistyp wird verwendet, um zu verfolgen, wann die Pufferung beginnt. Dieses Ereignis sollte beim Start der Pufferung gesendet werden. Es gibt keinen `bufferResume` Ereignistyp. Ein `bufferResume` wird abgeleitet, wenn Sie nach dem `bufferStart` ein Wiedergabeereignis senden.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bufferStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Bitratenänderung {#bitrate-change}

Der `media.bitrateChange` Ereignistyp wird verwendet, um zu verfolgen, wann sich die Bitrate ändert. Dieses Ereignis sollte gesendet werden, wenn sich die Bitrate ändert.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bitrateChange",
        mediaCollection: {
            qoeDataDetails: {
                framesPerSecond: 1,
                bitrate: 35000,
                droppedFrames: 30,
                timeToStart: 1364
            }
        }
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bitrateChange",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                qoeDataDetails: {
                    bitrate: 35000,
                    droppedFrames: 30,
                    timeToStart: 1364
                }
            }
        }
    });
});
```

>[!ENDTABS]


### Statusaktualisierungen {#state-updates}

Der `media.statesUpdate` Ereignistyp wird verwendet, um zu verfolgen, wann sich der Player-Status ändert. Dieses Ereignis sollte gesendet werden, wenn sich der Player-Status ändert.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.statesUpdate",
        mediaCollection: {
            statesStart: [{
                    name: "mute"
                },
                {
                    name: "pictureInPicture"
                }
            ],
            statesEnd: [{
                name: "fullScreen"
            }]
        }
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.stateUpdate",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                statesStart: [{
                        name: "mute"
                    },
                    {
                        name: "pictureInPicture"
                    }
                ],
                statesEnd: [{
                    name: "fullScreen"
                }]
            }
        }
    });
});
```

>[!ENDTABS]


### Sitzungsende {#session-end}

Der Ereignistyp `media.sessionEnd` wird verwendet, um das Media Analytics-Backend zu benachrichtigen, dass die Sitzung sofort geschlossen wird, wenn der Benutzer die Anzeige des Inhalts verlassen hat und er wahrscheinlich nicht mehr zurückkehren wird.

Wenn Sie kein `sessionEnd` senden, wird eine abgebrochene Sitzung beendet, wenn für 10 Minuten keine Ereignisse empfangen werden oder wenn für 30 Minuten keine Abspielkopfbewegung stattfindet. Die Sitzung wird automatisch gelöscht.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionEnd",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]


### Sitzung abgeschlossen {#session-complete}

Der `media.sessionComplete` Ereignistyp wird verwendet, um den Abschluss einer Mediensitzung zu verfolgen. Dieses Ereignis sollte gesendet werden, wenn das Ende des Hauptinhalts erreicht ist.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB Manuelles Sitzungs-Tracking]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]
