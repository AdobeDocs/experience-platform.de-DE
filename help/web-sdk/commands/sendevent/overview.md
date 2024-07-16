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

Der Befehl `sendEvent` ist die primäre Methode zum Senden von Daten an Adobe, zum Abrufen personalisierter Inhalte, Identitäten und Zielgruppenziele. Verwenden Sie das Objekt [`xdm`](xdm.md) , um Daten zu senden, die Ihrem Adobe Experience Platform-Schema zugeordnet sind. Verwenden Sie das Objekt [`data`](data.md) , um Nicht-XDM-Daten zu senden. Mit dem Datastream-Mapper können Sie Daten in diesem Objekt an Schemafeldern ausrichten.

## Senden von Ereignisdaten mit der Web SDK-Tag-Erweiterung

Das Senden von Ereignisdaten erfolgt als Aktion innerhalb einer Regel in der Adobe Experience Platform-Oberfläche für Datenerfassungs-Tags.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Aktionen] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den Aktionstyp ] auf **[!UICONTROL Ereignis senden]** fest.[!UICONTROL 
1. Legen Sie die gewünschten Felder fest, klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Senden von Ereignisdaten mit der Web SDK JavaScript-Bibliothek

Führen Sie den Befehl `sendEvent` aus, wenn Sie Ihre konfigurierte Instanz des Web SDK aufrufen. Rufen Sie den Befehl [`configure`](../configure/overview.md) auf, bevor Sie den Befehl `sendEvent` aufrufen.

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

Wenn Sie mit diesem Befehl die [Handhabung von Antworten](../command-responses.md) festlegen, sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`propositions`**: Ein Array von Vorschlägen, die vom Edge Network zurückgegeben werden. Vorschläge, die automatisch gerendert werden, beinhalten die Markierung `renderAttempted`, die auf `true` gesetzt ist.
* **`inferences`**: Ein Array von Inference-Objekten, die Informationen zum maschinellen Lernen über diesen Benutzer enthalten.
* **`destinations`**: Ein Array von Zielobjekten, die vom Edge Network zurückgegeben werden.
