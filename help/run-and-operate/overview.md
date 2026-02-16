---
title: Übersicht über Ausführung und Bedienung
description: Überprüfen, beheben und optimieren Sie Ihre Adobe Experience Platform-Implementierungen mit den Tools „Ausführen und Bedienen“. Gewinnen Sie Einblicke in geplante Batch-Aktivierungen, identifizieren Sie Konfigurationsprobleme und verbessern Sie die Systemzuverlässigkeit.
hide: true
source-git-commit: 436ce6843e96b76dac0595ff5ab8a6067fb521ea
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 1%

---


# Übersicht über Ausführung und Bedienung

>[!AVAILABILITY]
>
>Die Funktionen zum Ausführen und Betreiben sind derzeit nur in begrenztem Umfang verfügbar.

Wenn Batch-Vorgänge fehlschlagen oder unvollständige Daten bereitstellen, müssen Sie schnell verstehen, was das Problem verursacht hat. Die Ursache können Probleme mit der Datenverfügbarkeit, falsche Zeitplanung, Konfigurationsprobleme oder Einschränkungen der Systemkapazität sein. Ohne klare Sicht können Sie Stunden damit verbringen, mehrere Systeme zu untersuchen, bevor Sie die Antwort finden.

Mit [!UICONTROL Run and Operate] Tools können Sie:

* **Datenvorgänge überprüfen**: Verschaffen Sie sich einen vollständigen Überblick über den Auftragsausführungsstatus und den Status aller Ihrer Workflows.
* **Schnellere Fehlerbehebung**: Greifen Sie auf detaillierte Diagnoseinformationen und den Ausführungsverlauf zu, um die Grundursachen schnell zu identifizieren und die durchschnittliche Zeit bis zur Behebung zu verkürzen.
* **Probleme proaktiv verhindern**: Analysieren Sie Vorgangsmuster, erkennen Sie Konfigurationsprobleme, bevor sie zu Fehlern führen, und optimieren Sie Ihre Datenvorgänge.

## Zielgruppen {#target-audiences}

[!UICONTROL Run and Operate] Tools sind für mehrere Zielgruppen in Ihrem Unternehmen konzipiert:

* **Daten- und IT-**: Systemadministratoren und Dateningenieure, die zuverlässige Datenpipelines verwalten und technische Probleme beheben.
* **Marketing-Vorgänge**: Marketing-Techniker, die die Datenbereitstellung an Marketing-Plattformen überprüfen und Aktivierungsprobleme beheben.
* **Implementierer**: Anwender, die die Implementierungseffizienz, Zuverlässigkeit und Fehlerbehebung bei technischen Problemen validieren.

## Voraussetzungen {#prerequisites}

Für den Zugriff auf die Ausführung und den Betrieb von Tools benötigen Sie die **[!UICONTROL View Job Schedules]** und **[!UICONTROL View Profile Management]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
Die Seite [!UICONTROL Job Schedules] bietet einen Überblick über alle geplanten Batch-Verarbeitungsaufträge.
Wenden Sie sich an Ihren Systemadministrator, um sicherzustellen, dass Sie über die entsprechenden Berechtigungen verfügen.

## Erste Schritte {#getting-started}

So greifen Sie über die Experience Platform-Benutzeroberfläche auf die Tools Ausführen und Bedienen zu:

1. Melden Sie sich bei Ihrem Experience Platform-Konto an und wählen Sie im linken Navigationsbereich **[!UICONTROL Run and Operate]** aus.
2. Wählen Sie das Tool aus, das Ihren Prüf- oder Fehlerbehebungsanforderungen entspricht.

   >[!NOTE]
   >
   >Derzeit ist nur die Funktion &quot;[&quot; &#x200B;](job-schedules.md).

![Experience Platform-Benutzeroberfläche mit der Option „Ausführen“ und „Linke Bedienung“.](assets/overview/run-and-operate.png)

## Verfügbare Tools {#available-tools}

Mit den folgenden Tools können Sie Ihre Datenvorgänge überprüfen und optimieren.

### Auftragszeitpläne {#job-schedules}

>[!IMPORTANT]
>
>[!UICONTROL Job schedules] sind derzeit nur für die folgenden Real-Time CDP-Aufträge verfügbar:
>
> * Batch-Data-Lake-Aufnahme
> * Batch-Profilaufnahme
> * Stapelsegmentierung
> * Batch-Zielaktivierung.

Mit [Vorgangszeitplänen](job-schedules.md) können Sie alle geplanten Batch-Vorgänge in Ihrem Unternehmen pro Sandbox überprüfen, einschließlich Data Lake-Aufnahme, Profilaufnahme, Segmentierung und Zielaktivierung. Zeigen Sie den Auftragsausführungsstatus, Leistungsmetriken und den Ausführungsverlauf an, um Muster zu identifizieren und Konfigurationsprobleme zu diagnostizieren, die die Zuverlässigkeit beeinträchtigen.

![Benutzeroberfläche von Experience Platform mit dem Bildschirm „Auftragszeitpläne“.](assets/overview/job-schedules-interface.png)

Job Schedules bietet drei Ermittlungsebenen:

* **[Prüfen von Vorgangszeitplänen](job-schedules.md)**: Zeigen Sie alle Datensätze und ihre geplanten Vorgänge in einer Zeitleiste an, um Muster und Planungskonflikte in der gesamten Pipeline zu identifizieren.
* **[Ermitteln von Anti-Mustern](job-schedules-anti-patterns.md)**: Erfahren Sie, wie Sie häufige Konfigurationsprobleme wie Zeitplanüberschneidungen, dichtes Batch-Stacking und übermäßiges Batch-Management erkennen und beheben können, die sich auf die Leistung auswirken.
* **[Auftragsdetails anzeigen](job-schedules-details.md)**: Drilldown in bestimmte Datensätze und einzelne Auftragsausführungen, um Fehler zu untersuchen, den Zeitpunkt zu überprüfen und verarbeitete Datensätze zu überprüfen.

Sie können auch die Abhängigkeiten zwischen den einzelnen Datenverarbeitungsstufen verstehen und so einen zuverlässigen Datenfluss in Ihren Experience Platform-Workflows sicherstellen.

## Nächste Schritte {#next-steps}

Nachdem Sie nun den Zweck und die Funktionen [!UICONTROL Run and Operate] Tools kennen, erkunden Sie die folgenden Ressourcen, um Ihr Wissen zu vertiefen:

* Erfahren Sie mehr über [Batch-Aufnahme](../ingestion/batch-ingestion/overview.md) um zu verstehen, wie Daten in Experience Platform aufgenommen werden
* Erfahren Sie, wie [&#x200B; Auftragspläne für &#x200B;](job-schedules.md) Batch-Aufnahme und -Aktivierungen prüfen
* Erfahren Sie, wie [geplante Aktivierungen](../destinations/ui/activate-batch-profile-destinations.md) für Batch-Ziele konfigurieren
* Erkunden Sie [Datenflussüberwachung](../dataflows/ui/monitor-destinations.md) für Ziele

