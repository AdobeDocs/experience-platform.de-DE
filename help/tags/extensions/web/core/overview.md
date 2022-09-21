---
title: Core-Erweiterung – Übersicht
description: Machen Sie sich mit der Haupt-Tag-Erweiterung in Adobe Experience Platform vertraut.
exl-id: 841f32ad-a6a8-49fb-a131-ef4faab47187
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '5482'
ht-degree: 96%

---

# Core-Erweiterung – Übersicht

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Die Haupt-Tag-Erweiterung ist die mit Adobe Experience Platform veröffentlichte Standarderweiterung.

Dieses Dokument enthält Informationen zu den verfügbaren Optionen bei der Verwendung der Haupterweiterung zum Erstellen einer Regel.

## Ereignistypen für die Haupterweiterung {#core-extension-event-types}

In diesem Thema werden die in der Haupterweiterung verfügbaren Ereignistypen beschrieben. Informationen zu den Optionen, die für verschiedene Ereignistypen festgelegt werden können, finden Sie im Abschnitt [Optionen](#options).

### Browser-basierte Ereignisse

#### Tab Blur

Das Ereignis „tab-blur“ löst die Aktion aus, wenn eine Registerkarte den Fokus verliert. Für diesen Ereignistyp sind keine Einstellungen vorhanden.

#### Tab Focus

Das Ereignis „tab-focus“ löst die Aktion aus, wenn eine Registerkarte den Fokus erhält. Für diesen Ereignistyp sind keine Einstellungen vorhanden.

### Formular

#### Blur

Das Ereignis „blur“ löst die Aktion aus, wenn ein Formular den Fokus verliert. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

#### Focus

Das Ereignis „focus“ löst die Aktion aus, wenn ein Formular den Fokus erhält. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

#### Submit

Das Ereignis „submit“ löst die Aktion aus, wenn ein Formular gesendet wird. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

### Tastaturgesteuerte Ereignisse

#### Key Press

Das Ereignis wird ausgelöst, wenn eine Taste gedrückt wird. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

### Medienbasierte Ereignisse

#### Media Ended

Das Ereignis wird ausgelöst, wenn das Medium beendet wird. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

#### Media-Loaded Data

Das Ereignis wird ausgeslöst, wenn Daten durch Medien geladen werden. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

#### Media Pause

Das Ereignis wird ausgelöst, wenn das Medium pausiert wird. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

#### Media Play

Das Ereignis wird ausgelöst, wenn das Medium wiedergegeben wird. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

#### Media Stalled

Das Ereignis wird ausgelöst, wenn das Medium angehalten wird. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

#### Media-Time Played

Das Ereignis wird ausgelöst, wenn das Medium für eine bestimmte Zeitdauer wiedergegeben wird. Sie müssen die Dauer festlegen, für die das Medium wiedergegeben werden muss, damit das Ereignis ausgelöst wird. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).


#### Media-Volume Changed

Das Ereignis wird ausgelöst, wenn die Lautstärke erhöht oder verringert wird. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

### Mobilgeräteorientierte Ereignisse

#### Orientation Change

Das Ereignis wird Trigger, wenn sich die Ausrichtung des Geräts ändert. Sie müssen die Dauer angeben, für die die Ausrichtung geändert werden muss, damit das Ereignis ausgelöst wird. Für diesen Ereignistyp sind keine Einstellungen vorhanden.

#### Zoom Change

Das Ereignis wird ausgelöst, wenn der Benutzer die Ansicht vergrößert oder verkleinert. Für diesen Ereignistyp sind keine Einstellungen vorhanden.

### Mausgesteuerte Ereignisse

#### Click

Das Ereignis wird ausgelöst, wenn das angegebene Element ausgewählt (angeklickt) wird. Optional können Sie Eigenschaftswerte angeben, die für das Element „true“ sein müssen, bevor das Ereignis ausgelöst wird.

Wenn das Element ein Anker-Tag (`<a>`) zu verlinkten Inhalten ist, können Sie auch angeben, ob die Navigation für einen bestimmten Zeitraum verzögert werden soll. Dies kann nützlich sein, wenn die Ausführung Ihrer Regel mehr Zeit erfordert und normalerweise nicht abgeschlossen würde, bevor die Seitennavigation stattfindet.

>[!WARNING]
>
>Bei dieser Option ist äußerste Vorsicht geboten, da sie sich bei falscher Verwendung negativ auf das Anwendererlebnis auswirken kann.

Wenn Sie die Link-Verzögerung verwenden, verhindert Platform tatsächlich, dass der Browser von der Seite weg navigiert. Anschließend führt es nach der angegebenen Zeitüberschreitung eine JavaScript-Umleitung zum ursprünglichen Ziel durch. Dies ist besonders dann problematisch, wenn Ihr Seiten-Markup `<a>`-Tags enthält, bei denen die vorgesehene Funktion den Benutzer nicht tatsächlich weg von der Seite navigieren lässt. Wenn Sie Ihr Problem nicht anders lösen können, sollten Sie mit der Definition Ihrer Auswahl sehr genau umgehen, damit dieses Ereignis nur genau dort ausgelöst wird, wo Sie es brauchen, und sonst nirgends.

Der Standardwert für die Link-Verzögerung ist 100 Millisekunden. Beachten Sie, dass Tags immer auf die angegebene Zeitdauer warten und in keiner Weise mit der Ausführung der Regelaktionen verbunden sind. Es ist möglich, dass die Verzögerung den Benutzer zwingt, länger zu warten, als nötig ist, und dass die Verzögerung auch nicht lang genug ist, damit alle Aktionen der Regel erfolgreich abgeschlossen werden können. Größere Verzögerungen bieten mehr Zeit für die Regelausführung, verschlechtern aber auch das Benutzererlebnis.

Um die Verzögerung zu implementieren, müssen sowohl das ausgewählte Element, das das Ereignis auslöst, als auch der spezifische Zeitraum angegeben werden, bevor das Ereignis ausgelöst wird.

