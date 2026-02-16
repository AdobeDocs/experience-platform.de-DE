---
description: Erfahren Sie, wie Sie detaillierte Informationen zu Datensätzen und einzelnen Auftragsausführungen in Auftragsplänen anzeigen können.
solution: Experience Platform
title: Details zur Auftragsplanung anzeigen
type: Tutorial
hide: true
source-git-commit: 436ce6843e96b76dac0595ff5ab8a6067fb521ea
workflow-type: tm+mt
source-wordcount: '1783'
ht-degree: 1%

---


# Details zur Auftragsplanung anzeigen

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules] sind derzeit als eingeschränkte Version verfügbar und nur für die folgenden Real-Time CDP-Aufträge:
>
> * Batch-Data-Lake-Aufnahme
> * Batch-Profilaufnahme
> * Stapelsegmentierung
> * Batch-Zielaktivierung.

Bei der Fehlerbehebung bei Auftragsfehlern oder der Untersuchung von Leistungsproblemen benötigen Sie detaillierte Informationen zu bestimmten Datensätzen und deren Vorgangsausführungen. Die [Vorgangszeitpläne](job-schedules.md) ermöglicht es Ihnen, einen Drilldown von der Zeitleisten -Ansicht nach einzelnen Datensätzen und Vorgängen durchzuführen, um Ausführungsverlauf, Timing und Status zu verstehen.

Verwenden Sie diese Detailansicht für Folgendes:

* Untersuchen, warum ein bestimmter Auftrag fehlgeschlagen ist oder länger als erwartet dauerte
* Überprüfen des Ausführungsverlaufs für einen Datensatz im Zeitverlauf
* Verstehen Sie die Zeitsteuerungs- und Dauermuster von Batch-Vorgängen
* Identifizieren Sie, welche spezifischen Batches Pipeline-Probleme verursachen
* Sammeln von Informationen zur Fehlerbehebung beim Adobe-Support

## Voraussetzungen {#prerequisites}

Bevor Sie Auftragsdetails anzeigen, sollten Sie Folgendes tun:

