---
title: eventType
description: Legen Sie den Ereignistyp für einen sendEvent-Aufruf fest.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

Mit der Eigenschaft `eventType` können Sie den Ereignistyp definieren, den Sie mit dem Web SDK senden. Dieses Feld füllt schließlich das Feld `xdm.eventType` aus. Es ist nützlich, wenn Sie die Ereignistypen unterscheiden möchten, die Sie an Adobe senden.

Adobe bietet einige vordefinierte Ereignistypen, die Sie verwenden können. Eine vollständige Liste der vordefinierten Werte finden Sie unter [Verfügbare Werte für `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) im XDM-Benutzerhandbuch. Sie können bei Bedarf auch Ihre eigenen Werte verwenden.

Wenn Sie sowohl `type` hier als auch `xdm.eventType` im Objekt [`xdm`](xdm.md) festlegen, hat der Wert in diesem Feld Priorität.

## Konfigurieren des Ereignistyps mithilfe der Web SDK-Tag-Erweiterung

Legen Sie das Dropdown-Feld **[!UICONTROL Typ]** innerhalb der Aktionen einer Tag-Regel fest.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Aktionen] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den Aktionstyp ] auf **[!UICONTROL Ereignis senden]** fest.[!UICONTROL 
1. Verwenden Sie das Dropdown-Menü unter dem Feld **[!UICONTROL Typ]** oder geben Sie Ihren eigenen Wert ein.
1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Ereignistyp mit der Web SDK JavaScript-Bibliothek konfigurieren

Legen Sie die String-Eigenschaft `eventType` fest, wenn Sie den Befehl `sendEvent` ausführen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
