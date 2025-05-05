---
title: applyResponse
description: Verwenden Sie eine Antwort aus dem Edge Network, um die Web-SDK zu initialisieren.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: 74725546163f0807d3188aff5b5ffda9b8d6350b
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

Mit dem Befehl `applyResponse` können Sie basierend auf einer Antwort des Edge Networks verschiedene Aktionen ausführen. Sie wird normalerweise in Hybridbereitstellungen verwendet, in denen der -Server einen ersten Aufruf an das -Edge Network durchführt. Dieser Befehl übernimmt die Antwort dieses Aufrufs und initialisiert die Web-SDK im Browser.

## Anwenden einer Antwort mithilfe der Tag-Erweiterung „Web SDK&quot;

Das Anwenden von Antworten wird als Aktion innerhalb einer Regel in der Tags-Benutzeroberfläche der Datenerfassung von Adobe Experience Platform ausgeführt.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL &#x200B; unter &quot;]&quot; eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie im Dropdown[!UICONTROL Feld &#x200B;]Erweiterung“ den Wert **[!UICONTROL Adobe Experience Platform Web SDK]** fest und legen Sie als [!UICONTROL Aktionstyp] den Wert **[!UICONTROL Antwort anwenden]** fest.
1. Legen Sie die gewünschten Felder auf der rechten Seite fest.
1. Klicken Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

## Anwenden von Antworten mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den `applyResponse` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Das -Objekt, das Konfigurationsoptionen enthält, unterstützt die folgenden Felder:

* **`renderDecisions`**: Ein boolescher Wert, der Web SDK zwingt, alle personalisierten Inhalte zu rendern, die für die automatische Wiedergabe geeignet sind. Identisch mit [`renderDecisions`](sendevent/renderdecisions.md) im [`sendEvent`](sendevent/overview.md).
* **`responseHeaders`**: Eine Zuordnung von Zeichenfolgen-Header-Namen zu Zeichenfolgen-Header-Werten.
* **`responseBody`**: Erforderlich. Ein JSON-Antworttext vom Server-Aufruf an das Edge Network.
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

* **`propositions`**: Ein Array von vom Edge Network zurückgegebenen Vorschlägen. Vorschläge, die automatisch gerendert werden, `renderAttempted` das Flag auf `true` gesetzt.
* **`inferences`**: Ein Array von Rückleitungsobjekten, die Informationen zum maschinellen Lernen über diesen Benutzer enthalten.
* **`destinations`**: Ein Array von Zielobjekten, die vom Edge Network zurückgegeben werden.
