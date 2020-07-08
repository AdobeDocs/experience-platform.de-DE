---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zur Adobe Experience Platform Abfrage Service Abfrage Editor
topic: query editor
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# Abfrage Editor-Benutzerhandbuch

Abfrage Editor ist ein interaktives Tool des Adobe Experience Platform Abfrage Service, mit dem Sie Abfragen für Kundenerlebnisdaten in der Benutzeroberfläche der Experience Platform schreiben, validieren und ausführen können. Abfrage Editor unterstützt die Entwicklung von Abfragen für die Analyse und Datenforschung und ermöglicht Ihnen, interaktive Abfragen zu Entwicklungszwecken sowie nicht interaktive Abfragen zum Ausfüllen von Datensätzen in der Experience Platform auszuführen.

Weitere Informationen zu Konzepten und Funktionen von Abfrage Service finden Sie in der Übersicht über den [Abfrage Service][query-service-overview]. Weitere Informationen zum Navigieren in der Benutzeroberfläche des Abfrage Service auf Platform finden Sie in der Übersicht über die Benutzeroberfläche des [Abfrage-Dienstes][query-service-ui].

## Erste Schritte

Abfrage Editor ermöglicht eine flexible Ausführung von Abfragen durch Verbindung zum Abfrage Service. Abfragen werden nur ausgeführt, wenn diese Verbindung aktiv ist.

### Herstellen einer Verbindung zum Abfrage-Dienst

Der Abfrage Editor dauert einige Sekunden, bis er beim Öffnen initialisiert und eine Verbindung zum Abfrage-Dienst hergestellt wird. Die Konsole gibt an, wann eine Verbindung besteht (siehe unten). Wenn Sie versuchen, eine Abfrage auszuführen, bevor der Editor eine Verbindung hergestellt hat, wird die Ausführung verzögert, bis die Verbindung abgeschlossen ist.

![Bild](../images/queries/query-editor-overview/initializing-connection.png)

### Ausführung von Abfragen im Abfrage Editor

Abfragen, die vom Abfrage Editor ausgeführt werden, werden interaktiv ausgeführt. Das bedeutet, dass die Abfrage abgebrochen wird, wenn Sie den Browser schließen oder wegnavigieren. Dies gilt auch für Abfragen, die zum Generieren von Datensätzen aus Abfragen-Ausgaben vorgenommen werden.

## Erstellen von Abfragen mit dem Abfrage Editor

Mit dem Abfrage Editor können Sie Abfragen für Kundenerlebnisdaten schreiben, ausführen und speichern. Alle im Abfrage Editor ausgeführten oder gespeicherten Abfragen stehen allen Benutzern in Ihrem Unternehmen mit Zugriff auf den Abfrage Service zur Verfügung.

### Zugriff auf Abfrage Editor

Klicken Sie in der Benutzeroberfläche &quot;Experience Platform&quot;im linken Navigationsmenü auf **Abfragen** , um den Arbeitsbereich &quot;Abfrage-Dienst&quot;zu öffnen. Klicken Sie dann oben rechts auf dem Bildschirm auf Abfrage **** erstellen, um Abfragen zu schreiben. Dieser Link ist auf allen Seiten des Arbeitsbereichs &quot;Abfrage-Dienst&quot;verfügbar.

![Bild](../images/queries/query-editor-overview/create-query.png)

### Schreiben von Abfragen

Abfrage Editor ist so organisiert, dass das Schreiben von Abfragen so einfach wie möglich. Der folgende Screenshot zeigt, wie der Editor in der Benutzeroberfläche angezeigt wird, wobei die Schaltfläche &quot; **Abspielen** &quot;und das SQL-Eingabefeld hervorgehoben sind.

![Bild](../images/queries/query-editor-overview/editor.png)

