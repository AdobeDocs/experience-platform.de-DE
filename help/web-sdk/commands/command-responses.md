---
title: Umgang mit Befehlsantworten
description: Verarbeiten Sie Antworten von Befehlen mithilfe von JavaScript-Versprechen.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Umgang mit Befehlsantworten

Einige Web SDK-Befehle können ein Objekt zurückgeben, das Daten enthält, die für Ihr Unternehmen möglicherweise nützlich sind. Sie können bei Bedarf festlegen, was mit diesen Daten geschehen soll. Befehlsantworten sind für Vorschläge und Ziele nützlich, da sie Edge-Netzwerkdaten erfordern, um effektiv zu funktionieren.

Befehlsantworten verwenden JavaScript [Promises](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise), der als Proxy für einen Wert fungiert, der beim Erstellen des Promise nicht bekannt ist. Sobald der Wert bekannt ist, wird das Promise mit dem Wert &quot;aufgelöst&quot;.

## Verarbeiten von Befehlsantworten mit der Web SDK-Tag-Erweiterung

Erstellen Sie eine Regel, die die **[!UICONTROL Abschluss des Ereignisses senden]** -Ereignis als Teil einer Regel.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Veranstaltungen], wählen Sie ein vorhandenes Ereignis aus oder erstellen Sie ein Ereignis.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Ereignistyp] nach **[!UICONTROL Abschluss des Ereignisses senden]**.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

Sie können dann die Aktionen einbeziehen **[!UICONTROL Vorschläge anwenden]** oder **[!UICONTROL Antwort anwenden]** zu dieser Regel.

1. Wählen Sie beim Anzeigen der oben erstellten oder bearbeiteten Regel eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Vorschläge anwenden]** oder **[!UICONTROL Antwort anwenden]**, abhängig vom gewünschten Verhalten.
1. Legen Sie die gewünschten Aktionsfelder fest und klicken Sie auf **[!UICONTROL Änderungen beibehalten]**.

## Umgang mit Befehlsantworten mithilfe der Web SDK-JavaScript-Bibliothek

Verwenden Sie die `then` und `catch` -Methoden, um zu bestimmen, wann ein Befehl erfolgreich ausgeführt wird oder fehlschlägt. Sie können `then` oder `catch` , wenn ihre Ziele für Ihre Implementierung nicht wichtig sind.

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

Alle Promises, die von Befehlen zurückgegeben werden, verwenden eine `result` -Objekt. Sie können beispielsweise Bibliotheksinformationen aus dem `result` -Objekt, das [`getLibraryInfo`](getlibraryinfo.md) command:

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

Der Inhalt dieser `result` -Objekt hängt von einer Kombination des von Ihnen verwendeten Befehls und der Zustimmung des Benutzers ab. Wenn ein Benutzer seine Zustimmung zu einem bestimmten Zweck nicht erteilt hat, enthält das Antwortobjekt nur Informationen, die im Kontext dessen bereitgestellt werden können, was der Benutzer zugestimmt hat.
