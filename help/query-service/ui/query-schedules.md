---
title: Abfragezeitpläne
description: Erfahren Sie, wie Sie geplante Abfrageausführungen automatisieren, einen Abfragezeitplan löschen oder deaktivieren und die verfügbaren Planungsoptionen über die Adobe Experience Platform-Benutzeroberfläche nutzen können.
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 7d2027bf315ae6e354c906e4aabf6371a92e4148
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 39%

---

# Abfragepläne

Sie können die Ausführung von Abfragen automatisieren, indem Sie Abfragepläne erstellen. Geplante Abfragen werden in einer benutzerdefinierten Platzierung ausgeführt, um Ihre Daten basierend auf Häufigkeit, Datum und Uhrzeit zu verwalten. Sie können bei Bedarf auch einen Ausgabedatensatz für Ihre Ergebnisse auswählen. Abfragen, die als Vorlage gespeichert wurden, können im Abfrage-Editor geplant werden.

>[!IMPORTANT]
>
>Sie können einen Zeitplan nur zu einer Abfrage hinzufügen, die bereits erstellt, gespeichert und ausgeführt wurde.

Alle geplanten Abfragen werden der Liste im [!UICONTROL Geplante Abfragen] Registerkarte. Von diesem Arbeitsbereich aus können Sie den Status aller geplanten Abfrageaufträge über die Benutzeroberfläche überwachen. Im [!UICONTROL Geplante Abfragen] finden Sie wichtige Informationen zu Ihren Abfrageausführungen und abonnieren Warnungen. Zu den verfügbaren Informationen gehören Status, Planungsdetails und Fehlermeldungen/Codes für den Fall, dass eine Ausführung fehlschlägt. Siehe [Dokument zur Überwachung geplanter Abfragen](./monitor-queries.md) für weitere Informationen.

Dieser Workflow behandelt den Planungsprozess in der Benutzeroberfläche von Query Service. Informationen zum Hinzufügen von Zeitplänen mithilfe der API finden Sie im [Handbuch zu Endpunkten für geplante Abfragen](../api/scheduled-queries.md).

## Erstellen eines Abfragezeitplans {#create-schedule}

Um eine Abfrage zu planen, wählen Sie eine Abfragevorlage aus dem [!UICONTROL Vorlagen] oder [!UICONTROL Vorlage] Spalte [!UICONTROL Geplante Abfragen] Registerkarte. Durch Auswahl des Vorlagennamen gelangen Sie zum Abfrage-Editor.

Wenn Sie über den Abfrage-Editor auf eine gespeicherte Abfrage zugreifen, können Sie einen Zeitplan für die Abfrage erstellen oder den Zeitplan der Abfrage im Detailbereich anzeigen.

>[!TIP]
>
>Auswählen **[!UICONTROL Zeitplan anzeigen]** um zum Arbeitsbereich &quot;Zeitpläne&quot;zu navigieren und geplante Abfragen auf einen Blick anzuzeigen.

![Der Abfrage-Editor mit [!UICONTROL Zeitplan anzeigen] und [!UICONTROL Zeitplan hinzufügen] hervorgehoben.](../images/ui/query-schedules/view-add-schedule.png)

