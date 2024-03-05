---
title: documentUnloading
description: Verwenden Sie die JavaScript-API sendBeacon , um Daten an Adobe zu senden.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 2%

---

# `documentUnloading`

Die `documentUnloading` -Eigenschaft ermöglicht die Verwendung der [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) -Methode, um Daten an Adobe zu senden. Wenn eine typische Anfrage zu lange dauert, kann der Browser die Anfrage abbrechen. Sie können dem Web SDK die Verwendung der `sendBeacon` damit die Anforderung im Hintergrund ausgeführt wird, nachdem Sie von der Seite weg navigiert haben. Aktivieren Sie diese Eigenschaft, um zu verhindern, dass Datenanfragen beim Entladen vom Browser abgebrochen werden.

In mehreren Browsern ist die Datenmenge, mit der gesendet werden kann, auf 64 KB begrenzt `sendBeacon` auf einmal. Wenn der Browser das Ereignis ablehnt, weil die Payload zu groß ist, verwendet das Web SDK wieder die normale Transportmethode.

## Konfigurieren des Entladens von Dokumenten mithilfe der Web SDK-Tag-Erweiterung

Aktivieren Sie die **[!UICONTROL Dokument wird entladen]** innerhalb der Aktionen einer Tag-Regel.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Ereignis senden]**.
1. Aktivieren Sie die **[!UICONTROL Dokument wird entladen]** im [!UICONTROL Daten] Abschnitt.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Konfigurieren des Entladens von Dokumenten mithilfe der JavaScript-Bibliothek des Web SDK

Legen Sie die `documentUnloading` boolean beim Ausführen der `sendEvent` Befehl. Der Standardwert lautet `false`. Legen Sie diese Eigenschaft auf `true` , wenn Sie die `sendBeacon` -Methode, um Daten an Adobe zu senden.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
