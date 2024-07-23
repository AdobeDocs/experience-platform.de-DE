---
title: debugEnabled
description: Verwenden Sie Code, um Debugging-Funktionen im Web SDK zu aktivieren.
exl-id: 89392d16-9a0d-427b-86b6-70005f63f440
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

Mit der Eigenschaft `debugEnabled` können Sie das Debugging mithilfe des Web SDK-Codes aktivieren oder deaktivieren. Es ist eine der verfügbaren Möglichkeiten, das [Debugging](../../use-cases/debugging.md) zu aktivieren. Die Aktivierung des Debuggens in Ihrer Implementierung kann während der Website-Entwicklung praktischer sein als andere Methoden, wenn Sie das Debugging immer aktivieren möchten. Diese Debugging-Methode ermöglicht sie für alle Besucher, sodass sie nicht für Produktionsseiten empfohlen wird.

Weitere Möglichkeiten zum Aktivieren des Debuggens finden Sie auf der Seite mit den Anwendungsbeispielen für das [Debugging](../../use-cases/debugging.md) .

## Aktivieren des Debuggens mithilfe der Web SDK-Tag-Erweiterung

Es sind keine Debugging-Optionen verfügbar, die nativ mit der Web SDK-Tag-Erweiterung verwendet werden. Verwenden Sie eine [alternative Debugging-Methode](../../use-cases/debugging.md).

## Aktivieren des Debuggens mithilfe der Web SDK JavaScript-Bibliothek

Setzen Sie den booleschen Wert `debugEnabled` beim Ausführen des Befehls `configure` auf `true`. Wenn Sie diese Eigenschaft beim Konfigurieren des SDK weglassen, wird standardmäßig `false` verwendet.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```
