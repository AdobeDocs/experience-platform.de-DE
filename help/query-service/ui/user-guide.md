---
keywords: Experience Platform; Startseite; beliebte Themen; Abfrage-Editor; Abfrage-Editor; Query Service; Query Service;
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche des Abfrage-Editors
description: Der Abfrage-Editor ist ein interaktives Tool von Adobe Experience Platform Query Service, mit dem Sie Abfragen für Kundenerlebnisdaten in der Experience Platform-Benutzeroberfläche schreiben, validieren und ausführen können. Der Abfrage-Editor unterstützt die Entwicklung von Abfragen für die Analyse und Datenexploration und ermöglicht Ihnen das Ausführen interaktiver Abfragen für Entwicklungszwecke sowie nicht interaktiver Abfragen zum Auffüllen von Datensätzen in Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: e30942aec6c66aeed8375d6221b454725f5a958d
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 68%

---

# Handbuch für die [!DNL Query Editor]-Benutzeroberfläche

[!DNL Query Editor] ist ein interaktives Tool von Adobe Experience Platform [!DNL Query Service], mit dem Sie Abfragen für Kundenerlebnisdaten in der [!DNL Experience Platform]-Benutzeroberfläche schreiben, validieren und ausführen können. [!DNL Query Editor] unterstützt die Erstellung von Abfragen für die Analyse und Datenexploration und ermöglicht das Ausführen interaktiver Abfragen für Entwicklungszwecke sowie nicht interaktiver Abfragen zum Befüllen von Datensätzen in [!DNL Experience Platform].

Weitere Informationen zu den Konzepten und Funktionen von [!DNL Query Service] finden Sie in der [Query Service – Übersicht](../home.md). Weitere Informationen zum Navigieren in der Benutzeroberfläche von Query Service von [!DNL Platform] finden Sie in der [Übersicht über die Query Service-Benutzeroberfläche](./overview.md).

## Erste Schritte {#getting-started}

[!DNL Query Editor] bietet flexible Ausführung von Abfragen durch Verbinden mit [!DNL Query Service], und Abfragen werden nur ausgeführt, während diese Verbindung aktiv ist.

### Herstellen einer Verbindung mit [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] benötigt beim Öffnen einige Sekunden, um zu initialisieren und eine Verbindung mit [!DNL Query Service] herzustellen. Die Konsole gibt an, ob eine Verbindung besteht (siehe unten). Wenn Sie versuchen, eine Abfrage auszuführen, bevor der Editor eine Verbindung hergestellt hat, wird die Ausführung verzögert, bis die Verbindung hergestellt ist.

![Die Konsolenausgabe des Abfrage-Editors bei der ersten Verbindung.](../images/ui/query-editor/connect.png)

### Ausführen von Abfragen über [!DNL Query Editor] {#run-a-query}

Von ausgeführten Abfragen [!DNL Query Editor] interaktiv ausführen, was bedeutet, dass die Abfrage abgebrochen wird, wenn Sie den Browser schließen oder wegnavigieren. Dasselbe gilt für Abfragen, die zum Generieren von Datensätzen aus Abfrageausgaben durchgeführt werden.

## Abfragenerstellung mit [!DNL Query Editor] {#query-authoring}

Mit [!DNL Query Editor] können Sie Abfragen für Kundenerlebnisdaten schreiben, ausführen und speichern. Alle in [!DNL Query Editor] ausgeführten oder gespeicherten Abfragen stehen allen Benutzenden in Ihrem Unternehmen mit Zugriff auf [!DNL Query Service] zur Verfügung.

### Zugreifen auf [!DNL Query Editor] {#accessing-query-editor}

Wählen Sie in der Benutzeroberfläche von [!DNL Experience Platform] im linken Navigationsmenü **[!UICONTROL Abfragen]** aus, um den [!DNL Query Service]-Arbeitsbereich zu öffnen. Um als Nächstes Abfragen zu schreiben, wählen Sie **[!UICONTROL Abfrage erstellen]** oben rechts auf dem Bildschirm. Dieser Link ist auf allen Seiten des [!DNL Query Service]-Arbeitsbereichs verfügbar.

![Die Registerkarte „Übersicht“ für den Abfragearbeitsbereich mit hervorgehobener Option „Abfrage erstellen“.](../images/ui/query-editor/create-query.png)

