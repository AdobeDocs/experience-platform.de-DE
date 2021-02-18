---
title: Links mit dem Adobe Experience Platform Web SDK verfolgen
description: Erfahren Sie, wie Sie Linkdaten mit Experience Platform Web SDK an Adobe Analytics senden.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;page-Ansichten;Link-Verfolgung;Links;track-Links;clickCollection;click-Auflistung;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# Links verfolgen

Links können manuell eingestellt oder nachverfolgt werden [automatisch](#automaticLinkTracking). Die manuelle Verfolgung erfolgt durch Hinzufügen der Details im Bereich `web.webInteraction` des Schemas. Es gibt drei erforderliche Variablen:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value":1
      },
      "name":"My Custom Link", //Name that shows up in the custom links report
      "URL":"https://myurl.com", //the URL of the link
      "type":"other", // values: other, download, exit
      }
    }
  }
});
```

Der Linktyp kann einer von drei Werten sein:

* **`other`:** Benutzerspezifischer Link
* **`download`:** Download-Link
* **`exit`:** Ein Ausstiegslink

## Automatische Linktracking {#automaticLinkTracking}

Standardmäßig erfasst, kennzeichnet und zeichnet das Web SDK Klicks auf geeignete Link-Tags auf. Klicks werden mit einem [Capture](https://www.w3.org/TR/uievents/#capture-phase) click-Ereignis-Listener erfasst, der an das Dokument angehängt wird.

Die automatische Linktracking kann durch [Konfigurieren](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) des Web SDK deaktiviert werden.

```javascript
clickCollectionEnabled: false
```

### Welche Tags eignen sich für die Linktracking?{#qualifyingLinks}

Die automatische Linkverfolgung erfolgt für die Tags `A` und `AREA`. Diese Tags werden jedoch nicht für die Linktracking berücksichtigt, wenn sie einen `onclick`-Handler haben.

### Wie werden Links beschriftet?{#labelingLinks}

Links werden als Downloadlink bezeichnet, wenn das Anker-Tag ein Downloadattribut enthält oder wenn der Link mit einer beliebten Dateierweiterung endet. Der Qualifikator für den Download-Link kann [konfiguriert](../fundamentals/configuring-the-sdk.md) mit einem regulären Ausdruck sein:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Links werden als Ausstiegslink bezeichnet, wenn die Domäne der Link-Zielgruppe von der aktuellen `window.location.hostname` abweicht.

Links, die sich nicht als Download- oder Exitlink qualifizieren, werden als &quot;sonstige&quot;bezeichnet.
