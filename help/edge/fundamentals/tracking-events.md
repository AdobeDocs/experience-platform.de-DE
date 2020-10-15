---
title: Verfolgen von Ereignissen
seo-title: Verfolgen von Adobe Experience Platform Web SDK-Ereignissen
description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignisse verfolgen
seo-description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignisse verfolgen
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 69%

---


# Verfolgen von Ereignissen

Verwenden Sie den `sendEvent`-Befehl, um Ereignisdaten an Adobe Experience Cloud zu senden. Der `sendEvent`-Befehl ist die wichtigste Methode zum Senden von Daten an und zum Abrufen von personalisierten Inhalten, Identitäten und Zielgruppenzielen.[!DNL Experience Cloud]

An Adobe Experience Cloud gesendete Daten gehören zwei Kategorien an:

* XDM-Daten
* Nicht-XDM-Daten (derzeit nicht unterstützt)

## Senden von XDM-Daten

XDM-Daten sind Objekte, deren Inhalt und Struktur mit einem Schema übereinstimmen, das Sie in Adobe Experience Platform erstellt haben. [Erfahren Sie mehr darüber, wie Sie ein Schema erstellen.](../../xdm/tutorials/create-schema-ui.md)

Any XDM data that you would like to be part of your analytics, personalization, audiences, or destinations should be sent using the `xdm` option.


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

>[!NOTE]
>
>Die Daten, die in jedem Ereignis im XDM-Feld gesendet werden können, sind auf 32 KB beschränkt.

### Senden von Nicht-XDM-Daten

Derzeit wird das Senden von Daten, die nicht mit einem XDM-Schema übereinstimmen, nicht unterstützt. Die Unterstützung ist für einen späteren Termin geplant.

### Einstellen von `eventType`

In an XDM experience event, there is an optional `eventType` field. Dies enthält den primären Ereignistyp für den Datensatz. Das Festlegen eines Ereignistyps kann Ihnen helfen, zwischen den verschiedenen Ereignissen zu unterscheiden, die Sie senden werden. XDM bietet mehrere vordefinierte Ereignistyp, die Sie verwenden können, oder Sie erstellen Ihre eigenen benutzerdefinierten Ereignistyp für Ihre Anwendungsfälle. Nachfolgend finden Sie eine Liste aller vordefinierten Ereignistyp, die von XDM bereitgestellt werden. [Mehr darüber im öffentlich-rechtlichen XDM-Bericht](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values)


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


Diese Ereignistyp werden in einer Dropdown-Liste angezeigt, wenn Sie die Adobe Experience Platform Launch-Erweiterung verwenden, oder Sie können sie immer ohne Experience Platform Launch weitergeben. They can be passed in as part of the `xdm` option.


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

In einigen Anwendungsfällen möchten Sie möglicherweise ein Ereignis an einen anderen Datensatz als den in der Konfigurationsoberfläche konfigurierten senden. Dazu müssen Sie die `datasetId` Option auf dem `sendEvent` Befehl festlegen:


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### Hinzufügen von Identitätsinformationen

Benutzerspezifische Identitätsinformationen können auch dem Ereignis hinzugefügt werden. Siehe [Abrufen der Experience Cloud-ID](../identity/overview.md)

## Verwenden der sendBeacon-API

Es kann schwierig sein, Ereignisdaten zu senden, kurz bevor der Nutzer die Web-Seite verlassen hat. Wenn die Anforderung zu lange dauert, kann der Browser die Anforderung abbrechen. Einige Browser haben eine Web-Standard-API namens `sendBeacon` implementiert, mit der Daten in dieser Zeit leichter erfasst werden können. Bei der Verwendung von `sendBeacon` stellt der Browser die Web-Anforderung im globalen Browser-Kontext dar. Das bedeutet, dass der Browser die Beacon-Anforderung im Hintergrund ausführt und die Seitennavigation nicht beeinträchtigt. To tell Adobe Experience Platform [!DNL Web SDK] to use `sendBeacon`, add the option `"documentUnloading": true` to the event command.  Siehe folgendes Beispiel:


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

Browser haben Beschränkungen für die Datenmenge, die mit `sendBeacon` gleichzeitig gesendet werden kann. In vielen Browsern beträgt die Beschränkung 64 K. If the browser rejects the event because the payload is too large, Adobe Experience Platform [!DNL Web SDK] falls back to using its normal transport method (for example, fetch).

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

Wenn Sie Felder global aus dem Ereignis hinzufügen, entfernen oder ändern möchten, können Sie einen `onBeforeEventSend`-Rückruf konfigurieren.  Dieser Rückruf wird jedes Mal abgerufen, wenn ein Ereignis gesendet wird.  Dieser Rückruf wird an ein Ereignis-Objekt mit einem `xdm`-Feld übergeben.  Ändern Sie `event.xdm`, um die im Ereignis gesendeten Daten zu ändern.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(event) {
    // Change existing values
    event.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete event.xdm.web.webReferrer.URL;
    // Or add new values
    event.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

Die `xdm`-Felder werden in der folgenden Reihenfolge festgelegt:

1. Werte, die als Optionen an den Ereignis-Befehl übergeben werden `alloy("sendEvent", { xdm: ... });`
2. Automatisch erfasste Werte.  (Siehe [Automatische Informationen](../data-collection/automatic-information.md).)
3. Die Änderungen, die im `onBeforeEventSend`-Rückruf vorgenommen wurden.

Wenn der `onBeforeEventSend`-Rückruf eine Ausnahme auslöst, wird das Ereignis trotzdem gesendet. jedoch wird keine der im Rückruf vorgenommenen Änderungen auf das endgültige Ereignis angewendet.

## Potenzielle umsetzbare Fehler

Beim Senden eines Ereignisses wird möglicherweise ein Fehler ausgegeben, wenn die gesendeten Daten zu groß sind (mehr als 32 KB für eine vollständige Anforderung). In diesem Fall müssen Sie die Menge der gesendeten Daten verringern.

Wenn Debugging aktiviert ist, validiert der Server synchron die gesendeten Ereignisdaten für das konfigurierte XDM-Schema. Wenn die Daten nicht mit dem Schema übereinstimmen, werden Details zur Nichtübereinstimmung vom Server zurückgegeben und ein Fehler wird ausgegeben. Ändern Sie in diesem Fall die Daten entsprechend dem Schema. Wenn das Debugging nicht aktiviert ist, validiert der Server die Daten asynchron und kein entsprechender Fehler wird ausgegeben.
