---
title: Zusammenführen von Ereignisdaten
seo-title: Zusammenführen von Adobe Experience Platform Web SDK-Ereignisdaten
description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignisdaten zusammenführen
seo-description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignisdaten zusammenführen
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 95%

---


# Zusammenführen von Ereignisdaten

>[!IMPORTANT]
>
>Diese Funktion befindet sich noch in der Entwicklung, sodass nicht alle Lösungen diese Daten zusammenführen können.

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

In diesem Beispiel werden durch die Übergabe desselben Werts für die Ereigniszusammenführungs-ID an beide Ereignisbefehle die Daten im zweiten Ereignisbefehl mit Daten angereichert, die zuvor beim ersten Ereignisbefehl gesendet wurden. In Experience Data Platform wird ein Datensatz für jeden Ereignisbefehl erstellt, während des Reportings werden die Datensätze jedoch anhand der Ereigniszusammenführungs-ID verknüpft und als ein Ereignis angezeigt.

Wenn Sie Daten zu einem bestimmten Ereignis an Drittanbieter senden, können Sie auch dieselbe Ereigniszusammenführungs-ID für diese Daten angeben. Wenn Sie später die Daten von Drittanbietern in Adobe Experience Platform importieren, wird die Ereigniszusammenführungs-ID verwendet, um alle Daten zusammenzuführen, die aufgrund des diskreten Ereignisses auf Ihrer Web-Seite erfasst wurden.

## Generieren einer Ereigniszusammenführungs-ID

Der Wert für die Ereigniszusammenführungs-ID kann eine beliebige Zeichenfolge sein. Beachten Sie jedoch, dass alle Ereignisse, die mit derselben ID gesendet werden, als ein einziges Ereignis gemeldet werden. Achten Sie daher darauf, Eindeutigkeit zu erzwingen, wenn Ereignisse nicht zusammengeführt werden sollen. Wenn Sie möchten, dass das SDK in Ihrem Namen eine eindeutige Ereigniszusammenführungs-ID generiert (entsprechend der allgemein verwendeten [UUID v4-Spezifikation](https://www.ietf.org/rfc/rfc4122.txt)), können Sie dafür den `createEventMergeId`-Befehl verwenden.

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

Gehen Sie genauso vor, wenn Sie aus anderen Gründen auf die Ereigniszusammenführungs-ID zugreifen möchten (beispielsweise, um diese an einen Drittanbieter zu senden):

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
