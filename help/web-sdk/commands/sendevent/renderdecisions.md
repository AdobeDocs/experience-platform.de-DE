---
title: renderDecisions
description: Rendern Sie personalisierte Inhalte, die für das automatische Rendering geeignet sind.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# `renderDecisions`

Die `renderDecisions` -Eigenschaft können Sie erzwingen, dass das Web SDK personalisierte Inhalte rendert, die für die automatische Wiedergabe geeignet sind.

## Rendern von personalisiertem Inhalt mit der Web SDK-Tag-Erweiterung

Wählen Sie die **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]** innerhalb der Aktionen einer Tag-Regel.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Ereignis senden]**.
1. Scrollen Sie nach unten zum [!UICONTROL Personalisierung] und wählen Sie dann die **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]** aktivieren.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Rendern von personalisiertem Inhalt mit der JavaScript-Bibliothek des Web SDK

Legen Sie die `renderDecisions` boolean beim Ausführen der `sendEvent` Befehl. Wenn diese Eigenschaft weggelassen wird, wird standardmäßig `false`. Legen Sie diese Eigenschaft auf `true` , wenn Sie personalisierte Inhalte automatisch rendern möchten.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
