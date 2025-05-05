---
title: renderDecisions
description: Rendern Sie personalisierte Inhalte, die für die automatische Wiedergabe geeignet sind.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# `renderDecisions`

Mit der `renderDecisions`-Eigenschaft können Sie die Web-SDK zwingen, alle personalisierten Inhalte zu rendern, die für die automatische Wiedergabe geeignet sind.

## Rendern von personalisierten Inhalten mit der Tag-Erweiterung „Web SDK&quot;

Aktivieren **[!UICONTROL das Kontrollkästchen]** Visuelle Personalisierungsentscheidungen rendern“ in den Aktionen einer Tag-Regel.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL &#x200B; unter &quot;]&quot; eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das [!UICONTROL Erweiterung] Dropdown-Feld auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und legen Sie den [!UICONTROL Aktionstyp] auf **[!UICONTROL Ereignis senden]**.
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Personalization] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL Visuelle Personalisierungsentscheidungen rendern]**.
1. Klicken Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

## Rendern von personalisierten Inhalten mit der Web SDK JavaScript-Bibliothek

Legen Sie beim Ausführen des `sendEvent`-Befehls den booleschen Wert `renderDecisions` fest. Wenn diese Eigenschaft ausgelassen wird, ist sie standardmäßig auf `false` festgelegt. Legen Sie diese Eigenschaft auf `true` fest, wenn Sie personalisierten Inhalt automatisch rendern möchten.

>[!IMPORTANT]
>
>Die `renderDecisions`-Eigenschaft ist mit der [`documentUnloading`](documentunloading.md)-Eigenschaft nicht kompatibel. Sie sollten nicht beide Eigenschaften gleichzeitig auf `true` setzen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```
