---
description: Erfahren Sie, wie Sie geplante Batch-Verarbeitungsaufträge mit dem Tool für Vorgangszeitpläne in Adobe Experience Platform überprüfen und Fehler beheben können.
solution: Experience Platform
title: Prüfen von Vorgangszeitplänen
type: Tutorial
exl-id: ce855b19-66ab-4d3d-924e-fb9928676aa2
source-git-commit: 41abc542b11dcd9c295d29cdfad68720ad50129d
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---

# Prüfen von Vorgangszeitplänen

>[!IMPORTANT]
>
>[!UICONTROL Job schedules] sind derzeit nur für die folgenden Real-Time CDP-Aufträge verfügbar:
>
> * Batch-Data-Lake-Aufnahme
> * Batch-Profilaufnahme
> * Batch-Segmentierung
> * Batch-Zielaktivierung

[!UICONTROL Job Schedules] bietet eine einheitliche Ansicht aller geplanten Batch-Verarbeitungsaufträge in Ihrer Datenpipeline, von der Aufnahme bis zur Zielaktivierung. Überprüfen Sie den Ausführungsstatus, ermitteln Sie Planungskonflikte und diagnostizieren Sie Konfigurationsprobleme, bevor sie sich auf Ihre Geschäftsvorgänge auswirken.

Verwenden Sie Vorgangszeitpläne, um Fehler zu untersuchen, den Vorgangszeitpunkt zu optimieren und die Abhängigkeiten zwischen der Data-Lake-Aufnahme, der Profilverarbeitung, der Segmentierung und der Zielaktivierung zu verstehen. Anleitungen zum Beheben häufiger Konfigurationsprobleme finden Sie in der Dokumentation unter [Ermitteln von Anti-Mustern für den Auftragsplan](job-schedules-anti-patterns.md).

## Voraussetzungen {#prerequisites}

Für den Zugriff auf [!UICONTROL Job Schedules] benötigen Sie die **[!UICONTROL View Job Schedules]** und **[!UICONTROL View Profile Management]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions)

Wenden Sie sich an Ihren Systemadministrator, um sicherzustellen, dass Sie über die entsprechenden Berechtigungen verfügen.

## Erste Schritte {#getting-started}

Vor der Verwendung von [!UICONTROL Job Schedules] sollten Sie mit den folgenden Experience Platform-Konzepten vertraut sein:

* **[Batch-Aufnahme](../ingestion/batch-ingestion/overview.md)**: So werden Daten in terminierten Intervallen in den Data Lake und den Profilspeicher geladen.
* **[Segmentierung](../segmentation/home.md)**: Wie Zielgruppen basierend auf Profildaten und Segmentdefinitionen ausgewertet und aktualisiert werden.
* **[Echtzeit-Kundenprofil](../profile/home.md)**: So werden Profildaten zusammengeführt und für die Segmentierung und Aktivierung bereitgestellt.
* **[Ziele](../destinations/home.md)**: Wo und wie Daten für nachgelagerte Systeme und Marketing-Plattformen aktiviert werden.

Wenn Sie diese Komponenten verstehen, können Sie Auftragsausführungsmuster interpretieren und Probleme diagnostizieren, wenn sie auftreten.

## Grundlagen zur Benutzeroberfläche für Aufgabenplanungen {#understanding-interface}

So greifen Sie auf [!UICONTROL Job Schedules] zu:

1. Wählen Sie in der Benutzeroberfläche von Experience Platform im linken Navigationsbereich die Option **[!UICONTROL Run and Operate]** .
2. Wählen Sie **[!UICONTROL Job Schedules]** aus.

Die Seite [!UICONTROL Job Schedules] bietet einen Überblick über alle geplanten Batch-Verarbeitungsaufträge.

![Linke Navigation ausführen und bedienen](assets/job-schedules/run-and-operate-left-nav.png)

### Zusammenfassungskarten {#summary-cards}

Oben auf der Seite sehen Sie Zusammenfassungskarten, die einen schnellen Einblick in Ihre Batch-Verarbeitungsaufträge bieten.

![Zusammenfassungskarten für Auftragsplanungen mit Einblicken in Batch-Verarbeitungsaufträge](assets/job-schedules/job-schedules-cards.png)

* **Lake-**: Die Anzahl der ausgeführten Data-Lake-Aufnahmevorgänge.
* **Profilaufnahme-**: Die Anzahl der ausgeführten Profilaufnahmevorgänge.
* **Nächste Segmentierung**: Wann der nächste geplante Segmentierungsauftrag ausgeführt wird.
* **Nächste Zielaktivierung**: Wann der nächste geplante Zielaktivierungsauftrag ausgeführt wird.

Diese Karten helfen Ihnen, die Aktivität und die bevorstehenden Zeitpläne in Ihrer gesamten Daten-Pipeline zu verstehen. Die Werte für **Lake-**- und **Profilaufnahme-Durchgänge** ändern sich basierend auf dem ausgewählten Zeitintervall (Heute, Gestern oder Letzte 7 Tage). Die Karten für die nächste Ausführung (**Nächste Segmentierung** und **Nächste Zielaktivierung**) sind von der Zeitauswahl nicht betroffen.

