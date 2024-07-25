---
description: Erfahren Sie, wie Sie Datenflüsse während der Segmentierung mithilfe der Experience Platform-Benutzeroberfläche überwachen können.
title: Überwachen von Datenflüssen für Zielgruppen in der Benutzeroberfläche
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 7%

---

# Überwachen von Datenflüssen für Zielgruppen in der Benutzeroberfläche

Mit dem Segmentation Service können Sie Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile] -Daten erstellen. Platform bietet Datenflüsse zur transparenten Verfolgung dieses Datenflusses von Quellen zu Zielen.

Verwenden Sie das Monitoring-Dashboard, um eine visuelle Darstellung der Datenaktivität in einer Zielgruppe anzuzeigen, einschließlich des Status der Segmentierung Ihrer Daten. In diesem Tutorial erfahren Sie, wie Sie mit dem Monitoring-Dashboard die Segmentierung Ihrer Daten mithilfe der Experience Platform-Benutzeroberfläche überwachen können. So können Sie den Status von Zielgruppenaktivierungs-, Bewertungs- und Exportvorgängen verfolgen.

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   - [Datenfluss-Ausführungen](../../sources/notifications.md): Datenfluss-Ausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Frequenzkonfiguration ausgewählter Datenflüsse basieren.
- [Segmentierung](../../segmentation/home.md): Mit der Segmentierung können Sie Zielgruppen aus Ihren Echtzeit-Kundenprofildaten erstellen.
   - [Aktivierungsaufträge](../../destinations/ui/activation-overview.md): Mit einem Aktivierungsauftrag wird Ihre Zielgruppe für ein bestimmtes Ziel aktiviert.
   - [Auswertungsaufträge](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): Ein Auswertungsauftrag ist ein asynchroner Prozess, der die Zielgruppe auswertet.
   - [Exportaufträge](../../segmentation/api/export-jobs.md): Ein Exportauftrag ist ein asynchroner Vorgang, der verwendet wird, um Zielgruppenmitglieder in Datensätzen zu erhalten.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

## Dashboard zur Überwachung von Zielgruppen {#monitoring-audiences-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Zielgruppen"
>abstract="Die Zielgruppenansicht enthält Informationen zu allen Zielgruppen Ihrer Organisation sowie zu ihren Aktivierungs- und Evaluierungsvorgängen."

Um auf das Dashboard **[!UICONTROL Zielgruppen]** zuzugreifen, wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Überwachung]** aus. Wählen Sie auf der Seite **[!UICONTROL Überwachung]** die Karte **[!UICONTROL Zielgruppen]** aus.

![Die Karte Zielgruppen . Informationen zum letzten Bewertungsauftrag und zum letzten Exportauftrag werden angezeigt.](../assets/ui/monitor-audiences/audience-card.png)

Im Haupt-Dashboard **[!UICONTROL Zielgruppen]** zeigt die Karte **[!UICONTROL Zielgruppen]** den Status und das Datum des letzten Auswertungsauftrags sowie den letzten Exportauftrag an.

