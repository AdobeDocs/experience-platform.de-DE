---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Editor;Abfrage-Editor;Abfrage-Dienst;Abfrage-Dienst;
solution: Experience Platform
title: Abfrage Editor-UI-Handbuch
topic-legacy: query editor
description: Der Abfrage Editor ist ein interaktives Tool des Adobe Experience Platform Abfrage Service, mit dem Sie Abfragen für Kundenerlebnisdaten in der Benutzeroberfläche der Experience Platform schreiben, validieren und ausführen können. Der Abfrage-Editor unterstützt die Entwicklung von Abfragen für die Analyse und Datenexploration und ermöglicht Ihnen das Ausführen interaktiver Abfragen für Entwicklungszwecke sowie nicht interaktiver Abfragen zum Auffüllen von Datensätzen in Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
translation-type: tm+mt
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Query Editor] UI-Handbuch

[!DNL Query Editor] ist ein interaktives Tool von Adobe Experience Platform  [!DNL Query Service], mit dem Sie Abfragen für Kundenerlebnisdaten in der  [!DNL Experience Platform] Benutzeroberfläche schreiben, validieren und ausführen können. [!DNL Query Editor] unterstützt die Entwicklung von Abfragen für die Analyse und Datenforschung und ermöglicht Ihnen, interaktive Abfragen zu Entwicklungszwecken sowie nicht interaktive Abfragen zum Ausfüllen von Datensätzen in auszuführen  [!DNL Experience Platform].

Weitere Informationen zu Konzepten und Funktionen von [!DNL Query Service] finden Sie unter [Übersicht über den Abfrage-Dienst][query-service-overview]. Weitere Informationen zum Navigieren in der Benutzeroberfläche des Abfrage-Dienstes unter [!DNL Platform] finden Sie unter [Übersicht über die Benutzeroberfläche des Abfrage-Dienstes][query-service-ui].

## Erste Schritte

[!DNL Query Editor] ermöglicht eine flexible Ausführung von Abfragen durch Verbinden mit  [!DNL Query Service]und Abfragen werden nur ausgeführt, wenn diese Verbindung aktiv ist.

### Verbindung zu [!DNL Query Service]

[!DNL Query Editor] Es dauert einige Sekunden, bis die Verbindung zum  [!DNL Query Service] Öffnen initialisiert wird. Die Konsole gibt an, ob eine Verbindung besteht (siehe unten). Wenn Sie versuchen, eine Abfrage auszuführen, bevor der Editor eine Verbindung hergestellt hat, wird die Ausführung verzögert, bis die Verbindung hergestellt ist.

![Bild](../images/ui/query-editor/connect.png)

### Ausführung von Abfragen von [!DNL Query Editor]

Von [!DNL Query Editor] ausgeführte Abfragen werden interaktiv ausgeführt. Das bedeutet, dass die Abfrage abgebrochen wird, wenn Sie den Browser schließen oder wegnavigieren. Dies gilt auch für Abfragen, die zum Generieren von Datensätzen aus Abfrageausgaben vorgenommen werden.

## Erstellen von Abfragen mit [!DNL Query Editor]

Mit [!DNL Query Editor] können Sie Abfragen für Kundenerlebnisdaten schreiben, ausführen und speichern. Alle in [!DNL Query Editor] ausgeführten oder gespeicherten Abfragen stehen allen Benutzern in Ihrem Unternehmen mit Zugriff auf [!DNL Query Service] zur Verfügung.

### Zugreifen auf [!DNL Query Editor]

Wählen Sie in der Benutzeroberfläche [!DNL Experience Platform] im linken Navigationsmenü **[!UICONTROL Abfragen]** aus, um den Arbeitsbereich [!DNL Query Service] zu öffnen. Wählen Sie dann oben rechts im Bildschirm **[!UICONTROL Abfrage erstellen]**, um Abfragen zu schreiben. Dieser Link ist auf allen Seiten im Arbeitsbereich [!DNL Query Service] verfügbar.

![Bild](../images/ui/query-editor/create-query.png)

### Schreiben von Abfragen

