---
keywords: Experience Platform; Startseite; beliebte Themen; Abfrage-Editor; Abfrage-Editor; Query Service; Query Service;
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche des Abfrage-Editors
description: Der Abfrage-Editor ist ein interaktives Tool von Adobe Experience Platform Query Service, mit dem Sie Abfragen für Kundenerlebnisdaten in der Experience Platform-Benutzeroberfläche schreiben, validieren und ausführen können. Der Abfrage-Editor unterstützt die Entwicklung von Abfragen für die Analyse und Datenexploration und ermöglicht Ihnen das Ausführen interaktiver Abfragen für Entwicklungszwecke sowie nicht interaktiver Abfragen zum Auffüllen von Datensätzen in Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 45eab8f894819eea36465ea0b8f3f3dd8f91fbe0
workflow-type: tm+mt
source-wordcount: '2432'
ht-degree: 31%

---

# Anleitung zur Benutzeroberfläche des Abfrage-Editors

>[!NOTE]
>
>Der alte Editor wurde am 24. Mai 2024 eingestellt. Es ist nicht mehr verfügbar. Sie können jetzt die [Verbesserter Abfrage-Editor](#enhanced-editor-toggle) zum Schreiben, Validieren und Ausführen von Abfragen

Der Abfrage-Editor ist ein interaktives Tool von Adobe Experience Platform Query Service, mit dem Sie Abfragen für Kundenerlebnisdaten im [!DNL Experience Platform] -Benutzeroberfläche. Der Abfrage-Editor unterstützt die Entwicklung von Abfragen für die Analyse und Datenexploration und ermöglicht Ihnen das Ausführen interaktiver Abfragen zu Entwicklungszwecken sowie nicht-interaktiver Abfragen zum Ausfüllen von Datensätzen in [!DNL Experience Platform].

Weitere Informationen zu Konzepten und Funktionen von Query Service finden Sie in der [Query Service – Übersicht](../home.md). Weitere Informationen zum Navigieren in der Benutzeroberfläche von Query Service von [!DNL Platform] finden Sie in der [Übersicht über die Query Service-Benutzeroberfläche](./overview.md).

## Erste Schritte {#getting-started}

Der Abfrage-Editor bietet eine flexible Ausführung von Abfragen durch Herstellen einer Verbindung zu Query Service. Abfragen werden nur ausgeführt, wenn diese Verbindung aktiv ist.

## Aufrufen des Abfrage-Editors {#accessing-query-editor}

Im [!DNL Experience Platform] Benutzeroberfläche, auswählen **[!UICONTROL Abfragen]** im linken Navigationsmenü, um den Arbeitsbereich Query Service zu öffnen. Um als Nächstes Abfragen zu schreiben, wählen Sie **[!UICONTROL Abfrage erstellen]** oben rechts auf dem Bildschirm. Dieser Link ist auf allen Seiten des Arbeitsbereichs „Query Service“ verfügbar.

![Die Registerkarte „Übersicht“ für den Abfragearbeitsbereich mit hervorgehobener Option „Abfrage erstellen“.](../images/ui/query-editor/create-query.png)

### Herstellen einer Verbindung zu Query Service {#connecting-to-query-service}

Der Abfrage-Editor benötigt beim Öffnen einige Sekunden, um Query Service zu initialisieren und eine Verbindung herzustellen. Die Konsole gibt an, ob eine Verbindung besteht (siehe unten). Wenn Sie versuchen, eine Abfrage auszuführen, bevor der Editor eine Verbindung hergestellt hat, wird die Ausführung verzögert, bis die Verbindung hergestellt ist.

![Die Konsolenausgabe des Abfrage-Editors bei der ersten Verbindung.](../images/ui/query-editor/connect.png)

### Ausführen von Abfragen im Abfrage-Editor {#run-a-query}

Im Abfrage-Editor ausgeführte Abfragen werden interaktiv ausgeführt. Das bedeutet, dass die Abfrage abgebrochen wird, wenn Sie den Browser schließen oder wegnavigieren. Dasselbe gilt für Abfragen, die zum Generieren von Datensätzen aus Abfrageausgaben durchgeführt werden.

## Abfragebearbeitung mit dem erweiterten Abfrage-Editor {#query-authoring}

>[!NOTE]
>
>Der alte Editor wurde am 24. Mai 2024 eingestellt. Es ist nicht mehr verfügbar. Sie können jetzt den erweiterten Abfrage-Editor verwenden, um Ihre Abfragen zu schreiben, zu validieren und auszuführen.

Mit dem Abfrage-Editor können Sie Abfragen für Kundenerlebnisdaten schreiben, ausführen und speichern. Alle Abfragen, die ausgeführt oder im Abfrage-Editor gespeichert werden, stehen allen Benutzern in Ihrer Organisation mit Zugriff auf Query Service zur Verfügung.

### Einstellungen {#settings}

Ein Einstellungssymbol über dem Eingabefeld Abfrage-Editor enthält Optionen zum Aktivieren/Deaktivieren des Dunklen Designs oder Deaktivieren/Aktivieren der automatischen Vervollständigung.

>[!TIP]
>
>Sie können [!UICONTROL Automatische Syntaxvervollständigung deaktivieren] beim Verfassen einer Abfrage, ohne den Fortschritt zu verlieren.

Um dunkle oder helle Themen zu aktivieren, wählen Sie das Einstellungssymbol (![Ein Einstellungssymbol.](../images/ui/query-editor/settings-icon.png)) gefolgt von der Option im angezeigten Dropdown-Menü.

![Die Optionen Abfrage-Editor mit dem Einstellungssymbol und Dropdown-Menü Dunkles Design aktivieren wurden hervorgehoben.](../images/ui/query-editor/query-editor-settings.png)

#### Automatische Vervollständigung {#auto-complete}

Der Abfrage-Editor schlägt bei der Erstellung der Abfrage automatisch potenzielle SQL-Schlüsselwörter zusammen mit Tabellen- oder Spaltendetails vor. Die Funktion zur automatischen Vervollständigung ist standardmäßig aktiviert und kann jederzeit über die Einstellungen des Abfrage-Editors deaktiviert oder aktiviert werden.

Die Konfigurationseinstellung für die automatische Vervollständigung erfolgt pro Benutzer und wird für die aufeinander folgenden Anmeldungen für diesen Benutzer gespeichert. Die Deaktivierung dieser Funktion verhindert, dass mehrere Metadatenbefehle verarbeitet werden, und bietet Empfehlungen, die in der Regel die Bearbeitung von Abfragen durch den Autor beschleunigt.

<!-- Currently editing the auto complete setting info. -->



### Mehrere sequenzielle Abfragen ausführen {#execute-multiple-sequential-queries}

Verwenden Sie den erweiterten Abfrage-Editor, um mehr als eine Abfrage zu schreiben und alle Abfragen sequenziell auszuführen. Die Ausführung mehrerer Abfragen in einer Sequenz generiert jeweils einen Protokolleintrag. In der Konsole &quot;Abfrage-Editor&quot;werden jedoch nur die Ergebnisse der ersten Abfrage angezeigt. Überprüfen Sie das Abfrageprotokoll, ob Sie eine Fehlerbehebung durchführen oder die ausgeführten Abfragen bestätigen müssen. Siehe [Dokumentation zu Abfrageprotokollen](./query-logs.md) für weitere Informationen.

>[!NOTE]
> 
>Wenn nach der ersten Abfrage im Abfrage-Editor eine CTAS-Abfrage ausgeführt wird, wird weiterhin eine Tabelle erstellt, jedoch keine Ausgabe in der Abfrage-Editor-Konsole.

### Ausgewählte Abfrage ausführen {#execute-selected-query}

Wenn Sie mehrere Abfragen geschrieben haben, aber nur eine Abfrage ausführen müssen, können Sie Ihre ausgewählte Abfrage markieren und die
[!UICONTROL Ausgewählte Abfrage ausführen] Symbol. Dieses Symbol ist standardmäßig deaktiviert, bis Sie im Editor die Abfragesyntax auswählen.

![Der Abfrage-Editor mit dem [!UICONTROL Ausgewählte Abfrage ausführen] hervorgehoben.](../images/ui/query-editor/run-selected-query.png)

### Sitzung des Abfrage-Editors abbrechen {#cancel-query}

Übernehmen Sie die Kontrolle über die Ausführung von Abfragen und verbessern Sie Ihre Produktivität, indem Sie langwierige Abfragen abbrechen. Durch diese Aktion wird der Abfrage-Editor während einer Abfrageausführung gelöscht. Beachten Sie, dass die Abfrage weiterhin im Hintergrund ausgeführt wird. Wenn es sich um eine CTAS-Abfrage handelt, wird weiterhin ein Ausgabedatensatz generiert. Um die Ausführung im Editor abzubrechen und mit dem Erstellen einer SQL-Anweisung fortzufahren, wählen Sie **[!UICONTROL Abfrage abbrechen]** nach der Ausführung einer Abfrage.

![Der Abfrage-Editor mit [!UICONTROL Abfrage abbrechen] hervorgehoben.](../images/ui/query-editor/cancel-query-run.png)

Ein Bestätigungsdialogfeld wird angezeigt. Auswählen **[!UICONTROL Bestätigen]** , um die Ausführung der Abfrage abzubrechen.

![Das Dialogfeld Abbrechen der Abfragebestätigung mit hervorgehobener Bestätigung.](../images/ui/query-editor/cancel-query-confirmation-dialog.png)

### Ergebniszähler {#result-count}

Der Abfrage-Editor verfügt über eine Ausgabe von maximal 50.000 Zeilen. Sie können die Anzahl der Zeilen auswählen, die gleichzeitig in der Konsole &quot;Abfrage-Editor&quot;angezeigt werden. Um die Anzahl der in der Konsole angezeigten Zeilen zu ändern, wählen Sie die **[!UICONTROL Ergebnisanzahl]** und wählen Sie aus den Optionen 50, 100, 150, 300 und 500 aus.

![Der Abfrage-Editor mit der Dropdown-Liste Ergebnisanzahl wurde hervorgehoben.](../images/ui/query-editor/result-count.png)

## Schreiben von Abfragen {#writing-queries}

Der [!UICONTROL Abfrage-Editor] ist so organisiert, dass das Schreiben von Abfragen so einfach wie möglich ist. Der folgende Screenshot zeigt, wie der Editor in der Benutzeroberfläche angezeigt wird, wobei das SQL-Eingabefeld und **Abspielen** hervorgehoben sind.

![Der Abfrage-Editor mit dem SQL-Eingabefeld und hervorgehobener „Abspielen“-Option.](../images/ui/query-editor/editor.png)

Um Ihre Entwicklungszeit zu minimieren, sollten Sie Ihre Abfragen mit Begrenzungen für die Anzahl der zurückgegebenen Zeilen entwickeln. Beispiel: `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Nachdem Sie überprüft haben, ob Ihre Abfrage die erwartete Ausgabe erzeugt, entfernen Sie die Begrenzungen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren.

## Schreibwerkzeuge im Abfrage-Editor {#writing-tools}

- **Automatische Syntaxhervorhebung**: Erleichtert das Lesen und Organisieren von SQL.

![Eine SQL-Anweisung im Abfrage-Editor, in der die Syntaxfarbhervorhebung veranschaulicht ist.](../images/ui/query-editor/syntax-highlight.png)

- **SQL-Schlüsselwort automatisch vervollständigen:** Beginnen Sie mit der Eingabe Ihrer Abfrage, navigieren Sie mit den Pfeiltasten zum gewünschten Begriff und drücken Sie die **Eingabetaste**.

![Einige SQL-Zeichen mit dem Dropdown-Menü zur automatischen Vervollständigung mit Optionen aus dem Abfrage-Editor.](../images/ui/query-editor/syntax-auto.png)

- **Tabelle und Felder automatisch vervollständigen:** Beginnen Sie mit der Eingabe des Tabellennamens für den `SELECT`-Vorgang, navigieren Sie mit den Pfeiltasten zur gewünschten Tabelle und drücken Sie die **Eingabetaste**. Sobald eine Tabelle ausgewählt ist, erkennt die automatische Vervollständigung die Felder in dieser Tabelle.

![Die Eingabe im Abfrage-Editor mit einem Dropdown-Menü mit Tabellennamenvorschlägen.](../images/ui/query-editor/tables-auto.png)

### Text formatieren {#format-text}

Die [!UICONTROL Text formatieren] -Funktion ermöglicht eine bessere Lesbarkeit Ihrer Abfrage durch das Hinzufügen standardisierter Syntaxstile. Auswählen **[!UICONTROL Text formatieren]** , um den gesamten Text im Abfrage-Editor zu standardisieren.

>[!NOTE]
>
>Die [!UICONTROL Text formatieren] -Funktion funktioniert nicht mit anonymen Bausteinen. Informationen dazu, wie Sie eine oder mehrere SQL-Anweisungen sequenziell verketten, finden Sie unter [Anonyme Blockdokumentation](../key-concepts/anonymous-block.md).

![Der Abfrage-Editor mit [!UICONTROL Text formatieren] und die SQL-Anweisungen hervorgehoben.](../images/ui/query-editor/format-text.png)

<!-- ### Undo text {#undo-text}

If you format your SQL in the Query Editor, you can undo the formatting applied by the [!UICONTROL Format text] feature. To return your SQL back to its original form, select **[!UICONTROL Undo text]**.

![The Query Editor with [!UICONTROL Undo text] and the SQL statements highlighted.](../images/ui/query-editor/undo-text.png) -->

### SQL kopieren {#copy-sql}

Wählen Sie das Kopiersymbol aus, um SQL aus dem Abfrage-Editor in die Zwischenablage zu kopieren. Diese Kopierfunktion ist sowohl für Abfragevorlagen als auch für neu erstellte Abfragen im Abfrage-Editor verfügbar.

![Der Arbeitsbereich Abfragen mit einer Beispielabfragevorlage mit hervorgehobenem Kopiersymbol.](../images/ui/query-editor/copy-sql.png)

### Details zur Abfrage {#query-details}

Um eine Abfrage im Abfrage-Editor anzuzeigen, wählen Sie eine beliebige gespeicherte Vorlage aus dem [!UICONTROL Vorlagen] Registerkarte. Das Bedienfeld &quot;Abfragedetails&quot;enthält weitere Informationen und Tools zur Verwaltung der ausgewählten Abfrage. Außerdem werden nützliche Metadaten angezeigt, z. B. das letzte Mal, dass die Abfrage geändert wurde und wer sie gegebenenfalls geändert hat.

>[!NOTE]
>
>Die [!UICONTROL Zeitplan anzeigen], [!UICONTROL Zeitplan hinzufügen] und [!UICONTROL Abfrage löschen] -Optionen stehen erst zur Verfügung, nachdem die Abfrage als Vorlage gespeichert wurde. Die [!UICONTROL Zeitplan hinzufügen] -Option gelangen Sie direkt vom Abfrage-Editor zum Zeitplan-Builder. Die [!UICONTROL Zeitplan anzeigen] -Option führt Sie direkt zum Planbestand für diese Abfrage. Weitere Informationen finden Sie in der Dokumentation zu Abfragezeitplänen . [Erstellen von Abfrageplänen in der Benutzeroberfläche](./query-schedules.md#create-schedule).

![Der Abfrage-Editor mit hervorgehobenem Bedienfeld mit Abfragedetails.](../images/ui/query-editor/query-details.png)

Im Detailbereich können Sie einen Ausgabedatensatz direkt über die Benutzeroberfläche generieren, die angezeigte Abfrage löschen oder benennen, den Zeitplan für die Ausführung der Abfrage anzeigen und die Abfrage einem Zeitplan hinzufügen.

Um einen Ausgabedatensatz zu generieren, wählen Sie **[!UICONTROL Als CTAS ausführen]**. Die **[!UICONTROL Ausgabedatasdetails eingeben]** angezeigt. Geben Sie einen Namen und eine Beschreibung ein und wählen Sie **[!UICONTROL Als CTAS ausführen]**. Der neue Datensatz wird im **[!UICONTROL Datensätze]** Registerkarte Durchsuchen . Siehe [die Dokumentation zum Anzeigen von Datensätzen](../../catalog/datasets/user-guide.md#view-datasets) , um mehr über verfügbare Datensätze für Ihre Organisation zu erfahren.

>[!NOTE]
>
>Die [!UICONTROL Als CTAS ausführen] ist nur verfügbar, wenn die Abfrage **not** wurden geplant.

![Die [!UICONTROL Ausgabedatasdetails eingeben] angezeigt.](../images/ui/query-editor/output-dataset-details.png)

Nachdem Sie die **[!UICONTROL Als CTAS ausführen]** -Aktion, wird eine Bestätigungsmeldung angezeigt, die Sie über die erfolgreiche Aktion informiert. Diese Popup-Nachricht enthält einen Link, der eine praktische Möglichkeit bietet, zum Arbeitsbereich &quot;Abfrageprotokolle&quot;zu navigieren. Siehe [Dokumentation zu Abfrageprotokollen](./query-logs.md) für weitere Informationen zu Abfrageprotokollen.

### Speichern von Abfragen {#saving-queries}

Der Abfrage-Editor bietet eine Speicherfunktion, mit der Sie eine Abfrage speichern und später daran arbeiten können. Um eine Abfrage zu speichern, wählen Sie **[!UICONTROL Speichern]** in der oberen rechten Ecke des Abfrage-Editors. Bevor eine Abfrage gespeichert werden kann, muss über das Bedienfeld **[!UICONTROL Details zur Abfrage]** ein Name für die Abfrage angegeben werden.

>[!NOTE]
>
>Mit dem Abfrage-Editor benannte und gespeicherte Abfragen sind als Vorlagen in der Registerkarte [!UICONTROL Vorlagen] im Abfrage-Dashboard verfügbar. Weitere Informationen finden Sie in der [Dokumentation zu Vorlagen](./query-templates.md).

Wenn Sie eine Abfrage im Abfrage-Editor speichern, wird eine Bestätigungsmeldung angezeigt, die Sie über die erfolgreiche Aktion informiert. Diese Popup-Nachricht enthält einen Link, der eine praktische Möglichkeit bietet, zum Arbeitsbereich &quot;Planung von Abfragen&quot;zu navigieren. Siehe [Planungsabfragedokumentation](./query-schedules.md) , um zu erfahren, wie Sie Abfragen für eine benutzerdefinierte Cadence ausführen.

### Geplante Abfragen {#scheduled-queries}

Abfragen, die als Vorlage gespeichert wurden, können im Abfrage-Editor geplant werden. Mit der Planung von Abfragen können Sie die Ausführung von Abfragen in einem benutzerdefinierten Ordner automatisieren. Sie können Abfragen basierend auf Häufigkeit, Datum und Uhrzeit planen und bei Bedarf auch einen Ausgabedatensatz für Ihre Ergebnisse auswählen. Abfragezeitpläne können auch über die Benutzeroberfläche deaktiviert oder gelöscht werden.

Zeitpläne werden im Abfrage-Editor festgelegt. Bei Verwendung des Abfrage-Editors können Sie einer bereits erstellten und gespeicherten Abfrage nur einen Zeitplan hinzufügen. Dasselbe gilt nicht für die Query Service-API.

>[!NOTE]
>
>Geplante Abfragen, die zehn aufeinander folgende Ausführungen fehlschlagen, werden automatisch in eine [!UICONTROL In Quarantäne] -Status. Eine Abfrage mit diesem Status erfordert Ihre Intervention, bevor weitere Ausführungen durchgeführt werden können. Siehe [Quarantäne-Abfragen](./monitor-queries.md#quarantined-queries) Dokumentation für weitere Details.

Weitere Informationen finden Sie in der Dokumentation zu Abfragezeitplänen . [Erstellen von Abfrageplänen in der Benutzeroberfläche](./query-schedules.md). Informationen zum Hinzufügen von Zeitplänen mithilfe der API finden Sie im Abschnitt [Endpunktleitfaden für geplante Abfragen](../api/scheduled-queries.md).

Alle geplanten Abfragen werden der Liste im [!UICONTROL Geplante Abfragen] Registerkarte. Von diesem Arbeitsbereich aus können Sie den Status aller geplanten Abfrageaufträge über die Benutzeroberfläche überwachen. Im [!UICONTROL Geplante Abfragen] finden Sie wichtige Informationen zu Ihren Abfrageausführungen und abonnieren Warnungen. Zu den verfügbaren Informationen gehören Status, Planungsdetails und Fehlermeldungen/Codes, falls eine Ausführung fehlgeschlagen ist. Siehe [Dokument zur Überwachung geplanter Abfragen](./monitor-queries.md) für weitere Informationen.


### Auffinden früherer Abfragen {#previous-queries}

Alle vom Abfrage-Editor ausgeführten Abfragen werden in der Tabelle „Protokoll“ erfasst. Sie können die Suchfunktion auf der Registerkarte **[!UICONTROL Protokoll]** verwenden, um Abfrageausführungen zu finden. Gespeicherte Abfragen werden auf der Registerkarte **[!UICONTROL Vorlagen]** angezeigt.

Wenn eine Abfrage geplant wurde, bietet die Registerkarte [!UICONTROL Geplante Abfragen] über die Benutzeroberfläche eine verbesserte Sichtbarkeit für diese Abfrageaufträge. Weitere Informationen finden Sie in der [Dokumention zur Abfrageüberwachung](./monitor-queries.md).

>[!NOTE]
>
>Nicht ausgeführte Abfragen werden nicht im Protokoll gespeichert. Damit die Abfrage in Query Service verfügbar ist, muss sie im Abfrage-Editor ausgeführt oder gespeichert werden.

## Ausführen von Abfragen mit dem Abfrage-Editor {#executing-queries}

Um eine Abfrage im Abfrage-Editor auszuführen, können Sie SQL im Editor eingeben oder eine frühere Abfrage aus dem **[!UICONTROL Protokoll]** oder **[!UICONTROL Vorlagen]** und wählen Sie **Play**. Der Ausführungsstatus der Abfrage wird auf der Registerkarte **[!UICONTROL Konsole]** angezeigt und die Ausgabedaten werden auf der Registerkarte **[!UICONTROL Ergebnisse]** angezeigt.

### Konsole {#console}

Die Konsole bietet Informationen zum Status und zum Betrieb von Query Service. Die Konsole zeigt den Verbindungsstatus zu Query Service, die ausgeführten Abfragen und alle Fehlermeldungen an, die sich aus diesen Abfragen ergeben.

![Die Registerkarte „Konsole“ der Abfrage-Editor-Konsole.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>Die Konsole zeigt nur Fehler an, die bei der Ausführung einer Abfrage aufgetreten sind. Es werden keine Fehler bei der Abfrage-Validierung angezeigt, die vor der Ausführung einer Abfrage auftreten.

### Abfrageergebnisse {#query-results}

Nach Abschluss einer Abfrage werden die Ergebnisse auf der Registerkarte **[!UICONTROL Ergebnisse]** neben der Registerkarte **[!UICONTROL Konsole]** angezeigt. Diese Ansicht zeigt die tabellarische Ausgabe Ihrer Abfrage, die je nach ausgewähltem Ergebnis zwischen 50 und 500 Zeilen der Ergebnisse anzeigt [Ergebnisanzahl](#result-count). Mit dieser Ansicht können Sie überprüfen, ob Ihre Abfrage die erwartete Ausgabe erzeugt. Um einen Datensatz mit Ihrer Abfrage zu generieren, entfernen Sie Begrenzungen für zurückgegebene Zeilen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren. Anweisungen zum Generieren eines Datensatzes aus Abfragen im Abfrage-Editor finden Sie im [Tutorial zum Generieren von Datensätzen](./create-datasets.md).

![Auf der Registerkarte „Ergebnisse“ der Abfrage-Editor-Konsole werden die Ergebnisse einer Abfrageausführung angezeigt.](../images/ui/query-editor/query-results.png)

## Anwendungsfälle {#use-cases}

Query Service bietet Lösungen für eine Vielzahl von Anwendungsfällen in verschiedenen Branchen und Geschäftsszenarien. Diese praktischen Beispiele belegen die Flexibilität und die Wirkung des Dienstes bei der Bewältigung verschiedener Bedürfnisse. nach [Erfahren Sie, wie Query Service für Ihre spezifischen Geschäftsanforderungen von Nutzen sein kann.](../use-cases/overview.md), lesen Sie die umfassende Sammlung von Anwendungsfalldokumenten. Erfahren Sie, wie Sie mithilfe von Query Service Einblicke und Lösungen für eine verbesserte betriebliche Effizienz und Geschäftserfolg erhalten.

<!-- This video is from 2019. The logic is sounds but the workflow is too outdated. -->

## Tutorial zum Ausführen von Abfragen mit Query Service {#query-tutorial-video}

Im folgenden Video erfahren Sie, wie Sie Abfragen in der Adobe Experience Platform-Benutzeroberfläche und in einem PSQL-Client ausführen. Das Video zeigt außerdem die Verwendung einzelner Eigenschaften in einem XDM-Objekt, Adobe-definierte Funktionen und die Verwendung von CREATE TABLE AS SELECT (CTAS)-Abfragen.

>[!NOTE]
>
>Die im Video dargestellte Benutzeroberfläche ist veraltet, die im Workflow verwendete Logik bleibt jedoch unverändert.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Nächste Schritte

Nachdem Sie wissen, welche Funktionen im Abfrage-Editor verfügbar sind und wie Sie in der Anwendung navigieren, können Sie Ihre eigenen Abfragen direkt in [!DNL Platform]. Weitere Informationen zum Ausführen von SQL-Abfragen für Datensätze im [!DNL Data Lake] finden Sie im Handbuch zum [Ausführen von Abfragen](../best-practices/writing-queries.md).