Das Dashboard selbst enthält Metriken für Zielgruppen und Segmentierungsaufträge. Standardmäßig zeigt das Dashboard die Zielgruppenmetriken für die letzten 24 Stunden an. Weitere Informationen zur Ansicht der Segmentierungsaufträge finden Sie im Abschnitt [Überwachungssegmentierungsaufträge](#monitoring-segmentation-jobs-dashboard) .

>[!IMPORTANT]
>
>Derzeit werden für das Dashboard der Überwachungszielgruppen nur Zielgruppen unterstützt, die für [Batch-(dateibasierte) Ziele](../../destinations/destination-types.md#file-based) aktiviert sind.

![Das Zielgruppen-Dashboard. Informationen zu den verschiedenen Zielgruppen in Ihrer Organisation und Sandbox werden angezeigt.](../assets/ui/monitor-audiences/audience-dashboard.png)

Für diese Dashboard-Ansicht stehen die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Zielgruppenname]** | Der Name der Zielgruppe. |
| **[!UICONTROL Datentyp]** | Der Datentyp der Audience. Mögliche Werte sind **[!UICONTROL Kunde]**, **[!UICONTROL Konto]** und **[!UICONTROL Interessent]**. Mithilfe des Filters [!UICONTROL Datentyp] über dem Kartenband können Sie Audiences eines bestimmten Datentyps anzeigen. |
| **[!UICONTROL Letzter Bewertungszeitstempel]** | Datum und Uhrzeit der letzten Ausführung des Audience-Auswertungsauftrags. |
| **[!UICONTROL Letzter Bewertungsstatus]** | Der Status des letzten Auswertungsauftrags der Zielgruppe. Mögliche Werte sind **[!UICONTROL Erfolg]**, **[!UICONTROL Keine Ausführungen]** und **[!UICONTROL Fehlgeschlagen]**. |
| **[!UICONTROL Letzte Auswertungsmethode]** | Die Auswertungsmethode der Audience. Da nur die Batch-Segmentierung unterstützt wird, ist der einzig mögliche Wert **[!UICONTROL Batch]**. |
| **[!UICONTROL Letzte Testprofile]** | Die Anzahl der Profile, die im letzten Auswertungsauftrag der Zielgruppe ausgewertet wurden. |
| **[!UICONTROL Letzter Aktivierungszeitstempel]** | Datum und Uhrzeit der letzten Ausführung des Aktivierungsauftrags der Zielgruppe. |
| **[!UICONTROL Letzter Aktivierungsstatus]** | Der Status des letzten Aktivierungsauftrags der Zielgruppe. Mögliche Werte sind **[!UICONTROL Erfolg]**, **[!UICONTROL Keine Ausführungen]** und **[!UICONTROL Fehlgeschlagen]**. |
| **[!UICONTROL Letzte Aktivierungsidentitäten]** | Die Anzahl der Identitäten, die im letzten Aktivierungsauftrag der Zielgruppe aktiviert wurden. |
| **[!UICONTROL Letztes Aktivierungsziel]** | Der Name des Ziels, für das der letzte Aktivierungsauftrag der Zielgruppe aktiviert wurde. |

Sie können die Ergebnisse nach einer bestimmten Zielgruppe filtern und die zugehörigen Segmentierungsaufträge anzeigen, indem Sie das Filtersymbol (![Filtersymbol) auswählen.](/help/images/icons/filter-add.png)). Die Segmentierungsaufträge werden in chronologischer Reihenfolge sortiert, wobei die neuesten Segmentierungsaufträge zuerst angezeigt werden.

![Das Filtersymbol wird hervorgehoben. Wenn Sie diese Option auswählen, können Sie die Segmentierungsaufträge für die angegebene Zielgruppe anzeigen.](../assets/ui/monitor-audiences/filter-audience.png)

Das Dashboard der gefilterten Zielgruppe wird angezeigt. Auf der Karte **[!UICONTROL Zielgruppen]** werden der Status und das Datum des letzten Bewertungsauftrags sowie der letzte Aktivierungsauftrag angezeigt.

![Die Karte Zielgruppen . Informationen zum letzten Bewertungsauftrag und zum letzten Aktivierungsauftrag werden angezeigt.](../assets/ui/monitor-audiences/specified-audience-card.png)

Das Dashboard selbst zeigt die Zeit und den Status der letzten Evaluierungs- und Aktivierungsaufträge, ein Diagramm mit der Profilanzahl der Zielgruppenbewertung und Metriken für die ausgeführten Segmentierungsaufträge an. Standardmäßig zeigt das Dashboard Metriken für Segmentierungsaufträge für die letzten 24 Stunden an.

![Das gefilterte Zielgruppen-Dashboard. Informationen zu den verschiedenen Segmentierungsaufträgen, die für diese Zielgruppe ausgeführt wurden, werden angezeigt.](../assets/ui/monitor-audiences/filter-audience.png)

