---
description: Erfahren Sie, wie Sie Datenflüsse während der Segmentierung mithilfe der Benutzeroberfläche von Experience Platform überwachen können.
title: Überwachen von Datenflüssen für Zielgruppen in der Benutzeroberfläche
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 7%

---

# Überwachen von Datenflüssen für Zielgruppen in der Benutzeroberfläche

Mit dem Segmentierungs-Service können Sie über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile] Zielgruppen erstellen. Experience Platform bietet Datenflüsse, mit denen dieser Datenfluss von Quellen zu Zielen transparent verfolgt werden kann.

Verwenden Sie das Monitoring-Dashboard, um eine visuelle Darstellung der Datenaktivität in einer Audience zu erhalten, einschließlich des Status der Segmentierung Ihrer Daten. Lesen Sie das Tutorial für Anweisungen dazu, wie Sie mit dem Monitoring-Dashboard die Segmentierung Ihrer Daten mithilfe der Experience Platform-Benutzeroberfläche überwachen können, sodass Sie den Status von Zielgruppenaktivierungs-, Auswertungs- und Exportvorgängen verfolgen können.

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Datenflüsse](../home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Experience Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
   - [Datenflussausführungen](../../sources/notifications.md): Datenflussausführungen sind die wiederkehrenden geplanten Aufträge, die auf der Häufigkeitskonfiguration ausgewählter Datenflüsse basieren.
- [Segmentierung](../../segmentation/home.md): Mit der Segmentierung können Sie Zielgruppen aus Ihren Echtzeit-Kundenprofildaten erstellen.
   - [Aktivierungsaufträge](../../destinations/ui/activation-overview.md): Ein Aktivierungsauftrag wird verwendet, um Ihre Audience für ein bestimmtes Ziel zu aktivieren.
   - [Auswertungsaufträge](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment): Ein Auswertungsauftrag ist ein asynchroner Prozess, der die Zielgruppe auswertet.
   - [Exportvorgänge](../../segmentation/api/export-jobs.md): Ein Exportvorgang ist ein asynchroner Prozess, der zum Beibehalten von Zielgruppenmitgliedern in Datensätzen verwendet wird.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

## Dashboard zur Überwachung von Zielgruppen {#monitoring-audiences-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="Zielgruppen"
>abstract="Die Zielgruppenansicht enthält Informationen zu allen Zielgruppen Ihrer Organisation sowie zu ihren Aktivierungs- und Evaluierungsvorgängen."

Um auf das Dashboard **[!UICONTROL Zielgruppen]** zuzugreifen, wählen Sie **[!UICONTROL Monitoring]** in der linken Navigationsleiste aus. Wählen Sie auf der **[!UICONTROL Überwachung]** die Karte **[!UICONTROL Zielgruppen]** aus.

![Die Karte Zielgruppen . Es werden Informationen zum letzten Auswertungsauftrag und zum letzten Exportauftrag angezeigt.](../assets/ui/monitor-audiences/audience-card.png)

Im Haupt-Dashboard **[!UICONTROL Zielgruppen]** zeigt die Karte **[!UICONTROL Zielgruppen]** den Status und das Datum des letzten Auswertungsauftrags und des letzten Exportauftrags an.

Das Dashboard selbst enthält Metriken für Zielgruppen und Segmentierungsaufträge. Standardmäßig zeigt das Dashboard die Zielgruppenmetriken der letzten 24 Stunden an. Weitere Informationen zur Ansicht Segmentierungsaufträge finden Sie im Abschnitt [Überwachen von &#x200B;](#monitoring-segmentation-jobs-dashboard)&quot;.

>[!IMPORTANT]
>
>Derzeit werden nur Zielgruppen, die für [Batch-Ziele (dateibasiert) aktiviert &#x200B;](../../destinations/destination-types.md#file-based), für das Dashboard „Zielgruppen-Überwachung“ unterstützt.

![Das Zielgruppen-Dashboard. Es werden Informationen zu den verschiedenen Zielgruppen in Ihrer Organisation und Sandbox angezeigt.](../assets/ui/monitor-audiences/audience-dashboard.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Zielgruppenname]** | Der Name der Zielgruppe. |
| **[!UICONTROL Datentyp]** | Der Datentyp der Zielgruppe. Mögliche Werte sind **[!UICONTROL Kunde]**, **[!UICONTROL Konto]** und **[!UICONTROL Interessent]**. Sie können mit dem Filter [!UICONTROL Datentyp“ über dem Kartenband Zielgruppen eines bestimmten &#x200B;] anzeigen. |
| **[!UICONTROL Zeitstempel der letzten Auswertung]** | Datum und Uhrzeit der letzten Ausführung des Auswertungsauftrags für die Zielgruppe. |
| **[!UICONTROL Letzter Auswertungsstatus]** | Der Status des letzten Auswertungsauftrags der Zielgruppe. Mögliche Werte sind **[!UICONTROL Erfolg]**, **[!UICONTROL Keine]** und **[!UICONTROL Fehlgeschlagen]**. |
| **[!UICONTROL Letzte Auswertungsmethode]** | Die Auswertungsmethode der Zielgruppe. Da nur die Batch-Segmentierung unterstützt wird, ist der einzige mögliche Wert **[!UICONTROL Batch]**. |
| **[!UICONTROL Letzte Auswertungsprofile]** | Die Anzahl der Profile, die im letzten Auswertungsauftrag der Zielgruppe ausgewertet wurden. |
| **[!UICONTROL Zeitstempel der letzten Aktivierung]** | Datum und Uhrzeit der letzten Ausführung des Aktivierungsauftrags der Zielgruppe. |
| **[!UICONTROL Status der letzten Aktivierung]** | Der Status des letzten Aktivierungsauftrags der Zielgruppe. Mögliche Werte sind **[!UICONTROL Erfolg]**, **[!UICONTROL Keine]** und **[!UICONTROL Fehlgeschlagen]**. |
| **[!UICONTROL Identitäten der letzten Aktivierung]** | Die Anzahl der Identitäten, die im letzten Aktivierungsauftrag der Zielgruppe aktiviert wurden. |
| **[!UICONTROL Ziel der letzten Aktivierung]** | Der Name des Ziels, für das der letzte Aktivierungsauftrag der Zielgruppe aktiviert wurde. |

Sie können die Ergebnisse nach einer bestimmten Zielgruppe filtern und die zugehörigen Segmentierungsaufträge anzeigen, indem Sie das Filtersymbol (![&#x200B; Filtersymbol) auswählen.](/help/images/icons/filter-add.png)). Die Segmentierungsaufträge werden in chronologischer Reihenfolge sortiert, wobei die neuesten Segmentierungsaufträge zuerst angezeigt werden.

![Das Filtersymbol ist hervorgehoben. Wenn Sie diese Option auswählen, können Sie die Segmentierungsaufträge für die angegebene Zielgruppe anzeigen.](../assets/ui/monitor-audiences/filter-audience.png)

Das Dashboard für gefilterte Zielgruppen wird angezeigt. Die Karte **[!UICONTROL Zielgruppen]** zeigt den Status und das Datum des letzten Auswertungsauftrags und des letzten Aktivierungsauftrags an.

![Die Karte Zielgruppen . Es werden Informationen zum letzten Auswertungsauftrag und zum letzten Aktivierungsauftrag angezeigt.](../assets/ui/monitor-audiences/specified-audience-card.png)

Das Dashboard selbst zeigt die Zeit und den Status der letzten Evaluierungs- und Aktivierungsaufträge an, ein Diagramm, das die Profilanzahl der Zielgruppenevaluierung und Metriken für die ausgeführten Segmentierungsaufträge anzeigt. Standardmäßig zeigt das Dashboard Segmentierungsauftragsmetriken für die letzten 24 Stunden an.

![Das gefilterte Zielgruppen-Dashboard. Es werden Informationen zu den verschiedenen Segmentierungsaufträgen angezeigt, die für diese Zielgruppe ausgeführt wurden.](../assets/ui/monitor-audiences/filter-audience.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Auftragsstart]** | Datum und Uhrzeit des Starts des Segmentierungsauftrags. |
| **[!UICONTROL Typ]** | Gibt den Typ des Segmentierungsauftrags an. Die beiden unterstützten Vorgangstypen sind **Aktivierungs** und **Evaluierungs** Vorgänge. |
| **[!UICONTROL Vorgang abgeschlossen]** | Datum und Uhrzeit des Abschlusses des Segmentierungsauftrags. |
| **[!UICONTROL Verarbeitungszeit]** | Die Zeit, die für den Abschluss des Segmentierungsauftrags benötigt wurde. |
| **[!UICONTROL Auftragsstatus]** | Der Status des Segmentierungsauftrags. Unterstützte Werte sind **[!UICONTROL Erfolg]**, **[!UICONTROL In]** und **[!UICONTROL Fehlgeschlagen]**. |
| **[!UICONTROL Anzahl der Profile]** | Die Anzahl der Profile, die der Segmentierungsauftrag auswertet. Jeder Benutzer sollte über ein eindeutiges Profil verfügen. |
| **[!UICONTROL Identität aktiviert]** | Die Anzahl der Identitäten, die der Segmentierungsauftrag aktiviert. Jedes Profil kann mehrere Identitäten haben. Ein Profil könnte beispielsweise eine E-Mail-Adresse, eine Telefonnummer und eine Treuenummer als Identitäten haben. |
| **[!UICONTROL Zielname]** | Der Name des Ziels, für das der Segmentierungsauftrag aktiviert wird. |

Sie können weiter nach einem bestimmten Segmentierungsauftrag filtern und dessen Details anzeigen, indem Sie das Filtersymbol (das ![) auswählen.](/help/images/icons/filter.png)). Es gibt zwei verschiedene Arten von Segmentierungsaufträgen, die gefiltert werden können: Aktivierungsaufträge und Auswertungsaufträge.

### Details zum Aktivierungsvorgang {#activation-job-details}

Die Seite mit den Details der Datenflussausführung für den Aktivierungsauftrag enthält Informationen zu den Metriken des Durchgangs, zu Datenflussausführungsfehlern und zu Zielgruppen, die mit dem Segmentierungsauftrag in Verbindung stehen. Ein Aktivierungsauftrag wird verwendet, um Ihre Zielgruppe für ein bestimmtes Ziel zu aktivieren.

![Das Dashboard des Aktivierungsvorgangs. Es werden Informationen zu den verschiedenen Segmentierungsaufträgen angezeigt, die für diese Zielgruppe ausgeführt wurden.](../assets/ui/monitor-audiences/activation-job-dashboard.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Empfangene Profile]** | Die Gesamtzahl der im Aktivierungsfluss empfangenen Profile. |
| **[!UICONTROL Identitäten aktiviert]** | Die Gesamtzahl der Identitäten, die basierend auf den empfangenen Profilen erfolgreich für das Ziel aktiviert wurden. |
| **[!UICONTROL Identitäten ausgeschlossen]** | Die Gesamtzahl der Identitäten, die von der Aktivierung für das Ziel ausgeschlossen wurden, basierend auf den empfangenen Profilen. Diese Identitäten konnten aufgrund fehlender Attribute oder Einverständnisverletzungen ausgeschlossen werden. |
| **[!UICONTROL Größe der Daten]** | Die Größe des aktivierten Datenflusses. |
| **[!UICONTROL Dateien insgesamt]** | Die Gesamtzahl der Dateien, die im Datenfluss aktiviert werden. |
| **[!UICONTROL Status]** | Der aktuelle Status des Aktivierungsvorgangs. |
| **[!UICONTROL Start der Datenflussausführung]** | Datum und Uhrzeit des Starts des Aktivierungsauftrags. |
| **[!UICONTROL Ende der Datenflussausführung]** | Das Datum und die Uhrzeit, zu der der Aktivierungsvorgang beendet wurde. |
| **[!UICONTROL Datenflussausführungs-ID]** | Die ID des aktuellen Aktivierungsauftrags. |
| **[!UICONTROL IMS-Organisations-ID]** | Die ID der Organisation, zu der der Aktivierungsauftrag gehört. |
| **[!UICONTROL Zielname]** | Der Name des Ziels, für das die Daten aktiviert werden. |

Im Abschnitt Zielgruppen wird eine Liste von Zielgruppen angezeigt, die im Rahmen des Aktivierungsauftrags aktiviert wurden.

![Das Dashboard des Aktivierungsvorgangs. Informationen zu den fehlgeschlagenen oder ausgeschlossenen Identitäten werden hervorgehoben.](../assets/ui/monitor-audiences/activation-job-audiences.png)

Für den Abschnitt Zielgruppen sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Name]** | Der Name der aktivierten Zielgruppe. |
| **[!UICONTROL Identitäten aktiviert]** | Die Gesamtzahl der Identitäten, die basierend auf den empfangenen Profilen erfolgreich für das Ziel aktiviert wurden. |
| **[!UICONTROL Identitäten ausgeschlossen]** | Die Gesamtzahl der Identitäten, die von der Aktivierung für das Ziel ausgeschlossen wurden, basierend auf den empfangenen Profilen. Diese Identitäten konnten aufgrund fehlender Attribute oder Einverständnisverletzungen ausgeschlossen werden. |
| **[!UICONTROL Letzter Ausführungsstatus für Datenfluss]** | Der Status des letzten Aktivierungsvorgangs, der für diese Zielgruppe ausgeführt wurde. |
| **[!UICONTROL Letztes Ausführungsdatum für Datenfluss]** | Datum und Uhrzeit des letzten Aktivierungsvorgangs, der für diese Zielgruppe ausgeführt wurde. |

Darüber hinaus können Sie Details zu den Datenflussausführungsfehlern anzeigen. Im Abschnitt Fehler bei der Ausführung des Datenflusses können Sie sowohl die fehlgeschlagenen Identitäten als auch die ausgeschlossenen Identitäten anzeigen. Der Abschnitt Fehler enthält Details zum Fehler-Code und zur Anzahl der fehlgeschlagenen oder ausgeschlossenen Identitäten.

![Das Dashboard des Aktivierungsvorgangs. Informationen zu den fehlgeschlagenen oder ausgeschlossenen Identitäten werden hervorgehoben.](../assets/ui/monitor-audiences/activation-job-errors.png)

### Details zum Auswertungsauftrag {#evaluation-job-details}

Die Seite mit den Ausführungsdetails für den Datenfluss des Auswertungsauftrags zeigt Informationen über die Metriken und Zielgruppen des Durchgangs an, die mit dem Segmentierungsauftrag in Verbindung stehen.

![Das Dashboard des Auswertungsauftrags. Es werden Informationen zum Auswertungsauftrag der Zielgruppe angezeigt.](../assets/ui/monitor-audiences/evaluation-job-details.png)

Für diese Dashboard-Ansicht sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Profile insgesamt]** | Die Gesamtzahl der Profile, die ausgewertet werden. |
| **[!UICONTROL Status]** | Der Status des Auswertungsauftrags. Mögliche Status für den Auswertungsauftrag sind **[!UICONTROL Erfolg]** und **[!UICONTROL Fehlgeschlagen]**. |
| **[!UICONTROL Auftragsstart]** | Datum und Uhrzeit des Starts des Auswertungsauftrags. |
| **[!UICONTROL Ende des Vorgangs]** | Das Datum und die Uhrzeit, zu der der Auswertungsauftrag beendet wurde. |
| **[!UICONTROL Vorgangstyp]** | Der Typ des Segmentierungsauftrags. In diesem Fall handelt es sich immer um einen Vorgang **[!UICONTROL Segmentauswertung]**. |
| **[!UICONTROL Auswertungstyp]** | Die Art der durchgeführten Auswertung. Dies kann entweder &quot;**[!UICONTROL &quot;]** &quot;**[!UICONTROL &quot;]**. |
| **[!UICONTROL Vorgangs-ID]** | Die ID des Auswertungsauftrags. |
| **[!UICONTROL IMS-Organisations-ID]** | Die ID der Organisation, zu der der Auswertungsauftrag gehört. |
| **[!UICONTROL Zielgruppenname]** | Der Name der Zielgruppe, die ausgewertet wird. |
| **[!UICONTROL Zielgruppen-ID]** | Die ID der Zielgruppe, die ausgewertet wird. |

Im Abschnitt [!UICONTROL Audiences] wird eine Liste von Audiences angezeigt, die im Rahmen des Auswertungsauftrags ausgewertet werden. Sie können die Liste der Zielgruppen mithilfe der Suchleiste nach Namen filtern.

>[!IMPORTANT]
>
>Diese Dashboard-Ansicht unterstützt derzeit bis zu 800 Zielgruppenmetriken.

Für den Abschnitt [!UICONTROL Zielgruppen] sind die folgenden Metriken verfügbar:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Name]** | Der Name der Zielgruppe, die ausgewertet wird. |
| **[!UICONTROL Anzahl der Profile]** | Die Anzahl der Profile, die ausgewertet werden. |

## Dashboard zur Überwachung von Segmentierungsaufträgen {#monitoring-segmentation-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="Segmentierungsaufträge"
>abstract="Die Ansicht „Segmentierungsaufträge“ enthält Informationen zu den Auswertungs- und Exportaufträgen für alle Ihre Zielgruppen."

Um auf das Dashboard **[!UICONTROL Segmentierungsaufträge]** zuzugreifen, wählen Sie **[!UICONTROL Segmentierungsaufträge]** im Dashboard [!UICONTROL Zielgruppen] aus. Das [!UICONTROL Monitoring]-Dashboard enthält Metriken und Informationen zu Evaluierungs- und Exportvorgängen.

>[!NOTE]
>
>Nur **Segmentierungsbewertungsaufträge** werden für die Überwachung pro Zielgruppe unterstützt. Segmentierungs-Exportvorgänge unterstützen nur die Überwachung auf Organisationsebene.

![Das Dashboard zur Überwachung von Segmentierungsaufträgen wird angezeigt. Der Umschalter zum Wechseln zwischen Audiences und Segmentierungsaufträgen ist hervorgehoben.](../assets/ui/monitor-audiences/segmentation-jobs-dashboard.png)

Verwenden Sie das Dashboard [!UICONTROL Segmentierungsvorgänge] um zu verstehen, ob die Profilauswertung und der Export pünktlich und ohne Ausnahmen erfolgt, sodass die nachgelagerten Services für die Zielaktivierung über die neuesten ausgewerteten Profildaten verfügen können.

Die folgenden Metriken sind für Segmentierungsaufträge verfügbar:

| Metrik | Beschreibung |
| ------ | ----------- |
| **[!UICONTROL Segmentierungsvorgang]** | Gibt den Namen des Segmentierungsauftrags an. |
| **[!UICONTROL Typ]** | Gibt den Typ des Segmentierungsauftrags an - Export oder Auswertung. Beachten Sie, dass der Segmentierungsauftrag in beiden Fällen **alle** Zielgruppen einer Organisation auswertet oder exportiert. Weitere Informationen zu Exportvorgängen finden Sie im Handbuch zum Endpunkt [Exportvorgänge](../../segmentation/api/export-jobs.md). Weitere Informationen zu Auswertungsaufträgen finden Sie im Tutorial [Evaluieren einer Segmentdefinition](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL Auftragsstart]** | Datum und Uhrzeit des Starts des Segmentierungsauftrags. |
| **[!UICONTROL Ende des Vorgangs]** | Datum und Uhrzeit des Abschlusses des Segmentierungsauftrags. |
| **[!UICONTROL Status]** | Der Status des abgeschlossenen Auftrags. Mögliche Status für den Segmentierungsauftrag sind Erfolg oder Fehlgeschlagen. |
