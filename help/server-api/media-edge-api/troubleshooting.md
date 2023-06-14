---
keywords: Experience Platform; Medien-Edge; beliebte Themen; Datumsbereich
solution: Experience Platform
title: Erste Schritte mit Media Edge-APIs
description: Handbuch zur Fehlerbehebung bei Media Edge-APIs
source-git-commit: f723114eebc9eb6bfa2512b927c5055daf97188b
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 1%

---


# Handbuch zur Fehlerbehebung bei Media Edge API

Dieses Handbuch enthält Anweisungen zur Fehlerbehebung und zum Erhalten erfolgreicher Antworten.

## Verwenden von Fehlerreaktionshilfen

Um die Fehlerbehebung bei fehlerhaften Antworten zu unterstützen, wird den Fehlern ein Antworttext mit einem Fehlerobjekt hinzugefügt. In diesem Fall enthält der Antworttext Problemdetails, wie definiert durch [RFC 7807 - Problemdetails für HTTP-APIs](https://datatracker.ietf.org/doc/html/rfc7807). Um das Benutzererlebnis der API zu verbessern, sind die Problemdetails beschreibend (die Details der Array-Schlüssel werden mit JsonPath zum fehlenden oder ungültigen Feld angezeigt). Sie sind auch kumulativ (alle ungültigen Felder werden in derselben Anfrage gemeldet).


## Validieren von Sitzungsstarts

Die meisten Probleme beim Erstellen von Sitzungsstartanfragen führen zu einer Antwort mit 207 Mehrfachstatus.
Die Payload ähnelt den nicht schwerwiegenden Fehlern der Experience Edge Network Server-API. Alle Media Analytics-Fehler haben den folgenden Typ:  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. Die in der Antwort angezeigten Zahlen entsprechen dem Fehlerstatus.

Das folgende Beispiel zeigt einen Antworttext für eine Sitzungsstartanforderung, bei der beide kein Pflichtfeld und kein ungültiges Feld vorhanden sind.

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

Im obigen Beispiel werden beide Probleme durch `name` und `reason` under `details`: Der erste Grund wird angezeigt `missing required field` und der zweite Abschnitt beschreibt die Nichteinhaltung der ISO 8601-Norm.


>[!NOTE]
>
> Adobe empfiehlt, die generierte Mediensitzung auch weiterhin zu verarbeiten, wenn Fehler auftreten, die zuvor in Media Analytics verursacht wurden.

## Validieren von Ereignissen

Die meisten ungültigen Ereignisanfragen führen zu einer Antwort &quot;400 Ungültige Anfrage&quot;. In diesen Fällen ähnelt die Payload den schwerwiegenden Fehlern der Experience Edge Network Server-API.

Für Ereignisanfragen umfasst der Media Edge-API-Dienst zusätzliche Prüfungen, die nicht im XDM-Modell selbst erfasst werden. Dazu gehört auch die Prüfung, ob der Pfad `eventType` entspricht der Anfrage-Payload `eventType`.


Das folgende Beispiel zeigt eine `eventType` nicht übereinstimmen mit einer `adBreakStart` Nutzlast gesendet an `ee/va/v1/chapterStart`:

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

Das folgende Beispiel zeigt eine zusätzliche Media Edge-API-Prüfung, anhand derer eine `chapterStart` Aufruf fehlt `chapterDetails` info:

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

## Umgang mit Fehlern der Stufe 400 und der Stufe 500

In der folgenden Tabelle finden Sie Anweisungen zum Umgang mit Statusreaktionsfehlern:


| Fehler-Code | Beschreibung |
| ---------- | --------- |
| 4xx Bad request | Die meisten 4xx-Fehler (z. B. `400`, `403`, `404`) sollte vom Benutzer nicht erneut versucht werden. Eine erneute Ausführung der Anfrage führt nicht zu einer erfolgreichen Antwort. Der Benutzer sollte den Fehler beheben, bevor er die Anfrage erneut versucht. Ereignisse, die zu 4xx-Status-Codes führen, werden nicht verfolgt. Dies könnte sich auf die Genauigkeit von Daten in Sitzungen auswirken, die 4xx-Antworten erhalten haben. |
| 410 Stück | Gibt an, dass die für die Verfolgung bestimmte Sitzung nicht mehr serverseitig berechnet wird. Der häufigste Grund dafür ist, dass die Sitzung länger als 24 Stunden dauert. Nach Erhalt einer `410`, versuchen Sie, eine neue Sitzung zu starten und sie zu verfolgen. |
| 429 Zu viele Anfragen | Dieser Antwort-Code gibt an, dass der Server die Anforderungen durch Ratenbegrenzung begrenzt. Befolgen Sie die **Wiederholen nach** Anweisungen im Antwortheader sorgfältig beschrieben. Jede Antwort, die zurückfließt, muss den HTTP-Antwort-Code mit einem domänenspezifischen Fehlercode enthalten. |
| 500 Interner Server-Fehler | `500` Fehler sind allgemeine, allgemeingültige Fehler. `500` -Fehler sollten nicht wiederholt werden, mit Ausnahme von `502`, `503` und `504`. |
| 502 Schlechtes Gateway | Dieser Fehlercode Gibt an, dass der Server als Gateway eine ungültige Antwort von Upstream-Servern erhalten hat. Dies kann aufgrund von Netzwerkproblemen zwischen Servern geschehen. Das temporäre Netzwerkproblem kann sich selbst lösen, sodass ein erneuter Versuch mit der Anfrage das Problem möglicherweise beheben kann. |
| 503 Dienst nicht verfügbar | Dieser Fehlercode zeigt an, dass der Dienst vorübergehend nicht verfügbar ist. Dies kann während der Wartungszeiträume geschehen. Empfänger `503` Fehler können die Anfrage erneut versuchen, sollten aber auch dem **Wiederholen nach** Kopfzeilenanweisungen. |


## Einreihen von Ereignissen in die Warteschlange bei langsamen Sitzungsantworten

Nach dem Starten einer Medien-Tracking-Sitzung wird der Medienplayer möglicherweise ausgelöst, bevor die Antwort &quot;Sitzungsstart&quot;aus dem Backend (mit dem Parameter Sitzungs-ID ) zurückgegeben wird. In diesem Fall muss Ihre App alle Tracking-Ereignisse in die Warteschlange stellen, die zwischen der Sitzungsanforderung und der zugehörigen Antwort eintreffen. Wenn die Sitzungsantwort eingeht, sollten Sie zunächst alle Ereignisse in der Warteschlange verarbeiten und dann mit der Verarbeitung von Live-Ereignissen beginnen.

Die besten Ergebnisse erzielen Sie, wenn Sie im Referenz-Player in Ihrer Distribution Anweisungen zur Verarbeitung von Ereignissen vor dem Erhalt einer Sitzungs-ID finden.

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


