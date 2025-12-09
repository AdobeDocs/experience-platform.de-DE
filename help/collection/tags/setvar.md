---
title: setVar()
description: Legt einen Wert fest, den Sie später mit getVar() abrufen können.
source-git-commit: 54c32803136bf37a13bb9ca14b1d1c7b09a2041c
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# `setVar()`

Mit der `_satellite.setVar()`-Methode können Sie ein oder mehrere benutzerdefinierte Name/Wert-Paare festlegen, auf die später von [`_satellite.getVar()`](getvar.md) verwiesen werden kann.

```ts
// Set a single name/value pair
_satellite.setVar(name: string, value: unknown): void

// Set multiple name/value pairs at once
_satellite.setVar(vars: { [name: string]: unknown }): void;
```

>[!IMPORTANT]
>
>Während die `getVar()`-Methode sowohl Datenelemente als auch von `setVar()` festgelegte Werte abrufen kann, sind diese beiden Entitätstypen getrennt. Wenn Sie `setVar()` verwenden, um einen Wert mit demselben Namen wie ein Datenelement in der Tags-Benutzeroberfläche festzulegen, wird dieser nicht überschrieben.

## Persistenz und Umfang

`setVar()` Werte sind nur im Seitenspeicher verfügbar:

* **Nur aktuelle Seite**: Die Werte bleiben so lange bestehen, bis die Seite entladen wird. In Einzelseitenanwendungen bleiben sie erhalten, bis sie vollständig neu geladen oder überschrieben/gelöscht werden.
* **Kein Browser-**: Es wird nichts in Cookies, den lokalen Speicher oder den Sitzungsspeicher geschrieben.

## Referenzieren von Werten, die mithilfe von `setVar()` festgelegt wurden

Sie können Werte in benutzerdefiniertem Code mit `getVar()` abrufen:

```js
// Set a custom variable using setVar()
_satellite.setVar('Ad location','Banner advertisement');

// Returns the string 'Banner advertisement'
_satellite.getVar('Ad location');
```

Sie können diese Variablen auch in der Tags-Benutzeroberfläche in Feldern referenzieren, die die Datenelementnotation unterstützen:

```text
%Ad location%
```

>[!NOTE]
>
>Wenn ein Wert, der mithilfe von `setVar()` festgelegt wird, denselben Namen wie ein Datenelement verwendet und Sie in der Datenelementnotation auf diesen Namen verweisen, hat das Datenelement Vorrang.

## Beispiele

```js
// Set a single name/value pair
_satellite.setVar('product', 'Circuit Pro');

// Set multiple name/value pairs at once (same as calling setVar() three times)
_satellite.setVar({ 'title': 'Blinding Light', 'category': 'Game', 'genre': 'Tower defense' });

// Retrieve each value
_satellite.getVar('title'); // Blinding Light
_satellite.getVar('category'); // Game
_satellite.getVar('genre'); // Tower defense
```

>[!NOTE]
>
>Vermeiden Sie beim Festlegen von Variablennamen mit dieser Methode die Verwendung von Punkten (`.`). Die `getVar()` Methode erkennt keine Variablen, die Punkte enthalten, die mithilfe von `setVar()` festgelegt wurden. Datenelemente, die Punkte verwenden`getVar()` erkennt _jedoch_ wenn sie in der Tags-Benutzeroberfläche definiert sind.
