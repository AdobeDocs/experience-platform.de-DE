---
title: Abfragezeitpläne
description: Erfahren Sie, wie Sie geplante Abfrageausführungen automatisieren, einen Abfragezeitplan löschen oder deaktivieren und die verfügbaren Planungsoptionen über die Adobe Experience Platform-Benutzeroberfläche nutzen können.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 8d3da7f33aefa822e24bd60168760d856a85865f
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 8%

---

# Abfragepläne

Sie können die Ausführung von Abfragen automatisieren, indem Sie Abfragezeitpläne erstellen. Geplante Abfragen werden mit einer benutzerdefinierten Kadenz ausgeführt, um Ihre Daten basierend auf Häufigkeit, Datum und Uhrzeit zu verwalten. Bei Bedarf können Sie auch einen Ausgabedatensatz für Ihre Ergebnisse auswählen. Abfragen, die als Vorlage gespeichert wurden, können über den Abfrage-Editor geplant werden.

>[!IMPORTANT]
>
>Sie können einen Zeitplan nur zu einer Abfrage hinzufügen, die bereits erstellt und gespeichert wurde.

## Kontoanforderungen für geplante Abfragen {#technical-account-user-requirements}

Damit geplante Abfragen zuverlässig ausgeführt werden können, empfiehlt Adobe, dass Admins ein technisches Konto (mit OAuth-Server-zu-Server-Anmeldeinformationen) zum Erstellen geplanter Abfragen bereitstellen. Geplante Abfragen können auch mit einem persönlichen Benutzerkonto erstellt werden. Auf diese Weise erstellte Abfragen werden jedoch nicht mehr ausgeführt, wenn der Zugriff dieses Benutzers entfernt oder deaktiviert wird.

