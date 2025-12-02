---
title: debugEnabled
description: Verwenden Sie den -Code, um Debugging-Funktionen in der Web-SDK zu aktivieren.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `debugEnabled`

Mit der `debugEnabled` Eigenschaft können Sie das Debugging mithilfe von Web SDK-Code aktivieren oder deaktivieren. Dies ist eine der verfügbaren Methoden zum Aktivieren von [Debugging](/help/collection/use-cases/debugging.md). Das Aktivieren des Debuggens innerhalb Ihrer Implementierung kann während der Website-Entwicklung praktischer sein als andere Methoden, wenn Sie das Debuggen immer aktivieren möchten. Diese Debugging-Methode aktiviert sie für alle Besucher, sodass sie für Produktionsseiten nicht empfohlen wird. Weitere Möglichkeiten zum Aktivieren [&#x200B; Debuggens finden &#x200B;](/help/collection/use-cases/debugging.md) auf der Seite zum Anwendungsfall „Debugging“.

Setzen Sie den `debugEnabled` booleschen Wert auf `true`, wenn Sie den `configure` Befehl ausführen. Wenn Sie diese Eigenschaft beim Konfigurieren der SDK weglassen, wird sie standardmäßig auf `false` gesetzt.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

## Aktivieren des Debuggens mithilfe der Tag-Erweiterung „Web SDK&quot;

Es sind keine Debugging-Optionen verfügbar, die nativ die Tag-Erweiterung „Web SDK&quot; verwenden. Verwenden Sie [alternative Debugging-Methode](/help/collection/use-cases/debugging.md) beim Konfigurieren Ihrer Tag-Eigenschaft.
