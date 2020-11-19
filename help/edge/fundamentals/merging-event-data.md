---
title: Zusammenführen von Ereignisdaten
seo-title: Zusammenführen von Adobe Experience Platform Web SDK-Ereignisdaten
description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignisdaten zusammenführen
seo-description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignisdaten zusammenführen
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise; Merge Id Promise;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 53%

---


# Zusammenführen von Ereignisdaten

>[!IMPORTANT]
>
>Diese Funktion befindet sich noch in der Entwicklung. Nicht alle Lösungen können Ereignis-Daten zusammenführen, wie auf dieser Seite beschrieben.

Manchmal sind nicht alle Daten verfügbar, wenn ein Ereignis auftritt. Möglicherweise möchten Sie die vorhandenen Daten erfassen, damit sie nicht verloren gehen, wenn der Nutzer beispielsweise den Browser schließt. Vielleicht möchten Sie aber auch alle Daten einbeziehen, die später verfügbar werden.

In diesem Fall können Sie Daten mit vorherigen Ereignissen zusammenführen, indem Sie `mergeId` wie folgt als Option an `event`-Befehle übergeben:

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  },
  "mergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "payments": [
          {
            "transactionID": "TR426941",
            "paymentAmount": 999.98,
            "paymentType": "credit_card",
            "currencyCode": "USD"
          }
        ]
      }
    }
  },
  "mergeId": "ABC123"
});
```

By passing the same value for the `mergeId` option to both event commands in this example, the data in the second event command is augmented to data previously sent on the first event command. A record for each event command is created in the [!DNL Experience Data Platform], but during reporting the records are joined together using the event merge ID and appear as a single event.

Wenn Sie Daten zu einem bestimmten Ereignis an Drittanbieter senden, können Sie auch dieselbe Ereigniszusammenführungs-ID für diese Daten angeben. Wenn Sie später die Daten von Drittanbietern in Adobe Experience Platform importieren, wird die Ereignis-Zusammenführungs-ID verwendet, um alle Daten zusammenzuführen, die aufgrund des diskreten Ereignisses auf Ihrer Webseite erfasst wurden.

## Generieren einer Ereigniszusammenführungs-ID

Die Ereignis Merge-ID kann eine beliebige Zeichenfolge sein. Denken Sie jedoch daran, dass alle Ereignis, die mit derselben ID gesendet werden, als ein einziges Ereignis gemeldet werden. Achten Sie daher darauf, Eindeutigkeit zu erzwingen, wenn Ereignis nicht zusammengeführt werden sollten. Wenn Sie möchten, dass das SDK in Ihrem Namen eine eindeutige Ereigniszusammenführungs-ID generiert (entsprechend der allgemein verwendeten [UUID v4-Spezifikation](https://www.ietf.org/rfc/rfc4122.txt)), können Sie dafür den `createEventMergeId`-Befehl verwenden.

Wie bei allen Befehlen wird ein Promise zurückgegeben, da Sie den Befehl ausführen können, bevor das SDK geladen wurde. Das Promise wird so bald wie möglich mit einer eindeutigen Ereigniszusammenführungs-ID aufgelöst. Sie können wie folgt warten, bis das Promise aufgelöst ist, bevor Sie Daten an den Server senden:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
    "xdm": {
      "commerce": {
        "order": {
          "purchaseID": "a8g784hjq1mnp3",
          "purchaseOrderNumber": "VAU3123",
          "currencyCode": "USD",
          "priceTotal": 999.98
        }
      }
    },
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
    "xdm": {
      "commerce": {
        "order": {
          "payments": [
            {
              "transactionID": "TR426941",
              "paymentAmount": 999.98,
              "paymentType": "credit_card",
              "currencyCode": "USD"
            }
          ]
        }
      }
    },
    "mergeId": results.eventMergeId
  });
});
```

Gehen Sie genauso vor, wenn Sie aus anderen Gründen auf die Ereigniszusammenführungs-ID zugreifen möchten (beispielsweise, um diese an einen Drittanbieter zu senden):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Hinweis zum XDM-Format

Innerhalb des Befehls &quot;Ereignis&quot;wird die Ereignis-Merge-ID der `xdm` Payload am richtigen Speicherort in Ihrem Namen hinzugefügt.  If desired, the event merge ID can be sent as part of the `xdm` option instead, like this:

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    },
    "eventMergeId": "ABC123"
  }
});
```

Beachten Sie beim direkten Hinzufügen der Ereignis-Zusammenführungs-ID zum `xdm` Objekt, dass der Name `eventMergeID` anstelle von `mergeId`verwendet wird.