Auswählen **[!UICONTROL Zeitplan hinzufügen]** , um zur [Seite mit Zeitplandetails](#schedule-details).

Alternativ können Sie die **[!UICONTROL Zeitpläne]** unter dem Namen der Abfrage klicken.

![Der Abfrage-Editor mit der hervorgehobenen Registerkarte „Zeitpläne“.](../images/ui/query-schedules/schedules-tab.png)

Der Arbeitsbereich für Zeitpläne wird angezeigt. Wählen Sie **[!UICONTROL Zeitplan hinzufügen]** aus, um einen Zeitplan zu erstellen.

![Der Arbeitsbereich „Zeitplan“ des Abfrage-Editors mit hervorgehobener Option „Zeitplan hinzufügen“.](../images/ui/query-schedules/add-schedule.png)

### Planungsdetails bearbeiten {#schedule-details}

Die Seite mit den Zeitplandetails wird angezeigt. Auf dieser Seite können Sie die Häufigkeit der geplanten Abfrage, das Start- und Enddatum, den Wochentag, an dem die geplante Abfrage ausgeführt wird, sowie den zu exportierenden Datensatz auswählen.

![Das hervorgehobene Bedienfeld „Zeitplandetails“.](../images/ui/query-schedules/schedule-details.png)

Für **[!UICONTROL Häufigkeit]** können Sie die folgenden Optionen auswählen:

- **[!UICONTROL Stündlich]**: Die geplante Abfrage wird im ausgewählten Datumsbereich stündlich ausgeführt.
- **[!UICONTROL Täglich]**: Die geplante Abfrage wird alle X Tage zum ausgewählten Zeitpunkt und im ausgewählten Zeitraum ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.
- **[!UICONTROL Wöchentlich]**: Die ausgewählte Abfrage wird an den ausgewählten Wochentagen, zur ausgewählten Uhrzeit und im ausgewählten Datumsbereich ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.
- **[!UICONTROL Monatlich]**: Die ausgewählte Abfrage wird jeden Monat am ausgewählten Tag, zur ausgewählten Uhrzeit und im ausgewählten Datumsbereich ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.
- **[!UICONTROL Jährlich]**: Die ausgewählte Abfrage wird jedes Jahr am ausgewählten Tag, im ausgewählten Monat, zur ausgewählten Uhrzeit und im ausgewählten Datumsbereich ausgeführt. Beachten Sie, dass die ausgewählte Zeit in **UTC** angegeben ist, nicht in Ihrer lokalen Zeitzone.

Für den Ausgabedatensatz haben Sie die Möglichkeit, entweder an einen vorhandenen Datensatz angehängt oder einen neuen Datensatz zu erstellen und anzuhängen. Die zweite Option bedeutet, dass bei der erstmaligen Ausführung einer Abfrage und der Erstellung eines Datensatzes alle nachfolgenden Ausführungen die Daten in diesen Datensatz einfügen.

>[!IMPORTANT]
>
> Da Sie entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen, müssen Sie **weder** `INSERT INTO` noch `CREATE TABLE AS SELECT` als Teil die Abfrage einbeziehen, da die Datensätze bereits festgelegt sind. Das Einbeziehen von `INSERT INTO` oder `CREATE TABLE AS SELECT` als Teil Ihrer geplanten Abfragen führt zu einem Fehler.

Wenn Sie keinen Zugriff auf parametrierte Abfragen haben, fahren Sie mit dem [Zeitplan löschen oder deaktivieren](#delete-schedule) Abschnitt.

### Festlegen von Parametern für eine geplante parametrisierte Abfrage {#set-parameters}

>[!IMPORTANT]
>
>Die Funktion der parametrisierten Abfragebenutzeroberfläche ist derzeit in einer **Nur begrenzte Version** und ist nicht für alle Kunden verfügbar.

Wenn Sie eine geplante Abfrage für eine parametrisierte Abfrage erstellen, müssen Sie jetzt die Parameterwerte für diese Abfrageausführungen festlegen.

![Der Abschnitt Planungsdetails des Workflows zur Planerstellung mit dem Abschnitt Abfrageparameter wurde hervorgehoben.](../images/ui/query-schedules/scheduled-query-parameter.png)

Nachdem Sie alle diese Details geprüft haben, wählen Sie **[!UICONTROL Speichern]** aus, um einen Zeitplan zu erstellen. Sie werden zum Arbeitsbereich für Zeitpläne zurückgeleitet, der Details zum neu erstellten Zeitplan anzeigt, darunter die Zeitplan-ID, den Zeitplan selbst und den Ausgabedatensatz des Zeitplans. Sie können die Zeitplan-ID verwenden, um weitere Informationen zu den Ausführungen der geplanten Abfrage selbst zu erhalten. Weitere Informationen finden Sie im [Handbuch zu Endpunkten für die Ausführung geplanter Abfragen](../api/runs-scheduled-queries.md).

![Der Arbeitsbereich für Zeitpläne mit dem hervorgehobenen neu erstellten Zeitplan.](../images/ui/query-schedules/schedules-workspace.png)

## Geplante Abfrageausführungen anzeigen {#scheduled-query-runs}

Um eine Liste der geplanten Ausführungen einer Abfragevorlage anzuzeigen, navigieren Sie zum [!UICONTROL Geplante Abfragen] und wählen Sie einen Vorlagennamen aus der verfügbaren Liste aus.

![Die Registerkarte Geplante Abfragen mit einer benannten Vorlage wurde hervorgehoben.](../images/ui/query-schedules/view-scheduled-runs.png)

Die Liste der ausgeführten Abfragen für diese geplante Abfrage wird angezeigt.

![Der Detailabschnitt des Arbeitsbereichs Geplante Abfragen mit einer Liste von Abfragen wird für eine geplante Abfrage hervorgehoben.](../images/ui/query-schedules/list-of-scheduled-runs.png)

Siehe [Handbuch zur Überwachung geplanter Abfragen](./monitor-queries.md#inline-actions) für vollständige Informationen zur Überwachung des Status aller Abfrageaufträge über die Benutzeroberfläche.

## Löschen oder Deaktivieren eines Zeitplans {#delete-schedule}

Sie können einen Zeitplan im Arbeitsbereich Zeitpläne einer bestimmten Abfrage oder im [!UICONTROL Geplante Abfragen] Arbeitsbereich, der alle geplanten Abfragen auflistet.

So greifen Sie auf die [!UICONTROL Zeitpläne] im Tab der von Ihnen ausgewählten Abfrage den Namen einer Abfragevorlage aus dem [!UICONTROL Vorlagen] oder [!UICONTROL Geplante Abfragen] Registerkarte. Dadurch wird zum Abfrage-Editor für diese Abfrage navigiert. Wählen Sie im Abfrage-Editor **[!UICONTROL Zeitpläne]** , um auf den Arbeitsbereich Zeitpläne zuzugreifen.

Wählen Sie einen Zeitplan aus den Zeilen der verfügbaren Zeitpläne aus. Sie können den Umschalter verwenden, um die geplante Abfrage zu deaktivieren oder zu aktivieren.

>[!IMPORTANT]
>
>Sie müssen einen Zeitplan deaktivieren, bevor Sie ihn für eine Abfrage löschen können.

Wählen Sie **[!UICONTROL Zeitplan löschen]** aus, um den deaktivierten Zeitplan zu löschen.

![Der Arbeitsbereich „Zeitpläne“ mit den hervorgehobenen Optionen „Zeitplan deaktivieren“ und „Zeitplan löschen“.](../images/ui/query-schedules/delete-schedule.png)

Alternativ kann die Variable [!UICONTROL Geplante Abfragen] bietet eine Sammlung von Inline-Aktionen für jede geplante Abfrage. Zu den verfügbaren Inline-Aktionen gehören [!UICONTROL Zeitplan deaktivieren] oder [!UICONTROL Zeitplan aktivieren], [!UICONTROL Zeitplan löschen], und [!UICONTROL Abonnieren] auf Warnhinweise für die geplante Abfrage. Vollständige Anweisungen zum Löschen oder Deaktivieren einer geplanten Abfrage über die Registerkarte &quot;Geplante Abfragen&quot;finden Sie in der [Handbuch zur Überwachung geplanter Abfragen](./monitor-queries.md#inline-actions).
