---
keywords: Experience Platform; Startseite; beliebte Themen; Abfrageeditor; Abfrageeditor; Query Service; Query Service;
solution: Experience Platform
title: Anleitung zur Benutzeroberfläche des Abfrage-Editors
topic-legacy: query editor
description: Der Abfrage-Editor ist ein interaktives Tool von Adobe Experience Platform Query Service, mit dem Sie Abfragen für Kundenerlebnisdaten in der Experience Platform-Benutzeroberfläche schreiben, validieren und ausführen können. Der Abfrage-Editor unterstützt die Entwicklung von Abfragen für die Analyse und Datenexploration und ermöglicht Ihnen das Ausführen interaktiver Abfragen für Entwicklungszwecke sowie nicht interaktiver Abfragen zum Auffüllen von Datensätzen in Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 7eaa808ecc644fdb9bc6b3fe1347c7651d54a33b
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 33%

---

# Handbuch für die [!DNL Query Editor]-Benutzeroberfläche

[!DNL Query Editor] ist ein interaktives Tool von Adobe Experience Platform,  [!DNL Query Service]mit dem Sie Abfragen für Kundenerlebnisdaten in der  [!DNL Experience Platform] Benutzeroberfläche schreiben, validieren und ausführen können. [!DNL Query Editor] unterstützt die Entwicklung von Abfragen für die Analyse und Datenexploration und ermöglicht Ihnen das Ausführen interaktiver Abfragen zu Entwicklungszwecken sowie nicht-interaktiver Abfragen zum Ausfüllen von Datensätzen in  [!DNL Experience Platform].

Weitere Informationen zu Konzepten und Funktionen von [!DNL Query Service] finden Sie unter [Query Service - Übersicht](../home.md). Weitere Informationen zum Navigieren in der Query Service-Benutzeroberfläche unter [!DNL Platform] finden Sie in der [Übersicht über die Query Service-Benutzeroberfläche](./overview.md).

## Erste Schritte

[!DNL Query Editor] bietet flexible Ausführung von Abfragen durch Verbinden mit  [!DNL Query Service]. Abfragen werden nur ausgeführt, wenn diese Verbindung aktiv ist.

### Verbindung zu [!DNL Query Service]

[!DNL Query Editor] Es dauert ein paar Sekunden,  [!DNL Query Service] wenn die Initialisierung und Verbindung mit erfolgt. Die Konsole gibt an, ob eine Verbindung besteht (siehe unten). Wenn Sie versuchen, eine Abfrage auszuführen, bevor der Editor eine Verbindung hergestellt hat, wird die Ausführung verzögert, bis die Verbindung hergestellt ist.

![Bild](../images/ui/query-editor/connect.png)

### Ausführen von Abfragen über [!DNL Query Editor]

Von [!DNL Query Editor] ausgeführte Abfragen werden interaktiv ausgeführt. Das bedeutet, dass die Abfrage abgebrochen wird, wenn Sie den Browser schließen oder wegnavigieren. Dies gilt auch für Abfragen, die zum Generieren von Datensätzen aus Abfrageausgaben vorgenommen werden.

## Abfragebearbeitung mit [!DNL Query Editor]

Mit [!DNL Query Editor] können Sie Abfragen für Kundenerlebnisdaten schreiben, ausführen und speichern. Alle Abfragen, die in [!DNL Query Editor] ausgeführt oder gespeichert werden, stehen allen Benutzern in Ihrer Organisation mit Zugriff auf [!DNL Query Service] zur Verfügung.

### Zugreifen auf [!DNL Query Editor]

Wählen Sie in der Benutzeroberfläche [!DNL Experience Platform] im linken Navigationsmenü **[!UICONTROL Abfragen]** aus, um den Arbeitsbereich [!DNL Query Service] zu öffnen. Wählen Sie dann **[!UICONTROL Abfrage erstellen]** oben rechts im Bildschirm aus, um Abfragen zu schreiben. Dieser Link ist auf allen Seiten im Arbeitsbereich [!DNL Query Service] verfügbar.

![Bild](../images/ui/query-editor/create-query.png)

### Schreiben von Abfragen

[!UICONTROL Der Abfrage-Editor ist so organisiert, dass das Schreiben von Abfragen so einfach wie möglich ist.] Der folgende Screenshot zeigt, wie der Editor in der Benutzeroberfläche angezeigt wird, wobei die Schaltfläche **Abspielen** und das SQL-Eingabefeld hervorgehoben sind.

