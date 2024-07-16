---
title: Clientseitige Protokollierung für A4T-Daten im Platform Web SDK
description: Erfahren Sie, wie Sie die clientseitige Protokollierung für Adobe Analytics for Target (A4T) mithilfe des Experience Platform Web SDK aktivieren.
seo-title: Client-side logging for A4T data in the Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: Target; a4t; Protokollierung; Web SDK; Erlebnis; Plattform;
exl-id: 7071d7e4-66e0-4ab5-a51a-1387bbff1a6d
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Clientseitige Protokollierung für A4T-Daten im Platform Web SDK

## Übersicht {#overview}

Mit dem Adobe Experience Platform Web SDK können Sie [Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) -Daten auf der Clientseite Ihrer Webanwendung erfassen.

Clientseitige Protokollierung bedeutet, dass relevante [!DNL Target] -Daten auf Client-Seite zurückgegeben werden, sodass Sie sie erfassen und für Analytics freigeben können. Diese Option sollte aktiviert sein, wenn Sie Daten mithilfe der [Dateneinfüge-API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html) manuell an Analytics senden möchten.

>[!NOTE]
>
>Eine Methode zur Durchführung dieses Vorgangs mit [AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=de) befindet sich derzeit in der Entwicklung und wird demnächst verfügbar sein.

In diesem Dokument werden die Schritte zum Einrichten der clientseitigen A4T-Protokollierung für das Web SDK beschrieben und einige Implementierungsbeispiele für häufige Anwendungsfälle bereitgestellt.

## Voraussetzungen {#prerequisites}

In diesem Tutorial wird davon ausgegangen, dass Sie mit den grundlegenden Konzepten und Prozessen im Zusammenhang mit der Verwendung des Web SDK zu Personalisierungszwecken vertraut sind. Wenn Sie eine Einführung benötigen, lesen Sie die folgende Dokumentation:

* [Web SDK konfigurieren](/help/web-sdk/commands/configure/overview.md)
* [Ereignisse senden](/help/web-sdk/commands/sendevent/overview.md)
* [Rendern von Personalisierungsinhalten](../../rendering-personalization-content.md)

## Clientseitige Protokollierung in Analytics einrichten {#set-up-client-side-logging}

In den folgenden Unterabschnitten wird beschrieben, wie Sie die clientseitige Protokollierung für Ihre Web SDK-Implementierung aktivieren.

### Aktivieren der clientseitigen Analytics-Protokollierung {#enable-analytics-client-side-logging}

Um die clientseitige Protokollierung in Analytics für Ihre Implementierung als aktiviert zu betrachten, müssen Sie die Adobe Analytics-Konfiguration in Ihrem [Datastream](../../../../datastreams/overview.md) deaktivieren.

![Analytics-Datastream-Konfiguration deaktiviert](../assets/disable-analytics-datastream.png)

### [!DNL A4T] -Daten aus dem SDK abrufen und an Analytics senden {#a4t-to-analytics}

Damit diese Berichtsmethode ordnungsgemäß funktioniert, müssen Sie die [!DNL A4T] -bezogenen Daten senden, die aus dem Befehl [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) im Analytics-Treffer abgerufen wurden.

Wenn Target Edge eine Vorschlagsantwort berechnet, wird überprüft, ob die clientseitige Protokollierung in Analytics aktiviert ist (d. h. ob Analytics in Ihrem Datastream deaktiviert ist). Wenn die clientseitige Protokollierung aktiviert ist, fügt das System jedem Vorschlag in der Antwort ein Analytics-Token hinzu.

Der Fluss sieht in etwa so aus:

![Client-seitiger Protokollierungsfluss](../assets/analytics-client-side-logging.png)

Im Folgenden finden Sie ein Beispiel für eine `interact` -Antwort, wenn die clientseitige Protokollierung in Analytics aktiviert ist. Wenn der Vorschlag für eine Aktivität mit Analytics-Berichten gilt, verfügt er über eine `scopeDetails.characteristics.analyticsToken` -Eigenschaft.

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

Vorschläge für formularbasierte Experience Composer-Aktivitäten können sowohl Inhalte als auch Klickmetriken unter demselben Vorschlag enthalten. Anstatt also ein einzelnes Analytics-Token für die Inhaltsanzeige in der Eigenschaft `scopeDetails.characteristics.analyticsToken` zu haben, können für diese sowohl ein Anzeige- als auch ein Klick-Analytics-Token in den Eigenschaften `scopeDetails.characteristics.analyticsDisplayToken` und `scopeDetails.characteristics.analyticsClickToken` angegeben werden, entsprechend.

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
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
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

Alle Werte aus `scopeDetails.characteristics.analyticsToken` sowie `scopeDetails.characteristics.analyticsDisplayToken` (für angezeigten Inhalt) und `scopeDetails.characteristics.analyticsClickToken` (für Klickmetriken) sind die A4T-Payloads, die erfasst und als `tnta`-Tag im Aufruf der [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) eingefügt werden müssen.

