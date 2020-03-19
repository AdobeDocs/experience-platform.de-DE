---
title: Ereignisse verfolgen
seo-title: Verfolgen von Adobe Experience Platform Web SDK-Ereignissen
description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignis verfolgen können
seo-description: Erfahren Sie, wie Sie Experience Platform Web SDK-Ereignis verfolgen können
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# Ereignisse verfolgen

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Verwenden Sie den `event` Befehl, um Ereignis-Daten an die Adobe Experience Cloud zu senden. Der `event` Befehl ist die wichtigste Methode zum Senden von Daten an die Experience Cloud und zum Abrufen personalisierter Inhalte, Identitäten und Audiencen-Ziele.

An Adobe Experience Cloud gesendete Daten sind in zwei Kategorien unterteilt:

* XDM-Daten
* Nicht-XDM-Daten (derzeit nicht unterstützt)

## Senden von XDM-Daten

XDM-Daten sind Objekte, deren Inhalt und Struktur mit einem Schema übereinstimmen, das Sie in Adobe Experience Platform erstellt haben. [Erfahren Sie mehr darüber, wie Sie ein Schema erstellen.](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md)

Alle XDM-Daten, die Sie als Teil Ihrer Analyse, Personalisierung, Audiencen oder Ziele verwenden möchten, sollten mit der `xdm` Option gesendet werden.

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

### Senden von Nicht-XDM-Daten

Derzeit wird das Senden von Daten, die nicht mit einem XDM-Schema übereinstimmen, nicht unterstützt. Die Unterstützung ist für einen späteren Termin geplant.

### Wenn `eventType`

In einem XDM-Erlebnis-Ereignis gibt es ein `eventType` Feld. Dies hält den primären Ereignistyp für den Datensatz. Dies kann als Teil der `xdm` Option weitergegeben werden.

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

Alternativ `eventType` kann der Befehl &quot;Ereignis&quot;mit der `type` Option übergeben werden. Hinter den Kulissen wird dies den XDM-Daten hinzugefügt. Mit der Option `type` als Option können Sie einfacher einstellen, `eventType` ohne die XDM-Nutzlast zu ändern.