### Erweiterter Abfrage-Editor-Umschalter {#enhanced-editor-toggle}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_enhancedEditorToggle"
>title="Erweiterter Editor-Umschalter"
>abstract="Wechsel Sie zwischen der alten und der erweiterten Version des Abfrage-Editors. Die ältere Version ist standardmäßig aktiviert, obwohl die verbesserte Version bessere Zugänglichkeit und Unterstützung für mehrere Designs bietet. Weitere Informationen zu diesen Änderungen finden Sie in der Dokumentation."

Mit einem UI-Umschalter können Sie zwischen der alten und der erweiterten Version des Abfrage-Editors wechseln. Die ältere Version ist standardmäßig aktiviert, obwohl die verbesserte Version bessere Zugänglichkeit und Unterstützung für mehrere Designs bietet. Aktivieren Sie die erweiterte Version, um auf die Einstellungen des Abfrage-Editors zuzugreifen.

![Der Abfrage-Editor mit dem erweiterten Abfrage-Editor wurde hervorgehoben.](../images/ui/query-editor/enhanced-query-editor-toggle.png)

Durch Aktivierung des Umschalters wird der Editor zu einem helleren Design geändert und die Lesbarkeit der Syntax verbessert. Darüber hinaus wird über dem Eingabefeld Abfrage-Editor ein Einstellungssymbol angezeigt, das den Umschalter für die automatische Vervollständigung enthält. Über das Einstellungssymbol können Sie das Dunkle Design aktivieren oder die automatische Vervollständigung deaktivieren/aktivieren.

>[!TIP]
>
>Mit dem erweiterten Abfrage-Editor können Sie [!UICONTROL Automatische Syntaxvervollständigung deaktivieren] beim Verfassen einer Abfrage, ohne den Fortschritt zu verlieren. Wenn Sie die Funktion zum automatischen Vervollständigen während der Bearbeitung deaktivieren, gehen in der Regel alle Änderungen an der Abfrage verloren.

Um dunkle oder helle Themen zu aktivieren, wählen Sie das Einstellungssymbol (![Ein Einstellungssymbol.](../images/ui/query-editor/settings-icon.png)) gefolgt von der Option im angezeigten Dropdown-Menü.

![Die Optionen Abfrage-Editor mit dem Einstellungssymbol und Dropdown-Menü Dunkles Design aktivieren wurden hervorgehoben.](../images/ui/query-editor/query-editor-settings.png)

### Schreiben von Abfragen {#writing-queries}

Der [!UICONTROL Abfrage-Editor] ist so organisiert, dass das Schreiben von Abfragen so einfach wie möglich ist. Der folgende Screenshot zeigt, wie der Editor in der Benutzeroberfläche angezeigt wird, wobei das SQL-Eingabefeld und **Abspielen** hervorgehoben sind.

![Der Abfrage-Editor mit dem SQL-Eingabefeld und hervorgehobener „Abspielen“-Option.](../images/ui/query-editor/editor.png)

