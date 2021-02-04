---
title: Seiten- und Linktracking mit Adobe Analytics
seo-title: Linktracking mit Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Linkdaten mit Experience Platform Web SDK an Adobe Analytics senden.
seo-description: Erfahren Sie, wie Sie Linkdaten mit Experience Platform Web SDK an Adobe Analytics senden.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;page-Ansichten;Link-Verfolgung;Links;track-Links;clickCollection;click-Auflistung;
translation-type: tm+mt
source-git-commit: c9d777f4350f0b039608c4f9b01d5206994e2572
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Daten an Adobe Analytics senden

Während in der Vergangenheit verschiedene Funktionen zur Unterscheidung zwischen einer Ansicht und einem Link (z. B. `s.t(), s.tl()`) vorhanden waren, gibt es im Web SDK nur den Befehl `sendEvent`. Die Daten, die Sie mit einem Ereignis senden, bestimmen, ob es sich um eine Ansicht oder einen Link handeln soll. [Weitere Informationen zur Verfolgung von Links](../track-links.md).

## Senden einer Ansicht

Sie können eine Ansicht angeben, indem Sie die Variable `web.webPageDetails.pageViews.value=1` festlegen.

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