![Bild](../images/ui/query-editor/editor.png)

Um Ihre Entwicklungszeit zu minimieren, sollten Sie Ihre Abfragen mit Begrenzungen für die zurückgegebenen Zeilen entwickeln. Beispiel: `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Nachdem Sie überprüft haben, ob Ihre Abfrage die erwartete Ausgabe erzeugt, entfernen Sie die Begrenzungen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren.

### Schreibwerkzeuge in [!DNL Query Editor]

- **Automatische Syntaxhervorhebung:** Erleichtert das Lesen und Organisieren von SQL.

![Bild](../images/ui/query-editor/syntax-highlight.png)

- **SQL-Schlüsselwort automatisch vervollständigen:** Beginnen Sie mit der Eingabe Ihrer Abfrage, navigieren Sie mit den Pfeiltasten zum gewünschten Begriff und drücken Sie die **Eingabetaste**.

![Bild](../images/ui/query-editor/syntax-auto.png)

- **Tabelle und Felder automatisch vervollständigen:** Beginnen Sie mit der Eingabe des Tabellennamens für den `SELECT`-Vorgang, navigieren Sie mit den Pfeiltasten zur gewünschten Tabelle und drücken Sie die **Eingabetaste**. Sobald eine Tabelle ausgewählt ist, erkennt das automatische Vervollständigung die Felder in dieser Tabelle.

![Bild](../images/ui/query-editor/tables-auto.png)

### Fehlererkennung

[!DNL Query Editor] validiert eine Abfrage beim Schreiben automatisch, wobei eine allgemeine SQL-Validierung und eine spezifische Ausführungsvalidierung bereitgestellt werden. Wenn eine rote Unterstreichung unter der Abfrage angezeigt wird (wie in der Abbildung unten dargestellt), handelt es sich um einen Fehler in der Abfrage.

![Bild](../images/ui/query-editor/syntax-error-highlight.png)

Wenn Fehler erkannt werden, können Sie die spezifischen Fehlermeldungen anzeigen, indem Sie den Mauszeiger über den SQL-Code bewegen.

![Bild](../images/ui/query-editor/linting-error.png)

### Details zur Abfrage

Während Sie eine Abfrage in [!DNL Query Editor] anzeigen, bietet das Bedienfeld **[!UICONTROL Abfragedetails]** Tools zum Verwalten der ausgewählten Abfrage.

![Bild](../images/ui/query-editor/query-details.png)

In diesem Bedienfeld können Sie einen Ausgabedatensatz direkt über die Benutzeroberfläche generieren, die angezeigte Abfrage löschen oder benennen und der Abfrage einen Zeitplan hinzufügen.

In diesem Bedienfeld werden außerdem nützliche Metadaten angezeigt, z. B. das letzte Mal, dass die Abfrage geändert wurde und wer sie ggf. geändert hat. Um einen Datensatz zu generieren, wählen Sie **[!UICONTROL Ausgabedatensatz]** aus. Das Dialogfeld **[!UICONTROL Ausgabedatensatz]** wird angezeigt. Geben Sie einen Namen und eine Beschreibung ein und wählen Sie dann **[!UICONTROL Abfrage ausführen]** aus. Der neue Datensatz wird auf der Registerkarte **[!UICONTROL Datensätze]** der [!DNL Query Service]-Benutzeroberfläche unter [!DNL Platform] angezeigt.

### Geplante Abfragen {#scheduled-queries}

>[!NOTE]
>
> Sie können einen Zeitplan nur zu einer Abfrage hinzufügen, die bereits erstellt, gespeichert und ausgeführt wurde. Außerdem können Sie **nicht** einen Zeitplan zu einer parametrisierten Abfrage hinzufügen.

Um einen Zeitplan zu einer Abfrage hinzuzufügen, wählen Sie **[!UICONTROL Zeitplan hinzufügen]** aus.

![Bild](../images/ui/query-editor/add-schedule.png)

Die Seite **[!UICONTROL Details des Zeitplans]** wird angezeigt. Auf dieser Seite können Sie die Häufigkeit der geplanten Abfrage, das Datum der Ausführung der geplanten Abfrage sowie den Datensatz auswählen, in den die Abfrage exportiert werden soll.

![Bild](../images/ui/query-editor/schedule-details.png)

Sie können die folgenden Optionen für **[!UICONTROL Häufigkeit]** auswählen:

- **[!UICONTROL Stündlich]**: Die geplante Abfrage wird für den ausgewählten Datumsbereich stündlich ausgeführt.
- **[!UICONTROL Täglich]**: Die geplante Abfrage wird alle X Tage zum ausgewählten Zeitpunkt und zum ausgewählten Zeitraum ausgeführt. Bitte beachten Sie, dass die ausgewählte Zeit in **UTC** und nicht in Ihrer lokalen Zeitzone liegt.
- **[!UICONTROL Wöchentlich]**: Die ausgewählte Abfrage wird an den Wochentagen, zur Uhrzeit und zum ausgewählten Datumsbereich ausgeführt. Bitte beachten Sie, dass die ausgewählte Zeit in **UTC** und nicht in Ihrer lokalen Zeitzone liegt.
- **[!UICONTROL Monatlich]**: Die ausgewählte Abfrage wird jeden Monat am Tag, zur Uhrzeit und zum ausgewählten Datumsbereich ausgeführt. Bitte beachten Sie, dass die ausgewählte Zeit in **UTC** und nicht in Ihrer lokalen Zeitzone liegt.
- **[!UICONTROL Jährlich]**: Die ausgewählte Abfrage wird jedes Jahr an dem von Ihnen ausgewählten Tag, Monat, Uhrzeit und Zeitraum ausgeführt. Bitte beachten Sie, dass die ausgewählte Zeit in **UTC** und nicht in Ihrer lokalen Zeitzone liegt.

Für den Datensatz haben Sie die Möglichkeit, entweder einen vorhandenen Datensatz zu verwenden oder einen neuen Datensatz zu erstellen.

>[!IMPORTANT]
>
> Da Sie einen vorhandenen Datensatz verwenden oder einen neuen erstellen, müssen Sie **not** entweder `INSERT INTO` oder `CREATE TABLE AS SELECT` als Teil der Abfrage einbeziehen, da die Datensätze bereits festgelegt sind. Wenn Sie `INSERT INTO` oder `CREATE TABLE AS SELECT` als Teil Ihrer geplanten Abfragen einbeziehen, wird ein Fehler ausgegeben.

Nachdem Sie alle diese Details bestätigt haben, wählen Sie **[!UICONTROL Speichern]** aus, um einen Zeitplan zu erstellen.

Die Seite mit den Abfragedetails wird erneut angezeigt und zeigt nun die Details des neu erstellten Zeitplans einschließlich der Zeitplan-ID, des Zeitplans selbst und des Ausgabedatensatzes des Zeitplans an. Sie können die Zeitplan-ID verwenden, um weitere Informationen zu den Ausführungen der geplanten Abfrage selbst zu erhalten. Weiterführende Informationen finden Sie im [Handbuch zu geplanten Abfrage-Run-Endpunkten](../api/runs-scheduled-queries.md).

>[!NOTE]
>
> Sie können die Abfragevorlage **eine** nur mithilfe der Benutzeroberfläche planen. Wenn Sie einer Abfragevorlage zusätzliche Zeitpläne hinzufügen möchten, müssen Sie die API verwenden. Wenn mit der API bereits ein Zeitplan hinzugefügt wurde, können Sie **not** zusätzliche Zeitpläne über die Benutzeroberfläche hinzufügen. Wenn bereits mehrere Zeitpläne an eine Abfragevorlage angehängt sind, wird nur der älteste Zeitplan angezeigt. Informationen zum Hinzufügen von Zeitplänen mithilfe der API finden Sie im [Handbuch zum geplanten Abfrageendpunkt](../api/scheduled-queries.md).
>
> Darüber hinaus sollten Sie die Seite aktualisieren, wenn Sie sicherstellen möchten, dass Sie über den neuesten Status für den Zeitplan verfügen, den Sie anzeigen.

#### Zeitplan löschen

Sie können einen Zeitplan löschen, indem Sie **[!UICONTROL einen Zeitplan löschen]** auswählen.

![Bild](../images/ui/query-editor/delete-schedule.png)

>[!IMPORTANT]
>
> Wenn Sie einen Zeitplan für eine Abfrage löschen möchten, müssen Sie den Zeitplan zuerst deaktivieren.

### Speichern von Abfragen

[!DNL Query Editor] bietet eine Speicherfunktion, mit der Sie eine Abfrage speichern und später daran arbeiten können. Um eine Abfrage zu speichern, wählen Sie **[!UICONTROL Save]** in der oberen rechten Ecke von [!DNL Query Editor] aus. Bevor eine Abfrage gespeichert werden kann, muss über das Bedienfeld **[!UICONTROL Details zur Abfrage]** ein Name für die Abfrage angegeben werden.

### Auffinden früherer Abfragen

Alle von [!DNL Query Editor] ausgeführten Abfragen werden in der Log-Tabelle erfasst. Sie können die Suchfunktion auf der Registerkarte **[!UICONTROL Protokoll]** verwenden, um Abfrageausführungen zu finden. Gespeicherte Abfragen werden auf der Registerkarte **[!UICONTROL Durchsuchen]** angezeigt.

Weitere Informationen finden Sie in der [Übersicht über die Query Service-Benutzeroberfläche](./overview.md).

>[!NOTE]
>
> Nicht ausgeführte Abfragen werden nicht im Protokoll gespeichert. Damit die Abfrage in [!DNL Query Service] verfügbar ist, muss sie in [!DNL Query Editor] ausgeführt oder gespeichert werden.

## Ausführen von Abfragen mit dem Abfrage-Editor

Um eine Abfrage in [!DNL Query Editor] auszuführen, können Sie SQL im Editor eingeben oder eine frühere Abfrage von der Registerkarte **[!UICONTROL Protokoll]** oder **[!UICONTROL Durchsuchen]** laden und **Abspielen** auswählen. Der Ausführungsstatus der Abfrage wird auf der Registerkarte **[!UICONTROL Konsole]** angezeigt und die Ausgabedaten werden auf der Registerkarte **[!UICONTROL Ergebnisse]** angezeigt.

### Konsole

Die Konsole bietet Informationen zum Status und zum Betrieb von [!DNL Query Service]. Die Konsole zeigt den Verbindungsstatus zu [!DNL Query Service], die ausgeführten Abfragevorgänge sowie alle Fehlermeldungen an, die aus diesen Abfragen resultieren.

![Bild](../images/ui/query-editor/console.png)

>[!NOTE]
>
> Die Konsole zeigt nur Fehler an, die beim Ausführen einer Abfrage aufgetreten sind. Es werden keine Fehler bei der Abfragevalidierung angezeigt, bevor eine Abfrage ausgeführt wird.

### Abfrageergebnisse

Nach Abschluss einer Abfrage werden die Ergebnisse auf der Registerkarte **[!UICONTROL Ergebnisse]** neben der Registerkarte **[!UICONTROL Konsole]** angezeigt. Diese Ansicht zeigt die tabellarische Ausgabe Ihrer Abfrage mit bis zu 100 Zeilen an. Mit dieser Ansicht können Sie überprüfen, ob Ihre Abfrage die erwartete Ausgabe erzeugt. Um einen Datensatz mit Ihrer Abfrage zu generieren, entfernen Sie Begrenzungen für zurückgegebene Zeilen und führen Sie die Abfrage mit `CREATE TABLE tablename AS SELECT` aus, um einen Datensatz mit der Ausgabe zu generieren. Anweisungen zum Generieren eines Datensatzes aus Abfrageergebnissen finden Sie im Tutorial [Generieren von Datensätzen](./create-datasets.md) .[!DNL Query Editor]

![Bild](../images/ui/query-editor/query-results.png)

## Video-Tutorial zum Ausführen von Abfragen mit [!DNL Query Service]

Im folgenden Video erfahren Sie, wie Sie Abfragen in der Adobe Experience Platform-Benutzeroberfläche und in einem PSQL-Client ausführen. Darüber hinaus wird die Verwendung einzelner Eigenschaften in einem XDM-Objekt, die Verwendung von Adobe-definierten Funktionen und die Verwendung von CREATE TABLE AS SELECT (CTAS) demonstriert.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Nächste Schritte

Nachdem Sie nun wissen, welche Funktionen in [!DNL Query Editor] verfügbar sind und wie Sie in der Anwendung navigieren, können Sie Ihre eigenen Abfragen direkt in [!DNL Platform] erstellen. Weitere Informationen zum Ausführen von SQL-Abfragen für Datensätze in [!DNL Data Lake] finden Sie im Handbuch zu [laufenden Abfragen](../best-practices/writing-queries.md).
