---
title: Umgang mit Befehlsantworten
description: Verarbeiten Sie Antworten von Befehlen mithilfe von JavaScript-Versprechen.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: 8abdd206f5fcff0e1cec7bb6ecd25c5eb9354286
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Umgang mit Befehlsantworten

Einige Web-SDK-Befehle können ein -Objekt mit Daten zurückgeben, die für Ihr Unternehmen möglicherweise nützlich sind. Sie können bei Bedarf auswählen, was mit diesen Daten gemacht werden soll. Befehlsantworten sind für Vorschläge und Ziele nützlich, da sie Edge Network-Daten benötigen, um effektiv zu funktionieren.

Befehlsantworten verwenden JavaScript [Promises](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) als Proxy für einen Wert, der beim Erstellen des Promises nicht bekannt ist. Sobald der Wert bekannt ist, wird die Zusage mit dem Wert „aufgelöst“.

Verwenden Sie die `then` und `catch` Methoden, um zu bestimmen, wann ein Befehl erfolgreich ist oder fehlschlägt. Sie können entweder `then` oder `catch` auslassen, wenn deren Zwecke für Ihre Implementierung nicht wichtig sind.

```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    console.log("The sendEvent command succeeded.");
  })
  .catch(function(error) {
    console.log("The sendEvent command failed.");
  });
```

Alle von Befehlen zurückgegebenen Zusagen verwenden ein `result`. Beispielsweise können Sie Bibliotheksinformationen mithilfe des `result`-Befehls aus dem [`getLibraryInfo`](getlibraryinfo.md) abrufen:

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

Der Inhalt dieses `result` hängt von einer Kombination aus dem von Ihnen verwendeten Befehl und dem Einverständnis des Benutzers ab. Wenn ein Benutzer für einen bestimmten Zweck sein Einverständnis nicht gegeben hat, enthält das Antwortobjekt nur Informationen, die im Zusammenhang mit dem bereitgestellt werden können, was der Benutzer eingewilligt hat.

## Befehlsantworten unter Verwendung der Tag-Erweiterung „Web SDK&quot;

Die Web-SDK-Tag-Erweiterung, die Befehlsantworten entspricht, ist eine Regel, die das [**[!UICONTROL Send event complete]**](/help/tags/extensions/client/web-sdk/event-types.md#send-event-complete) abonniert. Sie können dann Aktionen wie [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md) oder [**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md) in diese Regel einbeziehen.
