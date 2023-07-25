---
solution: Experience Platform
title: Erste Schritte mit Media Edge-APIs
description: Handbuch zur Fehlerbehebung bei Media Edge-APIs
source-git-commit: ff4bc64843e3d05277f56ab67b60400fb9e65c4f
workflow-type: ht
source-wordcount: '669'
ht-degree: 100%

---


# Handbuch zur Fehlerbehebung bei Media Edge-APIs

Dieses Handbuch enthält Anweisungen zur Fehlerbehebung und zum Erhalt erfolgreicher Antworten.

## Verwenden von Fehlerantworthilfen

Um die Fehlerbehebung bei fehlgeschlagenen Antworten zu unterstützen, wird den Fehlern ein Antworttext mit einem Fehlerobjekt hinzugefügt. In diesem Fall enthält der Antworttext Problemdetails, wie im Dokument [RFC 7807 – Problemdetails für HTTP-APIs](https://datatracker.ietf.org/doc/html/rfc7807) definiert. Um das API-Anwendererlebnis zu verbessern, sind die Problemdetails zum einen beschreibend (Details der Array-Schlüssel werden mit JsonPath zum fehlenden oder ungültigen Feld angezeigt), zum anderen kumulativ (alle ungültigen Felder werden in derselben Anfrage gemeldet).


## Validieren von Sitzungsstarts

Die meisten Probleme bei Sitzungsstart-Anfragen führen zu einer 207-Mehrfachstatus-Antwort.
Die Payload ähnelt nicht schwerwiegenden Fehlern der Experience Edge Network-Server-API. Alle
Media Analytics-Fehler weisen den folgenden Typ auf:  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. Die in der Antwort angezeigten Zahlen entsprechen dem Fehlerstatus.

Das folgende Beispiel zeigt einen Antworttext für eine Sitzungsstart-Anfrage, bei der ein Pflichtfeld fehlt und zudem ein ungültiges Feld enthalten ist.

```
{
    "requestId": "d4be4f91-a535-41e7-80c6-bdd031d3a365",
    "handle": [
        ...
    ],
    "errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
            "status": 400,
            "title": "Invalid request",
            "report": {
                "eventIndex": 0,
                "details": [
                    {
                        "name": "$.xdm.mediaCollection.sessionDetails.name",
                        "reason": "Missing required field"
                    },
                    {
                        "name": "$.xdm.timestamp",
                        "reason": "Field should respect ISO 8601 standard for presenting date and time with offset to UTC (e.g. 2022-05-19T19:31:02Z, 2022-05-19T21:31:02+02:00, 2022-05-19T21:31:02.234+02:00)"
                    }
                ]
            }
        }
    ]
}
```

Im obigen Beispiel sind beide Probleme durch `name` und `reason` unter `details` vermerkt: Als erster Grund wird `missing required field` angezeigt, als zweiter wird die Nichteinhaltung des ISO 8601-Standards genannt.


>[!NOTE]
>
> Adobe empfiehlt, die Verarbeitung der generierten Mediensitzung fortzusetzen, wenn Fehler auftreten, die zuvor in Media Analytics verursacht wurden.

## Validieren von Ereignissen

Die meisten ungültigen Ereignisanfragen führen zu einer Antwort vom Typ „400 Ungültige Anfrage“. In diesen Fällen ähnelt die Payload schwerwiegenden Fehlern der Experience Edge Network-Server-API.

Bei Ereignisanfragen umfasst der Media Edge-API-Service zusätzliche Prüfungen, die nicht im XDM-Modell selbst erfasst werden. Dazu gehört auch die Prüfung, ob der Pfad `eventType` der Anfrage-Payload `eventType` entspricht.


Das folgende Beispiel zeigt einen `eventType`-Konflikt mit einer an `ee/va/v1/chapterStart` gesendeten `adBreakStart`-Payload:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": "The payload eventType adBreakStart was different from the path eventType chapterStart"
    }
}
```

Das folgende Beispiel zeigt eine zusätzliche Media Edge-API-Prüfung, durch die ein `chapterStart`-Aufruf mit fehlenden `chapterDetails`-Informationen gefunden wurde:

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": [
            {
                "name": "$.events[0].xdm.mediaCollection.chapterDetails",
                "reason": "Missing required field"
            }
        ]
    }
}
```

## Umgang mit Fehlern der 400er- und 500er-Reihe

In der folgenden Tabelle finden Sie Anweisungen zum Umgang mit Statusantwortfehlern:


