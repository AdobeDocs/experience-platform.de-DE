---
title: Übersicht über die Hauptereignisweiterleitungserweiterung
description: Machen Sie sich mit der Hauptereignisweiterleitungserweiterung in Adobe Experience Platform vertraut.
feature: Event Forwarding
exl-id: b5ee4ccf-6fa5-4472-be04-782930f07e20
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 100%

---

# Übersicht über die Hauptereignisweiterleitungserweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

Die Hauptereignisweiterleitungserweiterung stellt die Standardereignisse, Bedingungen und Datentypen für die Ereignisweiterleitung in Adobe Experience Platform bereit.

Verwenden Sie diese Referenz, um Informationen zu den verfügbaren Optionen beim Erstellen einer Regel mithilfe dieser Erweiterung zu erhalten.

## Bedingungstypen für die Haupterweiterung

In diesem Abschnitt werden die in der Haupterweiterung verfügbaren Bedingungstypen beschrieben. Diese Bedingungstypen können entweder mit dem Logiktyp „normal“ oder „Ausnahme“ verwendet werden.

### Benutzerspezifischer Code

Geben Sie einen benutzerspezifischen Code an, der als Bedingung des Ereignisses vorhanden sein muss. Verwenden Sie für die Eingabe des benutzerspezifischen Codes den integrierten Code-Editor. Die Ereignisweiterleitung in Adobe Experience Platform unterstützt ES6.

1. Wählen Sie **[!UICONTROL Editor öffnen]**.
1. Geben Sie den benutzerspezifischen Code ein.
1. Wählen Sie **[!UICONTROL Speichern]** aus.

Der Zugriff auf den Wert eines Datenelements in benutzerdefiniertem Code erfolgt über die Methode `getDataElementValue`. Um beispielsweise den Wert eines Datenelements mit dem Namen `productName` abzurufen, geben Sie Folgendes ein: 

```javascript
getDataElementValue('productName') 
```

#### ruleStash-Objekt

In Ihrem benutzerspezifischen Code können Sie auch das Objekt `ruleStash` verwenden.

```javascript
utils.logger.log(context.arc.ruleStash);
```

`ruleStash` ist ein Objekt, das alle von Aktionsmodulen zurückgegebenen Ergebnisse erfasst.

Jede Erweiterung hat ihren eigenen Namensraum. Wenn Ihre Erweiterung beispielsweise den Namen `send-beacon` hat, werden alle Ergebnisse der `send-beacon`-Aktionen im Namensraum `ruleStash['send-beacon']` gespeichert.

```javascript
utils.logger.log(context.arc.ruleStash['adobe-cloud-connector']);
```

Der Namensraum ist für jede Erweiterung eindeutig und hat am Anfang den Wert `undefined`.

Der Namensraum wird mit dem zurückgegebenen Ergebnis jeder Aktion überschrieben. Das dem Namensraum zugrunde liegende Prinzip ist ganz einfach. Angenommen, Sie haben eine Erweiterung `transform`, die die Aktionen `generate-fullname` und `generate-fulladdress` enthält, dann werden einfach diese beiden Aktionen einer Regel hinzugefügt.

Wenn das Ergebnis der Aktion `generate-fullname` `Firstname Lastname` lautet, wird der ruleStash nach Abschluss der Aktion wie folgt angezeigt:

