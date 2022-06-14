---
title: Versionshinweise zu Adobe Experience Platform Debugger
description: Die neuesten Versionshinweise für Adobe Experience Platform Debugger.
keywords: Debugger;Experience Platform Debugger-Erweiterung;Chrome;Erweiterung;Versionshinweise
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 9c4f16c84b78403e5baf02595a38093341eefa67
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 2%

---

# Versionshinweise zu Adobe Experience Platform Debugger

## Version 1.3.2 - 9. Juni 2022

* Es wurde ein Standardavatar hinzugefügt, wenn der Benutzer angemeldet ist.
* Es wurde eine Syntaxhervorhebung zu JSON-Objekten in Protokollen hinzugefügt.

## Version 1.3.1 - 24. Mai 2022

* Aktualisierte Abhängigkeiten.
* Es wurde ein Analytics-Problem behoben, bei dem Nachbearbeitungstreffer nicht aktiviert werden konnten.
* Es wurde ein Problem behoben, bei dem der Debugger an das Anmeldefenster der Adobe angehängt wurde.
* AT.js-Problem behoben, bei dem Protokollmeldungen im Debugger nicht angezeigt wurden.

## Version 1.3.0 - 28. Januar 2022

* Der Link Info wurde hinzugefügt, um die aktuelle Version und Hinweise anzuzeigen.
* Ein Umschalter wurde hinzugefügt, um nach der Verarbeitung gesendete Treffer für Analytics-Anforderungen anzuzeigen. Der Umschalter ist im Abschnitt Analytics verfügbar.
* Fehlerkorrektur - Sitzungsfehler beim Remote-Debugging wurde behoben, der auftrat, wenn die Sitzung außerhalb des Debuggers geschlossen wurde.
* Fehlerkorrektur - Die Fehlerbenachrichtigung, die auf der Registerkarte &quot;Edge-Transaktionen&quot;des Web SDK angezeigt wurde, wurde korrigiert.
* Die Adobe-Tags bei veralteter Seite wurden korrigiert, wenn der Debugger auf das _satellite -Objekt zugegriffen hat.
* Es wurden einige Fälle behoben, in denen eine AppMeasurement-Instanz auf der Seite nicht gefunden wurde.
* Es wurde ein Problem mit der Seitenverbindung behoben, das beim ersten Öffnen des Debugger-Fensters auftrat.

## Version 1.2.0 - 26. Oktober 2021

* Anzeigen von Ereignissen aus allen Browser-Registerkarten in der Netzwerkansicht. Um nur die Ereignisse aus der aktuellen Registerkarte anzuzeigen, wählen Sie das Sperrsymbol in der rechten unteren Ecke des Debuggers aus.
* Das Branding wurde aktualisiert.

## Version 1.1.0 - 5. Oktober 2021

* Visualisierung für Remote-Debugging - Organisieren Sie die Remote-Debugging-Ereignisse in einem visuellen Flussdiagramm im Abschnitt Adobe Experience Platform Web SDK > Edge-Transaktionen .
* Die auf der Seite verwendete Adobe Experience Platform Web SDK-IMS-Organisation muss mit der angemeldeten Organisation übereinstimmen, wenn eine neue Remote-Debugging-Sitzung gestartet wird.
* Zeigt nur die Edge-Transaktionen für die Registerkarte &quot;Verbunden&quot;an. Target-Trace-Protokolle sind weiterhin im Abschnitt Protokolle > Edge verfügbar.
* Zulassen der Überschreibung der separaten Datenstrom-ID-Konfiguration für jede Instanz des Adobe Experience Platform Web SDK auf der Seite. Umschalter Debugging aktiviert hinzufügen.
* Es wurde ein Problem behoben, bei dem das Adobe Target-Trace-Token nicht immer mit Remote-Debugging-Sitzungen für das Adobe Experience Platform Web SDK gesendet wurde.

## Version 1.0.0 5. Mai 2021

* Erste Hauptversion von Experience Platform Debugger. Soll den Experience Cloud Debugger ersetzen.
