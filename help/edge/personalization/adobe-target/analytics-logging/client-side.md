---
title: Clientseitige Protokollierung für A4T-Daten im Platform Web SDK
description: Erfahren Sie, wie Sie die clientseitige Protokollierung für Adobe Analytics for Target (A4T) mithilfe des Experience Platform Web SDK aktivieren.
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: Target; a4t; Protokollierung; Web SDK; Erlebnis; Plattform;
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 5%

---

# Clientseitige Protokollierung für A4T-Daten im Platform Web SDK

## Übersicht {#overview}

Mit dem Adobe Experience Platform Web SDK können Sie [Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=de) Daten auf der Clientseite Ihrer Webanwendung.

Die clientseitige Protokollierung bedeutet, dass [!DNL Target] -Daten werden Client-seitig zurückgegeben, sodass Sie sie erfassen und für Analytics freigeben können. Diese Option sollte aktiviert sein, wenn Sie Daten manuell mit der [Dateneinfüge-API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).

>[!NOTE]
>
>Eine Methode, um dies mit [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=de) befindet sich derzeit in der Entwicklung und wird demnächst verfügbar sein.

In diesem Dokument werden die Schritte zum Einrichten der clientseitigen A4T-Protokollierung für das Web SDK beschrieben und einige Implementierungsbeispiele für häufige Anwendungsfälle bereitgestellt.

## Voraussetzungen {#prerequisites}

In diesem Tutorial wird davon ausgegangen, dass Sie mit den grundlegenden Konzepten und Prozessen im Zusammenhang mit der Verwendung des Web SDK zu Personalisierungszwecken vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die folgende Dokumentation:

* [Web SDK konfigurieren](../../../fundamentals/configuring-the-sdk.md)
* [Senden von Ereignissen](../../../fundamentals/tracking-events.md)
* [Rendern von Personalisierungsinhalten](../../rendering-personalization-content.md)

## Clientseitige Protokollierung in Analytics einrichten {#set-up-client-side-logging}

In den folgenden Unterabschnitten wird beschrieben, wie Sie die clientseitige Protokollierung für Ihre Web SDK-Implementierung aktivieren.

### Aktivieren der clientseitigen Analytics-Protokollierung {#enable-analytics-client-side-logging}

Um die clientseitige Protokollierung in Analytics für Ihre Implementierung zu berücksichtigen, müssen Sie die Adobe Analytics-Konfiguration in Ihrer [datastream](../../../fundamentals/datastreams.md).

![Analytics-Datenspeicherkonfiguration deaktiviert](../assets/disable-analytics-datastream.png)

### Abrufen [!DNL A4T] Daten aus dem SDK und Senden an Analytics {#a4t-to-analytics}

Damit diese Berichtsmethode ordnungsgemäß funktioniert, müssen Sie die [!DNL A4T] verwandte Daten, die von der [`sendEvent`](../../../fundamentals/tracking-events.md) im Analytics-Treffer.

Wenn Target Edge eine Vorschlagsantwort berechnet, wird überprüft, ob die clientseitige Protokollierung in Analytics aktiviert ist (d. h. ob Analytics in Ihrem Datastream deaktiviert ist). Wenn die clientseitige Protokollierung aktiviert ist, fügt das System jedem Vorschlag in der Antwort ein Analytics-Token hinzu.

Der Fluss sieht in etwa so aus:

![Client-seitiger Protokollierungsfluss](../assets/analytics-client-side-logging.png)