| Fehler-Code | Beschreibung |
| ---------- | --------- |
| 4xx Ungültige Anfrage | Bei den meisten 4xx-Fehlern (z. B. `400`, `403`, `404`) sollten Benutzende die Anfrage nicht wiederholen. Eine erneute Ausführung der Anfrage führt nicht zu einer erfolgreichen Antwort. Benutzende sollten den Fehler beheben, bevor sie die Anfrage wiederholen. Ereignisse, die zu 4xx-Status-Codes führen, werden nicht nachverfolgt. Dies könnte sich auf die Genauigkeit von Daten in Sitzungen auswirken, die 4xx-Antworten erhalten haben. |
| 410 Nicht mehr auffindbar | Dieser Antwort-Code gibt an, dass die zum Tracking bestimmte Sitzung Server-seitig nicht mehr berechnet wird. Der häufigste Grund dafür ist, dass die Sitzung länger als 24 Stunden dauert. Versuchen Sie nach Erhalt eines `410`-Fehlers, eine neue Sitzung zu starten und sie nachzuverfolgen. |
| 429 Zu viele Anfragen | Dieser Antwort-Code gibt an, dass der Server Anfragen durch Ratenbegrenzung einschränkt. Halten Sie sich genau an den Anweisungen in der **Retry-After**-Antwortkopfziele. Jede Antwort, die zurückgegeben wird, muss den HTTP-Antwort-Code mit einem Domain-spezifischen Fehler-Code enthalten. |
| 500 Interner Server-Fehler | `500`-Fehler sind generische, allgemeingültige Fehler. `500`-Fehler sollten nicht wiederholt werden, mit Ausnahme von `502`, `503` und `504`. |
| 502 Ungültiges Gateway | Dieser Fehler-Code gibt an, dass der Server als Gateway eine ungültige Antwort von Upstream-Servern erhalten hat. Hierzu kann es aufgrund von Netzwerkproblemen zwischen Servern kommen. Das temporäre Netzwerkproblem kann sich von selbst lösen, sodass das Problem durch einen erneuten Anfrageversuch möglicherweise behoben wird. |
| 503 Service nicht verfügbar | Dieser Fehler-Code gibt an, dass der Service vorübergehend nicht verfügbar ist. Hierzu kann es während Wartungszeiträumen kommen. Empfänger von `503`-Fehlern können die Anfrage wiederholen, sollten aber ebenfalls den Anweisungen im **Retry-After**-Header folgen. |


## Einreihen von Ereignissen in die Warteschlange bei langsamen Sitzungsantworten

Nach Start einer Medien-Tracking-Sitzung wird der Medien-Player möglicherweise ausgelöst, bevor vom Backend die Sitzungsstart-Antwort (mit dem Sitzungs-ID-Parameter) zurückgegeben wird. In diesem Fall muss Ihre Applikation sämtliche Tracking-Ereignisse in die Warteschlange einreihen, die zwischen der Sitzungsstart-Anfrage und ihrer Antwort eingehen. Wenn die Sitzungsantwort eingeht, sollten Sie zunächst alle Ereignisse in der Warteschlange verarbeiten. Anschließend können Sie mit der Verarbeitung von Live-Ereignissen beginnen.

Um optimale Ergebnisse zu erzielen, folgen Sie im Referenz-Player Ihrer Distribution den Anweisungen zur Verarbeitung von Ereignissen vor dem Erhalt einer Sitzungs-ID.

Das folgende Beispiel zeigt eine Methode zur Verarbeitung von Ereignissen vor dem Erhalt einer Sitzungs-ID:


```
// For event payload format, see "Request body" sections of "Session Start Request", "Event Requests" respectively.  *
 
VideoPlayer.prototype._collectEvent = function(event) {
    var sessionID = event.events[0].xdm.mediaCollection.sessionID
    var eventType = event.events[0].xdm.eventType.substring("media.".length);
    // If we don't have a Session ID yet,
    // queue the event and return...
    if (sessionId === undefined) {
        console.log("[Player] Queueing event")
        _pendingEvents.push(event)
        return;
    }
 
    // If we DO have a Session ID, process the
    // tracking event...
    apiClient.request({
        "baseUrl": `${endpoint}`,
        "path": `ee/va/v1/${eventType}`,
        "method": `POST`,
        "data": `${event}`
    }).then((response) => {
        if (eventType === "sessionStart") {
            var newSessionID = response.json().handle.filter((h) => h.type === "media-analytics:new-session")[0].payload[0].sessionId;
            _processPendingEvents(newSessionID);
        }
        […]
    }
}
 
VideoPlayer.prototype._processPendingEvents function(sessionID) {
    _pendingEvents.forEach((event) => {
        event.events[0].xdm.mediaCollection.sessionID = sessionID;
        _collectEvent(event);
    });
    _pendingEvents = [];
}
```


