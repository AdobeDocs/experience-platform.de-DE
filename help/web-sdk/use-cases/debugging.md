---
title: Debugging-Methoden
description: Erfahren Sie, wie Sie Debugging-Funktionen im Web SDK umschalten.
keywords: Debugging von Web SDK;Debugging;Konfigurieren;Befehl konfigurieren;Debugging-Befehl;edgeConfigId;setDebug;debugEnabled;debug;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Debugging-Methoden

Wenn das Debugging aktiviert ist, gibt das Web SDK Meldungen an die Browser-Konsole aus, die beim Debugging Ihrer Implementierung hilfreich sein können. Das Debugging ist nützlich, wenn Sie wissen möchten, wie sich das SDK gemäß den von Ihnen festgelegten Regeln und Datenelementen verhält.

Das Debugging ist standardmäßig deaktiviert, kann jedoch auf vier verschiedene Arten aktiviert werden. Sie können eine beliebige Kombination dieser Methoden verwenden, um das Debugging zu aktivieren oder zu deaktivieren, das für Ihren Entwicklungs-Workflow am bequemsten ist.

## Verwendung `debugEnabled` im `configure` command

Legen Sie die `debugEnabled` boolesch auf &quot;true&quot;fest, wenn die Erweiterung konfiguriert wird. Diese Option wird normalerweise für Entwicklungsumgebungen verwendet, da sie das Debugging für alle Besucher einer beliebigen Seite Ihrer Site ermöglicht:

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

Siehe [`debugEnabled`](../commands/configure/debugenabled.md) für weitere Informationen.

## Verwenden Sie die `setDebug` command

Ähnlich wie der obige boolesche Befehl ermöglicht dieser Befehl das Debugging über alle Besucher der Seite hinweg.

```js
alloy("setDebug", {"enabled": true});
```

Siehe [`setDebug`](../commands/setdebug.md) für weitere Informationen.

## Abfragezeichenfolgenparameter festlegen

Sie können das Debugging aktivieren, indem Sie die Abfragezeichenfolge hinzufügen `?alloy_debug=true` an das Ende einer beliebigen URL. Beispiel:

`http://example.com/?alloy_debug=true`

Diese Methode gilt nur für Ihren lokalen Computer, sodass Sie Produktions-Websites debuggen können, ohne das Debugging für alle zu aktivieren. Die Aktivierung des Debuggens auf diese Weise bleibt für den Rest der Browser-Sitzung aktiviert oder bis Sie sie deaktivieren.

## Verwenden des Adobe Experience Platform Debuggers

Der Adobe Experience Platform Debugger ist ein leistungsstarkes Tool, das Ihre Webseiten überprüft und Ihnen dabei hilft, Ihre Implementierung von Experience Cloud-Produkten zu debuggen. Sie können das Debugging auf der Registerkarte &quot;Konfiguration&quot;des AEP Web SDK-Abschnitts aktivieren.

![Aktivieren des Debuggers](../assets/enable-debugging.png)

Siehe [Übersicht über Adobe Experience Platform Debugger](/help/debugger/home.md) für weitere Informationen.
