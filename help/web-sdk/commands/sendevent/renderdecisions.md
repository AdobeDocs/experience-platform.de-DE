---
title: renderDecisions
description: Rendern Sie personalisierte Inhalte, die für das automatische Rendering geeignet sind.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# `renderDecisions`

Mit der Eigenschaft `renderDecisions` können Sie das Web SDK zwingen, personalisierte Inhalte wiederzugeben, die für die automatische Wiedergabe geeignet sind.

## Rendern von personalisiertem Inhalt mit der Web SDK-Tag-Erweiterung

Aktivieren Sie das Kontrollkästchen **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]** innerhalb der Aktionen einer Tag-Regel.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Aktionen] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den Aktionstyp ] auf **[!UICONTROL Ereignis senden]** fest.[!UICONTROL 
1. Scrollen Sie nach unten zum Bereich [!UICONTROL Personalization] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]** .
1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Rendern von personalisierten Inhalten mit der Web SDK JavaScript-Bibliothek

Legen Sie den booleschen Wert `renderDecisions` fest, wenn Sie den Befehl `sendEvent` ausführen. Wenn diese Eigenschaft weggelassen wird, wird standardmäßig `false` verwendet. Setzen Sie diese Eigenschaft auf `true` , wenn Sie personalisierte Inhalte automatisch rendern möchten.

>[!IMPORTANT]
>
>Die Eigenschaft `renderDecisions` ist nicht mit der Eigenschaft [`documentUnloading`](documentunloading.md) kompatibel. Sie sollten nicht beide Eigenschaften gleichzeitig auf `true` setzen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
