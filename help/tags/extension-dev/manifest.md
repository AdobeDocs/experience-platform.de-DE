---
title: Erweiterungsmanifest
description: Erfahren Sie, wie Sie eine JSON-Manifestdatei konfigurieren, die Adobe Experience Platform Informationen zur korrekten Verwendung Ihrer Erweiterung bereitstellt.
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '2607'
ht-degree: 85%

---

# Erweiterungsmanifest

Im Basisverzeichnis der Erweiterung müssen Sie eine Datei mit dem Namen `extension.json` erstellen. Sie enthält wichtige Details zu Ihrer Erweiterung, die es Adobe Experience Platform ermöglichen, diese ordnungsgemäß zu nutzen. Einige Inhalte sind nach dem Vorbild von [npm `package.json`](https://docs.npmjs.com/files/package.json) gestaltet.

Ein Beispiel für `extension.json` finden Sie im GitHub-Repository [Hello World Extension](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json).

Ein Erweiterungsmanifest muss Folgendes enthalten:

| Eigenschaft | Beschreibung |
|--------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | Name der Erweiterung. Dies muss sich von allen anderen Erweiterungen unterscheiden und den [Benennungsregeln](#naming-rules) entsprechen. **Er wird von Tags als Kennung verwendet und sollte nach der Veröffentlichung der Erweiterung nicht geändert werden.** |
| `platform` | Die Plattform für die Erweiterung. Der einzige Wert, der im Moment akzeptiert wird, lautet `web`. |
| `version` | Die Version der Erweiterung. Sie muss dem Versionierungsformat [semver](https://semver.org/lang/de/) entsprechen. Dies entspricht dem [npm-Feld version](https://docs.npmjs.com/files/package.json#version). |
| `displayName` | Der für Menschen lesbare Name der Erweiterung. Dies wird Experience Platform-Benutzern angezeigt. Es ist nicht erforderlich, „Tags“ oder „Erweiterung“ zu erwähnen, da die Benutzer bereits wissen, dass sie eine Tag-Erweiterung vor sich haben. |
| `description` | Die Beschreibung der Erweiterung. Dies wird Experience Platform-Benutzern angezeigt. Wenn Benutzer mit Ihrer Erweiterung Ihr Produkt auf ihrer Website implementieren können, beschreiben Sie die Funktionen Ihres Produkts. Es ist nicht erforderlich, „Tags“ oder „Erweiterung“ zu erwähnen, da die Benutzer bereits wissen, dass sie eine Tag-Erweiterung vor sich haben. |
| `iconPath` *(Optional)* | Der relative Pfad zu dem Symbol, das für die Erweiterung angezeigt wird. Er sollte nicht mit einem Schrägstrich beginnen. Er muss auf eine SVG-Datei mit der Erweiterung `.svg` verweisen. Der SVG sollte quadratisch sein und kann von Experience Platform skaliert werden. |
| `author` | „author“ ist ein Objekt, das wie folgt strukturiert sein sollte: <ul><li>`name`: Der Name des Autors der Erweiterung. Alternativ kann hier der Name der Firma angegeben werden.</li><li>`url` *(Optional)*: Eine URL, die weitere Informationen zum Autor der Erweiterung bietet.</li><li>`email` *(Optional)*: Die E-Mail-Adresse des Autors der Erweiterung.</li></ul>Dies entspricht den Regeln des [npm-Felds author](https://docs.npmjs.com/files/package.json#people-fields-author-contributors). |
| `releaseNotesUrl` *(Optional)* | Die URL zu den Versionshinweisen Ihrer Erweiterung, wenn Sie über einen Speicherort für die Veröffentlichung dieser Informationen verfügen. Diese URL wird in der Adobe Tags-Benutzeroberfläche verwendet, um diesen Link während der Installation und Aktualisierung der Erweiterung anzuzeigen. Diese Eigenschaft wird nur für Web- und Edge-Erweiterungen unterstützt. |
| `exchangeUrl` *(Erforderlich für öffentliche Erweiterungen)* | Die URL zum Listeneintrag Ihrer Erweiterung auf Adobe Exchange. Sie muss dem Muster `https://www.adobeexchange.com/experiencecloud.details.######.html` entsprechen. |
| `viewBasePath` | Der relative Pfad zu dem Unterverzeichnis, das alle Ihre Ansichten und ansichtsbezogenen Ressourcen (HTML, JavaScript, CSS, Bilder) enthält. Experience Platform hostet dieses Verzeichnis auf einem Webserver und lädt iframe-Inhalte daraus. Dies ist ein erforderliches Feld und darf nicht mit einem Schrägstrich beginnen. Wenn sich beispielsweise alle Ihre Ansichten im Verzeichnis `src/view/` befinden, hat `viewBasePath` den Wert `src/view/`. |
| `hostedLibFiles` *(Optional)* | Viele Benutzer bevorzugen es, alle Tag-bezogenenen Dateien auf ihrem eigenen Server zu hosten. Dies bietet den Benutzern höhere Sicherheit in Bezug auf die Dateiverfügbarkeit zur Laufzeit und sie können den Code einfach auf Sicherheitslücken überprüfen. Wenn die Bibliothekskomponente der Erweiterung zur Laufzeit JavaScript-Dateien laden muss, sollten Sie diese Eigenschaft verwenden, um die betreffenden Dateien aufzulisten. Die aufgelisteten Dateien werden zusammen mit der Tag-Laufzeitbibliothek gehostet. Ihre Erweiterung kann die Dateien dann über eine URL laden, die mit der [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file)-Methode abgerufen wird.<br><br>Diese Option enthält ein Array mit relativen Pfaden zu Bibliotheksdateien von Drittanbietern, die gehostet werden müssen. |
| `main` *(Optional)* | Der relative Pfad eines Bibliotheksmoduls, das zur Laufzeit ausgeführt werden soll.<br><br>Dieses Modul wird immer in die Laufzeitbibliothek eingebunden und ausgeführt. Weil das Modul immer in die Laufzeitbibliothek eingebunden wird, empfehlen wir, nur dann ein „main“-Modul zu verwenden, wenn es unbedingt erforderlich ist, und seine Code-Größe minimal zu halten.<br><br>Es ist nicht garantiert, dass dieses Modul zuerst ausgeführt wird. Andere Module können davor ausgeführt werden. |
| `configuration` *(Optional)* | Dies beschreibt den Abschnitt mit der [Erweiterungskonfiguration](./configuration.md) der Erweiterung. Dies ist erforderlich, wenn Benutzer globale Einstellungen für die Erweiterung angeben müssen. Weitere Informationen dazu, wie dieses Feld aufgebaut sein soll, finden Sie im [Anhang](#config-object). |
| `events` *(Optional)* | Ein Array von Typdefinitionen für [Ereignisse](./web/event-types.md). Die Struktur der einzelnen Objekte im Array finden Sie im Anhang unter [Typdefinitionen](#type-definitions). |
| `conditions` *(Optional)* | Ein Array von Typdefinitionen für [Bedingungen](./web/condition-types.md). Die Struktur der einzelnen Objekte im Array finden Sie im Anhang unter [Typdefinitionen](#type-definitions). |
| `actions` *(Optional)* | Ein Array von Typdefinitionen für [Aktionen](./web/action-types.md). Die Struktur der einzelnen Objekte im Array finden Sie im Anhang unter [Typdefinitionen](#type-definitions). |
| `dataElements` *(Optional)* | Ein Array von Typdefinitionen für [Datenelemente](./web/data-element-types.md). Die Struktur der einzelnen Objekte im Array finden Sie im Anhang unter [Typdefinitionen](#type-definitions). |
| `sharedModules` *(Optional)* | Ein Array von gemeinsamen Moduldefinitionsobjekten. Jedes gemeinsame Modulobjekt im Array sollte wie folgt aufgebaut sein: <ul><li>`name`: Der Name des gemeinsamen Moduls. Beachten Sie, dass dieser Name verwendet wird, wenn von anderen Erweiterungen auf gemeinsame Module verwiesen wird, wie unter [Gemeinsame Module](./web/shared.md) beschrieben. Dieser Name wird in keiner Benutzeroberfläche angezeigt. Er sollte sich von den Namen anderer gemeinsamer Module in Ihrer Erweiterung unterscheiden und muss den [Benennungsregeln](#naming-rules) entsprechen. **Er wird von Tags als Kennung verwendet und sollte nach der Veröffentlichung der Erweiterung nicht geändert werden.**</li><li>`libPath`: Der relative Pfad zum gemeinsamen Modul. Er sollte nicht mit einem Schrägstrich beginnen. Er muss auf eine JavaScript-Datei mit der Erweiterung `.js` verweisen.</li></ul> |

## Anhang

### Benennungsregeln {#naming-rules}

Der Wert eines jeden Felds `name` in `extension.json` muss den folgenden Regeln entsprechen:

* Darf höchstens 214 Zeichen lang sein
* Darf nicht mit einem Punkt oder Unterstrich beginnen
* Darf keine Großbuchstaben enthalten
* Darf nur Zeichen enthalten, die in einer URL zulässig sind

Diese Regeln entsprechen den Regeln für [npm-Paketnamen](https://docs.npmjs.com/files/package.json#name).

### Eigenschaften von Konfigurationsobjekten {#config-object}

Das Konfigurationsobjekt sollte wie folgt strukturiert sein:

<table>
  <thead>
    <tr>
      <th>Eigenschaft</th>
      <th>Beschreibung</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>viewPath</code></td>
      <td>Die relative URL zur Erweiterungskonfigurationsansicht. Sie sollte relativ zu <code>viewBasePath</code> sein und nicht mit einem Schrägstrich beginnen. Sie muss auf eine HTML-Datei mit der Erweiterung <code>.html</code> verweisen. Abfragezeichenfolgen- und Fragmentbezeichner-Suffixe (Hashes) sind zulässig.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Ein Objekt vom Typ <a href="https://json-schema.org/">JSON-Schema</a>, das das Format eines gültigen Objekts beschreibt, das in der Erweiterungskonfigurationsansicht gespeichert wird. Da Sie der Entwickler der Konfigurationsansicht sind, müssen Sie sicherstellen, dass alle gespeicherten Einstellungsobjekte diesem Schema entsprechen. Dieses Schema wird auch für die Validierung verwendet, wenn Benutzende versuchen, Daten mithilfe von Experience Platform-Services zu speichern.<br><br>Beispiel für ein schema-Objekt:
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Es wird empfohlen, zum manuellen Testen Ihres Schemas ein Tool wie <a href="https://www.jsonschemavalidator.net/">JSON Schema Validator</a> zu verwenden.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Optional)</em></td>
      <td>Ein Array von Objekten, wobei jedes Objekt eine Transformation darstellt, die bei der Ausgabe in die Laufzeitbibliothek an jedem entsprechenden Einstellungsobjekt durchgeführt werden soll. Weitere Informationen dazu, warum dies erforderlich ist und wie es verwendet wird, finden Sie im Abschnitt <a href="#transforms">Transformationen</a>.</td>
    </tr>
  </tbody>
</table>

### Typdefinitionen {#type-definitions}

Eine Typdefinition ist ein Objekt, mit dem ein Ereignis-, Bedingungs-, Aktions- oder Datenelementtyp beschrieben wird. Das Objekt besteht aus folgenden Elementen:

<table>
  <thead>
    <tr>
      <th>Eigenschaft</th>
      <th>Beschreibung</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>Name des Typs. Dies muss ein eindeutiger Name innerhalb der Erweiterung sein. Der Name muss den <a href="#naming-rules">Benennungsregeln</a> entsprechen. <strong>Er wird von Tags als Kennung verwendet und sollte nach der Veröffentlichung Ihrer Erweiterung nicht geändert werden.</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>Der Text, der zur Darstellung des Typs in der Datenerfassungs-Benutzeroberfläche verwendet wird. Er sollte für Menschen lesbar sein.</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(Optional)</em></td>
      <td>Wenn angegeben, wird die <code>displayName</code> in der Benutzeroberfläche unter der <code>categoryName</code> aufgeführt. Alle Typen mit dem gleichen <code>categoryName</code>-Wert werden unter der gleichen Kategorie aufgeführt. Wenn Ihre Erweiterung beispielsweise den Ereignistyp <code>keyUp</code> und den Ereignistyp <code>keyDown</code> bereitstellt und beide Ereignistypen einen <code>categoryName</code>-Wert von <code>Keyboard</code> aufweisen, werden beide Ereignistypen unter der Kategorie „Keyboard“ aufgelistet, während der Benutzer beim Erstellen einer Regel einen Eintrag aus der Liste der verfügbaren Ereignistypen auswählt. Der Wert von <code>categoryName</code> sollte für Menschen lesbar sein.</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>Der relative Pfad zum Bibliotheksmodul des Typs. Er sollte nicht mit einem Schrägstrich beginnen. Er muss auf eine JavaScript-Datei mit der Erweiterung <code>.js</code> verweisen.</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(Optional)</em></td>
      <td>Die relative URL zur Ansicht des Typs. Sie sollte relativ zu <code>viewBasePath</code> sein und nicht mit einem Schrägstrich beginnen. Sie muss auf eine HTML-Datei mit der Erweiterung <code>.html</code> verweisen. Abfragezeichenfolgen und Fragmentbezeichner (Hashes) sind zulässig. Wenn das Bibliotheksmodul Ihres Typs keine Einstellungen von Benutzern verwendet, können Sie diese Eigenschaft ausschließen. Stattdessen zeigt Experience Platform einen Platzhalter an, der angibt, dass keine Konfiguration erforderlich ist.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Ein Objekt vom Typ <a href="https://json-schema.org/">JSON-Schema</a>, das das Format eines gültigen Einstellungsobjekts beschreibt, das vom Benutzer gespeichert werden kann. Die Einstellungen werden normalerweise von einem Benutzer über die Datenerfassungs-Benutzeroberfläche konfiguriert und gespeichert. In diesen Fällen kann die Ansicht der Erweiterung die erforderlichen Schritte zur Überprüfung der vom Benutzer bereitgestellten Einstellungen durchführen. Auf der anderen Seite entscheiden sich einige Benutzer dafür, Tag-APIs direkt ohne die Hilfe einer Benutzeroberfläche zu verwenden. Mit diesem Schema wird Experience Platform in die Lage versetzt, genau zu überprüfen, ob die von den Benutzenden gespeicherten Einstellungsobjekte unabhängig davon, ob eine Benutzeroberfläche verwendet wird, in einem Format vorliegen, das mit dem Bibliotheksmodul kompatibel ist, das zur Laufzeit das Einstellungsobjekt verarbeitet.<br><br>Ein Beispiel für ein schema-Objekt:<br>
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Es wird empfohlen, zum manuellen Testen Ihres Schemas ein Tool wie <a href="https://www.jsonschemavalidator.net/">JSON Schema Validator</a> zu verwenden.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Optional)</em></td>
      <td>Ein Array von Objekten, wobei jedes Objekt eine Transformation darstellt, die bei der Ausgabe in die Laufzeitbibliothek an jedem entsprechenden Einstellungsobjekt durchgeführt werden soll. Weitere Informationen dazu, warum dies erforderlich ist und wie es verwendet wird, finden Sie im Abschnitt zu <a href="#transforms">Transformationen</a>.</td>
    </tr>
  </tbody>
</table>

### Transformationen {#transforms}

Für bestimmte spezifische Anwendungsfälle müssen für Erweiterungen die in einer Ansicht gespeicherten Einstellungsobjekte von Experience Platform transformiert werden, bevor sie in die Tag-Laufzeitbibliothek ausgegeben werden. Sie können anfordern, dass eine oder mehrere dieser Transformationen durchgeführt werden, indem Sie die `transforms`-Eigenschaft beim Definieren einer Typdefinition in `extension.json` festlegen. Die `transforms`-Eigenschaft ist ein Array von Objekten, wobei jedes Objekt eine auszuführende Transformation darstellt.

Alle Transformationen benötigen einen `type`-Wert und einen `propertyPath`-Wert. Der `type` muss einer der Werte `function`, `remove` und `file` sein und beschreibt, welche Transformation von Experience Platform auf das Einstellungsobjekt angewendet werden soll. Der `propertyPath` ist eine durch Punkte getrennte Zeichenfolge, die Tags mitteilt, wo die zu ändernde Eigenschaft im Einstellungsobjekt zu finden ist. Es folgen ein Beispiel für ein Einstellungsobjekt und einige Angaben für `propertyPath`:

```js
{
  foo: {
    bar: "A string",
    baz: [
      "A",
      "B",
      "C"
    ]
  }
}
```

* Wenn Sie für `propertyPath` die Zeichenfolge `foo.bar` angeben, wird der Wert `"A string"` umgewandelt.
* Wenn Sie für `propertyPath` die Zeichenfolge `foo.baz[]` angeben, wird jeder Wert im Array `baz` umgewandelt.
* Wenn Sie für `propertyPath` die Zeichenfolge `foo.baz` angeben, wird das Array `baz` umgewandelt.

Für Eigenschaftenpfade können beliebige Kombinationen aus Array- und Objektnotation verwendet werden, um Transformationen auf jeder Ebene des Einstellungsobjekts anzuwenden.

>[!WARNING]
>
>Die Verwendung der Array-Notation im `propertyPath`-Attribut (z. B. `foo.baz[]`) wird im Sandboxtool für Erweiterungen noch nicht unterstützt.

In den folgenden Abschnitten werden die verfügbaren Transformationstypen und ihre Verwendung beschrieben.

#### Transformationstyp „function“

Die Funktionstransformation ermöglicht die Ausführung von Code, der von Experience Platform-Benutzern geschrieben wurde, durch ein Bibliotheksmodul in der ausgegebenen Tag-Laufzeitbibliothek.

Angenommen, wir möchten einen Aktionstyp für ein „benutzerdefiniertes Skript“ bereitstellen. Die Aktionsansicht „benutzerdefiniertes Skript“ bietet vielleicht einen Textbereich, in dem der Benutzer Code eingeben kann. Nehmen wir an, ein Benutzer hat den folgenden Code in den Textbereich eingegeben:

`console.log('Welcome, ' + username +'. This is ZomboCom.');`

Wenn der Benutzer die Regel speichert, kann das von der Ansicht gespeicherte Einstellungsobjekt wie folgt aussehen:

```javascript
{
  foo: {
    bar: "console.log('Welcome, ' + username +'. This is ZomboCom.');"
  }
}
```

Wenn eine Regel, die unsere Aktion verwendet, in der Tag-Laufzeitbibliothek ausgelöst wird, soll der Code des Benutzers ausgeführt und ihm ein Benutzername übergeben werden.

Wenn das settings-Objekt aus der Ansicht des Aktionstyps gespeichert wird, ist der Benutzercode einfach eine Zeichenfolge. Dies ist gut, da es ordnungsgemäß zu und von JSON serialisiert werden kann. Es ist jedoch auch schlecht, da es in der Tag-Laufzeitbibliothek normalerweise auch als Zeichenfolge und nicht als ausführbare Funktion ausgegeben wird. Obwohl Sie versuchen könnten, den Code innerhalb des Bibliotheksmoduls Ihres Aktionstyps mit [`eval`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) oder einem [Function-Konstruktor](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Function) auszuführen, wird davon dringend abgeraten, weil [Sicherheitsrichtlinien für Inhalte](https://developer.mozilla.org/en-US/docs/Web/Security/CSP) die Ausführung potenziell blockieren können.

Als Problemumgehung für diese Situation weist die Verwendung der Funktionstransformation Experience Platform an, den Code des Benutzers in eine ausführbare Funktion einzuschließen, wenn er in der Tag-Laufzeitbibliothek ausgegeben wird. Zur Lösung unseres Beispielproblems würden wir die Transformation in der Typdefinition in `extension.json` wie folgt definieren:

```json
{
  "transforms": [
    {
      "type": "function",
      "propertyPath": "foo.bar",
      "parameters": ["username"]
    }
  ]
}
```

* `type` definiert den Typ der Transformation, die auf das Einstellungsobjekt angewendet werden soll.
* `propertyPath` ist eine Zeichenfolge mit Punkt als Trennzeichen, die Experience Platform angibt, wo sich die Eigenschaft befindet, die im Einstellungsobjekt geändert werden muss.
* `parameters` ist ein Array von Parameternamen, die in die Signatur der Wrapping-Funktion aufgenommen werden sollen.

Wenn das Einstellungsobjekt in der Tag-Laufzeitbibliothek ausgegeben wird, wird es wie folgt umgewandelt:

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

Ihr Bibliotheksmodul kann dann die Funktion aufrufen, die den Code des Benutzers enthält, und das Argument `username` übergeben.

#### Transformationstyp „file“

Die Dateitransformation ermöglicht die Ausgabe von Code, der von Experience Platform-Benutzern geschrieben wurde, in eine Datei, die von der Tag-Laufzeitbibliothek getrennt ist. Die Datei wird zusammen mit der Tag-Laufzeitbibliothek gehostet und kann dann von der Erweiterung zur Laufzeit nach Bedarf geladen werden.

Angenommen, wir möchten einen Aktionstyp für ein „benutzerdefiniertes Skript“ bereitstellen. Die Ansicht des Aktionstyps kann einen Textbereich bereitstellen, in dem der Benutzer Code eingeben kann. Nehmen wir an, ein Benutzer hat den folgenden Code in den Textbereich eingegeben:

`console.log('This is ZomboCom.');`

Wenn der Benutzer die Regel speichert, kann das von der Ansicht gespeicherte Einstellungsobjekt wie folgt aussehen:

```js
{
  foo: {
    bar: "console.log('This is ZomboCom.');"
  }
}
```

Wir möchten, dass der Code des Benutzers in einer separaten Datei platziert wird, anstatt in die Tag-Laufzeitbibliothek aufgenommen zu werden. Wenn eine Regel, die unsere Aktion verwendet, in der Tag-Laufzeitbibliothek ausgelöst wird, soll der Code des Benutzers geladen werden, indem ein Skriptelement an den Dokument-Textkörper angehängt wird. Zur Lösung unseres Beispielproblems würden wir die Transformation in der Aktionstypdefinition in `extension.json` wie folgt definieren:

```json
{
  "transforms": [
    {
      "type": "file",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` definiert den Typ der Transformation, die auf das Einstellungsobjekt angewendet werden soll.
* `propertyPath` ist eine Zeichenfolge mit Punkt als Trennzeichen, die Experience Platform angibt, wo sich die Eigenschaft befindet, die im Einstellungsobjekt geändert werden muss.

Wenn das Einstellungsobjekt in der Tag-Laufzeitbibliothek ausgegeben wird, wird es wie folgt umgewandelt:

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

In diesem Fall wurde der Wert von `foo.bar` in eine URL transformiert. Die genaue URL wird zum Zeitpunkt der Erstellung der Bibliothek bestimmt. Die Datei erhält immer die Erweiterung `.js` und wird mit einem JavaScript-orientierten MIME-Typ bereitgestellt. Möglicherweise werden in Zukunft weitere MIME-Typen unterstützt.

#### Transformationstyp „remove“

Standardmäßig werden alle Eigenschaften des Einstellungsobjekts in der Tag-Laufzeitbibliothek ausgegeben. Wenn bestimmte Eigenschaften nur für die Erweiterungsansicht verwendet werden, insbesondere wenn sie vertrauliche Informationen enthalten (z. B. geheime Token), sollten Sie den Transformationstyp „remove“ verwenden, um zu verhindern, dass diese Informationen in die Tag-Laufzeitbibliothek ausgegeben werden.

Angenommen wir möchten einen neuen Aktionstyp bereitstellen. Die Ansicht des Aktionstyps kann ein Eingabefeld enthalten, in das der Benutzer einen geheimen Schlüssel eingeben kann, um eine Verbindung mit einer bestimmten API herzustellen. Nehmen wir an, ein Benutzer hat den folgenden Text in das Eingabefeld eingegeben:

`ABCDEFG`

Wenn der Benutzer die Regel speichert, kann das von der Ansicht gespeicherte Einstellungsobjekt wie folgt aussehen:

```js
{
  foo: {
    bar: "ABCDEFG"
  }
}
```

Wir möchten die Eigenschaft `bar` nicht in die Tag-Laufzeitbibliothek einschließen. Zur Lösung unseres Beispielproblems würden wir die Transformation in der Aktionstypdefinition in `extension.json` wie folgt definieren:

```json
{
  "transforms": [
    {
      "type": "remove",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` definiert den Typ der Transformation, die auf das Einstellungsobjekt angewendet werden soll.
* `propertyPath` ist eine Zeichenfolge mit Punkt als Trennzeichen, die Experience Platform angibt, wo sich die Eigenschaft befindet, die im Einstellungsobjekt geändert werden muss.

Wenn das Einstellungsobjekt in der Tag-Laufzeitbibliothek ausgegeben wird, wird es wie folgt umgewandelt:

```js
{
  foo: {
  }
}
```

In diesem Fall wurde der Wert von `foo.bar` aus dem settings-Objekt entfernt.
