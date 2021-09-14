---
title: Kontext in Edge-Erweiterungsmodulen
description: Erfahren Sie mehr über das Kontextobjekt und die Rolle, die es bei der Interaktion mit Bibliotheksmodulen in Tag-Erweiterungen von Edge-Eigenschaften spielt.
exl-id: 04e4e369-687e-4b46-9d24-18a97a218555
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 100%

---

# Kontext in Edge-Erweiterungsmodulen

>[!NOTE]
>
> Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Für alle Bibliotheksmodule in Edge-Erweiterungen wird beim Ausführen ein `context`-Objekt bereitgestellt. Dieses Dokument behandelt die Eigenschaften des `context`-Objekts und die Rolle, die sie in Bibliotheksmodulen spielen.

## Adobe-Anfragekontext (arc)

Die Eigenschaft `arc` ist ein Objekt, das Informationen über das Ereignis bereitstellt, das die Regel auslöst. Die folgenden Abschnitte behandeln die verschiedenen Untereigenschaften, die in diesem Objekt enthalten sind.

### [!DNL event]

Das `event`-Objekt repräsentiert das Ereignis, das die Regel ausgelöst hat und die folgenden Werte enthält:

```js
logger.log(context.arc.event);
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdm` | Das XDM-Objekt des Ereignisses. |
| `data` | Die benutzerdefinierte Datenschicht. |

### [!DNL request]

`request` sollte nicht mit einer Anfrage vom Client-Gerät verwechselt werden. Es ist ein geringfügig modifiziertes Objekt, das vom Adobe Experience Platform Edge Network stammt.

```js
logger.log(context.arc.request)
```

Das `request`-Objekt besitzt zwei Eigenschaften auf der obersten Ebene: `body` und `head`. Die `body`-Eigenschaft enthält Informationen zum Experience-Datenmodell (XDM) und kann im Adobe Experience Platform Debugger eingesehen werden, indem Sie zu **[!UICONTROL Launch]** navigieren und die Registerkarte **[!UICONTROL Edge Trace]** auswählen.

### [!DNL ruleStash] {#rulestash}

`ruleStash` ist ein Objekt, das jedes Ergebnis aus Aktionsmodulen erfasst.

```js
logger.log(context.arc.ruleStash);
```

Jede Erweiterung hat ihren eigenen Namensraum. Wenn Ihre Erweiterung beispielsweise den Namen `send-beacon` hat, werden alle Ergebnisse von `send-beacon`-Aktionen im `ruleStash['send-beacon']`-Namespace gespeichert.

Der Namespace ist für jede Erweiterung eindeutig und beginnt mit dem Wert `undefined`.

Der Namespace wird mit dem von jeder Aktion zurückgegebenen Ergebnis überschrieben. Eine Erweiterung `transform` enthält beispielsweise zwei Aktionen: `generate-fullname` und `generate-fulladdress`. Diese beiden Aktionen werden dann einer Regel hinzugefügt.

Wenn das Ergebnis der Aktion `generate-fullname` `Firstname Lastname` lautet, wird der Regel-Stash nach dem Abschluss der Aktion wie folgt angezeigt:

```js
{
  transform: 'Firstname Lastname'
}
```

Wenn das Ergebnis der Aktion `generate-address` `3900 Adobe Way` lautet, wird der Regel-Stash nach dem Abschluss der Aktion wie folgt angezeigt:

```js
{
  transform: '3900 Adobe Way'
}
```

Beachten Sie, dass „Vorname Nachname“ nicht mehr im Regel-Stash vorhanden ist, da die `generate-address`-Aktion ihn mit einem neuen Wert überschrieben hat.

Wenn `ruleStash` die Ergebnisse beider Aktionen im `transform`-Namespace speichern soll, kann Ihr Aktionsmodul dem folgenden Beispiel folgen:

```js
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;

  if (!transformRuleStash) {
    transformRuleStash = {};
  }

  transformRuleStash.fullName = 'Firstname Lastname';

  return transformRuleStash;
}
```

