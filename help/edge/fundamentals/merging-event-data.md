---
title: Zusammenführen von Ereignisdaten
seo-title: Zusammenführen von Adobe Experience Platform Web SDK-Ereignisdaten
description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignisdaten zusammenführen
seo-description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignisdaten zusammenführen
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 42%

---


# Zusammenführen von Ereignisdaten

>[!IMPORTANT]
>
>Diese Funktion befindet sich noch in der Entwicklung. Nicht alle Lösungen können Ereignis-Daten zusammenführen, wie auf dieser Seite beschrieben.

Manchmal sind nicht alle Daten verfügbar, wenn ein Ereignis auftritt. Möglicherweise möchten Sie die _vorhandenen_ Daten erfassen, damit sie nicht verloren gehen, wenn der Nutzer beispielsweise den Browser schließt. Vielleicht möchten Sie aber auch alle Daten einbeziehen, die später verfügbar werden.

In diesem Fall können Sie Daten mit vorherigen Ereignissen zusammenführen, indem Sie `eventMergeId` wie folgt als Option an `event`-Befehle übergeben:

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
  }
  "eventMergeId": "ABC123"
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
  }
  "eventMergeId": "ABC123"
});
```

By passing the same `eventMergeID` value to both event commands in this example, the data in the second event command is augmented to data previously sent on the first event command. A record for each event command is created in the [!DNL Experience Data Platform], but during reporting the records are joined together using the `eventMergeID` and appear as a single event.

If you are sending data about a particular event to third-party providers, you can include the same `eventMergeID` with that data as well. Later, if you choose to import the third-party data into the Adobe Experience Platform, `eventMergeID` will be used to merge together all data that was collected as a result of the discrete event that occurred on your webpage.

## Generieren einer `eventMergeID`

The `eventMergeID` value can be any string you choose, but remember that all events sent using the same ID are reported as a single event, so be careful to enforce uniqueness when events should not be merged. If you would like the SDK to generate a unique `eventMergeID` on your behalf (following the widely-adopted [UUID v4 specification](https://www.ietf.org/rfc/rfc4122.txt)), you can use the `createEventMergeId` command to do so.

Wie bei allen Befehlen wird ein Promise zurückgegeben, da Sie den Befehl ausführen können, bevor das SDK geladen wurde. The promise will be resolved with a unique `eventMergeID` as soon as possible. Sie können wie folgt warten, bis das Promise aufgelöst ist, bevor Sie Daten an den Server senden:

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
    }
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
    }
    "mergeId": results.eventMergeId
  });
});
```

Follow this same pattern if you would like access to the `eventMergeID` for other reasons (for example, to send it to a third-party provider):

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## Hinweis zum XDM-Format

Innerhalb des Ereignisbefehls wird die `mergeId` tatsächlich zur `xdm`-Payload hinzugefügt.  Falls gewünscht, kann die `mergeId` stattdessen als Teil der XDM-Option gesendet werden. Beispiel:

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
