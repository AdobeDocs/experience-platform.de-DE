---
title: Seiten- und Linktracking mit Adobe Analytics
seo-title: Linktracking mit Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Linkdaten mit Experience Platform Web SDK an Adobe Analytics senden.
seo-description: Erfahren Sie, wie Sie Linkdaten mit Experience Platform Web SDK an Adobe Analytics senden.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: c6b572f8757e46ccb22ccea326a7537747f81893
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 4%

---


# Senden von Daten an Adobe Analytics

Während in der Vergangenheit verschiedene Funktionen existierten, um zwischen einer Ansicht und einem Link zu unterscheiden (z. B. `s.t(), s.tl()`), gibt es im Web SDK nur den `sendEvent` Befehl. Die Daten, die Sie mit einem Ereignis senden, bestimmen, ob es sich um eine Ansicht oder einen Link handeln soll.

## Senden einer Ansicht

Sie können eine Ansicht der Seite festlegen, indem Sie die `web.webPageDetails.pageViews.value=1` Variable festlegen.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        "pageViews": {
            "value":1
         }
      }
    }
  }
});
```

Obwohl Analytics eine Seitenvariable technisch aufzeichnet, auch wenn diese nicht eingestellt ist, empfiehlt es sich, diese Ansicht immer dann einzustellen, wenn Sie eine Ansicht aufzeichnen möchten, die in Ihren Daten explizit aufgeführt ist, und um Ihre Implementierung zukunftssicher zu gestalten.

## Tracking-Links

Links können manuell eingestellt oder [automatisch](#automaticLinkTracking)verfolgt werden. Die manuelle Verfolgung erfolgt durch Hinzufügen der Details unter dem `web.webInteraction` Schema. Es gibt drei erforderliche Variablen: `web.webInteraction.name`, `web.webInteraction.type` und `web.webInteraction.linkClicks.value`.

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

* **`other`:** Ein benutzerspezifischer Link
* **`download`:** Link zum Herunterladen
* **`exit`:** Ein Ausstiegslink

### Automatische Linkverfolgung {#automaticLinkTracking}

Standardmäßig erfasst das Web SDK [Beschriftungen](#labelingLinks)und [zeichnet](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) Klicks auf [qualifizierte](#qualifyingLinks) Link-Tags auf. Klicks werden mit einem [Capture](https://www.w3.org/TR/uievents/#capture-phase) Click-Ereignis-Listener erfasst, der mit dem Dokument verbunden ist.

Die Deaktivierung der automatischen Linktracking kann durch die [Konfiguration](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) des Web SDK erfolgen.

```javascript
clickCollectionEnabled: false
```

#### Welche Tags sind für die Linktracking geeignet?{#qualifyingLinks}

Die automatische Linkverfolgung erfolgt für Anker- `A` und `AREA` -Tags. Diese Tags werden jedoch nicht für die Linktracking berücksichtigt, wenn sie über einen angehängten `onclick` Handler verfügen.

#### Wie werden Links beschriftet?{#labelingLinks}

Links werden als Downloadlink bezeichnet, wenn das Anker-Tag ein Downloadattribut enthält oder wenn der Link mit einer beliebten Dateierweiterung endet. Der Qualifikator für Downloadlinks kann mit einem regulären Ausdruck [konfiguriert](../../fundamentals/configuring-the-sdk.md) werden:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Links werden als Ausstiegslink bezeichnet, wenn sich die Domäne der Zielgruppe des Links von der aktuellen Domäne unterscheidet `window.location.hostname`.

Links, die sich nicht als Download- oder Exitlink qualifizieren, werden als &quot;sonstige&quot;bezeichnet.
