---
title: Seiten- und Linktracking mit Adobe Analytics
seo-title: Linktracking mit Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Linkdaten mit Experience Platform Web SDK an Adobe Analytics senden.
seo-description: Erfahren Sie, wie Sie Linkdaten mit Experience Platform Web SDK an Adobe Analytics senden.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---


# Senden von Daten an Adobe Analytics

Während in der Vergangenheit verschiedene Funktionen existierten, um zwischen einer Ansicht und einem Link zu unterscheiden (z. B. `s.t(), s.tl()`), gibt es im Web SDK nur den `sendEvent` Befehl. Die Daten, die Sie mit einem Ereignis senden, bestimmen, ob es sich um eine Ansicht oder einen Link handeln soll.

## Senden einer Ansicht

Sie können eine Ansicht der Seite festlegen, indem Sie die `web.webPageDetails.pageViews.value=1` Variable festlegen.

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetailsr": {
        "pageViews": {
            "value":1
      }
    }
  }
});
```

Obwohl Analytics eine Seitenvariable technisch aufzeichnet, auch wenn diese nicht eingestellt ist, empfiehlt es sich, diese Ansicht immer dann einzustellen, wenn Sie eine Ansicht aufzeichnen möchten, die in Ihren Daten explizit aufgeführt ist, und um Ihre Implementierung zukunftssicher zu gestalten.

## Tracking-Links

Die Links können durch Hinzufügen der Details unter dem `web.webInteraction` Schema eingestellt werden. Es gibt drei erforderliche Variablen: `web.webInteraction.name`, `web.webInteraction.type` und `web.webInteraction.linkClicks.value`.

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
});
```

Der Linktyp kann einer von drei Werten sein:

* **`other`:** Ein benutzerspezifischer Link
* **`download`:** Link zum Herunterladen (diese können automatisch von der Bibliothek verfolgt werden)
* **`exit`:** Ein Ausstiegslink

### Automatische Linkverfolgung

Das Web SDK kann automatisch alle Link-Klicks verfolgen, indem [clickCollection](../../fundamentals/configuring-the-sdk.md#clickCollectionEnabled)aktiviert wird.

Downloadlinks werden automatisch anhand der gängigen Dateitypen erkannt. Die Logik für die Klassifizierung von Downloads ist konfigurierbar.
