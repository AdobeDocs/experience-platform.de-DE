---
title: Ereignisse mit dem Adobe Experience Platform Web SDK verfolgen
description: Erfahren Sie, wie Sie Adobe Experience Platform Web SDK-Ereignis verfolgen.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;sendBeacon;documentUnloading;Dokument Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 25cf425df92528cec88ea027f3890abfa9cd9b41
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 46%

---


# Ereignisse verfolgen

Verwenden Sie zum Senden von Ereignis-Daten an Adobe Experience Cloud den Befehl `sendEvent`. Der `sendEvent`-Befehl ist die wichtigste Methode zum Senden von Daten an und zum Abrufen von personalisierten Inhalten, Identitäten und Zielgruppenzielen.[!DNL Experience Cloud]

An Adobe Experience Cloud gesendete Daten gehören zwei Kategorien an:

* XDM-Daten
* Nicht-XDM-Daten (derzeit nicht unterstützt)

## Senden von XDM-Daten

XDM-Daten sind Objekte, deren Inhalt und Struktur mit einem Schema übereinstimmen, das Sie in Adobe Experience Platform erstellt haben. [Erfahren Sie mehr darüber, wie Sie ein Schema erstellen.](../../xdm/tutorials/create-schema-ui.md)

Alle XDM-Daten, die Sie in Ihre Analyse-, Personalisierungs-, Audiencen- oder Zielorte aufnehmen möchten, sollten mit der Option `xdm` gesendet werden.


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
});
```

Zwischen der Ausführung des Befehls `sendEvent` und dem Senden der Daten an den Server kann eine gewisse Zeit vergehen (z. B. wenn die Web SDK-Bibliothek noch nicht vollständig geladen wurde oder die Zustimmung noch nicht eingegangen ist). Wenn Sie nach dem Ausführen des Befehls `sendEvent` einen beliebigen Teil des Objekts ändern möchten, sollten Sie das `xdm`-Objekt _vor dem Ausführen des Befehls_ unbedingt klonen. `xdm``sendEvent` Beispiel:

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

In diesem Beispiel wird die Datenschicht geklont, indem sie in JSON serialisiert und anschließend deserialisiert wird. Als Nächstes wird das geklonte Ergebnis an den Befehl `sendEvent` übergeben. Dadurch wird sichergestellt, dass der Befehl `sendEvent` eine Momentaufnahme der Datenschicht enthält, wie sie bei Ausführung des Befehls `sendEvent` existierte, sodass spätere Änderungen am ursprünglichen Datenschichtobjekt nicht in den an den Server gesendeten Daten übernommen werden. Wenn Sie eine Ereignis-basierte Datenschicht verwenden, wird das Klonen der Daten wahrscheinlich bereits automatisch durchgeführt. Wenn Sie beispielsweise die Client-Datenschicht [Adobe](https://github.com/adobe/adobe-client-data-layer/wiki) verwenden, stellt die `getState()`-Methode einen berechneten, geklonten Schnappschuss aller vorherigen Änderungen bereit. Dies wird auch automatisch verarbeitet, wenn Sie die Adobe Experience Platform Web SDK Extension in Adobe Experience Platform Launch verwenden.

>[!NOTE]
>
>Die Daten, die in jedem Ereignis im XDM-Feld gesendet werden können, sind auf 32 KB beschränkt.

### Senden von Nicht-XDM-Daten

Derzeit wird das Senden von Daten, die nicht mit einem XDM-Schema übereinstimmen, nicht unterstützt. Die Unterstützung ist für einen späteren Termin geplant.

### Einstellen von `eventType` {#event-types}

In einem XDM-Erlebnis-Ereignis gibt es ein optionales `eventType`-Feld. Dies enthält den primären Ereignistyp für den Datensatz. Das Festlegen eines Ereignistyps kann Ihnen helfen, zwischen den verschiedenen Ereignissen zu unterscheiden, die Sie senden werden. XDM bietet mehrere vordefinierte Ereignistyp, die Sie verwenden können, oder Sie erstellen Ihre eigenen benutzerdefinierten Ereignistyp für Ihre Anwendungsfälle. Nachfolgend finden Sie eine Liste aller vordefinierten Ereignistyp, die von XDM bereitgestellt werden. [Lesen Sie mehr im öffentlichen XDM-Bericht](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values).


| **Ereignistyp:** | **Definition:** |
| ---------------------------------- | ------------ |
| advertising.completes | Gibt an, ob ein zeitgesteuertes Medienelement bis zum Abschluss angesehen wurde. Dies bedeutet nicht unbedingt, dass der Betrachter das gesamte Video angesehen hat. Der Betrachter hätte vorausspringen können |
| advertising.timePlayed | Beschreibt die Zeitdauer, die ein Benutzer für ein bestimmtes zeitgesteuertes Medienelement verbracht hat |
| advertising.federated | Zeigt an, ob ein Erlebnis-Ereignis über den Datenverband (Datenfreigabe zwischen Kunden) erstellt wurde |
| advertising.clicks | Klickaktionen für eine Werbung |
| advertising.conversions | Vom Kunden vordefinierte Aktionen, die ein Ereignis zur Leistungsbewertung auslösen |
| advertising.firstQuartiles | Eine digitale Videoanzeige hat 25 % ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben |
| advertising.impressions | Impression(en) einer Werbung für einen Endbenutzer mit dem Potenzial, angezeigt zu werden |
| advertising.midpoints | Eine digitale Videoanzeige hat 50% ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben |
| advertising.starts | Die Wiedergabe einer digitalen Videoanzeige hat begonnen |
| advertising.thirdQuartiles | Eine digitale Videoanzeige hat 75% ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben |
| web.webpagedetails.pageViews | Eine Webseite wurde angezeigt |
| web.webinteraction.linkClicks | Ein Weblink wurde geklickt |
| commerce.checkouts | Eine Aktion während eines Checkout-Prozesses einer Produktliste. Es kann mehr als ein Checkout-Ereignis geben, wenn ein Checkout-Prozess mehrere Schritte umfasst. Bei mehreren Schritten werden die Zeitinformationen des Ereignisses und die referenzierte Seite oder das referenzierte Ereignis verwendet, um den Schritt zu identifizieren, den einzelne Ereignisse der Reihe nach darstellen |
| commerce.productListAdds | Aufnahme eines Produkts in die Produktliste. Beispiel: Ein Produkt wird dem Warenkorb hinzugefügt |
| commerce.productListOpens | Initialisierungen einer neuen Produktliste. Beispiel: Ein Warenkorb wird erstellt |
| commerce.productListRemovals | Entfernen eines Produkteintrags aus einer Produktliste. Beispiel: Ein Produkt wird aus dem Warenkorb entfernt |
| commerce.productListReopens | Eine Produktliste, die nicht mehr zugänglich (aufgegeben) war, wurde vom Benutzer erneut aktiviert. Beispielsweise über eine Re-Marketing-Aktivität |
| commerce.productListViews | Eine Produktliste wurde angezeigt |
| commerce.productViews | Ein Produkt wurde angezeigt |
| commerce.purchases | Eine Bestellung wurde angenommen. Der Kauf ist die einzige erforderliche Aktion bei einer Handelskonversion. Für den Kauf muss eine Produktliste angegeben sein |
| commerce.saveForLaters | Die Liste des Produkts wird für die zukünftige Verwendung gespeichert. Beispiel: Eine Produktwunschliste |
| delivery.feedback | Feedback-Ereignis für einen Versand. Beispiel-Feedback-Ereignisse für einen E-Mail-Versand |


Diese Ereignistyp werden in einer Dropdown-Liste angezeigt, wenn Sie die Adobe Experience Platform Launch-Erweiterung verwenden, oder Sie können sie immer ohne Experience Platform Launch weitergeben. Sie können als Teil der `xdm`-Option übergeben werden.


```javascript
alloy("sendEvent", {
  "xdm": {
    "eventType": "commerce.purchases",
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Alternativ hierzu kann `eventType` über die `type`-Option an den Ereignisbefehl übergeben werden. Hinter den Kulissen wird dies den XDM-Daten hinzugefügt. Mit `type` als Option können Sie `eventType` einfacher einstellen, ohne die XDM-Payload zu ändern.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Außerkraftsetzen der DataSet-ID

In einigen Anwendungsfällen möchten Sie möglicherweise ein Ereignis an einen anderen Datensatz als den in der Konfigurationsoberfläche konfigurierten senden. Dazu müssen Sie die Option `datasetId` für den Befehl `sendEvent` festlegen:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Hinzufügen von Identitätsinformationen

Benutzerspezifische Identitätsinformationen können auch dem Ereignis hinzugefügt werden. Siehe [Abrufen der Experience Cloud-ID](../identity/overview.md).

## Verwenden der sendBeacon-API

Es kann schwierig sein, Ereignisdaten zu senden, kurz bevor der Nutzer die Web-Seite verlassen hat. Wenn die Anforderung zu lange dauert, kann der Browser die Anforderung abbrechen. Einige Browser haben eine Web-Standard-API namens `sendBeacon` implementiert, mit der Daten in dieser Zeit leichter erfasst werden können. Bei der Verwendung von `sendBeacon` stellt der Browser die Web-Anforderung im globalen Browser-Kontext dar. Das bedeutet, dass der Browser die Beacon-Anforderung im Hintergrund ausführt und die Seitennavigation nicht beeinträchtigt. Um Adobe Experience Platform [!DNL Web SDK] anzuweisen, `sendBeacon` zu verwenden, fügen Sie die Option `"documentUnloading": true` zum Ereignis-Befehl hinzu.  Siehe folgendes Beispiel:


```javascript
alloy("sendEvent", {
  "documentUnloading": true,
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
});
```

Browser haben Beschränkungen für die Datenmenge, die mit `sendBeacon` gleichzeitig gesendet werden kann. In vielen Browsern beträgt die Beschränkung 64 K. Wenn der Browser das Ereignis ablehnt, weil die Nutzlast zu groß ist, kehrt Adobe Experience Platform [!DNL Web SDK] zurück zu seiner normalen Transportmethode (z. B. fetch).

## Umgang mit Antworten von Ereignissen

Wenn Sie eine Antwort eines Ereignisses bearbeiten möchten, können Sie wie folgt über einen Erfolg oder Fehler benachrichtigt werden:


```javascript
alloy("sendEvent", {
  "renderDecisions": true,
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
}).then(function(results) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## Globale Änderung von Ereignissen {#modifying-events-globally}

Wenn Sie Felder global aus dem Ereignis hinzufügen, entfernen oder ändern möchten, können Sie einen `onBeforeEventSend`-Rückruf konfigurieren.  Dieser Rückruf wird jedes Mal abgerufen, wenn ein Ereignis gesendet wird.  Dieser Rückruf wird an ein Ereignis-Objekt mit einem `xdm`-Feld übergeben.  Ändern Sie `content.xdm`, um die mit dem Ereignis gesendeten Daten zu ändern.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

Die `xdm`-Felder werden in der folgenden Reihenfolge festgelegt:

1. Werte, die als Optionen an den Ereignis-Befehl übergeben werden `alloy("sendEvent", { xdm: ... });`
2. Automatisch erfasste Werte.  (Siehe [Automatische Informationen](../data-collection/automatic-information.md).)
3. Die Änderungen, die im `onBeforeEventSend`-Rückruf vorgenommen wurden.

Einige Hinweise zum Rückruf `onBeforeEventSend`:

* Ereignis XDM kann während des Rückrufs geändert werden. Nachdem der Rückruf zurückgegeben wurde, können alle geänderten Felder und Werte von
die Objekte content.xdm und content.data werden mit dem Ereignis gesendet.

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Wenn der Rückruf eine Ausnahme auslöst, wird die Verarbeitung für das Ereignis abgebrochen und das Ereignis wird nicht gesendet.
* Wenn der Rückruf den booleschen Wert von `false` zurückgibt, wird die Verarbeitung des Ereignisses abgebrochen.
ohne Fehler und das Ereignis wird nicht gesendet. Dieser Mechanismus ermöglicht es, bestimmte Ereignis leicht zu ignorieren durch
Prüfung der Ereignis-Daten und Rückgabe von `false`, wenn das Ereignis nicht gesendet werden sollte.

   >[!NOTE]
   >Es sollte darauf geachtet werden, dass beim ersten Ereignis auf einer Seite kein Fehler zurückgegeben wird. Die Ausgabe von &quot;false&quot;im ersten Ereignis kann sich negativ auf die Personalisierung auswirken.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Jeder andere Rückgabewert als der boolesche `false` ermöglicht es dem Ereignis, nach dem Rückruf zu verarbeiten und zu senden.

* Ereignis können gefiltert werden, indem Sie den Ereignistyp untersuchen (Siehe [Ereignistyp](#event-types).):

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## Potenzielle umsetzbare Fehler

Beim Senden eines Ereignisses wird möglicherweise ein Fehler ausgegeben, wenn die gesendeten Daten zu groß sind (mehr als 32 KB für eine vollständige Anforderung). In diesem Fall müssen Sie die Menge der gesendeten Daten verringern.