```js
{
  transform: 'Firstname Lastname`
}
```

Wenn das Ergebnis der Aktion `generate-address` `3900 Adobe Way` lautet, wird der ruleStash nach Abschluss der Aktion wie folgt angezeigt:

```js
{
  transform: '3900 Adobe Way`
}
```

Beachten Sie, dass `Firstname Lastname` nicht mehr im ruleStash vorhanden ist. Dies liegt daran, dass die Aktion `generate-address` diesen Eintrag mit der Adresse überschrieben hat.

Wenn Sie Ergebnisse aus beiden Aktionen im Namensraum `transform` in `ruleStash` speichern möchten, können Sie für Ihr Aktionsmodul eine Eingabe wie die folgende verwenden:

```javascript
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;
  if (!transformRuleStash) {
    transformRuleStash = {};
  }
  transformRuleStash.fullName = 'Firstname Lastname';
  return transformRuleStash;
}
```

Wenn diese Aktion zum ersten Mal ausgeführt wird, hat `ruleStash` den Wert `undefined` und wird mit einem leeren Objekt initialisiert. Wenn die Aktion das nächste Mal ausgeführt wird, wird `ruleStash` von der Aktion zurückgegeben, bei der sie zuvor aufgerufen wurde. Durch die Verwendung eines Objekts als `ruleStash` können Sie neue Daten hinzufügen, ohne zuvor durch andere Aktionen der Erweiterung festgelegte Daten zu verlieren.

Beachten Sie, dass Sie in diesem Fall immer den vollständigen ruleStash der Erweiterung zurückgeben müssen. Das Zurückgeben eines einfachen Werts (z. B. 5) würde für den ruleStash Folgendes liefern.

```js
{
  transform: 5
}
```

### Wertvergleich {#value-comparison}

Vergleicht zwei Werte, um zu ermitteln, ob diese Bedingung „true“ zurückgibt.

Wenn Sie eine Regel mit mehreren Bedingungen haben, ist es möglich, dass diese Bedingung möglicherweise „true“ zurückgibt, die Regel jedoch trotzdem nicht ausgelöst wird, weil die andere Bedingung als „false“ oder eine der Ausnahmen als „true“ ausgewertet wird.

1. Stellen Sie einen Wert bereit.
1. Wählen Sie den Operator aus. Weitere Einzelheiten dazu finden Sie unten in der Liste der Wertvergleichsoperatoren.
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



## Aktionstypen für die Haupterweiterung

In diesem Abschnitt werden die in der Haupterweiterung verfügbaren Aktionstypen beschrieben.

### Benutzerspezifischer Code

Geben Sie den Code an, der ausgeführt wird, nachdem das Ereignis ausgelöst wurde und die Bedingungen ausgewertet wurden. Die Ereignisweiterleitung in Adobe Experience Platform unterstützt ES6.

1. Benennen Sie den Aktionscode.
1. Wählen Sie **[!UICONTROL Editor öffnen]**.
1. Bearbeiten Sie den Code und klicken Sie dann auf **[!UICONTROL Speichern]**.

Der Zugriff auf den Wert eines Datenelements in benutzerdefiniertem Code erfolgt über die Methode `getDataElementValue`. Um beispielsweise den Wert eines Datenelements mit dem Namen `productName` abzurufen, geben Sie Folgendes ein: 

```javascript
getDataElementValue('productName') 
```

Die Ereignisweiterleitungsaktionen werden sequenziell ausgeführt. Zudem kann der von einer Aktion in benutzerspezifischem Code zurückgegebene Wert in einer auf diese folgende Aktion verwendet werden. Der zurückgegebene Wert kann aus dem Code innerhalb dieser Aktion oder aus dem über einen Aufruf einer externen Quelle erhaltenen Antworttext stammen. Um auf Daten aus einer zuvor ausgeführten Aktion innerhalb einer einzelnen Regel zu verweisen, bei der die Core-Erweiterung verwendet wird, erstellen Sie ein Datenelement vom Typ `Path` und verwenden Sie den folgenden Pfad, um auf den Wert einer Variablen mit dem Namen `productCategory` zu verweisen, die im benutzerdefinierten Code innerhalb der Core-Erweiterung definiert ist:

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## Datenelementtypen der Haupterweiterung

Datenelementtypen werden durch die Erweiterung bestimmt. Die erstellbaren Typen sind nicht beschränkt.

In den folgenden Abschnitten werden die in der Haupterweiterung verfügbaren Datenelementtypen beschrieben. In anderen Erweiterungen werden andere Datenelementtypen verwendet.

### Benutzerspezifischer Code

Benutzerdefiniertes JavaScript kann auf der Benutzeroberfläche eingegeben werden, indem Sie auf **[!UICONTROL Editor öffnen]** klicken und den Code in das Editor-Fenster einfügen.

Im Editor-Fenster muss über eine return-Anweisung der für das Datenelement zu verwendende Wert angegeben werden. Wird keine return-Anweisung angegeben oder der Wert `null` oder `undefined` zurückgegeben, lautet der Standardwert des Datenelements `null` oder `undefined`.

Der Zugriff auf den Wert eines Datenelements in benutzerdefiniertem Code erfolgt über die Methode `getDataElementValue`. Um beispielsweise den Wert eines Datenelements mit dem Namen `productName` abzurufen, geben Sie Folgendes ein: 

```javascript
getDataElementValue('productName') 
```

**Beispiel:**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### Path

Ein Pfad zu einem Schlüssel-Wert-Paar auf einem Ereignis, das an Adobe Experience Platform Edge Network gesendet wird, kann mithilfe des Pfad-Datenelementtyps referenziert werden.

Um auf das gesamte Objekt eines Ereignisses zu verweisen, geben Sie `arc` als Pfad ein. Das Akronym `arc` steht für Adobe Resource Context und ist der Pfad der obersten Ebene für ein Ereignis, das an Adobe Experience Platform Edge Network gesendet wird.

Beispielsweise liegt dem `interact`-Aufruf des Clients an Edge Network die folgende in der Browserkonsole dargestellte Anfrage zugrunde:

```javascript
"events": [ 
        { 
             "xdm": { 
                    "page": { 
                            "btnHover": false, 
                            "pageName": "We Travel Home Page", 
                            "siteSection": "Landing Page" 
                     }] 
```

Geben Sie für einen Pfad, der auf `pageName` verweist, Folgendes in das Pfadfeld ein:

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>Der `interact`-Aufruf des Clients enthält `events`, aber für die Ereignisweiterleitung benötigen Sie `event`. Der Grund dafür ist, dass die Ereignisweiterleitung jedes Ereignis einzeln prüft, während auf dem Client die Prüfung für einen Batch mehrerer Ereignisse erfolgt (wie dargestellt).
