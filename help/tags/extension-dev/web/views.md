---
title: Ansichten in Web-Erweiterungen
description: Erfahren Sie, wie Sie Ansichten für Bibliotheksmodule in Ihren Adobe Experience Platform Web-Erweiterungen definieren.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 76%

---

# Ansichten in Web-Erweiterungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Jedes Ereignis, jede Bedingung, jede Aktion und jeder Datenelementtyp kann eine Ansicht bieten, die es dem Benutzer ermöglicht, Einstellungen bereitzustellen. Die Erweiterung kann auch über eine übergeordnete [Erweiterungskonfigurationsansicht](../configuration.md) verfügen, in der Benutzer globale Einstellungen für die gesamte Erweiterung angeben können. Der Vorgang zum Erstellen einer Ansicht ist bei allen Arten von Ansichten identisch.

## Einbinden eines Dokumenttyps

Stellen Sie sicher, dass Sie ein `doctype`-Tag in Ihre HTML-Datei aufnehmen. Normalerweise bedeutet dies, dass Sie die HTML-Datei mit der folgenden Zeile beginnen:

```xml
<!DOCTYPE html>
```

## Einfügen des iFrame-Skripts für Tags

Fügen Sie das iframe-Skript der Tags in den HTML-Code Ihrer Ansicht ein:

```html
<script src="https://assets.adobedtm.com/activation/reactor/extensionbridge/extensionbridge.min.js"></script>
```

Dieses Skript stellt eine Kommunikations-API bereit, mit der Ihre Ansicht mit der Tags-Anwendung kommunizieren kann.

## Registrieren bei der Kommunikations-API extensionBridge

Nachdem das iframe-Skript geladen wurde, müssen Sie einige Methoden für Tags bereitstellen, die für die Kommunikation verwendet werden. Rufen Sie `window.extensionBridge.register` auf und übergeben Sie in diesem Aufruf wie folgt ein Objekt:

```js
window.extensionBridge.register({
  init: function(info) {
    // Populate view with info.settings which will exist if the user is editing something
    // that was previously saved.
    if (info.settings) {
      document.getElementById('name').value = info.settings.name;
    }
  },
  validate: function() {
    // Return whether the view is valid.
    return document.getElementById('name').value.length > 0;
  },
  getSettings: function() {
    // Return user-provided settings.
    return {
      name: document.getElementById('name').value
    };
  }
});
```

Der Inhalt der einzelnen Methoden muss an Ihre jeweiligen Ansichtsanforderungen angepasst werden.

### [!DNL init]

Die `init`-Methode wird durch -Tags aufgerufen, sobald die Ansicht in den iframe geladen wurde. Es wird ein einzelnes Argument (`info`) übergeben, bei dem es sich um ein Objekt mit den folgenden Eigenschaften handeln muss:

