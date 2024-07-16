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

Mit dem Befehl `applyResponse` können Sie basierend auf einer Antwort des Edge Networks verschiedene Aktionen durchführen. Sie wird normalerweise in Hybridbereitstellungen verwendet, bei denen der Server einen ersten Aufruf an das Edge Network durchführt. Dieser Befehl nimmt die Antwort aus diesem Aufruf und initialisiert das Web SDK im Browser.

## Anwenden der Antwort mithilfe der Web SDK-Tag-Erweiterung

Das Anwenden von Antworten erfolgt als Aktion innerhalb einer Regel in der Adobe Experience Platform-Oberfläche für Datenerfassungs-Tags.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Aktionen] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den Aktionstyp ] auf **[!UICONTROL Antwort anwenden]** fest.[!UICONTROL 
1. Legen Sie die gewünschten Felder auf der rechten Seite fest.
1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Anwenden von Antworten mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den Befehl `applyResponse` aus, wenn Sie Ihre konfigurierte Instanz des Web SDK aufrufen. Das Objekt, das Konfigurationsoptionen enthält, unterstützt die folgenden Felder:

* **`renderDecisions`**: Ein boolescher Wert, der das Web SDK zwingt, personalisierte Inhalte wiederzugeben, die für die automatische Wiedergabe geeignet sind. Identisch mit [`renderDecisions`](sendevent/renderdecisions.md) im Befehl [`sendEvent`](sendevent/overview.md).
* **`responseHeaders`**: Eine Zuordnung der Namen von Zeichenfolgen-Kopfzeilen zu Zeichenfolgen-Kopfzeilenwerten.
* **`responseBody`**: Erforderlich. Ein JSON-Antworttext vom Server-Aufruf an das Edge Network.
* **`personalization.sendDisplayEvent`**: Ein boolescher Wert, der im Befehl `sendEvent` identisch mit [`personalization.sendDisplayEvent`](sendevent/personalization.md) arbeitet.

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

Wenn Sie mit diesem Befehl die [Handhabung von Antworten](command-responses.md) festlegen, sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`propositions`**: Ein Array von Vorschlägen, die vom Edge Network zurückgegeben werden. Vorschläge, die automatisch gerendert werden, beinhalten die Markierung `renderAttempted`, die auf `true` gesetzt ist.
* **`inferences`**: Ein Array von Inference-Objekten, die Informationen zum maschinellen Lernen über diesen Benutzer enthalten.
* **`destinations`**: Ein Array von Zielobjekten, die vom Edge Network zurückgegeben werden.
