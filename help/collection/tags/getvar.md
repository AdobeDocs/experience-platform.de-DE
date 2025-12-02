---
title: getVar()
description: Gibt den Wert eines Datenelements oder eines Werts zurück, der mithilfe von setVar() festgelegt wurde.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# `getVar()`

Die `_satellite.getVar()` Methode gibt den aktuellen Wert eines [Datenelements“ ](/help/tags/ui/managing-resources/data-elements.md) einen Wert zurück, der mithilfe von [`_satellite.setVar()`](setvar.md) festgelegt wurde. Wenn ein Datenelement und ein `setVar()` denselben Namen haben, hat das Datenelement Vorrang. Wenn Sie eine Zeichenfolgenkennung aufrufen, die noch nicht vorhanden ist, gibt die Methode `undefined` zurück. Die Auswertung erfolgt synchron.

```js
_satellite.getVar(name: string, event?: unknown) => unknown
```

Der Rückgabewert und der Typ hängen vom Datenelementtyp ab, auf den Sie verweisen. Wenn Sie beispielsweise `getVar()` aufrufen, das eine Zeichenfolgenvariable abruft, wird der zurückgegebene Typ `string`. Wenn Sie `getVar()` aufrufen, das ein Datenelement einer Web SDK-Variablen zurückgibt, ist der zurückgegebene Typ ein `object`, das alle in dieser Variablen festgelegten Eigenschaften enthält.

```js
// Retrieves the value in the `Example` data element
_satellite.getVar('Example');

// Execute custom logic depending on the numeric value in the `cartTotal` data element
const cartValue = Number(_satellite.getVar('cartTotal'));
if (cartValue > 100) {
  _satellite.logger.info('Purchase larger than $100 detected');
}

// Some data elements like Web SDK variables support deeply nested properties
const pageName = _satellite.getVar('Data layer')?.web?.webPageDetails?.name;
if (!pageName) {
  _satellite.logger.warn('Page name is not set');
}

// Custom code data elements support a second argument
// Works in a Launch custom code block where `event` is provided by the rule engine.
const rule = _satellite.getVar('Return event rule', event);
```

## Verfügbare Felder

Die `getVar()`-Methode unterstützt zwei Argumente. Die meisten Anwendungsfälle enthalten nicht das zweite optionale Argument.

| Name | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| **`name`** | `string` | Ja | Der Name des Datenelements, das Sie abrufen möchten. Bei Namen von Datenelementen wird zwischen Groß- und Kleinschreibung unterschieden. |
| **`event`** | `object` | Nein | Ereigniskontext aus der Auslöseregel. Wird nur in erweiterten Anwendungsfällen von Datenelementen verwendet, die [benutzerdefinierten Code](/help/tags/ui/managing-resources/data-elements.md#custom-code) oder benutzerdefinierte Erweiterungen verwenden. Wenn eine Regel durch ein Ereignis ausgelöst wird (z. B. ein Klick, eine Formularübermittlung oder einen benutzerdefinierten JavaScript-Dispatch), wird das zugehörige Ereignisobjekt hier eingeschlossen. Datenelemente können diese Informationen verwenden, um kontextuelle Werte zurückzugeben, z. B. die Details oder Eigenschaften des angeklickten Elements aus einem benutzerdefinierten Ereignis. |
