---
title: Adobe Client-Datenschicht-Erweiterung
description: Machen Sie sich mit der Tag-Erweiterung „Adobe Client Data Layer“ in Adobe Experience Platform vertraut.
exl-id: c4d1b4d3-4b51-4701-be2e-31b08e109bf6
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 95%

---

# Adobe Client-Datenschicht-Erweiterung

Diese Dokumentation enthält Beispiele und Best Practices für die Verwendung der Adobe Client-Datenschicht-Erweiterung.

<!-- (Missing document?)
If you would like to have more details on development consideration, [please reach this page](./dev.md). -->

## Installation

Um die Erweiterung zu installieren, navigieren Sie zum Erweiterungskatalog in der Experience Platform-Benutzeroberfläche oder der Datenerfassungs-Benutzeroberfläche und wählen Sie Adobe Client Data Layer aus.

![ACDL-Erweiterungsansicht im Katalog](./images/catalog.png)

<!-- (GitHub link?)
There is also the possibility to fork this project. You can download this github project, realize the change that you deem required for your specific use-case and re-upload it on your Organization as a private extension.
This installation will not be supported on our end.<br>
>[!NOTE]
>
> _Consider renaming the extension name in the extension.json file_ -->

## Erweiterungsansicht

Standardmäßig erstellt das ACDL-Script eine neue Datenschicht mit dem Variablennamen `adobeDataLayer`. Die Erweiterungsansicht bietet Ihnen die Möglichkeit, diesen Namen bei Bedarf zu ändern. Der von Ihnen festgelegte Name wird beim Laden von Tags instanziiert.

>[!NOTE]
>
>Beim Ändern des Objektnamens wird das ursprüngliche `adobeDataLayer`-Objekt noch instanziiert und dann in den von Ihnen ausgewählten neuen Variablennamen dupliziert.

## Ereignisse

Die Erweiterung bietet Ihnen die Möglichkeit, Ereignisse auf der Datenschicht zu überwachen. Die folgenden Ereignisse sind verfügbar:

### Überwachen aller Datenänderungen

Wenn Sie diese Option auswählen, überwacht Ihr Ereignis-Listener alle Änderungen an der Datenschicht.

>[!IMPORTANT]
>
>Push-Ereignisse ändern nicht die Datenschicht selbst.

Das folgende Beispiel für Push-Ereignisse wird vom Listener verfolgt:

* ` adobeDataLayer.push({"data":"something"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

Das folgende Beispiel für ein Push-Ereignis wird vom Listener nicht verfolgt:

* ` adobeDataLayer.push({"event":"myevent"})`

### Überwachen aller Ereignisse

Wenn Sie diese Option auswählen, überwacht Ihr Ereignis-Listener alle Ereignisse, die an die Datenschicht gepusht werden.

Das folgende Beispiel für Push-Ereignisse wird vom Listener verfolgt:

* ` adobeDataLayer.push({"event":"myevent"})`
* ` adobeDataLayer.push({"event":"myevent","data":"something"})`

Das folgende Beispiel für ein Push-Ereignis wird vom Listener nicht verfolgt:

* ` adobeDataLayer.push({"data":"something"}) `

### Überwachen eines bestimmten Ereignisses

Wenn Sie ein Ereignis angeben, verfolgt der Ereignis-Listener alle Ereignisse, die mit einer bestimmten Zeichenfolge übereinstimmen.

Wenn Sie beispielsweise `myEvent` bei Verwendung dieser Konfiguration festlegen, verfolgt der Listener nur das folgende Push-Ereignis:

* `adobeDataLayer.push({"event":"myEvent"})`

Sie können auch den Umfang Ihres Ereignis-Listeners ändern. Die verschiedenen Optionen werden im Folgenden zusammengefasst:

* `all`: Dies ist die Standardoption. Sie löst die Regel jedes Mal aus, wenn die oben ausgewählte Bedingung in der Vergangenheit erfüllt wurde oder in der Zukunft gepusht wird. Dies ist die sicherste Option, wenn Sie eine asynchrone Implementierung verwenden.
* `future`: Diese Option löst die Regel nur aus, wenn neue Push-Ereignisse, die Ihrer Bedingung entsprechen, an die Datenschicht gesendet werden.
* `past`: Diese Option löst die Regel nur für alte Push-Ereignisse aus, die Ihrer Bedingung entsprechen. Neue Push-Benachrichtigungen, die Ihrer Bedingung entsprechen, werden ignoriert und lösen die Regel nicht mehr aus.

## Aktionen

In den folgenden Abschnitten werden die von der Erweiterung unterstützten Aktionen beschrieben.

### Zurücksetzen der Datenschicht

Die Erweiterung bietet Ihnen die Möglichkeit, die Länge der Datenschicht zurückzusetzen, was dazu beitragen kann, eine begrenzte Größe für eine Single-Page Application (SPA) beizubehalten.

Es besteht jedoch derzeit keine Möglichkeit, Informationen, die zuvor während der Push-Methoden festgelegt wurden, vollständig zu entfernen.

Die Aktion **Berechneten Status zurücksetzen und festlegen** kopiert den letzten berechneten Status, leert das Datenschichtobjekt und pusht den letzten Status erneut.

### Pushen zur Datenschicht

Die Erweiterung bietet eine Aktion zum Pushen von JSON-Inhalten in die Datenschicht selbst. Diese Aktion ermöglicht die direkte Verwendung von Datenelementen in der JSON-Datei. Innerhalb des JSON-Editors sollten Datenelemente mit Prozentnotation referenziert werden (z. B. `%dataElementName%`).

```json
{
    "page": {
        "url": "%url%",
        "previous_url": "%previous_url%",
        "concatenated_values": "static string %dataElement%"
    }
}
```

## Datenelemente

Die folgenden Abschnitte behandeln die eindeutigen Datenelementtypen, die von der Erweiterung bereitgestellt werden.

### Berechneter Status

Das Datenelement „Datenschicht - berechneter Status“ kann je nach Konfiguration eines von zwei Elementen zurückgeben:

* Status „vollständige Datenschicht“: Standardmäßig wird der berechnete Status „vollständige Datenschicht“ zurückgegeben.
* Bestimmter Pfad: Sie können den Pfad angeben, den Sie in Ihrer Datenschicht zurückgeben möchten. Pfade werden mit Punktnotation angegeben (z. B. `data.foo`).

### Datenschichtgröße

Dieses Datenelement gibt die Größe der Datenschicht zurück. Die Größe der Datenschicht wird durch die Anzahl der Elemente dargestellt, die an dieses Objekt gepusht wurden.

Bei der folgenden Liste von Push-Ereignissen gibt dieses Datenelement die Ganzzahl `2` zurück:

```js
adobeDataLayer.push({"event":"myEvent"})
adobeDataLayer.push({"data":{"foo":"bar"}})
```
