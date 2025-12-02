---
title: applyResponse
description: Verwenden Sie eine Antwort von Edge Network, um die Web-SDK zu initialisieren.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# `applyResponse`

Mit dem Befehl `applyResponse` können Sie verschiedene Aktionen ausführen, die auf einer Antwort von Edge Network basieren. Sie wird normalerweise in Hybridbereitstellungen verwendet, bei denen der Server einen ersten Aufruf an die Edge Network durchführt. Dieser Befehl übernimmt die Antwort dieses Aufrufs und initialisiert die Web-SDK im Browser.

Führen Sie den `applyResponse` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Das -Objekt, das Konfigurationsoptionen enthält, unterstützt die folgenden Felder:

* **`renderDecisions`**: Ein boolescher Wert, der Web SDK zwingt, alle personalisierten Inhalte zu rendern, die für die automatische Wiedergabe geeignet sind. Identisch mit [`renderDecisions`](sendevent/renderdecisions.md) im [`sendEvent`](sendevent/overview.md).
* **`responseHeaders`**: Eine Zuordnung von Zeichenfolgen-Header-Namen zu Zeichenfolgen-Header-Werten.
* **`responseBody`**: Erforderlich. Ein JSON-Antworttext vom Server-Aufruf an die Edge Network.
* **`personalization.sendDisplayEvent`**: Ein boolescher Wert, der mit dem [`personalization.sendDisplayEvent`](sendevent/personalization.md) im `sendEvent`-Befehl identisch ist.

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## Antwortobjekt

Wenn Sie sich für [Handhabung von Antworten](command-responses.md) mit diesem Befehl entscheiden, sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`propositions`**: Ein Array von Vorschlägen, die von der Edge Network zurückgegeben werden. Vorschläge, die automatisch gerendert werden, `renderAttempted` das Flag auf `true` gesetzt.
* **`inferences`**: Ein Array von Rückleitungsobjekten, die Informationen zum maschinellen Lernen über diesen Benutzer enthalten.
* **`destinations`**: Ein Array von Zielobjekten, die von der Edge Network zurückgegeben werden.

## Anwenden einer Antwort mithilfe der Tag-Erweiterung „Web SDK&quot;

Die diesem Befehl entsprechende Web SDK-Tag-Erweiterung ist die [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md).
