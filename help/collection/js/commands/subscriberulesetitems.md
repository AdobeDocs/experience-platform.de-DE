---
title: subscribeRulesetItems
description: Abonnieren von Inhaltskarten für eine bestimmte Oberfläche mit dem Befehl „subscribeRuleSetItems“.
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 4%

---

# `subscribeRulesetItems`

Mit dem Befehl `subscribeRulesetItems` können Sie Vorschläge abonnieren, die das Ergebnis erfüllter Regelsätze sind. Hierzu können Sie angeben, nach welchen Oberflächen und Schemata gefiltert werden soll, und eine Rückruffunktion bereitstellen.

Jedes Mal, wenn Regelsätze ausgewertet werden, empfängt die Callback-Funktion ein `result` mit einem Array von Vorschlägen darin.

>[!IMPORTANT]
>
>Der Befehl `subscribeRulesetItems` ist die einzige Möglichkeit, Vorschläge aus Regelsätzen abzurufen, da sie nicht zusammen mit [`sendEvent`](sendevent/overview.md) Ergebnissen zurückgegeben werden.


```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://example.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```

Der obige Code abonniert die `web://example.com/#welcome` für Inhaltskarten und verwendet die `collectEvent` Convenience-Methode, um `display` Ereignisse für alle Vorschläge auszugeben.

## Befehlsoptionen {#command-options}

Dieser Befehl akzeptiert ein `options` mit den folgenden Eigenschaften:

| Eigenschaft | Typ | Beschreibung |
| --- | --- | --- |
| `surfaces` | Zeichenfolgen-Array | Eine Liste von Oberflächen. Vorschläge werden von der Callback-Funktion nur dann empfangen, wenn sie mit einer der hier bereitgestellten Oberflächen übereinstimmen. |
| `schemas` | Zeichenfolgen-Array | Eine Liste von Schemata. Vorschläge werden nur dann von der Callback-Funktion empfangen, wenn sie mit einem der hier bereitgestellten Schemata übereinstimmen. |
| `callback` | Funktion | Eine Callback-Funktion, die aufgerufen wird, wenn Vorschläge das Ergebnis erfüllter Regelsätze sind. Die Rückruffunktion erhält zwei Parameter, wenn sie aufgerufen wird: `result` und `collectEvent`. Siehe [Callback-Parameter](#callback-parameters) für Details. |

### Callback-Parameter {#callback-parameters}

Die Rückruffunktion empfängt beim Aufrufen die beiden in der folgenden Tabelle beschriebenen Parameter.

| Parameter | Typ | Beschreibung |
| --- | --- | --- |
| `result` | Objekt | Dieses Objekt enthält ein `propositions`-Array.  Diese Vorschläge sind das direkte Ergebnis von zufriedenen Regelsätzen. Das `result`-Objekt ist genauso strukturiert wie das [Ergebnisobjekt](command-responses.md) das von `sendEvent` mit einer `then` -Klausel zurückgegeben wird. |
| `collectEvent` | Funktion | Eine praktische Funktion, mit der Sie Edge Network-Ereignisse senden können, um Interaktionen, Anzeigen und andere Ereignisse zu verfolgen. |

### `collectEvent`-Funktion {#collectevent-function}

Die Funktion `collectEvent` ist eine praktische Funktion, mit der Sie Edge Network-Ereignisse senden können, um Interaktionen, Anzeigen und andere Ereignisse zu verfolgen. Sie akzeptiert die beiden in der folgenden Tabelle beschriebenen Parameter.

| Parameter | Typ | Beschreibung |
| --- | --- | --- |
| Ereignistyp | String | Eine Zeichenfolge, die angibt, welcher Vorschlagsereignistyp ausgegeben werden soll. Unterstützte Ereignistypen sind `display`, `interact` oder `dismiss`. |
| `propositions` | Array | Ein Array von Vorschlägen, die dem Ereignis entsprechen. |

## Abonnieren von Inhaltskarten mit der Tag-Erweiterung Web SDK

Die Web-SDK-Tag-Erweiterung, die Befehlsantworten entspricht, ist eine Regel, die das [**[!UICONTROL Subscribe ruleset items]**](/help/tags/extensions/client/web-sdk/event-types.md#subscribe-ruleset-items) abonniert. Mit dem Ereignis können Sie die gewünschten Schemas und Oberflächen bereitstellen.
