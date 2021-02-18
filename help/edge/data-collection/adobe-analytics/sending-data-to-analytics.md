---
title: Senden von Daten an Adobe Analytics mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Daten mit dem Adobe Experience Platform Web SDK an Adobe Analytics gesendet werden.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;webInteraction;page-Ansichten;Link-Verfolgung;Links;track-Links;clickCollection;click-Auflistung;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '162'
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
