---
title: Versionshinweise zu Adobe Experience Platform Debugger
description: Die neuesten Versionshinweise für Adobe Experience Platform Debugger.
keywords: Debugger;Experience Platform Debugger-Erweiterung;Chrome;Erweiterung;Versionshinweise
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: a5af5c194bc6b3bf9a6e119a2f147efa85f263f0
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 93%

---

# Versionshinweise zu Adobe Experience Platform Debugger

## Version 1.6.3 - 30. April 2025

### Fehlerbehebungen und Verbesserungen

* Fehlerkorrektur - Der Debugger verhindert, dass DTM- und Tags-Funktionen funktionieren.
* Es wurde ein Problem behoben, bei dem nachbearbeitete Analytics-Treffer nicht in Protokollen angezeigt wurden.
* Es wurde ein Problem behoben, bei dem Daten in Nicht-ASCII-Sprachen wie Japanisch in Protokollen nicht korrekt angezeigt wurden.

## Version 1.6.2 – Mittwoch, 1. Oktober 2024

### Fehlerbehebungen und Verbesserungen

* Es wurde ein Problem behoben, bei dem der Debugger zu empfindlich auf alle CSP-Fehler reagierte

## Version 1.6.1 – 25. Juli 2024

### Fehlerbehebungen und Verbesserungen

* Es wurde ein Problem behoben, durch das Benutzende keine neuen Tags-Einbettungs-Codes zu Seiten hinzufügen konnten, für die sie nicht vorhanden waren.

## Version 1.6.0 – 11. Juli 2024

### Neue Funktionen

* Ermöglicht es Benutzenden, die Erfassung technischer und personenbezogenen Daten auszuwählen/abzuwählen.

### Fehlerbehebungen und Verbesserungen

* Der Link zur Skriptinjektion und Datenschutzrichtlinie von Firefox wurde korrigiert.
* Es wurden fehlende Analytics-Anforderungen erfasst.
* Es wurden Abstürze auf Seiten mit vielen komplexen Konsolenmeldungen behoben.
* Der Adobe Experience Platform Debugger wurde auf die Manifest v3-Erweiterung aktualisiert.

## Version 1.5.4 – 19. Dezember 2023

### Fehlerbehebungen und Verbesserungen

* Es wurde ein Problem behoben, bei dem Einstellungen nicht beibehalten wurden.
* Es wurde ein Fehler behoben, bei dem der Debugger abstürzte, während die Analytics-Treffer nach der Verarbeitung angezeigt wurden.

## Version 1.5.3 – 6. Dezember 2023

### Neue Funktionen

* Eine Einstellung zum Fixieren der aktiven Registerkarte beim Öffnen des Debuggers wurde hinzugefügt.

### Fehlerbehebungen und Verbesserungen

* Es wurde ein Problem behoben, bei dem Analytics-Anfragen auf privaten Domains fehlten.
* Es wurde ein Problem behoben, bei dem Activity Map-Daten in der Analytics-Anfragentabelle fehlten.
* Es wurde ein Problem behoben, bei dem das Anzeigen der Target Trace zu einem Absturz führte.
* Es wurde eine Warnung hinzugefügt, wenn der Debugger die Einrichtung einer On-Page-Infrastruktur in Firefox nicht durchführt.

## Version 1.5.2 – 10. November 2023

(Nur Firefox)

### Fehlerbehebungen und Verbesserungen

* Die Organisation von Dateien wurde aktualisiert.

## Version 1.5.1 – 2. November 2023

### Fehlerbehebungen und Verbesserungen

* Es wurden Probleme behoben, bei denen Analytics-Ereignisse ignoriert oder dupliziert wurden.
* Es wurde ein Problem behoben, bei dem die maximale Speichergröße für den Status überschritten wurde.
* Es wurde ein Problem behoben, bei dem die Edge Logs-Suche keine Ereignisse filterte.

## Version 1.5.0 – 19. Oktober 2023

### Neue Funktionen

* Zeigt Links zu Eigenschaften, Umgebungen und Regeln in der Zusammenfassung und den Protokollen von Tags an.

### Fehlerbehebungen und Verbesserungen

* Es wurde ein Problem behoben, bei dem keine Daten zu Tag-Zusammenfassungen gesendet wurden.
* Es wurde ein Problem behoben, durch das bei Assurance-Sitzungen ein CORS-Fehler ausgegeben wurde.
* Es wurde ein Problem behoben, das die Anzeige von Target Trace verhinderte.
* Ein Fehler bei der Schaltfläche „Feedback senden“ wurde korrigiert.
* Das Fehlen der „Datastream-ID“ in der Web SDK-Zusammenfassung für Version ≥ 2.18.0 wurde behoben.
* Es wurde ein Problem behoben, bei dem Edge-Protokolle nicht durchsuchbar waren.
* Es wurde ein Hinweis zu zusätzlichen Profilen für bestimmte Kontotypen hinzugefügt.

