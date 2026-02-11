---
title: Konversation
description: Konfigurieren Sie die Chat-Einstellungen für Brand Concierge.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '111'
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
| **`stickyConversationSession`** | `boolean` | Legt fest, ob Web SDK ein Sitzungs-Cookie setzt, um Brand Concierge-Chat-Sitzungen über Seitenladevorgänge hinweg beizubehalten. Die Standardeinstellung ist `false`. Wenn er ausgelassen oder auf `false` gesetzt wird, startet der Brand Concierge-Chat bei jedem Laden der Seite eine neue Sitzung. |

## Beispiel

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  conversation: {
    stickyConversationSession: true
  }
});
```

## Konfigurieren von Gesprächseinstellungen mit der Tag-Erweiterung „Web SDK&quot;

Diese Einstellungen können in der Tag-Erweiterung „Web SDK&quot; mithilfe von [Brand Concierge-Einstellungen konfiguriert &#x200B;](/help/tags/extensions/client/web-sdk/configure/brand-concierge.md).
