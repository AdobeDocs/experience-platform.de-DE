---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zum Abfrage-Editor für Adobe Experience Platform Query Service
topic: query editor
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 57%

---


# [!DNL Query Editor] Benutzerhandbuch

[!DNL Query Editor] ist ein interaktives Tool der Adobe Experience Platform [!DNL Query Service], mit dem Sie Abfragen für Kundenerlebnisdaten in der [!DNL Experience Platform] Benutzeroberfläche schreiben, validieren und ausführen können. [!DNL Query Editor] unterstützt die Entwicklung von Abfragen für die Analyse und Datenforschung und ermöglicht Ihnen, interaktive Abfragen zu Entwicklungszwecken sowie nicht interaktive Abfragen zum Ausfüllen von Datensätzen in auszuführen [!DNL Experience Platform].

For more information about the concepts and features of [!DNL Query Service], see the [Query Service overview][query-service-overview]. To learn more about how to navigate the Query Service user interface on [!DNL Platform], see the [Query Service UI overview][query-service-ui].

## Erste Schritte

[!DNL Query Editor] ermöglicht eine flexible Ausführung von Abfragen durch Verbinden mit [!DNL Query Service]und Abfragen werden nur ausgeführt, wenn diese Verbindung aktiv ist.

### Connecting to [!DNL Query Service]

[!DNL Query Editor] Es dauert einige Sekunden, bis das Programm initialisiert und eine Verbindung hergestellt wird, [!DNL Query Service] wenn es geöffnet wird. Die Konsole gibt an, ob eine Verbindung besteht (siehe unten). Wenn Sie versuchen, eine Abfrage auszuführen, bevor der Editor eine Verbindung hergestellt hat, wird die Ausführung verzögert, bis die Verbindung hergestellt ist.

![Bild](../images/queries/query-editor-overview/initializing-connection.png)

### Ausführung von Abfragen [!DNL Query Editor]

Abfragen, die interaktiv ausgeführt [!DNL Query Editor] werden. Das bedeutet, dass die Abfrage abgebrochen wird, wenn Sie den Browser schließen oder wegnavigieren. Dies gilt auch für Abfragen, die zum Generieren von Datensätzen aus Abfrageausgaben vorgenommen werden.

## Erstellen von Abfragen mit [!DNL Query Editor]

Using [!DNL Query Editor], you can write, execute, and save queries for customer experience data. All queries executed in [!DNL Query Editor], or saved, are available to all users in your organization with access to [!DNL Query Service].

### Zugreifen auf [!DNL Query Editor]

In the [!DNL Experience Platform] UI, click **[!UICONTROL Queries]** in the left navigation menu to open the [!DNL Query Service] workspace. Klicken Sie dann oben rechts im Bildschirm auf **[!UICONTROL Abfrage erstellen]**, um Abfragen zu schreiben. This link is available from any of the pages in the [!DNL Query Service] workspace.

![Bild](../images/queries/query-editor-overview/create-query.png)

### Schreiben von Abfragen

[!UICONTROL Der Abfrage-Editor ist so organisiert, dass das Schreiben von Abfragen so einfach wie möglich ist. ] Der folgende Screenshot zeigt, wie der Editor in der Benutzeroberfläche angezeigt wird, wobei die Schaltfläche **Abspielen** und das SQL-Eingabefeld hervorgehoben sind.

![Bild](../images/queries/query-editor-overview/editor.png)