```javascript
var myXDMData = { ... };

alloy("event", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### Starten einer Ansicht

Wenn eine Ansicht gestartet wurde, ist es wichtig, das SDK zu benachrichtigen, indem Sie `viewStart` auf `true` den `event` Befehl einstellen. Dies deutet unter anderem darauf hin, dass das SDK personalisierte Inhalte abrufen und rendern sollte. Auch wenn Sie derzeit keine Personalisierung verwenden, wird die Aktivierung der Personalisierung oder anderer Funktionen später erheblich vereinfacht, da Sie den Code auf der Seite nicht ändern müssen. Darüber hinaus ist die Verfolgung von Ansichten nützlich, wenn Analyseberichte nach der Datenerfassung angezeigt werden.

Die Definition einer Ansicht kann vom Kontext abhängen.

* Auf einer regulären Website wird jede Webseite in der Regel als individuelle Ansicht betrachtet. In diesem Fall sollte ein Ereignis mit der `viewStart` Einstellung `true` so bald wie möglich am Seitenanfang ausgeführt werden.
* In einer Einzelseitenanwendung \(SPA\) ist eine Ansicht weniger definiert. Dies bedeutet in der Regel, dass der Benutzer innerhalb der Anwendung navigiert hat und der Großteil des Inhalts geändert wurde. Für diejenigen, die mit den technischen Grundlagen von Einzelseitenanwendungen vertraut sind, ist dies normalerweise der Fall, wenn die Anwendung eine neue Route lädt. Wenn ein Benutzer zu einer neuen Ansicht wechselt, unabhängig davon, ob Sie eine _Ansicht_ definieren, sollte ein Ereignis mit der `viewStart` Einstellung &quot; `true` &quot;ausgeführt werden.

Das auf `viewStart` &quot; `true` ist&quot;eingestellte Ereignis ist der Hauptmechanismus zum Senden von Daten an die Adobe Experience Cloud und zum Anfordern von Inhalten aus der Adobe Experience Cloud. So wird eine Ansicht Beginn:

```javascript
alloy("event", {
  "viewStart": true,
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

Nach dem Senden der Daten reagiert der Server unter anderem mit personalisierten Inhalten. Dieser personalisierte Inhalt wird automatisch in Ihre Ansicht gerendert. Link-Handler werden auch automatisch an den Inhalt der neuen Ansicht angehängt.

## Verwenden der sendBeacon-API

Es kann schwierig sein, Ereignis-Daten zu senden, bevor der Benutzer die Webseite verlassen hat. Wenn die Anforderung zu lange dauert, kann der Browser die Anforderung abbrechen. Einige Browser haben eine Web-Standard-API implementiert, `sendBeacon` mit der Daten in dieser Zeit leichter erfasst werden können. Bei der Verwendung `sendBeacon`stellt der Browser die Webanforderung im globalen Browserkontext dar. Das bedeutet, dass der Browser die Beacon-Anforderung im Hintergrund ausführt und die Seitennavigation nicht beeinträchtigt. Um Adobe Experience Platform Web SDK zu verwenden, `sendBeacon`fügen Sie die Option `"documentUnloading": true` zum Ereignis-Befehl hinzu.  Siehe folgendes Beispiel:

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

Browser haben Beschränkungen für die Datenmenge festgelegt, mit der gleichzeitig Daten gesendet werden können `sendBeacon` . In vielen Browsern beträgt die Beschränkung 64K. Wenn der Browser das Ereignis ablehnt, weil die Nutzlast zu groß ist, verwendet das Adobe Experience Platform Web SDK wieder die normale Übertragungsmethode (z. B. Abrufen).

## Umgang mit Antworten von Ereignissen

Wenn Sie eine Antwort eines Ereignisses bearbeiten möchten, können Sie wie folgt über einen Erfolg oder Fehler benachrichtigt werden:

```javascript
alloy("event", {
  "viewStart": true,
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
}).then(function() {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## Globale Änderung von Ereignissen {#modifying-events-globally}

Wenn Sie Felder global aus dem Ereignis hinzufügen, entfernen oder ändern möchten, können Sie einen `onBeforeEventSend` Rückruf konfigurieren.  Dieser Rückruf wird jedes Mal aufgerufen, wenn ein Ereignis gesendet wird.  Dieser Rückruf wird an ein Ereignis-Objekt mit einem `xdm` Feld übergeben.  Ändern Sie `event.xdm` die Daten, die im Ereignis gesendet werden.

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

`xdm` Die Felder werden in der folgenden Reihenfolge festgelegt:

1. Werte, die als Optionen an den Ereignis-Befehl übergeben werden `alloy("event", { xdm: ... });`
2. Automatisch erfasste Werte.  (Siehe [Automatische Informationen](../reference/automatic-information.md).)
3. Die Änderungen, die im `onBeforeEventSend` Rückruf vorgenommen wurden.

Wenn der `onBeforeEventSend` Rückruf eine Ausnahme auslöst, wird das Ereignis trotzdem gesendet. jedoch werden keine der im Rückruf vorgenommenen Änderungen auf das endgültige Ereignis angewendet.

## Potenzielle umsetzbare Fehler

Beim Senden eines Ereignisses wird möglicherweise ein Fehler ausgegeben, wenn die gesendeten Daten zu groß sind (mehr als 32 KB für die vollständige Anforderung). In diesem Fall müssen Sie die Menge der gesendeten Daten verringern.

Wenn das Debugging aktiviert ist, validiert der Server synchron die gesendeten Ereignis-Daten für das konfigurierte XDM-Schema. Wenn die Daten nicht mit dem Schema übereinstimmen, werden Details zur Nichtübereinstimmung vom Server zurückgegeben und es wird ein Fehler ausgegeben. Ändern Sie in diesem Fall die Daten entsprechend dem Schema. Wenn das Debugging nicht aktiviert ist, validiert der Server die Daten asynchron und es wird daher kein entsprechender Fehler ausgegeben.
