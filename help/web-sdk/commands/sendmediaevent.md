---
title: sendMediaEvent
description: Erfahren Sie, wie Sie mit dem Befehl sendMediaEvent Mediensitzungen im Web SDK verfolgen können.
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# `sendMediaEvent`

Die `sendMediaEvent` -Befehl ist Teil des Web SDK `streamingMedia` -Komponente. Sie können diese Komponente verwenden, um Daten zu Mediensitzungen auf Ihrer Website zu erfassen. Siehe `streamingMedia` [Dokumentation](configure/streamingmedia.md) , um zu erfahren, wie Sie diese Komponente konfigurieren.

Verwenden Sie die `sendMediaEvent` -Befehl zum Verfolgen von Medienwiedergaben, Pausen, Beendigungen, Player-Statusaktualisierungen und anderen damit zusammenhängenden Ereignissen.

Web SDK kann Medienereignisse basierend auf dem Typ des Medien-Sitzungs-Tracking verarbeiten:

* **Ereignisverarbeitung für automatisch verfolgte Sitzungen**. In diesem Modus müssen Sie die Variable `sessionID` zum Medienereignis oder zum Abspielleistenwert. Das Web SDK verarbeitet dies für Sie basierend auf der angegebenen Player-ID und der `getPlayerDetails` Callback-Funktion, die beim Starten der Mediensitzung bereitgestellt wird.
* **Ereignisverarbeitung für manuell verfolgte Sitzungen**. In diesem Modus müssen Sie die `sessionID` zum Medienereignis zusammen mit dem Wert der Abspielleiste (Ganzzahlwert). Bei Bedarf können Sie auch die Details zur Erlebnisqualität übermitteln.

## Umgang mit Medienereignissen nach Typ {#handle-by-type}

Wählen Sie die folgenden Registerkarten aus, um Beispiele für die Handhabung von Ereignistypen für jeden Ereignistyp und für die Tracking-Methode von Sitzungen zu erhalten (automatisch oder manuell).


### Play {#play}

Die `media.play` Ereignistyp wird verwendet, um zu verfolgen, wann die Medienwiedergabe beginnt. Dieses Ereignis sollte gesendet werden, wenn der Player den Status von einem anderen Status zu &quot;Playing&quot;(Wiedergabe) ändert. Andere Status, von denen der Player zu &quot;Playing&quot;(Wiedergabe) wechselt, umfassen &quot;Buffering&quot;(Puffern), den Fortsetzen der Wiedergabe von &quot;Paused&quot;(Pause), den Player, der sich von einem Fehler erholt, oder die automatische Wiedergabe.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB Manuelle Sitzungsverfolgung]

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


### Anhalten {#pause}

Die `media.pauseStart` Ereignistyp wird verwendet, um zu verfolgen, wann eine Medienwiedergabe angehalten wird. Dieses Ereignis sollte gesendet werden, wenn der Benutzer die **[!UICONTROL Anhalten]**. Es gibt keinen Ereignistyp Fortsetzen . Beim Senden einer `media.play` -Ereignis nach einer `media.pauseStart`.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB Manuelle Sitzungsverfolgung]

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

Die `media.error` Ereignistyp wird verwendet, um zu verfolgen, wann während der Medienwiedergabe ein Fehler auftritt. Dieses Ereignis sollte gesendet werden, wenn ein Fehler auftritt.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

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

>[!TAB Manuelle Sitzungsverfolgung]

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

Die `media.adBreakStart` Ereignistyp wird verwendet, um zu verfolgen, wann eine Werbeunterbrechung beginnt. Dieses Ereignis sollte gesendet werden, wenn eine Werbeunterbrechung beginnt.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

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

>[!TAB Manuelle Sitzungsverfolgung]

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


### Abschluss der Werbeunterbrechung {#ad-break-complete}

Die `media.adBreakComplete` Ereignistyp wird verwendet, um zu verfolgen, wann eine Werbeunterbrechung abgeschlossen ist. Dieses Ereignis sollte nach Abschluss einer Werbeunterbrechung gesendet werden.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB Manuelle Sitzungsverfolgung]

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

