---
title: Versionshinweise zur Adobe Target v2-Erweiterung
description: Aktuelle Versionshinweise für die Tag-Erweiterung „Adobe Target v2“ in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: ht
source-wordcount: '572'
ht-degree: 100%

---

# Versionshinweise zur Erweiterung „Adobe Target v2“

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere Terminologieänderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

## 20. Juli 2021

### Adobe Target v2-Erweiterung 0.15.1

- Es wurde ein Problem mit einem `stringify`-Funktionsnamen behoben, das dazu führte, dass falsche UUID-Werte für `sessionId`, `requestId` usw. generiert wurden.

## 16. Juli 2021

### Adobe Target v2-Erweiterung 0.15.0

- Das Sichern-Attribut wird zu Cookies hinzugefügt, wenn die at.js-Einstellung „secureOnly“ auf „Wahr“ gesetzt ist
- Es sind jetzt Response-Token verfügbar, wenn man `triggerView()` verwendet
- Es wurde ein Fehler im Zusammenhang mit dem `CONTENT_RENDERING_NO_OFFERS`-Ereignis behoben. Es wird nun korrekt ausgelöst, wenn keine Inhalte von Target zurückgegeben werden
- Details zur A4T-Klickmetrik werden bei der Verwendung von Prefetch-Anfragen korrekt zurückgegeben
- Die UUID-Generierung verwendet nicht mehr `Math.random()`, sondern beruht auf `window.crypto`
- Der Verfall des `sessionId`-Cookies wird bei jedem Netzwerkaufruf korrekt verlängert
- Die Cache-Initialisierung der SPA-Ansicht wird jetzt korrekt verarbeitet und berücksichtigt die `viewsEnable`-Einstellungen

## 2. Juni 2021

### Adobe Target v2-Erweiterung 0.14.2

- Behebung eines Fehlers, durch den das finale Bundle zwei at.js-Versionen enthält, eine mit On-Device Decisioning und eine ohne.

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
- Es wurde ein Problem mit globalen Dokument- und Fensterobjekten in der Tag-Erweiterung behoben, indem die globalen Objektabhängigkeiten durch direkte Verweise darauf ersetzt wurden.
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

- Es wurde ein Fehler bei der Verwendung von CNAME und Edge Override behoben, bei dem at.js 1.x fälschlicherweise die Server-Domain erstellte, wodurch die Target-Anfrage fehlschlug.
- Es wurde ein Problem behoben, bei dem bei Verwendung der v2-Tag-Erweiterung für Target und Adobe Analytics Target den sendBeacon-Aufruf an Analytics verzögerte.
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
>Aktualisieren Sie Ihre ECID-Tag-Erweiterung auf Version 4.4.1, um diese Leistungsverbesserung nutzen zu können.

## 31. Juli 2019

### Adobe Target v2-Erweiterung 0.11.1

- Aktualisierung der Erweiterungsversion zur Unterstützung von at.js 2.1.1.
- Eine Korrektur für die Verwendung von Parametern wurde hinzugefügt.

## 3. Juni 2019

### Adobe Target v2-Erweiterung 0.11.0

- Neue Tag-Erweiterung zur Unterstützung von at.js 2.1