Bei der ersten Ausführung dieser Aktion ist `ruleStash` im Zustand `undefined` und wird daher als leeres Objekt initialisiert. Bei der nächsten Ausführung der Aktion erhält sie `ruleStash`, das beim vorherigen Aufruf der Aktion zurückgegeben wurde. Bei der Verwendung eines Objekts als `ruleStash` können Sie neue Daten hinzufügen, ohne zuvor durch andere Aktionen unserer Erweiterung festgelegte Daten zu verlieren.

>[!NOTE]
>
>Achten Sie darauf, bei dieser Methode immer den vollständigen Erweiterungsregel-Stash zurückzugeben. Wenn Sie stattdessen nur einen Wert zurückgeben, werden alle anderen zuvor festgelegten Eigenschaften überschrieben.

## Hilfsprogramme

Die `utils`-Eigenschaft stellt ein Objekt zur Bereitstellung von Dienstprogrammen dar, die spezifisch für die Tag-Laufzeit sind.

### [!DNL logger]

Mit dem Dienstprogramm `logger` können Sie Meldungen protokollieren, die während Debugging-Sitzungen angezeigt werden, wenn Sie den [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) verwenden.

```js
context.utils.logger.error('Error!');
```

Die Protokollfunktion verfügt über die folgenden Methoden, wobei `message` die zu protokollierende Meldung ist:

| Methode | Beschreibung |
| --- | --- |
| `log(message)` | Protokolliert eine Meldung auf der Browser-Konsole. |
| `info(message)` | Protokolliert eine Informationsmeldung auf der Konsole. |
| `warn(message)` | Protokolliert eine Warnmeldung auf der Konsole. |
| `error(message)` | Protokolliert eine Fehlermeldung auf der Konsole. |
| `debug(message)` | Protokolliert eine Debugging-Meldung auf der Konsole. Nur sichtbar, wenn die `verbose`-Protokollierung in der Browser-Konsole aktiviert ist. |

### [!DNL fetch]

Dieses Dienstprogramm implementiert die [Fetch-API](https://developer.mozilla.org/de-DE/docs/Web/API/Fetch_API). Mit dieser Funktion können Sie Anforderungen an Endpunkte von Drittanbietern senden.

```js
context.utils.fetch('http://example.com/movies.json')
  .then(response => response.json())
```

### [!DNL getBuildInfo]

Dieses Dienstprogramm gibt ein Objekt zurück, das Informationen zum Build der aktuellen Tag-Laufzeitbibliothek enthält.

```js
logger.log(context.utils.getBuildInfo().turbineBuildDate);
```

Das Objekt enthält die folgenden Werte:

| Eigenschaft | Beschreibung |
| --- | --- |
| `turbineVersion` | Die in der aktuellen Bibliothek verwendete [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge)-Version. |
| `turbineBuildDate` | Das ISO-8601-Datum, an dem die im aktuellen Container verwendete [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine-edge)-Version erstellt wurde. |
| `buildDate` | Das ISO-8601-Datum, an dem die aktuelle Bibliothek erstellt wurde. |
| `environment` | Die Umgebung, für die diese Bibliothek erstellt wurde. Zu den möglichen Werten gehören `development`, `staging` und `production.` |

Im Folgenden finden Sie ein Beispiel für ein `getBuildInfo`-Objekt, das die zurückgegebenen Werte veranschaulicht:

```js
{
  turbineVersion: "1.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

### [!DNL getExtensionSettings]

Dieses Dienstprogramm gibt das `settings`-Objekt zurück, das zuletzt von der Ansicht der [Erweiterungskonfiguration](../configuration.md) gespeichert wurde.

```js
logger.log(context.utils.getExtensionSettings());
```

### [!DNL getSettings]

Dieses Dienstprogramm gibt das `settings`-Objekt zurück, das zuletzt von der entsprechenden Ansicht des Bibliothekmoduls gespeichert wurde.

```js
logger.log(context.utils.getSettings());
```

### [!DNL getRule]

Dieses Dienstprogramm gibt ein Objekt zurück, das Informationen zur Regel enthält, die das Modul auslöst.

```js
logger.log(context.utils.getRule());
```

Das Objekt enthält die folgenden Werte:

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Die Regel-ID. |
| `name` | Den Regelnamen. |
