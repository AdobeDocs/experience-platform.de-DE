---
title: Senden von Daten an Adobe Analytics mithilfe des Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Web SDK Daten an Adobe Analytics senden.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;Web Interaction;Seitenansichten;Linktracking;Links;Link verfolgen;ClickCollection;ClickCollection;Sammlung;
exl-id: cec4a9eb-2079-4386-88da-9b995e0673e6
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Senden von Daten an Adobe Analytics

Während es in der Vergangenheit verschiedene Funktionen gab, um zwischen einer Seitenansicht und einer Verknüpfung zu unterscheiden (z. B. `s.t(), s.tl()`), gibt es im Web SDK nur die `sendEvent` Befehl. Die Daten, die Sie mit einem Ereignis senden, bestimmen, ob es sich um eine Seitenansicht oder einen Link handeln soll. [Weitere Informationen zu Tracking-Links](../track-links.md).

## Senden einer Seitenansicht

Sie können eine Seitenansicht angeben, indem Sie die Variable `web.webPageDetails.pageViews.value=1` -Variable.

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

Obwohl Analytics technisch eine Seitenansicht aufzeichnet, auch wenn diese Variable nicht festgelegt ist, empfiehlt es sich, diese Variable immer dann festzulegen, wenn Sie eine Seitenansicht aufzeichnen möchten, die in Ihren Daten explizit ist, und Ihre Implementierung in Zukunft zu testen.
