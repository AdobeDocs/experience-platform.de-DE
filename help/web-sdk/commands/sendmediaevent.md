---
title: sendMediaEvent
description: Erfahren Sie, wie Sie mit dem Befehl sendMediaEvent Mediensitzungen im Web SDK verfolgen können.
exl-id: a38626fd-4810-40a0-8893-e98136634fac
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# `sendMediaEvent`

Der Befehl `sendMediaEvent` ist Teil der Komponente Web SDK `streamingMedia` . Sie können diese Komponente verwenden, um Daten zu Mediensitzungen auf Ihrer Website zu erfassen. Informationen zum Konfigurieren dieser Komponente finden Sie in der Dokumentation zu `streamingMedia` [Dokumentation](configure/streamingmedia.md) .

Verwenden Sie den Befehl `sendMediaEvent` , um Medienwiedergaben, Pausen, Beendigungen, Player-Statusaktualisierungen und andere zugehörige Ereignisse zu verfolgen.

Web SDK kann Medienereignisse basierend auf dem Typ des Medien-Sitzungs-Tracking verarbeiten:

* **Ereignisbehandlung für automatisch verfolgte Sitzungen**. In diesem Modus müssen Sie die `sessionID` nicht an das Medienereignis oder den Abspielleistenwert übergeben. Das Web SDK verarbeitet dies für Sie basierend auf der angegebenen Player-ID und der beim Starten der Mediensitzung bereitgestellten Rückruffunktion `getPlayerDetails` .
* **Ereignisbehandlung für manuell verfolgte Sitzungen**. In diesem Modus müssen Sie die `sessionID` zusammen mit dem Wert der Abspielleiste (Ganzzahlwert) an das Medienereignis übergeben. Bei Bedarf können Sie auch die Details zur Erlebnisqualität übermitteln.

## Umgang mit Medienereignissen nach Typ {#handle-by-type}

Wählen Sie die folgenden Registerkarten aus, um Beispiele für die Handhabung von Ereignistypen für jeden Ereignistyp und für die Tracking-Methode von Sitzungen zu erhalten (automatisch oder manuell).


### Play {#play}

Der Ereignistyp `media.play` wird verwendet, um zu verfolgen, wann die Medienwiedergabe beginnt. Dieses Ereignis sollte gesendet werden, wenn der Player den Status von einem anderen Status zu &quot;Playing&quot;(Wiedergabe) ändert. Andere Status, von denen der Player zu &quot;Playing&quot;(Wiedergabe) wechselt, umfassen &quot;Buffering&quot;(Puffern), den Fortsetzen der Wiedergabe von &quot;Paused&quot;(Pause), den Player, der sich von einem Fehler erholt, oder die automatische Wiedergabe.

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

Der Ereignistyp `media.pauseStart` wird verwendet, um zu verfolgen, wann eine Medienwiedergabe angehalten wird. Dieses Ereignis sollte gesendet werden, wenn der Benutzer die Taste **[!UICONTROL Pause]** drückt. Es gibt keinen Ereignistyp Fortsetzen . Eine Wiederaufnahme wird erkannt, wenn Sie ein `media.play` -Ereignis nach einer `media.pauseStart` senden.

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

Der Ereignistyp `media.error` wird verwendet, um zu verfolgen, wann während der Medienwiedergabe ein Fehler auftritt. Dieses Ereignis sollte gesendet werden, wenn ein Fehler auftritt.

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

Der Ereignistyp `media.adBreakStart` wird verwendet, um zu verfolgen, wann eine Werbeunterbrechung beginnt. Dieses Ereignis sollte gesendet werden, wenn eine Werbeunterbrechung beginnt.

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


### Abschluss der Werbeunterbrechung {#ad-break-complete}

Der Ereignistyp `media.adBreakComplete` wird verwendet, um nachzuverfolgen, wann eine Werbeunterbrechung abgeschlossen ist. Dieses Ereignis sollte nach Abschluss einer Werbeunterbrechung gesendet werden.

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

Der Ereignistyp `media.adStart` wird verwendet, um zu verfolgen, wann eine Anzeige beginnt. Dieses Ereignis sollte beim Start einer Anzeige gesendet werden.

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


### Abschluss der Anzeige {#ad-complete}

Der Ereignistyp `media.adComplete` wird verwendet, um nachzuverfolgen, wann eine Anzeige abgeschlossen ist. Dieses Ereignis sollte gesendet werden, wenn eine Anzeige abgeschlossen ist.

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

Der Ereignistyp `media.adSkip` wird verwendet, um zu verfolgen, wann eine Anzeige übersprungen wird. Dieses Ereignis sollte gesendet werden, wenn eine Anzeige übersprungen wird.

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

Der Ereignistyp `media.chapterStart` wird verwendet, um zu verfolgen, wann ein Kapitel beginnt. Dieses Ereignis sollte beim Start eines Kapitels gesendet werden.

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


### Kapitelbeendigung {#chapter-complete}

Der Ereignistyp `media.chapterComplete` wird verwendet, um zu verfolgen, wann ein Kapitel abgeschlossen ist. Dieses Ereignis sollte nach Abschluss eines Kapitels gesendet werden.

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


### Überspringen eines Kapitels {#chapter-skip}

Der Ereignistyp `media.chapterSkip` wird verwendet, um zu verfolgen, wann ein Kapitel übersprungen wird. Dieses Ereignis sollte gesendet werden, wenn ein Kapitel übersprungen wird.

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


### Pufferstart {#buffer-start}

Der Ereignistyp `media.bufferStart` wird verwendet, um zu verfolgen, wann die Pufferung beginnt. Dieses Ereignis sollte beim Start der Pufferung gesendet werden. Es gibt keinen `bufferResume` -Ereignistyp. Eine `bufferResume` wird abgeleitet, wenn Sie ein Wiedergabeereignis nach `bufferStart` senden.

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

Der Ereignistyp `media.bitrateChange` wird verwendet, um zu verfolgen, wann sich die Bitrate ändert. Dieses Ereignis sollte gesendet werden, wenn sich die Bitrate ändert.

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

Der Ereignistyp `media.stateUpdate` wird verwendet, um zu verfolgen, wann sich der Player-Status ändert. Dieses Ereignis sollte gesendet werden, wenn sich der Player-Status ändert.

>[!BEGINTABS]

>[!TAB Automatisches Sitzungs-Tracking]

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

Der Ereignistyp `media.sessionEnd` wird verwendet, um das Media Analytics-Backend darauf hinzuweisen, die Sitzung sofort zu schließen, wenn der Benutzer die Anzeige des Inhalts abgebrochen hat und wahrscheinlich nicht zurückkehren wird.

Wenn Sie kein `sessionEnd` -Ereignis senden, wird die Sitzung abgebrochen, nachdem 10 Minuten lang keine Ereignisse eingegangen sind oder die Abspielleiste sich 30 Minuten lang nicht verändert hat. Die Sitzung wird automatisch gelöscht.

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


### Sitzungsende {#session-complete}

Der Ereignistyp `media.sessionComplete` wird verwendet, um zu verfolgen, wann eine Mediensitzung abgeschlossen ist. Dieses Ereignis sollte gesendet werden, wenn das Ende des Hauptinhalts erreicht ist.

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
