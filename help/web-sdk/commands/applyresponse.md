---
title: applyResponse
description: Verwenden Sie eine Antwort des Edge Networks, um das Web SDK zu initialisieren.
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: 74725546163f0807d3188aff5b5ffda9b8d6350b
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# `applyResponse`

Die `applyResponse` -Befehl können Sie basierend auf einer Antwort des Edge Networks verschiedene Aktionen ausführen. Sie wird normalerweise in Hybridbereitstellungen verwendet, bei denen der Server einen ersten Aufruf an das Edge Network durchführt. Dieser Befehl nimmt die Antwort aus diesem Aufruf und initialisiert das Web SDK im Browser.

## Anwenden der Antwort mithilfe der Web SDK-Tag-Erweiterung

Das Anwenden von Antworten erfolgt als Aktion innerhalb einer Regel in der Adobe Experience Platform-Oberfläche für Datenerfassungs-Tags.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Antwort anwenden]**.
1. Legen Sie die gewünschten Felder auf der rechten Seite fest.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Anwenden von Antworten mithilfe der Web SDK-JavaScript-Bibliothek

Führen Sie die `applyResponse` beim Aufruf Ihrer konfigurierten Instanz des Web SDK. Das Objekt, das Konfigurationsoptionen enthält, unterstützt die folgenden Felder:

* **`renderDecisions`**: Ein boolescher Wert, der das Web SDK zwingt, personalisierte Inhalte wiederzugeben, die für die automatische Wiedergabe geeignet sind. Identisch mit [`renderDecisions`](sendevent/renderdecisions.md) im [`sendEvent`](sendevent/overview.md) Befehl.
* **`responseHeaders`**: Eine Zuordnung von Zeichenfolgen-Kopfzeilennamen zu Zeichenfolgen-Kopfzeilenwerten.
* **`responseBody`**: Erforderlich. Ein JSON-Antworttext vom Server-Aufruf an das Edge Network.
* **`personalization.sendDisplayEvent`**: Ein boolescher Wert, der identisch mit [`personalization.sendDisplayEvent`](sendevent/personalization.md) im `sendEvent` Befehl.

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

Wenn Sie sich für [Antworten verarbeiten](command-responses.md) Mit diesem Befehl sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`propositions`**: Ein Array von Vorschlägen, die vom Edge Network zurückgegeben werden. Automatisch gerenderte Vorschläge beinhalten das Flag `renderAttempted` auf `true`.
* **`inferences`**: Ein Array von Inference-Objekten, die Informationen zum maschinellen Lernen über diesen Benutzer enthalten.
* **`destinations`**: Ein Array von Zielobjekten, die vom Edge Network zurückgegeben werden.
