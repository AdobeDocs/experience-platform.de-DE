---
title: Verfolgen von Ereignissen mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Adobe Experience Platform Web SDK-Ereignisse verfolgen.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;Send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 3f5f17275e28ba35a302a42d66b151c4234bc79c
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 43%

---

# Verfolgen von Ereignissen

Um Ereignisdaten an Adobe Experience Cloud zu senden, verwenden Sie den Befehl `sendEvent` . Der `sendEvent`-Befehl ist die wichtigste Methode zum Senden von Daten an und zum Abrufen von personalisierten Inhalten, Identitäten und Zielgruppenzielen.[!DNL Experience Cloud]

An Adobe Experience Cloud gesendete Daten gehören zwei Kategorien an:

* XDM-Daten
* Nicht-XDM-Daten (derzeit nicht unterstützt)

## Senden von XDM-Daten

XDM-Daten sind Objekte, deren Inhalt und Struktur mit einem Schema übereinstimmen, das Sie in Adobe Experience Platform erstellt haben. [Erfahren Sie mehr darüber, wie Sie ein Schema erstellen.](../../xdm/tutorials/create-schema-ui.md)

Alle XDM-Daten, die Sie in Ihre Analyse, Personalisierung, Zielgruppen oder Ziele aufnehmen möchten, sollten mit der Option `xdm` gesendet werden.


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

Zwischen der Ausführung des Befehls `sendEvent` und dem Senden der Daten an den Server kann etwas Zeit vergehen (z. B. wenn die Web SDK-Bibliothek nicht vollständig geladen wurde oder die Zustimmung noch nicht eingegangen ist). Wenn Sie einen Teil des `xdm`-Objekts nach dem Ausführen des Befehls `sendEvent` ändern möchten, wird dringend empfohlen, das `xdm`-Objekt _zu klonen, bevor_ den Befehl `sendEvent` ausgeführt wird. Beispiel:

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

