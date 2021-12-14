---
title: Verfolgen von Ereignissen mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Adobe Experience Platform Web SDK-Ereignisse verfolgen.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;Send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 32%

---

# Verfolgen von Ereignissen

Um Ereignisdaten an Adobe Experience Cloud zu senden, verwenden Sie die `sendEvent` Befehl. Der `sendEvent`-Befehl ist die wichtigste Methode zum Senden von Daten an und zum Abrufen von personalisierten Inhalten, Identitäten und Zielgruppenzielen.[!DNL Experience Cloud]

An Adobe Experience Cloud gesendete Daten gehören zwei Kategorien an:

* XDM-Daten
* Nicht-XDM-Daten

## Senden von XDM-Daten

XDM-Daten sind Objekte, deren Inhalt und Struktur mit einem Schema übereinstimmen, das Sie in Adobe Experience Platform erstellt haben. [Erfahren Sie mehr darüber, wie Sie ein Schema erstellen.](../../xdm/tutorials/create-schema-ui.md)

Alle XDM-Daten, die Sie als Teil Ihrer Analyse, Personalisierung, Zielgruppen oder Ziele verwenden möchten, sollten mit der `xdm` -Option.


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

Es kann einige Zeit vergehen, zwischen denen `sendEvent` ausgeführt wird und wenn die Daten an den Server gesendet werden (z. B. wenn die Web SDK-Bibliothek nicht vollständig geladen wurde oder die Zustimmung noch nicht eingegangen ist). Wenn Sie einen Teil der `xdm` -Objekt nach dem Ausführen der `sendEvent` -Befehl verwenden, wird dringend empfohlen, die `xdm` Objekt _before_ Ausführung der `sendEvent` Befehl. Beispiel:

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

