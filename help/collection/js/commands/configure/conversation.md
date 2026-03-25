---
title: Konversation
description: Konfigurieren Sie die Chat-Einstellungen für Brand Concierge.
exl-id: 0f64c7f1-2c28-4c67-af05-dc9ee688fdc0
source-git-commit: 9f7464b78da9615bf6966e34eb129150a481fb5f
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 13%

---

# `conversation`

>[!AVAILABILITY]
>
>Brand Concierge für das Web SDK befindet sich derzeit in der **Beta**. Die Funktionalität und Dokumentation können sich ändern.

Das `conversation`-Objekt enthält Konfigurationsoptionen für Brand Concierge-Chat-Sitzungen. Dieses Objekt wird in Web SDK ab Version 2.31.0 unterstützt.

## Properties

| Eigenschaft | Typ | Beschreibung |
| --- | --- | --- |
| **`collectSources`** | `boolean` | Bestimmt, ob Web SDK den `adobe_brand_concierge_source` Abfragezeichenfolgenparameter liest und in `xdm.channel.referringSource` einbezieht. Die Standardeinstellung ist `false`. |
| **`stickyConversationSession`** | `boolean` | Legt fest, ob Web SDK ein Sitzungs-Cookie setzt, um Brand Concierge-Chat-Sitzungen über Seitenladevorgänge hinweg beizubehalten. Die Standardeinstellung ist `false`. Wenn er ausgelassen oder auf `false` gesetzt wird, startet der Brand Concierge-Chat bei jedem Laden der Seite eine neue Sitzung. |

## Beispiel

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    collectSources: true
    stickyConversationSession: true
  }
});
```

## Konfigurieren von Gesprächseinstellungen mit der Tag-Erweiterung „Web SDK&quot;

Diese Einstellungen können in der Tag-Erweiterung „Web SDK&quot; mithilfe von [Brand Concierge-Einstellungen konfiguriert &#x200B;](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
