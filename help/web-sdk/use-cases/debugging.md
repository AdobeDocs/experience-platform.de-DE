---
title: Debugging-Methoden
description: Erfahren Sie, wie Sie die Debugging-Funktionen in der Web-SDK umschalten.
keywords: Debugging des Web SDK;Debugging;Debugging-Befehl;setDebug;debugEnabled;debug
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Debugging-Methoden

Wenn der Debugging-Modus aktiviert ist, gibt Web SDK Meldungen an die Browser-Konsole aus, die beim Debuggen Ihrer Implementierung hilfreich sein können. Das Debugging ist nützlich, wenn Sie verstehen möchten, wie sich die SDK gemäß den von Ihnen festgelegten Regeln und Datenelementen verhält.

Das Debugging ist standardmäßig deaktiviert, kann jedoch auf vier verschiedene Arten aktiviert werden. Sie können eine beliebige Kombination dieser Methoden verwenden, um das Debugging zu aktivieren oder zu deaktivieren, was für Ihren Entwicklungs-Workflow am bequemsten ist.

## Verwenden von `debugEnabled` im `configure`

Legen Sie beim Konfigurieren der Erweiterung den booleschen Wert `debugEnabled` auf „true“ fest. Diese Option wird normalerweise für Entwicklungsumgebungen verwendet, da sie Debugging für alle ermöglicht, die eine Seite auf Ihrer Site besuchen:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  debugEnabled: true
});
```

Weitere Informationen finden Sie unter [`debugEnabled`](../commands/configure/debugenabled.md) .

## Verwenden des Befehls `setDebug`

Ähnlich wie beim obigen booleschen Wert ermöglicht dieser Befehl das Debugging für alle Besucher der Seite.

```js
alloy("setDebug", {"enabled": true});
```

Weitere Informationen finden Sie unter dem Befehl [`setDebug`](../commands/setdebug.md) .

## Festlegen eines Abfragezeichenfolgenparameters

Sie können das Debugging aktivieren, indem Sie die Abfragezeichenfolgen-`?alloy_debug=true` am Ende einer beliebigen URL hinzufügen. z. B.:

`http://example.com/?alloy_debug=true`

Diese Methode gilt nur für Ihren lokalen Computer, sodass Sie Produktions-Websites debuggen können, ohne dass Debugging für alle aktiviert ist. Eine solche Aktivierung des Debugging-Modus bleibt für den Rest Ihrer Browsersitzung oder bis zur Deaktivierung aktiviert.

## Verwenden des Adobe Experience Platform Debuggers

Der Adobe Experience Platform Debugger ist ein leistungsstarkes Tool, das Ihre Web-Seiten untersucht und Sie bei der Fehlerbehebung bei der Implementierung von Experience Cloud-Produkten unterstützt. Sie können das Debugging über die Konfigurationsregisterkarte des Abschnitts AEP Web SDK aktivieren.

![Debugger aktivieren](../assets/enable-debugging.png)

Weitere Informationen finden Sie unter Übersicht über ](/help/debugger/home.md) Adobe Experience Platform Debugger .[
