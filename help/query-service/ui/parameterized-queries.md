---
title: Parameterisierte Abfragen
description: Erfahren Sie, wie Sie parametrisierte Abfragen in der Adobe Experience Platform-Benutzeroberfläche verwenden.
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: a78f7499b55dcedbe379e917b94946948c66e6e5
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 12%

---

# Parametrierte Abfragen {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Parametrierte Abfragen"
>abstract="Verwenden Sie parametrierte Abfragen, um zum Zeitpunkt der Ausführung Parameterwerte hinzuzufügen. Auf diese Weise können Sie mit dynamischen Daten arbeiten und Abfragen für unterschiedliche Anwendungsfälle wiederverwenden. Verwenden Sie den `'$'`-Vorspann, um einen Abfrageparameter in Ihre Abfrage im Texteditor einzugeben. Fügen Sie anschließend im Abschnitt „Abfrageparameter“ unter dem Editor einen Wert für den Schlüssel hinzu."

Query Service unterstützt die Verwendung parametrisierter Abfragen im Abfrage-Editor. Bei parametrierten Abfragen können Sie jetzt Platzhalter für Parameter verwenden und die Parameterwerte zur Ausführungszeit hinzufügen. Mit Platzhaltern können Sie mit dynamischen Daten arbeiten, bei denen Sie nicht wissen, welche Werte verwendet werden, bis die Anweisung ausgeführt wird. Sie können Ihre Abfragen auch vorzeitig vorbereiten und für ähnliche Zwecke wiederverwenden. Die Wiederverwendung von Abfragen erspart Ihnen erheblichen Aufwand, da Sie die Erstellung eigener SQL-Abfragen für jeden Anwendungsfall vermeiden.

## Voraussetzungen

Lesen Sie vor dem Fortfahren mit diesem Handbuch die [Anleitung zur Benutzeroberfläche des Abfrage-Editors](./user-guide.md). Das Handbuch zum Abfrage-Editor enthält detaillierte Informationen zum Schreiben, Überprüfen und Ausführen von Abfragen für Kundenerlebnisdaten in der Experience Platform-Benutzeroberfläche.

>[!NOTE]
>
>In der Adobe Experience Platform-Benutzeroberfläche werden parametrisierte Abfragen nur auf der übergeordneten Ebene von Inline-Vorlagen unterstützt. Dies bedeutet, dass parametrisierte Abfragen nur bei Verwendung in der ursprünglichen Vorlage funktionieren. Untergeordnete Vorlagen müssen eine statische Vorlage sein und dürfen keine dynamischen Parameter aufweisen. Siehe [Dokumentation zu Inline-Vorlagen](../essential-concepts/inline-templates.md) , um mehr zu erfahren.

## Parametrisierte Abfragesyntax {#syntax}

Parametrisierte Abfragen verwenden das Format `'$YOUR_PARAMETER_NAME'` und können mit Punktnotation verkettet werden. Nachfolgend finden Sie ein Beispiel für eine SQL-Anweisung, die parametrisierte Abfragen verwendet.

```sql
INSERT INTO
   $Database_Name.Schema_Name.adwh_lkup_process_delta_log
   (process_name, merge_policy_id, process_status, process_date, create_ts, change_ts)
SELECT
   '$Table_Process_Name' process_name,
   hash('$Merge_PolicyID') merge_policy_id,
   '$process_status' process_status,
   to_date('$date_key') process_date,
   CURRENT_TIMESTAMP create_ts,
   CURRENT_TIMESTAMP change_ts;
```

## Eine parametrierte Abfrage erstellen {#create}