Im Folgenden finden Sie ein Beispiel für eine `interact` Antwort, wenn die clientseitige Protokollierung in Analytics aktiviert ist. Wenn der Vorschlag für eine Aktivität mit Analytics-Berichten verwendet wird, wird eine `scopeDetails.characteristics.analyticsToken` -Eigenschaft.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            }
          ]
        },
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Vorschläge für formularbasierte Experience Composer-Aktivitäten können sowohl Inhalte als auch Klickmetriken unter demselben Vorschlag enthalten. Anstatt also nur ein Analytics-Token für die Inhaltsanzeige in `scopeDetails.characteristics.analyticsToken` -Eigenschaft verwenden, können diese sowohl ein Anzeigen- als auch ein Klick-Analysetoken unter `scopeDetails.characteristics.analyticsTokens` -Objekt, in `display` und `click` -Eigenschaften entsprechend.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
              "eventTokens": {
                "display": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
                "click": "E0gb6q1+WyFW3FMbbQJmrg=="
              },
              "analyticsTokens": {
                "display": "434689:0:0|2,434689:0:0|1",
                "click": "434689:0:0|32767"
              }
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            },
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

Alle Werte aus `scopeDetails.characteristics.analyticsToken`sowie `scopeDetails.characteristics.analyticsTokens.display` (für angezeigten Inhalt) und `scopeDetails.characteristics.analyticsTokens.click` (für Klickmetriken) sind die A4T-Payloads, die erfasst und als `tnta` -Tag im [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) aufrufen.

>[!IMPORTANT]
>
>Beachten Sie, dass einige `analyticsToken`/`analyticsTokens` -Eigenschaften können mehrere Token enthalten, die als einzelne, kommagetrennte Zeichenfolge verkettet sind.
>
>In den Implementierungsbeispielen, die im nächsten Abschnitt bereitgestellt werden, werden mehrere Analytics-Token iterativ erfasst. Verwenden Sie eine ähnliche Funktion, um ein Array von Analytics-Token zu verketten:
>
>
```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## Implementierungsbeispiele {#implementation-examples}

Die folgenden Unterabschnitte zeigen, wie Sie die clientseitige Protokollierung in Analytics für häufige Anwendungsfälle implementieren.

### Formularbasierte Experience Composer-Aktivitäten {#form-based-composer}

Sie können das Web SDK verwenden, um die Ausführung von Vorschlägen von [Formularbasierter Experience Composer für Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de) Aktivitäten.

Wenn Sie Vorschläge für einen bestimmten Entscheidungsbereich anfordern, enthält der zurückgegebene Vorschlag das entsprechende Analytics-Token. Best Practice ist, das Platform Web SDK zu ketten `sendEvent` und navigieren Sie durch die zurückgegebenen Vorschläge, um sie beim gleichzeitigen Erfassen der Analytics-Token auszuführen.

Sie können eine `sendEvent` für einen formularbasierten Experience Composer-Aktivitätsbereich wie folgt:

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

Von hier aus müssen Sie Code implementieren, um die Vorschläge auszuführen und eine Payload zu erstellen, die letztendlich an Analytics gesendet wird. Dies ist ein Beispiel dafür, was `results.propositions` enthalten könnte:

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventTokens": {
          "display": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "click": "Tagb6q1+WyFW3FMbbQJrtg=="
        },
        "analyticsTokens": {
          "display": "434688:0:0|2,434688:0:0|1",
          "click": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

Um das Analytics-Token aus einem Vorschlag mit Inhaltselementen zu extrahieren, können Sie eine Funktion implementieren, die der folgenden ähnelt:

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsTokens) {
    return characteristics.analyticsTokens.display;
  }
  return characteristics.analyticsToken;
}
```

Ein Vorschlag kann verschiedene Arten von Artikeln enthalten, wie durch die Variable `schema` -Eigenschaft des betreffenden Elements. Es werden vier Vorschlagselementschemata für formularbasierte Experience Composer-Aktivitäten unterstützt:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` und `JSON_SCHEMA` sind die Schemas, die den Angebotstyp widerspiegeln, während `MEASUREMENT_SCHEMA` spiegelt die Metriken wider, die an ein DOM-Element angehängt werden sollen.

Analytics-Payloads für Klickmetriken sollten erfasst und separat von den Inhaltselementen an Analytics gesendet werden, und zwar zu dem Zeitpunkt, zu dem der Besucher tatsächlich auf den zuvor angezeigten Inhalt klickt.

Die folgende Hilfsfunktion zum Abrufen der A4T-Klickmetrik-Payloads ist in diesem Fall praktisch:

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsTokens) {
    return characteristics.analyticsTokens.click;
  }
  return characteristics.analyticsToken;
}
```

