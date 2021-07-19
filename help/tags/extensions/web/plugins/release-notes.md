---
title: Versionshinweise zur Common Analytics Plugins-Erweiterung
description: Die aktuellen Versionshinweise für die allgemeine Analytics-Plug-in-Tag-Erweiterung in Adobe Experience Platform.
source-git-commit: cce218d984bae92428c7d48aefcd0f57dab837ea
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 92%

---

# Common Analytics Plugins – Versionshinweise

## 23. Juni 2021

### Allgemeine Analytics-Plug-ins-Erweiterung 3.0.6

#### Fehlerkorrekturen

* Es wurde ein Problem behoben, bei dem getPercentPageViewed bei der Verwendung von Sonderzeichen fehlschlug.

## 20. Mai 2021

### Allgemeine Analytics-Plug-ins-Erweiterung 3.0.5

#### Fehlerkorrekturen

* Es wurde ein Problem behoben, bei dem getTimeParting bei Verwendung der generischen Initialisierungsaktion nicht korrekt initialisiert wurde.

## 26. März 2021

### Allgemeine Analytics-Plug-ins-Erweiterung 3.0.4

#### Fehlerkorrekturen

* Es wurde ein Problem behoben, bei dem getPageLoadTime fälschlicherweise Variablen für das Fensterobjekt festgelegt hat.
* Es wurde ein Problem behoben, bei dem getQueryParam „nicht definiert“ anstelle von &quot;&quot; zurückgab, wenn queryParam in der Abfragezeichenfolge nicht vorhanden war.
* Es wurde ein Problem behoben, bei dem die falschen Versionsnummern in der Initialisierungsaktion angezeigt wurden.

## 19. März 2021

### Allgemeine Analytics-Plug-ins-Erweiterung 3.0.2

#### Funktionen

* Alle Plug-ins wurden aktualisiert, um automatisch Versionsinformationen als Kontextdaten einzuschließen
* Plug-in „getPercentPageViewed“ hinzugefügt
* Datenelemente für die folgenden Plug-ins hinzugefügt
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* Stile wurden aktualisiert

## 9. April 2020

### Allgemeine Analytics-Plug-ins-Erweiterung 2.2.0

#### Fehlerkorrekturen

* Formulierungen in Erweiterungsansichten wurden korrigiert.

#### Funktionen

* Die Dokumentation in der Initialisierungsaktion wurde aktualisiert.

## 5. Dezember 2019

### Allgemeine Analytics-Plug-ins-Erweiterung 2.1.1

#### Fehlerkorrekturen

* Es wurde ein Problem behoben, das die Abwärtskompatibilität mit Version 2.0.X verhinderte.
* Es wurde ein Problem behoben, bei dem Dokumentationslinks auf die falsche Dokumentation verwiesen.
* Es wurde ein Problem behoben, bei dem in der Initialisierungsaktion zweimal `getTimeSinceLastVisit` angezeigt wurde.

## 15. November 2019

### Allgemeine Analytics-Plug-ins-Erweiterung 2.1.0

#### Fehlerkorrekturen

* Bestimmte Plug-in-Aktionen zur Unterstützung der Abwärtskompatibilität wurden wieder eingeführt
* Es wurde ein Problem mit dem `cleanStr`-Plug-in behoben.
* Es wurde ein Problem mit dem `getResponsiveLayout`-Plug-in behoben.
* Es wurde ein Problem mit dem `getPageName`-Plug-in behoben.

#### Funktionen

* Versionsaktualisierung für `getTimeParting`
* Versionsaktualisierung für `numberSuite`
* Versionsaktualisierung für `getNewRepeat`
* Aktualisierte Dokumentation für alle Plug-ins

## 30. Oktober 2019

### Allgemeine Analytics-Plug-ins-Erweiterung 2.0.3

#### Fehlerkorrekturen

* Es wurde ein Problem behoben, bei dem Dokumentations-Links beschädigt waren.

## 11. Oktober 2019

### Allgemeine Analytics-Plug-ins-Erweiterung 2.0.2

#### Funktionen

* Es wurden 15 Plug-ins zur Erweiterung hinzugefügt.
* Es wurde eine neue Initialisierungsaktion zur einfacheren Implementierung erstellt.

## 11. Juli 2019

### Allgemeine Analytics-Plug-ins-Erweiterung 1.0.4

#### Funktionen

* Eine Erweiterung mit sieben Plug-ins wurde veröffentlicht
* Einzelaktionen zum Initialisieren der einzelnen Plug-ins
