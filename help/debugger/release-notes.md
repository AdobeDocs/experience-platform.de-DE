---
title: Versionshinweise zu Adobe Experience Platform Debugger
description: Die neuesten Versionshinweise für Adobe Experience Platform Debugger.
keywords: Debugger;Experience Platform Debugger-Erweiterung;Chrome;Erweiterung;Versionshinweise
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: ht
source-wordcount: '429'
ht-degree: 100%

---

# Versionshinweise zu Adobe Experience Platform Debugger

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
