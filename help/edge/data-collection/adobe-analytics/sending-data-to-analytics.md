---
title: Seiten- und Linktracking mit Adobe Analytics
seo-title: Linktracking mit Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Linkdaten mit Experience Platform Web SDK an Adobe Analytics senden.
seo-description: Erfahren Sie, wie Sie Linkdaten mit Experience Platform Web SDK an Adobe Analytics senden.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;web Interaction;page views;link tracking;links;track links;clickCollection;click collection;
translation-type: tm+mt
source-git-commit: 9e1ad05285b27a9fc8b56db903609add3fef144e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Daten an Adobe Analytics senden

Während es in der Vergangenheit verschiedene Funktionen gab, um zwischen einer Ansicht und einem Link zu unterscheiden (z. B. `s.t(), s.tl()`), gibt es im Web SDK nur den `sendEvent` Befehl. Die Daten, die Sie mit einem Ereignis senden, bestimmen, ob es sich um eine Ansicht oder einen Link handeln soll. [Weitere Informationen zu Linktracking-Links](../track-links.md)

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

Obwohl Analytics eine Seitenvariable technisch aufzeichnet, auch wenn diese nicht festgelegt ist, empfiehlt es sich, diese Ansicht immer dann einzustellen, wenn Sie eine Seitenvariable aufzeichnen möchten, damit sie in Ihren Daten explizit angegeben ist und in Zukunft Testversand zu Ihrer Implementierung führt.
