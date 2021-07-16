---
title: Ereignistypen für Web-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul für Ereignistypen für eine Web-Erweiterung in Adobe Experience Platform definieren.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 42%

---

# Ereignistypen

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Ein Ereignistyp-Bibliotheksmodul dient dazu, zu erkennen, wann eine Aktivität auftritt, und dann eine Funktion aufzurufen, um eine zugehörige Regel auszulösen. Das erkannte Ereignis kann angepasst werden. Es kann erkennen, wann ein Benutzer eine bestimmte Geste macht, schnell scrollt oder mit etwas interagiert?

>[!NOTE]
>
>In diesem Dokument wird davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Tag-Erweiterungen vertraut sind. Lesen Sie zunächst den Überblick über die [Formatierung von Bibliotheksmodulen](./format.md), der eine Einführung in deren Implementierung bietet, bevor Sie zu dieser Anleitung zurückkehren.

`module.exports` die  `settings` Parameter  `trigger` und akzeptieren. Dies ermöglicht die Anpassung des Ereignistyps.

```js
module.exports = function(settings, trigger) { … };
```

| Parameter | Beschreibung |
| --- | --- |
| `settings` | Ein Objekt, das alle vom Benutzer in der Ansicht des Ereignistyps konfigurierten Einstellungen enthält. Sie haben die ultimative Kontrolle darüber, was in diesem Objekt enthalten ist. |
| `trigger` | Eine Funktion, die das Modul bei jedem Auslösen der Regel aufrufen sollte. Es gibt eine Eins-zu-Eins-Beziehung zwischen einem `settings`-Objekt, einer `trigger`-Funktion und einer Regel. Das bedeutet, dass die Regelfunktion, die Sie für eine Trigger erhalten haben, nicht zum Auslösen einer anderen Regel verwendet werden kann. |

>[!NOTE]
>
>Die exportierte Funktion wird für jede Regel, die für die Verwendung Ihres Ereignistyps konfiguriert wurde, nur einmal aufgerufen.

Anhand der Aktivität von fünf Sekunden, die als Beispiel verwendet wird, hat die Aktivität stattgefunden und die Regel wird ausgelöst, nachdem fünf Sekunden vergangen sind. Das Modul sieht in etwa wie im folgenden Beispiel aus.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

Wenn Sie möchten, dass die Dauer vom Adobe Experience Platform-Benutzer konfiguriert werden kann, ist die Option zum Eingeben und Speichern einer Dauer im settings-Objekt erforderlich. Das Objekt könnte etwa so aussehen:

```js
{
  "duration": 25000
}
```

Um mit der benutzerdefinierten Dauer arbeiten zu können, muss das Modul aktualisiert werden, um dies einzuschließen.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## Weiterleiten von Kontextereignisdaten

Wenn eine Regel ausgelöst wird, ist es oft nützlich, zusätzliche Details über das eingetretene Ereignis bereitzustellen. Benutzer, die Regeln erstellen, können diese Informationen nützlich finden, um ein bestimmtes Verhalten zu erreichen. Wenn beispielsweise ein Marketing-Experte eine Regel erstellen möchte, bei der jedes Mal, wenn der Benutzer den Bildschirm wischt, ein Analytics-Beacon gesendet wird. Die Erweiterung muss einen Ereignistyp `swipe` bereitstellen, damit der Marketingexperte diesen Ereignistyp zum Trigger der entsprechenden Regel verwenden kann. Wenn der Marketingexperte den Winkel einbeziehen möchte, in dem die Wischbewegung im Beacon stattgefunden hat, wäre dies schwierig, ohne zusätzliche Informationen bereitzustellen. Um weitere Informationen zum aufgetretenen Ereignis bereitzustellen, übergeben Sie beim Aufrufen der Funktion `trigger` ein Objekt. Beispiel:

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

