---
title: Versionshinweise zur Adobe Target v2-Erweiterung
description: Aktuelle Versionshinweise für die Tag-Erweiterung „Adobe Target v2“ in Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: a062305e3ed0eb4d127f93ff37efe15e41eaa601
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 68%

---

# Versionshinweise zur Adobe Target v2-Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

## v0.20.3 (23. Januar 2024)

- Aktualisierung zur Unterstützung von `at.js` 2.11.4
- Es wurde ein Fehler behoben, durch den verhindert wurde, dass ungültige Geodaten an die Bereitstellungs-API gesendet wurden.

## v0.20.2 (29. November 2023)

- Aktualisierung zur Unterstützung von `at.js` 2.11.3
- Es wurde ein Fehler behoben, der verhinderte, dass Antwort-Token bei at-content-rendering-failed-Ereignissen gesendet wurden.

## v0.20.1 (3. November 2023)

- Es wurde eine Aktualisierung vorgenommen, sodass `at.js` 2.11.2 unterstützt wird.
- Es wurde ein Fehler behoben, der zu Inkonsistenzen in den Antwort-Token führte, die bei benutzerdefinierten Ereignissen gesendet wurden.

## v0.20.0 (9. Oktober 2023)

- Es wurde eine Aktualisierung vorgenommen, sodass `at.js` 2.11.0 unterstützt wird.
- Es wurde Unterstützung für das Festlegen der benutzerdefinierten Adobe Experience Platform-Sandbox-ID und des Sandbox-Namens in targetGlobalSettings hinzugefügt, die bei getOffer/getOffers-Aufrufen an die Bereitstellungs-API übergeben werden.
- Shadow-DOM-Fehlerbehebung für Verkettung :eq() im -Selektor.

## v0.19.3 (18. September 2023)

- Es wurde eine Aktualisierung vorgenommen, sodass `at.js` v2.10.3 unterstützt wird.
- Es wurde ein Problem behoben, das fälschlicherweise das benutzerdefinierte Ereignis „at-content-rendering-success“ auslöste, wenn keine Angebote gerendert werden. Das richtige Ereignis „at-content-rendering-no-offers“ wird jetzt ausgelöst.
- Dem Fehlerobjekt wurden eventToken und responseToken für das benutzerdefinierte Ereignis „at-content-rendering-failed“ hinzugefügt.

## v0.19.2 (14. Februar 2023)

- Es wurde ein Problem behoben, bei dem die Zeitüberschreitung für ein Datenelement festgelegt werden konnte.

## v0.19.1 (3. Februar 2023)

- Es wurde eine Aktualisierung vorgenommen, sodass `at.js` v2.10.1 unterstützt wird
- Benutzerdefinierte Client-Mbox-Parameter unterstützen jetzt korrekt die Punktnotation
- Versandaufrufe nicht mehr in VEC

## v0.19.0 (19. September 2022)

- Es wurde eine Aktualisierung vorgenommen, sodass `at.js` v2.10.0 unterstützt wird
- Domain-übergreifende Tracking-Unterstützung hinzugefügt.

## v0.18.0 (1. Juni 2022)

- Es wurde eine Aktualisierung vorgenommen, sodass `at.js` v2.9.0 unterstützt wird
- Unterstützung für User Agent Client-Hinweise hinzugefügt.

## v0.17.1 (28. Januar 2022)

- Es wurde eine Aktualisierung vorgenommen, sodass `at.js` v2.8.1 unterstützt wird
- Es wurde ein Problem behoben, bei dem `pageLoad` im hybriden ODD-Ausführungsmodus nicht auf `target-global-mbox` abgebildet wurde.
- Es wurde ein Problem mit Analysedetails für `mbox`-Anfragen behoben
- Dev-Abhängigkeiten wurden aktualisiert, um Sicherheitslücken zu beheben

## v0.17.0 (7. Januar 2022)

- Es wurde eine Aktualisierung vorgenommen, sodass `at.js` v2.8.0 unterstützt und jetzt Funktionsnutzungs- und Performance-Telemetriedaten erfasst werden.  Personenbezogene Daten werden nicht erfasst. Um diese Funktion abzuwählen, setzen Sie `telemetryEnabled` in `targetGlobalSettings` auf `false`.

## v0.16.0 (28. Oktober 2021)

- Es wurde eine Aktualisierung vorgenommen, sodass `at.js` v2.7.0 unterstützt wird und jetzt zum Download von Adobe Target verfügbar ist.

## v0.15.2 (16. August 2021)

- Es wurde eine Aktualisierung vorgenommen, sodass `at.js` 2.6.1 unterstützt wird.
- Initialisieren der geräteinternen Entscheidungsfindung beim Start, unabhängig vom Seitenladeereignis.
- Die geräteinterne Entscheidungsfindung kann jetzt beim ersten Besuch nach dem Herunterladen des Artefakts verwendet werden.

## v0.15.1 (20. Juli 2021)

- Es wurde ein Problem mit einem `stringify`-Funktionsnamen behoben, das dazu führte, dass falsche UUID-Werte für `sessionId`, `requestId` usw. generiert wurden.

## v0.15.0 (16. Juli 2021)

