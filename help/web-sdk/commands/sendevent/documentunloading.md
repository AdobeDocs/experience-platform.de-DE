---
title: DokumentEntladen
description: Verwenden Sie die JavaScript sendBeacon-API, um Daten an Adobe zu senden.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: f12d222e81a39a26bd71ab4bede05aa992889605
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# `documentUnloading`

Mit der `documentUnloading`-Eigenschaft können Sie die [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)-Methode von JavaScript verwenden, um Daten an Adobe zu senden. Wenn eine typische Anfrage zu lange dauert, kann der Browser die Anfrage abbrechen. Sie können Web SDK anweisen, `sendBeacon` zu verwenden, damit die Anfrage im Hintergrund ausgeführt wird, nachdem Sie die Seite verlassen haben. Aktivieren Sie diese Eigenschaft, um zu verhindern, dass Datenanfragen beim Entladen vom Browser abgebrochen werden.

In verschiedenen Browsern ist die Datenmenge, die mit `sendBeacon` gleichzeitig gesendet werden kann, auf 64 KB beschränkt. Wenn der Browser das Ereignis ablehnt, weil die Payload zu groß ist, greift der Web SDK auf die Verwendung seiner normalen Transportmethode zurück.

## Konfigurieren des Entladens von Dokumenten mithilfe der Tag-Erweiterung „Web SDK&quot;

Aktivieren Sie **[!UICONTROL Kontrollkästchen]** Dokument wird entladen“ innerhalb der Aktionen einer Tag-Regel.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL &#x200B; unter &quot;]&quot; eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das [!UICONTROL Erweiterung] Dropdown-Feld auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und legen Sie den [!UICONTROL Aktionstyp] auf **[!UICONTROL Ereignis senden]**.
1. Aktivieren Sie **[!UICONTROL Kontrollkästchen]** Dokument wird entladen“ im Abschnitt [!UICONTROL Daten].
1. Klicken Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

## Konfigurieren des Entladens von Dokumenten mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie beim Ausführen des `sendEvent`-Befehls den booleschen Wert `documentUnloading` fest. Der Standardwert lautet `false`. Legen Sie diese Eigenschaft auf `true` fest, wenn Sie die `sendBeacon`-Methode zum Senden von Daten an Adobe verwenden möchten.

>[!IMPORTANT]
>
>Die `documentUnloading`-Eigenschaft ist mit der [`renderDecisions`](renderdecisions.md)-Eigenschaft nicht kompatibel. Sie sollten nicht beide Eigenschaften gleichzeitig auf `true` setzen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```