Der Werbungtreibende könnte diesen Wert dann in einem Analytics-Beacon verwenden, indem er den Wert `%event.swipeAngle%` in einem Textfeld angibt. Er könnte auch von anderen Kontexten aus auf `event.swipeAngle` zugreifen (z. B. eine benutzerdefinierte Code-Aktion). Es ist möglich, andere Arten optionaler Ereignisinformationen einzuschließen, die für einen Marketing-Experten auf die gleiche Weise nützlich sein können.

### [!DNL nativeEvent]

Wenn Ihr Ereignistyp auf einem nativen Ereignis basiert (z. B. wenn Ihre Erweiterung einen `click` -Ereignistyp bereitstellt), wird empfohlen, die `nativeEvent` -Eigenschaft wie folgt festzulegen.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

Dies kann für Werbungtreibende nützlich sein, die auf Informationen aus dem nativen Ereignis zugreifen möchten, z. B. Cursor-Koordinaten.

### [!DNL element]

Wenn eine starke Beziehung zwischen einem Element und dem aufgetretenen Ereignis besteht, wird empfohlen, die Eigenschaft `element` auf den DOM-Knoten des Elements festzulegen. Wenn Ihre Erweiterung beispielsweise den Ereignistyp `click` bereitstellt und Sie es Marketing-Experten ermöglichen, ihn so zu konfigurieren, dass die Regel nur ausgelöst wird, wenn ein Element mit der ID `herobanner` ausgewählt ist. Wenn der Benutzer in diesem Fall das Hero-Banner auswählt, wird empfohlen, `trigger` aufzurufen und `element` auf den DOM-Knoten des Hero-Banners festzulegen.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## Einhalten der Regelreihenfolge

Mit Tags in Adobe Experience Platform können Benutzer Regeln anordnen. Beispielsweise kann ein Benutzer zwei Regeln erstellen, die sowohl den Ereignistyp orientation-change als auch die Reihenfolge verwenden, in der die Regeln ausgelöst werden. Angenommen, der Adobe Experience Platform-Benutzer gibt für das Orientierungsänderungsereignis in Regel A den Anordnungswert `2` und für das Orientierungsänderungsereignis in Regel B den Anordnungswert `1` an. Dies bedeutet, dass Regel B vor Regel A ausgelöst werden sollte, wenn sich die Ausrichtung auf einem Mobilgerät ändert (Regeln mit niedrigeren Anordnungswerten werden zuerst ausgelöst).

Wie bereits erwähnt, wird die Exportfunktion in unserem Ereignismodul für jede Regel, die für die Verwendung unseres Ereignistyps konfiguriert wurde, genau einmal aufgerufen. Bei jedem Aufruf der exportierten Funktion wird eine eindeutige `trigger`-Funktion übergeben, die mit einer bestimmten Regel verknüpft ist. Im oben beschriebenen Szenario wird unsere exportierte Funktion einmal mit einer `trigger`-Funktion aufgerufen, die an Regel B gebunden ist, und dann erneut mit einer `trigger`-Funktion, die an Regel A gebunden ist. Regel B kommt zuerst, weil der Benutzer ihr einen geringeren Anordnungswert als Regel A gegeben hat. Wenn unser Bibliotheksmodul eine Änderung der Ausrichtung erkennt, ist es wichtig, dass die `trigger`-Funktionen in der gleichen Reihenfolge aufgerufen werden, in der sie dem Bibliotheksmodul bereitgestellt wurden.

Beachten Sie im folgenden Beispiel-Code, dass bei Erkennung einer Ausrichtungsänderung die Auslöserfunktionen in der gleichen Reihenfolge aufgerufen werden, in der sie für unsere Exportfunktion bereitgestellt wurden:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Dadurch wird sichergestellt, dass die vom Benutzer angegebene Reihenfolge beibehalten wird.

Bei einer fehlerhaften Implementierung werden die Auslöserfunktionen in einer anderen Reihenfolge aufgerufen:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Natürliche Programmierungspraktiken behalten in der Regel die richtige Reihenfolge bei, aber es ist wichtig, sich der Auswirkungen bewusst zu sein und entsprechend zu entwickeln.