## Version 1.4.1 – 1. November 2022

* Die Leistung auf Seiten mit vielen Adobe Experience Platform Assurance-Ereignissen wurde verbessert.

## Version 1.4.0 – 3. Oktober 2022

* Es wurde Unterstützung zum Debuggen von AEP Assurance für Hybrid-Implementierungen des Web SDK hinzugefügt.
* Innerhalb derselben AEP Assurance-Sitzung werden nun mehrere Registerkarten unterstützt.
* Es wurde ein Problem behoben, bei dem Benutzende nach der Anmeldung keine Profile/Organisationen wechseln konnten.
   * Bei einigen Konten ist eine Abmeldung und eine erneute Anmeldung erforderlich, um zwischen Organisationen zu wechseln.
* Es wurde eine Fehlermeldung hinzugefügt, wenn die Target-Trace-Aktivierung fehlschlägt.
* Abhängigkeiten wurden aktualisiert.

## Version 1.3.3 – 20. Juni 2022

* Es wurde ein Problem behoben, durch das das Öffnen von Popups aus Netzwerkereignistabellen verhindert wurde.
* Es wurde ein Problem behoben, durch das das Laden von Alloy-Informationen auf der Seite verhindert wurde.

## Version 1.3.2 – 9. Juni 2022

* Es wurde ein Standard-Avatar hinzugefügt, wenn die Benutzerin bzw. der Benutzer angemeldet ist.
* Es wurde eine Syntaxhervorhebung für JSON-Objekte in Protokollen hinzugefügt.

## Version 1.3.1 – 24. Mai 2022

* Abhängigkeiten wurden aktualisiert.
* Es wurde ein Analytics-Problem behoben, bei dem Nachbearbeitungstreffer nicht aktiviert werden konnten.
* Es wurde ein Problem behoben, bei dem der Debugger an das Adobe-Anmeldefenster angehängt wurde.
* Es wurde ein AT.js-Problem behoben, bei dem Protokollmeldungen nicht im Debugger angezeigt wurden.

## Version 1.3.0 – 28. Januar 2022

* Es wurde ein „Info über“-Link hinzugefügt, um die aktuelle Version und Hinweise anzuzeigen.
* Es wurde ein Umschalter hinzugefügt, um Nachbearbeitungstreffer für Analytics-Anfragen anzuzeigen. Der Umschalter ist im Analytics-Abschnitt verfügbar.
* Es wurde ein Remote-Debugging-Sitzungsfehler behoben, der auftrat, wenn die Sitzung außerhalb des Debuggers geschlossen wurde.
* Es wurde ein Fehler bei einer Fehlerbenachrichtigung behoben, der auf der Web SDK-Registerkarte für Edge-Transaktionen angezeigt wurde.
* Es wurden Adobe-Tags bei Warnungen für veraltete Seiten korrigiert, wenn der Debugger auf das _satellite-Objekt zugegriffen hat.
* Es wurden einige Fälle korrigiert, bei denen eine AppMeasurement-Instanz auf der Seite nicht gefunden wurde.
* Es wurde ein Problem mit der Seitenverbindung behoben, das beim ersten Öffnen des Debugger-Fensters auftrat.

## Version 1.2.0 – 26. Oktober 2021

* Es werden Ereignisse von allen Browser-Registerkarten in der Netzwerkansicht angezeigt. Um nur die Ereignisse von der aktuellen Registerkarte anzuzeigen, wählen Sie das Schlosssymbol unten rechts im Debugger aus.
* Das Branding wurde aktualisiert.

## Version 1.1.0 – 5. Oktober 2021

* Visualisierung für Remote-Debugging: Remote-Debugging-Ereignisse werden in einem visuellen Flussdiagramm unter „Adobe Experience Platform Web SDK > Edge-Transaktionen“ organisiert.
* Die auf der Seite verwendete Organisation für das Adobe Experience Platform Web SDK muss mit der angemeldeten Organisation übereinstimmen, wenn eine neue Remote-Debugging-Sitzung gestartet wird.
* Es werden nur die Edge-Transaktionen für die Registerkarte „Verbunden“ angezeigt. Target-Trace-Protokolle sind weiterhin unter „Protokolle“ > „Edge“ verfügbar.
* Das Überschreiben separater Datenstrom-ID-Konfigurationen für jede Instanz des Adobe Experience Platform Web SDK auf der Seite ist jetzt zulässig. Ein Debugging-fähiger Umschalter wurde hinzugefügt.
* Es wurde ein Problem behoben, durch das das Adobe Target-Trace-Token nicht immer mit Remote-Debugging-Sitzungen für das Adobe Experience Platform Web SDK gesendet wurde.

## Version 1.0.0 – 5. Mai 2021

* Erste Hauptversion von Experience Platform Debugger. Soll Experience Cloud Debugger ersetzen.