In diesem Beispiel wird die Datenschicht geklont, indem sie in JSON serialisiert und dann deserialisiert wird. Als Nächstes wird das geklonte Ergebnis an die `sendEvent` Befehl. Dadurch wird sichergestellt, dass die `sendEvent` -Befehl hat einen Schnappschuss der Datenschicht, wie er beim `sendEvent` wurde ausgeführt, sodass spätere Änderungen am ursprünglichen Datenschichtobjekt nicht in den an den Server gesendeten Daten übernommen werden. Wenn Sie eine ereignisbasierte Datenschicht verwenden, wird das Klonen Ihrer Daten wahrscheinlich bereits automatisch durchgeführt. Wenn Sie beispielsweise die [Adobe Client-Datenschicht](https://github.com/adobe/adobe-client-data-layer/wiki), die `getState()` -Methode liefert eine berechnete, geklonte Momentaufnahme aller vorherigen Änderungen. Dies wird auch automatisch für Sie verarbeitet, wenn Sie die Adobe Experience Platform Web SDK-Tag-Erweiterung verwenden.

>[!NOTE]
>
>Die Daten, die in jedem Ereignis im XDM-Feld gesendet werden können, sind auf 32 KB begrenzt.


## Senden von Nicht-XDM-Daten

Daten, die nicht mit einem XDM-Schema übereinstimmen, sollten mit der `data` der `sendEvent` Befehl. Diese Funktion wird in den Versionen 2.5.0 und höher des Web SDK unterstützt.

Dies ist nützlich, wenn Sie ein Adobe Target-Profil aktualisieren oder Target Recommendations-Attribute senden müssen. [Weitere Informationen zu diesen Target-Funktionen.](../personalization/adobe-target/target-overview.md#single-profile-update)

Zukünftig können Sie Ihre gesamte Datenschicht unter der `data` und ordnen Sie sie serverseitig XDM zu.

**So senden Sie Profil- und Recommendations-Attribute an Adobe Target:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### Einstellen von `eventType` {#event-types}

In XDM ExperienceEvent-Schemata gibt es eine optionale `eventType` -Feld. Dies enthält den primären Ereignistyp für den Datensatz. Die Festlegung eines Ereignistyps kann Ihnen dabei helfen, zwischen den verschiedenen Ereignissen zu unterscheiden, die Sie senden werden. XDM bietet verschiedene vordefinierte Ereignistypen, die Sie verwenden können oder Sie immer eigene benutzerdefinierte Ereignistypen für Ihre Anwendungsfälle erstellen. Eine finden Sie in der XDM-Dokumentation . [Liste aller vordefinierten Ereignistypen](../../xdm/classes/experienceevent.md#eventType).

Diese Ereignistypen werden in einer Dropdown-Liste angezeigt, wenn Sie die Tag-Erweiterung verwenden oder sie immer ohne Tags übergeben können. Sie können als Teil der `xdm` -Option.


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

In einigen Anwendungsfällen möchten Sie möglicherweise ein Ereignis an einen anderen Datensatz als den in der Konfigurationsoberfläche konfigurierten senden. Dazu müssen Sie die `datasetId` -Option auf `sendEvent` command:


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

Es kann schwierig sein, Ereignisdaten zu senden, kurz bevor der Nutzer die Web-Seite verlassen hat. Wenn die Anforderung zu lange dauert, kann der Browser die Anforderung abbrechen. Einige Browser haben eine Web-Standard-API namens `sendBeacon` implementiert, mit der Daten in dieser Zeit leichter erfasst werden können. Bei der Verwendung von `sendBeacon` stellt der Browser die Web-Anforderung im globalen Browser-Kontext dar. Das bedeutet, dass der Browser die Beacon-Anforderung im Hintergrund ausführt und die Seitennavigation nicht beeinträchtigt. Informationen zu Adobe Experience Platform [!DNL Web SDK] zur Verwendung `sendBeacon`, die Option `"documentUnloading": true` zum Ereignisbefehl.  Siehe folgendes Beispiel:


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

Browser haben Beschränkungen für die Datenmenge, die mit `sendBeacon` gleichzeitig gesendet werden kann. In vielen Browsern beträgt die Beschränkung 64 K. Wenn der Browser das Ereignis ablehnt, weil die Payload zu groß ist, wird Adobe Experience Platform [!DNL Web SDK] zurück zu seiner normalen Transportmethode (z. B. Abruf).

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
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### Die `result` Objekt

Die `sendEvent` gibt einen Promise zurück, der mit einer `result` -Objekt. Die `result` -Objekt enthält die folgenden Eigenschaften:

**Vorschläge**: Die Personalisierung bietet , für die sich der Besucher qualifiziert hat. [Erfahren Sie mehr über Vorschläge.](../personalization/rendering-personalization-content.md#manually-rendering-content)

**Entscheidungen**: Diese Eigenschaft wird nicht mehr unterstützt. Verwenden Sie stattdessen `propositions`.

**Ziele**: Segmente aus Adobe Experience Platform, die für externe Personalisierungsplattformen, Content-Management-Systeme, Anzeigen-Server und andere Anwendungen freigegeben werden können, die auf Kunden-Websites ausgeführt werden. [Erfahren Sie mehr über Ziele.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` ist derzeit als Betaversion verfügbar. Dokumentation und Funktionalität können sich ändern.

**Rückschlüsse**: Einblicke in maschinelles Lernen in Echtzeit. [Erfahren Sie mehr über maschinelles Lernen in Echtzeit.](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/real-time-machine-learning/home.html?lang=en)

>[!WARNING]
>
>`inferences` ist derzeit als Betaversion verfügbar. Dokumentation und Funktionalität können sich ändern.



## Globale Änderung von Ereignissen {#modifying-events-globally}

Wenn Sie Felder global aus dem Ereignis hinzufügen, entfernen oder ändern möchten, können Sie einen `onBeforeEventSend`-Rückruf konfigurieren.  Dieser Rückruf wird jedes Mal abgerufen, wenn ein Ereignis gesendet wird.  Dieser Rückruf wird an ein Ereignis-Objekt mit einem `xdm`-Feld übergeben.  Ändern `content.xdm` , um die mit dem Ereignis gesendeten Daten zu ändern.


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

Einige Hinweise zu `onBeforeEventSend` callback:

* Ereignis-XDM kann während des Rückrufs geändert werden. Nachdem der Rückruf zurückgegeben wurde, werden alle geänderten Felder und Werte der Objekte content.xdm und content.data mit dem Ereignis gesendet.

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* Wenn der Rückruf eine Ausnahme auslöst, wird die Verarbeitung für das Ereignis beendet und das Ereignis wird nicht gesendet.
* Wenn der Rückruf den booleschen Wert von `false`, wird die Ereignisverarbeitung ohne Fehler beendet und das Ereignis wird nicht gesendet. Dieser Mechanismus ermöglicht es, bestimmte Ereignisse einfach zu ignorieren, indem die Ereignisdaten geprüft und `false` , wenn das Ereignis nicht gesendet werden soll.

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

Beliebiger Rückgabewert außer dem booleschen Wert `false` ermöglicht die Verarbeitung und den Versand des Ereignisses nach dem Rückruf.

* Ereignisse können durch Untersuchung des Ereignistyps gefiltert werden (siehe [Ereignistypen](#event-types).):

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