### Zeitraumauswahl {#time-period}

Verwenden Sie die Zeitraumauswahl, um festzulegen, wie weit die geplanten Aufträge in der Vergangenheit angezeigt werden sollen.

![Animiertes Beispiel der Benutzeroberfläche der Zeitraumauswahl in Auftragsplänen](assets/job-schedules/time-selector.gif)

* **Heute**: Für heute geplante Aufträge anzeigen (Standardansicht).
* **Gestern**: Zeigt Aufträge an, die gestern ausgeführt wurden.
* **Letzte 7 Tage**: Zeigt Aufträge der letzten Woche an.

### Details zu Batch-Vorgangszeitplänen {#job-schedules-details}

Die Hauptansicht zeigt an, wann die Ausführung Ihrer Batch-Vorgänge für den gesamten Tag geplant ist. Sie haben folgende Möglichkeiten:

* **Aufträge nach Datensatz oder Entität anzeigen**: Die linke Spalte zeigt die Namen von Datensätzen oder Verarbeitungsaufträgen (z. B. Aufnahme-Datensätze oder Segmentierungsvorgänge).
* **Siehe Auftrags-Timing**: Die Zeitleiste zeigt an, wann jeder Auftrag ausgeführt werden soll, wobei visuelle Indikatoren die geplante Zeit markieren.
* **Filteraufträge**: Verwenden Sie das Filtersymbol, um einzugrenzen, welche Datensätze in den Bericht aufgenommen werden sollen.
* **Vorgangsarten verstehen**: Die farbcodierte Legende unten hilft Ihnen bei der Identifizierung verschiedener Vorgangsarten:
   * **Lake-Aufnahme** (grün): Datenaufnahme in den Data Lake
   * **Profilaufnahme** (rosa): Datenaufnahme in den Profilspeicher
   * **Segmentierung** (hellblau): Aufträge zur Zielgruppenbewertung
   * **Profilexport** (blau): Export von Profildaten
   * **Activation** (dark grey): Zielaktivierungsaufträge
   * **In Bearbeitung** (gestreift): Aufträge, die derzeit ausgeführt werden oder sich in der Warteschlange befinden

Diese Zeitleistenansicht hilft Ihnen, Planungskonflikte zu identifizieren, Abhängigkeiten zwischen Aufträgen zu verstehen und Ihre Batch-Verarbeitungspläne zu optimieren.

## Ermitteln von Konfigurationsproblemen {#identifying-issues}

Wenn Sie Ihre Auftragspläne überprüfen, werden Sie möglicherweise Muster bemerken, die auf Konfigurationsprobleme hinweisen. Häufige Probleme sind:

* Vorgänge, die so geplant sind, dass sie sich schließen, was zu Ressourcenkonflikten führt
* Zu viele Batches im selben Zeitfenster
* Einzelne Datensätze mit übermäßigen täglichen Batch-Vorgängen
* unmittelbar vor Ausführung der Segmentierung geplante Aufnahmevorgänge

Diese Muster können zu Auftragsfehlern, unvollständiger Datenverarbeitung und schlechter Systemleistung führen. Informationen zum Identifizieren und Beheben dieser Probleme finden Sie in der Dokumentation unter [Identifizieren von Antimustern bei der Auftragsplanung](job-schedules-anti-patterns.md).

Wenn Sie bestimmte Datensätze oder Auftragsausführungen untersuchen müssen, können Sie einen Drilldown in detaillierte Ansichten durchführen, um den Ausführungsverlauf, Fehlermeldungen, Leistungsmetriken und Abhängigkeiten anzuzeigen. Informationen zum Anzeigen dieser detaillierten Daten finden Sie in der Dokumentation unter [Anzeigen von Auftragsdetails](job-schedules-details.md).

## Nächste Schritte {#next-steps}

Nachdem Sie sich mit Stellenplänen vertraut gemacht haben, sollten Sie sich mit diesen verwandten Themen beschäftigen:

* [Auftragsdetails anzeigen](job-schedules-details.md) Erfahren Sie, wie Sie einzelne Datensätze und Auftragsdurchgänge detailliert untersuchen können.
* [Identifizieren von Antimustern bei der Auftragsplanung](job-schedules-anti-patterns.md): Erfahren Sie, wie Sie häufige Konfigurationsprobleme, die sich auf die Pipeline-Leistung auswirken, erkennen und beheben können.
* [Batch-Aufnahme](../ingestion/batch-ingestion/overview.md): Erfahren Sie, wie Sie Daten mithilfe der Batch-Verarbeitung in Experience Platform aufnehmen.
* [Segmentierung](../segmentation/home.md): Verstehen Sie, wie Zielgruppen in terminierten Intervallen ausgewertet und aktualisiert werden.
* [Überwachen von Datenflüssen für Ziele](../dataflows/ui/monitor-destinations.md): Erfahren Sie, wie Sie Zielaktivierungs-Datenflüsse überwachen.
* [Planen von Zielgruppenexporten](../destinations/ui/activate-batch-profile-destinations.md): Erfahren Sie, wie Sie geplante Batch-Zielaktivierungen konfigurieren.
