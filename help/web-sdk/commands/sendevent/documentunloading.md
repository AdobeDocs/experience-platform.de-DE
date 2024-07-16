---
title: documentUnloading
description: Verwenden Sie die JavaScript sendBeacon-API, um Daten an Adobe zu senden.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# `documentUnloading`

Mit der `documentUnloading` -Eigenschaft können Sie die JavaScript-Methode [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) verwenden, um Daten an Adobe zu senden. Wenn eine typische Anfrage zu lange dauert, kann der Browser die Anfrage abbrechen. Sie können dem Web SDK mitteilen, dass es &quot;`sendBeacon`&quot; verwenden soll, damit die Anforderung im Hintergrund ausgeführt wird, nachdem Sie von der Seite weg navigiert sind. Aktivieren Sie diese Eigenschaft, um zu verhindern, dass Datenanfragen beim Entladen vom Browser abgebrochen werden.

Mehrere Browser legen eine Beschränkung von 64 KB auf die Datenmenge fest, die mit `sendBeacon` gleichzeitig gesendet werden kann. Wenn der Browser das Ereignis ablehnt, weil die Payload zu groß ist, verwendet das Web SDK wieder die normale Transportmethode.

## Konfigurieren des Entladens von Dokumenten mithilfe der Web SDK-Tag-Erweiterung

Aktivieren Sie das Kontrollkästchen **[!UICONTROL Dokument entladen]** innerhalb der Aktionen einer Tag-Regel.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Aktionen] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den Aktionstyp ] auf **[!UICONTROL Ereignis senden]** fest.[!UICONTROL 
1. Aktivieren Sie das Kontrollkästchen **[!UICONTROL Dokument wird entladen]** im Abschnitt [!UICONTROL Daten] .
1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Konfigurieren des Entladens von Dokumenten mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie den booleschen Wert `documentUnloading` fest, wenn Sie den Befehl `sendEvent` ausführen. Der Standardwert ist `false`. Setzen Sie diese Eigenschaft auf `true` , wenn Sie die `sendBeacon` -Methode verwenden möchten, um Daten an Adobe zu senden.

>[!IMPORTANT]
>
>Die Eigenschaft `documentUnloading` ist nicht mit der Eigenschaft [`renderDecisions`](renderdecisions.md) kompatibel. Sie sollten nicht beide Eigenschaften gleichzeitig auf `true` setzen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
