---
title: Ereignistypen für Web-Erweiterungen
description: Erfahren Sie, wie Sie ein Bibliotheksmodul vom Typ „event-type“ für eine Web-Erweiterung in Adobe Experience Platform definieren.
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 100%

---

# Ereignistypen für Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

In einer Tag-Regel ist ein Ereignis eine Aktivität, die auftreten muss, damit eine Regel ausgelöst wird. Beispielsweise könnte eine Erweiterung einen Ereignistyp „Geste“ bereitstellen, der überwacht, ob eine bestimmte Maus- oder Touch-Geste auftritt. Sobald die Geste auftritt, löst die Logik dieses Ereignisses die Regel aus.

Ein Ereignistyp-Bibliotheksmodul dient dazu, zu erkennen, wann eine Aktivität auftritt, und dann eine Funktion aufzurufen, um eine zugehörige Regel auszulösen. Das erkannte Ereignis kann angepasst werden. Er könnte etwa erkennen, wann ein Benutzer eine bestimmte Geste macht, schnell scrollt oder mit etwas interagiert.

In diesem Dokument wird beschrieben, wie Sie Ereignistypen für eine Web-Erweiterung in Adobe Experience Platform definieren.

>[!NOTE]
>
>In diesem Dokument wird davon ausgegangen, dass Sie mit Bibliotheksmodulen und deren Integration in Web-Erweiterungen vertraut sind. Lesen Sie zunächst den Überblick über die [Formatierung von Bibliotheksmodulen](./format.md), der eine Einführung in deren Implementierung bietet, bevor Sie zu dieser Anleitung zurückkehren.

Ereignistypen werden durch Erweiterungen definiert und bestehen normalerweise aus folgenden Elementen:

1. Eine [Ansicht](./views.md), die in der Datenerfassungs-Benutzeroberfläche angezeigt wird und es Benutzern ermöglicht, die Einstellungen für das Ereignis zu ändern.
2. Ein Bibliotheksmodul, das in der Tag-Laufzeitbibliothek ausgegeben wird, um die Einstellungen zu interpretieren und um zu überwachen, ob eine bestimmte Aktivität eintritt.

`module.exports` akzeptieren die Parameter `settings` und `trigger`. Dies ermöglicht die Anpassung des Ereignistyps.

```js
module.exports = function(settings, trigger) { … };
```

| Parameter | Beschreibung |
| --- | --- |
| `settings` | Ein Objekt, das alle vom Benutzer in der Ansicht des Ereignistyps konfigurierten Einstellungen enthält. Sie haben die ultimative Kontrolle darüber, was in diesem Objekt enthalten ist. |
| `trigger` | Eine Funktion, die das Modul bei jedem Auslösen der Regel aufrufen sollte. Es besteht eine Eins-zu-eins-Beziehung zwischen einem `settings`-Objekt, einer `trigger`-Funktion und einer Regel. Mit anderen Worten, die Auslöserfunktion, die Sie für eine bestimmte Regel erhalten haben, kann nicht zum Auslösen einer anderen Regel verwendet werden. |

>[!NOTE]
>
>Die exportierte Funktion wird für jede Regel, die für die Verwendung Ihres Ereignistyps konfiguriert wurde, nur einmal aufgerufen.

Anhand der Aktivität von fünf Sekunden, die als Beispiel verwendet wird, hat die Aktivität stattgefunden und die Regel wird ausgelöst, nachdem fünf Sekunden vergangen sind. Das Modul sieht in etwa wie im folgenden Beispiel aus.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

Wenn Sie möchten, dass die Dauer vom Adobe Experience Platform-Benutzer konfiguriert werden kann, ist die Option zum Eingeben und Speichern einer Dauer im Einstellungsobjekt erforderlich. Das Objekt könnte etwa so aussehen:

```js
{
  "duration": 25000
}
```

Um mit der benutzerdefinierten Dauer arbeiten zu können, muss unser Modul so aktualisiert werden, dass es diese enthält.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## Weitergeben kontextueller Ereignisdaten

Wenn eine Regel ausgelöst wird, ist es oft nützlich, zusätzliche Details über das eingetretene Ereignis bereitzustellen. Benutzer, die Regeln erstellen, können diese Informationen nützlich finden, um ein bestimmtes Verhalten zu erreichen. Nehmen wir beispielsweise an, dass ein Marketer eine Regel erstellen möchte, bei der jedes Mal, wenn der Benutzer über den Bildschirm wischt, ein Analyse-Beacon gesendet wird. Die Erweiterung muss einen Ereignistyp `swipe` bereitstellen, damit der Marketer diesen Ereignistyp zum Auslösen der entsprechenden Regel verwenden kann. Wenn der Marketer den Winkel einbeziehen möchte, in dem die Wischbewegung auf dem Beacon stattgefunden hat, wäre dies ohne zusätzliche Informationen schwer zu erreichen. Um weitere Informationen zum aufgetretenen Ereignis bereitzustellen, übergeben Sie beim Aufrufen der Funktion `trigger` ein Objekt. Beispiel:

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

Der Werbungtreibende könnte diesen Wert dann in einem Analytics-Beacon verwenden, indem er den Wert `%event.swipeAngle%` in einem Textfeld angibt. Er könnte auch von anderen Kontexten aus auf `event.swipeAngle` zugreifen (z. B. eine benutzerdefinierte Code-Aktion). Es ist möglich, andere Arten optionaler Ereignisinformationen einzuschließen, die für einen Marketer auf die gleiche Weise nützlich sein können.

### [!DNL nativeEvent]

Wenn Ihr Ereignistyp auf einem nativen Ereignis basiert (z. B. wenn Ihre Erweiterung einen `click`-Ereignistyp übermittelt hat) wird empfohlen, die `nativeEvent`-Eigenschaft wie folgt festzulegen.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

Dies kann für Werbungtreibende nützlich sein, die auf Informationen aus dem nativen Ereignis zugreifen möchten, z. B. Cursor-Koordinaten.

### [!DNL element]

Wenn eine starke Beziehung zwischen einem Element und dem aufgetretenen Ereignis besteht, wird empfohlen, die `element`-Eigenschaft auf den DOM-Knoten des Elements festzulegen. Ein Beispiel: Ihre Nebenstelle übermittelt einen `click`-Ereignistyp und Sie bieten Marketern die Möglichkeit, ihn so zu konfigurieren, dass die Regel nur ausgelöst wird, wenn ein Element mit der ID `herobanner` ausgewählt ist. Wenn der Benutzer in diesem Fall das Hero-Banner auswählt, wird empfohlen, `trigger` aufzurufen und `element` auf den DOM-Knoten des Hero-Banners festzulegen.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## Einhalten der Regelreihenfolge

Mit Tags können Benutzer Regeln anordnen. Zum Beispiel könnte ein Benutzer zwei Regeln erstellen, die beide den Ereignistyp „Orientierungsänderung“ nutzen, und der Benutzer möchte die Reihenfolge, in der die Regeln ausgelöst werden, anpassen können. Angenommen, der Adobe Experience Platform-Benutzer gibt einen Ordnungswert von `2` für das Ausrichtungsänderungsereignis in Regel A und einen Ordnungswert von `1` für das Ausrichtungsänderungsereignis in Regel B an. Dies bedeutet, dass bei einer Ausrichtungsänderung auf einem Mobilgerät Regel B vor Regel A ausgelöst werden soll (Regeln mit Werten niedrigerer Ordnung werden zuerst ausgelöst).

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
