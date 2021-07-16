---
title: Versionshinweise zur Adobe Target-Erweiterung
description: Die neuesten Versionshinweise für die Adobe Target-Tag-Erweiterung in Adobe Experience Platform.
source-git-commit: 573c13f5136a4efc3accf2838783a91ea914e949
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 77%

---

# Versionshinweise zu Adobe Target

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

## 24. Juli 2020

### Adobe Target-Erweiterung 0.11.3

* Es wurde ein Fehler behoben, der auftrat, wenn die Erweiterung fehlschlug, wenn ein Skript oder Code die `default`-Eigenschaft zu `window` oder `document` hinzufügte.

## 15. Juni 2020

### Adobe Target-Erweiterung 0.11.2

* Es wurde ein Fehler bei der Verwendung von CNAME und Edge Override behoben, bei dem at.js 1.x fälschlicherweise die Serverdomäne erstellte, wodurch die Target-Anfrage fehlschlug.

## 25. März 2020

### Adobe Target-Erweiterung 0.11.1

* at.js wurde auf Version 1.8.1 aktualisiert.
* Es wurde ein Problem behoben, bei dem Parameter und Seitenladeparameter nicht korrekt verarbeitet wurden.

## 10. Oktober 2019

### Adobe Target-Erweiterung 0.11.0

* at.js wurde auf Version 1.8 aktualisiert.
* Verbesserte Leistung bei Integrationen zwischen Experience Cloud ID Library (ECID) v4.4 und at.js 1.8.
* Zuvor führte die ECID-Bibliothek zwei Sperraufrufe durch, bevor at.js Erlebnisse abrufen konnte. Dies wurde auf einen einzigen Aufruf reduziert, wodurch die Leistung deutlich verbessert wird.

>[!NOTE]
>Bitte aktualisieren Sie Ihre ECID-Tag-Erweiterung für Adobe Experience Platform auf Version 4.4.1, um diese Leistungsverbesserung nutzen zu können.

## 31. Juli 2019

### Adobe Target-Erweiterung 0.10.1

* Hotfix für Parameter, die die Tag-Erweiterung für Adobe Target verarbeiten

## 4. Mai 2019

### Adobe Target-Erweiterung 0.10.0

* Behebung eines Problems mit Datenelementen, das durch aktuelle Google Chrome-Änderungen verursacht wurde.

## 14. März 2019

### Adobe Target-Erweiterung 0.9.3

* Aktualisierung der Erweiterungsversion für die Verwendung von at.js 1.7.1.

## 20. Februar 2019

### Adobe Target-Erweiterung 0.9.2

* Reparatur der Gleichzeitigkeitsbedingung zwischen Target- und Analytics-Erweiterungen.

## 12. Februar 2019

### Adobe Target-Erweiterung 0.9.1

#### **Funktionen**

* Aktualisierung der Erweiterung für die Verwendung von at.js 1.7.0, bei dem die Opt-in-Datenschutzfunktion über -Tags unterstützt wird, um zu steuern, wie und wann das Target-Tag ausgelöst wird. Informationen zum Einrichten Ihrer Opt-in-Implementierung finden Sie in der Dokumentation zu Tags . Hinzufügung der Anpassungsmöglichkeit, ob ein Mbox-Parameter mit einem leeren Wert an Target gesendet werden soll oder nicht.

## 23. Januar 2019

### Adobe Target-Erweiterung 0.8.4

* „at.js“ auf Version 1.6.4 aktualisiert.
* Migration der Erweiterungs-Benutzeroberfläche in Adobe Spectrum.

## 15. November 2018

### Adobe Target-Erweiterung 0.8.2

* „at.js“ auf Version 1.6.3 aktualisiert.

## 24. Oktober 2018

### Adobe Target-Erweiterung 0.8.1

* „at.js“ auf Version 1.6.2 aktualisiert.

## 23. August 2018

### Adobe Target-Erweiterung 0.8.0

* „at.js“ auf Version 1.6.0 aktualisiert.

## 10. August 2018

### Adobe Target-Erweiterung 0.7.2

* Geringfügige Änderungen
* Aktualisierung der `exchangeUrl`-Eigenschaft in der `extension.json`-Datei.

## 1. August 2018

### Adobe Target-Erweiterung 0.7.1

* Kleinere Behebungen.

## 18. Juni 2018

### Adobe Target-Erweiterung 0.7.0

* Aktualisierung der at.js-Version auf 1.5.0.
* Behebung eines Problems, bei dem Media Optimizer einen Nullreferenzfehler in IE 11 ausgab.

## 15. Juni 2018

### Adobe Target-Erweiterung 0.6.0

#### **Funktionen**

* Aktualisierung der Target-Erweiterung für die Verwendung von at.js 1.3.1. Wenn Sie Target mit Analytics bereitstellen, warten wir nun, bis alle Target-Aufrufe aufgelöst wurden (einschließlich Umleitungsangebote), bevor Analytics ausgelöst wird, wodurch die bisher vorhandene Gleichzeitigkeitsbedingung aufgehoben wird.

## 22. Februar 2018

### Adobe Target-Erweiterung 0.4.1

#### **Funktionen**

* Hinzufügung der Adobe Exchange-Liste zu extension.json.
* Hinzufügung der Prüfung, ob Target deaktiviert und ob Authoring aktiviert ist.

#### **Fehlerkorrekturen**

* Es wurde ein Fehler in der Adobe Target-Erweiterung behoben, der verhinderte, dass der Visual Experience Composer die Ausblendung der Seite aufhebt, wenn diese über Tags bereitgestellt wurde.

## 8. Februar 2018

### Adobe Target-Erweiterung 0.4.0

#### **Funktionen**

* Aktualisierung der Ansichten in Erweiterungsbildschirmen.
* Aktualisierung von at.js auf Version 1.2.3 (hinzugefügte Unterstützung für JSON-Angebote).
