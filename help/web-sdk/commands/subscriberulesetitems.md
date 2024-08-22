---
title: subscribeRulesetItems
description: Abonnieren Sie mit dem Befehl subscribeRulesetItems Inhaltskarten für eine bestimmte Oberfläche.
source-git-commit: 01cba985e22e4673fb60721c810ac9cbee287386
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---


# `subscribeRulesetItems`

Mit dem Befehl `subscribeRulesetItems` können Sie Vorschläge abonnieren, die das Ergebnis zufrieden stellender Regelsätze sind. Dazu können Sie angeben, nach welchen Oberflächen und Schemata gefiltert werden soll, und eine Rückruffunktion bereitstellen.

Jedes Mal, wenn Regelsätze ausgewertet werden, empfängt die Callback-Funktion ein `result` -Objekt mit einem Array von Vorschlägen darin.

>[!IMPORTANT]
>
>Der Befehl `subscribeRulesetItems` ist die einzige Möglichkeit, Vorschläge zu erhalten, die aus Regelsätzen stammen, da sie nicht zusammen mit [`sendEvent`](sendevent/overview.md) Ergebnissen zurückgegeben werden.

## Komprimierungsoptionen {#command-options}

Dieser Befehl akzeptiert ein `options` -Objekt mit den folgenden Eigenschaften:

| Eigenschaft | Typ | Beschreibung |
| --- | --- | --- |
| `surfaces` | Zeichenfolgen-Array | Eine Liste der Oberflächen. Vorschläge werden nur von der Callback-Funktion empfangen, wenn sie mit einer der hier angegebenen Oberflächen übereinstimmen. |
| `schemas` | Zeichenfolgen-Array | Eine Liste von Schemas. Vorschläge werden nur von der Callback-Funktion empfangen, wenn sie mit einem der hier angegebenen Schemas übereinstimmen. |
| `callback` | Funktion | Eine Callback-Funktion, die aufgerufen wird, wenn Vorschläge das Ergebnis erfüllter Regelsätze sind. Die Callback-Funktion empfängt beim Aufrufen zwei Parameter: `result` und `collectEvent`. Weitere Informationen finden Sie unter [Rückrufparameter](#callback-parameters) . |

### Callback-Parameter {#callback-parameters}

Die Callback-Funktion empfängt beim Aufrufen die beiden in der folgenden Tabelle beschriebenen Parameter.

| Parameter | Typ | Beschreibung |
| --- | --- | --- |
| `result` | Objekt | Dieses Objekt enthält ein `propositions` -Array.  Diese Vorschläge sind das direkte Ergebnis zufrieden stellender Regelsätze. Das `result` -Objekt ist genauso strukturiert wie das [result -Objekt](command-responses.md), das von `sendEvent` mit einer `then` -Klausel zurückgegeben wird. |
| `collectEvent` | Funktion | Eine bequeme Funktion, mit der Sie Edge Network-Ereignisse senden können, um Interaktionen, Anzeigen und andere Ereignisse zu verfolgen. |

### `collectEvent`-Funktion {#collectevent-function}

Die Funktion `collectEvent` ist eine praktische Funktion, mit der Sie Edge Network-Ereignisse senden können, um Interaktionen, Anzeigen und andere Ereignisse zu verfolgen. Es akzeptiert die beiden in der folgenden Tabelle beschriebenen Parameter.

| Parameter | Typ | Beschreibung |
| --- | --- | --- |
| Ereignistyp | String | Eine Zeichenfolge, die angibt, welcher Vorschlagsereignistyp ausgegeben werden soll. Unterstützte Ereignistypen sind `display`, `interact` oder `dismiss`. |
| `propositions` | Array | Ein Array von Vorschlägen, die dem Ereignis entsprechen. |

## Abonnieren von Inhaltskarten mit der Web SDK-Tag-Erweiterung {#tag-extension}

Gehen Sie wie folgt vor, um über die Benutzeroberfläche &quot;Tags&quot;Inhaltskarten zu abonnieren.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Ereignisse] ein vorhandenes Ereignis aus oder erstellen Sie ein neues.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und setzen Sie den **[!UICONTROL Ereignistyp]** auf **[!UICONTROL Regelsatzelemente abonnieren]**.
1. Wählen Sie rechts im Bildschirm die Schemata und Oberflächen aus, für die Sie Inhaltskarten abonnieren möchten.
1. Wählen Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Abonnieren von Inhaltskarten mit der Web SDK JavaScript-Bibliothek {#library}

Der folgende Beispielcode abonniert die `web://mywebsite.com/#welcome` -Oberfläche für Inhaltskarten und verwendet die `collectEvent`-Convenience-Methode, um `display` -Ereignisse für alle Vorschläge auszugeben.

```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://mywebsite.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```