Weitere Informationen zu den erweiterten Optionen finden Sie im Abschnitt [Optionen](#options).

#### Hover

Das Ereignis wird ausgelöst, wenn der Benutzer den Mauszeiger über ein angegebenes Element bewegt. Konfigurieren Sie zudem, ob die Regel sofort oder nach einer angegebenen Anzahl Millisekunden ausgelöst wird. Im Abschnitt [Optionen](#options) finden Sie weitere Informationen zu anpassbaren Ereigniseinstellungen.

### Andere Ereignisse

#### Custom Event

Das Ereignis wird ausgelöst, wenn ein benutzerspezifischer Ereignistyp eintritt. Benannte JavaScript-Funktionen, die an anderer Stelle in der Code-Basis definiert sind, können als benutzerdefinierter Ereignistyp verwendet werden. Sie müssen den Namen des benutzerdefinierten Ereignistyps angeben und alle anderen Einstellungen konfigurieren, wie im Abschnitt [Optionen](#options) unten beschrieben.

#### Data Element Changed

Das Ereignis wird ausgelöst, wenn sich ein angegebenes Datenelement ändert. Sie müssen einen Namen für das Datenelement angeben. Sie können das Datenelement auswählen, indem Sie entweder seinen Namen in das Textfeld eingeben oder auf der rechten Seite des Textfelds das Datenelementsymbol auswählen und im angezeigten Dialogfeld aus einer Liste wählen.

#### Direktaufruf {#direct-call-event}

Ein Direktaufruferereignis umgeht die Ereigniserkennung und Suchsysteme. Direktaufrufregeln eignen sich optimal für Situationen, in denen Sie dem System explizit vorgeben möchten, was passieren soll. Außerdem eignen sich Regeln dieses Typs ideal für Fälle, in denen das System kein Ereignis im DOM erkennen kann.

Beim Definieren eines Direktaufrufereignisses müssen Sie eine Zeichenfolge angeben, die als Kennung dieses Ereignisses fungiert. Wenn eine [Trigger-Direktaufruf-Aktion](#direct-call-action) mit derselben Kennung ausgelöst wird, werden alle Regeln für Direktaufrufereignisse ausgeführt, die auf diese Kennung warten.

![Screenshot eines Direktaufruferereignisses in der Datenerfassungs-Benutzeroberfläche](../../../images/extensions/core/direct-call-event.png)

#### Element Exists

Das Ereignis wird ausgelöst, wenn ein angegebenes Element vorhanden ist. Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

#### Enters Viewport

Das Ereignis wird ausgelöst, wenn der Benutzer einen angegebenen Viewport aufruft. Sie müssen einen CSS-Selektor als Kriterium für das Targeting von übereinstimmenden Elementen bereitstellen. Sie müssen außerdem konfigurieren, ob die Regel sofort oder nach einer bestimmten Anzahl von Millisekunden ausgelöst wird und ob das Ereignis bei jedem Auftreten des Ereignisses oder nur beim ersten Mal ausgelöst werden soll.

Weitere Informationen zu anpassbaren Ereigniseinstellungen finden Sie im Abschnitt [Optionen](#options).

#### History Change

Das Ereignis wird ausgelöst, wenn ein pushState- oder ein hashchange-Ereignis auftritt. Für diesen Ereignistyp sind keine Einstellungen vorhanden.

#### Time-Spent on Page

Das Ereignis wird ausgelöst, wenn der Benutzer für eine bestimmte Anzahl Sekunden auf der Seite bleibt. Geben Sie die Anzahl Sekunden an, die vergehen müssen, bevor das Ereignis ausgelöst wird.

### Seitenladereignisse

#### DOM Ready

Das Ereignis wird ausgelöst, wenn das DOM bereit ist und wenn der Benutzer mit der Seite interagieren kann. Für diesen Ereignistyp sind keine Einstellungen vorhanden.

#### Library Loaded (Page Top) {#library-loaded-page-top}

Das Ereignis wird ausgelöst, sobald die Tag-Bibliothek geladen wird. Für diesen Ereignistyp sind keine Einstellungen vorhanden.

#### Page Bottom {#page-bottom}

Das Ereignis wird ausgelöst, wenn `_satellite.pageBottom();` aufgerufen wurde. Beim asynchronen Laden der Tag-Bibliothek sollte dieser Ereignistyp nicht verwendet werden. Für diesen Ereignistyp sind keine Einstellungen vorhanden.

#### Window Loaded

Das Ereignis wird ausgelöst, wenn onLoad vom Browser aufgerufen wird und die Seite fertig geladen wurde. Für diesen Ereignistyp sind keine Einstellungen vorhanden.

### Optionen {#options}

Für die einzelnen Formularereignistypen werden die folgenden Einstellungen verwendet:

#### Specific Elements \| Any Element

* Wenn Sie **[!UICONTROL Bestimmte Elemente]** auswählen, werden die Optionen zum Auswählen der Elemente und Eigenschaftswerte angezeigt.
* Wenn Sie **[!UICONTROL Beliebiges Element]** auswählen, sind keine weiteren Optionen erforderlich, um die Elemente einzugrenzen.

#### Elements matching the CSS selector

Geben Sie die CSS-Auswahl zur Identifizierung der Elemente ein, anhand deren das Ereignis ausgelöst wird.

#### And having certain property values

Wenn Sie diese Option auswählen, werden folgende Parameter verfügbar:

* `property=value`

   Geben Sie den Wert für die Eigenschaft an

* Regex

   Aktivieren Sie diese Option, wenn `property=value` ein regulärer Ausdruck ist.

* Add

   Fügen Sie ein weiteres `property=value`-Paar hinzu.

#### Advanced options (Bubbling)

* Führen Sie diese Regel auch dann aus, wenn das Ereignis aus einem nachkommenden Element stammt
* Lassen Sie die Ausführung dieser Regel auch dann zu, wenn durch das Ereignis bereits eine Regel ausgelöst wurde, die auf ein nachkommendes Element abzielt
* Nach dem Ausführen der Regel wird verhindert, dass durch das Ereignis Regeln ausgelöst werden, die auf Vorgängerelemente abzielen

## Bedingungstypen für die Haupterweiterung

In diesem Abschnitt werden die in der Haupterweiterung verfügbaren Bedingungstypen beschrieben. Diese Bedingungstypen können entweder mit dem Logiktyp „normal“ oder „Ausnahme“ verwendet werden.

### Daten

#### Cookie

Geben Sie den Cookie-Namen und -Wert an, der für ein Ereignis vorhanden sein muss, damit eine Aktion ausgelöst wird.

1. Geben Sie einen Cookie-Namen an.
1. Geben Sie den Wert ein, der im Cookie vorhanden sein muss, wenn das Ereignis eine Aktion auslösen soll.
1. (Optional) Aktivieren Sie reguläre Ausdrücke, wenn dies ein regulärer Ausdruck ist.

#### Benutzerspezifischer Code

Geben Sie einen benutzerspezifischen Code an, der als Bedingung des Ereignisses vorhanden sein muss.

>[!NOTE]
>
>ES6+ JavaScript wird jetzt in benutzerdefiniertem Code unterstützt. Beachten Sie, dass einige ältere Browser ES6+ nicht unterstützen. Um die Auswirkungen der Verwendung von ES6+-Funktionen zu verstehen, testen Sie sie bitte mit allen zu unterstützenden Webbrowsern.

Verwenden Sie für die Eingabe des benutzerspezifischen Codes den integrierten Code-Editor:

1. Wählen Sie **[!UICONTROL Editor öffnen]**.
1. Geben Sie den benutzerspezifischen Code ein.
1. Wählen Sie **[!UICONTROL Speichern]** aus.

Automatisch wird eine Variable mit der Bezeichnung `event` verfügbar, die Sie in Ihrem benutzerdefinierten Code referenzieren können. Das `event`-Objekt enthält nützliche Informationen zum Ereignis, das die Regel ausgelöst hat. Die einfachste Methode zur Bestimmung der verfügbaren Ereignisdaten besteht darin, `event` mit dem console.log-Befehl in Ihrem benutzerspezifischen Code auf der Konsole auszugeben:

```javascript
console.log(event);
return true;
```

Führen Sie die Regel in einem Browser aus und überprüfen Sie das aufgezeichnete Ereignisobjekt in der Browser-Konsole. Sobald Sie wissen, welche Informationen verfügbar sind, können Sie sie für programmatische Entscheidungen in Ihrem benutzerspezifischen Code verwenden.

*Bedingungssequenzierung*

Wenn die Option &quot;Run rule components in sequence&quot;in den Eigenschafteneinstellungen aktiviert ist, können Sie festlegen, dass nachfolgende Regelkomponenten warten, während Ihre Bedingung eine asynchrone Aufgabe ausführt.

Wenn die Bedingung einen [Promise](https://developer.mozilla.org/de-DE/docs/Web/JavaScript/Reference/Global_Objects/Promise) zurückgibt, wird die nächste Bedingung in der Regel erst ausgeführt, nachdem der zurückgegebene Promise eingelöst wurde. Wenn die Zusage abgelehnt wird, betrachtet Tags diese Bedingung als fehlgeschlagen und es werden keine weiteren Bedingungen oder Aktionen aus dieser Regel ausgeführt

Beispiel einer Bedingung, die einen Promise zurückgibt:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

#### Wertvergleich {#value-comparison}

Vergleicht zwei Werte, um zu ermitteln, ob diese Bedingung „true“ zurückgibt.

Wenn Sie eine Regel mit mehreren Bedingungen haben, ist es möglich, dass diese Bedingung möglicherweise „true“ zurückgibt, die Regel jedoch trotzdem nicht ausgelöst wird, weil die andere Bedingung als „false“ oder eine der Ausnahmen als „true“ ausgewertet wird.

1. Stellen Sie einen Wert bereit.
1. Wählen Sie den Operator aus. Weitere Einzelheiten dazu finden Sie unten in der Liste der Wertvergleichsoperatoren.
1. (Falls erforderlich) Wählen Sie aus, ob bei dem Vergleich nicht nach Groß-/Kleinschreibung unterschieden werden soll.
1. Stellen Sie einen anderen Wert für den Vergleich bereit.

Die folgenden Wertvergleichsoperatoren sind verfügbar:

**Equal:** Die Bedingung gibt „true“ zurück, wenn die beiden Werte anhand eines nicht strikten Vergleichs gleich sind (in JavaScript der Operator ==). Die Werte können einem beliebigen Typ entsprechen: Wenn Sie ein Wort wie _wahr_, _falsch_, _null_ oder _undefiniert_ in ein Wertfeld eingeben, wird das Wort als Zeichenfolge verglichen und nicht in das zugehörige JavaScript-Äquivalent konvertiert.

**Does Not Equal:** Die Bedingung gibt „true“ zurück, wenn die beiden Werte anhand eines nicht strikten Vergleichs nicht gleich sind (in JavaScript der Operator !=). Die Werte können einem beliebigen Typ entsprechen: Wenn Sie ein Wort wie _wahr_, _falsch_, _null_ oder _undefiniert_ in ein Wertfeld eingeben, wird das Wort als Zeichenfolge verglichen und nicht in das zugehörige JavaScript-Äquivalent konvertiert.

**Contains:** Die Bedingung gibt „true“ zurück, wenn der erste Wert den zweiten Wert enthält. Zahlen werden in Zeichenfolgen konvertiert. Bei Werten, die keine Zahl oder Zeichenfolge sind, gibt die Bedingung „false“ zurück.

**Does Not Contain:** Die Bedingung gibt „true“ zurück, wenn der erste Wert den zweiten Wert nicht enthält. Zahlen werden in Zeichenfolgen konvertiert. Bei Werten, die keine Zahl oder Zeichenfolge sind, gibt die Bedingung „true“ zurück.

**Starts With:** Die Bedingung gibt „true“ zurück, wenn der erste Wert mit dem zweiten Wert beginnt. Zahlen werden in Zeichenfolgen konvertiert. Bei Werten, die keine Zahl oder Zeichenfolge sind, gibt die Bedingung „false“ zurück.

**Does Not Start With:** Die Bedingung gibt „true“ zurück, wenn der erste Wert nicht mit dem zweiten Wert beginnt. Zahlen werden in Zeichenfolgen konvertiert. Bei Werten, die keine Zahl oder Zeichenfolge sind, gibt die Bedingung „true“ zurück.

**Ends With:** Die Bedingung gibt „true“ zurück, wenn der erste Wert mit dem zweiten Wert endet. Zahlen werden in Zeichenfolgen konvertiert. Bei Werten, die keine Zahl oder Zeichenfolge sind, gibt die Bedingung „false“ zurück.

**Does Not End With:** Die Bedingung gibt „true“ zurück, wenn der erste Wert nicht mit dem zweiten Wert endet. Zahlen werden in Zeichenfolgen konvertiert. Bei Werten, die keine Zahl oder Zeichenfolge sind, gibt die Bedingung „true“ zurück.

**Matches Regex:** Die Bedingung gibt „true“ zurück, wenn der erste Wert mit dem regulären Ausdruck übereinstimmt. Zahlen werden in Zeichenfolgen konvertiert. Bei Werten, die keine Zahl oder Zeichenfolge sind, gibt die Bedingung „false“ zurück.

**Does Not Match Regex:** Die Bedingung gibt „true“ zurück, wenn der erste Wert nicht mit dem regulären Ausdruck übereinstimmt. Zahlen werden in Zeichenfolgen konvertiert. Bei Werten, die keine Zahl oder Zeichenfolge sind, gibt die Bedingung „true“ zurück.

**Is Less Than:** Die Bedingung gibt „true“ zurück, wenn der erste Wert kleiner als der zweite Wert ist. Zahlen repräsentierende Zeichenfolgen werden in Zahlen konvertiert. Bei Werten, die keine Zahl oder konvertierbare Zeichenfolge sind, gibt die Bedingung „false“ zurück.

**Is Less Than Or Equal To:** Die Bedingung gibt „true“ zurück, wenn der erste Wert kleiner oder gleich dem zweiten Wert ist. Zahlen repräsentierende Zeichenfolgen werden in Zahlen konvertiert. Bei Werten, die keine Zahl oder konvertierbare Zeichenfolge sind, gibt die Bedingung „false“ zurück.

**Is Greater Than:** Die Bedingung gibt „true“ zurück, wenn der erste Wert größer als der zweite Wert ist. Zahlen repräsentierende Zeichenfolgen werden in Zahlen konvertiert. Bei Werten, die keine Zahl oder konvertierbare Zeichenfolge sind, gibt die Bedingung „false“ zurück.

**Is Greater Than Or Equal To:** Die Bedingung gibt „true“ zurück, wenn der erste Wert größer oder gleich dem zweiten Wert ist. Zahlen repräsentierende Zeichenfolgen werden in Zahlen konvertiert. Bei Werten, die keine Zahl oder konvertierbare Zeichenfolge sind, gibt die Bedingung „false“ zurück.

**Is True:** Die Bedingung gibt „true“ zurück, wenn der Wert ein boolescher Wert mit dem Wert „true“ ist. Der von Ihnen bereitgestellte Wert wird nicht in einen booleschen Wert konvertiert, wenn er einem anderen Typ entspricht. Bei Werten, die kein boolescher Wert vom Typ „true“ sind, gibt die Bedingung „false“ zurück.

**Is Truthy:** Die Bedingung gibt „true“ zurück, wenn der Wert nach dem Konvertieren in einen booleschen Wert „true“ ist. Beispiele für Truthy-Werte finden Sie in der [Truthy-Dokumentation von MDN](https://developer.mozilla.org/de-DE/docs/Glossary/Truthy).

**Is False:** Die Bedingung gibt „true“ zurück, wenn der Wert ein boolescher Wert mit dem Wert „false“ ist. Der von Ihnen bereitgestellte Wert wird nicht in einen booleschen Wert konvertiert, wenn er einem anderen Typ entspricht. Bei Werten, die kein boolescher Wert vom Typ „false“ sind, gibt die Bedingung „false“ zurück.

**Is Falsy:** Die Bedingung gibt „true“ zurück, wenn der Wert nach dem Konvertieren in einen booleschen Wert „false“ ist. Beispiele für Falsy-Werte finden Sie in der [Falsy-Dokumentation von MDN](https://developer.mozilla.org/de-DE/docs/Glossary/Falsy).

#### Variable

Geben Sie den JavaScript-Variablennamen und -wert an, der für ein Ereignis vorhanden sein muss, damit eine Aktion ausgelöst wird.

1. Geben Sie den JavaScript-Variablennamen an.
1. Geben Sie den Variablenwert an, der als Bedingung für das Ereignis vorhanden sein muss.
1. (Optional) Aktivieren Sie reguläre Ausdrücke, wenn dies ein regulärer Ausdruck ist.

### Interaktion

#### Landing Page

Geben Sie die Seite an, auf der der Benutzer landen muss, um das Ereignis auszulösen.

1. Geben Sie die Landingpage an.
1. (Optional) Aktivieren Sie reguläre Ausdrücke, wenn dies ein regulärer Ausdruck ist.

#### New/Returning Visitor

Geben Sie an, ob der Besucher ein neuer oder ein wiederkehrender Besucher sein muss, damit ein Ereignis eine Aktion auslöst.

Wählen Sie eine der folgenden Optionen aus:

* New Visitor
* Returning Visitor

#### Page Views

Konfigurieren Sie die Anzahl Seitenansichten durch den Besucher, bevor die Aktion ausgelöst wird.

1. Wählen Sie aus, ob die Anzahl Seitenansichten größer, gleich oder kleiner als der angegebene Wert sein muss.
1. Geben Sie die Anzahl Seitenansichten an, mit deren Hilfe bestimmt wird, ob die Bedingung erfüllt ist.
1. Konfigurieren Sie, wann die Seitenansichten gezählt werden, indem Sie eine der folgenden Optionen auswählen:
   * Lifetime
   * Current Session

#### Sessions

Lösen Sie die Aktion aus, wenn die Anzahl Sitzungen des Benutzers die angegebenen Kriterien erfüllt.

1. Wählen Sie aus, ob die Anzahl Sitzungen größer, gleich oder kleiner als der angegebene Wert sein muss.
1. Geben Sie die Anzahl Sitzungen an, mit deren Hilfe bestimmt wird, ob die Bedingung erfüllt ist.

#### Time On Site

Lösen Sie die Aktion aus, wenn die Anzahl Sitzungen des Benutzers die angegebenen Kriterien erfüllt.

Konfigurieren Sie, wie lange der Besucher auf der Site bleiben muss, bevor die Aktion ausgelöst wird.

1. Wählen Sie aus, ob die Anzahl Minuten, die sich der Besucher auf der Site befindet, größer, gleich oder kleiner als der angegebene Wert sein muss.
1. Geben Sie die Anzahl Minuten an, mit deren Hilfe bestimmt wird, ob die Bedingung erfüllt ist.

#### Traffic Source

Lösen Sie die Aktion aus, wenn die Anzahl Sitzungen des Benutzers die angegebenen Kriterien erfüllt.

Geben Sie die Quelle des Besucher-Traffics an, die „true“ sein muss, damit die Aktion ausgelöst wird.

1. Geben Sie die Traffic-Quelle an.
1. (Optional) Aktivieren Sie reguläre Ausdrücke, wenn dies ein regulärer Ausdruck ist.

### Technologie

#### Browser

Wählen Sie den Browser aus, den der Besucher verwenden muss, damit die Aktion ausgelöst wird.

Wählen Sie einen oder mehrere der folgenden Browser aus:

* Chrome
* Firefox
* Internet Explorer/Edge
* Internet Explorer Mobile
* Mobile Safari
* OmniWeb
* Opera
* Opera Mini
* Opera Mobile
* Safari

#### Device Type

Wählen Sie den Gerätetyp aus, den der Besucher verwenden muss, damit die Aktion ausgelöst wird.

Wählen Sie einen oder mehrere der folgenden Gerätetypen aus:

* Android
* BlackBerry
* Desktop
* iPad
* iPhone
* iPod
* Nokia
* Windows Phone

#### Operating System

Wählen Sie das Betriebssystem aus, das der Besucher verwenden muss, damit die Aktion ausgelöst wird.

Wählen Sie eines oder mehrere der folgenden Betriebssysteme aus:

* Android
* BlackBerry
* iOS
* Linux
* MacOS
* Maemo
* Symbian OS
* Unix
* Windows

#### Screen Resolution

Wählen Sie die Bildschirmauflösung aus, die Besucher auf ihren Geräten verwenden müssen, damit die Aktion ausgelöst wird.

1. Wählen Sie aus, ob die Breite der Bildschirmauflösung des Besuchergeräts größer, gleich oder kleiner als der angegebene Wert sein muss.
1. Geben Sie die Anzahl Pixel an, die für die Breite der Bildschirmauflösung erforderlich sind.
1. Wählen Sie aus, ob die Höhe der Bildschirmauflösung des Besuchergeräts größer, gleich oder kleiner als der angegebene Wert sein muss.
1. Geben Sie die Anzahl Pixel an, die für die Höhe der Bildschirmauflösung erforderlich sind.

#### Window Size

Wählen Sie die Fenstergröße aus, die Besucher auf ihren Geräten verwenden müssen, damit die Aktion ausgelöst wird.

1. Wählen Sie aus, ob die Breite der Fenstergröße des Besuchergeräts größer, gleich oder kleiner als der angegebene Wert sein muss.
1. Geben Sie die Anzahl Pixel an, die für die Breite der Fenstergröße erforderlich sind.
1. Wählen Sie aus, ob die Höhe der Fenstergröße des Besuchergeräts größer, gleich oder kleiner als der angegebene Wert sein muss.
1. Geben Sie die Anzahl Pixel an, die für die Höhe der Fenstergröße erforderlich sind.

### URL

#### Domain

Geben Sie die Domain des Besuchers an.

#### Hash

Geben Sie ein oder mehrere Hash-Muster an, die in der URL vorhanden sein müssen.

>[!NOTE]
>
>Mehrere Hash-Muster werden durch ein OR verbunden.

1. Geben Sie das Hash-Muster an.
1. (Optional) Aktivieren Sie reguläre Ausdrücke, wenn dies ein regulärer Ausdruck ist.
1. Fügen Sie beliebige weitere Hash-Muster hinzu.

#### Path And Query String

Geben Sie einen oder mehrere Pfade an, die in der URL vorhanden sein müssen.  Dazu gehören der Pfad und die Abfragezeichenfolge.

>[!NOTE]
>
>Mehrere Pfade werden durch ein OR verbunden.

1. Geben Sie den Pfad an.
1. (Optional) Aktivieren Sie reguläre Ausdrücke, wenn dies ein regulärer Ausdruck ist.
1. Fügen Sie beliebige weitere Pfade hinzu.

#### Path Without Query String

Geben Sie einen oder mehrere Pfade an, die in der URL vorhanden sein müssen.  Dazu gehört der Pfad, jedoch nicht die Abfragezeichenfolge.

>[!NOTE]
>
>Mehrere Pfade werden durch ein OR verbunden.

1. Geben Sie den Pfad an.
1. (Optional) Aktivieren Sie reguläre Ausdrücke, wenn dies ein regulärer Ausdruck ist.
1. Fügen Sie beliebige weitere Pfade hinzu.

#### Protocol

Geben Sie das in der URL verwendete Protokoll an.

Wählen Sie eine der folgenden Optionen aus:

* HTTP
* HTTPS

#### Query String Parameter

Geben Sie den in der URL verwendeten URL-Parameter an.

1. Geben Sie einen URL-Parameternamen an.
1. Geben Sie den für den URL-Parameter verwendeten Wert an.
1. (Optional) Aktivieren Sie reguläre Ausdrücke, wenn dies ein regulärer Ausdruck ist.

#### Subdomain

Geben Sie eine oder mehrere Subdomains an, die in der URL vorhanden sein müssen.

>[!NOTE]
>
>Mehrere Subdomains werden durch ein OR verbunden.

1. Geben Sie die Subdomain an.
1. (Optional) Aktivieren Sie reguläre Ausdrücke, wenn dies ein regulärer Ausdruck ist.
1. Fügen Sie beliebige weitere Subdomains hinzu.

### Sonstige

#### Date Range

Geben Sie einen Datumsbereich an. Wählen Sie das Datum und die Uhrzeit aus, nach denen das Ereignis eintritt, sowie das Datum, vor dem es eintritt, und die Zeitzone.

#### Max Frequency

Geben Sie an, wie oft die Bedingung „true“ zurückgibt. Sie können aus den folgenden Optionen auswählen:

* Page view
* Sitzungen
* Visitor
* Seconds
* Minutes
* Days
* Weeks
* Months

Für die Bedingung der maximalen Häufigkeit von 1 pro Sitzung werden diese beiden `localStorage` Elemente verglichen. Wenn der Wert `visitorTracking.sessionCount` größer ist als die Anzahl `maxFrequency.session`, ist die Sampling-Bedingung wahr. Wenn sie gleich sind, ist die Bedingung nicht erfüllt („false“).

`sessionCount` ist ein `visitorTracking`-Element, sodass die Visitor-API aktiviert sein muss, damit die Sampling-Bedingung funktioniert.

#### Sampling

Geben Sie an, zu welchem Prozentsatz die Bedingung „true“ zurückgibt.

## Aktionstypen für die Haupterweiterung

In diesem Abschnitt werden die in der Haupterweiterung verfügbaren Aktionstypen beschrieben.

### Benutzerspezifischer Code

>[!NOTE]
>
>ES6+ JavaScript wird jetzt in benutzerdefiniertem Code unterstützt. Beachten Sie, dass einige ältere Browser ES6+ nicht unterstützen. Um die Auswirkungen der Verwendung von ES6+-Funktionen zu verstehen, testen Sie sie bitte mit allen zu unterstützenden Webbrowsern.

Geben Sie den Code an, der ausgeführt wird, nachdem das Ereignis ausgelöst wurde und die Bedingungen ausgewertet wurden.

1. Benennen Sie den Aktionscode.
1. Wählen Sie die zum Definieren der Aktion verwendete Sprache aus:
   * JavaScript
   * HTML
1. Wählen Sie aus, ob der Aktionscode global ausgeführt wird.
1. Wählen Sie **[!UICONTROL Editor öffnen]**.
1. Bearbeiten Sie den Code und klicken Sie dann auf **[!UICONTROL Speichern]**.

Wenn JavaScript als Sprache ausgewählt ist, wird automatisch eine Variable mit der Bezeichnung `event` verfügbar, die Sie in Ihrem benutzerdefinierten Code referenzieren können. Das `event`-Objekt enthält nützliche Informationen zum Ereignis, das die Regel ausgelöst hat. Die einfachste Methode zur Bestimmung der verfügbaren Ereignisdaten besteht darin, `event` mit dem console.log-Befehl in Ihrem benutzerspezifischen Code auf der Konsole auszugeben:

```javascript
console.log(event);
```

Führen Sie die Regel in einem Browser aus und überprüfen Sie das aufgezeichnete Ereignisobjekt in der Browser-Konsole. Sobald Sie die verfügbaren Informationen kennen, können Sie sie zur programmatischen Entscheidungsfindung in Ihrem benutzerdefinierten Code verwenden, einen Teil des `event`-Objekts an einen Server senden usw.

### Verarbeitung der Aktion mit benutzerspezifischem Code

Die für alle Adobe Experience Platform-Benutzer verfügbare Haupterweiterung enthält eine Aktion mit benutzerspezifischem Code zum Ausführen von JavaScript- oder HTML-Code, der vom Benutzer bereitgestellt wurde. Oftmals ist es für Benutzer hilfreich, zu verstehen, wie Aktionen mit benutzerspezifischem Code verarbeitet werden.

#### Regeln mit Seitenanfangs- oder Seitenende-Ereignissen

Der Code aus benutzerspezifischen Aktionen wird in die Tag-Hauptbibliothek eingebettet. Der Code wird mithilfe von „document.write“ in das Dokument geschrieben. Wenn eine Regel mehrere Aktionen mit benutzerspezifischem Code enthält, wird der Code in der Reihenfolge geschrieben, die in der Regel konfiguriert ist.

#### Regeln mit anderen Ereignissen als Seitenanfang oder Seitenende

Der Code aus benutzerspezifischen Aktionen wird vom Server geladen und mit [Postscribe](https://github.com/krux/postscribe) in das Dokument geschrieben. Wenn eine Regel mehrere Aktionen mit benutzerspezifischem Code enthält, wird der Code parallel vom Server geladen, jedoch in der Reihenfolge geschrieben, die in der Regel konfiguriert ist.

Während die Verwendung von „document.write“ nach dem Laden einer Seite normalerweise zu Problemen führen würde, stellt dies für von Aktionen mit benutzerspezifischem Code bereitgestelltem Code kein Problem dar. Sie können „document.write“ in Aktionen mit benutzerspezifischem Code ungeachtet dessen, wann der Code ausgeführt wird, verwenden.

#### Validierung von benutzerspezifischem Code

Der im Tag-Editor von Launch verwendete Validator dient der Identifizierung von Problemen mit Code, der von Entwicklern geschrieben wurde. Code, der einen Minimierungsprozess durchlaufen hat, z. B. der vom Code-Manager heruntergeladene AppMeasurement.js-Code, wird unter Umständen fälschlicherweise vom Validator als fehlerbehaftet markiert. Im Normalfall können Sie dies ignorieren.

#### Aktionssequenzierung

Wenn die Option &quot;Run rule components in sequence&quot;in den Eigenschafteneinstellungen aktiviert ist, können Sie festlegen, dass nachfolgende Regelkomponenten warten, während Ihre Aktion eine asynchrone Aufgabe ausführt.  Dies funktioniert bei benutzerdefiniertem JavaScript- und HTML-Code anders.

*JavaScript*

Beim Erstellen einer benutzerdefinierten JavaScript-Code-Aktion können Sie einen [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) in Ihrer Aktion zurückgeben. Die nächste Aktion in der Regel wird nur ausgeführt, wenn der zurückgegebene Promise ausgeführt wurde. Wenn der Promise abgelehnt wird, werden die nächsten Aktionen der Regel nicht ausgeführt.

>[!NOTE]
>
>Hinweis: Dies funktioniert nur, wenn JavaScript nicht für die globale Ausführung konfiguriert ist. Wenn Sie Ihre benutzerdefinierte Code-Aktion global ausführen, wird die Zusage von Tags als sofort eingelöst erachtet und es wird zum nächsten Element in der Verarbeitungswarteschlange übergegangen.

Beispiel für eine JavaScript-Aktion mit benutzerdefiniertem Code, die einen Promise zurückgibt:

```javascript
return new Promise(function(resolve, reject) {
  setTimeout(function() {
    if (new Date().getDay() === 5) {
      resolve();
    } else {
      reject();
    }
  }, 1000);
});
```

*HTML*

Beim Erstellen einer Aktion mit benutzerdefiniertem HTML-Code ist eine Funktion namens `onCustomCodeSuccess()` verfügbar, die in Ihrem benutzerspezifischen Code verwendet werden kann. Sie können diese Funktion aufrufen, um anzugeben, dass Ihr benutzerdefinierter Code abgeschlossen ist und Tags mit den nachfolgenden Aktionen fortfahren kann. Wenn Ihr benutzerdefinierter Code jedoch fehlschlägt, kann `onCustomCodeFailure()` aufrufen werden. Dadurch wird Tags informiert, dass die nachfolgenden Aktionen dieser Regel nicht ausgeführt werden sollen.

Beispiel für eine HTML-Aktion mit benutzerdefiniertem Code, bei der die neuen Callbacks verwendet werden:

```html
<script>
setTimeout(function() {
  if (new Date().getDay() === 5) {
    onCustomCodeSuccess();
  } else {
    onCustomCodeFailure();
  }
}, 1000);
</script>
```

### Trigger-Direktaufruf {#direct-call-action}

Diese Aktion löst alle Regeln aus, die ein bestimmtes [Direktaufrufereignis](#direct-call-event) verwenden. Beim Konfigurieren der Aktion müssen Sie die Kennungszeichenfolge für das Direktaufruferereignis angeben, das Sie auslösen möchten. Optional können Sie auch Daten über ein `detail`-Objekt, das einen benutzerdefinierten Satz von Schlüssel-Wert-Paaren enthalten kann, an ein Direktaufrufereignis weiterleiten.

![Screenshot einer Trigger-Direktaufruf-Aktion in der Datenerfassungs-Benutzeroberfläche](../../../images/extensions/core/direct-call-action.png)

Die Aktion wird direkt mit der [`track`-Methode](../../../ui/client-side/satellite-object.md?lang=en#track) im `satellite`-Objekt verknüpft, auf das Client-seitiger Code zugreifen kann.

## Datenelementtypen der Haupterweiterung

Datenelementtypen werden durch die Erweiterung bestimmt. Die erstellbaren Typen sind nicht beschränkt.

In den folgenden Abschnitten werden die in der Haupterweiterung verfügbaren Datenelementtypen beschrieben. In anderen Erweiterungen werden andere Datenelementtypen verwendet.

### Cookie

Jedes verfügbare Domain-Cookie kann im Cookie-Namensfeld referenziert werden.

#### Beispiel:

`cookieName`

### Konstante

Ein konstanter Zeichenfolgenwert, der in Aktionen oder Bedingungen referenziert werden kann.

#### Beispiel:

`string`

### Benutzerspezifischer Code

>[!NOTE]
>
>ES6+ JavaScript wird jetzt in benutzerdefiniertem Code unterstützt. Beachten Sie, dass einige ältere Browser ES6+ nicht unterstützen. Um die Auswirkungen der Verwendung von ES6+-Funktionen zu verstehen, testen Sie sie bitte mit allen zu unterstützenden Webbrowsern.

Benutzerdefiniertes JavaScript kann auf der Benutzeroberfläche eingegeben werden, indem Sie auf „Editor öffnen“ klicken und den Code in das Editor-Fenster einfügen.

Eine Rückkehranweisung ist im Editor erforderlich, damit festgelegt ist, welcher Wert als Datenelementwert verwendet wird. Wenn keine Rückkehranweisung angegeben ist oder der Wert `null` oder `undefined` zurückgegeben wird, wird der Standardwert des Datenelements als Datenelementwert verwendet.

**Beispiel:**

```javascript
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Wenn ein Datenelement des benutzerdefinierten Codes während der Ausführung einer Regel abgerufen wird, wird automatisch eine Variable mit der Bezeichnung `event` verfügbar, die Sie in Ihrem benutzerdefinierten Code referenzieren können. Das `event`-Objekt enthält nützliche Informationen zum Ereignis, das die Regel ausgelöst hat. Die einfachste Methode zur Bestimmung der verfügbaren Ereignisdaten besteht darin, `event` mit dem console.log-Befehl in Ihrem benutzerspezifischen Code auf der Konsole auszugeben:

```javascript
console.log(event);
return true;
```

Führen Sie die Regel in einem Browser aus und überprüfen Sie das aufgezeichnete Ereignisobjekt in der Browser-Konsole. Sobald Sie die Informationen kennen, die bei den unterschiedlichen Regeln, die Ihr Datenelement verwenden können, verfügbar sind, können Sie sie zur programmatischen Entscheidungsfindung in Ihrem benutzerdefinierten Code verwenden oder einen Teil des `event`-Objekts als Wert des Datenelements zurückgeben.


### DOM-Attribut

Es kann ein beliebiger Elementwert abgerufen werden, z. B. „div“ oder H1-Tag.

#### Beispiel:

CSS-Auswahlkette:

`id#dc logo img`

Wert abrufen von:

`src`

### JavaScript-Variable

Verfügbare JavaScript-Objekte oder -Variablen können mit dem Pfadfeld referenziert werden.

Mit Tag-Datenelementen können Sie Ihre Markup-JavaScript-Variablen oder Objekteigenschaften erfassen. Diese Werte können dann in Ihren Erweiterungen oder benutzerdefinierten Regeln verwendet werden, indem auf die Tag-Datenelemente verwiesen wird. Wenn sich die Quelle der Daten ändert, ist es nur erforderlich, den Verweis auf die Quelle zu aktualisieren.

Im folgenden Beispiel enthält das Markup eine JavaScript-Variable namens `Page_Name`.

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Wenn Sie das Datenelement  erstellen, geben Sie einfach den Pfad zu dieser Variablen an.

Wenn Sie ein Datenerfassungsobjekt als Teil Ihrer Datenschicht verwenden, verwenden Sie Punktnotation im Pfad, um auf das Objekt und die Eigenschaft zu verweisen, die Sie im Datenelement erfassen möchten, z. B. `_myData.pageName`oder `digitalData.pageName`usw.

#### Beispiel:

`window.document.title`

### Lokaler Speicher

Geben Sie den Namen Ihres lokalen Speicherelements im Feld „Name des lokalen Speicherelements“ an.

Der lokale Speicher bietet Browsern die Möglichkeit, Informationen seitenweise zu speichern ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). Die Funktion des lokalen Speichers ähnelt der von Cookies sehr stark. Er ist jedoch deutlich größer und bietet mehr Flexibilität.

Geben Sie in dem bereitgestellten Feld den Wert an, den Sie für ein lokales Speicherelement erstellt haben, z. B. `lastProductViewed.`

### Zusammengeführte Objekte

Wählen Sie mehrere Datenelemente aus, die jeweils ein Objekt bereitstellen sollen. Diese Objekte werden rekursiv zusammengeführt, um ein neues Objekt zu erzeugen. Die Quellobjekte werden nicht verändert. Wenn eine Eigenschaft an derselben Stelle in mehreren Quellobjekten gefunden wird, wird der Wert des letzten Objekts verwendet. Wenn eine Quelleigenschaft den Wert `undefined` hat, wird ein Wert aus einem früheren Quellobjekt nicht überschrieben. Wenn Arrays an derselben Stelle in mehreren Quellobjekten gefunden werden, werden die Arrays verkettet.

Nehmen wir an, ein ausgewähltes Datenelement stellt das folgende Objekt bereit:

```
{
  "sport": {
    "name": "tennis"
  },
  "dessert": "ice cream",
  "fruits": [
    "apple",
    "banana"
  ]
}
```

Angenommen, ein weiteres ausgewähltes Datenelement stellt das folgende Objekt bereit:

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": undefined,
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "cherry",
    "duku"
  ]
}
```

Das Ergebnis des Datenelements „Zusammengeführte Objekte“ wäre das folgende Objekt:

```
{
  "sport": {
    "name": "volleyball"
  },
  "dessert": "ice cream",
  "pet": "dog",
  "instrument": undefined,
  "fruits": [
    "apple",
    "banana",
    "cherry",
    "duku"
  ]
}
```

### Seiteninfo

Verwenden Sie diese Datenpunkte zum Erfassen von Seiteninfos für Ihre Regellogik oder zum Senden von Informationen an Analytics oder externe Tracking-Systeme.

Sie können eines der folgenden Seitenattribute auswählen, um es in Ihrem Datenelement zu verwenden:

* URL
* Hostname
* Pathname
* Protokoll
* Referrer
* Title

### Query String Parameter

Geben Sie im Feld „URL-Parameter“ einen einzelnen URL-Parameter an.

Nur der Abschnitt „Name“ ist erforderlich und spezielle Bezeichner wie „?“ oder „=“ sollten weggelassen werden.

#### Beispiel:

`contentType`

### Zufällige Nummer

Verwenden Sie dieses Datenelement zum Generieren einer zufälligen Nummer. Sie wird häufig zum Sampling von Daten oder zum Erstellen von IDs wie einer Treffer-ID verwendet. Die zufällige Nummer kann auch zum Verschleiern oder für Salt-Vorgänge für vertrauliche Daten verwendet. Mögliche Beispiele sind:

* Generieren einer Treffer-ID
* Verketten der Nummer für ein Benutzer-Token oder einen Zeitstempel zur Gewährleistung der Eindeutigkeit
* Ausführen eines unidirektionalen Hash-Vorgangs für PII-Daten
* Zufälliges Entscheiden, wann auf der Seite eine Anfrage zu einer Umfrage angezeigt wird

Geben Sie den Minimal- und Maximalwert für Ihre zufällige Nummer an.

**Standardeinstellungen:**

Minimum: 0

Maximum: 1000000000

### Sitzungsspeicher

Geben Sie den Namen Ihres Sitzungsspeicherelements im Feld „Name des Sitzungsspeicherelements“ an.

Der Sitzungsspeicher ähnelt dem lokalen Speicher. Der Unterschied besteht darin, dass die Daten nach Ende der Sitzung verworfen werden. Beim lokalen Speicher oder einem Cookie bleiben die Daten hingegen möglicherweise gespeichert.

### Besucherverhalten

Dieses Datenelement verwendet ähnlich wie die Seiteninformationen allgemeine Verhaltenstypen zur Erweiterung der Logik in Regeln und anderen Platform-Lösungen.

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
* Füllen der Analytics-Metrik, wenn dies die Landingpage für den Besuch ist
* Anzeigen eines neuen Angebots für den Besucher nach X Sitzungen
* Anzeigen einer Newsletter-Registrierung, wenn es sich um einen erstmaligen Besucher handelt

### Bedingter Wert

Ein Wrapper für die Bedingung [Wertvergleich](#value-comparison-value-comparison). Auf der Grundlage des Vergleichsergebnisses wird einer der beiden verfügbaren Werte in das Formular eingegeben. Kann dabei mit „If... Then... Else...“-Szenarien behandeln, ohne dass zusätzliche Regeln erforderlich sind.

### Laufzeitumgebung

Hier können Sie eine der folgenden Variablen auswählen:

* Umgebungsstufe - Gibt `_satellite.environment.stage` zurück, um zwischen Entwicklungs-/Staging-/Produktionsumgebung zu unterscheiden.
* Bibliothekerstellungsdatum - Gibt `turbine.buildInfo.buildDate` zurück, das denselben Wert wie `_satellite.buildInfo.buildDate` enthält.
* Eigenschaftsname - Gibt `_satellite.property.name` zurück, um den Namen der Launch-Eigenschaft zu erhalten.
* Eigenschafts-ID - Gibt `_satellite.property.id` zurück, um die ID der Launch-Eigenschaft zu erhalten.
* Regelname - Gibt `event.$rule.name` zurück, das den Namen der ausgeführten Regel enthält.
* Regel-ID - Gibt `event.$rule.id` zurück, das die ID der ausgeführten Regel enthält.
* Ereignistyp - Gibt `event.$type` mit dem Typ des Ereignisses zurück, das die Regel ausgelöst hat.
* Ereignisdetail-Payload - Gibt `event.detail` zurück, das die Payload eines benutzerdefinierten Ereignisses oder einer Direktaufruf-Regel enthält.
* Direktaufruf-Identifikator - Gibt `event.identifier` mit der Kennung einer Direktaufruf-Regel zurück.

### Geräte-Attribute

Gibt eines der folgenden Attribute für das Besuchergerät zurück:

* Größe des Browser-Fensters
* Bildschirmgröße

### JavaScript-Tools

Es ist ein Wrapper für gängige JavaScript-Operationen. Erhält ein Datenelement als Eingabe. Gibt das Ergebnis einer der folgenden Umwandlungen des Datenelementwerts zurück:

* Grundlegende String-Manipulation (replace, substring, regex match, first and last index, split, slice)
* Grundlegende Array-Operationen (slice, join, pop, shift)
* Universelle Grundoperationen (slice, lenth)