In diesem Beispiel wird die Datenschicht geklont, indem sie in JSON serialisiert und dann deserialisiert wird. Als Nächstes wird das geklonte Ergebnis an den Befehl `sendEvent` übergeben. Dadurch wird sichergestellt, dass der Befehl `sendEvent` einen Schnappschuss der Datenschicht enthält, wie er beim Ausführen des Befehls `sendEvent` vorhanden war, sodass spätere Änderungen am ursprünglichen Datenschichtobjekt nicht in den an den Server gesendeten Daten übernommen werden. Wenn Sie eine ereignisbasierte Datenschicht verwenden, wird das Klonen Ihrer Daten wahrscheinlich bereits automatisch durchgeführt. Wenn Sie beispielsweise die [Adobe Client-Datenschicht](https://github.com/adobe/adobe-client-data-layer/wiki) verwenden, stellt die `getState()`-Methode einen berechneten, geklonten Schnappschuss aller vorherigen Änderungen bereit. Dies wird auch automatisch für Sie verarbeitet, wenn Sie die Adobe Experience Platform Web SDK-Erweiterung in Adobe Experience Platform Launch verwenden.

>[!NOTE]
>
>Die Daten, die in jedem Ereignis im XDM-Feld gesendet werden können, sind auf 32 KB begrenzt.


### Senden von Nicht-XDM-Daten

Daten, die nicht mit einem XDM-Schema übereinstimmen, sollten mit der `data`-Option des Befehls `sendEvent` gesendet werden. Diese Funktion wird in den Versionen 2.5.0 und höher des Web SDK unterstützt.

Dies ist nützlich, wenn Sie ein Adobe Target-Profil aktualisieren oder Target Recommendations-Attribute senden müssen. [Weitere Informationen zu diesen Target-Funktionen.](../personalization/adobe-target/target-overview.md#single-profile-update)

Zukünftig können Sie Ihre gesamte Datenschicht unter der Option `data` senden und sie serverseitig XDM zuordnen.

**So senden Sie Profil- und Recommendations-Attribute an Adobe Target:**

```
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```


### Einstellung `eventType` {#event-types}

In einem XDM-Erlebnisereignis gibt es ein optionales Feld `eventType` . Dies enthält den primären Ereignistyp für den Datensatz. Die Festlegung eines Ereignistyps kann Ihnen dabei helfen, zwischen den verschiedenen Ereignissen zu unterscheiden, die Sie senden werden. XDM bietet verschiedene vordefinierte Ereignistypen, die Sie verwenden können oder Sie immer eigene benutzerdefinierte Ereignistypen für Ihre Anwendungsfälle erstellen. Nachfolgend finden Sie eine Liste aller vordefinierten Ereignistypen, die von XDM bereitgestellt werden. [Weitere Informationen finden Sie im öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values).


| **Ereignistyp:** | **Definition:** |
| ---------------------------------- | ------------ |
| advertising.completes | Gibt an, ob ein zeitgesteuertes Medienelement bis zum Abschluss angesehen wurde. Dies bedeutet nicht unbedingt, dass der Betrachter das gesamte Video angesehen hat. Der Betrachter hätte vorausspringen können |
| advertising.timePlayed | Beschreibt die Zeit, die ein Benutzer mit einem bestimmten zeitgesteuerten Medien-Asset verbringt |
| advertising.federated | Gibt an, ob ein Erlebnisereignis über eine Datenverknüpfung (Datenfreigabe zwischen Kunden) erstellt wurde |
| advertising.clicks | Klickaktionen für eine Anzeige |
| advertising.conversions | Vom Kunden vordefinierte Aktionen, die ein Ereignis zur Leistungsbewertung auslösen |
| advertising.firstQuartiles | Eine digitale Videoanzeige hat 25 % ihrer Laufzeit mit normaler Geschwindigkeit wiedergegeben |
| advertising.impressions | Impression(en) einer Anzeige für einen Endbenutzer mit dem Potenzial, angezeigt zu werden |
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
| delivery.feedback | Feedback-Ereignisse für einen Versand. Beispiel-Feedback-Ereignisse für einen E-Mail-Versand |


Diese Ereignistypen werden in einer Dropdown-Liste angezeigt, wenn Sie die Adobe Experience Platform Launch-Erweiterung verwenden oder Sie können sie immer ohne Experience Platform Launch übergeben. Sie können als Teil der `xdm`-Option übergeben werden.


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

### Überschreiben der Datensatz-ID

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

Benutzerdefinierte Identitätsinformationen können auch zum Ereignis hinzugefügt werden. Siehe [Abrufen der Experience Cloud-ID](../identity/overview.md).

## Verwenden der sendBeacon-API

Es kann schwierig sein, Ereignisdaten zu senden, kurz bevor der Nutzer die Web-Seite verlassen hat. Wenn die Anforderung zu lange dauert, kann der Browser die Anforderung abbrechen. Einige Browser haben eine Web-Standard-API namens `sendBeacon` implementiert, mit der Daten in dieser Zeit leichter erfasst werden können. Bei der Verwendung von `sendBeacon` stellt der Browser die Web-Anforderung im globalen Browser-Kontext dar. Das bedeutet, dass der Browser die Beacon-Anforderung im Hintergrund ausführt und die Seitennavigation nicht beeinträchtigt. Um Adobe Experience Platform [!DNL Web SDK] anzuweisen, `sendBeacon` zu verwenden, fügen Sie die Option `"documentUnloading": true` zum Ereignisbefehl hinzu.  Siehe folgendes Beispiel:


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

Browser haben Beschränkungen für die Datenmenge, die mit `sendBeacon` gleichzeitig gesendet werden kann. In vielen Browsern beträgt die Beschränkung 64 K. Wenn der Browser das Ereignis ablehnt, weil die Payload zu groß ist, verwendet Adobe Experience Platform [!DNL Web SDK] wieder die normale Transportmethode (z. B. Abruf).

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

Wenn Sie Felder global aus dem Ereignis hinzufügen, entfernen oder ändern möchten, können Sie einen `onBeforeEventSend`-Rückruf konfigurieren.  Dieser Rückruf wird jedes Mal abgerufen, wenn ein Ereignis gesendet wird.  Dieser Rückruf wird an ein Ereignis-Objekt mit einem `xdm`-Feld übergeben.  Ändern Sie `content.xdm` , um die mit dem Ereignis gesendeten Daten zu ändern.


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

* Ereignis-XDM kann während des Rückrufs geändert werden. Nachdem der Rückruf zurückgegeben wurde, werden alle geänderten Felder und Werte von
die Objekte content.xdm und content.data werden mit dem Ereignis gesendet.

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Wenn der Rückruf eine Ausnahme auslöst, wird die Verarbeitung für das Ereignis beendet und das Ereignis wird nicht gesendet.
* Wenn der Rückruf den booleschen Wert von `false` zurückgibt, wird die Ereignisverarbeitung beendet.
ohne Fehler und das Ereignis nicht gesendet wird. Dieser Mechanismus ermöglicht es, dass bestimmte Ereignisse von
Prüfung der Ereignisdaten und Rückgabe von `false` , wenn das Ereignis nicht gesendet werden soll.

   >[!NOTE]
   >Es sollte darauf geachtet werden, dass beim ersten Ereignis auf einer Seite nicht &quot;false&quot;zurückgegeben wird. Die Rückgabe von &quot;false&quot;beim ersten Ereignis kann sich negativ auf die Personalisierung auswirken.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

Jeder andere Rückgabewert als der boolesche Wert `false` ermöglicht die Verarbeitung und den Versand des Ereignisses nach dem Rückruf.

* Ereignisse können gefiltert werden, indem der Ereignistyp geprüft wird (siehe [Ereignistypen](#event-types)):

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
