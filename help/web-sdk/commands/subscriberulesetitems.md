---
title: subscribeRulesetItems
description: Abonnieren von Inhaltskarten für eine bestimmte Oberfläche mit dem Befehl „subscribeRuleSetItems“.
exl-id: bc932ba5-a810-4fa6-82cc-998af39fdd34
source-git-commit: d9e9275db1989df22b13b4f000dde645f40d5744
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# `subscribeRulesetItems`

Mit dem Befehl `subscribeRulesetItems` können Sie Vorschläge abonnieren, die das Ergebnis erfüllter Regelsätze sind. Hierzu können Sie angeben, nach welchen Oberflächen und Schemata gefiltert werden soll, und eine Rückruffunktion bereitstellen.

Jedes Mal, wenn Regelsätze ausgewertet werden, empfängt die Callback-Funktion ein `result` mit einem Array von Vorschlägen darin.

>[!IMPORTANT]
>
>Der Befehl `subscribeRulesetItems` ist die einzige Möglichkeit, Vorschläge aus Regelsätzen abzurufen, da sie nicht zusammen mit [`sendEvent`](sendevent/overview.md) Ergebnissen zurückgegeben werden.

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
| `collectEvent` | Funktion | Eine Komfortfunktion, mit der Sie Edge Network-Ereignisse senden können, um Interaktionen, Anzeigen und andere Ereignisse zu verfolgen. |

### `collectEvent`-Funktion {#collectevent-function}

Die Funktion `collectEvent` ist eine praktische Funktion, mit der Sie Ereignisereignisse senden können, um Edge Networks, Anzeigen und andere Ereignisse zu verfolgen. Sie akzeptiert die beiden in der folgenden Tabelle beschriebenen Parameter.

| Parameter | Typ | Beschreibung |
| --- | --- | --- |
| Ereignistyp | String | Eine Zeichenfolge, die angibt, welcher Vorschlagsereignistyp ausgegeben werden soll. Unterstützte Ereignistypen sind `display`, `interact` oder `dismiss`. |
| `propositions` | Array | Ein Array von Vorschlägen, die dem Ereignis entsprechen. |

## Abonnieren von Inhaltskarten mit der Tag-Erweiterung Web SDK {#tag-extension}

Gehen Sie wie folgt vor, um Inhaltskarten über die Benutzeroberfläche für Tags zu abonnieren.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL &#x200B; unter &quot;]&quot; ein vorhandenes Ereignis aus oder erstellen Sie ein neues.
1. Legen Sie das [!UICONTROL Erweiterung] Dropdown-Feld auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und setzen Sie den **[!UICONTROL Ereignistyp]** auf **[!UICONTROL Regelsatzelemente abonnieren]**.
1. Wählen Sie rechts im Bildschirm die Schemata und Oberflächen aus, für die Sie Inhaltskarten abonnieren möchten.
1. Wählen **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

## Abonnieren von Inhaltskarten mit der Web SDK JavaScript Library {#library}

Der folgende Beispiel-Code abonniert die `web://mywebsite.com/#welcome` für Inhaltskarten und verwendet die `collectEvent` Convenience-Methode zum Ausgeben `display` Ereignisse für alle Vorschläge.

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