Für diese Dashboard-Ansicht stehen die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Auftragsstart]** | Datum und Uhrzeit des Starts des Segmentierungsauftrags. |
| **[!UICONTROL Typ]** | Gibt den Typ des Segmentierungsauftrags an. Die beiden unterstützten Auftragstypen sind **Aktivierung** und **Auswertung**. |
| **[!UICONTROL Auftrag abgeschlossen]** | Datum und Uhrzeit des Abschlusses des Segmentierungsauftrags. |
| **[!UICONTROL Verarbeitungszeit]** | Die Zeit, die der Abschluss des Segmentierungsauftrags gedauert hat. |
| **[!UICONTROL Auftragsstatus]** | Der Status des Segmentierungsauftrags. Zu den unterstützten Werten gehören **[!UICONTROL Erfolg]**, **[!UICONTROL Wird ausgeführt]** und **[!UICONTROL Fehlgeschlagen]**. |
| **[!UICONTROL Anzahl der Profile]** | Die Anzahl der Profile, die der Segmentierungsauftrag auswertet. Jeder Benutzer sollte über ein eindeutiges Profil verfügen. |
| **[!UICONTROL Identität aktiviert]** | Die Anzahl der Identitäten, die der Segmentierungsauftrag aktiviert. Jedes Profil kann mehrere Identitäten aufweisen. Beispielsweise könnte ein Profil eine E-Mail-, Telefonnummer- und Treuenummer als Identitäten haben. |
| **[!UICONTROL Zielname]** | Der Name des Ziels, für das der Segmentierungsauftrag aktiviert wird. |

Sie können einen bestimmten Segmentierungsauftrag weiter filtern und dessen Details anzeigen, indem Sie das Filtersymbol (![Filtersymbol) auswählen.](/help/images/icons/filter.png)). Es gibt zwei verschiedene Arten von Segmentierungsaufträgen, die gefiltert werden können: Aktivierungsaufträge und Auswertungsaufträge.

### Details zum Aktivierungsauftrag {#activation-job-details}

Auf der Seite mit den Ausführungsdetails des Aktivierungsauftrags werden Informationen zu den Metriken der Ausführung, den Ausführungsfehlern des Datenflusses und den Zielgruppen angezeigt, die mit dem Segmentierungsauftrag zusammenhängen. Ein Aktivierungsauftrag wird verwendet, um Ihre Zielgruppe für ein bestimmtes Ziel zu aktivieren.

![Das Dashboard des Aktivierungsauftrags. Informationen zu den verschiedenen Segmentierungsaufträgen, die für diese Zielgruppe ausgeführt wurden, werden angezeigt.](../assets/ui/monitor-audiences/activation-job-dashboard.png)

Für diese Dashboard-Ansicht stehen die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL empfangenen Profile]** | Die Gesamtzahl der im Aktivierungsfluss empfangenen Profile. |
| **[!UICONTROL Identitäten aktiviert]** | Die Gesamtzahl der Identitäten, die erfolgreich für das Ziel aktiviert wurden, basierend auf den empfangenen Profilen. |
| **[!UICONTROL Ausgeschlossene Identitäten]** | Die Gesamtzahl der Identitäten, die von der Aktivierung für das Ziel ausgeschlossen wurden, basierend auf den empfangenen Profilen. Diese Identitäten können aufgrund fehlender Attribute oder Zustimmungsverletzungen ausgeschlossen werden. |
| **[!UICONTROL Datengröße]** | Die Größe des zu aktivierenden Datenflusses. |
| **[!UICONTROL Dateien insgesamt]** | Die Gesamtzahl der im Datenfluss aktivierten Dateien. |
| **[!UICONTROL Status]** | Der aktuelle Status des Aktivierungsauftrags. |
| **[!UICONTROL Start des Datenflusses]** | Datum und Uhrzeit des Beginns des Aktivierungsauftrags. |
| **[!UICONTROL Dataflow run end]** | Datum und Uhrzeit des Endes des Aktivierungsauftrags. |
| **[!UICONTROL Dataflow run ID]** | Die ID des aktuellen Aktivierungsauftrags. |
| **[!UICONTROL IMS-Organisations-ID]** | Die ID der Organisation, zu der der Aktivierungsauftrag gehört. |
| **[!UICONTROL Zielname]** | Der Name des Ziels, für das die Daten aktiviert werden. |