#### Implementierungszusammenfassung {#implementation-summary}

Zusammenfassend müssen die folgenden Schritte ausgeführt werden, wenn formularbasierte Experience Composer-Aktivitäten mit dem Platform Web SDK angewendet werden:

1. Senden Sie ein Ereignis, das formularbasierte Experience Composer-Aktivitätsangebote abruft.
1. Wenden Sie die Inhaltsänderungen auf die Seite an.
1. Senden Sie die `decisioning.propositionDisplay` Benachrichtigungsereignis;
1. Erfassen Sie die Analytics-Display-Token aus der SDK-Antwort und erstellen Sie eine Payload für den Analytics-Treffer.
1. Senden der Payload an Analytics mithilfe der [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Wenn Klick-Metriken in den gelieferten Vorschlägen vorhanden sind, sollten Klick-Listener eingerichtet werden, damit bei einem Klick die `decisioning.propositionInteract` Benachrichtigungsereignis. Die `onBeforeEventSend` -Handler so konfiguriert werden, dass beim Abfangen `decisioning.propositionInteract` -Ereignissen, werden die folgenden Aktionen ausgeführt:
   1. Abruf der Klick-Analytics-Token aus `xdm._experience.decisioning.propositions`
   1. Senden des Klickanalysetreffers mit der erfassten Analytics-Nutzlast über [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### Visual Experience Composer-Aktivitäten {#visual-experience-composer-acitivties}

Mit dem Web SDK können Sie Angebote verarbeiten, die mit [Visual Experience Composer (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).

>[!NOTE]
>
>Die Schritte zur Implementierung dieses Anwendungsfalls ähneln den Schritten für [Formularbasierte Experience Composer-Aktivitäten](#form-based-composer). Weitere Informationen finden Sie im vorherigen Abschnitt .

Wenn die automatische Wiedergabe aktiviert ist, können Sie die Analytics-Token aus den Vorschlägen erfassen, die auf der Seite ausgeführt wurden. Best Practice ist, das Platform Web SDK zu ketten `sendEvent` und navigieren Sie durch die zurückgegebenen Vorschläge, um die vom Web SDK zu rendernden Vorschläge zu filtern.

**Beispiel**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  
  for (var i = 0; i < results.propositions.length; i++) {
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### Verwenden `onBeforeEventSend` zur Verarbeitung von Seitenmetriken {#using-onbeforeeventsend}

Mithilfe von Adobe Target-Aktivitäten können Sie verschiedene Metriken auf der Seite einrichten, die entweder manuell an das DOM angehängt oder automatisch an das DOM (mit VEC erstellte Aktivitäten) angehängt werden. Bei beiden Typen handelt es sich um eine verzögerte Benutzerinteraktion auf der Webseite.

Um dies zu berücksichtigen, empfiehlt es sich, Analytics-Payloads mithilfe der Variablen `onBeforeEventSend` Adobe Experience Platform Web SDK-Erweiterungspunkt. Die `onBeforeEventSend` Der Erweiterungspunkt sollte mithilfe der `configure` und wird für alle Ereignisse übernommen, die über den Datastream gesendet werden.

Im Folgenden finden Sie ein Beispiel dafür, wie `onBeforeEventSent` kann für Trigger Analytics-Treffer konfiguriert werden:

```javascript
alloy("configure", {
  edgeConfigId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## Nächste Schritte {#next-steps}

In diesem Handbuch wurde die clientseitige Protokollierung für A4T-Daten im Web SDK behandelt. Siehe Handbuch unter [Serverseitige Protokollierung](server-side.md) Weitere Informationen zur Verarbeitung von A4T-Daten im Edge-Netzwerk.
