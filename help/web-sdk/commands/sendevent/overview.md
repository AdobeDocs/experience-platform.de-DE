---
title: sendEvent
description: Senden Sie Daten an das Adobe Experience Platform-Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# `sendEvent`

Die `sendEvent` -Befehl ist die primäre Methode zum Senden von Daten an Adobe, zum Abrufen personalisierter Inhalte, Identitäten und Zielgruppenziele. Verwenden Sie die [`xdm`](xdm.md) -Objekt zum Senden von Daten, die Ihrem Adobe Experience Platform-Schema zugeordnet sind. Verwenden Sie die [`data`](data.md) -Objekt zum Senden von Nicht-XDM-Daten. Mit dem Datastream-Mapper können Sie Daten in diesem Objekt an Schemafeldern ausrichten.

## Senden von Ereignisdaten mit der Web SDK-Tag-Erweiterung

Das Senden von Ereignisdaten erfolgt als Aktion innerhalb einer Regel in der Adobe Experience Platform-Oberfläche für Datenerfassungs-Tags.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Ereignis senden]**.
1. Legen Sie die gewünschten Felder fest, klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Senden von Ereignisdaten mit der JavaScript-Bibliothek des Web SDK

Führen Sie die `sendEvent` beim Aufruf Ihrer konfigurierten Instanz des Web SDK. Stellen Sie sicher, dass Sie die [`configure`](../configure/overview.md) -Befehl vor dem Aufruf der `sendEvent` Befehl.

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": false,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## Antwortobjekt

Wenn Sie sich für [Antworten verarbeiten](../command-responses.md) Mit diesem Befehl sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`propositions`**: Ein Array von Vorschlägen, die vom Edge Network zurückgegeben werden. Automatisch gerenderte Vorschläge beinhalten das Flag `renderAttempted` auf `true`.
* **`inferences`**: Ein Array von Inference-Objekten, die Informationen zum maschinellen Lernen über diesen Benutzer enthalten.
* **`destinations`**: Ein Array von Zielobjekten, die vom Edge Network zurückgegeben werden.
