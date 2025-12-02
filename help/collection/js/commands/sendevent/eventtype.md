---
title: eventType
description: Festlegen des Ereignistyps für einen sendEvent-Aufruf.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# `eventType`

Mit der `eventType`-Eigenschaft können Sie den Ereignistyp definieren, den Sie mit der Web-SDK senden. Dieses Feld füllt schließlich das `xdm.eventType`. Dies ist nützlich, wenn Sie die Ereignistypen unterscheiden möchten, die Sie an Adobe senden.

Adobe bietet einige vordefinierte Ereignistypen , die Sie verwenden können. Eine vollständige Liste [&#x200B; vordefinierten Werte finden Sie unter „Verfügbare Werte für die `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)&quot; im XDM-Benutzerhandbuch. Sie können auch eigene Werte verwenden, falls gewünscht.

Wenn Sie sowohl `type` hier als auch `xdm.eventType` im [`xdm`](xdm.md) festlegen, hat der Wert in diesem Feld Priorität.

Legen Sie beim Ausführen des `eventType`-Befehls die `sendEvent`-Zeichenfolgeneigenschaft fest.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```

## Ereignistyp unter Verwendung der Tag-Erweiterung „Web SDK&quot;

Die Web SDK-Tag-Erweiterung, die dieser Eigenschaft entspricht, ist das [**[!UICONTROL Type]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) Dropdown-Menü beim Konfigurieren einer &quot;[!UICONTROL Send event]&quot;-Aktion.
