---
title: Zusammenführen von Ereignis-Daten
seo-title: Zusammenführen von Adobe Experience Platform Web SDK-Ereignis-Daten
description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignis-Daten zusammenführen
seo-description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignis-Daten zusammenführen
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Zusammenführen von Ereignis-Daten

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Manchmal sind nicht alle Daten verfügbar, wenn ein Ereignis auftritt. Möglicherweise möchten Sie die _vorhandenen_ Daten erfassen, damit sie nicht verloren gehen, wenn der Benutzer beispielsweise den Browser schließt. Auf der anderen Seite können Sie auch alle Daten einbeziehen, die später verfügbar werden.

In diesem Fall können Sie Daten mit vorherigen Ereignissen zusammenführen, indem Sie `eventMergeId` eine Option wie folgt an `event` Befehle übergeben:

```javascript
alloy("event", {
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

alloy("event", {
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

Durch Übergabe des gleichen Ereignis-Zusammenführungs-ID-Werts an beide Ereignis-Befehle in diesem Beispiel werden die Daten im zweiten Ereignis-Befehl zu Daten erweitert, die zuvor mit dem ersten Ereignis-Befehl gesendet wurden. Ein Datensatz für jeden Ereignis-Befehl wird in der Experience Data Platform erstellt, aber während des Berichte werden die Datensätze mit der Ereignis Merge-ID verknüpft und als ein Ereignis angezeigt.

Wenn Sie Daten zu einem bestimmten Ereignis an Drittanbieter senden, können Sie auch dieselbe Ereignis-Zusammenführungs-ID mit diesen Daten einbeziehen. Wenn Sie später die Daten von Drittanbietern in die Adobe Experience Platform importieren, wird die Ereignis Merge-ID verwendet, um alle Daten zusammenzuführen, die aufgrund des diskreten Ereignisses auf Ihrer Webseite erfasst wurden.

## Generieren einer Ereignis Merge ID

Der Ereignis Merge ID-Wert kann eine beliebige Zeichenfolge sein. Beachten Sie jedoch, dass alle Ereignis, die mit derselben ID gesendet werden, als ein einziges Ereignis gemeldet werden. Achten Sie daher darauf, Eindeutigkeit zu erzwingen, wenn Ereignis nicht zusammengeführt werden sollten. Wenn Sie möchten, dass das SDK in Ihrem Namen eine eindeutige Ereignis-Merge-ID generiert (entsprechend der allgemein verwendeten [UUID v4-Spezifikation](https://www.ietf.org/rfc/rfc4122.txt)), können Sie dies mit dem `createEventMergeId` Befehl tun.

Wie bei allen Befehlen wird ein Versprechen zurückgegeben, da Sie den Befehl ausführen können, bevor das SDK geladen wurde. Das Versprechen wird so bald wie möglich mit einer eindeutigen Ereignis-Merge-ID gelöst. Sie können wie folgt warten, bis das Versprechen gelöst ist, bevor Sie Daten an den Server senden:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(eventMergeId) {
  alloy("event", {
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
    "mergeId": eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(eventMergeId) {
  alloy("event", {
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
    "mergeId": eventMergeId
  });
});
```

Führen Sie dasselbe Muster aus, wenn Sie aus anderen Gründen (z. B. um die Ereignis-Zusammenführungs-ID an einen Drittanbieter zu senden) zugreifen möchten:

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(eventMergeId) {
  // send event merge ID to a third-party provider
  console.log(eventMergeId);
});
```

## Hinweis zum XDM-Format

Innerhalb des Befehls &quot;Ereignis&quot; `mergeId` wird die `xdm` Payload hinzugefügt.  Falls gewünscht, `mergeId` kann die Datei stattdessen als Teil der xdm-Option gesendet werden. Beispiel:

```javascript
alloy("event", {
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