Um Ihre Entwicklungszeit zu minimieren, sollten Sie Ihre Abfragen mit Begrenzungen für die zurückgegebenen Zeilen entwickeln. Beispiel: `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Nachdem Sie überprüft haben, ob Ihre Abfrage die erwartete Ausgabe erzeugt, entfernen Sie die Begrenzungen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren.

### Schreiben von Werkzeugen in [!DNL Query Editor]

- **Automatische Syntaxhervorhebung:** Erleichtert das Lesen und Organisieren von SQL.

![Bild](../images/queries/query-editor-overview/syntax-highlight.png)

- **SQL-Schlüsselwort automatisch vervollständigen:** Beginnen Sie mit der Eingabe Ihrer Abfrage, navigieren Sie mit den Pfeiltasten zum gewünschten Begriff und drücken Sie die **Eingabetaste**.

![Bild](../images/queries/query-editor-overview/syntax-auto.png)

- **Tabelle und Felder automatisch vervollständigen:** Beginnen Sie mit der Eingabe des Tabellennamens für den `SELECT`-Vorgang, navigieren Sie mit den Pfeiltasten zur gewünschten Tabelle und drücken Sie die **Eingabetaste**. Sobald eine Tabelle ausgewählt ist, erkennt das automatische Vervollständigung die Felder in dieser Tabelle.

![Bild](../images/queries/query-editor-overview/tables-auto.png)

### Fehlererkennung

[!DNL Query Editor] überprüft eine Abfrage beim Schreiben automatisch, wobei eine generische SQL-Überprüfung und eine spezifische Ausführungsüberprüfung bereitgestellt werden. Wenn eine rote Unterstreichung unter der Abfrage angezeigt wird (wie in der Abbildung unten dargestellt), handelt es sich um einen Fehler in der Abfrage.

![Bild](../images/queries/query-editor-overview/syntax-error-highlight.png)

Wenn Fehler erkannt werden, können Sie die spezifischen Fehlermeldungen anzeigen, indem Sie den Mauszeiger über den SQL-Code bewegen.

![Bild](../images/queries/query-editor-overview/linting-error.png)

### Details zur Abfrage

While you are viewing a query in [!DNL Query Editor], the *[!UICONTROL Query Details]* panel provides tools to manage the selected query.

![Bild](../images/queries/query-editor-overview/query-details.png)

In diesem Bedienfeld können Sie ein Ausgabedatensatz direkt über die Benutzeroberfläche generieren, die angezeigte Abfrage löschen oder benennen und den SQL-Code in einem einfach zu kopierenden Format auf der Registerkarte *[!UICONTROL SQL-Abfrage]* anzeigen. In diesem Bedienfeld werden außerdem nützliche Metadaten angezeigt, z. B. das letzte Mal, dass die Abfrage geändert wurde und wer sie ggf. geändert hat. Klicken Sie auf **[!UICONTROL Ausgabedatensatz]**, um einen Datensatz zu erstellen. Das Dialogfeld *[!UICONTROL Ausgabedatensatz]* wird angezeigt. Geben Sie einen Namen und eine Beschreibung ein und klicken Sie dann auf **[!UICONTROL Abfrage ausführen]**. The new dataset is displayed in the *[!UICONTROL Datasets]* tab on the [!DNL Query Service] user interface on [!DNL Platform].

### Speichern von Abfragen

[!DNL Query Editor] bietet eine Speicherfunktion, mit der Sie eine Abfrage speichern und später daran arbeiten können. To save a query, click **[!UICONTROL Save]** in the top right corner of [!DNL Query Editor]. Bevor eine Abfrage gespeichert werden kann, muss über das Bedienfeld *[!UICONTROL Details zur Abfrage]* ein Name für die Abfrage angegeben werden.

### Auffinden früherer Abfragen

All queries executed from [!DNL Query Editor] are captured in the Log table. Sie können die Suchfunktion auf der Registerkarte *[!UICONTROL Protokoll]* verwenden, um Abfrageausführungen zu finden. Gespeicherte Abfragen werden auf der Registerkarte *[!UICONTROL Durchsuchen]* angezeigt.

Weitere Informationen finden Sie in der [Übersicht über die Query Service-Benutzeroberfläche][query-service-ui].

>[!NOTE]
>
>Nicht ausgeführte Abfragen werden nicht im Protokoll gespeichert. In order for the query to be available in [!DNL Query Service], it must be run or saved in [!DNL Query Editor].

## Ausführen von Abfragen mit dem Abfrage-Editor

To run a query in [!DNL Query Editor], you can enter SQL in the editor or load a previous query from the *Log* or *[!UICONTROL Browse]* tab, and click **Play**. Der Ausführungsstatus der Abfrage wird auf der Registerkarte *[!UICONTROL Konsole]* angezeigt und die Ausgabedaten werden auf der Registerkarte *[!UICONTROL Ergebnisse]* angezeigt.

### Konsole

Die Konsole bietet Informationen zum Status und zum Betrieb von [!DNL Query Service]. The console displays the connection status to [!DNL Query Service], query operations being executed, and any error messages that result from those queries.

![Bild](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>Die Konsole zeigt nur Fehler an, die beim Ausführen einer Abfrage aufgetreten sind. Es werden keine Fehler bei der Abfragevalidierung angezeigt, bevor eine Abfrage ausgeführt wird.

### Abfrageergebnisse

Nach Abschluss einer Abfrage werden die Ergebnisse auf der Registerkarte *[!UICONTROL Ergebnisse]* neben der Registerkarte *[!UICONTROL Konsole]* angezeigt. Diese Ansicht zeigt die tabellarische Ausgabe Ihrer Abfrage mit bis zu 100 Zeilen an. Mit dieser Ansicht können Sie überprüfen, ob Ihre Abfrage die erwartete Ausgabe erzeugt. Um einen Datensatz mit Ihrer Abfrage zu generieren, entfernen Sie Begrenzungen für zurückgegebene Zeilen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren. See the [generating datasets tutorial][query-service-create-datasets] for instructions on how to generate a dataset from query results in [!DNL Query Editor].

![Bild](../images/queries/query-editor-overview/query-results.png)

## Abfragen mit [!DNL Query Service] Lernvideo ausführen

Das folgende Video zeigt, wie Abfragen in der Benutzeroberfläche der Adobe Experience Platform und in einem PSQL-Client ausgeführt werden. Zusätzlich werden die Verwendung einzelner Eigenschaften in einem XDM-Objekt, die Verwendung von von Adobe definierten Funktionen und die Verwendung von CREATE TABLE AS SELECT (CTAS) demonstriert.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Nächste Schritte

Now that you know what features are available in [!DNL Query Editor] and how to navigate the application, you can start authoring your own queries directly in [!DNL Platform]. For more information about running SQL queries against datasets in [!DNL Data Lake], see the guide on [running queries][query-service-running-queries]. Beispiel-SQL-Abfragen für die Arbeit mit Adobe Analytics- und Adobe Target-Daten finden Sie in der [Referenz für Beispielabfragen][query-service-sample-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
