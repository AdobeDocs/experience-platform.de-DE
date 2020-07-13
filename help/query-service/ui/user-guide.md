---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zum Abfrage-Editor für Adobe Experience Platform Query Service
topic: query editor
translation-type: tm+mt
source-git-commit: cc101b1a439408861961c6fcd0899ca7c48bfa04
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 95%

---


# Benutzerhandbuch zum Abfrage-Editor

Abfrage-Editor ist ein interaktives Tool von Adobe Experience Platform Query Service, mit dem Sie Abfragen für Kundenerlebnisdaten in der Experience Platform-Benutzeroberfläche schreiben, validieren und ausführen können. Der Abfrage-Editor unterstützt die Entwicklung von Abfragen für die Analyse und Datenexploration und ermöglicht Ihnen das Ausführen interaktiver Abfragen für Entwicklungszwecke sowie nicht interaktiver Abfragen zum Auffüllen von Datensätzen in Experience Platform.

Weitere Informationen zu Konzepten und Funktionen von Query Service finden Sie in der [Übersicht über Query Service][query-service-overview]. Weitere Informationen zum Navigieren in der Benutzeroberfläche von Query Service von Platform finden Sie in der [Übersicht über die Query Service-Benutzeroberfläche][query-service-ui].

## Erste Schritte

Der Abfrage-Editor bietet eine flexible Ausführung von Abfragen durch Herstellen einer Verbindung zu Query Service. Abfragen werden nur ausgeführt, solange diese Verbindung aktiv ist.

### Herstellen einer Verbindung zu Query Service

Der Abfrage-Editor benötigt beim Öffnen einige Sekunden, um Query Service zu initialisieren und eine Verbindung herzustellen. Die Konsole gibt an, ob eine Verbindung besteht (siehe unten). Wenn Sie versuchen, eine Abfrage auszuführen, bevor der Editor eine Verbindung hergestellt hat, wird die Ausführung verzögert, bis die Verbindung hergestellt ist.

![Bild](../images/queries/query-editor-overview/initializing-connection.png)

### Ausführen von Abfragen im Abfrage-Editor

Im Abfrage-Editor ausgeführte Abfragen werden interaktiv ausgeführt. Das bedeutet, dass die Abfrage abgebrochen wird, wenn Sie den Browser schließen oder wegnavigieren. Dies gilt auch für Abfragen, die zum Generieren von Datensätzen aus Abfrageausgaben vorgenommen werden.

## Erstellen von Abfragen mit dem Abfrage-Editor

Mit dem Abfrage-Editor können Sie Abfragen für Kundenerlebnisdaten schreiben, ausführen und speichern. Alle im Abfrage Editor ausgeführten oder gespeicherten Abfragen stehen allen Benutzern in Ihrem Unternehmen mit Zugriff auf Query Service zur Verfügung.

### Aufrufen des Abfrage-Editors

Klicken Sie in der Benutzeroberfläche von Experience Platform im linken Navigationsmenü auf **Abfragen**, um den Arbeitsbereich „Query Service“ zu öffnen. Klicken Sie dann oben rechts im Bildschirm auf **Abfrage erstellen**, um Abfragen zu schreiben. Dieser Link ist auf allen Seiten des Arbeitsbereichs „Query Service“ verfügbar.

![Bild](../images/queries/query-editor-overview/create-query.png)

### Schreiben von Abfragen

Der Abfrage-Editor ist so organisiert, dass das Schreiben von Abfragen so einfach wie möglich ist. Der folgende Screenshot zeigt, wie der Editor in der Benutzeroberfläche angezeigt wird, wobei die Schaltfläche **Abspielen** und das SQL-Eingabefeld hervorgehoben sind.

![Bild](../images/queries/query-editor-overview/editor.png)