Um Ihre parametrisierte Abfrage in der Benutzeroberfläche zu erstellen, navigieren Sie zum Abfrage-Editor. Siehe Abschnitt zu [Zugriff auf den Abfrage-Editor](./user-guide.md#accessing-query-editor) für weitere Anweisungen.

Verwenden Sie den `'$'`-Vorspann, um einen Abfrageparameter in Ihre Abfrage im Texteditor einzugeben. Fügen Sie als Nächstes den fehlenden Wert für den Schlüssel im [!UICONTROL Abfrageparameter] Abschnitt unterhalb des Editors. Die Abfrage kann nicht ausgeführt werden, wenn Sie keinem der erforderlichen Schlüssel einen Wert hinzufügen. Ein Warnsymbol (![Ein Warnsymbol.](../images/ui/parameterized-queries/alert-icon.png)) im Abschnitt &quot;Abfrageparameter&quot;neben allen leeren [!UICONTROL Wert] Eingabefelder.

![Der Abfrage-Editor mit einer parametrisierten Abfrage und der Abschnitt Abfrageparameter wurden hervorgehoben.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Ändern von Registerkarten aus [!UICONTROL Abfrageparameter] nach [!UICONTROL Konsole] , um die Konsolenausgabe der Abfrage anzuzeigen.

Wenn Sie einen Parameter entfernen und versuchen, die Abfrage erneut auszuführen, nachdem sie bereits ausgeführt wurde, wird im [!UICONTROL Abfrageparameter] -Bereich, um Sie zu warnen.

>[!NOTE]
>
>Wenn für Ihre Abfrage keine Parameter verwendet werden, können Sie im Abfrage-Editor weiterhin unnötige Parameter eingeben. Der Abfrage-Editor ignoriert alle unnötigen Schlüssel-Wert-Paare und hat keine Auswirkungen auf die Ausführung oder die Ergebnisse der Abfrage.

![Der Abfrage-Editor mit einem leeren Wertefeld und der Abfrageparameter-Fehler hervorgehoben.](../images/ui/parameterized-queries/query-parameter-error.png)

## Verwenden Sie die Details der Abfrageprotokolle, um Parameterwerte zu überprüfen. {#check-parameter-values}

Parameter können nicht in Vorlagen gespeichert werden, da die verwendeten Werte nicht persistent sind. Sie können jedoch die [!UICONTROL Details zum Abfrage-Protokoll] -Seite, um die Parameterwerte zu finden, die in einem Abfrageablauf verwendet werden. In diesem Fall zeigen die Protokolle nicht an, dass es sich bei der Abfrage um eine parametrisierte Abfrage handelte. Siehe [Dokumentation zu Abfrageprotokollen](./query-logs.md) für Anweisungen zum Auffinden der verwendeten Werte.

![Die Ansicht der Abfrageprotokolle mit der SQL-Adresse einer parametrisierten Abfrage, die im Detailabschnitt hervorgehoben ist.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Eine parametrisierte Abfrage planen {#schedule}

Die Parameterwerte werden gespeichert, wenn Sie eine parametrisierte Abfrage planen. Um eine parametrisierte Abfrage zu planen, folgen Sie dem typischen Prozess, um eine geplante Abfrage zu erstellen, wie im Handbuch zu [Abfragezeitplan erstellen](./query-schedules.md#create-schedule)und geben Sie dann die Parameterwerte ein, die im Abfrageablauf verwendet werden sollen. Dieser UI-Abschnitt wird nur für parametrierte Abfragen angezeigt. Siehe Abschnitt zu [Festlegen von Parametern für eine geplante parametrisierte Abfrage](./query-schedules.md#set-parameters) für spezifische Anweisungen.

>[!TIP]
>
>Query Service unterstützt vorbereitete Anweisungen durch die Verwendung parametrisierter Abfragen. Siehe [Syntaxhandbuch für vorbereitete Anweisungen](../sql/prepared-statements.md) für weitere Informationen zur SQL-Syntax.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie gelernt, wie Sie Abfragen in der Adobe Experience Platform-Benutzeroberfläche parametrisieren und in geplanten Abfragemöglichkeiten verwenden können. In dem Dokument wurde auch hervorgehoben, wie die Protokolle auf die in Abfrageausführungen verwendeten Parameterwerte überprüft werden können.

Als Nächstes sollten Sie das Handbuch lesen unter [Überwachung geplanter Abfragen](./monitor-queries.md) , um über die Platform-Benutzeroberfläche ein besseres Verständnis des Status aller Abfrageaufträge zu erhalten.
