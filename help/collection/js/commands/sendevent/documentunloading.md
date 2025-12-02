---
title: DokumentEntladen
description: Verwenden Sie die JavaScript sendBeacon-API, um Daten an Adobe zu senden.
exl-id: 7683c0c4-ae2e-46ec-8471-628a10e17afc
source-git-commit: a229cec4a53ab85d13590205a008612719019ebd
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# `documentUnloading`

Mit der `documentUnloading`-Eigenschaft können Sie die [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)-Methode von JavaScript verwenden, um Daten an Adobe zu senden. Wenn eine typische Anfrage zu lange dauert, kann der Browser die Anfrage abbrechen. Sie können Web SDK anweisen, `sendBeacon` zu verwenden, damit die Anfrage im Hintergrund ausgeführt wird, nachdem Sie die Seite verlassen haben. Aktivieren Sie diese Eigenschaft, um zu verhindern, dass Datenanfragen beim Entladen vom Browser abgebrochen werden.

In verschiedenen Browsern ist die Datenmenge, die mit `sendBeacon` gleichzeitig gesendet werden kann, auf 64 KB beschränkt. Wenn der Browser das Ereignis ablehnt, weil die Payload zu groß ist, greift der Web SDK auf die Verwendung seiner normalen Transportmethode zurück. Selbst wenn ein bestimmter Browser größere Payloads zulässt, reduzieren Adobe-Datenerfassungs-Server Payloads auf 64 KB.

Legen Sie beim Ausführen des `documentUnloading`-Befehls den booleschen Wert `sendEvent` fest. Der Standardwert lautet `false`. Legen Sie diese Eigenschaft auf `true` fest, wenn Sie die `sendBeacon`-Methode zum Senden von Daten an Adobe verwenden möchten.

>[!IMPORTANT]
>
>Die `documentUnloading`-Eigenschaft ist mit der [`renderDecisions`](renderdecisions.md)-Eigenschaft nicht kompatibel. Vermeiden Sie es, beide Eigenschaften gleichzeitig auf `true` zu setzen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "documentUnloading": true
});
```

## Dokument-Upload mithilfe der Tag-Erweiterung „Web SDK&quot;

Das Kontrollkästchen &quot;**[!UICONTROL Document will unload]**&quot; ist beim Konfigurieren einer [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields) Aktion verfügbar, wenn die Tag-Erweiterung „Web SDK&quot; verwendet wird.