* Zugriff auf [!UICONTROL Job Schedules] mit den **[!UICONTROL View Job Schedules]** und **[!UICONTROL View Profile Management]**&#x200B;[&#x200B; Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
* Machen Sie sich mit der [Benutzeroberfläche für Auftragspläne](job-schedules.md#understanding-interface) und der Zeitleistenansicht vertraut.
* Machen Sie sich mit den verschiedenen [Vorgangstypen](job-schedules.md#job-schedules-details) (Seeaufnahme, Profilaufnahme, Segmentierung, Aktivierung) vertraut.

## Grundlagen zur Detailhierarchie {#details-hierarchy}

Auftragspläne bieten drei Detailebenen, mit denen Sie von allgemeinen Mustern zu bestimmten Problemen wechseln können:

| Ansichtsebene | Was angezeigt wird | Einsatz |
|------------|---------------|----------------|
| **Zeitleisten-Ansicht** | Alle Datensätze und ihre geplanten Aufträge über den ausgewählten Zeitraum | Ermitteln von Mustern, Erkennen [Anti-Mustern](job-schedules-anti-patterns.md) und Abrufen eines Überblicks über die gesamte Pipeline |
| **Datensatzdetails** | Aggregierte Metriken und Ausführungsverlauf für einen einzelnen Datensatz | Verfolgen der Gesamtleistung eines Datensatzes, Verstehen des Datenvolumens und Überprüfen der Vorgangsfrequenz |
| **Auftragsausführungsdetails** | Spezifische Ausführungsinformationen für einen einzelnen Auftragsdurchgang | Untersuchung, warum ein bestimmter Auftrag fehlgeschlagen ist, Überprüfung des genauen Zeitplans und Überprüfung der verarbeiteten Datensätze |

**Navigationsfluss**: Beginnen Sie mit der Zeitleisten -Ansicht, um Probleme zu identifizieren, → wählen Sie einen Datensatz aus, um dessen Details anzuzeigen, → wählen Sie einen bestimmten Auftragsdurchgang aus, um die Details zu untersuchen.

### Grundlegendes zur Zeitleisten-Ansicht {#timeline-visualization}

Die Zeitleisten -Ansicht verwendet ein horizontales und vertikales Layout, das Ihnen hilft, Auftragspläne und kritische Verarbeitungszeiten zu verstehen:

* **Horizontale Achse (Zeitverlauf)**: Datensätze und ihre Vorgangsausführungen werden über die Zeitleiste von links nach rechts angezeigt und zeigen an, wann Vorgänge über den ausgewählten Zeitraum ausgeführt werden (heute, gestern oder letzte 7 Tage). Jeder farbige Balken stellt eine Auftragsausführung dar, die entsprechend ihrer Start- und Endzeit horizontal positioniert wird.

* **Vertikale Achse (geplante Startzeiten)**: Kritische geplante Startzeiten werden als vertikale Linien angezeigt, die sich über alle Datensätze erstrecken und die Anzeige der zeitlichen Beziehung zwischen Upstream-Aufträgen und Downstream-Verarbeitung erleichtern:
   * **Blaue vertikale Linie**: Stellt dar, wann die Segmentierung beginnen soll
   * **Schwarze vertikale Linie**: Stellt dar, wann die Zielaktivierung beginnen soll

Mit diesem Layout können Sie schnell Timing-Beziehungen zwischen Ihren Datenpipeline-Aufträgen und der nachgelagerten Verarbeitung identifizieren. Idealerweise sollten Upstream-Aufträge (wie Data Lake und Profilaufnahme) links neben diesen vertikalen Markern abgeschlossen werden, um sicherzustellen, dass die Daten bereit sind, bevor die Segmentierung und Aktivierung beginnt. Aufträge, die über diese Marker hinausgehen, weisen auf potenzielle Zeitplanprobleme hin, bei denen nachgelagerte Prozesse beginnen können, bevor die Daten vollständig vorbereitet sind.

### Welche Ansicht sollte ich verwenden? {#which-view}

Verwenden Sie die nachstehende Tabelle, um die richtige Ansicht für Ihre Aufgabe auszuwählen. Stimmen Sie mit der empfohlenen Ansicht überein, was Sie tun müssen, um effizient zu navigieren.

| Ich muss… | Diese Ansicht verwenden |
|--------------|---------------|
| Alle meine profilaktivierten Datensätze und ihre Zeitpläne gleichzeitig anzeigen | [Zeitleisten-Ansicht](job-schedules.md) |
| Identifizieren von Planungskonflikten oder Anti-Muster | [Zeitleisten-Ansicht](job-schedules.md) |
| Nachverfolgen der Gesamtleistung eines Datensatzes | [Datensatzdetails](#view-dataset-details) |
| Anzeigen der Gesamtzahl der von einem Datensatz verarbeiteten Datensätze | [Datensatzdetails](#view-dataset-details) |
| Vergleichen der Auftragsleistung für einen Datensatz im Zeitverlauf | [Datensatzdetails](#view-dataset-details) |
| Untersuchen, warum ein bestimmter Auftrag fehlgeschlagen ist | [Auftragsausführungsdetails](#view-job-details) |
| Überprüfen des genauen Ausführungszeitpunkts eines bestimmten Auftrags | [Auftragsausführungsdetails](#view-job-details) |
| In einem Durchgang verarbeitete Datensätze überprüfen | [Auftragsausführungsdetails](#view-job-details) |
| Zugriff auf detaillierte Fehlermeldungen | [Auftragsausführungsdetails](#view-job-details) → Datenflussausführungs-ID auswählen |

## Details des Datensatzes anzeigen {#view-dataset-details}

So zeigen Sie Details für einen bestimmten Datensatz an:

1. Suchen Sie in der **[!UICONTROL Job Schedules]** Zeitleisten -Ansicht den Datensatz, den Sie untersuchen möchten.
2. Wählen Sie den Datensatznamen aus der linken Spalte aus.

Die Ansicht mit den Datensatzdetails wird in einem rechten Bedienfeld geöffnet, in dem Informationen zu allen mit diesem Datensatz verknüpften Aufträgen angezeigt werden.

![Bedienfeld mit Datensatzdetails mit aggregierten Metriken zur See- und Profilaufnahme für einen ausgewählten Datensatz.](assets/job-schedules/view-dataset-details.png)

Im Bedienfeld Datensatzdetails werden der Datensatzname, die ID und die auftragsspezifischen Metriken nach Auftragstyp geordnet angezeigt. Oben im Bedienfeld wird die Datensatz-ID als anklickbarer Link angezeigt. Wählen Sie diese ID aus, um zur Seite mit den vollständigen Datensatzdetails zu navigieren.

Jedes Bedienfeld mit Datensatzdetails enthält die folgenden Metriken:

### Lake-Aufnahmemetriken {#lake-ingestion-metrics}

Für Datensätze mit Data-Lake-Aufnahmevorgängen zeigt das Bedienfeld die folgenden Metriken an:

| Metrik | Beschreibung | Verwenden von für |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | Die Gesamtzahl der Data-Lake-Aufnahmeaufträge, die für diesen Datensatz abgeschlossen wurden | Aktivitäts-Tracking |
| **[!UICONTROL Runs in progress]** | Wie viele Seeaufnahmevorgänge derzeit ausgeführt werden | Engpasserkennung |
| **[!UICONTROL Total records added]** | Die kumulative Anzahl neuer Datensätze, die dem Data Lake über alle Auftragsdurchgänge hinweg hinzugefügt wurden | Lautstärkeüberwachung |
| **[!UICONTROL Total ingestion time]** | Die kombinierte Dauer aller Data-Lake-Aufnahmevorgänge | Bewertung der Verarbeitungszeit |
| **[!UICONTROL Total records updated]** | Die kumulative Anzahl der vorhandenen Datensätze, die während der Aufnahme aktualisiert wurden | Musteranalyse aktualisieren |
| **[!UICONTROL Avg. ingestion speed (records/second)]** | Die durchschnittliche Durchsatzrate für Data-Lake-Aufnahmeaufträge | Leistungsvergleich |

### Metriken zur Aufnahme von Profilen {#profile-ingestion-metrics}

Für Datensätze mit Profilaufnahmevorgängen zeigt das Bedienfeld die folgenden Metriken:

| Metrik | Beschreibung | Verwenden von für |
|--------|-------------|---------|
| **[!UICONTROL Total runs]** | Die Gesamtzahl der Profilaufnahmevorgänge, die für diesen Datensatz abgeschlossen wurden | Aktivitäts-Tracking |
| **[!UICONTROL Runs in progress]** | Wie viele Profilaufnahmevorgänge derzeit ausgeführt werden | Verzögerungserkennung |
| **[!UICONTROL Total profiles created]** | Die kumulative Anzahl neuer Profile, die aus diesem Datensatz für alle Auftragsausführungen erstellt wurden | Überwachung des Profilwachstums |
| **[!UICONTROL Total profile ingestion time]** | Die kombinierte Dauer aller Profilaufnahmevorgänge | Identifizierung des zeitgesteuerten Problems |
| **[!UICONTROL Total profiles updated]** | Die kumulative Anzahl der vorhandenen Profile, die mit Daten aus diesem Datensatz aktualisiert wurden | Tracking der Aktualisierungshäufigkeit |
| **[!UICONTROL Avg. profile ingestion speed (profiles/second)]** | Die durchschnittliche Durchsatzrate für Profilaufnahmevorgänge | Überwachen der Performance |

>[!NOTE]
>
> Diese Metriken zeigen kumulative Summen für alle Auftragsausführungen für diesen Datensatz an. Um Details zu einer bestimmten Ausführung anzuzeigen, wählen Sie einen Auftrag direkt in der Zeitleiste aus.

## Datensätze in der Zeitleiste filtern {#filter-datasets}

Wenn Sie über viele Datensätze mit geplanten Aufträgen verfügen, sollten Sie sich auf bestimmte Datensätze konzentrieren, anstatt sie alle gleichzeitig anzuzeigen. Mit dem Datensatzfilter können Sie auswählen, welche Datensätze in der Zeitleisten-Ansicht angezeigt werden.

![Das Bedienfeld „Datensatzfilter“, in dem Sie auswählen können, welche Datensätze in der Zeitleisten-Ansicht angezeigt werden.](assets/job-schedules/view-datasets.gif)

So filtern Sie die in der Zeitleiste angezeigten Datensätze:

1. Suchen Sie in der Zeitleisten -Ansicht oben links nach dem Datensatzzähler (z. B. „2 Datensätze„).
2. Wählen Sie das Filtersymbol neben dem Datensatzzähler aus.
3. Ein Bedienfeld zur Datensatzauswahl wird geöffnet, in dem alle verfügbaren profilaktivierten Datensätze mit geplanten Aufträgen angezeigt werden.
4. Datensätze auswählen oder die Auswahl aufheben, um sie in der Zeitleisten -Ansicht ein- oder auszublenden.
5. Die Zeitleiste wird sofort aktualisiert und zeigt nur die ausgewählten Datensätze an.

Verwenden Sie die Filterung für:

* **Konzentration auf bestimmte Datenquellen**: Wenn Sie Probleme mit einer bestimmten Datenpipeline beheben, filtern Sie so, dass nur die relevanten Datensätze angezeigt werden.
* **Geringeres visuelles**: Wenn Sie viele Datensätze haben, können Sie durch Filtern die Muster für eine Untergruppe von Daten besser erkennen.
* **Verwandte Datensätze vergleichen**: Wählen Sie nur Datensätze aus, die miteinander verknüpft sind, um ihre Zeitplanbeziehung zu verstehen.
* **Untersuchen Sie Anti-Muster**: Wenn Sie ein potenzielles [Konfigurationsproblem](job-schedules-anti-patterns.md) identifizieren, filtern Sie nach den betroffenen Datensätzen, um sie genauer zu untersuchen.

Der Filter bleibt während Ihrer Sitzung bestehen, sodass Sie unter Beibehaltung Ihrer Datensatzauswahl zwischen Zeiträumen (heute, gestern, letzte 7 Tage) navigieren können.

## Anzeigen der Details einzelner Auftragsausführungen {#view-job-details}

Wenn Sie einen bestimmten Auftragsdurchgang untersuchen müssen, wählen Sie ihn aus der Zeitleiste aus, um detaillierte Ausführungsinformationen für diesen bestimmten Durchgang anzuzeigen.

### Zugriff auf Auftragsausführungsdetails {#access-job-details}

So zeigen Sie Details für eine bestimmte Auftragsausführung an:

1. Suchen Sie in der Ansicht „Zeitleiste [!UICONTROL Job Schedules]&quot; den spezifischen Auftragsdurchgang, den Sie untersuchen möchten.
2. Wählen Sie die Auftragsanzeige in der Zeitleiste aus (der farbige Balken, der den Auftrag darstellt).

Das Bedienfeld **[!UICONTROL Dataflow run details]** wird geöffnet und zeigt Informationen zur Ausführung des jeweiligen Auftrags an.

![Das Bedienfeld mit den Details zur Datenflussausführung, das Ausführungsinformationen für eine bestimmte Auftragsausführung anzeigt.](assets/job-schedules/job-details.png)

### Details zur Datenflussausführung {#dataflow-run-details}

Das Bedienfeld mit den Details der Datenflussausführung zeigt Informationen über die spezifische Auftragsausführung an, sortiert nach Auftragstyp. Bei Aufnahmevorgängen werden Details für die Aufnahme in den See und die Profilaufnahme angezeigt.

#### Details zum Lake-Aufnahmeauftrag {#lake-ingestion-job-details}

| Feld | Beschreibung |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | Die eindeutige Kennung für diesen spezifischen Lake-Aufnahmevorgang. Wählen Sie die ID aus, um vollständige Details zur Datenflussüberwachung anzuzeigen. |
| **[!UICONTROL Run status]** | Das Ergebnis des Vorgangs (Erfolg, Fehlgeschlagen, In Bearbeitung, In Warteschlange). Ein grüner Indikator zeigt den erfolgreichen Abschluss an. |
| **[!UICONTROL Started at]** | Das Datum und die Uhrzeit, zu der der Lake-Aufnahmevorgang gestartet wurde. |
| **[!UICONTROL Completed at]** | Datum und die Uhrzeit, zu der der Lake-Aufnahmevorgang abgeschlossen wurde. |
| **[!UICONTROL Records added]** | Die Anzahl der neuen Datensätze, die während dieser Auftragsausführung zum Data Lake hinzugefügt wurden. |
| **[!UICONTROL Records updated]** | Die Anzahl der vorhandenen Datensätze, die während dieser Auftragsausführung im Data Lake aktualisiert wurden. |

#### Details zum Profilaufnahmevorgang {#profile-ingestion-job-details}

| Feld | Beschreibung |
|-------|-------------|
| **[!UICONTROL Dataflow run ID]** | Die eindeutige Kennung für diesen spezifischen Profilaufnahmevorgang. Wählen Sie die ID aus, um vollständige Details zur Datenflussüberwachung anzuzeigen. |
| **[!UICONTROL Run status]** | Das Ergebnis des Vorgangs (Erfolg, Fehlgeschlagen, In Bearbeitung, In Warteschlange). Ein grüner Indikator zeigt den erfolgreichen Abschluss an. |
| **[!UICONTROL Started at]** | Das Datum und die Uhrzeit, zu der bzw. zu der die Ausführung des Profilaufnahmevorgangs begonnen hat. |
| **[!UICONTROL Completed at]** | Das Datum und die Uhrzeit, zu der bzw. zu der der Profilaufnahmevorgang abgeschlossen wurde. |
| **[!UICONTROL Records added]** | Die Anzahl der neuen Profile, die während dieser Auftragsausführung erstellt wurden. |
| **[!UICONTROL Records updated]** | Die Anzahl der vorhandenen Profile, die während dieser Auftragsausführung aktualisiert wurden. |

### Grundlegendes zum Auftragsausführungsfluss {#job-execution-flow}

Beim Anzeigen eines bestimmten Auftragsdurchgangs können Sie die Beziehung zwischen der Lake-Aufnahme und der Profilaufnahme sehen:

* **Lake-Aufnahme wird zuerst ausgeführt**: Daten werden in den Data Lake geladen und validiert.
* **Profilaufnahme folgt**: Nach Abschluss der Seeaufnahme werden geeignete Datensätze in den Profilspeicher verarbeitet.
* **Der Zeitpunkt ist wichtig** Beachten Sie den Zeitunterschied zwischen dem Abschluss der Seeaufnahme und dem Beginn der Profilaufnahme. Lücken können sich auf nachgelagerte Prozesse wie die Segmentierung auswirken.

**Verwenden Sie Auftragsausführungsdetails für**:

* Überprüfen, ob ein bestimmter Auftrag erfolgreich abgeschlossen wurde
* Berechnen der tatsächlichen Dauer eines Auftragsdurchgangs (Abschlusszeit abzüglich Startzeit)
* Verstehen, wie viele Datensätze in einer bestimmten Ausführung verarbeitet wurden
* Leistung über verschiedene Auftragsausführungen hinweg vergleichen
* Zugriff auf eine detaillierte Datenflussüberwachung zur Fehlerbehebung
* Identifizieren von Zeitsteuerungsproblemen zwischen Lake- und Profilaufnahmephasen

## Fehlerbehebung bei Auftragsdetails {#troubleshooting}

Verwenden Sie Auftragsdetails, um Probleme zu untersuchen und die nächsten Schritte zu bestimmen:

**Fehlgeschlagene Aufträge**: Wählen Sie die ID der Datenflussausführung aus, um Fehlerdetails im Monitoring-Dashboard anzuzeigen. Überprüfen Sie [Datensatzdetails](#view-dataset-details) auf wiederkehrende Muster, überprüfen Sie die [Timeline](job-schedules.md) auf Ressourcenkonflikte und identifizieren Sie [Anti-Muster](job-schedules-anti-patterns.md) in Ihrer Konfiguration.

**Langsame Aufträge**: Vergleichen der Dauer mit historischen Durchschnittswerten in [Datensatzmetriken](#view-dataset-details). Häufige Ursachen sind [Planüberschneidung](job-schedules-anti-patterns.md#schedule-overlap-pattern), [dichtes Batch-Stacking](job-schedules-anti-patterns.md#scheduled-density) oder erhöhtes Datenvolumen.

**Nicht übereinstimmende Datensätze**: In den Auftragsausführungsdetails können Sie die Aufnahmedatensätze des Sees mit den Profilaufnahmedatensätzen vergleichen. Die Profilaufnahme zeigt aufgrund von Identitätsanforderungen und Datenqualitätsregeln normalerweise weniger Datensätze an.

Detaillierte Datenflussstatusinformationen finden Sie unter [Überwachen der Data Lake](../dataflows/ui/monitor-sources.md), [Überwachen von Datenflüssen für Profile](../dataflows/ui/monitor-profiles.md), [Überwachen von Datenflüssen für Zielgruppen](../dataflows/ui/monitor-audiences.md) und [Überwachen von Datenflüssen für Ziele](../dataflows/ui/monitor-destinations.md).

## Nächste Schritte {#next-steps}

Nachdem Sie gelernt haben, wie Sie Auftragsdetails anzeigen:

* Lesen Sie [Übersicht über Auftragspläne](job-schedules.md) um die Ansicht und Benutzeroberfläche der Zeitleiste besser zu verstehen.
* Erfahren Sie mehr über [Anti-Muster](job-schedules-anti-patterns.md) um häufige Konfigurationsprobleme zu vermeiden.
* Grundlegendes [zur Batch-Aufnahme](../ingestion/batch-ingestion/overview.md), um Ihre Datenladepläne zu optimieren.
* Erkunden Sie [Überwachen von Zieldatenflüssen](../dataflows/ui/monitor-destinations.md) um die End-to-End-Pipeline-Sichtbarkeit zu ermitteln.
