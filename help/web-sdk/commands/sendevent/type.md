---
title: eventType
description: Legen Sie den Ereignistyp für einen sendEvent-Aufruf fest.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# `eventType`

Die `eventType` -Eigenschaft können Sie den Ereignistyp definieren, den Sie mit dem Web SDK senden. Dieses Feld füllt schließlich die `xdm.eventType` -Feld. Es ist nützlich, wenn Sie die Ereignistypen unterscheiden möchten, die Sie an Adobe senden.

Adobe bietet einige vordefinierte Ereignistypen, die Sie verwenden können. Siehe [Verfügbare Werte für `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype) im XDM-Benutzerhandbuch eine vollständige Liste vordefinierter Werte. Sie können bei Bedarf auch Ihre eigenen Werte verwenden.

Wenn Sie beide `type` hier und `xdm.eventType` im [`xdm`](xdm.md) -Objekt, hat der Wert in diesem Feld Priorität.

## Konfigurieren des Ereignistyps mithilfe der Web SDK-Tag-Erweiterung

Legen Sie die **[!UICONTROL Typ]** Dropdown-Feld innerhalb der Aktionen einer Tag-Regel.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Ereignis senden]**.
1. Verwenden Sie das Dropdown-Menü unter **[!UICONTROL Typ]** oder geben Sie Ihren eigenen Wert ein.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Ereignistyp mit der JavaScript-Bibliothek des Web SDK konfigurieren

Legen Sie die `eventType` Zeichenfolgeneigenschaft beim Ausführen der `sendEvent` Befehl.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "type": "commerce.purchases"
});
```
