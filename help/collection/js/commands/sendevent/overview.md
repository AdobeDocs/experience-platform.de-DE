---
title: sendEvent
description: Senden von Daten an die Adobe Experience Platform Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# `sendEvent`

Der Befehl `sendEvent` ist die primäre Möglichkeit, Daten an Adobe zu senden. Ihr Antwortobjekt ist die primäre Möglichkeit zum Abrufen personalisierter Inhalte, Identitäten und Zielgruppenziele. Verwenden Sie das [`xdm`](xdm.md) -Objekt, um Daten zu senden, die Ihrem Adobe Experience Platform-Schema zugeordnet sind. Verwenden Sie das [`data`](data.md) -Objekt, um Nicht-XDM-Daten zu senden. Die Payload zum Senden von Daten an Adobe ist auf maximal 64 KB beschränkt.

Führen Sie den `sendEvent` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Stellen Sie sicher, dass Sie den [`configure`](../configure/overview.md)-Befehl aufrufen, bevor Sie den `sendEvent`-Befehl aufrufen.

```js
alloy("sendEvent", {
  data: dataObject,
  documentUnloading: false,
  edgeConfigOverrides: { datastreamId: "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  personalization: { decisionScopes: ["hero-banner"]},
  renderDecisions: true,
  type: "commerce.purchases",
  xdm: adobeDataLayer.getState(reference)
});
```

## Antwortobjekt

Wenn Sie sich für [Handhabung von Antworten](../command-responses.md) mit diesem Befehl entscheiden, sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`propositions`**: Ein Array von Vorschlägen, die von der Edge Network zurückgegeben werden. Vorschläge, die automatisch gerendert werden, `renderAttempted` das Flag auf `true` gesetzt.
* **`inferences`**: Ein Array von Rückleitungsobjekten, die Informationen zum maschinellen Lernen über diesen Benutzer enthalten.
* **`destinations`**: Ein Array von Zielobjekten, die von der Edge Network zurückgegeben werden.

## Senden eines Ereignisses mit der Tag-Erweiterung „Web SDK&quot;

Die Web SDK-Tag-Erweiterung, die diesem Befehl entspricht, ist die [**[!UICONTROL Send event]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#data-fields).
