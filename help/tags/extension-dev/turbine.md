---
title: Freie turbine-Variable
description: Machen Sie sich mit dem turbine-Objekt vertraut, einer freien Variablen, die Informationen und Dienstprogramme speziell für die Tag-Laufzeit in Adobe Experience Platform bereitstellt.
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 27dd38cc509040ea9dc40fc7030dcdec9a182d55
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 100%

---

# Freie turbine-Variable

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

Das `turbine`-Objekt ist eine „freie Variable“ im Gültigkeitsbereich der Bibliotheksmodule Ihrer Erweiterung. Es stellt Informationen und Dienstprogramme bereit, die für die Tag-Laufzeit von Adobe Experience Platform spezifisch sind, und ist ohne Verwendung von `require()` für Bibliotheksmodule immer verfügbar.

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` ist ein Objekt, das Build-Informationen zur aktuellen Tag-Laufzeitbibliothek enthält.

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `turbineVersion` | Die in der aktuellen Bibliothek verwendete [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine)-Version. |
| `turbineBuildDate` | Das ISO-8601-Datum, an dem die im aktuellen Container verwendete [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine)-Version erstellt wurde. |
| `buildDate` | Das ISO-8601-Datum, an dem die aktuelle Bibliothek erstellt wurde. |

{style="table-layout:auto"}

## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` ist ein Objekt, das Informationen über die Umgebung enthält, in der die Bibliothek bereitgestellt wird.

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die ID der Umgebung. |
| `stage` | Die Umgebung, für die diese Bibliothek erstellt wurde. Zu den möglichen Werten gehören `development`, `staging` und `production`. |

{style="table-layout:auto"}

## `debugEnabled`

Ein boolescher Wert, der angibt, ob das Tag-Debugging derzeit aktiviert ist.

Wenn Sie einfach Meldungen protokollieren möchten, ist es unwahrscheinlich, dass Sie dies verwenden müssen. Stattdessen sollten Sie Meldungen immer mit `turbine.logger` protokollieren, um sicherzustellen, dass Ihre Meldungen nur auf der Konsole ausgegeben werden, wenn Tag-Debugging aktiviert ist.

## `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

Gibt den Wert eines Datenelements zurück.

## `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

Gibt das Einstellungsobjekt zurück, das zuletzt in der Ansicht für die [Erweiterungskonfiguration](./configuration.md) gespeichert wurde.

Beachten Sie, dass die Werte in den zurückgegebenen Einstellungsobjekten möglicherweise von Datenelementen stammen. Deshalb kann der Aufruf von `getExtensionSettings()` zu unterschiedlichen Zeitpunkten zu unterschiedlichen Ergebnissen führen, wenn sich die Werte der Datenelemente geändert haben. Um die aktuellsten Werte zu erhalten, warten Sie mit dem Aufruf von `getExtensionSettings()` so lange wie möglich.

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

Die Eigenschaft [hostedLibFiles](./manifest.md) kann im Erweiterungsmanifest definiert werden, um verschiedene Dateien zusammen mit der Tag-Laufzeitbibliothek zu hosten. Dieses Modul gibt die URL zurück, unter der die angegebene Bibliotheksdatei gehostet wird.

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

Ruft ein Modul ab, das von einer anderen Erweiterung freigegeben wurde. Wenn kein passendes Modul gefunden wird, wird `undefined` zurückgegeben. Weitere Informationen zu freigegebenen Modulen finden Sie unter [Implementieren freigegebener Module](./web/shared.md).

## `logger`

```js
turbine.logger.error('Error!');
```

Das Protokollierungsdienstprogramm wird verwendet, um Meldungen auf der Konsole zu protokollieren. Meldungen werden nur dann auf der Konsole angezeigt, wenn der Benutzer den Debugging-Modus aktiviert hat. Die empfohlene Methode zum Aktivieren des Debuggens besteht in der Verwendung des [Adobe Experience Cloud-Debuggers](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda). Alternativ kann der Benutzer den Befehl `_satellite.setDebug(true)` in der Browser-Entwicklungskonsole ausführen. Die logger-Funktion verfügt über die folgenden Methoden:

* `logger.log(message: string)`: Protokolliert eine Meldung auf der Browser-Konsole.
* `logger.info(message: string)`: Protokolliert eine Informationsmeldung auf der Konsole.
* `logger.warn(message: string)`: Protokolliert eine Warnmeldung auf der Konsole.
* `logger.error(message: string)`: Protokolliert eine Fehlermeldung auf der Konsole.
* `logger.debug(message: string)`: Protokolliert eine Debug-Meldung auf der Konsole. (Nur sichtbar, wenn der Protokollierungsmodus `verbose` in der Browser-Konsole aktiviert ist.)
* `logger.deprecation(message: string)`: Protokolliert eine Warnmeldung auf der Konsole, unabhängig davon, ob der Benutzer Tag-Debugging aktiviert hat.

## `onDebugChanged`

Wenn eine Callback-Funktion an `turbine.onDebugChanged` übergeben wird, ruft Tags diesen Rückruf auf, sobald der Debugging-Modus aktiviert bzw. deaktiviert wird. Tags übergibt der Callback-Funktion einen booleschen Wert. Bei aktiviertem Debugging lautet dieser Wert „true“ und bei deaktiviertem Debugging „false“.

Wenn Sie einfach Meldungen protokollieren möchten, ist es unwahrscheinlich, dass Sie dies verwenden müssen. Stattdessen sollten Sie Meldungen immer mit `turbine.logger` protokollieren. Tags stellt dann sicher, dass die Meldungen nur dann auf der Konsole ausgegeben werden, wenn der Tag-Debugging-Modus aktiviert ist.

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

Ein Objekt, das die folgenden Einstellungen enthält, die vom Benutzer für die Eigenschaft der aktuellen Tag-Laufzeitbibliothek definiert werden:

* `propertySettings.domains: Array<String>`

   Ein Array von Domains, die von der Eigenschaft abgedeckt werden.

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   Entwickler von Erweiterungen sollten sich nicht mit dieser Einstellung befassen.
