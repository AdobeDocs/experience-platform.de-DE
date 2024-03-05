---
title: debugEnabled
description: Verwenden Sie Code, um Debugging-Funktionen im Web SDK zu aktivieren.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# `debugEnabled`

Die `debugEnabled` -Eigenschaft können Sie das Debugging mit Web SDK-Code aktivieren oder deaktivieren. Es ist eine der verfügbaren Möglichkeiten, [Debugging](../../use-cases/debugging.md). Die Aktivierung des Debuggens in Ihrer Implementierung kann während der Website-Entwicklung praktischer sein als andere Methoden, wenn Sie das Debugging immer aktivieren möchten. Diese Debugging-Methode ermöglicht sie für alle Besucher, sodass sie nicht für Produktionsseiten empfohlen wird.

Siehe [Debugging](../../use-cases/debugging.md) Anwendungsfallseite finden Sie weitere Möglichkeiten, das Debugging zu aktivieren.

## Aktivieren des Debuggens mithilfe der Web SDK-Tag-Erweiterung

Es sind keine Debugging-Optionen verfügbar, die nativ mit der Web SDK-Tag-Erweiterung verwendet werden. Verwenden Sie eine [alternative Debugging-Methode](../../use-cases/debugging.md).

## Aktivieren des Debuggens mithilfe der JavaScript-Bibliothek des Web SDK

Legen Sie die `debugEnabled` boolean to `true` beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft beim Konfigurieren des SDK weglassen, wird standardmäßig `false`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```
