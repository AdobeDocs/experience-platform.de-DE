---
title: Google-Datenschichterweiterung
description: Erfahren Sie mehr über die Google Client-Datenschicht-Tag-Erweiterung in Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 9c608f69f6ba219f9cb4e938a77bd4838158d42c
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 15%

---

# Google Data Layer-Erweiterung

Mit der Google Data Layer-Erweiterung können Sie eine Google-Datenschicht in Ihrer Tag-Implementierung verwenden. Die Erweiterung kann unabhängig oder gleichzeitig mit Google-Lösungen und der Open Source von Google verwendet werden [Data Layer Helper Library](https://github.com/google/data-layer-helper).

Die Hilfsbibliothek bietet ähnliche ereignisgesteuerte Funktionen wie der Adobe Client Data Dayer (ACDL). Die Datenelemente, Regeln und Aktionen der Google-Datenschicht-Erweiterung bieten ähnliche Funktionen wie die im [ACDL-Erweiterung](../client-data-layer/overview.md).

## Laufzeit

Version 1.2.x ist eine Beta-Version, die in der Produktion verwendet wird.

## Installation

Um die Erweiterung zu installieren, navigieren Sie zum Erweiterungskatalog in der Datenerfassungs-Benutzeroberfläche und wählen Sie **[!UICONTROL Google-Datenschicht]**.

Nach der Installation erstellt oder greift die Erweiterung auf eine Datenschicht bei jedem Laden der Adobe Experience Platform Tags-Bibliothek zu.

## Erweiterungsansicht

Die Erweiterungskonfiguration kann verwendet werden, um den Namen der Datenschicht zu definieren, die die Erweiterung nutzt. Wenn beim Laden von Adobe Experience Platform-Tags keine Datenschicht mit dem konfigurierten Namen vorhanden ist, erstellt die Erweiterung eine.

Der Standardwert für den Datenschichtnamen ist der Google-Standardname `dataLayer`.

>[!NOTE]
>
>Es spielt keine Rolle, ob Google- oder Adobe-Code zuerst geladen wird und die Datenschicht erstellt. Beide Systeme verhalten sich gleich - erstellen Sie die Datenschicht, falls sie nicht vorhanden ist, oder verwenden Sie die vorhandene Datenschicht.

## Ereignisse

>[!NOTE]
>
>Das Wort _event_ wird überlastet, wenn in Adobe Experience Platform-Tags eine ereignisbasierte Datenschicht verwendet wird. _Veranstaltungen_ kann sein:
> - Adobe Experience Platform Tags-Ereignisse (Bibliothek geladen usw.).
> - JavaScript-Ereignisse.
> - Daten, die mit der _event_ Keyword.


Die Erweiterung bietet Ihnen die Möglichkeit, auf Änderungen auf der Datenschicht zu warten.

>[!NOTE]
>
>Es ist wichtig, die Verwendung der _event_ Keyword, wenn Daten auf eine Google-Datenschicht übertragen werden, ähnlich wie bei der Adobe Client-Datenschicht. Die _event_ -Keyword ändert das Verhalten der Google-Datenschicht und daher diese Erweiterung.\
> Lesen Sie die Dokumentation zu Google oder recherchieren Sie, wenn Sie sich diesbezüglich nicht sicher sind.

### Suchen Sie nach allen Push-Benachrichtigungen auf der Datenschicht.

Wenn Sie diese Option auswählen, überwacht Ihr Ereignis-Listener alle Änderungen an der Datenschicht.

### Nach Push-Benachrichtigungen zum Ausschließen von Ereignissen suchen

Wenn Sie diese Option auswählen, überwacht Ihr Ereignis-Listener alle Datenübertragungen an die Datenschicht, wobei Ereignisse ausgeschlossen sind.

Das folgende Beispiel für Push-Ereignisse wird vom Listener verfolgt:

```js
dataLayer.push({"data":"something"})
```

Das folgende Beispiel für Push-Ereignisse wird vom Listener nicht verfolgt:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Alle Ereignisse überwachen

Wenn Sie diese Option auswählen, überwacht Ihr Ereignis-Listener alle Ereignisse, die an die Datenschicht gepusht werden.

Das folgende Beispiel für Push-Ereignisse wird vom Listener verfolgt:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

Das folgende Beispiel für ein Push-Ereignis wird vom Listener nicht verfolgt:

```js
dataLayer.push({"data":"something"})
```

### Suchen nach bestimmten Ereignissen

Wenn Sie ein Ereignis angeben, verfolgt der Ereignis-Listener alle Ereignisse, die mit einer bestimmten Zeichenfolge übereinstimmen.

Wenn Sie beispielsweise `myEvent` bei Verwendung dieser Konfiguration festlegen, verfolgt der Listener nur das folgende Push-Ereignis:

```js
dataLayer.push({"event":"myEvent"})
```

Es kann ein (ECMAScript-/JavaScript-) Regex verwendet werden, um Ereignisnamen zuzuordnen.

Wenn beispielsweise &quot;myEvent\d&quot;festgelegt wird, wird `myEvent` mit einer Ziffer (\d):

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Aktionen

### Pushen zur Datenschicht {#push-to-data-layer}

Die -Erweiterung bietet zwei Aktionen, um JSON an die Datenschicht zu pushen. ein freies Textfeld zur manuellen Erstellung des zu übertragenden JSON-Codes und ab Version 1.2.0 ein Multifield-Dialogfeld mit Schlüsselwerten.

#### Free text JSON

Die Aktion &quot;Freitext&quot;ermöglicht die direkte Verwendung von Datenelementen in der JSON-Datei. Innerhalb des JSON-Editors sollten Datenelemente mit der Prozentnotation referenziert werden. Beispiel: `%dataElementName%`.

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

#### Mehrfeld für Schlüssel-Wert

Das neuere multifield-Dialogfeld mit dem Schlüssel-Wert-Wert ist eine benutzerfreundlichere Benutzeroberfläche, mit der ein Push-Vorgang konfiguriert werden kann, ohne JSON manuell zu schreiben.

### Google DL auf berechneten Status zurücksetzen

Die -Erweiterung bietet Ihnen eine Aktion zum Zurücksetzen der Datenschicht. Wenn sie in einer Regel verwendet wird, die eine Google-Datenschichtänderung verarbeitet, wird die Datenschicht zum Zeitpunkt der Regelauslösung auf den berechneten Status der Datenschicht zurückgesetzt. Wenn die Aktion in einer Regel verwendet wird, die keine Änderung der Google-Datenschicht verarbeitet, wird die Datenschicht durch die Aktion geleert.

## Datenelemente

Das bereitgestellte Datenelement kann während der Ausführung einer Regel verwendet werden, die durch eine Google-Datenschichtänderung (Push-Ereignis) ausgelöst wird, oder in einer nicht verwandten Regel wie &quot;Bibliothek geladen&quot;. Im ersten Fall gibt das Datenelement einen Wert zurück, der aus dem berechneten Status zum Zeitpunkt der Datenschichtänderung entnommen wurde. Im letzteren Fall wird der berechnete Status zum Zeitpunkt der Regelausführung verwendet.

Mit einem Umschalter können Sie auswählen, ob das Datenelement Werte aus dem gesamten berechneten Status oder nur aus Ereignisinformationen zurückgeben soll (wenn es in einer durch eine Datenschichtänderung ausgelösten Regel verwendet wird).

Das Datenelement kann daher Folgendes zurückgeben:

- Leeres Feld: berechneter Status der Datenschicht.
- Feld mit Schlüssel (z. B. page.previous_url im obigen Beispiel): -Wert des Schlüssels im Ereignisobjekt oder im berechneten Status.

## Zusätzliche Informationen

Die Datenelement- und Ereignisdialogfelder der Erweiterung enthalten detaillierte Nutzungsinformationen und Beispiele.

Weitere allgemeine Informationen finden Sie unter [Projekt README](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md)