| Eigenschaft | Beschreibung |
| --- | --- |
| `settings` | Ein Objekt mit Einstellungen, die zuvor in dieser Ansicht gespeichert wurden. Wenn `settings` den Wert `null` hat, zeigt dies an, dass der Benutzer die anfänglichen Einstellungen erstellt, anstatt eine gespeicherte Version zu laden. Wenn `settings` ein Objekt ist, sollten Sie es in Ihre Ansicht laden, da der Benutzer die zuvor gespeicherten Einstellungen bearbeiten möchte. |
| `extensionSettings` | In der Erweiterungskonfigurationsansicht gespeicherte Einstellungen. Dies kann nützlich sein, um in Ansichten, bei denen es sich nicht um die Erweiterungskonfigurationsansicht handelt, auf Erweiterungseinstellungen zuzugreifen. Wenn es sich bei der aktuellen Ansicht um die Erweiterungskonfigurationsansicht handelt, verwenden Sie `settings` |
| `propertySettings` | Ein Objekt, das Einstellungen für die Eigenschaft enthält. Weitere Informationen zu den in diesem Objekt enthaltenen Elementen finden Sie in der [Anleitung zum turbine-Objekt](../turbine.md#property-settings). |
| `tokens` | Ein Objekt, das API-Token enthält. Für den Zugriff auf Adobe-APIs aus der Ansicht heraus müssen Sie normalerweise ein IMS-Token unter `tokens.imsAccess` verwenden. Dieses Token wird nur für von Adobe entwickelte Erweiterungen verfügbar gemacht. Wenn Sie ein Mitarbeiter der Adobe sind, der eine von Adobe verfasste Erweiterung darstellt, senden Sie bitte eine E-Mail an das Datenerfassungs-Engineering-Team](mailto:reactor@adobe.com) und geben Sie den Namen der Erweiterung ein, damit wir sie zur Zulassungsliste hinzufügen können.[ |
| `company` | Ein Objekt, das als einzige Eigenschaft `orgId` enthält, die Ihre Adobe Experience Cloud ID darstellt (eine 24-stellige alphanumerische Zeichenfolge). |
| `schema` | Ein Objekt im [JSON-Schema](http://json-schema.org/)-Format. Dieses Objekt stammt aus dem [Erweiterungsmanifest](../manifest.md) und kann bei der Validierung Ihres Formulars hilfreich sein. |

Ihre Ansicht sollte diese Informationen zum Rendern und Verwalten des Formulars verwenden. Wahrscheinlich müssen Sie sich nur mit `info.settings` befassen, die anderen Informationen werden jedoch für den Fall bereitgestellt, dass sie erforderlich sind.

### [!DNL validate]

Die `validate`-Methode wird aufgerufen, nachdem der Benutzer auf die Schaltfläche &quot;Speichern&quot;geklickt hat. Sie sollte eines der folgenden Elemente zurückgeben:

* Ein boolescher Wert, der angibt, ob die Eingabe des Benutzers gültig ist.
* Ein promise-Objekt, das später mit einem booleschen Wert aufgelöst wird, der angibt, ob die Eingabe des Benutzers gültig ist.

Sie als Entwickler der Erweiterung können bestimmen, was eine gültige Eingabe darstellt, da Ihr Bibliotheksmodul auf diese Eingabe reagiert.

Wenn die Benutzereingabe ungültig ist, zeigen Sie dies bitte in Ihrer Ansicht an, damit die Benutzer wissen, was korrigiert werden muss.

### [!DNL getSettings]

Die Methode `getSettings` wird aufgerufen, nachdem der Benutzer auf den Button „Speichern“ geklickt hat und die Ansicht validiert worden ist. Die Funktion sollte eines der folgenden Elemente zurückgeben:

* Ein Objekt mit Einstellungen, die auf der Benutzereingabe basieren.
* Ein promise-Objekt, das später mit einem Objekt, das auf der Benutzereingabe basierende Einstellungen enthält, aufgelöst werden soll.

Dieses settings-Objekt wird später in die Tag-Laufzeitbibliothek ausgegeben. Der Inhalt dieses Objekts liegt in Ihrem Ermessen. Das Objekt muss in JSON serialisierbar und aus JSON deserialisierbar sein. Werte wie Funktionen oder [RegExp](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/RegExp)-Instanzen erfüllen diese Kriterien nicht und sind daher nicht zulässig.

## Nutzung freigegebener Ansichten

Das `window.extensionBridge` -Objekt verfügt über mehrere Methoden, mit denen Sie vorhandene Ansichten, die über -Tags verfügbar sind, nutzen können, sodass Sie sie nicht in Ihrer Ansicht reproduzieren müssen. Folgende Methoden sind verfügbar:

### [!DNL openCodeEditor]

```js
window.extensionBridge.openCodeEditor().then(function(code) { 
  console.log(code);
});
```

Der Aufruf dieser Methode zeigt ein modales Element an, das es dem Benutzer ermöglicht, einen Code-Ausschnitt zu bearbeiten. Wenn der Benutzer die Bearbeitung des Codes abgeschlossen hat, wird das promise-Objekt mit dem aktualisierten Code aufgelöst. Schließt der Benutzer den Code-Editor, ohne die Änderungen zu speichern, wird das promise-Objekt nie aufgelöst. Das `options`-Objekt sollte wie folgt strukturiert sein:

| Eigenschaft | Beschreibung |
| --- | --- |
| `code` | Code, der im Editor angezeigt werden sollte. Diese Eigenschaft wird normalerweise bereitgestellt, wenn der Benutzer vorhandenen Code bearbeitet. Wenn sie nicht angegeben wird, ist der Code-Editor beim Öffnen leer. |
| `language` | Die Sprache des zu bearbeitenden Codes. Gültige Optionen sind `javascript`, `html`, `css`, `json` und `plaintext`. Wird dies nicht angegeben, dann wird `javascript` angenommen. |

### [!DNL openRegexTester]

```js
window.extensionBridge.openRegexTester().then(function(pattern) { 
  console.log(pattern);
});
```

Durch den Aufruf dieser Methode wird ein modales Element angezeigt, in dem der Benutzer das Muster eines regulären Ausdrucks testen und ändern kann. Wenn der Benutzer die Bearbeitung des regulären Ausdrucks abgeschlossen hat, wird das promise-Objekt mit dem aktualisierten Muster des regulären Ausdrucks aufgelöst. Wenn der Benutzer den Regex-Tester schließt, ohne die Änderungen zu speichern, wird das promise-Objekt nie aufgelöst. Das `options`-Objekt sollte die folgenden Eigenschaften enthalten:

| Eigenschaft | Beschreibung |
| --- | --- |
| `pattern` | Das Muster des regulären Ausdrucks, das als Ausgangswert des Musterfelds im Tester verwendet werden soll. Diese Eigenschaft wird normalerweise bereitgestellt, wenn der Benutzer einen vorhandenen regulären Ausdruck bearbeitet. Wenn sie nicht angegeben wird, ist das Musterfeld zunächst leer. |
| `flags` | Die Flags des regulären Ausdrucks, die vom Tester verwendet werden sollten. Beispiel: `gi` gibt das Flag für globale Übereinstimmung und das Flag zum Ignorieren der Groß-/Kleinschreibung an. Diese Flags können vom Benutzer im Tester nicht geändert werden, sie veranschaulichen jedoch die spezifischen Flags, die die Erweiterung beim Ausführen des regulären Ausdrucks verwendet. Wenn diese Eigenschaft nicht angegeben wird, werden im Tester keine Flags verwendet. Weitere Informationen zu Flags für reguläre Ausdrücke finden Sie in der [RegExp-Dokumentation von MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp).<br><br>Ein gängiges Szenario ist eine Erweiterung, mit der Benutzer umschalten können, ob bei einem regulären Ausdruck die Groß-/Kleinschreibung ignoriert wird oder nicht. Um dies zu unterstützen, stellt die Erweiterung normalerweise ein Kontrollkästchen in der Ansicht der Erweiterung bereit, das bei Aktivierung die Groß-/Kleinschreibung nicht berücksichtigt (dargestellt durch die Markierung `i` ). Das von der Ansicht gespeicherte settings-Objekt muss darstellen, ob das Kontrollkästchen aktiviert wurde, damit das Bibliotheksmodul, das den regulären Ausdruck ausführt, erfährt, ob das Flag `i` verwendet werden soll. Wenn die Erweiterungsansicht außerdem den Tester für reguläre Ausdrücke öffnen möchte, muss das Flag `i` übergeben werden, wenn das Kontrollkästchen zum Ignorieren der Groß-/Kleinschreibung aktiviert ist. Dadurch kann der Benutzer den regulären Ausdruck ordnungsgemäß testen, wobei die Groß-/Kleinschreibung nicht berücksichtigt wird. |

### [!DNL openDataElementSelector] {#open-data-element}

```js
window.extensionBridge.openDataElementSelector().then(function(dataElement) { 
  console.log(dataElement);
});
```

Der Aufruf dieser Methode zeigt ein modales Element an, mit dem der Benutzer ein Datenelement auswählen kann. Wenn der Benutzer die Auswahl eines Datenelements abgeschlossen hat, wird das promise-Objekt mit dem Namen des ausgewählten Datenelements aufgelöst (der Name wird standardmäßig in Prozentzeichen eingeschlossen). Wenn der Benutzer die Elementauswahl schließt, ohne die Änderungen zu speichern, wird das promise-Objekt nie aufgelöst.

Das `options`-Objekt sollte eine einzelne boolesche Eigenschaft, `tokenize`, enthalten. Diese Eigenschaft gibt an, ob der Name des ausgewählten Datenelements vor dem Auflösen des promise-Objekts in Prozentzeichen eingeschlossen werden soll. Informationen dazu, warum dies sinnvoll ist, finden Sie im Abschnitt zu [unterstützenden Datenelementen](#supporting-data-elements). Diese Option hat den Standardwert `true`.

## Unterstützende Datenelemente {#supporting-data-elements}

Ihre Ansichten verfügen vermutlich über Formularfelder, in denen Benutzer Datenelemente nutzen möchten. Wenn Ihre Ansicht beispielsweise über ein Textfeld verfügt, in das der Benutzer einen Produktnamen eingeben soll, ist es möglicherweise nicht sinnvoll, einen hartcodierten Wert in das Feld einzugeben. Stattdessen sollte der Wert des Felds dynamisch sein (zur Laufzeit bestimmt) und dies lässt sich mithilfe eines Datenelements erreichen.

Beispiel: Angenommen, wir erstellen eine Erweiterung, die einen Beacon sendet, um eine Konversion zu verfolgen. Nehmen wir weiter an, dass eines der Datenelemente, die unser Beacon sendet, ein Produktname ist. Unsere Erweiterungsansicht, die es dem Benutzer ermöglicht, das Beacon zu konfigurieren, würde wahrscheinlich über ein Textfeld für den Produktnamen verfügen. Es wäre normalerweise nicht sehr sinnvoll, wenn der Platform-Benutzer einen statischen Produktnamen wie &quot;Calzone Oven XL&quot;eingeben würde, da der Produktname wahrscheinlich von der Seite abhängt, von der das Beacon gesendet wird. Dies ist ein guter Fall für ein Datenelement.

Wenn ein Benutzer das Datenelement mit dem Namen `productname` für den Produktnamenwert verwenden möchte, kann er den Namen des Datenelements in Prozentzeichen eingeschlossen (`%productname%`) eingeben. Wir bezeichnen den Namen des in Prozentzeichen eingeschlossenen Datenelements als &quot;Datenelement-Token&quot;. Platform-Benutzer sind oft mit diesem Konstrukt vertraut. Ihre Erweiterung speichert dann das Datenelement-Token in dem `settings`-Objekt, das sie exportiert. Ihr settings-Objekt könnte dann wie folgt aussehen:

```js
{
  productName: '%productname%'
}
```

Zur Laufzeit wird vor Übergabe des settings-Objekts an Ihr Bibliotheksmodul das settings-Objekt gescannt und alle Datenelement-Token durch die entsprechenden Werte ersetzt. Wenn zur Laufzeit das `productname`-Datenelement den Wert `Ceiling Medallion Pro 2000` hat, würde das settings-Objekt, das an Ihr Bibliotheksmodul übergeben wird, wie folgt lauten:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Um anzugeben, wo die Verwendung von Datenelementen für die Benutzer hilfreich sein kann, und um den Benutzern die Eingabe von Datenelementen zu erleichtern, empfehlen wir dringend, neben den betreffenden Feldern eine Symbolschaltfläche hinzuzufügen, wie im Folgenden gezeigt:

![Datenelementfeld](../images/data-element-field.png)

Wenn ein Benutzer auf den Button neben dem Textfeld klickt, wird `window.extensionBridge.openDataElementSelector` wie [oben beschrieben](#open-data-element) aufgerufen. Daraufhin wird eine Liste der Datenelemente angezeigt, die dem Benutzer zur Auswahl stehen, sodass er sich weder den Namen merken noch die Prozentzeichen eingeben muss. Nachdem der Benutzer ein Datenelement ausgewählt hat, wird der Name des ausgewählten Datenelements, der in Prozentzeichen eingeschlossen ist (sofern die Option `tokenize` nicht auf `false` festgelegt wurde), übergeben. Wir empfehlen Ihnen, das Textfeld dann mit dem Ergebnis zu füllen.

### Ersetzen von Datenelement-Token

Angenommen, ein persistentes settings-Objekt würde wie oben beschrieben aus Folgendem bestehen:

```js
{
  productName: '%productname%'
}
```

Und zur Laufzeit hätte das `productname`-Datenelement den Wert `Ceiling Medallion Pro 2000`, dann würde das settings-Objekt, das in Ihr Bibliotheksmodul übergeben wird, wie folgt aussehen:

```js
{
  productName: 'Ceiling Medallion Pro 2000'
}
```

Wenn im settings-Objekt ein Wert gefunden wird, der aus einem Prozentzeichen, gefolgt von einer Zeichenfolge und einem weiteren Prozentzeichen _und sonst nichts_ besteht, wird er durch den Datenelementwert _ersetzt, ohne dass der Typ des Datenelementwerts_ geändert wird.

Hätte beispielsweise `productname` zur Laufzeit als Wert die Zahl `538` (statt einer Zeichenfolge), würde das folgende settings-Objekt an Ihr Bibliotheksmodul übergeben:

```js
{
  productName: 538
}
```

Beachten Sie, dass das Ergebnis `538` hier eine Zahl und keine Zeichenfolge ist. Wenn der Datenelementwert zur Laufzeit eine Funktion wäre (ein seltener, aber möglicher Anwendungsfall), würde das resultierende settings-Objekt wie folgt lauten:

```js
{
  productName: function() { … }
}
```

Angenommen, das gespeicherte settings-Objekt lautet dagegen wie folgt:

```js
{
  productName: '%productname% - %modelnumber%'
}
```

In diesem Fall ist das Ergebnis immer eine Zeichenfolge, da der Wert von `productName` mehr als ein einzelnes Datenelement-Token umfasst. Jedes Datenelement-Token wird durch seinen jeweiligen Wert ersetzt, nachdem es in eine Zeichenfolge umgewandelt wurde. Wenn der Wert von `productname` zur Laufzeit `Ceiling Medallion Pro` (eine Zeichenfolge) und `modelnumber` `2000` (eine Zahl) wäre, würde das resultierende settings-Objekt, das an Ihr Bibliotheksmodul übergeben wird, wie folgt lauten:

```js
{
  productName: 'Ceiling Medallion Pro - 2000'
}
```

## Vermeiden von Navigationsvorgängen

Die Kommunikation zwischen der Erweiterungsansicht und der zugehörigen Datenerfassungs-Benutzeroberfläche ist davon abhängig, dass in der Erweiterungsansicht keine Navigation stattfindet. Vermeiden Sie daher, der Erweiterungsansicht irgendetwas hinzuzufügen, das es dem Benutzer ermöglicht, von der HTML-Ansicht der Erweiterung weg zu navigieren. Wenn Sie beispielsweise in der Erweiterungsansicht einen Link angeben, stellen Sie sicher, dass ein neues Browser-Fenster geöffnet wird (in der Regel durch Hinzufügen von `target="_blank"` zum Anker-Tag). Wenn Sie ein `form`-Element in Ihrer Erweiterungsansicht verwenden, stellen Sie sicher, dass dieses Formular nie gesendet wird. Das Formular kann versehentlich übermittelt werden, wenn das Formular ein `button`-Element ohne die Angabe `type="button"` enthält. Das Absenden eines Formulars in der Erweiterungsansicht würde bewirken, dass das HTML-Dokument aktualisiert wird, was zu einem fehlerhaften Kundenerlebnis führen würde.
