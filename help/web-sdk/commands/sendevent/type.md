---
title: eventType
description: Festlegen des Ereignistyps für einen sendEvent-Aufruf.
exl-id: 9d0fae3b-827a-4084-b460-b755e478e06a
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

Mit der `eventType`-Eigenschaft können Sie den Ereignistyp definieren, den Sie mit der Web-SDK senden. Dieses Feld füllt schließlich das `xdm.eventType`. Dies ist nützlich, wenn Sie die Ereignistypen unterscheiden möchten, die Sie an Adobe senden.

Adobe bietet einige vordefinierte Ereignistypen, die Sie verwenden können. Eine vollständige Liste [ vordefinierten Werte finden Sie unter „Verfügbare Werte für die `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype)&quot; im XDM-Benutzerhandbuch. Sie können auch eigene Werte verwenden, falls gewünscht.

Wenn Sie sowohl `type` hier als auch `xdm.eventType` im [`xdm`](xdm.md) festlegen, hat der Wert in diesem Feld Priorität.

## Konfigurieren des Ereignistyps mit der Tag-Erweiterung „Web SDK&quot;

Legen Sie das **[!UICONTROL Typ]** Dropdown-Feld innerhalb der Aktionen einer Tag-Regel fest.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL  unter &quot;]&quot; eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das [!UICONTROL Erweiterung] Dropdown-Feld auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und legen Sie den [!UICONTROL Aktionstyp] auf **[!UICONTROL Ereignis senden]**.
1. Verwenden Sie das Dropdown-Menü unter dem Feld **[!UICONTROL Typ]** oder geben Sie Ihren eigenen Wert ein.
1. Klicken Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

## Konfigurieren des Ereignistyps mit der Web SDK JavaScript-Bibliothek

Legen Sie beim Ausführen des `sendEvent`-Befehls die `eventType`-Zeichenfolgeneigenschaft fest.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
