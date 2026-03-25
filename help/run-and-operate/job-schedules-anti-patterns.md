---
description: Erfahren Sie, wie Sie allgemeine Antimuster bei der Konfiguration von Auftragsplänen in Adobe Experience Platform identifizieren und auflösen.
solution: Experience Platform
title: Ermitteln von Anti-Mustern für Auftragspläne
type: Tutorial
exl-id: f94e3ef3-2252-46f5-8075-45b5483d9d83
source-git-commit: 41abc542b11dcd9c295d29cdfad68720ad50129d
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Identifizieren von Antimustern für Auftragspläne

>[!IMPORTANT]
>
>[!UICONTROL Job schedules] sind derzeit nur für die folgenden Real-Time CDP-Aufträge verfügbar:
>
> * Batch-Data-Lake-Aufnahme
> * Batch-Profilaufnahme
> * Batch-Segmentierung
> * Batch-Zielaktivierung

Die [Vorgangszeitpläne](job-schedules.md) hilft Ihnen, häufige Konfigurationsprobleme zu identifizieren, die sich negativ auf die Leistung und Zuverlässigkeit Ihrer Datenpipeline auswirken können. Diese Anti-Muster führen häufig zu Auftragsfehlern, Dateninkonsistenzen oder schlechterer Systemleistung. Durch das frühzeitige Erkennen dieser Muster können Sie Ihre Aufträge neu konfigurieren, um Probleme zu vermeiden, bevor sie sich auf Ihre Geschäftsvorgänge auswirken.

## Voraussetzungen {#prerequisites}

Bevor Sie Anti-Muster identifizieren, sollten Sie:

* Zugriff auf [!UICONTROL Job Schedules] mit der **[!UICONTROL View Job Schedules]** Zugriffssteuerungsberechtigung[ haben](/help/access-control/home.md#permissions).
* Machen Sie sich mit der [Benutzeroberfläche für Auftragspläne](job-schedules.md#understanding-interface) und dem Lesen der Zeitleisten-Ansicht vertraut.
* Grundlegende [ (Batch](../ingestion/batch-ingestion/overview.md)Aufnahme), [Segmentierung](../segmentation/home.md) und [Profilverarbeitung](../profile/home.md) Konzepte verstehen.

## Kurzübersicht {#anti-pattern-quick-reference}

| Anti-Muster | Was Sie auf der Timeline sehen werden | Primäre Auswirkung | Schweregrad |
|--------------|----------------------------------|----------------|----------|
| [Planen von Überschneidungen](#schedule-overlap-pattern) | Mehrere gleichzeitig ausgeführte Aufträge | Ressourcenkonflikt und fehlgeschlagene Aufträge | Hoch |
| [Geplante Auftragsdichte](#scheduled-density) | Viele Datensätze mit Batches in derselben Stunde gruppiert | Pipeline-Engpässe und unvollständige Segmentierung | Hoch |
| [Zu viele Batches pro Datensatz](#excessive-batches-per-dataset) | Einzelner Datensatz mit Dutzenden von täglichen Batches | Ineffiziente Verarbeitung und komplexe Betriebsabläufe | Mittel |

## Planen von Überschneidungen {#schedule-overlap-pattern}

**Schweregrad der Auswirkungen**: Hoch | **Primäres Problem**: Ressourcenkonflikt

**Worauf Sie achten sollten**: Mehrere Aufträge, die gleichzeitig oder in enger Abfolge ausgeführt werden sollen, insbesondere wenn ressourcenintensive Aufträge sich überschneiden.

Ein gängiges Beispiel sind Batch-Erfassungsaufträge, die gleichzeitig mit einem geplanten Segmentierungsauftrag ausgeführt werden. Dies führt zu einem Ressourcenkonflikt, da beide Vorgänge eine erhebliche Verarbeitungsleistung und Arbeitsspeicher erfordern.

**Warum ist das problematisch**:

* **Ressourcenkonflikt**: Wenn mehrere ressourcenintensive Aufträge gleichzeitig ausgeführt werden, konkurrieren sie um Systemressourcen (CPU, Arbeitsspeicher, E/A), wodurch alle Aufträge langsamer ausgeführt werden.
* **Unvorhersehbare Leistung**: Die Auftragsdauer wird inkonsistent, was die Planung zuverlässiger Zeitpläne erschwert.
* **Kaskadierende Verzögerungen**: Wenn Aufträge länger als erwartet dauern, können sie nachgelagerte abhängige Aufträge verzögern, was einen Welleneffekt in der gesamten Pipeline erzeugt.
* **Erhöhtes Ausfallrisiko**: Eine Ressourcenerschöpfung kann dazu führen, dass Aufträge aufgrund von Zeitüberschreitungen oder komplett fehlschlagen.

**Wie kann ich das Problem beheben**:

* **Auftragspläne staffeln**: Stellen Sie sicher, dass ressourcenintensive Vorgänge sequenziell und nicht gleichzeitig ausgeführt werden.
* **Pufferzeit hinzufügen**: Lassen Sie zur Berücksichtigung von Verarbeitungsvarianzen einen angemessenen Abstand zwischen Aufträgen.
* **Abhängigkeiten überprüfen**: Identifizieren Sie, welche Aufträge abgeschlossen werden müssen, bevor andere sicher starten können.

## Geplante Auftragsdichte {#scheduled-density}

**Schweregrad der Auswirkungen**: Hoch | **Primäres Problem**: Pipeline-Engpässe

**Suchen nach**: Zu viele Datensätze mit mehreren Batches, die innerhalb derselben Stunde geplant sind, insbesondere wenn diese Batches nahe beieinander gestapelt und in der Nähe kritischer Verarbeitungsfenster wie der Segmentierungs-Startzeiten geplant werden.

Dieses Muster umfasst normalerweise:

* Mehrere Datensätze mit jeweils mehreren Batches pro Tag
* ETL-Aufträge (Data-Lake-Aufnahme und Profilaufnahme), die innerhalb derselben Stunde geclustert wurden
* Batch-Aufnahme unmittelbar vor oder während geplanter Segmentierungsfenster geplant

**Warum ist das problematisch**:

* **Pipeline-Engpass**: Wenn innerhalb eines kurzen Zeitfensters zahlreiche Batches aus verschiedenen Datensätzen gestapelt werden, entsteht ein Verarbeitungs-Engpass, der die Aufnahme-Pipeline überfordern kann.
* **Verzögerte Profilverfügbarkeit**: Aufträge zur Profilaufnahme, die zu nahe an den Segmentierungs-Startzeiten liegen, werden möglicherweise nicht rechtzeitig abgeschlossen, was zu unvollständigen oder veralteten Zielgruppenauswertungen führt.
* **Unvorhersehbare Segmentierung**: Wenn Upstream-Aufnahmevorgänge zu Beginn der Segmentierung noch ausgeführt werden, besteht die Gefahr, dass Zielgruppen anhand unvollständiger Daten bewertet werden, was zu einer falschen Zielgruppenzugehörigkeit führt.
* **Kaskadierende Fehler**: Ein einzelner verzögerter Batch in einem dicht gestapelten Zeitplan kann einen Dominoeffekt verursachen, der alle nachfolgenden Batches und nachgelagerten Prozesse verzögert.
* **Ressourcenbelastung**: Das System kann Schwierigkeiten bei der Zuweisung ausreichender Ressourcen haben, wenn zu viele gleichzeitige Aufnahmevorgänge verarbeitet werden, was zu langsameren Verarbeitungszeiten oder Fehlern führt.

**Wie kann ich das Problem beheben**:

* **Batches konsolidieren**: Reduzieren Sie die Batch-Häufigkeit, indem Sie mehrere kleine Batches in weniger, größeren Batches pro Datensatz kombinieren.
* **Gleichmäßig verteilen**: Verteilen Sie Aufnahmeaufträge über den Tag, anstatt sie in bestimmten Stunden zu gruppieren.
* **Pufferzeit hinzufügen**: Stellen Sie sicher, dass zwischen dem Abschluss der Profilaufnahme und dem Start der Segmentierung ein Puffer von mindestens 1-2 Stunden vorhanden ist.
* **Anforderungen überprüfen**: Beurteilen, ob alle Datensätze wirklich mehrere tägliche Batches benötigen. Viele Anwendungsfälle funktionieren mit weniger häufigen Aktualisierungen.

## Zu viele Batches pro Datensatz {#excessive-batches-per-dataset}

**Schweregrad der Auswirkungen**: Medium | **Primäres Problem**: Ineffiziente Verarbeitung

**Wonach Sie suchen sollten**: Ein einzelner Datensatz mit einer übermäßigen Anzahl einzelner Batch-Vorgänge, die über den ganzen Tag geplant sind, wodurch ein langer vertikaler Stapel von Vorgängen auf der Timeline erstellt wird.

Dieses Muster beinhaltet einen einzelnen Datensatz mit vielen einzelnen Batch-Erfassungsvorgängen, die in häufigen Intervallen geplant werden, manchmal in Dutzenden von Batches pro Tag.

**Warum ist das problematisch**:

* **Ineffiziente Verarbeitung**: Jeder Batch-Vorgang verursacht Gemeinkosten (Initialisierung, Validierung, Metadatenaktualisierungen). Die Verarbeitung vieler kleiner Batches ist deutlich weniger effizient als die Verarbeitung weniger großer Batches.
* **Vergrößerte Ausfallfläche**: Mehr Arbeitsplätze bedeuten mehr Ausfallmöglichkeiten. Jeder fehlgeschlagene Batch muss untersucht und möglicherweise erneut verarbeitet werden.
* **Unnötige Systemlast**: Häufige kleine Batches sorgen dafür, dass das System ständig mit Overhead-Aufgaben beschäftigt ist, anstatt Daten zu verarbeiten, was den Gesamtdurchsatz verringert.
* **Verzögerte Datenverfügbarkeit**: Paradoxerweise kann die Ausführung vieler kleiner Batches eine Verzögerung verursachen, wenn Daten für nachgelagerte Prozesse verfügbar werden, im Vergleich zu konsolidierten Batches.
* **Schwierige Inspektion**: Das Nachverfolgen des Erfolgs und der Leistung von Dutzenden einzelner Batch-Vorgänge pro Datensatz wird betrieblich komplex und zeitaufwendig.
* **Profil-Verarbeitungsverzögerung**: Jeder Profil-Aufnahme-Batch Trigger die Profilverarbeitung. Häufig kleine Batches können dazu führen, dass die Profilverarbeitung fast kontinuierlich ausgeführt wird, was eine effiziente Batch-Optimierung verhindert.

**Wie kann ich das Problem beheben**:

* **Reduzieren der Batch** Häufigkeit: Konsolidieren Sie für die meisten Anwendungsfälle auf weniger Batches pro Tag und Datensatz.
* **Batch-Größe erhöhen**: Sammeln Sie mehr Daten, bevor Sie die Aufnahme auslösen, anstatt sie sofort aufzunehmen.
* **Geschäftsanforderungen anpassen**: Überprüfen Sie, ob stündliche Updates wirklich erforderlich sind oder ob tägliche/zweimal tägliche Updates ausreichen.
* **Streaming für Echtzeit verwenden**: Wechseln Sie zur Streaming-Aufnahme, um echte Echtzeitanforderungen zu erfüllen, anstatt dies mit häufigen Batches zu simulieren.

## Nächste Schritte {#next-steps}

Nachdem Sie Anti-Muster in Ihren Jobplänen identifiziert haben:

* Zeigen Sie [Auftragsdetails](job-schedules-details.md) an, um bestimmte Datensätze und Auftragsausführungen zu untersuchen, die Probleme verursachen können.
* Informieren Sie [ über die ](job-schedules.md) und Inspektionsfunktionen in der Übersicht zu Auftragsplänen.
* Erfahren Sie mehr über [Batch-Aufnahme](../ingestion/batch-ingestion/overview.md) um Ihre Datenladepläne zu optimieren.
* Grundlegendes [Segmentierungspläne](../segmentation/home.md), um einen korrekten Zeitplan für Zielgruppenbewertungen sicherzustellen.
* Erkunden Sie [Überwachen von Zieldatenflüssen](../dataflows/ui/monitor-destinations.md) um die End-to-End-Pipeline-Sichtbarkeit zu ermitteln.