>[!IMPORTANT]
>
>Die Eigenschaften `analyticsToken`, `analyticsDisplayToken` und `analyticsClickToken` können mehrere Token enthalten, die als einzelne, kommagetrennte Zeichenfolge verkettet sind.
>
>In den Implementierungsbeispielen, die im nächsten Abschnitt bereitgestellt werden, werden mehrere Analytics-Token iterativ erfasst. Verwenden Sie eine ähnliche Funktion, um ein Array von Analytics-Token zu verketten:
>
>```javascript
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

Sie können das Web SDK verwenden, um die Ausführung von Vorschlägen aus den Aktivitäten [Adobe Target Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de) zu steuern.

Wenn Sie Vorschläge für einen bestimmten Entscheidungsbereich anfordern, enthält der zurückgegebene Vorschlag das entsprechende Analytics-Token. Es empfiehlt sich, den Befehl &quot;Platform Web SDK `sendEvent`&quot;zu verketten und die zurückgegebenen Vorschläge zu durchlaufen, um sie beim gleichzeitigen Erfassen der Analytics-Token auszuführen.

Sie können einen `sendEvent` -Befehl für einen formularbasierten Experience Composer-Aktivitätsbereich wie den folgenden Trigger ausführen:

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
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
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
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

Ein Vorschlag kann verschiedene Elementtypen aufweisen, wie durch die Eigenschaft `schema` des betreffenden Elements angegeben. Es werden vier Vorschlagselementschemata für formularbasierte Experience Composer-Aktivitäten unterstützt:

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` und `JSON_SCHEMA` sind die Schemas, die den Typ des Angebots widerspiegeln, während `MEASUREMENT_SCHEMA` die Metriken widerspiegelt, die an ein DOM-Element angehängt werden sollen.

Analytics-Payloads für Klickmetriken sollten erfasst und separat von den Inhaltselementen an Analytics gesendet werden, und zwar zu dem Zeitpunkt, zu dem der Besucher tatsächlich auf den zuvor angezeigten Inhalt klickt.

Die folgende Hilfsfunktion zum Abrufen der A4T-Klickmetrik-Payloads ist in diesem Fall praktisch:

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### Implementierungszusammenfassung {#implementation-summary}

Zusammenfassend müssen die folgenden Schritte ausgeführt werden, wenn formularbasierte Experience Composer-Aktivitäten mit dem Platform Web SDK angewendet werden:

1. Senden Sie ein Ereignis, das formularbasierte Experience Composer-Aktivitätsangebote abruft.
1. Wenden Sie die Inhaltsänderungen auf die Seite an.
1. Senden Sie das Benachrichtigungsereignis `decisioning.propositionDisplay` .
1. Erfassen Sie die Analytics-Display-Token aus der SDK-Antwort und erstellen Sie eine Payload für den Analytics-Treffer.
1. Senden der Payload an Analytics mithilfe der [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);
1. Wenn in den gelieferten Vorschlägen Klickmetriken enthalten sind, sollten Klicklistener eingerichtet werden, damit bei einem Klick das `decisioning.propositionInteract` -Benachrichtigungsereignis gesendet wird. Der `onBeforeEventSend` -Handler sollte so konfiguriert werden, dass beim Abfangen von `decisioning.propositionInteract` -Ereignissen die folgenden Aktionen ausgeführt werden:
   1. Erfassen der Klick-Analytics-Token von `xdm._experience.decisioning.propositions`
   1. Senden des Klickanalysetreffers mit der erfassten Analytics-Nutzlast über die [Dateneinfüge-API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md);

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

Mit dem Web SDK können Sie Angebote verarbeiten, die mit [Visual Experience Composer (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) erstellt wurden.

>[!NOTE]
>
>Die Schritte zur Implementierung dieses Anwendungsfalls ähneln den Schritten für [Formularbasierte Experience Composer-Aktivitäten](#form-based-composer). Weitere Informationen finden Sie im vorherigen Abschnitt .

Wenn die automatische Wiedergabe aktiviert ist, können Sie die Analytics-Token aus den Vorschlägen erfassen, die auf der Seite ausgeführt wurden. Es empfiehlt sich, den Befehl &quot;Platform Web SDK `sendEvent`&quot;zu verketten und die zurückgegebenen Vorschläge zu durchlaufen, um die vom Web SDK zu rendernden Vorschläge zu filtern.

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

### Umgang mit Seitenmetriken mit `onBeforeEventSend` {#using-onbeforeeventsend}

Mithilfe von Adobe Target-Aktivitäten können Sie verschiedene Metriken auf der Seite einrichten, die entweder manuell an das DOM angehängt oder automatisch an das DOM (mit VEC erstellte Aktivitäten) angehängt werden. Bei beiden Typen handelt es sich um eine verzögerte Benutzerinteraktion auf der Webseite.

Um dies zu berücksichtigen, empfiehlt es sich, Analytics-Payloads mithilfe des Erweiterungspunkts `onBeforeEventSend` Adobe Experience Platform Web SDK zu erfassen. Der Erweiterungspunkt `onBeforeEventSend` sollte mit dem Befehl `configure` konfiguriert werden und wird über alle Ereignisse angezeigt, die über den Datastream gesendet werden.

Im Folgenden finden Sie ein Beispiel dafür, wie `onBeforeEventSent` für Trigger Analytics-Treffer konfiguriert werden kann:

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

In diesem Handbuch wurde die clientseitige Protokollierung für A4T-Daten im Web SDK behandelt. Weitere Informationen zur Verarbeitung von A4T-Daten im Edge Network finden Sie im Handbuch zur [serverseitigen Protokollierung](server-side.md) .
