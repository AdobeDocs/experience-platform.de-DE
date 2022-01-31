---
title: Versionshinweise zur Adobe Target v2-Erweiterung
description: Aktuelle Versionshinweise für die Tag-Erweiterung „Adobe Target v2“ in Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 824fea41bc7e7082814648efd58184f5208e5e6f
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 75%

---

# Versionshinweise zur Adobe Target v2-Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

## 28. Januar 2022

### Adobe Target v2-Erweiterung 0.17.1

- Auf Unterstützung aktualisiert `at.js` v2.8.1
- Fest `pageLoad` werden nicht zugeordnet zu `target-global-mbox` im ODD-Hybrid-Ausführungsmodus
- Es wurde ein Problem mit Analysedetails für behoben. `mbox` Anfrage
- Aktualisierte Dev-Abhängigkeiten zur Behebung von Sicherheitslücken

## 7. Januar 2022

### Adobe Target v2-Erweiterung 0.17.0

- Auf Unterstützung aktualisiert `at.js` Version 2.8.0, die jetzt Nutzungsdaten von Funktionen und Leistungstelemetriedaten erfasst.  Personenbezogene Daten werden nicht erfasst. Um diese Funktion abzuwählen, setzen Sie `telemetryEnabled` in `targetGlobalSettings` auf `false`.

## 28. Oktober 2021

### Adobe Target v2-Erweiterung 0.16.0

- Auf Unterstützung aktualisiert `at.js` Version 2.7.0, jetzt für den Download von Adobe Target verfügbar.

## 20. Juli 2021

### Adobe Target v2-Erweiterung 0.15.1

- Es wurde ein Problem mit einem `stringify`-Funktionsnamen behoben, das dazu führte, dass falsche UUID-Werte für `sessionId`, `requestId` usw. generiert wurden.

## 16. Juli 2021

### Adobe Target v2-Erweiterung 0.15.0

- Fügen Sie Cookies immer das Attribut secure hinzu, wenn `at.js` settings secureOnly auf true festgelegt ist
- Es sind jetzt Response-Token verfügbar, wenn man `triggerView()` verwendet
- Es wurde ein Fehler im Zusammenhang mit dem `CONTENT_RENDERING_NO_OFFERS`-Ereignis behoben. Es wird nun korrekt ausgelöst, wenn keine Inhalte von Target zurückgegeben werden
- Details zur A4T-Klickmetrik werden bei der Verwendung von Prefetch-Anfragen korrekt zurückgegeben
- Die UUID-Generierung verwendet nicht mehr `Math.random()`, sondern beruht auf `window.crypto`
- Der Verfall des `sessionId`-Cookies wird bei jedem Netzwerkaufruf korrekt verlängert
- Die Cache-Initialisierung der SPA-Ansicht wird jetzt korrekt verarbeitet und berücksichtigt die `viewsEnable`-Einstellungen

## 2. Juni 2021

### Adobe Target v2-Erweiterung 0.14.2

- Beheben Sie einen Fehler, durch den das finale Bundle zwei enthält. `at.js` Versionen, eine mit On-Device Decisioning und eine ohne.

## 19. Mai 2021

### Adobe Target v2-Erweiterung 0.14.1

- Die mit Version 0.14 eingeführte Regression wurde korrigiert, bei der die Aktion „Target laden“ globale Mbox-Aufrufe auslöste

## 14. Mai 2021

### Adobe Target v2-Erweiterung 0.14

- Es wurde die neue Aktion „Target mit [On-Device Decisioning](./overview.md#load-target-with-on-device-decisioning) laden“ hinzugefügt, die 2.5 mit Funktionen für On-Device Decisioning lädt.`at.js`
- Aktualisiert `at.js` bis 2.5


## 25. März 2021

### Adobe Target v2-Erweiterung 0.13.7

- Es wurde ein Problem behoben, bei dem `targetPageParams` in Mbox-Anforderungen enthalten war. `targetPageParams` sollten nur in `pageLoad`-Anforderungen aufgenommen werden.
- Es wurde ein Problem mit globalen Dokument- und Fensterobjekten in der Tag-Erweiterung behoben, indem die globalen Objektabhängigkeiten von Platform Launch durch direkte Verweise darauf ersetzt wurden.
- Aktualisiert `at.js` bis 2.4.1.

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
- Die `at.js` Version auf 2.3.3

## 24. Juli 2020

### Adobe Target v2-Erweiterung 0.13.3

- Es wurde ein Fehler behoben, der dazu führte, dass Links im QS-Modus für inaktive Aktivitäten nicht funktionierten.
- Es wurde ein Fehler behoben, der auftrat, wenn die Erweiterung fehlschlug, wenn ein Skript oder Code die `default`-Eigenschaft zu `window` oder `document` hinzufügte.

## 15. Juni 2020

### Adobe Target v2-Erweiterung 0.13.2

- Es wurde ein Problem bei der Verwendung von CNAME und Edge Override behoben, bei dem `at.js` 1.x kann die Serverdomäne falsch erstellen, was dazu führt, dass die Target-Anforderung fehlschlägt
- Es wurde ein Problem behoben, bei dem Target bei Verwendung der v2-Tag-Erweiterung für die Tag-Erweiterung von Target und Adobe Analytics den Analytics-Aufruf „sendBeacon“ verzögerte.
- Die `deviceIdLifetime` Einstellung wurde verbessert, indem sie durch `targetGlobalSettings` überschrieben werden kann.

## 25. März 2020

### Adobe Target v2-Erweiterung 0.13.0

- Aktualisiert `at.js` auf v2.3.
- adobe.target.getOffer-API unterstützt jetzt Target Global Mbox.
- Es wurde ein Problem behoben, bei dem Parameter und Seitenladeparameter nicht korrekt verarbeitet wurden.

## 10. Oktober 2019

### Adobe Target v2-Erweiterung 0.12.0

- Aktualisiert `at.js` auf v2.2.
- Verbesserte Leistung bei Integrationen zwischen der Experience Cloud ID Library (ECID) v4.4 und `at.js` 2.2.
- Zuvor führte die ECID-Bibliothek zwei Blockierungsaufrufe durch, bevor `at.js` Erlebnisse abrufen. Dies wurde auf einen einzigen Aufruf reduziert, wodurch die Leistung deutlich verbessert wird.

>[!NOTE]
>Aktualisieren Sie Ihre ECID-Tag-Erweiterung auf Version 4.4.1, um diese Leistungsverbesserung nutzen zu können.

## 31. Juli 2019

### Adobe Target v2-Erweiterung 0.11.1

- Aktualisierte Erweiterungsversion zur Verwendung `at.js` 2.1.1
- Eine Korrektur für die Verwendung von Parametern wurde hinzugefügt.

## 3. Juni 2019

### Adobe Target v2-Erweiterung 0.11.0

- Neue Tag-Erweiterung zur Unterstützung `at.js` 2,1
