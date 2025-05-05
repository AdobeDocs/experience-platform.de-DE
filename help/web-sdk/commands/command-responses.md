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

Einige Web-SDK-Befehle können ein -Objekt mit Daten zurückgeben, die für Ihr Unternehmen möglicherweise nützlich sind. Sie können bei Bedarf auswählen, was mit diesen Daten gemacht werden soll. Befehlsantworten sind für Vorschläge und Ziele nützlich, da sie Edge Network-Daten benötigen, um effektiv zu funktionieren.

Befehlsantworten verwenden JavaScript [Promises](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) als Proxy für einen Wert, der beim Erstellen des Promises nicht bekannt ist. Sobald der Wert bekannt ist, wird die Zusage mit dem Wert „aufgelöst“.

## Verarbeiten von Befehlsantworten mithilfe der Tag-Erweiterung „Web SDK&quot;

Erstellen Sie eine Regel, die das Ereignis **[!UICONTROL Senden abgeschlossen]** als Teil einer Regel abonniert.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL &#x200B; unter „Ereignisse] ein vorhandenes Ereignis aus oder erstellen Sie ein Ereignis.
1. Legen Sie das [!UICONTROL Erweiterung] Dropdown-Feld auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und setzen Sie den [!UICONTROL Ereignistyp] auf **[!UICONTROL Ereignis senden abgeschlossen]**.
1. Klicken Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

Sie können dann die Aktionen **[!UICONTROL Vorschläge anwenden]** oder **[!UICONTROL Antwort anwenden]** auf diese Regel anwenden.

1. Wenn Sie die oben erstellte oder bearbeitete Regel anzeigen, wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie im Dropdown[!UICONTROL Feld &#x200B;]Erweiterung“ den Wert **[!UICONTROL Adobe Experience Platform Web SDK]** fest, und legen Sie [!UICONTROL Aktionstyp] je nach gewünschtem Verhalten **[!UICONTROL Vorschläge anwenden]** oder **[!UICONTROL Antwort anwenden]** fest.
1. Legen Sie die gewünschten Felder der Aktion fest und klicken Sie dann auf **[!UICONTROL Änderungen beibehalten]**.

## Verarbeiten von Befehlsantworten mithilfe der Web SDK JavaScript-Bibliothek

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

Alle von Befehlen zurückgegebenen Zusagen verwenden ein `result`. Beispielsweise können Sie Bibliotheksinformationen mithilfe des [`getLibraryInfo`](getlibraryinfo.md)-Befehls aus dem `result` abrufen:

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

Der Inhalt dieses `result` hängt von einer Kombination aus dem von Ihnen verwendeten Befehl und dem Einverständnis des Benutzers ab. Wenn ein Benutzer für einen bestimmten Zweck sein Einverständnis nicht gegeben hat, enthält das Antwortobjekt nur Informationen, die im Zusammenhang mit dem bereitgestellt werden können, was der Benutzer eingewilligt hat.
