---
title: renderDecisions
description: Rendern Sie personalisierte Inhalte, die für die automatische Wiedergabe geeignet sind.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# `renderDecisions`

Mit der `renderDecisions`-Eigenschaft können Sie die Web-SDK zwingen, alle personalisierten Inhalte zu rendern, die für die automatische Wiedergabe geeignet sind.

Legen Sie beim Ausführen des `renderDecisions`-Befehls den booleschen Wert `sendEvent` fest. Wenn diese Eigenschaft ausgelassen wird, ist sie standardmäßig auf `false` festgelegt. Legen Sie diese Eigenschaft auf `true` fest, wenn Sie personalisierten Inhalt automatisch rendern möchten.

>[!IMPORTANT]
>
>Die `renderDecisions`-Eigenschaft ist mit der [`documentUnloading`](documentunloading.md)-Eigenschaft nicht kompatibel. Vermeiden Sie es, beide Eigenschaften gleichzeitig auf `true` zu setzen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```

Stellen Sie sicher, dass Sie beim Festlegen dieser Eigenschaft auf `true` auch verknüpfte Bereiche oder Oberflächen einbeziehen. Diese Bereiche oder Oberflächen können automatisch (z. B. beim ersten `sendEvent` auf einer Seite) oder explizit (mit [`personalization.decisionScopes`](personalization.md#personalizationdecisionscopes) oder [`personalization.surfaces`](personalization.md#personalizationsurfaces)) angefordert werden. Ein häufiges Problem beim Rendern der Personalisierung ist das folgende Szenario:

1. Ein `sendEvent` Befehl wird früh auf der Seite ausgeführt, die eine Standardpersonalisierung anfordert, wobei `renderDecisions` nicht festgelegt ist (standardmäßig `false`). Vorschläge werden abgerufen, aber nicht gerendert.
1. Ein anderer `sendEvent` Trigger weiter unten auf der Seite, dessen `renderDecisions` auf `true` festgelegt ist, aber keine Bereiche oder Oberflächen enthält. Da in diesem zweiten Aufruf keine Bereiche oder Oberflächen vorhanden sind, wird nichts gerendert.

Sie können dieses Problem wie folgt vermeiden:

* Beim ersten `renderDecisions`-Aufruf `true` auf `sendEvent` setzen oder
* Explizites Festlegen von `decisionScopes` oder `surfaces` bei einem nachfolgenden `sendEvent`-Aufruf beim Festlegen von `renderDecisions` auf `true`.

## Rendern von Entscheidungen mithilfe der Tag-Erweiterung „Web SDK&quot;

Das Äquivalent der Web SDK-Tag-Erweiterung zu dieser Eigenschaft ist das Kontrollkästchen [**Visuelle Personalisierungsentscheidungen rendern**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) innerhalb der Aktion &quot;[!UICONTROL Send event]&quot;.