Die `media.adStart` Ereignistyp wird verwendet, um zu verfolgen, wann eine Anzeige beginnt. Dieses Ereignis sollte beim Start einer Anzeige gesendet werden.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

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

>[!TAB Manuelle Sitzungsverfolgung]

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


### Abschluss der Anzeige {#ad-complete}

Die `media.adComplete` Ereignistyp wird verwendet, um zu verfolgen, wann eine Anzeige abgeschlossen ist. Dieses Ereignis sollte gesendet werden, wenn eine Anzeige abgeschlossen ist.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB Manuelle Sitzungsverfolgung]

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

Die `media.adSkip` Ereignistyp wird verwendet, um zu verfolgen, wann eine Anzeige übersprungen wird. Dieses Ereignis sollte gesendet werden, wenn eine Anzeige übersprungen wird.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB Manuelle Sitzungsverfolgung]

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

Die `media.chapterStart` Ereignistyp wird verwendet, um zu verfolgen, wann ein Kapitel beginnt. Dieses Ereignis sollte beim Start eines Kapitels gesendet werden.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

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

>[!TAB Manuelle Sitzungsverfolgung]

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


### Kapitelbeendigung {#chapter-complete}

Die `media.chapterComplete` Ereignistyp wird verwendet, um zu verfolgen, wann ein Kapitel abgeschlossen ist. Dieses Ereignis sollte nach Abschluss eines Kapitels gesendet werden.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB Manuelle Sitzungsverfolgung]

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


### Überspringen eines Kapitels {#chapter-skip}

Die `media.chapterSkip` Ereignistyp wird verwendet, um zu verfolgen, wann ein Kapitel übersprungen wird. Dieses Ereignis sollte gesendet werden, wenn ein Kapitel übersprungen wird.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB Manuelle Sitzungsverfolgung]

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


### Pufferstart {#buffer-start}

Die `media.bufferStart` Ereignistyp wird verwendet, um zu verfolgen, wann die Pufferung beginnt. Dieses Ereignis sollte beim Start der Pufferung gesendet werden. Es gibt keine `bufferResume` Ereignistyp. A `bufferResume` wird erkannt, wenn Sie ein Wiedergabeereignis senden, nachdem `bufferStart`.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB Manuelle Sitzungsverfolgung]

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

Die `media.bitrateChange` Ereignistyp wird verwendet, um zu verfolgen, wann sich die Bitrate ändert. Dieses Ereignis sollte gesendet werden, wenn sich die Bitrate ändert.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

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

>[!TAB Manuelle Sitzungsverfolgung]

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

Die `media.stateUpdate` Ereignistyp wird verwendet, um zu verfolgen, wann sich der Player-Status ändert. Dieses Ereignis sollte gesendet werden, wenn sich der Player-Status ändert.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.stateUpdate",
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

>[!TAB Manuelle Sitzungsverfolgung]

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

Die `media.sessionEnd` Ereignistyp wird verwendet, um das Media Analytics-Backend darauf hinzuweisen, die Sitzung sofort zu schließen, wenn der Benutzer die Anzeige des Inhalts abgebrochen hat und wahrscheinlich nicht zurückkehren wird.

Wenn Sie keine `sessionEnd` -Ereignis, wird eine abgebrochene Sitzung beendet, nachdem 10 Minuten lang keine Ereignisse empfangen wurden oder 30 Minuten lang keine Verschiebung der Abspielleiste stattgefunden hat. Die Sitzung wird automatisch gelöscht.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB Manuelle Sitzungsverfolgung]

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


### Sitzungsende {#session-complete}

Die `media.sessionComplete` Ereignistyp wird verwendet, um zu verfolgen, wann eine Mediensitzung abgeschlossen ist. Dieses Ereignis sollte gesendet werden, wenn das Ende des Hauptinhalts erreicht ist.

>[!BEGINTABS]

>[!TAB Automatische Sitzungsverfolgung]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB Manuelle Sitzungsverfolgung]

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



