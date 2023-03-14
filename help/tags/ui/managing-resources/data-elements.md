---
title: Datenelemente
description: Datenelemente sind Bausteine für Ihr Datenwörterbuch (oder Ihre Datenkarte). Verwenden Sie Datenelemente zum Sammeln, Organisieren und Bereitstellen von Daten in Marketing- und Werbetechnologie.
exl-id: 1e7b03cc-5a54-403d-bf8d-dbc206cfeb2d
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1622'
ht-degree: 97%

---

# Datenelemente

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Datenelemente sind Bausteine für Ihr Datenwörterbuch (oder Ihre Datenkarte). Verwenden Sie Datenelemente zum Sammeln, Organisieren und Bereitstellen von Daten in Marketing- und Werbetechnologie.

Ein einzelnes Datenelement ist eine Variable, deren Wert Abfragezeichenfolgen, URLs, Cookie-Werten, JavaScript-Variablen usw. zugeordnet werden kann. Sie können diesen Wert anhand des zugehörigen Variablennamens in Adobe Experience Platform referenzieren. Diese Sammlung von Datenelementen wird zum Wörterbuch definierter Daten, mit deren Hilfe Sie eigene Regeln erstellen können (Ereignisse, Bedingungen und Aktionen). Dieses Datenwörterbuch ist überall in Tags für die Verwendung mit beliebigen Erweiterungen verfügbar, die Sie Ihrer Eigenschaft hinzugefügt haben.

>[!IMPORTANT]
>
>Änderungen werden erst wirksam, nachdem sie [veröffentlicht](../publishing/overview.md) wurden.

Nutzen Sie Datenelemente so weit wie möglich für die Erstellung von Regeln, für die Konsolidierung der Definition von dynamischen Daten und zur Verbesserung der Effizienz Ihres Tagging-Vorgangs. Sie definieren die Datenregeln einmalig und können sie dann an mehreren Stellen nutzen.

Das Konzept wiederverwendbarer Datenelemente ist ein sehr leistungsstarkes und sollte in die Best Practices übernommen werden.

Wenn Sie beispielsweise auf eine bestimmte Weise auf Seitennamen oder Produkt-IDs verweisen oder Informationen aus Abfragezeichenfolgenparametern von einem Affiliate-Marketing-Link oder von [!DNL AdWords] abrufen, etc. können Sie ein Datenwörterbuch (Datenelemente) erstellen, indem Sie Informationen aus seiner Quelle abrufen und diese Daten dann in verschiedenen Tag-Regeln verwenden.

Hier das Beispiel „Seitennamen“: Nehmen wir an, dass Sie ein bestimmtes Seitennamensschema durch Referenzierung einer Datenschicht, eines `document.title`-Elements oder eines Überschrift-Tags auf der Website verwenden. Mit Tags in Adobe Experience Platform können Sie ein Datenelement erstellen, das für diesen Datenpunkt als alleiniger Bezugspunkt dient. Anschließend können Sie das Datenelement in allen Regeln verwenden, die auf den Seitennamen verweisen sollen. Sollten Sie sich in Zukunft dafür entscheiden, die Referenzierung des Seitennamens zu ändern (Sie haben beispielsweise bisher mit `document.title` gearbeitet, möchten nun aber auf eine bestimmte Datenschicht umstellen), müssen Sie nur eine einzige Regel bearbeiten, um die Referenzierung anzupassen. Ändern Sie einfach die eine Referenz im Datenelement, und alle Regeln, die dieses Datenelement nutzen, werden automatisch aktualisiert.

>[!NOTE]
>
>Wenn ein Datenelement nicht in einer Regel referenziert ist, wird es auf keiner Seite geladen, sofern es nicht speziell über ein benutzerdefiniertes Skript aufgerufen wird.

Datenelemente enthalten Daten, wenn sie in Regeln verwendet oder manuell in einem Skript aufgerufen werden. Auf übergeordneter Ebene bedeutet das:

1. [Erstellen Sie ein Datenelement](#create-a-data-element), falls noch keines vorhanden ist.
1. Verwenden Sie das Datenelement in einer [-Regel](./rules.md) oder einem benutzerdefinierten Skript.

## Verwendung von Datenelementen

### In Regeln

Sie können Datenelemente auf der Benutzeroberfläche zur Regelbearbeitung verwenden, indem Sie mithilfe des Suchfelds nach dem Namen des Datenelements suchen.

### In benutzerdefinierten Skripten

Mithilfe der `_satellite`-Objektsyntax können Sie Datenelemente in benutzerdefinierten Skripten verwenden:

`_satellite.getVar('data element name');`

## ein Datenelement erstellen {#create-a-data-element}

Datenelemente stellen die Bausteine zum Erstellen von Regeln dar. Dank Datenelementen sind Sie dazu in der Lage, für beliebige Objekte auf Ihrer Site ein Datenwörterbuch (oder eine Datenkarte) der häufig verwendeten Elemente einer Seite zu erstellen, unabhängig davon, wo deren Ursprung liegt (Abfragezeichenfolgen, URLs oder Cookie-Werte).

1. Öffnen Sie auf einer Eigenschaftsseite die Registerkarte [!UICONTROL Datenelemente] und wählen Sie **[!UICONTROL Neues Datenelement erstellen]** aus.
1. Benennen Sie das Datenelement.
1. Wählen Sie eine Erweiterung und einen Typ aus.

   Die verfügbaren Datenelementtypen werden durch die Erweiterung bestimmt. Informationen zu den mit der Haupt-Tag-Erweiterung verfügbaren Typen finden Sie unter [Typen von Datenelementen](data-elements.md#types-of-data-elements).

1. Stellen Sie in den vorhandenen Feldern die angeforderten Informationen zum ausgewählten Typ bereit.
1. (Optional) Geben Sie einen Standardwert ein.

   Wenn Sie diese Option nicht auswählen, gibt es keinen Standardwert. Die meisten Benutzer belassen dies im Standardzustand. Verschiedene Systeme gehen unterschiedlich mit einer leeren Variablen um. Manche Personen geben z. B. „Kein“ oder „k. A.“ ein, damit sie eine konsistente Berichterstellung erhalten, wenn das Datenelement keinen Wert zurückgibt.

1. Wählen Sie aus, ob Sie einen klein geschriebenen Wert erzwingen und Zeilenumbrüche und Leerzeichen entfernen möchten.
1. Wählen Sie eine Dauer aus.

   Die verfügbaren Auswahlmöglichkeiten lauten wie folgt:

   * Keine
      * Der Wert wird nicht gespeichert.
   * Page view
      * Der Wert wird in einer JavaScript-Variablen gespeichert, bis die Seite aktualisiert oder eine neue Seite geladen wird.
      * Kann mithilfe der `_satellite`-Objektsyntax erstellt und in Skripten festgelegt werden:

         `_satellite.setVar('data_element_name')`
   * Session
      * Werte bleiben bis zum Schließen der Browser-Registerkarte im Sitzungsspeicher des Browsers erhalten.
      * Verfügbar während des gesamten Site-Besuchs.
   * Visitor
      * Der Wert wird unbegrenzt im lokalen Speicher des Browsers gespeichert.

1. Wählen Sie **[!UICONTROL Speichern]** aus.

Beim Erstellen oder Bearbeiten von Elementen können Sie in Ihrer [aktiven Bibliothek](../publishing/libraries.md#active-library) speichern und Erstellungen vornehmen. Dadurch werden Ihre Änderungen direkt in Ihrer Bibliothek gespeichert, und ein Build wird ausgeführt. Der Build-Status wird angezeigt. Sie können auch eine neue Bibliothek über das Dropdown-Feld [!UICONTROL Aktive Bibliothek] erstellen.

## Datenelement-Typen {#types-of-data-elements}

Datenelementtypen werden durch die Erweiterung bestimmt. Die erstellbaren Typen sind nicht beschränkt.

In den folgenden Abschnitten werden die in der Haupterweiterung verfügbaren Datenelementtypen beschrieben. In anderen Erweiterungen werden andere Datenelementtypen verwendet.

### Cookie

Jedes verfügbare Domain-Cookie kann im Cookie-Namensfeld referenziert werden.

#### Beispiel:

`cookieName`

### Benutzerspezifischer Code

Benutzerdefiniertes JavaScript kann auf der Benutzeroberfläche eingegeben werden, indem Sie auf [!UICONTROL Editor öffnen] klicken und den Code in das Editor-Fenster einfügen.

Eine Rückkehranweisung ist im Editor erforderlich, damit festgelegt ist, welcher Wert als Datenelementwert festgelegt wird. Wenn keine Rückgabeanweisung enthalten ist, wird das Datenelement aufgelöst zu `undefined`. Dadurch wird der Fallback ausgelöst, um nach einem gespeicherten Wert zu suchen, und dann ein Standardwert verwendet, wenn kein gespeicherter Wert vorhanden ist.

**Beispiel:**

```text
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Benutzerdefinierter Code kann das Objekt `event` aus der aufrufenden Regel als Argument akzeptieren. Dadurch kann der Code dort den Wert lesen.

**Beispiel:**

```text
// `event` is the default object provided by the rule
var eventType = event.$type;
return eventType; // if this data element is called from a "DOM Ready" event, then `core.dom-ready` is returned
```

Mithilfe der `_satellite`-Objektsyntax können Sie dies dann in benutzerdefinierten Skripten verwenden:

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

Bei Verwendung von Prozent (`%`), müssen Sie nur den Datenelementnamen angeben. Sie brauchen `event` nicht zu spezifizieren.

```text
%data element name%
```

### DOM-Attribut

Es kann ein beliebiger Elementwert abgerufen werden, z. B. „div“ oder H1-Tag.

#### Beispiel:

CSS-Auswahlkette:

`id#dc logo img`

Wert abrufen von:

`src`

### JavaScript-Variable

Verfügbare JavaScript-Objekte oder -Variablen können mit dem Pfadfeld referenziert werden.

Wenn Sie JavaScript-Variablen oder Objekteigenschaften in Ihrem Markup erfassen und diese mit Ihren Erweiterungen oder Regeln verwenden möchten, können Datenelemente zum Erfassen dieser Werte verwendet werden. Auf diese Weise können Sie das Datenelement allen Ihren Regeln referenzieren, und sollte sich die Quelle der Daten jemals ändern, müssen Sie nur den Verweis auf die Quelle (das Datenelement) an einer Stelle in  ändern.

Nehmen wir beispielsweise an, das Markup enthält eine JavaScript-Variable namens `Page_Name` wie hier gezeigt:

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Sie müssen den Pfad zu dieser Variablen angeben, wenn Sie das Datenelement erstellen.

Wenn Sie ein Datenerfassungsobjekt als Teil Ihrer Datenschicht verwenden, verwenden Sie im Pfad Punktnotation zur Referenzierung des Objekts und der Eigenschaft, die Sie im Datenelement erfassen möchten, z. B. `_myData.pageName`oder `digitalData.pageName` usw.

#### Beispiel:

`window.document.title`

### Lokaler Speicher

Geben Sie den Namen Ihres lokalen Speicherelements im Feld [!UICONTROL Name des lokalen Speicherelements] an.

Der lokale Speicher bietet Browsern die Möglichkeit, Informationen seitenweise zu speichern ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). Die Funktion des lokalen Speichers ähnelt der von Cookies sehr stark. Er ist jedoch deutlich größer und bietet mehr Flexibilität.

Geben Sie in dem bereitgestellten Feld den Wert an, den Sie für ein lokales Speicherelement erstellt haben, z. B. `lastProductViewed.`

### Seiteninfo

Verwenden Sie diese Datenpunkte zum Erfassen von Seiteninfos für Ihre Regellogik oder zum Senden von Informationen an [!DNL Analytics] oder externe Tracking-Systeme.

Sie können eines der folgenden Seitenattribute auswählen, um es in Ihrem Datenelement zu verwenden:

* URL
* Hostname
* Pathname
* Protocol
* Referrer
* Title

### Query String Parameter

Geben Sie im Feld [!UICONTROL URL-Parameter] einen einzelnen URL-Parameter an.

Nur der Abschnitt „Name“ ist erforderlich und spezielle Bezeichner wie „?“ oder „=“ sollten weggelassen werden.

#### Beispiel:

`contentType`

### Zufällige Nummer

Verwenden Sie dieses Datenelement zum Generieren einer zufälligen Nummer. Sie wird häufig zum Sampling von Daten oder zum Erstellen von IDs wie einer Treffer-ID verwendet. Die Zufallszahl kann auch verwendet werden, um sensible Daten zu verschleiern oder zu verbergen. Mögliche Beispiele sind:

* Generieren einer Treffer-ID
* Verketten der Nummer für ein Benutzer-Token oder einen Zeitstempel zur Gewährleistung der Eindeutigkeit
* Ausführen eines unidirektionalen Hash-Vorgangs für PII-Daten
* Zufälliges Entscheiden, wann auf der Seite eine Anfrage zu einer Umfrage angezeigt wird

Geben Sie den Minimal- und Maximalwert für Ihre zufällige Nummer an.

**Standardeinstellungen:**

Minimum: 0

Maximum: 1000000000

### Sitzungsspeicher

Geben Sie den Namen Ihres Sitzungsspeicherelements im Feld [!UICONTROL Name des Sitzungsspeicherelements] an.

Der Sitzungsspeicher ähnelt dem lokalen Speicher. Der Unterschied besteht darin, dass die Daten nach Ende der Sitzung verworfen werden. Beim lokalen Speicher oder einem Cookie bleiben die Daten hingegen möglicherweise gespeichert.

### Besucherverhalten

Dieses Datenelement verwendet ähnlich wie die Seiteninformationen allgemeine Verhaltenstypen zur Erweiterung der Logik in Regeln oder anderen Platform-Lösungen.

Wählen Sie eines der folgenden Attribute für das Besucherverhalten aus:

* Landing page
* Traffic-Quelle
* Minutes on site
* Session count
* Session page view count
* Lifetime page view count
* Is new visitor

Einige häufige Anwendungsfälle lauten wie folgt:

* Anzeigen einer Umfrage, nachdem ein Besucher fünf Minuten auf der Site war
* Wenn dies die Landingpage für den Besuch ist, füllen Sie eine [!DNL Analytics]-Metrik
* Anzeigen eines neuen Angebots für den Besucher nach X Sitzungen
* Anzeigen einer Newsletter-Registrierung, wenn es sich um einen erstmaligen Besucher handelt

## Integrierte Datenelemente

Sie müssen zusätzliche benutzerdefinierte Datenelemente erstellen, wenn Sie zuvor eines der folgenden Datenelemente verwendet haben:

* URI
* Protocol
* Hostname
