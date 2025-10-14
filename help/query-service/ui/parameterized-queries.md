---
title: Parametrisierte Abfragen
description: Erfahren Sie, wie Sie parametrisierte Abfragen in der Adobe Experience Platform-Benutzeroberfläche verwenden.
exl-id: 5c5ac691-5e29-4262-ba53-84dcc56e744f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 13%

---

# Parametrierte Abfragen {#parameterized-queries}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_parameterizedQueries"
>title="Parametrierte Abfragen"
>abstract="Verwenden Sie parametrierte Abfragen, um zum Zeitpunkt der Ausführung Parameterwerte hinzuzufügen. Auf diese Weise können Sie mit dynamischen Daten arbeiten und Abfragen für unterschiedliche Anwendungsfälle wiederverwenden. Verwenden Sie den `'$'`-Vorspann, um einen Abfrageparameter in Ihre Abfrage im Texteditor einzugeben. Fügen Sie anschließend im Abschnitt „Abfrageparameter“ unter dem Editor einen Wert für den Schlüssel hinzu."

Query Service unterstützt die Verwendung parametrisierter Abfragen im Abfrage-Editor. Bei parametrisierten Abfragen können Sie jetzt Platzhalter für Parameter verwenden und die Parameterwerte zur Ausführungszeit hinzufügen. Platzhalter ermöglichen es Ihnen, mit dynamischen Daten zu arbeiten, bei denen Sie die Werte erst dann kennen, wenn die Anweisung ausgeführt wird. Sie können Ihre Abfragen auch vorab vorbereiten und für ähnliche Zwecke wiederverwenden. Die Wiederverwendung von Abfragen spart viel Aufwand, da Sie für jeden Anwendungsfall keine separaten SQL-Abfragen erstellen müssen.

## Voraussetzungen

Bevor Sie mit diesem Handbuch fortfahren, lesen Sie das [Handbuch zur Benutzeroberfläche des Abfrage-Editors](./user-guide.md). Das Handbuch zum Abfrage-Editor enthält detaillierte Informationen zum Schreiben, Validieren und Ausführen von Abfragen für Kundenerlebnisdaten in der Benutzeroberfläche von Experience Platform.

>[!NOTE]
>
>In der Adobe Experience Platform-Benutzeroberfläche werden parametrisierte Abfragen nur auf der übergeordneten Ebene von Inline-Vorlagen unterstützt. Dies bedeutet, dass parametrisierte Abfragen nur bei Verwendung in der ursprünglichen Vorlage funktionieren. Untergeordnete Vorlagen müssen eine statische Vorlage sein und dürfen keine dynamischen Parameter enthalten. Weitere Informationen finden [&#x200B; in der Dokumentation &#x200B;](../key-concepts/inline-templates.md) Inline-Vorlagen .

## Parametrisierte Abfragesyntax {#syntax}

Parametrisierte Abfragen verwenden das Format `'$YOUR_PARAMETER_NAME'` und können mit der Punktnotation verkettet werden. Nachfolgend finden Sie eine Beispiel-SQL-Anweisung, die parametrisierte Abfragen verwendet.

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

## Erstellen einer parametrisierten Abfrage {#create}

Um Ihre parametrisierte Abfrage in der Benutzeroberfläche zu erstellen, navigieren Sie zum Abfrage-Editor. Weitere Anweisungen finden Sie im Abschnitt [Zugriff auf den Abfrage](./user-guide.md#accessing-query-editor)Editor).

Verwenden Sie den `'$'`-Vorspann, um einen Abfrageparameter in Ihre Abfrage im Texteditor einzugeben. Wählen Sie anschließend die Registerkarte **[!UICONTROL Abfrageparameter]** neben der [!UICONTROL Konsole] und fügen Sie den fehlenden Wert für den Schlüssel hinzu. Die Abfrage kann nicht ausgeführt werden, wenn Sie versäumen, einem der erforderlichen Schlüssel einen Wert hinzuzufügen. Ein Warnhinweissymbol (![Warnhinweissymbol.](/help/images/icons/alert.png)) im Abschnitt Abfrageparameter neben leeren Eingabefeldern [!UICONTROL Wert] angezeigt.

>[!NOTE]
>
>Wenn Ihre Abfrage keine Parameter akzeptiert, können Sie im Abfrage-Editor dennoch unnötige Parameter eingeben. Der Abfrage-Editor ignoriert alle unnötigen Schlüssel-Wert-Paare und sie haben keine Auswirkungen auf die Ausführung oder das Ergebnis der Abfrage.

![Der Abfrage-Editor mit einer parametrisierten Abfrage und dem hervorgehobenen Abschnitt „Abfrageparameter“.](../images/ui/parameterized-queries/parameterized-query.png)

>[!TIP]
>
>Ändern Sie die Registerkarten von [!UICONTROL Abfrageparameter] in [!UICONTROL Konsole], um die Konsolenausgabe der Abfrage anzuzeigen.

## Verwenden Sie Details der Abfrageprotokolle, um Parameterwerte zu überprüfen {#check-parameter-values}

Sie können keine Parameter in Vorlagen speichern, da die verwendeten Werte nicht persistent sind. Sie können jedoch die Seite [!UICONTROL Details zum Abfrageprotokoll] überprüfen, um die in einer Abfrageausführung verwendeten Parameterwerte zu finden. In diesem Fall geben die Protokolle nicht an, dass die Abfrage eine parametrisierte Abfrage war. Anweisungen [&#x200B; Ermitteln der verwendeten Werte finden Sie &#x200B;](./query-logs.md) der Dokumentation zu Abfrageprotokollen .

![Die Ansicht mit den Abfrageprotokollen, wobei der SQL-Code einer parametrisierten Abfrage im Detailabschnitt hervorgehoben ist.](../images/ui/parameterized-queries/parameterized-query-logs.png)

<!-- improve screenshot above ^ I am waiting for a scheduled run to complete -->

## Planen einer parametrisierten Abfrage {#schedule}

Parameterwerte werden gespeichert, wenn Sie eine parametrisierte Abfrage planen. Um eine parametrisierte Abfrage zu planen, folgen Sie dem typischen Prozess zum Erstellen einer geplanten Abfrage, wie in der Anleitung zum [Erstellen eines Abfrageplans](./query-schedules.md#create-schedule) beschrieben, und geben Sie dann die Parameterwerte ein, die bei der Abfrageausführung verwendet werden sollen. Dieser Abschnitt der Benutzeroberfläche wird nur für parametrisierte Abfragen angezeigt. Spezifische Anweisungen finden Sie [&#x200B; Abschnitt zum Festlegen von Parametern für eine geplante parametrisierte &#x200B;](./query-schedules.md#set-parameters) .

>[!TIP]
>
>Der Abfrage-Service unterstützt vorbereitete Anweisungen durch die Verwendung parametrisierter Abfragen. Weitere Informationen [&#x200B; verwendeten SQL-Syntax finden Sie &#x200B;](../sql/prepared-statements.md) Handbuch zur Syntax von vorbereiteten Anweisungen .

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie Abfragen in der Adobe Experience Platform-Benutzeroberfläche parametrisieren und in geplanten Abfrageausführungen verwenden können. In dem Dokument wurde auch hervorgehoben, wie die Protokolle auf die in Abfrageausführungen verwendeten Parameterwerte überprüft werden können.

Als Nächstes wird empfohlen, das Handbuch unter [Überwachen geplanter Abfragen](./monitor-queries.md) zu lesen, um über die Experience Platform-Benutzeroberfläche einen besseren Überblick über den Status aller Abfrageaufträge zu erhalten.