Weitere Informationen zum Einrichten technischer Konten und zum Zuweisen der erforderlichen Berechtigungen finden Sie unter [Voraussetzungen für das Anmeldeinformationshandbuch](./credentials.md#prerequisites) und [API-Authentifizierung](../../landing/api-authentication.md).

Weitere Anleitungen zum Erstellen und Konfigurieren eines technischen Kontos finden Sie unter:

- [Developer Console-Setup](https://experienceleague.adobe.com/en/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman): Schrittweise Anweisungen zum Konfigurieren der Adobe Developer Console und zum Abrufen von OAuth-Anmeldeinformationen.
- [Einrichtung eines technischen Endkontos](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/setup) Eine umfassende Anleitung zum Erstellen und Konfigurieren eines technischen Kontos in Adobe Experience Platform.

Wenn Sie nur die Benutzeroberfläche des Abfrage-Service verwenden, stellen Sie sicher, dass Sie über die erforderlichen Berechtigungen verfügen, oder stimmen Sie sich mit einem Administrator ab, der technische Konten verwaltet. Alle geplanten Abfragen werden der Liste auf der Registerkarte [!UICONTROL Scheduled queries] hinzugefügt, wo Sie den Status, Zeitplandetails und Fehlermeldungen für alle geplanten Abfrageaufträge überwachen sowie Warnhinweise abonnieren können. Weitere Informationen zur Überwachung und Verwaltung Ihrer Abfragen finden Sie im Dokument [Überwachen geplanter Abfragen](./monitor-queries.md).

Dieser Workflow behandelt den Zeitplanungsprozess in der Benutzeroberfläche des Abfrage-Service. Informationen zum Hinzufügen von Zeitplänen mithilfe der API finden Sie [ Handbuch zu Endpunkten für geplante Abfragen](../api/scheduled-queries.md).

>[!NOTE]
>
>Verwenden Sie ein technisches Konto, um sicherzustellen, dass geplante Abfragen weiterhin ausgeführt werden, selbst wenn Benutzende das Unternehmen verlassen oder sich ihre Rollen ändern. Wählen Sie, wann immer möglich, ein technisches Konto für eine unterbrechungsfreie Abfrageautomatisierung.

## Abfragezeitplan erstellen {#create-schedule}

Um eine Abfrage zu planen, wählen Sie eine Abfragevorlage auf der Registerkarte [!UICONTROL Templates] oder der Spalte [!UICONTROL Template] der Registerkarte [!UICONTROL Scheduled Queries] aus. Wenn Sie den Vorlagennamen auswählen, gelangen Sie zum Abfrage-Editor.

Wenn Sie über den Abfrage-Editor auf eine gespeicherte Abfrage zugreifen, können Sie einen Zeitplan für die Abfrage erstellen oder den Zeitplan der Abfrage im Detailbereich anzeigen.

>[!TIP]
>
>Wählen Sie **[!UICONTROL View schedule]** aus, um zum Arbeitsbereich für Zeitpläne zu navigieren und geplante Abfrageausführungen auf einen Blick zu sehen.

![Der Abfrage-Editor mit hervorgehobenen [!UICONTROL View schedule] und [!UICONTROL Add schedule].](../images/ui/query-schedules/view-add-schedule.png)

Wählen Sie **[!UICONTROL Add schedule]** aus, um zur Seite [Zeitplandetails“ ](#schedule-details).

Alternativ können Sie die Registerkarte **[!UICONTROL Schedules]** unter dem Namen der Abfrage auswählen.

![Der Abfrage-Editor mit der hervorgehobenen Registerkarte „Zeitpläne“.](../images/ui/query-schedules/schedules-tab.png)

Der Arbeitsbereich für Zeitpläne wird angezeigt. Die Benutzeroberfläche zeigt eine Liste aller geplanten Ausführungen an, mit denen die Vorlage verknüpft ist. Wählen Sie **[!UICONTROL Add Schedule]** aus, um einen Zeitplan zu erstellen.

![Der Arbeitsbereich „Zeitplan“ des Abfrage-Editors mit hervorgehobener Option „Zeitplan hinzufügen“.](../images/ui/query-schedules/add-schedule.png)

### Zeitplandetails hinzufügen {#schedule-details}

Die Seite mit den Zeitplandetails wird angezeigt. Auf dieser Seite können Sie eine Vielzahl von Details für die geplante Abfrage bearbeiten. Zu den Details gehören [Häufigkeit und Wochentag der geplanten Abfrage](#scheduled-query-frequency) Ausführung, das Start- und Enddatum, der Datensatz, in den die Ergebnisse exportiert werden sollen, und [Abfragestatus-Warnhinweise](#alerts-for-query-status).

>[!IMPORTANT]
>
>Die Benutzeroberfläche der Abfrageplanung unterstützt keine unbegrenzte oder dauerhafte Planung. Ein Enddatum muss angegeben werden. Für das Enddatum gibt es keine Obergrenze.

![Das hervorgehobene Bedienfeld „Zeitplandetails“.](../images/ui/query-schedules/schedule-details.png)

#### Geplante Abfragefrequenz {#scheduled-query-frequency}

Sie können die folgenden Optionen für **[!UICONTROL Frequency]** auswählen:

- **[!UICONTROL Hourly]**: Die geplante Abfrage wird im ausgewählten Datumsbereich stündlich ausgeführt.
- **[!UICONTROL Daily]**: Die geplante Abfrage wird alle X Tage zum ausgewählten Zeitpunkt und im ausgewählten Datumsbereich ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.
- **[!UICONTROL Weekly]**: Die ausgewählte Abfrage wird an den ausgewählten Wochentagen, zur ausgewählten Uhrzeit und im ausgewählten Datumsbereich ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.
- **[!UICONTROL Monthly]**: Die ausgewählte Abfrage wird jeden Monat am ausgewählten Tag, zur ausgewählten Uhrzeit und im ausgewählten Datumsbereich ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.
- **[!UICONTROL Yearly]**: Die ausgewählte Abfrage wird jedes Jahr am ausgewählten Tag, im ausgewählten Monat, zur ausgewählten Uhrzeit und im ausgewählten Datumsbereich ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.

### Angeben von Datensatzdetails {#dataset-details}

Verwalten Sie die Abfrageergebnisse, indem Sie entweder die Daten an einen vorhandenen Datensatz anhängen oder einen neuen Datensatz erstellen und die Daten an ihn anhängen.

Wählen Sie **[!UICONTROL Create and append into new dataset]** aus, um einen Datensatz zu erstellen, wenn Sie eine Abfrage zum ersten Mal ausführen. Bei nachfolgenden Ausführungen werden weiterhin Daten in diesen Datensatz eingefügt. Geben Sie abschließend einen Namen und eine Beschreibung für den Datensatz an.

>[!IMPORTANT]
>
> Da Sie entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen, müssen Sie **weder** `INSERT INTO` noch `CREATE TABLE AS SELECT` als Teil die Abfrage einbeziehen, da die Datensätze bereits festgelegt sind. Das Einbeziehen von `INSERT INTO` oder `CREATE TABLE AS SELECT` als Teil Ihrer geplanten Abfragen führt zu einem Fehler.

![Das Bedienfeld „Zeitplandetails“ mit hervorgehobenen Datensatzdetails und [!UICONTROL Create and append into new dataset] hervorgehobenen Optionen.](../images/ui/query-schedules/dataset-details-create-and-append.png)

Wählen Sie alternativ **[!UICONTROL Append into existing dataset]** und dann das Datensatzsymbol (![ Datensatzsymbol .](/help/images/icons/database.png)) aus.

![Das Bedienfeld „Zeitplandetails“ mit hervorgehobenen Datensatzdetails und „An vorhandenen Datensatz anhängen“.](../images/ui/query-schedules/dataset-details-existing.png)

Das Dialogfeld **[!UICONTROL Select output dataset]** wird angezeigt.

Durchsuchen Sie als Nächstes entweder die vorhandenen Datensätze oder verwenden Sie das Suchfeld, um die Optionen zu filtern. Wählen Sie die Zeile des Datensatzes aus, den Sie verwenden möchten. Die Datensatzdetails werden im Bedienfeld auf der rechten Seite angezeigt. Wählen Sie **[!UICONTROL Done]** aus, um Ihre Auswahl zu bestätigen.

![Das Dialogfeld „Ausgabedatensatz auswählen“ mit Hervorhebung des Suchfelds, einer Datensatzzeile und „Fertig“.](../images/ui/query-schedules/select-output-dataset-dialog.png)

### Abfragen in Quarantäne verschieben, wenn sie kontinuierlich fehlschlagen {#quarantine}

Bei der Erstellung eines Zeitplans können Sie Ihre Abfrage in der Quarantänefunktion registrieren, um Systemressourcen zu schützen und potenzielle Unterbrechungen zu vermeiden. Die Quarantänefunktion identifiziert und isoliert Abfragen, die wiederholt fehlschlagen, automatisch, indem sie in einen [!UICONTROL Quarantined] Status versetzt wird. Indem Sie Abfragen nach zehn aufeinander folgenden Fehlern unter Quarantäne stellen, können Sie eingreifen, Probleme überprüfen und korrigieren, bevor Sie weitere Ausführungen zulassen. Dies hilft, Ihre betriebliche Effizienz und Datenintegrität zu erhalten.

![Der Arbeitsbereich „Zeitpläne für Abfragen“ mit hervorgehobenen [!UICONTROL Query Quarantine] und „Ja“ wurde ausgewählt.](../images/ui/query-schedules/quarantine-enroll.png)

Sobald eine Abfrage für die Quarantänefunktion registriert ist, können Sie Warnhinweise für diese Änderung des Abfragestatus abonnieren. Wenn eine geplante Abfrage nicht unter Quarantäne gestellt wird, wird sie nicht als Option im [Dialogfeld Warnhinweise“ ](./monitor-queries.md#alert-subscription).

Sie können eine geplante Abfrage auch über die Inline-Aktionen auf der Registerkarte [!UICONTROL Scheduled Queries] für die Quarantänefunktion registrieren. Weitere Informationen finden [ in der ](./monitor-queries.md#alert-subscription) zum Überwachen von Abfragen .

### Festlegen von Warnhinweisen für den Status geplanter Abfragen {#alerts-for-query-status}

Sie können im Rahmen Ihrer Einstellungen für geplante Abfragen auch Abfrage-Warnhinweise abonnieren. Sie können Ihre Einstellungen so konfigurieren, dass Benachrichtigungen für verschiedene Situationen empfangen werden. Warnhinweise können für einen Quarantänestatus, Verzögerungen bei der Abfrageverarbeitung oder eine Änderung des Status Ihrer Abfrage festgelegt werden. Zu den verfügbaren Warnoptionen für den Abfragestatus gehören „Start“, „Erfolg“ und „Fehler“. Warnhinweise können entweder in Form von eingeblendeten Benachrichtigungen oder per E-Mail empfangen werden. Aktivieren Sie das Kontrollkästchen, um Warnhinweise für diesen Status der geplanten Abfrage zu abonnieren.

![Das Bedienfeld „Zeitplandetails“ mit hervorgehobenen Warnoptionen.](../images/ui/query-editor/alerts.png)

In der folgenden Tabelle werden die unterstützten Warnhinweistypen für Abfragen erläutert:

| Warnhinweistyp | Beschreibung |
|---|---|
| `start` | Dieser Warnhinweis informiert Sie, wenn eine geplante Abfrageausführung initiiert wird oder mit der Verarbeitung beginnt. |
| `success` | Dieser Warnhinweis informiert Sie, wenn eine geplante Abfrage erfolgreich ausgeführt wurde, und gibt an, dass die Abfrage fehlerfrei ausgeführt wurde. |
| `failed` | Dieser Warnhinweis Trigger, wenn bei der Ausführung einer geplanten Abfrage ein Fehler auftritt oder sie nicht erfolgreich ausgeführt werden kann. So können Sie Probleme schnell identifizieren und beheben. |
| `quarantine` | Dieser Warnhinweis wird aktiviert, wenn eine geplante Abfrageausführung in den Quarantänestatus versetzt wird. Sobald eine Abfrage [in der Quarantänefunktion registriert) ](#quarantine), wird jede geplante Abfrage, die zehn aufeinander folgende Ausführungen fehlschlägt, automatisch in einen [!UICONTROL Quarantined] Status versetzt. Eine unter Quarantäne gestellte Abfrage erfordert dann Ihr Eingreifen, bevor weitere Ausführungen stattfinden können. Hinweis: Abfragen müssen für die Quarantänefunktion registriert sein, damit Sie Quarantänewarnungen abonnieren können. |
| `delay` | Dieser Warnhinweis benachrichtigt Sie, wenn das [ einer geplanten Abfrageausführung einen bestimmten Schwellenwert ](./monitor-queries.md#query-run-delay). Sie können einen benutzerdefinierten Zeitpunkt festlegen, zu dem der Warnhinweis Trigger wird, wenn die Abfrage für diesen Zeitraum ausgeführt wird, ohne dass entweder der Abschluss erfolgt oder ein Fehler auftritt. Das Standardverhalten legt einen Warnhinweis für 150 Minuten fest, nachdem die Verarbeitung der Abfrage begonnen hat. |

>[!NOTE]
>
>Wenn Sie einen [!UICONTROL Query Run Delay] festlegen, müssen Sie Ihre gewünschte Verzögerungszeit in Minuten in der Experience Platform-Benutzeroberfläche festlegen. Geben Sie die Dauer in Minuten ein. Die maximale Verzögerung beträgt 24 Stunden (1440 Minuten).

Einen Überblick über Warnhinweise in Adobe Experience Platform, einschließlich der Struktur der Definition von Warnhinweisregeln, finden Sie unter [Warnhinweise - Übersicht](../../observability/alerts/overview.md). Anleitungen zum Verwalten von Warnhinweisen und Warnhinweisregeln in der Adobe Experience Platform-Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche von Warnhinweisen](../../observability/alerts/ui.md).

### Festlegen von Parametern für eine geplante parametrisierte Abfrage {#set-parameters}

Wenn Sie eine geplante Abfrage für eine parametrisierte Abfrage erstellen, müssen Sie jetzt die Parameterwerte für diese Abfrageausführungen festlegen.

![Der Abschnitt „Zeitplandetails“ des Workflows für die Zeitplanerstellung mit hervorgehobenem Abschnitt „Abfrageparameter“.](../images/ui/query-schedules/scheduled-query-parameter.png)

Nachdem Sie Ihre Zeitplandetails bestätigt haben, wählen Sie **[!UICONTROL Save]** aus, um einen Zeitplan zu erstellen. Sie kehren zur Registerkarte Zeitpläne Ihrer Vorlage zurück. Dieser Arbeitsbereich zeigt Details zum neu erstellten Zeitplan an, einschließlich der Zeitplan-ID, des Zeitplans selbst und des Ausgabedatensatzes des Zeitplans.

## Geplante Abfrageausführungen anzeigen {#scheduled-query-runs}

Wählen Sie auf der Registerkarte [!UICONTROL Schedules] Ihrer Vorlage die Zeitplan-ID aus, um zur Liste der Abfrageausführungen für Ihre neu geplante Abfrage zu navigieren.

![Der Arbeitsbereich für Zeitpläne mit dem hervorgehobenen neu erstellten Zeitplan.](../images/ui/query-schedules/schedules-workspace.png)

Alternativ können Sie eine Liste der geplanten Ausführungen einer Abfragevorlage anzeigen, indem Sie zur Registerkarte **[!UICONTROL Scheduled queries]** navigieren und einen Vorlagennamen aus der verfügbaren Liste auswählen.

![Die Registerkarte „Geplante Abfragen“ mit einer hervorgehobenen benannten Vorlage.](../images/ui/query-schedules/view-scheduled-runs.png)

Die Liste der Abfrageausführungen für diese geplante Abfrage wird angezeigt.

### Stunden auf Auftragsebene berechnen {#compute-hours}

Verfolgen Sie die auf der Abfrageausführungsebene verbrauchten Rechenstunden für Ihre CTAS/ITAS-Batch-Abfragen. Diese Funktion bietet Einblicke in die Computernutzung und hilft Ihnen, die Ressourcenzuweisung zu optimieren und die Abfrageleistung zu verbessern.

>[!AVAILABILITY]
>
>Die Funktion „Stunden berechnen“ ist nur für Benutzer verfügbar, die die [Data Distiller SKU](../data-distiller/overview.md) erworben haben. Wenden Sie sich an den Adobe-Support, um weitere Informationen zu erhalten.

![Der Detailabschnitt des Arbeitsbereichs Geplante Abfragen mit einer Liste von Abfrageausführungen, die für eine geplante Abfrage hervorgehoben sind.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Die folgende Tabelle enthält Beschreibungen der einzelnen Spalten, die im Detailabschnitt verfügbar sind und geplante Abfrageausführungen auflisten.

| Spaltentitel | Beschreibung |
|---------------------|----------------------------------|
| [!UICONTROL Query Run ID] | Zeigt für jede ausgeführte Abfrage eine eindeutige Kennung an, mit der Sie einzelne Ausführungen Ihrer geplanten Abfragen verfolgen und referenzieren können. |
| [!UICONTROL Query Run Start] | Gibt das Startdatum und die Uhrzeit der Abfrageausführung an, damit Sie überwachen können, wann jede Ausführung begann. |
| [!UICONTROL Query Run Complete] | Zeigt das Abschlussdatum und die Uhrzeit der Abfrageausführung an, um die Ausführungsdauer und den Status von insight anzugeben. |
| [!UICONTROL Status] | Zeigt den aktuellen Status der Abfrageausführung an, z. B. `Completed,` `Running,` oder `Failed,`, um das Ergebnis schnell zu bewerten. |
| [!UICONTROL Datasets] | Listet die bei der Abfrageausführung verwendeten Datensätze auf, um anzuzeigen, welche Datenquellen an der Ausführung beteiligt waren. |
| [!UICONTROL Compute Hours] | Zeigt die für jede Abfrageausführung verwendete Berechnungszeit in Stunden. Dies hilft bei der Verfolgung der Ressourcennutzung und der Optimierung der Abfrageleistung. |

{style="table-layout:auto"}

>[!NOTE]
>
>Die Daten zur Stundenberechnung sind ab 08/15/2024 verfügbar. Daten vor diesem Datum werden als „Nicht verfügbar“ angezeigt.

Vollständige Informationen [ Überwachen des Status aller Abfrageaufträge über die Benutzeroberfläche finden ](./monitor-queries.md#inline-actions) im Handbuch zur Überwachung geplanter Abfragen .

Wählen Sie ein **[!UICONTROL Query run ID]** aus der Liste aus, um zur Übersicht über die Abfrageausführung zu navigieren. Eine vollständige Aufschlüsselung der in der (Übersicht über die [) verfügbaren Informationen ](./monitor-queries.md#query-run-overview) Sie in der Dokumentation Überwachen geplanter Abfragen .

Informationen zum Überwachen geplanter Abfragen mithilfe der Abfrage-Service-API finden Sie [Handbuch zu Endpunkten für die Ausführung geplanter Abfragen](../api/runs-scheduled-queries.md).

## Zeitplan aktivieren, deaktivieren oder löschen {#delete-schedule}

Sie können einen Zeitplan im Arbeitsbereich für Zeitpläne einer bestimmten Abfrage oder im Arbeitsbereich [!UICONTROL Scheduled Queries] , in dem alle geplanten Abfragen aufgelistet sind, aktivieren, deaktivieren oder löschen.

Um auf die Registerkarte [!UICONTROL Schedules] der ausgewählten Abfrage zuzugreifen, müssen Sie den Namen einer Abfragevorlage auf der Registerkarte [!UICONTROL Templates] oder der Registerkarte [!UICONTROL Scheduled Queries] auswählen. Dadurch wird zum Abfrage-Editor für diese Abfrage navigiert. Wählen Sie im Abfrage-Editor die Option **[!UICONTROL Schedules]** aus, um auf den Arbeitsbereich für Zeitpläne zuzugreifen.

Wählen Sie einen Zeitplan aus den Zeilen der verfügbaren Zeitpläne aus, um den Detailbereich auszufüllen. Verwenden Sie den Umschalter, um die geplante Abfrage zu deaktivieren (oder zu aktivieren).

### Deaktivierte Abfragen löschen

>[!IMPORTANT]
>
>Sie müssen einen Zeitplan deaktivieren, bevor Sie ihn für eine Abfrage löschen können.

![Die Liste der Zeitpläne einer Vorlage mit hervorgehobenem Detailbereich.](../images/ui/query-schedules/schedule-details-panel.png)

Ein Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Disable]** aus, um die Aktion zu bestätigen.

![Der Bestätigungsdialog zum Deaktivieren des Zeitplans.](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

Wählen Sie **[!UICONTROL Delete a schedule]** aus, um den deaktivierten Zeitplan zu löschen.

![Der Arbeitsbereich für Zeitpläne mit hervorgehobener Option „Zeitplan löschen“.](../images/ui/query-schedules/delete-schedule.png)

Alternativ dazu bietet die Registerkarte [!UICONTROL Scheduled Queries] eine Sammlung von Inline-Aktionen für jede geplante Abfrage. Zu den verfügbaren Inline-Aktionen gehören [!UICONTROL Disable schedule] oder [!UICONTROL Enable schedule], [!UICONTROL Delete schedule] und [!UICONTROL Subscribe] zu Warnhinweisen für die geplante Abfrage. Vollständige Anweisungen zum Löschen oder Deaktivieren einer geplanten Abfrage über die Registerkarte Geplante Abfragen finden Sie im [Handbuch zu geplanten Abfragen überwachen](./monitor-queries.md#inline-actions).
