---
title: Abfragezeitpläne
description: Erfahren Sie, wie Sie geplante Abfrageausführungen automatisieren, einen Abfragezeitplan löschen oder deaktivieren und die verfügbaren Planungsoptionen über die Adobe Experience Platform-Benutzeroberfläche nutzen können.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 0b056da8457010ce36efc48e3dd91f280a9b15c5
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 15%

---

# Abfragepläne

Sie können die Ausführung von Abfragen automatisieren, indem Sie Abfragepläne erstellen. Geplante Abfragen werden in einer benutzerdefinierten Platzierung ausgeführt, um Ihre Daten basierend auf Häufigkeit, Datum und Uhrzeit zu verwalten. Sie können bei Bedarf auch einen Ausgabedatensatz für Ihre Ergebnisse auswählen. Abfragen, die als Vorlage gespeichert wurden, können im Abfrage-Editor geplant werden.

>[!IMPORTANT]
>
>Sie können einen Zeitplan nur zu einer bereits erstellten und gespeicherten Abfrage hinzufügen.

Alle geplanten Abfragen werden der Liste auf der Registerkarte [!UICONTROL Geplante Abfragen] hinzugefügt. Von diesem Arbeitsbereich aus können Sie den Status aller geplanten Abfrageaufträge über die Benutzeroberfläche überwachen. Auf der Registerkarte [!UICONTROL Geplante Abfragen] finden Sie wichtige Informationen zu Ihren Abfrageausführungen und abonnieren Warnungen. Zu den verfügbaren Informationen gehören Status, Planungsdetails und Fehlermeldungen/Codes für den Fall, dass eine Ausführung fehlschlägt. Weitere Informationen finden Sie im Dokument [Terminierte Abfragen überwachen](./monitor-queries.md) .

Dieser Workflow behandelt den Planungsprozess in der Benutzeroberfläche von Query Service. Informationen zum Hinzufügen von Zeitplänen mithilfe der API finden Sie im [Handbuch zu Endpunkten für geplante Abfragen](../api/scheduled-queries.md).

## Erstellen eines Abfragezeitplans {#create-schedule}

Um eine Abfrage zu planen, wählen Sie entweder auf der Registerkarte [!UICONTROL Vorlagen] oder in der Spalte [!UICONTROL Vorlage] der Registerkarte [!UICONTROL Geplante Abfragen] eine Abfragevorlage aus. Durch Auswahl des Vorlagennamen gelangen Sie zum Abfrage-Editor.

Wenn Sie über den Abfrage-Editor auf eine gespeicherte Abfrage zugreifen, können Sie einen Zeitplan für die Abfrage erstellen oder den Zeitplan der Abfrage im Detailbereich anzeigen.

>[!TIP]
>
>Wählen Sie **[!UICONTROL Zeitplan anzeigen]** aus, um zum Arbeitsbereich &quot;Zeitpläne&quot;zu navigieren und geplante Abfragen auf einen Blick anzuzeigen.

![Der Abfrage-Editor, in dem [!UICONTROL Zeitplan anzeigen] und [!UICONTROL Zeitplan hinzufügen] hervorgehoben sind.](../images/ui/query-schedules/view-add-schedule.png)

