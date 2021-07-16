---
title: Freie turbine-Variable
description: Erfahren Sie mehr über das Turbinenobjekt, eine freie Variable, die Informationen und Dienstprogramme bereitstellt, die für die Adobe Experience Platform-Tag-Laufzeit spezifisch sind.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 58%

---

# Freie turbine-Variable

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

Das `turbine`-Objekt ist eine „freie Variable“ im Gültigkeitsbereich der Bibliotheksmodule Ihrer Erweiterung. Es stellt Informationen und Dienstprogramme bereit, die spezifisch für die Tag-Laufzeit von Adobe Experience Platform sind, und ist immer für Bibliotheksmodule verfügbar, ohne `require()` zu verwenden.

## [!DNL buildInfo]

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` ist ein Objekt, das Build-Informationen zur aktuellen Tag-Laufzeitbibliothek enthält.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z",
    environment: "development"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `turbineVersion` | Die in der aktuellen Bibliothek verwendete [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine)-Version. |
| `turbineBuildDate` | Das ISO-8601-Datum, an dem die im aktuellen Container verwendete [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine)-Version erstellt wurde. |
| `buildDate` | Das ISO-8601-Datum, an dem die aktuelle Bibliothek erstellt wurde. |
| `environment` | Die Umgebung, für die diese Bibliothek erstellt wurde. Zulässige Werte sind `development`, `staging` und `production`. |


## [!DNL debugEnabled]

Gibt an, ob das Tag-Debugging derzeit aktiviert ist.

Wenn Sie einfach Meldungen protokollieren möchten, ist es unwahrscheinlich, dass Sie dies verwenden müssen. Protokollieren Sie stattdessen Nachrichten immer mit `turbine.logger`, um sicherzustellen, dass Ihre Nachrichten nur dann in der Konsole gedruckt werden, wenn das Tag-Debugging aktiviert ist.

### [!DNL getDataElementValue]

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Gibt den Wert eines Datenelements zurück.

### [!DNL getExtensionSettings] {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Gibt das settings-Objekt zurück, das zuletzt in der Ansicht für die [Erweiterungskonfiguration](./configuration.md) gespeichert wurde.

Beachten Sie, dass die Werte in den zurückgegebenen settings-Objekten möglicherweise von Datenelementen stammen. Deshalb kann der Aufruf von `getExtensionSettings()` zu unterschiedlichen Zeitpunkten zu unterschiedlichen Ergebnissen führen, wenn sich die Werte der Datenelemente geändert haben. Um die aktuellsten Werte zu erhalten, warten Sie so lange wie möglich, bevor Sie `getExtensionSettings()` aufrufen.

### [!DNL getHostedLibFileUrl] {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

Die Eigenschaft [hostedLibFiles](./manifest.md) kann innerhalb des Erweiterungsmanifests definiert werden, um verschiedene Dateien zusammen mit der Tag-Laufzeitbibliothek zu hosten. Dieses Modul gibt die URL zurück, unter der die angegebene Bibliotheksdatei gehostet wird.

### [!DNL getSharedModule] {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Ruft ein Modul ab, das von einer anderen Erweiterung freigegeben wurde. Wenn kein passendes Modul gefunden wird, wird `undefined` zurückgegeben. Weitere Informationen zu freigegebenen Modulen finden Sie unter [Implementieren freigegebener Module](./web/shared.md).

### [!DNL logger]

```js
turbine.logger.error('Error!');
```

Das Protokollierungsdienstprogramm wird verwendet, um Meldungen in der Konsole zu protokollieren. Meldungen werden nur dann auf der Konsole angezeigt, wenn der Benutzer den Debugging-Modus aktiviert hat. Die empfohlene Methode zum Aktivieren des Debugging-Modus besteht darin, [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda) oder [ Launch und DTM Switch](https://chrome.google.com/webstore/detail/adobe-dtm-switch/nlgdemkdapolikbjimjajpmonpbpmipk) als Chrome-Erweiterung zu verwenden. Alternativ kann der Benutzer den folgenden Befehl `_satellite.setDebug(true)` in der Browser-Entwicklerkonsole ausführen. Die logger-Funktion verfügt über die folgenden Methoden:

* `logger.log(message: string)`: Protokolliert eine Meldung auf der Browser-Konsole.
* `logger.info(message: string)`: Protokolliert eine Informationsmeldung auf der Konsole.
* `logger.warn(message: string)`: Protokolliert eine Warnmeldung auf der Konsole.
* `logger.error(message: string)`: Protokolliert eine Fehlermeldung auf der Konsole.
* `logger.debug(message: string)`: Protokolliert eine Debug-Meldung auf der Konsole. (Nur sichtbar, wenn der Protokollierungsmodus `verbose` in der Browser-Konsole aktiviert ist.)

### [!DNL onDebugChanged]

Durch Übergabe einer Rückruffunktion an `turbine.onDebugChanged` rufen Tags Ihren Rückruf auf, sobald das Debugging umgeschaltet wird. Tags übergeben der Callback-Funktion einen booleschen Wert. Dieser lautet true (wahr), wenn das Debugging aktiviert war, und false (falsch), wenn das Debugging deaktiviert war.

Wenn Sie einfach Meldungen protokollieren möchten, ist es unwahrscheinlich, dass Sie dies verwenden müssen. Stattdessen protokollieren Sie Meldungen immer mit `turbine.logger` und -Tags, um sicherzustellen, dass Ihre Nachrichten nur dann in der Konsole gedruckt werden, wenn das Tag-Debugging aktiviert ist.

### [!DNL propertySettings] {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Ein Objekt, das die folgenden Einstellungen enthält, die vom Benutzer für die Eigenschaft der aktuellen Tag-Laufzeitbibliothek definiert werden:

* `propertySettings.domains: Array<String>`

   Ein Array von Domänen, die von der Eigenschaft abgedeckt werden.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   Entwickler von Erweiterungen sollten sich nicht mit dieser Einstellung befassen.