Um Ihre Entwicklungszeit zu minimieren, sollten Sie Ihre Abfragen mit Begrenzungen für die zurückgegebenen Zeilen entwickeln. Beispiel: `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Nachdem Sie überprüft haben, ob Ihre Abfrage die erwartete Ausgabe erzeugt, entfernen Sie die Begrenzungen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren.

### Schreib-Tools in [!DNL Query Editor] {#writing-tools}

- **Automatische Syntaxhervorhebung**: Erleichtert das Lesen und Organisieren von SQL.

![Eine SQL-Anweisung im Abfrage-Editor, in der die Syntaxfarbhervorhebung veranschaulicht ist.](../images/ui/query-editor/syntax-highlight.png)

- **SQL-Schlüsselwort automatisch vervollständigen:** Beginnen Sie mit der Eingabe Ihrer Abfrage, navigieren Sie mit den Pfeiltasten zum gewünschten Begriff und drücken Sie die **Eingabetaste**.

![Einige SQL-Zeichen mit dem Dropdown-Menü zur automatischen Vervollständigung mit Optionen aus dem Abfrage-Editor.](../images/ui/query-editor/syntax-auto.png)

- **Tabelle und Felder automatisch vervollständigen:** Beginnen Sie mit der Eingabe des Tabellennamens für den `SELECT`-Vorgang, navigieren Sie mit den Pfeiltasten zur gewünschten Tabelle und drücken Sie die **Eingabetaste**. Sobald eine Tabelle ausgewählt ist, erkennt die automatische Vervollständigung die Felder in dieser Tabelle.

![Die Eingabe im Abfrage-Editor mit einem Dropdown-Menü mit Tabellennamenvorschlägen.](../images/ui/query-editor/tables-auto.png)

### Umschalter für die Konfiguration der Benutzeroberfläche für die automatische Vervollständigung {#auto-complete}

[!DNL Query Editor] schlägt automatisch potenzielle SQL-Schlüsselwörter zusammen mit Tabellen- oder Spaltendetails für die Abfrage vor, während Sie sie schreiben. Die Funktion zur automatischen Vervollständigung ist standardmäßig aktiviert und kann jederzeit deaktiviert oder aktiviert werden, indem Sie den Umschalter [!UICONTROL Automatische Syntaxvervollständigung] oben rechts im Abfrage-Editor auswählen.

Die Konfigurationseinstellung für die automatische Vervollständigung erfolgt pro Benutzer bzw. Benutzerin und wird für die späteren Anmeldungen dieser Person gespeichert.

![Abfrage-Editor mit hervorgehobenem Umschalter für die automatische Syntaxvervollständigung.](../images/ui/query-editor/auto-complete-toggle.png)

Die Deaktivierung dieser Funktion verhindert, dass mehrere Metadatenbefehle verarbeitet werden, und bietet Empfehlungen, die in der Regel die Bearbeitung von Abfragen durch den Autor beschleunigt.

Wenn Sie den Umschalter verwenden, um die Funktion für die automatische Vervollständigung zu aktivieren, sind nach einer kurzen Pause empfohlene Vorschläge für Tabellen- und Spaltennamen sowie SQL-Schlüsselwörter verfügbar. Eine Erfolgsmeldung in der Konsole unter dem Abfrage-Editor zeigt an, dass die Funktion aktiv ist.

Wenn Sie die Funktion zur automatischen Vervollständigung deaktivieren, ist eine Seitenaktualisierung erforderlich, damit die Funktion wirksam wird. Wenn Sie den Umschalter [!UICONTROL Automatische Syntaxvervollständigung] deaktivieren, wird ein Bestätigungsdialogfeld mit drei Optionen angezeigt:

- [!UICONTROL Abbrechen]
- [!UICONTROL Änderungen speichern und aktualisieren]
- [!UICONTROL Ohne Speichern von Änderungen aktualisieren]

>[!IMPORTANT]
>
>Wenn Sie eine Abfrage schreiben oder bearbeiten, während Sie diese Funktion deaktivieren, müssen Sie alle Änderungen an Ihrer Abfrage speichern, bevor Sie die Seite aktualisieren. Andernfalls geht der gesamte Fortschritt verloren.

![Das Bestätigungsdialogfeld zum Deaktivieren der Funktion für die automatische Vervollständigung.](../images/ui/query-editor/confirmation-dialog.png)

Um die Funktion zur automatischen Vervollständigung zu deaktivieren, wählen Sie die entsprechende Bestätigungsoption aus.

### Fehlererkennung {#error-detection}

[!DNL Query Editor] validiert eine Abfrage automatisch, während Sie sie schreiben, und bietet dabei eine allgemeine SQL-Validierung und eine spezifische Ausführungsvalidierung. Wenn die Abfrage rot unterstrichen ist (wie in der Abbildung unten), liegt ein Fehler in der Abfrage vor.

![Die Eingabe in den Abfrage-Editor, in der SQL rot unterstrichen ist, um einen Fehler anzugeben.](../images/ui/query-editor/syntax-error-highlight.png)

Wenn Fehler erkannt werden, können Sie die spezifischen Fehlermeldungen anzeigen, indem Sie den Mauszeiger über den SQL-Code bewegen.

![Ein Dialogfeld mit einer Fehlermeldung.](../images/ui/query-editor/linting-error.png)

### Details zur Abfrage {#query-details}

Um eine Abfrage im Abfrage-Editor anzuzeigen, wählen Sie eine beliebige gespeicherte Vorlage aus dem [!UICONTROL Vorlagen] Registerkarte. Das Bedienfeld mit Abfragedetails enthält weitere Informationen und Tools zur Verwaltung der ausgewählten Abfrage.

![Der Abfrage-Editor mit hervorgehobenem Bedienfeld mit Abfragedetails.](../images/ui/query-editor/query-details.png)

In diesem Bedienfeld können Sie einen Ausgabedatensatz direkt über die Benutzeroberfläche generieren, die angezeigte Abfrage löschen oder benennen und der Abfrage einen Zeitplan hinzufügen.

In diesem Bedienfeld werden auch nützliche Metadaten angezeigt, z. B. das letzte Mal, dass die Abfrage geändert wurde und wer sie ggf. geändert hat. Wählen Sie **[!UICONTROL Ausgabedatensatz]** aus, um einen Datensatz zu generieren. Das Dialogfeld **[!UICONTROL Ausgabedatensatz]** wird angezeigt. Geben Sie einen Namen und eine Beschreibung ein und wählen Sie dann **[!UICONTROL Abfrage ausführen]** aus. Der neue Datensatz wird in der [!DNL Query Service]-Benutzeroberfläche von [!DNL Platform] auf der Registerkarte **[!UICONTROL Datensätze]** angezeigt.

### Geplante Abfragen {#scheduled-queries}

Abfragen, die als Vorlage gespeichert wurden, können im Abfrage-Editor geplant werden. Mit der Planung von Abfragen können Sie die Ausführung von Abfragen in einem benutzerdefinierten Ordner automatisieren. Sie können Abfragen basierend auf Häufigkeit, Datum und Uhrzeit planen und bei Bedarf auch einen Ausgabedatensatz für Ihre Ergebnisse auswählen. Abfragezeitpläne können auch über die Benutzeroberfläche deaktiviert oder gelöscht werden.

Zeitpläne werden im Abfrage-Editor festgelegt. Bei Verwendung des Abfrage-Editors können Sie einer bereits erstellten, gespeicherten und ausgeführten Abfrage nur einen Zeitplan hinzufügen. Dieselbe Einschränkung gilt nicht für [!DNL Query Service] API:

Weitere Informationen finden Sie in der Dokumentation zu Abfragezeitplänen . [Erstellen von Abfrageplänen in der Benutzeroberfläche](./query-schedules.md). Informationen zum Hinzufügen von Zeitplänen mithilfe der API finden Sie im Abschnitt [Endpunktleitfaden für geplante Abfragen](../api/scheduled-queries.md).

Alle geplanten Abfragen werden der Liste im [!UICONTROL Geplante Abfragen] Registerkarte. Von diesem Arbeitsbereich aus können Sie den Status aller geplanten Abfrageaufträge über die Benutzeroberfläche überwachen. Im [!UICONTROL Geplante Abfragen] finden Sie wichtige Informationen zu Ihren Abfrageausführungen und abonnieren Warnungen. Zu den verfügbaren Informationen gehören Status, Planungsdetails und Fehlermeldungen/Codes, falls eine Ausführung fehlgeschlagen ist. Siehe [Dokument zur Überwachung geplanter Abfragen](./monitor-queries.md) für weitere Informationen.

### Speichern von Abfragen {#saving-queries}

Der [!DNL Query Editor] bietet eine Speicherfunktion, mit der Sie eine Abfrage speichern und später daran arbeiten können. Um eine Abfrage zu speichern, wählen Sie **[!UICONTROL Speichern]** in der oberen rechten Ecke von [!DNL Query Editor]. Bevor eine Abfrage gespeichert werden kann, muss über das Bedienfeld **[!UICONTROL Details zur Abfrage]** ein Name für die Abfrage angegeben werden.

>[!NOTE]
>
>Mit dem Abfrage-Editor benannte und gespeicherte Abfragen sind als Vorlagen in der Registerkarte [!UICONTROL Vorlagen] im Abfrage-Dashboard verfügbar. Weitere Informationen finden Sie in der [Dokumentation zu Vorlagen](./query-templates.md).

### Auffinden früherer Abfragen {#previous-queries}

Alle vom [!DNL Query Editor] ausgeführten Abfragen werden in der Protokolltabelle erfasst. Sie können die Suchfunktion auf der Registerkarte **[!UICONTROL Protokoll]** verwenden, um Abfrageausführungen zu finden. Gespeicherte Abfragen werden auf der Registerkarte **[!UICONTROL Vorlagen]** angezeigt.

Wenn eine Abfrage geplant wurde, bietet die Registerkarte [!UICONTROL Geplante Abfragen] über die Benutzeroberfläche eine verbesserte Sichtbarkeit für diese Abfrageaufträge. Weitere Informationen finden Sie in der [Dokumention zur Abfrageüberwachung](./monitor-queries.md).

>[!NOTE]
>
>Nicht ausgeführte Abfragen werden nicht im Protokoll gespeichert. Damit die Abfrage in [!DNL Query Service] verfügbar ist, muss sie im [!DNL Query Editor] ausgeführt oder gespeichert werden.

## Ausführen von Abfragen mit dem Abfrage-Editor {#executing-queries}

Um eine Abfrage im [!DNL Query Editor] auszuführen, können Sie SQL im Editor eingeben oder eine frühere Abfrage über die Registerkarte **[!UICONTROL Protokoll]** oder **[!UICONTROL Vorlagen]** laden und auf **Abspielen** klicken. Der Ausführungsstatus der Abfrage wird auf der Registerkarte **[!UICONTROL Konsole]** angezeigt und die Ausgabedaten werden auf der Registerkarte **[!UICONTROL Ergebnisse]** angezeigt.

### Konsole {#console}

Die Konsole bietet Informationen zum Status und zum Betrieb von [!DNL Query Service]. Die Konsole zeigt den Verbindungsstatus zum [!DNL Query Service], die ausgeführten Abfragen und alle Fehlermeldungen an, die aus diesen Abfragen resultieren.

![Die Registerkarte „Konsole“ der Abfrage-Editor-Konsole.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>Die Konsole zeigt nur Fehler an, die bei der Ausführung einer Abfrage aufgetreten sind. Es werden keine Fehler bei der Abfrage-Validierung angezeigt, die vor der Ausführung einer Abfrage auftreten.

### Abfrageergebnisse {#query-results}

Nach Abschluss einer Abfrage werden die Ergebnisse auf der Registerkarte **[!UICONTROL Ergebnisse]** neben der Registerkarte **[!UICONTROL Konsole]** angezeigt. Diese Ansicht zeigt die tabellarische Ausgabe Ihrer Abfrage mit bis zu 100 Zeilen an. Mit dieser Ansicht können Sie überprüfen, ob Ihre Abfrage die erwartete Ausgabe erzeugt. Um einen Datensatz mit Ihrer Abfrage zu generieren, entfernen Sie Begrenzungen für zurückgegebene Zeilen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren. Anweisungen zum Generieren eines Datensatzes aus Abfragen im [!DNL Query Editor] finden Sie im [Tutorial zum Generieren von Datensätzen](./create-datasets.md).

![Auf der Registerkarte „Ergebnisse“ der Abfrage-Editor-Konsole werden die Ergebnisse einer Abfrageausführung angezeigt.](../images/ui/query-editor/query-results.png)

## Tutorial-Video zum Ausführen von Abfragen mit [!DNL Query Service] {#query-tutorial-video}

Im folgenden Video erfahren Sie, wie Sie Abfragen in der Adobe Experience Platform-Benutzeroberfläche und in einem PSQL-Client ausführen. Das Video zeigt außerdem die Verwendung einzelner Eigenschaften in einem XDM-Objekt, von Adoben definierte Funktionen und die Verwendung von CREATE TABLE AS SELECT (CTAS)-Abfragen.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Nächste Schritte

Nachdem Sie nun wissen, welche Funktionen im [!DNL Query Editor] verfügbar sind und wie Sie in der Anwendung navigieren, können Sie damit beginnen, Ihre eigenen Abfragen direkt im [!DNL Platform] zu erstellen. Weitere Informationen zum Ausführen von SQL-Abfragen für Datensätze im [!DNL Data Lake] finden Sie im Handbuch zum [Ausführen von Abfragen](../best-practices/writing-queries.md).