Wählen Sie **[!UICONTROL Zeitplan hinzufügen]** aus, um zur Seite [Details des Zeitplans](#schedule-details) zu navigieren.

Alternativ können Sie die Registerkarte **[!UICONTROL Zeitpläne]** unter dem Namen der Abfrage auswählen.

![Der Abfrage-Editor mit der hervorgehobenen Registerkarte „Zeitpläne“.](../images/ui/query-schedules/schedules-tab.png)

Der Arbeitsbereich für Zeitpläne wird angezeigt. Die Benutzeroberfläche zeigt eine Liste aller geplanten Ausführungen an, mit denen die Vorlage verknüpft ist. Wählen Sie **[!UICONTROL Zeitplan hinzufügen]** aus, um einen Zeitplan zu erstellen.

![Der Arbeitsbereich „Zeitplan“ des Abfrage-Editors mit hervorgehobener Option „Zeitplan hinzufügen“.](../images/ui/query-schedules/add-schedule.png)

### Hinzufügen von Planungsdetails {#schedule-details}

Die Seite mit den Zeitplandetails wird angezeigt. Auf dieser Seite können Sie verschiedene Details für die geplante Abfrage bearbeiten. Zu den Details gehören die [Häufigkeit und der Wochentag der geplanten Abfrage](#scheduled-query-frequency)-Ausführung, das Start- und Enddatum, der Datensatz, in den die Ergebnisse exportiert werden sollen, und [Warnhinweise zum Abfragestatus](#alerts-for-query-status).

>[!IMPORTANT]
>
>Die Benutzeroberfläche des Abfrageplaners unterstützt keine unbegrenzte oder unbefristete Zeitplanung. Es muss ein Enddatum angegeben werden. Für das Enddatum gibt es keine Obergrenze.

![Das hervorgehobene Bedienfeld „Zeitplandetails“.](../images/ui/query-schedules/schedule-details.png)

#### Geplante Abfragefrequenz {#scheduled-query-frequency}

Für **[!UICONTROL Häufigkeit]** können Sie die folgenden Optionen auswählen:

- **[!UICONTROL Stündlich]**: Die geplante Abfrage wird im ausgewählten Datumsbereich stündlich ausgeführt.
- **[!UICONTROL Täglich]**: Die geplante Abfrage wird alle X Tage zum ausgewählten Zeitpunkt und im ausgewählten Zeitraum ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.
- **[!UICONTROL Wöchentlich]**: Die ausgewählte Abfrage wird an den ausgewählten Wochentagen, zur ausgewählten Uhrzeit und im ausgewählten Datumsbereich ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.
- **[!UICONTROL Monatlich]**: Die ausgewählte Abfrage wird jeden Monat am ausgewählten Tag, zur ausgewählten Uhrzeit und im ausgewählten Datumsbereich ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.
- **[!UICONTROL Jährlich]**: Die ausgewählte Abfrage wird jedes Jahr am ausgewählten Tag, im ausgewählten Monat, zur ausgewählten Uhrzeit und im ausgewählten Datumsbereich ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.

### Bereitstellen von Datensatzdetails {#dataset-details}

Verwalten Sie die Abfrageergebnisse, indem Sie entweder die Daten an einen vorhandenen Datensatz anhängen oder einen neuen Datensatz erstellen und die Daten daran anhängen.

Wählen Sie **[!UICONTROL Erstellen und an neuen Datensatz anhängen]** aus, um einen Datensatz zu erstellen, wenn Sie eine Abfrage zum ersten Mal ausführen. Nachfolgende Ausführungen fügen weiterhin Daten in diesen Datensatz ein. Geben Sie abschließend einen Namen und eine Beschreibung für den Datensatz an.

>[!IMPORTANT]
>
> Da Sie entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen, müssen Sie **weder** `INSERT INTO` noch `CREATE TABLE AS SELECT` als Teil die Abfrage einbeziehen, da die Datensätze bereits festgelegt sind. Das Einbeziehen von `INSERT INTO` oder `CREATE TABLE AS SELECT` als Teil Ihrer geplanten Abfragen führt zu einem Fehler.

![Das Bedienfeld Zeitplandetails mit Datensatzdetails und die Optionen [!UICONTROL Erstellen und Anhängen an neuen Datensatz] wurden hervorgehoben.](../images/ui/query-schedules/dataset-details-create-and-append.png)

Wählen Sie alternativ **[!UICONTROL In vorhandenen Datensatz anhängen]** und danach das Datensatzsymbol (![Das Datensatzsymbol.](../images/ui/query-schedules/dataset-icon.png)).

![Das Bedienfeld &quot;Zeitplandetails&quot;mit Datensatzdetails und &quot;An vorhandenen Datensatz anhängen&quot;wurde hervorgehoben.](../images/ui/query-schedules/dataset-details-existing.png)

Das Dialogfeld **[!UICONTROL Ausgabedatensatz auswählen]** wird angezeigt.

Navigieren Sie anschließend entweder zu den vorhandenen Datensätzen oder verwenden Sie das Suchfeld, um die Optionen zu filtern. Wählen Sie die Zeile des Datensatzes aus, die Sie verwenden möchten. Die Datensatzdetails werden im Bereich auf der rechten Seite angezeigt. Wählen Sie **[!UICONTROL Fertig]** aus, um Ihre Auswahl zu bestätigen.

![Das Dialogfeld Ausgabedatensatz auswählen mit dem Suchfeld, einer Datensatzzeile und hervorgehoben Fertig .](../images/ui/query-schedules/select-output-dataset-dialog.png)

### Abfragen in Quarantäne stellen, wenn sie ständig fehlschlagen {#quarantine}

Bei der Erstellung eines Zeitplans können Sie Ihre Abfrage in der Quarantänefunktion registrieren, um Systemressourcen zu schützen und potenzielle Unterbrechungen zu vermeiden. Die Quarantänefunktion identifiziert und isoliert Abfragen, die wiederholt fehlschlagen, automatisch, indem sie sie in den Status [!UICONTROL In Quarantäne] versetzt. Durch Quarantäne von Abfragen nach zehn aufeinander folgenden Fehlern können Sie Probleme eingreifen, überprüfen und beheben, bevor Sie weitere Ausführungen zulassen. Dies hilft Ihnen bei der Aufrechterhaltung Ihrer betrieblichen Effizienz und Datenintegrität.

![Der Arbeitsbereich &quot;Zeitpläne für Abfragen&quot;, in dem [!UICONTROL Quarantäne für Abfragen] hervorgehoben und &quot;Ja&quot;ausgewählt ist.](../images/ui/query-schedules/quarantine-enroll.png)

Nachdem eine Abfrage für die Quarantänefunktion registriert wurde, können Sie Warnhinweise für diese Änderung des Abfragestatus abonnieren. Wenn eine geplante Abfrage nicht unter Quarantäne gestellt wird, wird sie nicht als Option im Dialogfeld &quot;Warnhinweise&quot;](./monitor-queries.md#alert-subscription) angezeigt.[

Sie können auch eine geplante Abfrage über die Inline-Aktionen auf der Registerkarte [!UICONTROL Geplante Abfragen] in die Quarantänefunktion eintragen. Weitere Informationen finden Sie in der Dokumentation zu [Monitorabfragen](./monitor-queries.md#alert-subscription) .

### Warnhinweise für den Status einer geplanten Abfrage festlegen {#alerts-for-query-status}

Sie können im Rahmen Ihrer geplanten Abfrageeinstellungen auch Abfragewarnungen abonnieren. Sie können Ihre Einstellungen so konfigurieren, dass Benachrichtigungen für eine Vielzahl von Situationen empfangen werden. Warnhinweise können für einen Quarantänestatus, Verzögerungen bei der Abfrageverarbeitung oder eine Statusänderung Ihrer Abfrage festgelegt werden. Zu den verfügbaren Warnungsoptionen für den Abfragestatus gehören Start, Erfolg und Fehler. Warnhinweise können entweder als Popup-Benachrichtigungen oder E-Mails empfangen werden. Aktivieren Sie das Kontrollkästchen, um Warnhinweise für diesen Status der geplanten Abfrage zu abonnieren.

![Das Bedienfeld Zeitplandetails mit hervorgehobenen Warnhinweisoptionen.](../images/ui/query-editor/alerts.png)

In der folgenden Tabelle werden die unterstützten Abfragewarnungstypen erläutert:

| Warnhinweistyp | Beschreibung |
|---|---|
| `start` | Dieser Warnhinweis benachrichtigt Sie, wenn eine geplante Abfrage gestartet wird oder mit der Verarbeitung beginnt. |
| `success` | Dieser Warnhinweis informiert Sie darüber, wenn eine geplante Abfrage erfolgreich ausgeführt wurde, und zeigt an, dass die Abfrage fehlerfrei ausgeführt wurde. |
| `failed` | Dieser Warnhinweis wird Trigger, wenn eine geplante Abfrage einen Fehler auftritt oder nicht erfolgreich ausgeführt werden kann. Dies hilft Ihnen, Probleme schnell zu identifizieren und zu beheben. |
| `quarantine` | Dieser Warnhinweis wird aktiviert, wenn eine geplante Abfrage unter Quarantäne gestellt wird. Sobald eine Abfrage [in die Quarantänefunktion ](#quarantine) aufgenommen wurde, wird jede geplante Abfrage, bei der zehn aufeinander folgende Ausführungen fehlschlagen, automatisch in den Status [!UICONTROL In Quarantäne] versetzt. Eine in Quarantäne befindliche Abfrage erfordert Ihre Intervention, bevor weitere Ausführungen durchgeführt werden können. Hinweis: Für die Quarantänefunktion müssen Abfragen registriert werden, damit Sie Benachrichtigungen unter Quarantäne stellen können. |
| `delay` | Dieser Warnhinweis benachrichtigt Sie, wenn das Ergebnis einer geplanten Abfrageausführung ](./monitor-queries.md#query-run-delay) eine [Verzögerung über einen festgelegten Schwellenwert hinaus aufweist. Sie können einen benutzerdefinierten Zeitpunkt festlegen, zu dem die Warnung Trigger wird, wenn die Abfrage für diesen Zeitraum ausgeführt wird, ohne dass ein Abschluss oder ein Fehler auftritt. Das Standardverhalten setzt einen Warnhinweis für 150 Minuten, nachdem die Verarbeitung der Abfrage begonnen hat. |

>[!NOTE]
>
>Wenn Sie einen Warnhinweis für die [!UICONTROL Verzögerung bei der Abfrage] festlegen, müssen Sie die gewünschte Verzögerungszeit in Minuten in der Platform-Benutzeroberfläche festlegen. Geben Sie die Dauer in Minuten ein. Die maximale Verzögerung beträgt 24 Stunden (1440 Minuten).

Einen Überblick über Warnhinweise in Adobe Experience Platform, einschließlich der Definition von Warnregeln, finden Sie in der [Warnhinweisübersicht](../../observability/alerts/overview.md). Eine Anleitung zum Verwalten von Warnhinweisen und Warnregeln in der Adobe Experience Platform-Benutzeroberfläche finden Sie im Handbuch zur Benutzeroberfläche von [Warnhinweisen](../../observability/alerts/ui.md).

### Festlegen von Parametern für eine geplante parametrisierte Abfrage {#set-parameters}

>[!IMPORTANT]
>
>Die parametrisierte Abfragebenutzeroberfläche-Funktion ist derzeit nur in einer **limitierten Version** verfügbar und steht nicht allen Kunden zur Verfügung. Wenn Sie keinen Zugriff auf parametrierte Abfragen haben, fahren Sie mit dem Abschnitt [Löschen oder Deaktivieren eines Zeitplans](#delete-schedule) fort.

Wenn Sie eine geplante Abfrage für eine parametrisierte Abfrage erstellen, müssen Sie jetzt die Parameterwerte für diese Abfrageausführungen festlegen.

![Der Abschnitt &quot;Details planen&quot;des Workflows zur Planerstellung mit dem Abschnitt Abfrageparameter ist hervorgehoben.](../images/ui/query-schedules/scheduled-query-parameter.png)

Nachdem Sie Ihre Planungsdetails bestätigt haben, wählen Sie **[!UICONTROL Speichern]** aus, um einen Zeitplan zu erstellen. Sie werden zum Tab Zeitpläne Ihrer Vorlage zurückgeleitet. In diesem Arbeitsbereich werden Details zum neu erstellten Zeitplan angezeigt, einschließlich der Zeitplan-ID, des Zeitplans selbst und des Ausgabedatensatzes des Zeitplans.

## Geplante Abfrageausführungen anzeigen {#scheduled-query-runs}

Wählen Sie auf der Registerkarte [!UICONTROL Zeitpläne] Ihrer Vorlage die Zeitplan-ID aus, um zur Liste der Abfrageausführungen für Ihre neu geplante Abfrage zu navigieren.

![Der Arbeitsbereich für Zeitpläne mit dem hervorgehobenen neu erstellten Zeitplan.](../images/ui/query-schedules/schedules-workspace.png)

Alternativ können Sie eine Liste der geplanten Ausführungen einer Abfragevorlage anzeigen, indem Sie zur Registerkarte **[!UICONTROL Geplante Abfragen]** navigieren und einen Vorlagennamen aus der verfügbaren Liste auswählen.

![ Die Registerkarte &quot;Geplante Abfragen&quot;, auf der eine benannte Vorlage hervorgehoben ist.](../images/ui/query-schedules/view-scheduled-runs.png)

Die Liste der ausgeführten Abfragen für diese geplante Abfrage wird angezeigt.

![Der Detailabschnitt des Arbeitsbereichs &quot;Geplante Abfragen&quot;mit einer Liste von Abfragen wird für eine geplante Abfrage hervorgehoben.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Vollständige Informationen zum Überwachen des Status aller Abfrageaufträge über die Benutzeroberfläche finden Sie im Leitfaden [Geplante abgefragte Abfragen überwachen](./monitor-queries.md#inline-actions) .

Wählen Sie eine **[!UICONTROL Kennung der Abfrage-Ausführung]** aus der Liste aus, um zur Übersicht der Abfrageausführung zu navigieren. Eine vollständige Aufschlüsselung der Informationen, die in der [Übersicht über die Abfrageausführung](./monitor-queries.md#query-run-overview) verfügbar sind, finden Sie in der Dokumentation zu geplanten Abfragen zur Überwachung .

Informationen zum Überwachen geplanter Abfragen mithilfe der Query Service-API finden Sie im Handbuch [geplante Abfrage-Run-Endpunkte](../api/runs-scheduled-queries.md) .

## Zeitplan aktivieren, deaktivieren oder löschen {#delete-schedule}

Sie können einen Zeitplan im Arbeitsbereich Zeitpläne einer bestimmten Abfrage oder im Arbeitsbereich [!UICONTROL Geplante Abfragen] aktivieren, deaktivieren oder löschen, in dem alle geplanten Abfragen aufgelistet werden.

Um auf die Registerkarte [!UICONTROL Zeitpläne] Ihrer ausgewählten Abfrage zuzugreifen, müssen Sie den Namen einer Abfragevorlage auf der Registerkarte [!UICONTROL Vorlagen] oder auf der Registerkarte [!UICONTROL Geplante Abfragen] auswählen. Dadurch wird zum Abfrage-Editor für diese Abfrage navigiert. Wählen Sie im Abfrage-Editor **[!UICONTROL Zeitpläne]** aus, um auf den Arbeitsbereich &quot;Zeitpläne&quot;zuzugreifen.

Wählen Sie einen Zeitplan aus den Zeilen der verfügbaren Zeitpläne aus, um den Detailbereich zu füllen. Verwenden Sie den Umschalter, um die geplante Abfrage zu deaktivieren (oder zu aktivieren).

### Löschen deaktivierter Abfragen

>[!IMPORTANT]
>
>Sie müssen einen Zeitplan deaktivieren, bevor Sie ihn für eine Abfrage löschen können.

![Die Liste der Zeitpläne einer Vorlage mit hervorgehobenem Detailbereich.](../images/ui/query-schedules/schedule-details-panel.png)

Ein Bestätigungsdialogfeld wird angezeigt. Wählen Sie **[!UICONTROL Deaktivieren]** aus, um die Aktion zu bestätigen.

![Das Dialogfeld Planungsbestätigung deaktivieren](../images/ui/query-schedules/disable-schedule-confirmation-dialog.png)

Wählen Sie **[!UICONTROL Zeitplan löschen]** aus, um den deaktivierten Zeitplan zu löschen.

![Der Arbeitsbereich &quot;Zeitpläne&quot;mit hervorgehobenem Löschplan.](../images/ui/query-schedules/delete-schedule.png)

Alternativ bietet die Registerkarte [!UICONTROL Geplante Abfragen] eine Sammlung von Inline-Aktionen für jede geplante Abfrage. Zu den verfügbaren Inline-Aktionen gehören [!UICONTROL Zeitplan deaktivieren] oder [!UICONTROL Zeitplan aktivieren], [!UICONTROL Zeitplan löschen] und [!UICONTROL Abonnieren] , um Warnhinweise für die geplante Abfrage anzuzeigen. Vollständige Anweisungen zum Löschen oder Deaktivieren einer geplanten Abfrage über die Registerkarte &quot;Geplante Abfragen&quot;finden Sie im Handbuch [Geplante Abfrage überwachen](./monitor-queries.md#inline-actions) .
