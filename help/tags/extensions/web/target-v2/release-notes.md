---
title: Versionshinweise zur Adobe Target v2-Erweiterung
description: Die neuesten Versionshinweise für die Adobe Target v2-Tag-Erweiterung in Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 78%

---

# Versionshinweise zur Adobe Target v2-Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

## 19. Mai 2021

### Adobe Target v2-Erweiterung 0.14.1

- Die mit Version 0.14 eingeführte Regression wurde korrigiert, bei der die Aktion „Target laden“ globale Mbox-Aufrufe auslöste

## 14. Mai 2021

### Adobe Target v2-Erweiterung 0.14

- Es wurde die neue Aktion „Target mit [On-Device Decisioning](./overview.md#load-target-with-on-device-decisioning) laden“ hinzugefügt, die at.js 2.5 mit Funktionen für On-Device Decisioning lädt.
- „at.js“ wurde auf 2.5 aktualisiert.


## 25. März 2021

### Adobe Target v2-Erweiterung 0.13.7

- Es wurde ein Problem behoben, bei dem `targetPageParams` in Mbox-Anforderungen enthalten war. `targetPageParams` sollten nur in `pageLoad`-Anforderungen aufgenommen werden.
- Es wurde ein Problem mit globalen Dokumenten- und Fensterobjekten in der Tag-Erweiterung behoben, indem globale Objektabhängigkeiten durch direkte Verweise auf sie ersetzt wurden.
- „at.js“ wurde auf 2.4.1 aktualisiert.

## 25. Januar 2021

### Adobe Target v2-Erweiterung 0.13.6

- Unterstützt Versand-API-Kunden-IDs mit einheitlicher Profil-/Plattform-ID
- Behebt eine ungültige Injektion eines Stil-Tags
- Aktualisierung von at.s auf 2.4.0
- Behebung eines Problems, bei dem undefinierte Parameter zu fehlerhaften Versandanforderungen führen können

## 25. November 2020

### Adobe Target v2-Erweiterung 0.13.4

- Es wurde ein Fehler behoben, durch den mbox-Parameter nicht in der UI angezeigt wurden
- Brandingupdates
- Aktualisierung der at.js-Version auf 2.3.3

## 24. Juli 2020

### Adobe Target v2-Erweiterung 0.13.3

- Es wurde ein Fehler behoben, der dazu führte, dass Links im QS-Modus für inaktive Aktivitäten nicht funktionierten.
- Es wurde ein Fehler behoben, der auftrat, wenn die Erweiterung fehlschlug, wenn ein Skript oder Code die `default`-Eigenschaft zu `window` oder `document` hinzufügte.

## 15. Juni 2020

### Adobe Target v2-Erweiterung 0.13.2

- Es wurde ein Fehler bei der Verwendung von CNAME und Edge Override behoben, bei dem at.js 1.x fälschlicherweise die Serverdomäne erstellte, wodurch die Target-Anfrage fehlschlug.
- Es wurde ein Problem behoben, bei dem Target bei Verwendung der v2-Tag-Erweiterung für die Target- und Adobe Analytics-Tag-Erweiterung den Analytics-Aufruf &quot;sendBeacon&quot;verzögerte.
- Die `deviceIdLifetime` Einstellung wurde verbessert, indem sie durch `targetGlobalSettings` überschrieben werden kann.

## 25. März 2020

### Adobe Target v2-Erweiterung 0.13.0

- at.js wurde auf Version 2.3 aktualisiert.
- adobe.target.getOffer-API unterstützt jetzt Target Global Mbox.
- Es wurde ein Problem behoben, bei dem Parameter und Seitenladeparameter nicht korrekt verarbeitet wurden.

## 10. Oktober 2019

### Adobe Target v2-Erweiterung 0.12.0

- at.js wurde auf Version 2.2 aktualisiert.
- Verbesserte Leistung bei Integrationen zwischen Experience Cloud ID Library (ECID) v4.4 und at.js 2.2.
- Zuvor führte die ECID-Bibliothek zwei Sperraufrufe durch, bevor at.js Erlebnisse abrufen konnte. Dies wurde auf einen einzigen Aufruf reduziert, wodurch die Leistung deutlich verbessert wird.

>[!NOTE]
>Bitte aktualisieren Sie Ihre ECID-Tag-Erweiterung auf Version 4.4.1, um diese Leistungsverbesserung nutzen zu können.

## 31. Juli 2019

### Adobe Target v2-Erweiterung 0.11.1

- Aktualisierung der Erweiterungsversion zur Unterstützung von at.js 2.1.1.
- Eine Korrektur für die Verwendung von Parametern wurde hinzugefügt.

## 3. Juni 2019

### Adobe Target v2-Erweiterung 0.11.0

- Neue Tag-Erweiterung zur Unterstützung von at.js 2.1
