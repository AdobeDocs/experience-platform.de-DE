---
title: Umgang mit Befehlsantworten
description: Lösen Sie mithilfe von JavaScript-Versprechen Antworten aus Befehlen.
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Umgang mit Befehlsantworten

Einige Web SDK-Befehle können ein Objekt zurückgeben, das Daten enthält, die für Ihr Unternehmen möglicherweise nützlich sind. Sie können bei Bedarf festlegen, was mit diesen Daten geschehen soll. Befehlsantworten sind für Vorschläge und Ziele nützlich, da sie Edge Network-Daten erfordern, um effektiv zu funktionieren.

Befehlsantworten verwenden JavaScript [Promises](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) und fungieren als Proxy für einen Wert, der beim Erstellen des Promises nicht bekannt ist. Sobald der Wert bekannt ist, wird das Promise mit dem Wert &quot;aufgelöst&quot;.

## Verarbeiten von Befehlsantworten mit der Web SDK-Tag-Erweiterung

Erstellen Sie eine Regel, die das Ereignis **[!UICONTROL Ereignis zum Abschluss senden]** als Teil einer Regel abonniert.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Ereignisse] ein vorhandenes Ereignis aus oder erstellen Sie ein Ereignis.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den Ereignistyp [!UICONTROL 5} auf **[!UICONTROL Ereignis-Abschluss senden]** fest.]
1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

Anschließend können Sie die Aktionen **[!UICONTROL Vorschläge anwenden]** oder **[!UICONTROL Antwort anwenden]** auf diese Regel anwenden.

1. Wählen Sie beim Anzeigen der oben erstellten oder bearbeiteten Regel eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den [!UICONTROL Aktionstyp] je nach gewünschtem Verhalten auf **[!UICONTROL Vorschläge anwenden]** oder **[!UICONTROL Antwort anwenden]** fest.
1. Legen Sie die gewünschten Felder der Aktion fest und klicken Sie dann auf **[!UICONTROL Änderungen beibehalten]**.

## Umgang mit Befehlsantworten mithilfe der Web SDK JavaScript-Bibliothek

Verwenden Sie die Methoden `then` und `catch`, um zu bestimmen, wann ein Befehl erfolgreich ausgeführt wird oder fehlschlägt. Sie können entweder `then` oder `catch` auslassen, wenn deren Zwecke für Ihre Implementierung nicht wichtig sind.

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

Alle von Befehlen zurückgegebenen Promises verwenden ein `result` -Objekt. Sie können beispielsweise Bibliotheksinformationen über den Befehl [`getLibraryInfo`](getlibraryinfo.md) vom Objekt `result` abrufen:

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

Der Inhalt dieses `result` -Objekts hängt von einer Kombination aus dem von Ihnen verwendeten Befehl und der Zustimmung des Benutzers ab. Wenn ein Benutzer seine Zustimmung zu einem bestimmten Zweck nicht erteilt hat, enthält das Antwortobjekt nur Informationen, die im Kontext dessen bereitgestellt werden können, was der Benutzer zugestimmt hat.