Im Bereich Zielgruppen wird eine Liste der Zielgruppen angezeigt, die im Rahmen des Aktivierungsauftrags aktiviert wurden.

![Das Dashboard des Aktivierungsauftrags. Informationen zu den Identitäten, die fehlgeschlagen sind oder ausgeschlossen wurden, werden hervorgehoben.](../assets/ui/monitor-audiences/activation-job-audiences.png)

Für den Abschnitt &quot;Zielgruppen&quot;stehen die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Name]** | Der Name der aktivierten Audience. |
| **[!UICONTROL Identitäten aktiviert]** | Die Gesamtzahl der Identitäten, die erfolgreich für das Ziel aktiviert wurden, basierend auf den empfangenen Profilen. |
| **[!UICONTROL Ausgeschlossene Identitäten]** | Die Gesamtzahl der Identitäten, die von der Aktivierung für das Ziel ausgeschlossen wurden, basierend auf den empfangenen Profilen. Diese Identitäten können aufgrund fehlender Attribute oder Zustimmungsverletzungen ausgeschlossen werden. |
| **[!UICONTROL Letzter Ausführungsstatus des Datenflusses]** | Der Status des letzten Aktivierungsauftrags, der für diese Zielgruppe ausgeführt wurde. |
| **[!UICONTROL Letztes Datum für die Ausführung des Datenflusses]** | Datum und Uhrzeit des letzten Aktivierungsauftrags, der für diese Zielgruppe ausgeführt wurde. |

Darüber hinaus können Sie Details zu den Fehlern beim Ausführen des Datenflusses anzeigen. Im Abschnitt &quot;Fehler beim Ausführen des Datenflusses&quot;können Sie sowohl die fehlgeschlagenen Identitäten als auch die ausgeschlossenen Identitäten anzeigen. Der Abschnitt &quot;Fehler&quot;enthält Details zum Fehlercode und zur Anzahl der fehlgeschlagenen oder ausgeschlossenen Identitäten.

![Das Dashboard des Aktivierungsauftrags. Informationen zu den Identitäten, die fehlgeschlagen sind oder ausgeschlossen wurden, werden hervorgehoben.](../assets/ui/monitor-audiences/activation-job-errors.png)

### Details zum Testauftrag {#evaluation-job-details}

Auf der Seite mit den Ausführungsdetails des Testauftrags werden Informationen zu den Metriken und Zielgruppen der Ausführung angezeigt, die mit dem Segmentierungsauftrag zusammenhängen.

![Das Dashboard des Auswertungsauftrags. Es werden Informationen zum Auswertungsauftrag der Zielgruppe angezeigt.](../assets/ui/monitor-audiences/evaluation-job-details.png)

Für diese Dashboard-Ansicht stehen die folgenden Metriken zur Verfügung:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Profile insgesamt]** | Die Gesamtzahl der Profile, die ausgewertet werden. |
| **[!UICONTROL Status]** | Der Status des Bewertungsauftrags. Mögliche Status für den Auswertungsauftrag sind **[!UICONTROL Erfolg]** und **[!UICONTROL Fehlgeschlagen]**. |
| **[!UICONTROL Auftragsstart]** | Datum und Uhrzeit des Beginns des Auswertungsauftrags. |
| **[!UICONTROL Auftragsende]** | Datum und Uhrzeit des Endes des Auswertungsauftrags. |
| **[!UICONTROL Auftragstyp]** | Der Typ des Segmentierungsauftrags. In diesem Fall handelt es sich immer um einen **[!UICONTROL Segmentauswertungsauftrag]**. |
| **[!UICONTROL Testtyp]** | Die Art der durchgeführten Bewertung. Dies kann entweder **[!UICONTROL Batch]** oder **[!UICONTROL Streaming]** sein. |
| **[!UICONTROL Auftrags-ID]** | Die ID des Auswertungsauftrags. |
| **[!UICONTROL IMS-Organisations-ID]** | Die ID der Organisation, zu der der Auswertungsauftrag gehört. |
| **[!UICONTROL Zielgruppenname]** | Der Name der auszuwertenden Zielgruppe. |
| **[!UICONTROL Zielgruppen-ID]** | Die ID der Zielgruppe, die ausgewertet wird. |

