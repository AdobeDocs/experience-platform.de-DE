---
title: Verfolgen von Ereignissen
seo-title: Verfolgen von Adobe Experience Platform Web SDK-Ereignissen
description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignisse verfolgen
seo-description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignisse verfolgen
translation-type: tm+mt
source-git-commit: c49ac064d310fbe12e19d58b80c2267a35d585e8

---


# Verfolgen von Ereignissen

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Nutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Verwenden Sie den `event`-Befehl, um Ereignisdaten an Adobe Experience Cloud zu senden. Der `event`-Befehl ist die wichtigste Methode zum Senden von Daten an Experience Cloud und zum Abrufen von personalisierten Inhalten, Identitäten und Zielgruppenzielen.

An Adobe Experience Cloud gesendete Daten gehören zwei Kategorien an:

* XDM-Daten
* Nicht-XDM-Daten (derzeit nicht unterstützt)

## Senden von XDM-Daten

XDM-Daten sind Objekte, deren Inhalt und Struktur mit einem Schema übereinstimmen, das Sie in Adobe Experience Platform erstellt haben. [Erfahren Sie mehr darüber, wie Sie ein Schema erstellen.](../../xdm/tutorials/create-schema-ui.md)

Alle XDM-Daten, die Sie als Teil Ihrer Analyse, Personalisierung, Zielgruppen oder Ziele verwenden möchten, sollten mit der `xdm`-Option gesendet werden.

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
});
```

>[!NOTE]
>Die Daten, die in jedem Ereignis im XDM-Feld gesendet werden können, sind auf 32 KB beschränkt.

### Senden von Nicht-XDM-Daten

Derzeit wird das Senden von Daten, die nicht mit einem XDM-Schema übereinstimmen, nicht unterstützt. Die Unterstützung ist für einen späteren Termin geplant.

### Einstellen von `eventType`

In einem XDM-Erlebnis-Ereignis gibt es ein `eventType`-Feld. Dies enthält den primären Ereignistyp für den Datensatz. Dies kann als Teil der `xdm`-Option übergeben werden.

```javascript
alloy("event", {
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

alloy("event", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

## Verwenden der sendBeacon-API

Es kann schwierig sein, Ereignisdaten zu senden, kurz bevor der Nutzer die Web-Seite verlassen hat. Wenn die Anforderung zu lange dauert, kann der Browser die Anforderung abbrechen. Einige Browser haben eine Web-Standard-API namens `sendBeacon` implementiert, mit der Daten in dieser Zeit leichter erfasst werden können. Bei der Verwendung von `sendBeacon` stellt der Browser die Web-Anforderung im globalen Browser-Kontext dar. Das bedeutet, dass der Browser die Beacon-Anforderung im Hintergrund ausführt und die Seitennavigation nicht beeinträchtigt. Damit das Adobe Experience Platform Web SDK `sendBeacon` verwendet, fügen Sie die Option `"documentUnloading": true` zum Ereignis-Befehl hinzu.  Siehe folgendes Beispiel:

```javascript
alloy("event", {
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

Browser haben Beschränkungen für die Datenmenge, die mit `sendBeacon` gleichzeitig gesendet werden kann. In vielen Browsern beträgt die Beschränkung 64 K. Wenn der Browser das Ereignis ablehnt, weil die Payload zu groß ist, verwendet das Adobe Experience Platform Web SDK wieder die normale Übertragungsmethode (z. B. Abrufen).

## Umgang mit Antworten von Ereignissen

Wenn Sie eine Antwort eines Ereignisses bearbeiten möchten, können Sie wie folgt über einen Erfolg oder Fehler benachrichtigt werden:

```javascript
alloy("event", {
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
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
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

1. Werte, die als Optionen an den Ereignis-Befehl übergeben werden `alloy("event", { xdm: ... });`
2. Automatisch erfasste Werte.  (Siehe [Automatische Informationen](../reference/automatic-information.md).)
3. Die Änderungen, die im `onBeforeEventSend`-Rückruf vorgenommen wurden.

Wenn der `onBeforeEventSend`-Rückruf eine Ausnahme auslöst, wird das Ereignis trotzdem gesendet. jedoch wird keine der im Rückruf vorgenommenen Änderungen auf das endgültige Ereignis angewendet.

## Potenzielle umsetzbare Fehler

Beim Senden eines Ereignisses wird möglicherweise ein Fehler ausgegeben, wenn die gesendeten Daten zu groß sind (mehr als 32 KB für eine vollständige Anforderung). In diesem Fall müssen Sie die Menge der gesendeten Daten verringern.

Wenn Debugging aktiviert ist, validiert der Server synchron die gesendeten Ereignisdaten für das konfigurierte XDM-Schema. Wenn die Daten nicht mit dem Schema übereinstimmen, werden Details zur Nichtübereinstimmung vom Server zurückgegeben und ein Fehler wird ausgegeben. Ändern Sie in diesem Fall die Daten entsprechend dem Schema. Wenn das Debugging nicht aktiviert ist, validiert der Server die Daten asynchron und kein entsprechender Fehler wird ausgegeben.
