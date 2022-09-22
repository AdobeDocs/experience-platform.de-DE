---
title: Google-Datenschichterweiterung
description: Erfahren Sie mehr über die Google Client-Datenschicht-Tag-Erweiterung in Adobe Experience Platform.
exl-id: 7990351d-8669-432b-94a9-4f9db1c2b3fe
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 8%

---

# Google Data Layer-Erweiterung (Beta)

>[!IMPORTANT]
>
>Diese Erweiterung befindet sich derzeit in der Beta-Phase und wurde noch nicht vollständig in der Produktion getestet.

Mit der Google Data Layer-Erweiterung können Sie eine Google-Datenschicht in Ihrer Tag-Implementierung verwenden. Die Erweiterung kann unabhängig oder gleichzeitig mit Google-Lösungen und der Open Source von Google verwendet werden [Data Layer Helper Library](https://github.com/google/data-layer-helper).

Die Hilfsbibliothek bietet ähnliche ereignisgesteuerte Funktionen wie der Adobe Client Data Dayer (ACDL). Die Datenelemente, Regeln und Aktionen der Google-Datenschicht-Erweiterung bieten ähnliche Funktionen wie die im [ACDL-Erweiterung](../client-data-layer/overview.md).

## Laufzeit

Version 1.0.x der Erweiterung ist eine Beta-Version. Diese Erweiterung wurde in der Produktion nicht vollständig getestet.

## Installation

Um die Erweiterung zu installieren, navigieren Sie zum Erweiterungskatalog in der Datenerfassungs-Benutzeroberfläche und wählen Sie **Google-Datenschicht**.

Nach der Installation erstellt oder greift die Erweiterung jedes Mal, wenn die Tag-Bibliothek auf Ihre Website geladen wird, auf eine Datenschicht zu.

## Erweiterungsansicht

Beim Konfigurieren der Erweiterung (entweder während der Installation der Erweiterung oder durch Auswahl von **[!UICONTROL Konfigurieren]** aus dem Erweiterungskatalog) müssen Sie den Namen der Datenschicht definieren, die die Erweiterung nutzt. Wenn beim Laden der Bibliothek keine Datenschicht mit dem konfigurierten Namen vorhanden ist, erstellt die Erweiterung stattdessen eine.

>[!NOTE]
>
>Es spielt keine Rolle, ob Google- oder Adobe-Code zuerst geladen wird und die Datenschicht erstellt. Beide Systeme erstellen die Datenschicht, falls nicht vorhanden, oder verwenden die vorhandene Datenschicht.

Standardmäßig verwendet die Datenschicht den Google-Standardnamen `dataLayer`.

## Ereignisse

Mit der Erweiterung können Sie auf Änderungen (Ereignisse) innerhalb der Datenschicht warten. Ein Ereignis kann eines der folgenden sein:

* Tag-Ereignisse (z. B. eine Bibliothek, die geladen wird)
* JavaScript-Ereignisse
* Daten, die mit der `event` Keyword.

Es ist wichtig, die Verwendung der [`event` Keyword](https://developers.google.com/tag-platform/devguides/datalayer#use_a_data_layer_with_event_handlers) wenn Daten auf eine Google-Datenschicht übertragen werden, ähnlich wie auf die Adobe Client-Datenschicht. Die `event` -Keyword ändert das Verhalten der Google-Datenschicht, sodass das Verhalten der Erweiterung entsprechend aktualisiert wird.

In den folgenden Abschnitten werden die verschiedenen Ereignistypen beschrieben, auf die die Erweiterung warten kann.

### Suchen Sie nach allen Push-Benachrichtigungen auf der Datenschicht.

Wenn Sie diese Option auswählen, überwacht die Erweiterung alle Änderungen an der Datenschicht.

### Nach Push-Benachrichtigungen zum Ausschließen von Ereignissen suchen

Wenn Sie diese Option auswählen, überwacht die Erweiterung alle an die Datenschicht gepushten Elemente, wobei Ereignisse ausgeschlossen sind.

Das folgende Beispiel-Push-Ereignis wird vom Listener verfolgt:

```js
dataLayer.push({"data":"something"})
```

Das folgende Beispiel für Push-Ereignisse wird vom Listener nicht verfolgt:

```js
dataLayer.push({"event":"myevent"})
dataLayer.push({"event":"myevent","data":"something"})
```

### Alle Ereignisse überwachen

Wenn Sie diese Option auswählen, überwacht die Erweiterung alle Ereignisse, die an die Datenschicht gesendet werden.

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

Wenn Sie auf ein bestimmtes Ereignis warten möchten, wählen Sie diese Option aus, damit der Ereignis-Listener alle Ereignisse verfolgt, die mit einer bestimmten Zeichenfolge übereinstimmen.

Wenn Sie beispielsweise `myEvent` bei Verwendung dieser Konfiguration festlegen, verfolgt der Listener nur das folgende Push-Ereignis:

```js
dataLayer.push({"event":"myEvent"})
```

Sie können auch eine Regex-Zeichenfolge verwenden, um Ereignisnamen zuzuordnen. Beispiel: `myEvent\d` verfolgt Ereignisse, die mit beginnen `myEvent` gefolgt von einer Ziffer:

```js
dataLayer.push({"event":"myEvent1"})
dataLayer.push({"event":"myEvent2"})
```

## Aktionen

In den folgenden Abschnitten werden die verschiedenen Aktionen beschrieben, die die Erweiterung ausführen kann, wenn sie in einer [Regel](../../../ui/managing-resources/rules.md).

### Pushen zur Datenschicht {#push-to-data-layer}

Durch diese Aktion wird der JSON-Inhalt auf die Datenschicht selbst übertragen, sodass Datenelemente direkt in JSON-Payloads verwendet werden können. Im bereitgestellten JSON-Editor können Sie Datenelemente mit der Prozentnotation referenzieren (z. B. `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

### Google DL auf berechneten Status zurücksetzen

>[!NOTE]
>
>Diese Aktion ist ab Version 1.0.5 verfügbar.

Durch diese Aktion wird die Datenschicht zurückgesetzt. Wenn sie in einer Regel verwendet wird, die eine Google-Datenschichtänderung verarbeitet, wird die Datenschicht zum Zeitpunkt der Regelauslösung auf den berechneten Status der Datenschicht zurückgesetzt. Wenn die Aktion in einer Regel verwendet wird, die keine Änderung der Google-Datenschicht verarbeitet, wird die Datenschicht durch die Aktion geleert.

## Datenelemente

Die Erweiterung bietet ein eindeutiges Datenelement, das mithilfe eines Schlüssels auf die Datenschicht zugreift (z. B. `page.url` im [Ausschnitt oben](#push-to-data-layer)).

Das Datenelement kann Folgendes bereitstellen:

* Ein bestimmter Wert aus der Datenschicht (z. B. `page.url`)
* Das gesamte Datenschichtarray (leeres Schlüsselfeld)
* Werte aus einem Datenschichtereignis mithilfe des Schlüssels (wenn die Variable `event` Keyword wurde verwendet)
* Das gesamte Ereignisobjekt (leeres Schlüsselfeld)

Die Erweiterung gibt Ereignisinformationen immer Priorität. Wenn eine Datenschicht `event` verarbeitet wird, werden Werte immer aus diesem Ereignis gelesen. Wenn eine `event` nicht vorhanden ist, werden Werte stattdessen aus der direkten Datenschicht gelesen.

## Zusätzliche Informationen

Weitere Informationen finden Sie im Abschnitt [Projekt README](https://github.com/adobe/reactor-extension-googledatalayer/blob/main/README.md) und in den Datenelement- und Ereignisdialogfeldern der Erweiterung.