Um Ihre Entwicklungszeit zu minimieren, sollten Sie Ihre Abfragen mit Einschränkungen für die zurückgegebenen Zeilen entwickeln. Beispiel: `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Nachdem Sie überprüft haben, ob Ihre Abfrage die erwartete Ausgabe erzeugt, entfernen Sie die Grenzwerte und führen Sie die Abfrage aus, mit der ein Datensatz mit der Ausgabe generiert `CREATE TABLE tablename AS SELECT` werden soll.

### Schreiben von Werkzeugen im Abfragen-Editor

- **Automatische Syntaxhervorhebung:** Erleichtert das Lesen und Organisieren von SQL.

![Bild](../images/queries/query-editor-overview/syntax-highlight.png)

- **SQL-Schlüsselwort automatisch vervollständigen:** Beginn, die Ihre Abfrage eingeben, dann mit den Pfeiltasten zum gewünschten Begriff navigieren und die **Eingabetaste drücken**.

![Bild](../images/queries/query-editor-overview/syntax-auto.png)

- **Automatische Vervollständigung von Tabellen und Feldern:** Beginn, der den gewünschten Tabellennamen `SELECT` eingibt, dann mit den Pfeiltasten zur gewünschten Tabelle navigiert und die **Eingabetaste** drückt. Sobald eine Tabelle ausgewählt ist, erkennt das automatische Ausfüllen die Felder in dieser Tabelle.

![Bild](../images/queries/query-editor-overview/tables-auto.png)

### Fehlererkennung

Abfrage Editor validiert eine Abfrage automatisch, während Sie sie schreiben, und stellt eine generische SQL-Überprüfung und eine spezifische Ausführungsüberprüfung bereit. Wenn eine rote Unterstreichung unterhalb der Abfrage angezeigt wird (wie in der Abbildung unten dargestellt), stellt sie einen Fehler innerhalb der Abfrage dar.

![Bild](../images/queries/query-editor-overview/syntax-error-highlight.png)

Wenn Fehler erkannt werden, können Sie die jeweiligen Fehlermeldungen durch Bewegen des Mauszeigers über den SQL-Code Ansicht werden.

![Bild](../images/queries/query-editor-overview/linting-error.png)

### Einzelheiten zur Abfrage

Während Sie eine Abfrage im Abfragen-Editor anzeigen, stehen Ihnen im Bedienfeld &quot; *Abfragen-Details* &quot;Tools zur Verwaltung der ausgewählten Abfrage zur Verfügung.

![Bild](../images/queries/query-editor-overview/query-details.png)

In diesem Bedienfeld können Sie ein Ausgabedataset direkt aus der Benutzeroberfläche generieren, die angezeigte Abfrage löschen oder benennen und den SQL-Code auf der Registerkarte &quot; *SQL-Abfrage* &quot;in einem leicht zu kopierenden Format Ansicht geben. In diesem Bedienfeld werden auch nützliche Metadaten angezeigt, z. B. das letzte Mal, dass die Abfrage geändert wurde und wer sie ggf. geändert hat. Um einen Datensatz zu erstellen, klicken Sie auf **Ausgabedatensatz**. Das Dialogfeld &quot; *Ausgabedatensatz* &quot;wird angezeigt. Geben Sie einen Namen und eine Beschreibung ein und klicken Sie dann auf Abfrage **ausführen**. Der neue Datensatz wird in der Benutzeroberfläche des Abfrage-Dienstes auf der Platform auf der Registerkarte &quot; *Datensätze* &quot;angezeigt.

### Speichern von Abfragen

Abfrage Editor bietet eine Speicherfunktion, mit der Sie eine Abfrage speichern und später daran arbeiten können. Klicken Sie zum Speichern einer Abfrage oben rechts im Abfragen-Editor auf **Speichern** . Bevor eine Abfrage gespeichert werden kann, muss über das Bedienfeld &quot; *Abfragen-Details* &quot;ein Name für die Abfrage angegeben werden.

### Wie Sie frühere Abfragen finden

Alle vom Abfrage Editor ausgeführten Abfragen werden in der Tabelle &quot;Protokoll&quot;erfasst. Sie können die Suchfunktion auf der Registerkarte &quot; *Protokoll* &quot;verwenden, um Abfragen zu finden. Gespeicherte Abfragen werden auf der Registerkarte &quot; *Durchsuchen* &quot;angezeigt.

Weitere Informationen finden Sie in der Übersicht über die Benutzeroberfläche des [Abfrage-Dienstes][query-service-ui] .

>[!NOTE]
>
>Nicht ausgeführte Abfragen werden nicht im Protokoll gespeichert. Damit die Abfrage im Abfrage-Dienst verfügbar ist, muss sie im Abfrage-Editor ausgeführt oder gespeichert werden.

## Ausführen von Abfragen mit dem Abfrage Editor

Um eine Abfrage im Abfrage Editor auszuführen, können Sie SQL in den Editor eingeben oder eine vorherige Abfrage über die Registerkarte &quot; *Protokoll* &quot;oder &quot; *Durchsuchen* &quot;laden und auf &quot; **Abspielen**&quot;klicken. Der Ausführungsstatus der Abfrage wird auf der Registerkarte &quot; *Konsole* &quot;angezeigt und die Ausgabedaten werden auf der Registerkarte &quot; *Ergebnisse* &quot;angezeigt.

### Konsole

Die Konsole bietet Informationen zum Status und zum Betrieb des Abfrage Service. Die Konsole zeigt den Verbindungsstatus zum Abfrage-Dienst, die ausgeführten Abfragen und alle Fehlermeldungen an, die sich aus diesen Abfragen ergeben.

![Bild](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>Die Konsole zeigt nur Fehler an, die beim Ausführen einer Abfrage aufgetreten sind. Es werden keine Fehler bei der Überprüfung der Abfrage angezeigt, bevor eine Abfrage ausgeführt wird.

### Abfragen

Nach Abschluss einer Abfrage werden die Ergebnisse auf der Registerkarte &quot; *Ergebnisse* &quot;neben der Registerkarte &quot; *Konsole* &quot;angezeigt. Diese Ansicht zeigt die tabellarische Ausgabe Ihrer Abfrage mit bis zu 100 Zeilen an. Mit dieser Ansicht können Sie überprüfen, ob Ihre Abfrage die erwartete Ausgabe erzeugt. Um ein Dataset mit Ihrer Abfrage zu generieren, entfernen Sie Begrenzungen für zurückgegebene Zeilen und führen Sie die Abfrage aus, mit der ein Datensatz mit der Ausgabe generiert `CREATE TABLE tablename AS SELECT` werden soll. Anweisungen zum Generieren eines Datensatzes aus Abfragen im Abfrage Editor finden Sie im Lernprogramm [zum][query-service-create-datasets] Generieren von Datensätzen.

![Bild](../images/queries/query-editor-overview/query-results.png)

## Nächste Schritte

Nachdem Sie wissen, welche Funktionen im Abfrage Editor zur Verfügung stehen und wie Sie in der Anwendung navigieren, können Sie Beginn erstellen, die Ihre eigenen Abfragen direkt in der Platform erstellen. Weitere Informationen zum Ausführen von SQL-Abfragen für Datasets in Data Lake finden Sie im Handbuch zu [laufenden Abfragen][query-service-running-queries]. Beispiel-SQL-Abfragen für die Verwendung von Adobe Analytics- und Adobe Target-Daten finden Sie in der [Abfragen-Referenz][query-service-sample-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