- Das Attribut „secure“ wird zu Cookies hinzugefügt, wenn die `at.js`-Einstellung „secureOnly“ auf „true“ gesetzt ist
- Es sind jetzt Response-Token verfügbar, wenn man `triggerView()` verwendet
- Es wurde ein Fehler im Zusammenhang mit dem `CONTENT_RENDERING_NO_OFFERS`-Ereignis behoben. Es wird nun korrekt ausgelöst, wenn keine Inhalte von Target zurückgegeben werden
- Details zur A4T-Klickmetrik werden bei der Verwendung von Prefetch-Anfragen korrekt zurückgegeben
- Die UUID-Generierung verwendet nicht mehr `Math.random()`, sondern beruht auf `window.crypto`
- Der Verfall des `sessionId`-Cookies wird bei jedem Netzwerkaufruf korrekt verlängert
- Die Cache-Initialisierung der SPA-Ansicht wird jetzt korrekt verarbeitet und berücksichtigt die `viewsEnable`-Einstellungen

## v0.14.2 (2. Juni 2021)

- Behebung eines Fehlers, durch den das endgültige Bundle zwei `at.js`-Versionen enthielt, eine mit On-Device Decisioning und eine ohne.

## v0.14.1 (19. Mai 2021)

- Die mit Version 0.14 eingeführte Regression wurde korrigiert, bei der die Aktion „Target laden“ globale Mbox-Aufrufe auslöste

## v0.14 (14. Mai 2021)

- Es wurde die neue Aktion „Target mit [On-Device Decisioning](./overview.md#load-target-with-on-device-decisioning) laden“ hinzugefügt, die `at.js` 2.5 mit Funktionen für On-Device Decisioning lädt.
- `at.js` auf 2.5 aktualisiert


## v0.13.7 (25. März 2021)

- Es wurde ein Problem behoben, bei dem `targetPageParams` in Mbox-Anforderungen enthalten war. `targetPageParams` sollten nur in `pageLoad`-Anforderungen aufgenommen werden.
- Es wurde ein Problem mit globalen Dokument- und Fensterobjekten in der Tag-Erweiterung behoben, indem die globalen Objektabhängigkeiten von Platform Launch durch direkte Verweise darauf ersetzt wurden.
- `at.js` auf 2.4.1 aktualisiert

## v0.13.6 (25. Januar 2021)

- Unterstützt Versand-API-Kunden-IDs mit einheitlicher Profil-/Plattform-ID
- Behebt eine ungültige Injektion eines Stil-Tags
- Aktualisierung von at.s auf 2.4.0
- Behebung eines Problems, bei dem undefinierte Parameter zu fehlerhaften Versandanforderungen führen können

## v0.13.4 (25. November 2020)

- Es wurde ein Fehler behoben, durch den mbox-Parameter nicht in der UI angezeigt wurden
- Brandingupdates
- Aktualisierung der `at.js`-Version auf 2.3.3

## v0.13.3 (24. Juli 2020)

- Es wurde ein Fehler behoben, der dazu führte, dass Links im QS-Modus für inaktive Aktivitäten nicht funktionierten.
- Es wurde ein Fehler behoben, der auftrat, wenn die Erweiterung fehlschlug, wenn ein Skript oder Code die `default`-Eigenschaft zu `window` oder `document` hinzufügte.

## v0.13.2 (15. Juni 2020)

- Es wurde ein Fehler bei der Verwendung von CNAME und Edge Override behoben, bei dem `at.js` 1.x fälschlicherweise die Server-Domain erstellte, wodurch die Target-Anfrage fehlschlug
- Es wurde ein Problem behoben, bei dem Target bei Verwendung der v2-Tag-Erweiterung für die Tag-Erweiterung von Target und Adobe Analytics den Analytics-Aufruf „sendBeacon“ verzögerte.
- Die `deviceIdLifetime` Einstellung wurde verbessert, indem sie durch `targetGlobalSettings` überschrieben werden kann.

## v0.13.0 (25. März 2020)

- `at.js` wurde auf Version 2.3 aktualisiert.
- adobe.target.getOffer-API unterstützt jetzt Target Global Mbox.
- Es wurde ein Problem behoben, bei dem Parameter und Seitenladeparameter nicht korrekt verarbeitet wurden.

## v0.12.0 (10. Oktober 2019)

- `at.js` wurde auf Version 2.2 aktualisiert.
- Verbesserte Performance bei Integrationen zwischen Experience Cloud ID Library (ECID) v4.4 und `at.js` 2.2.
- Zuvor führte die ECID-Bibliothek zwei Sperraufrufe durch, bevor `at.js` Erlebnisse abrufen konnte. Dies wurde auf einen einzigen Aufruf reduziert, wodurch die Performance deutlich verbessert wird.

>[!NOTE]
>Aktualisieren Sie Ihre ECID-Tag-Erweiterung auf Version 4.4.1, um diese Performance-Verbesserung nutzen zu können.

## v0.11.1 (31. Juli 2019)

- Aktualisierung der Erweiterungsversion für die Verwendung von `at.js` 2.1.1.
- Eine Korrektur für die Verwendung von Parametern wurde hinzugefügt.

## v0.11.0 (3. Juni 2019)

- Neue Tag-Erweiterung zur Unterstützung von `at.js` 2.1