Unter dem Abschnitt [!UICONTROL Zielgruppen] können Sie eine Liste der Zielgruppen anzeigen, die im Rahmen des Auswertungsauftrags ausgewertet werden. Mithilfe der Suchleiste können Sie die Liste der Zielgruppen nach Namen filtern.

>[!IMPORTANT]
>
>Diese Dashboard-Ansicht unterstützt derzeit bis zu 800 Zielgruppenmetriken.

Für den Abschnitt [!UICONTROL Zielgruppen] sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Name]** | Der Name der auszuwertenden Zielgruppe. |
| **[!UICONTROL Anzahl der Profile]** | Die Anzahl der Profile, die ausgewertet werden. |

## Dashboard zur Überwachung von Segmentierungsaufträgen {#monitoring-segmentation-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Segmentierungsaufträge"
>abstract="Die Ansicht „Segmentierungsaufträge“ enthält Informationen zu den Auswertungs- und Exportaufträgen für alle Ihre Zielgruppen."

Um auf das Dashboard **[!UICONTROL Segmentierungsaufträge]** zuzugreifen, wählen Sie **[!UICONTROL Segmentierungsaufträge]** im Dashboard [!UICONTROL Zielgruppen] aus. Das Dashboard [!UICONTROL Überwachung] enthält Metriken und Informationen zu den Evaluierungs- und Exportvorgängen.

>[!NOTE]
>
>Für die Überwachung pro Zielgruppe werden nur **Auswertungsaufträge für die Segmentierung** unterstützt. Exportaufträge für Segmentierung unterstützen nur die Überwachung auf Unternehmensebene.

![Das Monitoring-Dashboard für Segmentierungsaufträge wird angezeigt. Der Umschalter zwischen Zielgruppen und Segmentierungsaufträgen wird hervorgehoben.](../assets/ui/monitor-audiences/segmentation-jobs-dashboard.png)

Verwenden Sie das Dashboard [!UICONTROL Segmentierungsaufträge] , um zu verstehen, ob die Profilauswertung und der Export rechtzeitig und ohne Ausnahmen erfolgen. Auf diese Weise können die nachgelagerten Dienste für die Zielaktivierung über die neuesten ausgewerteten Profildaten verfügen.

Die folgenden Metriken sind für Segmentierungsaufträge verfügbar:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Segmentierungsauftrag]** | Gibt den Namen des Segmentierungsauftrags an. |
| **[!UICONTROL Typ]** | Gibt den Typ des Segmentierungsauftrags - Export oder Auswertung an. Beachten Sie, dass der Segmentierungsauftrag in beiden Fällen **alle** Zielgruppen auswertet oder exportiert, die zu einer Organisation gehören. Weiterführende Informationen zu Exportvorgängen finden Sie im Handbuch zum Endpunkt [Exportaufträge](../../segmentation/api/export-jobs.md). Weiterführende Informationen zu Auswertungsaufträgen finden Sie im Tutorial zum [Auswerten einer Segmentdefinition](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Auftragsstart]** | Datum und Uhrzeit des Starts des Segmentierungsauftrags. |
| **[!UICONTROL Auftragsende]** | Datum und Uhrzeit des Abschlusses des Segmentierungsauftrags. |
| **[!UICONTROL Status]** | Der Status des abgeschlossenen Auftrags. Mögliche Status für den Segmentierungsauftrag umfassen Erfolg oder Fehlgeschlagen. |
