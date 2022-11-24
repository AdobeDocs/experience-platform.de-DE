---
title: Gemeinsam genutzte Module für die Adobe Analytics-Erweiterung
description: Machen Sie sich mit den von der Tag-Erweiterung „Adobe Analytics“ in Adobe Experience Platform bereitgestellten Modulen für die gemeinsame Bibliothek vertraut.
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 100%

---

# Gemeinsam genutzte Module für die Adobe Analytics-Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Die [Adobe Analytics-Erweiterung](./overview.md) stellt zwei [gemeinsam genutzte Module](../../../extension-dev/web/shared.md) für die Integration in Ihre Erlebnisanwendung zur Auswahl. Diese Module werden im Folgenden erläutert.

## [!DNL get-tracker]

Bevor Adobe Analytics Beacons sendet, muss es das Tracker-Objekt initialisieren. Im Rahmen des Initialisierungsprozesses wird zunächst [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=de) geladen und anschließend ein Tracker-Objekt erstellt.

Sobald das Tracker-Objekt initialisiert wurde, können Sie darauf zugreifen, indem Sie das gemeinsam genutzte Modul `get-tracker` wie folgt verwenden:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### Überprüfen, ob Adobe Analytics installiert ist

Es ist möglich, dass Adobe Analytics nicht in derselben Tag-Bibliothek installiert oder enthalten ist wie Ihre Erweiterung. Daher wird dringend empfohlen, in Ihrem Code eine entsprechende Prüfung sowie das Vorgehen in einem solchen Fall zu implementieren. Umsetzen lässt sich dies etwa mit dem folgenden JavaScript:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

if (getTracker) {
  getTracker().then(function(tracker) {
    // Use tracker in some way
  });
} else {
  turbine.logger.error("The Adobe Analytics extension is required for Extension XYZ to function properly.");
}
```

Wenn `getTracker` den Wert `undefined` hat, ist die Adobe Analytics-Erweiterung ist in der Tag-Bibliothek nicht vorhanden. Sie können die Formulierung der Meldung so anpassen, dass sie genau vermittelt, welche Funktionen verloren gehen, wenn Adobe Analytics nicht installiert ist.


## [!DNL augment-tracker]

Nach Initialisierung des Tracker-Objekts besteht der nächsten Schritt im Prozess in der Augmentation. Mit diesem Schritt kann Ihre Erweiterung den Tracker mit allem Notwendigen erweitern, bevor Variablen aus der Adobe Analytics-Erweiterungskonfiguration angewendet oder Beacons gesendet wurden.

Darüber hinaus ist Ihre Erweiterung in der Lage, den Initialisierungsprozess des Trackers anzuhalten, während sie eine eigene asynchrone Aufgabe ausführt (z. B. das Abrufen von Daten oder JavaScript von einem Server).

Sie können das Modul `augment-tracker` wie folgt implementieren:

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

Die Funktion, die an `augmentTracker()` übergeben wird, wird aufgerufen, sobald die Augmentierungsphase des Initialisierungsprozesses des Trackers erreicht ist.

Wenn Ihre Erweiterung vor dem Augmentieren des Trackers eine asynchrone Aufgabe abschließen muss, können Sie einen Promise von Ihrer Funktion wie folgt zurückgeben:

```js
var Promise = require('@adobe/reactor-promise');
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  return new Promise(function(resolve) {
    // Augment the tracker object, then call resolve()
  });
});
```

Durch die Rückgabe eines Promise signalisiert Ihre Erweiterung Adobe Analytics, dass es den Initialisierungsprozess des Trackers anhalten sollte, bis der Promise eingelöst ist.

>[!WARNING]
>
>Beachten Sie jedoch, dass das Anhalten des Initialisierungsprozesses des Trackers dazu führen kann, dass Beacons mit Verzögerung gesendet werden und daher Daten nicht erfasst werden (wenn der Benutzer beispielsweise von der Seite weg navigiert, bevor das Beacon gesendet wird).