[!UICONTROL Der Abfrage-Editor ist so organisiert, dass das Schreiben von Abfragen so einfach wie möglich ist.] Der folgende Screenshot zeigt, wie der Editor in der Benutzeroberfläche angezeigt wird, wobei die Schaltfläche **Abspielen** und das SQL-Eingabefeld hervorgehoben sind.

![Bild](../images/ui/query-editor/editor.png)

Um Ihre Entwicklungszeit zu minimieren, sollten Sie Ihre Abfragen mit Begrenzungen für die zurückgegebenen Zeilen entwickeln. Beispiel: `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Nachdem Sie überprüft haben, ob Ihre Abfrage die erwartete Ausgabe erzeugt, entfernen Sie die Begrenzungen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren.

### Schreiben von Werkzeugen in [!DNL Query Editor]

- **Automatische Syntaxhervorhebung:** Erleichtert das Lesen und Organisieren von SQL.

![Bild](../images/ui/query-editor/syntax-highlight.png)

- **SQL-Schlüsselwort automatisch vervollständigen:** Beginnen Sie mit der Eingabe Ihrer Abfrage, navigieren Sie mit den Pfeiltasten zum gewünschten Begriff und drücken Sie die **Eingabetaste**.

![Bild](../images/ui/query-editor/syntax-auto.png)

- **Tabelle und Felder automatisch vervollständigen:** Beginnen Sie mit der Eingabe des Tabellennamens für den `SELECT`-Vorgang, navigieren Sie mit den Pfeiltasten zur gewünschten Tabelle und drücken Sie die **Eingabetaste**. Sobald eine Tabelle ausgewählt ist, erkennt das automatische Vervollständigung die Felder in dieser Tabelle.

![Bild](../images/ui/query-editor/tables-auto.png)

### Fehlererkennung

[!DNL Query Editor] überprüft eine Abfrage beim Schreiben automatisch, wobei eine generische SQL-Überprüfung und eine spezifische Ausführungsüberprüfung bereitgestellt werden. Wenn eine rote Unterstreichung unter der Abfrage angezeigt wird (wie in der Abbildung unten dargestellt), handelt es sich um einen Fehler in der Abfrage.

![Bild](../images/ui/query-editor/syntax-error-highlight.png)

Wenn Fehler erkannt werden, können Sie die spezifischen Fehlermeldungen anzeigen, indem Sie den Mauszeiger über den SQL-Code bewegen.

![Bild](../images/ui/query-editor/linting-error.png)

### Details zur Abfrage

Während Sie eine Abfrage in [!DNL Query Editor] anzeigen, bietet das Bedienfeld **[!UICONTROL Abfrage Details]** Tools zum Verwalten der ausgewählten Abfrage.

![Bild](../images/ui/query-editor/query-details.png)

In diesem Bedienfeld können Sie ein Ausgabedatensatz direkt über die Benutzeroberfläche generieren, die angezeigte Abfrage löschen oder benennen und den SQL-Code in einem einfach zu kopierenden Format auf der Registerkarte **[!UICONTROL SQL-Abfrage]** anzeigen. In diesem Bedienfeld werden außerdem nützliche Metadaten angezeigt, z. B. das letzte Mal, dass die Abfrage geändert wurde und wer sie ggf. geändert hat. Um einen Datensatz zu erstellen, wählen Sie **[!UICONTROL Ausgabedatensatz]**. Das Dialogfeld **[!UICONTROL Ausgabedatensatz]** wird angezeigt. Geben Sie einen Namen und eine Beschreibung ein und wählen Sie **[!UICONTROL Abfrage ausführen]**. Der neue Datensatz wird auf der Registerkarte **[!UICONTROL Datensätze]** der [!DNL Query Service]-Benutzeroberfläche unter [!DNL Platform] angezeigt.

### Speichern von Abfragen

[!DNL Query Editor] bietet eine Speicherfunktion, mit der Sie eine Abfrage speichern und später daran arbeiten können. Um eine Abfrage zu speichern, wählen Sie **[!UICONTROL Speichern]** oben rechts in [!DNL Query Editor]. Bevor eine Abfrage gespeichert werden kann, muss über das Bedienfeld **[!UICONTROL Details zur Abfrage]** ein Name für die Abfrage angegeben werden.

### Auffinden früherer Abfragen

Alle von [!DNL Query Editor] ausgeführten Abfragen werden in der Tabelle &quot;Protokoll&quot;erfasst. Sie können die Suchfunktion auf der Registerkarte **[!UICONTROL Protokoll]** verwenden, um Abfrageausführungen zu finden. Gespeicherte Abfragen werden auf der Registerkarte **[!UICONTROL Durchsuchen]** angezeigt.

Weitere Informationen finden Sie in der [Übersicht über die Query Service-Benutzeroberfläche][query-service-ui].

>[!NOTE]
>
> Nicht ausgeführte Abfragen werden nicht im Protokoll gespeichert. Damit die Abfrage in [!DNL Query Service] verfügbar ist, muss sie in [!DNL Query Editor] ausgeführt oder gespeichert werden.

## Ausführen von Abfragen mit dem Abfrage-Editor

Um eine Abfrage in [!DNL Query Editor] auszuführen, können Sie SQL im Editor eingeben oder eine vorherige Abfrage von der Registerkarte **[!UICONTROL Protokoll]** oder **[!UICONTROL Durchsuchen]** laden und **Abspielen** auswählen. Der Ausführungsstatus der Abfrage wird auf der Registerkarte **[!UICONTROL Konsole]** angezeigt und die Ausgabedaten werden auf der Registerkarte **[!UICONTROL Ergebnisse]** angezeigt.

### Konsole

Die Konsole bietet Informationen zum Status und zum Betrieb von [!DNL Query Service]. Die Konsole zeigt den Verbindungsstatus zu [!DNL Query Service], ausgeführte Abfragen-Vorgänge und alle Fehlermeldungen an, die sich aus diesen Abfragen ergeben.

![Bild](../images/ui/query-editor/console.png)

>[!NOTE]
>
> Die Konsole zeigt nur Fehler an, die beim Ausführen einer Abfrage aufgetreten sind. Es werden keine Fehler bei der Abfragevalidierung angezeigt, bevor eine Abfrage ausgeführt wird.

### Abfrageergebnisse

Nach Abschluss einer Abfrage werden die Ergebnisse auf der Registerkarte **[!UICONTROL Ergebnisse]** neben der Registerkarte **[!UICONTROL Konsole]** angezeigt. Diese Ansicht zeigt die tabellarische Ausgabe Ihrer Abfrage mit bis zu 100 Zeilen an. Mit dieser Ansicht können Sie überprüfen, ob Ihre Abfrage die erwartete Ausgabe erzeugt. Um einen Datensatz mit Ihrer Abfrage zu generieren, entfernen Sie Begrenzungen für zurückgegebene Zeilen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren. Anweisungen zum Generieren eines Datensatzes aus Abfragen finden Sie im Tutorial [Generieren von Datensätzen][query-service-create-datasets].[!DNL Query Editor]

![Bild](../images/ui/query-editor/query-results.png)

## Abfragen mit einem Tutorial zum Thema [!DNL Query Service] ausführen

Das folgende Video zeigt, wie Abfragen auf der Adobe Experience Platform-Oberfläche und in einem PSQL-Client ausgeführt werden. Darüber hinaus werden die Verwendung einzelner Eigenschaften in einem XDM-Objekt, die Verwendung von Adobe-definierten Funktionen und die Verwendung von CREATE TABLE AS SELECT (CTAS) demonstriert.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Nächste Schritte

Nachdem Sie wissen, welche Funktionen in [!DNL Query Editor] verfügbar sind und wie Sie in der Anwendung navigieren, können Sie Ihre eigenen Abfragen direkt in [!DNL Platform] erstellen. Weitere Informationen zum Ausführen von SQL-Abfragen für Datasets in [!DNL Data Lake] finden Sie im Handbuch [Ausführen von Abfragen][query-service-running-queries].

[query-service-overview]: ../home.md
[query-service-ui]: overview.md
[query-service-running-queries]: ../best-practices/writing-queries.md
[query-service-create-datasets]: ./create-datasets.md