Um Ihre Entwicklungszeit zu minimieren, sollten Sie Ihre Abfragen mit Begrenzungen für die zurückgegebenen Zeilen entwickeln. Beispiel: `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Nachdem Sie überprüft haben, ob Ihre Abfrage die erwartete Ausgabe erzeugt, entfernen Sie die Begrenzungen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren.

### Schreibwerkzeuge im Abfrage-Editor

- **Automatische Syntaxhervorhebung:** Erleichtert das Lesen und Organisieren von SQL.

![Bild](../images/queries/query-editor-overview/syntax-highlight.png)

- **SQL-Schlüsselwort automatisch vervollständigen:** Beginnen Sie mit der Eingabe Ihrer Abfrage, navigieren Sie mit den Pfeiltasten zum gewünschten Begriff und drücken Sie die **Eingabetaste**.

![Bild](../images/queries/query-editor-overview/syntax-auto.png)

- **Tabelle und Felder automatisch vervollständigen:** Beginnen Sie mit der Eingabe des Tabellennamens für den `SELECT`-Vorgang, navigieren Sie mit den Pfeiltasten zur gewünschten Tabelle und drücken Sie die **Eingabetaste**. Sobald eine Tabelle ausgewählt ist, erkennt das automatische Vervollständigung die Felder in dieser Tabelle.

![Bild](../images/queries/query-editor-overview/tables-auto.png)

### Fehlererkennung

Der Abfrage-Editor validiert eine Abfrage automatisch, während Sie sie schreiben, und bietet eine allgemeine SQL-Validierung und eine spezifische Ausführungsvalidierung. Wenn eine rote Unterstreichung unter der Abfrage angezeigt wird (wie in der Abbildung unten dargestellt), handelt es sich um einen Fehler in der Abfrage.

![Bild](../images/queries/query-editor-overview/syntax-error-highlight.png)

Wenn Fehler erkannt werden, können Sie die spezifischen Fehlermeldungen anzeigen, indem Sie den Mauszeiger über den SQL-Code bewegen.

![Bild](../images/queries/query-editor-overview/linting-error.png)

### Details zur Abfrage

Während Sie eine Abfrage im Abfrage-Editor anzeigen, stehen Ihnen im Bedienfeld *Details zur Abfrage* Werkzeuge zum Verwalten der ausgewählten Abfrage zur Verfügung.

![Bild](../images/queries/query-editor-overview/query-details.png)

In diesem Bedienfeld können Sie ein Ausgabedatensatz direkt über die Benutzeroberfläche generieren, die angezeigte Abfrage löschen oder benennen und den SQL-Code in einem einfach zu kopierenden Format auf der Registerkarte *SQL-Abfrage* anzeigen. In diesem Bedienfeld werden außerdem nützliche Metadaten angezeigt, z. B. das letzte Mal, dass die Abfrage geändert wurde und wer sie ggf. geändert hat. Klicken Sie auf **Ausgabedatensatz**, um einen Datensatz zu erstellen. Das Dialogfeld *Ausgabedatensatz* wird angezeigt. Geben Sie einen Namen und eine Beschreibung ein und klicken Sie dann auf **Abfrage ausführen**. Der neue Datensatz wird in der Query Service-Benutzeroberfläche von Platform auf der Registerkarte *Datensätze* angezeigt.

### Speichern von Abfragen

Der Abfrage-Editor bietet eine Speicherfunktion, mit der Sie eine Abfrage speichern und später daran arbeiten können. Klicken Sie zum Speichern einer Abfrage oben rechts im Abfragen-Editor auf **Speichern**. Bevor eine Abfrage gespeichert werden kann, muss über das Bedienfeld *Details zur Abfrage* ein Name für die Abfrage angegeben werden.

### Auffinden früherer Abfragen

Alle vom Abfrage-Editor ausgeführten Abfragen werden in der Tabelle „Protokoll“ erfasst. Sie können die Suchfunktion auf der Registerkarte *Protokoll* verwenden, um Abfrageausführungen zu finden. Gespeicherte Abfragen werden auf der Registerkarte *Durchsuchen* angezeigt.

Weitere Informationen finden Sie in der [Übersicht über die Query Service-Benutzeroberfläche][query-service-ui].

>[!NOTE]
>
>Nicht ausgeführte Abfragen werden nicht im Protokoll gespeichert. Damit die Abfrage in Query Service verfügbar ist, muss sie im Abfrage-Editor ausgeführt oder gespeichert werden.

## Ausführen von Abfragen mit dem Abfrage-Editor

Um eine Abfrage im Abfrage-Editor auszuführen, können Sie SQL im Editor eingeben oder eine frühere Abfrage über die Registerkarte *Protokoll* oder *Durchsuchen* laden und auf **Abspielen** klicken. Der Ausführungsstatus der Abfrage wird auf der Registerkarte *Konsole* angezeigt und die Ausgabedaten werden auf der Registerkarte *Ergebnisse* angezeigt.

### Konsole

Die Konsole bietet Informationen zum Status und zum Betrieb von Query Service. Die Konsole zeigt den Verbindungsstatus zu Query Service, die ausgeführten Abfragen und alle Fehlermeldungen an, die sich aus diesen Abfragen ergeben.

![Bild](../images/queries/query-editor-overview/console.png)

>[!NOTE]
>
>Die Konsole zeigt nur Fehler an, die beim Ausführen einer Abfrage aufgetreten sind. Es werden keine Fehler bei der Abfragevalidierung angezeigt, bevor eine Abfrage ausgeführt wird.

### Abfrageergebnisse

Nach Abschluss einer Abfrage werden die Ergebnisse auf der Registerkarte *Ergebnisse* neben der Registerkarte *Konsole* angezeigt. Diese Ansicht zeigt die tabellarische Ausgabe Ihrer Abfrage mit bis zu 100 Zeilen an. Mit dieser Ansicht können Sie überprüfen, ob Ihre Abfrage die erwartete Ausgabe erzeugt. Um einen Datensatz mit Ihrer Abfrage zu generieren, entfernen Sie Begrenzungen für zurückgegebene Zeilen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren. Anweisungen zum Generieren eines Datensatzes aus Abfragen im Abfrage-Editor finden Sie im [Tutorial zum Generieren von Datensätzen][query-service-create-datasets].

![Bild](../images/queries/query-editor-overview/query-results.png)

## Abfragen mit Abfrage Service-Lernvideo ausführen

Das folgende Video zeigt, wie Abfragen in der Benutzeroberfläche der Adobe Experience Platform und in einem PSQL-Client ausgeführt werden. Zusätzlich werden die Verwendung einzelner Eigenschaften in einem XDM-Objekt, die Verwendung von von Adobe definierten Funktionen und die Verwendung von CREATE TABLE AS SELECT (CTAS) demonstriert.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Nächste Schritte

Nachdem Sie nun wissen, welche Funktionen im Abfrage-Editor verfügbar sind und wie Sie in der Anwendung navigieren, können Sie Ihre eigenen Abfragen direkt in Platform erstellen. Weitere Informationen zum Ausführen von SQL-Abfragen für Datensätze im Data Lake finden Sie im Handbuch zum [Ausführen von Abfragen][query-service-running-queries]. Beispiel-SQL-Abfragen für die Arbeit mit Adobe Analytics- und Adobe Target-Daten finden Sie in der [Referenz für Beispielabfragen][query-service-sample-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../creating-queries/creating-queries.md
[query-service-sample-queries]: ../sample-queries/overview.md
[query-service-create-datasets]: ../creating-queries/create-datasets.md
