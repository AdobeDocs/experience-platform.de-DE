---
title: sendEvent
description: Senden von Daten an das Adobe Experience Platform-Edge Network.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# `sendEvent`

Der Befehl `sendEvent` ist die primäre Möglichkeit, Daten an Adobe zu senden, um personalisierte Inhalte, Identitäten und Zielgruppenziele abzurufen. Verwenden Sie das [`xdm`](xdm.md) -Objekt, um Daten zu senden, die Ihrem Adobe Experience Platform-Schema zugeordnet sind. Verwenden Sie das [`data`](data.md) -Objekt, um Nicht-XDM-Daten zu senden. Sie können die Datenstrom-Zuordnung verwenden, um Daten innerhalb dieses Objekts an Schemafeldern auszurichten.

## Senden von Ereignisdaten mit der Tag-Erweiterung „Web SDK&quot;

Das Senden von Ereignisdaten wird als Aktion innerhalb einer Regel in der Benutzeroberfläche „Tags der Datenerfassung“ von Adobe Experience Platform ausgeführt.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL &#x200B; unter &quot;]&quot; eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das [!UICONTROL Erweiterung] Dropdown-Feld auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und legen Sie den [!UICONTROL Aktionstyp] auf **[!UICONTROL Ereignis senden]**.
1. Legen Sie die gewünschten Felder fest, klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Senden von Ereignisdaten mit der Web SDK JavaScript-Bibliothek

Führen Sie den `sendEvent` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Stellen Sie sicher, dass Sie den [`configure`](../configure/overview.md)-Befehl aufrufen, bevor Sie den `sendEvent`-Befehl aufrufen.

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

Wenn Sie sich für [Handhabung von Antworten](../command-responses.md) mit diesem Befehl entscheiden, sind die folgenden Eigenschaften im Antwortobjekt verfügbar:

* **`propositions`**: Ein Array von vom Edge Network zurückgegebenen Vorschlägen. Vorschläge, die automatisch gerendert werden, `renderAttempted` das Flag auf `true` gesetzt.
* **`inferences`**: Ein Array von Rückleitungsobjekten, die Informationen zum maschinellen Lernen über diesen Benutzer enthalten.
* **`destinations`**: Ein Array von Zielobjekten, die vom Edge Network zurückgegeben werden.
