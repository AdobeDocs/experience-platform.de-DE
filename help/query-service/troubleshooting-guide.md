---
keywords: Experience Platform;Startseite;beliebte Themen;abfrage-service;Abfrage-Service;Handbuch zur Fehlerbehebung;FAQ;Fehlerbehebung
solution: Experience Platform
title: Häufig gestellte Fragen zu Query Service und Data Distiller
description: Dieses Dokument enthält häufige Fragen und Antworten zu Query Service und Data Distiller. Zu den Themen gehören der Datenexport, Tools von Drittanbietern und PSQL-Fehler.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: f0656fcde077fc6c983a7a2d8dc21d2548fa7605
workflow-type: tm+mt
source-wordcount: '5186'
ht-degree: 78%

---

# Häufig gestellte Fragen zu Query Service und Data Distiller

In diesem Dokument werden häufig gestellte Fragen zu Query Service und Data Distiller beantwortet. Es enthält auch häufig angezeigte Fehler-Codes bei der Verwendung des Produkts „Abfragen“ für die Datenvalidierung oder das Zurückschreiben umgewandelter Daten in den Data Lake. Fragen und Fehlerbehebungen für andere Adobe Experience Platform-Services finden Sie im [Handbuch zur Fehlerbehebung bei Experience Platform](../landing/troubleshooting.md).

Zwei grundlegende Fragen erläutern die Zusammenarbeit von Query Service und Data Distiller in Adobe Experience Platform.

## Welche Beziehung besteht zwischen dem Abfrage-Service und Data Distiller?

Query Service und Data Distiller sind unterschiedliche, komplementäre Komponenten, die spezielle Datenabfragefunktionen bereitstellen. Query Service ist für Ad-hoc-Abfragen konzipiert, um aufgenommene Daten zu untersuchen, zu validieren und mit ihnen zu experimentieren, ohne den Data Lake zu ändern. Im Gegensatz dazu konzentriert sich Data Distiller auf Batch-Abfragen, die Daten transformieren und anreichern, wobei die Ergebnisse zur zukünftigen Verwendung zurück in den Data Lake gespeichert werden. Batch-Abfragen in Data Distiller können geplant, überwacht und verwaltet werden, wodurch eine tiefer gehende Datenverarbeitung und -bearbeitung unterstützt wird, die durch den Abfrage-Service allein nicht möglich ist.

Gemeinsam ermöglicht Query Service schnelle Einblicke, während Data Distiller tief greifende, persistente Datenumwandlungen ermöglicht.

## Was ist der Unterschied zwischen Abfrage-Service und Data Distiller?

**Abfrage-Service**: Wird für SQL-Abfragen verwendet, die sich auf die Untersuchung, Validierung und das Experimentieren von Daten konzentrieren. Ausgaben werden nicht im Data Lake gespeichert und die Ausführungszeit ist auf 10 Minuten beschränkt. Ad-hoc-Abfragen eignen sich für einfache, interaktive Datenprüfungen und -analysen.

**Data Distiller**: Ermöglicht Batch-Abfragen, die Daten verarbeiten, bereinigen und anreichern, wobei die Ergebnisse im Data Lake gespeichert werden. Diese Abfragen unterstützen eine längere Ausführung (bis zu 24 Stunden) und zusätzliche Funktionen wie Planung, Überwachung und beschleunigtes Reporting. Data Distiller eignet sich ideal für detaillierte Datenmanipulationen und geplante Datenverarbeitungsaufgaben.

Ausführlichere Informationen finden Sie [ Dokument zum ](./packaging.md) von Query Service.

## Fragenkategorien {#categories}

Die folgende Liste von Antworten auf häufig gestellte Fragen ist in folgende Kategorien unterteilt:

- [Allgemein](#general)
- [Data Distiller](#data-distiller)
- [Benutzeroberfläche für Abfragen](#queries-ui)
- [Datensatzbeispiele](#dataset-samples)
- [Exportieren von Daten](#exporting-data)
- [SQL-Syntax](#sql-syntax) 
- [ITAS-Abfragen](#itas-queries)
- [Drittanbieter-Tools](#third-party-tools)
- [PostgreSQL-API-Fehler](#postgresql-api-errors)
- [REST-API-Fehler](#rest-api-errors)

## Allgemeine Fragen zum Abfrage-Service {#general}

Dieser Abschnitt enthält Informationen zu Performance, Beschränkungen und Prozessen.

### Kann ich die Funktion zur automatischen Vervollständigung im Editor des Abfrage-Service deaktivieren?

+++Antwort 
Nr. Das Deaktivieren der Funktion zur automatischen Vervollständigung wird derzeit vom Editor nicht unterstützt.
+++

### Warum wird der Abfrage-Editor manchmal langsam, wenn ich eine Abfrage eingebe?

+++Antwort
Eine potenzielle Ursache ist die Funktion zur automatischen Vervollständigung. Die Funktion verarbeitet bestimmte Metadatenbefehle, die den Editor bei der Abfragebearbeitung gelegentlich verlangsamen können.
+++

### Kann ich [!DNL Postman] für die Abfrage-Service-API verwenden?

+++Antwort
Ja, Sie können alle Adobe-API-Dienste mithilfe von [!DNL Postman] (eine kostenlose Drittanbieteranwendung) visualisieren und mit ihnen interagieren. Sehen Sie sich das [[!DNL Postman] Setup-Handbuch](https://video.tv.adobe.com/v/31575?captions=ger) an, um schrittweise Anleitungen zum Einrichten eines Projekts in der Adobe Developer Console und zum Abrufen aller erforderlichen Anmeldedaten für die Verwendung mit [!DNL Postman] zu erhalten. In der offiziellen Dokumentation finden Sie [Anleitungen zum Starten, Ausführen und Freigeben von  [!DNL Postman] -Sammlungen](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### Gibt es eine Begrenzung für die maximale Anzahl von Zeilen, die von einer Abfrage über die Benutzeroberfläche zurückgegeben werden?

+++Antwort
Ja, der Abfrage-Service wendet intern eine Beschränkung von 50.000 Zeilen an, es sei denn, extern wird eine explizite Begrenzung angegeben. Weitere Informationen finden Sie in den Leitlinien zur [interaktiven Ausführung von Abfragen](./best-practices/writing-queries.md#interactive-query-execution).
+++

### Kann ich Abfragen verwenden, um Zeilen zu aktualisieren?

+++Antwort
In Batch-Abfragen wird das Aktualisieren einer Zeile im Datensatz nicht unterstützt.
+++

### Gibt es eine Größenbeschränkung für die resultierende Ausgabe einer Abfrage?

+++Antwort 
Nr. Es gibt keine Begrenzung der Datengröße, aber es gibt eine Zeitbeschränkung von 10 Minuten für Abfragen aus einer interaktiven Sitzung. Wenn die Abfrage als Batch-CTAS ausgeführt wird, gilt keine Zeitbeschränkung auf 10 Minuten. Weitere Informationen finden Sie in den Leitlinien zur [interaktiven Ausführung von Abfragen](./best-practices/writing-queries.md#interactive-query-execution).
+++

### Wie kann ich verhindern, dass meine Abfragen nach 10 Minuten ablaufen?

+++Antwort
Es werden eine oder mehrere der folgenden Lösungen empfohlen, wenn bei Abfragen eine Zeitüberschreitung auftritt.

- [Konvertieren Sie die Abfrage in eine CTAS-Abfrage](./sql/syntax.md#create-table-as-select) und planen Sie die Ausführung. Eine Ausführung kann entweder [über die Benutzeroberfläche](./ui/user-guide.md#scheduled-queries) oder die [API](./api/scheduled-queries.md#create) geplant werden.
- Führen Sie die Abfrage auf einen kleineren Datensatz aus, indem Sie zusätzliche [Filterbedingungen](https://spark.apache.org/docs/latest/api/sql/index.html#filter) anwenden.
- [Führen Sie den Befehl „EXPLAIN“ aus](./sql/syntax.md#explain), um weitere Details zu erhalten.
- Überprüfen Sie die Statistiken der Daten im Datensatz.
- Konvertieren Sie die Abfrage in eine vereinfachte Form und führen Sie sie mithilfe von [vorbereiteten Anweisungen](./sql/prepared-statements.md) erneut aus.
+++

### Gibt es Probleme oder Auswirkungen auf die Performance des Abfrage-Service, wenn mehrere Abfragen gleichzeitig ausgeführt werden?

+++Antwort 
Nr. Der Abfrage-Service verfügt über eine Funktion zur automatischen Skalierung, die sicherstellt, dass gleichzeitige Abfragen keine merklichen Auswirkungen auf die Performance des Service haben.
+++

### Kann ich reservierte Keywords als Spaltennamen verwenden?

+++Antwort
Es gibt bestimmte reservierte Keywords, die nicht als Spaltenname verwendet werden können, z. B.: `ORDER`, `GROUP BY`, `WHERE` und `DISTINCT`. Wenn Sie diese Keywords verwenden möchten, müssen Sie diese Spalten mit Escape-Zeichen versehen.
+++

### Wie finde ich einen Spaltennamen aus einem hierarchischen Datensatz?

+++Antwort
Die folgenden Schritte beschreiben, wie Sie eine tabellarische Ansicht eines Datensatzes einschließlich aller verschachtelten Felder und Spalten in einer vereinfachten Form über die Benutzeroberfläche anzeigen.

- Wählen Sie nach der Anmeldung bei Experience Platform die Option **[!UICONTROL Datensätze]** im linken Navigationsbereich der Benutzeroberfläche, um zum Dashboard [!UICONTROL Datensätze] zu navigieren.
- Die Datensatz-Registerkarte [!UICONTROL Durchsuchen] wird geöffnet. Sie können die Suchleiste verwenden, um die verfügbaren Optionen zu verfeinern. Wählen Sie einen Datensatz aus der Liste aus.

![Das Dashboard „Datensätze“ in der Experience Platform-Benutzeroberfläche mit Suchleiste und hervorgehobenem Datensatz.](./images/troubleshooting/dataset-selection.png)

- Der Bildschirm [!UICONTROL Datensatzaktivität] wird angezeigt. Wählen Sie **[!UICONTROL Vorschau des Datensatzes anzeigen]**, um einen Dialog des XDM-Schemas und eine tabellarische Ansicht von vereinfachten Daten aus dem ausgewählten Datensatz zu öffnen. Weitere Informationen finden Sie in der [Dokumentation zur Vorschau eines Datensatzes](../catalog/datasets/user-guide.md#preview-a-dataset)

![Die Registerkarte „Datensatzaktivität“ im Dashboard „Datensätze“ mit hervorgehobener Vorschau des Datensatzes.](./images/troubleshooting/dataset-preview.png)

- Wählen Sie ein beliebiges Feld aus dem Schema aus, um seinen Inhalt in einer vereinfachten Spalte anzuzeigen. Der Name der Spalte wird oberhalb ihres Inhalts rechts auf der Seite angezeigt. Sie sollten diesen Namen kopieren, um ihn für die Abfrage dieses Datensatzes zu verwenden.

![Das XDM-Schema und die Tabellenansicht der vereinfachten Daten. Der Spaltenname eines verschachtelten Datensatzes wird in der Benutzeroberfläche hervorgehoben.](./images/troubleshooting/column-name.png)

Die vollständige Anleitung finden Sie in der Dokumentation zum [Arbeiten mit verschachtelten Datenstrukturen](./key-concepts/nested-data-structures.md) mit dem Abfrage-Editor oder dem Client eines Drittanbieters.
+++

### Wie beschleunige ich eine Abfrage für einen Datensatz, der Arrays enthält?

+++Antwort
Um die Performance von Abfragen von Datensätzen mit Arrays zu verbessern, sollten Sie das Array zunächst während der Laufzeit als [CTAS-Abfrage](./sql/syntax.md#create-table-as-select) [auflösen](https://spark.apache.org/docs/latest/api/sql/index.html#explode). Danach können Sie es weiter auf Möglichkeiten zur Verbesserung der Verarbeitungszeit untersuchen.
+++

### Warum wird meine CTAS-Abfrage für eine geringe Anzahl von Zeilen nach vielen Stunden immer noch bearbeitet?

+++Antwort
Wenn die Abfrage für einen sehr kleinen Datensatz lange gedauert hat, wenden Sie sich an den Kunden-Support.

Es kann verschiedene Gründe dafür geben, dass eine Abfrage bei der Verarbeitung hängenbleibt. Um die genaue Ursache zu bestimmen, ist eine gründliche Analyse von Fall zu Fall erforderlich. [Kontaktieren Sie den Kunden-Support von Adobe](#customer-support) zu diesem Prozess.
+++

### Wie kontaktiere ich den Kunden-Support von Adobe? {#customer-support}

+++Antwort
[Eine vollständige Liste der Telefonnummern des Kunden-Supports von Adobe](https://helpx.adobe.com/de/contact/phone.html) ist auf der Hilfeseite von Adobe verfügbar. Alternativ können Sie Hilfe online finden, indem Sie die folgenden Schritte ausführen:

- Navigieren Sie zu [https://www.adobe.com/](https://www.adobe.com/) in Ihrem Webbrowser.
- Wählen Sie rechts in der oberen Navigationsleiste die Option **[!UICONTROL Anmelden]**.

![Die Adobe-Website mit hervorgehobener Option „Anmelden“.](./images/troubleshooting/adobe-sign-in.png)

- Verwenden Sie Ihre Adobe ID und Ihr Kennwort, die mit Ihrer Adobe-Lizenz registriert sind.
- Wählen Sie **[!UICONTROL Hilfe und Support]** über die Navigationsleiste am oberen Bildschirmrand.

![Das Dropdown-Menü der oberen Navigationsleiste mit hervorgehobenen Optionen „Hilfe und Support“, „Enterprise-Support“ und „Kontakt“.](./images/troubleshooting/help-and-support.png)

Es wird ein Dropdown-Banner mit dem Bereich [!UICONTROL Hilfe und Support] geöffnet. Wählen Sie **[!UICONTROL Kontakt]**, um den virtuellen Assistenten für Kundenunterstützung von Adobe zu öffnen, oder wählen Sie **[!UICONTROL Enterprise-Support]**, um spezielle Hilfe für große Unternehmen zu erhalten.
+++

### Wie implementiere ich eine sequenzielle Auftragsreihe so, dass nachfolgende Aufträge nicht ausgeführt werden, wenn der vorherige Auftrag nicht erfolgreich abgeschlossen wurde?

+++Antwort
Mit der Funktion für anonyme Blöcke können Sie eine oder mehrere SQL-Anweisungen verketten, die nacheinander ausgeführt werden. Sie beinhalten auch die Möglichkeit der Ausnahmebehandlung.

Weitere Informationen finden Sie in der [Dokumentation zu anonymen Blöcken](./key-concepts/anonymous-block.md).
+++

### Wie implementiere ich eine benutzerdefinierte Attribution im Abfrage-Service?

+++Antwort
Es gibt zwei Möglichkeiten, benutzerdefinierte Attributionen zu implementieren:

1. Verwenden Sie eine Kombination aus vorhandenen, [von Adobe definierten Funktionen](./sql/adobe-defined-functions.md), um festzustellen, ob die Anforderungen des Anwendungsfalls erfüllt sind.
1. Wenn der vorherige Vorschlag nicht auf Ihren Anwendungsfall anwendbar ist, sollten Sie eine Kombination aus [Fensterfunktionen](./sql/adobe-defined-functions.md#window-functions) verwenden. Fensterfunktionen betrachten alle Ereignisse in einer Sequenz. Sie ermöglichen es Ihnen auch, die Verlaufsdaten zu überprüfen und können in jeder beliebigen Kombination verwendet werden.
+++

### Kann ich meine Abfragen als Vorlage speichern, damit ich sie einfach wiederverwenden kann?

+++Antwort
Ja, Sie können Abfragen mithilfe von vorbereiteten Anweisungen als Vorlage verwenden. Vorbereitete Anweisungen können die Performance optimieren und das wiederholte Parsen derselben Abfrage vermeiden. Weitere Informationen finden Sie in der [Dokumentation zu vorbereiteten Anweisungen](./sql/prepared-statements.md).
+++

### Wie erhalte ich Fehlerprotokolle für eine Abfrage? {#error-logs}

+++Antwort
Um Fehlerprotokolle für eine bestimmte Abfrage abzurufen, müssen Sie zunächst die Abfrage-Service-API verwenden, um die Details des Abfrageprotokolls abzurufen. Die HTTP-Antwort enthält die Abfrage-IDs, die zur Untersuchung eines Abfragefehlers erforderlich sind.

Verwenden Sie den Befehl „GET“, um mehrere Abfragen abzurufen. Informationen zum Aufruf der API finden Sie in der [Dokumentation zu Beispielen für API-Aufrufe](./api/queries.md#sample-api-calls).

Identifizieren Sie in der Antwort die Abfrage, die Sie untersuchen möchten, und stellen Sie mithilfe ihres `id`-Werts eine weitere GET-Anfrage. Vollständige Anweisungen finden Sie in der [Dokumentation zum Abrufen einer Abfrage nach ID](./api/queries.md#retrieve-a-query-by-id).

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zurück und enthält das `errors`-Array. Die Antwort wurde zur Vereinfachung gekürzt.

```json
{
    "isInsertInto": false,
    "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
    "clientId": "8c2455819a624534bb665c43c3759877",
    "state": "SUCCESS",
    "rowCount": 0,
    "errors": [{
      'code': '58000', 
      'message': 'Batch query execution gets : [failed reason ErrorCode: 58000 Batch query execution gets : [Analysis error encountered. Reason: [sessionId: f055dc73-1fbd-4c9c-8645-efa609da0a7b Function [varchar] not defined.]]]', 
      'errorType': 'USER_ERROR'
      }],
    "isCTAS": false,
    "version": 1,
    "id": "343388b0-e0dd-4227-a75b-7fc945ef408a",
}
```

Die [Referenzdokumentation zur Abfrage-Service-API](https://www.adobe.io/experience-platform-apis/references/query-service/) bietet weitere Informationen zu allen verfügbaren Endpunkten.
+++

### Was bedeutet „Fehler beim Validieren des Schemas“?

+++Antwort
Die Meldung „Fehler beim Validieren des Schemas“ bedeutet, dass das System ein Feld innerhalb des Schemas nicht finden kann. Sie sollten das Best Practice-Dokument für [Organisieren von Datenbeständen im Abfrage-Service](./best-practices/organize-data-assets.md) lesen, gefolgt von der Dokumentation [Tabelle aus Auswahl erstellen](./sql/syntax.md#create-table-as-select).

Das folgende Beispiel zeigt die Verwendung einer CTAS-Syntax und eines „struct“-Datentyps:

```sql
CREATE TABLE table_name WITH (SCHEMA='schema_name')

AS SELECT '1' as _id,

 STRUCT

  ('2021-02-17T15:39:29.0Z' AS taskActualCompletionDate,

    '2020-09-09T21:21:16.0Z' AS taskActualStartDate,

    'Consulting' AS taskdescription,

    '5f6527c10011e09b89666c52d9a8c564' AS taskguide,

    'Stakeholder Consulting Engagement' AS taskname, 

    '2020-09-09T15:00:00.0Z' AS taskPlannedStartDate,

    '2021-02-15T11:00:00.0Z' AS taskPlannedCompletionDate

  ) AS _workfront ;
```

+++

### Wie kann ich die neuen Daten, die täglich in das System gelangen, schnell verarbeiten?

+++Antwort 
Die [`SNAPSHOT`](./sql/syntax.md#snapshot-clause)-Klausel kann verwendet werden, um Daten einer Tabelle basierend auf einer Schnappschuss-ID inkrementell zu lesen. Dies eignet sich ideal für die Verwendung mit dem Design-Muster für [inkrementelles Laden](./key-concepts/incremental-load.md), bei dem nur Informationen im Datensatz verarbeitet werden, die seit der letzten Ausführung des Ladevorgangs erstellt oder geändert wurden. Dadurch hat es eine höhere Verarbeitungseffizienz und kann sowohl bei der Streaming- als auch bei der Batch-Datenverarbeitung verwendet werden.
+++

### Warum unterscheiden sich die in der Profil-Benutzeroberfläche angezeigten Zahlen von den aus dem Profil-Exportdatensatz berechneten Zahlen?

+++Antwort
Die im Profil-Dashboard angezeigten Zahlen entsprechen dem Stand des letzten Schnappschusses. Die in der Tabelle für den Profilexport generierten Zahlen hängen vollständig von der Exportabfrage ab. Daher ist die Abfrage der Anzahl der Profile, die für eine bestimmte Zielgruppe qualifiziert sind, häufig eine Ursache für diese Diskrepanz.

>[!NOTE]
>
>Die Abfrage umfasst historische Daten, während in der Benutzeroberfläche nur die aktuellen Profildaten angezeigt werden.

+++

### Warum hat meine Abfrage eine leere Teilmenge zurückgegeben, und was soll ich tun?

+++Antwort
Die wahrscheinlichste Ursache ist, dass Ihre Abfrage im Umfang zu eng gefasst ist. Sie sollten systematisch je einen Abschnitt der `WHERE`-Klausel entfernen, bis Sie erste Daten sehen.

Sie können auch mithilfe einer kleinen Abfrage bestätigen, dass Ihr Datensatz Daten enthält, z. B.:

```sql
SELECT count(1) FROM myTableName
```

+++

### Kann ich meine Daten stichprobenweise überprüfen?

+++Antwort
An dieser Funktion wird derzeit gearbeitet. Details werden in den [Versionshinweisen](../release-notes/latest/latest.md) und über die Dialogfelder der Experience Platform-Benutzeroberfläche bekannt gegeben, sobald die Funktion zur Veröffentlichung bereit ist.
+++

### Welche Helferfunktionen werden vom Abfrage-Service unterstützt?

+++Antwort
Der Abfrage-Service bietet mehrere integrierte SQL-Helferfunktionen zur Erweiterung der SQL-Funktionalität. Im Dokument finden Sie eine vollständige Liste der [vom Abfrage-Service unterstützten SQL-Funktionen](./sql/spark-sql-functions.md).
+++

### Werden alle nativen [!DNL Spark SQL]-Funktionen unterstützt oder sind die Benutzenden nur auf die von Adobe bereitgestellten [!DNL Spark SQL]-Wrapper-Funktionen beschränkt?

+++Antwort
Bisher wurden noch nicht alle Open-Source-[!DNL Spark SQL]-Funktionen an Data Lake-Daten getestet. Sobald sie getestet und bestätigt sind, werden sie in die Liste der unterstützten Funktionen aufgenommen. Bitte sehen Sie in der [Liste der unterstützten  [!DNL Spark SQL] -Funktionen](./sql/spark-sql-functions.md) nach, um eine bestimmte Funktion zu finden.
+++

### Können Benutzende ihre eigenen benutzerdefinierten Funktionen (UDF) definieren, die über andere Abfragen hinweg verwendet werden können?

+++Antwort
Aus Gründen der Datensicherheit ist die benutzerdefinierte Definition von UDFs nicht zulässig.
+++

### Was sollte ich tun, wenn meine geplante Abfrage fehlschlägt?

+++Antwort
Zunächst überprüfen Sie die Protokolle, um die Details des Fehlers zu ermitteln. Der FAQ-Abschnitt zum [Suchen von Fehlern in Protokollen](#error-logs) enthält weitere Informationen dazu.

Sie sollten auch in der Dokumentation nachlesen, wie Sie [geplante Abfragen in der Benutzeroberfläche](./ui/user-guide.md#scheduled-queries) und über [die API](./api/scheduled-queries.md) durchführen können.

Beachten Sie, dass Sie bei Verwendung der [!DNL Query Editor] nur einen Zeitplan zu einer Abfrage hinzufügen können, die bereits erstellt und gespeichert wurde. Dies gilt nicht für die [!DNL Query Service]-API.
+++

### Was bedeutet die Fehlermeldung „Sitzungs-Limit erreicht“?

+++Antwort
„Sitzungs-Limit erreicht“ bedeutet, dass die für Ihr Organisation maximal zulässige Anzahl von Sitzungen des Abfrage-Service erreicht wurde. Wenden Sie sich an den Adobe Experience Platform-Administrator Ihrer Organisation.
+++

### Wie behandelt das Abfrageprotokoll Abfragen, die sich auf einen gelöschten Datensatz beziehen?

+++Antwort
Der Abfrage-Service löscht den Abfrageverlauf nie. Das bedeutet, dass alle Abfragen, die auf einen gelöschten Datensatz verweisen, als Ergebnis „Kein gültiger Datensatz“ zurückgeben.
+++

### Wie erhalte ich nur die Metadaten für eine Abfrage?

+++Antwort
Sie können eine Abfrage ausführen, die null Zeilen zurückgibt, um nur die Metadaten in der Antwort zu erhalten. Diese Beispielabfrage gibt nur die Metadaten für die angegebene Tabelle zurück.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### Wie kann ich eine CTAS-Abfrage (Tabelle aus Auswahl erstellen) schnell durchlaufen, ohne sie zu materialisieren?

+++Antwort
Sie können temporäre Tabellen erstellen, um eine Abfrage schnell zu iterieren und zu experimentieren, bevor sie zur Verwendung materialisiert wird. Sie können auch temporäre Tabellen verwenden, um zu überprüfen, ob eine Abfrage funktioniert.

Sie können zum Beispiel eine temporäre Tabelle erstellen:

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

Anschließend können Sie die temporäre Tabelle wie folgt verwenden:

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

+++

### Wie ändere ich die Zeitzone von und zu einem UTC-Zeitstempel?

+++Antwort
Adobe Experience Platform behält Daten im UTC-Zeitstempelformat (Coordinated Universal Time) bei. Ein Beispiel für das UTC-Format ist `2021-12-22T19:52:05Z`

Der Abfrage-Service unterstützt integrierte SQL-Funktionen zum Konvertieren eines bestimmten Zeitstempels in das und aus dem UTC-Format. Sowohl die Methode `to_utc_timestamp()` als auch `from_utc_timestamp()` benötigt zwei Parameter: Zeitstempel und Zeitzone.

| Parameter | Beschreibung |
|-----------|---------------|
| Zeitstempel | Der Zeitstempel kann entweder im UTC-Format oder im einfachen `{year-month-day}`-Format geschrieben werden. Wenn keine Uhrzeit angegeben wird, ist der Standardwert Mitternacht am Morgen des angegebenen Tages. |
| Zeitzone | Die Zeitzone wird im Format `{continent/city})` angegeben. Es muss einer der anerkannten Zeitzonen-Codes sein, die in der [öffentlich zugänglichen TZ-Datenbank](https://data.iana.org/time-zones/tz-link.html#tzdb) zu finden sind. |

#### Konvertieren in den UTC-Zeitstempel

Die Methode `to_utc_timestamp()` interpretiert die angegebenen Parameter und konvertiert sie **in den Zeitstempel Ihrer lokalen Zeitzone** im UTC-Format. Beispielsweise ist die Zeitzone in Seoul, Südkorea UTC/GMT +9 Stunden. Bei Angabe eines Zeitstempels, der nur das Datum enthält, verwendet die Methode den Standardwert Mitternacht am Morgen. Der Zeitstempel und die Zeitzone werden vom Zeitpunkt dieser Region in einen UTC-Zeitstempel Ihrer lokalen Region im UTC-Format konvertiert.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

Die Abfrage gibt einen Zeitstempel in der Ortszeit der Benutzenden zurück. In diesem Fall 15 Uhr am Vortag, da Seoul neun Stunden voraus ist.

```
2021-08-30 15:00:00
```

Ein weiteres Beispiel: Wenn der angegebene Zeitstempel `2021-07-14 12:40:00.0` für die Zeitzone `Asia/Seoul` lautet, wäre der zurückgegebene UTC-Zeitstempel `2021-07-14 03:40:00.0`

Die Konsolenausgabe in der Benutzeroberfläche des Abfrage-Service ist ein besser lesbares Format:

```
8/30/2021, 3:00 PM
```

#### Konvertieren aus dem UTC-Zeitstempel

Die Methode `from_utc_timestamp()` interpretiert die angegebenen Parameter **aus dem Zeitstempel Ihrer lokalen Zeitzone** und liefert den entsprechenden Zeitstempel der gewünschten Region im UTC-Format. Im folgenden Beispiel ist die Stunde 2:40PM in der lokalen Zeitzone des Benutzers. Die als Variable übergebene Zeitzone Seoul ist der lokalen Zeitzone neun Stunden voraus.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

Die Abfrage gibt einen Zeitstempel im UTC-Format für die Zeitzone zurück, die als Parameter übergeben wird. Das Ergebnis liegt neun Stunden vor der Zeitzone, die die Abfrage ausgeführt hat.

```
8/31/2021, 11:40 PM
```

### Wie sollte ich meine Zeitreihendaten filtern?

+++Antwort
Bei Abfragen mit Zeitreihendaten sollten Sie den Zeitstempelfilter verwenden, wann immer dies möglich ist, um eine genauere Analyse zu ermöglichen.

>[!NOTE]
>
> Die Datums-Zeichenfolge **muss** im Format `yyyy-mm-ddTHH24:MM:SS` sein.

Nachfolgend finden Sie ein Beispiel für die Verwendung des Zeitstempelfilters:

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### Wie verwende ich den `CAST`-Operator richtig, um meine Zeitstempel in SQL-Abfragen zu konvertieren?

+++Antwort
Wenn Sie den `CAST`-Operator verwenden, um einen Zeitstempel zu konvertieren, müssen Sie **sowohl** das Datum als auch die Uhrzeit angeben.

Fehlt zum Beispiel die Zeitkomponente, wie unten gezeigt, führt dies zu einem Fehler:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Die korrekte Verwendung des `CAST`-Operators finden Sie unten:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### Sollte ich Platzhalter verwenden, z. B. *, um alle Zeilen aus meinen Datensätzen zu erhalten?

+++Antwort
Sie können keine Platzhalter verwenden, um alle Daten aus Ihren Zeilen abzurufen, da der Abfrage-Service als **Spalten-Speicher** und nicht als traditionelles zeilenbasiertes Speichersystem behandelt werden sollte.
+++

### Sollte ich `NOT IN` in meiner SQL-Abfrage verwenden?

+++Antwort
Der `NOT IN`-Operator wird häufig zum Abrufen von Zeilen verwendet, die nicht in einer anderen Tabelle oder SQL-Anweisung gefunden werden. Dieser Operator kann die Performance verlangsamen und unerwartete Ergebnisse liefern, wenn die zu vergleichenden Spalten `NOT NULL` akzeptieren oder wenn Sie eine große Anzahl von Datensätzen haben.

Anstatt `NOT IN` zu verwenden, können Sie entweder `NOT EXISTS` oder `LEFT OUTER JOIN` verwenden.

Wenn Sie zum Beispiel die folgenden Tabellen erstellt haben:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Wenn Sie den `NOT EXISTS`-Operator verwenden, können Sie den `NOT IN`-Operator replizieren, indem Sie die folgende Abfrage verwenden:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Wenn Sie den `LEFT OUTER JOIN`-Operator verwenden, können Sie alternativ mit dem `NOT IN`-Operator replizieren, indem Sie die folgende Abfrage verwenden:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### Kann ich einen Datensatz mithilfe einer CTAS-Abfrage mit einem Namen mit doppeltem Unterstrich erstellen, wie er in der Benutzeroberfläche angezeigt wird? Beispiel: `test_table_001`.

+++Antwort
Nein, dies ist eine absichtliche Einschränkung in der gesamten Experience Platform, die für alle Adobe-Services gilt, einschließlich Abfrage-Service. Ein Name mit zwei Unterstrichen ist als Schema- und Datensatzname zulässig, aber der Tabellenname für den Datensatz darf nur einen einzigen Unterstrich enthalten.
+++

### Wie viele gleichzeitige Abfragen können parallel ausgeführt werden?

+++Antwort
Es gibt keine Begrenzung der Gleichzeitigkeit von Abfragen, da Batch-Abfragen als Backend-Aufträge ausgeführt werden. Es gibt jedoch ein Zeitlimit für Abfragen, das auf 24 Stunden festgelegt ist.
+++

### Gibt es ein Aktivitäts-Dashboard, in dem Abfrageaktivitäten und -status zu sehen sind?

+++Antwort
Es gibt Monitoring- und Warnfunktionen, mit denen Sie sich über Abfrageaktivitäten und -status informieren können. Weitere Informationen finden Sie in den Dokumenten zur [Auditprotokollintegration für den Abfrage-Service](./data-governance/audit-log-guide.md) und zu [Abfrageprotokollen](./ui/overview.md#log).
+++

### Gibt es eine Möglichkeit, Aktualisierungen zurückzusetzen? Wenn beispielsweise ein Fehler auftritt oder einige Berechnungen beim Zurückschreiben von Daten in Experience Platform neu konfiguriert werden müssen, wie sollte dieses Szenario gehandhabt werden?

+++Antwort
Derzeit unterstützen wir keine Zurücksetzungen oder Aktualisierungen auf diese Weise.
+++

### Wie können Abfragen in Adobe Experience Platform optimiert werden?

+++Antwort
Das System hat keine Indizes, da es keine Datenbank ist, aber es sind andere Optimierungen im Zusammenhang mit dem Datenspeicher vorhanden. Die folgenden Optionen stehen zur Abstimmung Ihrer Abfragen zur Verfügung:

- Ein zeitbasierter Filter für Zeitreihendaten.
- Optimierter Push-Down für den „struct“-Datentyp.
- Optimierter Push-Down von Kosten und Arbeitsspeicher für Arrays und Map-Datentypen.
- Inkrementelle Verarbeitung mit Schnappschüssen.
- Ein beibehaltenes Datenformat.
+++

### Können Anmeldungen auf bestimmte Aspekte vom Abfrage-Service beschränkt werden oder ist dies eine „Alles-oder-Nichts“-Lösung?

+++Antwort
Der Abfrage-Service ist eine „Alles-oder-Nichts“-Lösung. Es kann kein Teilzugriff gewährt werden.
+++

### Kann ich einschränken, welche Daten der Abfrage-Service nutzen kann, oder greift er einfach auf den gesamten Adobe Experience Platform Data Lake zu?

+++Antwort
Ja, Sie können die Abfrage auf Datensätze mit schreibgeschütztem Zugriff beschränken.
+++

### Welche anderen Optionen gibt es zum Einschränken der Daten, auf die der Abfrage-Service zugreifen kann?

+++Antwort
Es gibt drei Möglichkeiten, den Zugriff zu beschränken. Diese sind wie folgt:

- Verwenden Sie nur SELECT-Anweisungen und geben Sie Datensätzen nur Lesezugriff. Weisen Sie außerdem die Berechtigung zum Verwalten von Abfragen zu.
- Verwenden Sie SELECT/INSERT/CREATE-Anweisungen und geben Sie Datensätzen Schreibzugriff. Weisen Sie außerdem die Berechtigung zur Verwaltung von Abfragen zu.
- Verwenden Sie ein Integrationskonto mit den oben genannten Vorschlägen und weisen Sie die Berechtigung für die Abfrageintegration zu.

+++

### Gibt es nach Rückgabe der Daten durch den Abfrage-Service irgendwelche Prüfungen, die von Experience Platform ausgeführt werden können, um sicherzustellen, dass keine geschützten Daten zurückgegeben wurden?

- Der Abfrage-Service unterstützt eine attributbasierte Zugriffssteuerung. Sie können den Zugriff auf Daten auf die Spalten-/Blattebene und/oder die Strukturebene einschränken. Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie in der Dokumentation.

### Kann ich einen SSL-Modus für die Verbindung zu einem Drittanbieter-Client angeben? Kann ich beispielsweise „verify-full“ mit Power BI verwenden?

+++Antwort
Ja, SSL-Modi werden unterstützt. Siehe [Dokumentation zu SSL-Modi](./clients/ssl-modes.md) für eine Aufschlüsselung der verschiedenen verfügbaren SSL-Modi und des Schutzniveaus, das sie bieten.
+++

### Wird TLS 1.2 für alle Verbindungen von Power BI-Clients zum Abfrage-Service verwendet?

+++Antwort
Ja. Daten in Bewegung sind immer HTTPS-konform. Die derzeit unterstützte Version ist TLS1.2.
+++

### Wird bei einer Verbindung über Port 80 immer noch https verwendet?

+++Antwort
Ja, eine über Port 80 hergestellte Verbindung verwendet immer noch SSL. Sie können auch Port 5432 verwenden.
+++

### Kann ich den Zugriff auf bestimmte Datensätze und Spalten für eine bestimmte Verbindung steuern? Wie ist dies konfiguriert?

+++Antwort 
Ja, die attributbasierte Zugriffssteuerung wird erzwungen, wenn sie konfiguriert ist. Weitere Informationen finden Sie in der [Übersicht über die attributbasierte Zugriffssteuerung](../access-control/abac/overview.md).
+++

### Unterstützt Query Service den Befehl „INSERT OVERWRITE INTO“?

+++Antwort 
Nein, Query Service unterstützt den Befehl „INSERT OVERWRITE INTO“ nicht.
+++

### Wie oft werden die Nutzungsdaten im Lizenznutzungs-Dashboard für Data Distiller Compute Hours aktualisiert?

+++Antwort
Das Lizenznutzungs-Dashboard für Data Distiller-Computerstunden wird viermal täglich alle sechs Stunden aktualisiert.
+++

### Kann ich den Befehl „CREATE VIEW“ ohne Zugriff auf Data Distiller verwenden?

+++Antwort
Ja, Sie können `CREATE VIEW` Befehl ohne Zugriff auf Data Distiller verwenden. Dieser Befehl bietet eine logische Ansicht von Daten, schreibt sie jedoch nicht zurück in den Data Lake.
+++

### Kann ich anonyme Blöcke in DbVisualizer verwenden?

+++Antwort
Ja. Bestimmte Drittanbieter-Clients wie DbVisualizer benötigen jedoch möglicherweise eine separate Kennung vor und nach einem SQL-Block, um anzugeben, dass ein Teil eines Skripts als einzelne Anweisung gehandhabt werden soll. Weitere Informationen finden Sie in der [Dokumentation zu anonymen Blöcken](./key-concepts/anonymous-block.md) oder in [offiziellen DbVisualizer-Dokumentation](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsinganSQLDialect).
+++

## Data Distiller {#data-distiller}

### Wie wird die Lizenznutzung von Data Distiller verfolgt und wo kann ich diese Informationen sehen?

+++Antwort\
Die Hauptmetrik zur Verfolgung der Batch-Abfragenutzung ist „Compute Hour“. Sie haben über das Dashboard „Lizenznutzung[ Zugriff auf diese Informationen und ](../dashboards/guides/license-usage.md) aktuellen Verbrauch.
+++

### Was ist eine Compute Hour?

+++Antwort\
Berechnungsstunden sind die Zeit, die die Abfrage-Service-Engines zum Lesen, Verarbeiten und Zurückschreiben von Daten in den Data Lake benötigen, wenn eine Batch-Abfrage ausgeführt wird.
+++

### Wie werden Compute Hours gemessen?

+++Antwort\
Berechnungsstunden werden kumulativ für alle autorisierten Sandboxes gemessen.
+++

### Warum bemerke ich manchmal Schwankungen beim Verbrauch der Rechenstunden, selbst wenn ich dieselbe Abfrage nacheinander ausführe?

+++Antwort\
Die Berechnung der Stunden für eine Abfrage kann aufgrund mehrerer Faktoren schwanken. Dazu gehören das verarbeitete Datenvolumen, die Komplexität der Umwandlungsvorgänge innerhalb der SQL-Abfrage usw. Query Service skaliert den Cluster basierend auf den oben genannten Parametern für jede Abfrage, was zu Unterschieden bei den Rechenstunden führen kann.
+++

### Ist es normal, eine Verringerung der Compute Hours zu bemerken, wenn ich dieselbe Abfrage über einen langen Zeitraum mit denselben Daten ausführe? Warum kann das passieren?

+++Antwort\
Die Backend-Infrastruktur wird ständig verbessert, um die Auslastung und Verarbeitungszeit der Rechenstunden zu optimieren. Daher kann es vorkommen, dass sich die Leistung im Laufe der Zeit verbessert.
+++

### Unterscheidet sich die Leistung von Data Distiller zwischen Entwicklungs- und Produktions-Sandboxes?

+++Antwort
Sie können ähnliche Leistung erwarten, wenn Sie Abfragen sowohl in Entwicklungs- als auch in Produktions-Sandboxes ausführen. Beide Umgebungen sind so konzipiert, dass sie denselben Verarbeitungsgrad bieten. Je nach der Menge der verarbeiteten Daten und der gesamten Systemaktivität zum Zeitpunkt der Ausführung der Abfrage können jedoch Unterschiede in den Berechnungsstunden auftreten.

Verfolgen Sie die Nutzung Ihrer Compute Hour im [Lizenznutzungs-Dashboard](../dashboards/guides/license-usage.md) der Experience Platform-Benutzeroberfläche.
+++

## Benutzeroberfläche für Abfragen

### Die Meldung „Abfrage erstellen“ bleibt beim Versuch, eine Verbindung zum Abfrage-Service herzustellen, hängen „Verbindung wird initialisiert…“. Wie behebe ich das Problem?

+++Antwort
Wenn die Option „Abfrage erstellen“ bei „Verbindung wird initialisiert…“ hängt, handelt es sich wahrscheinlich um ein Verbindungs- oder Sitzungsproblem. Aktualisieren Sie den Browser, wenn Sie die Experience Platform-Benutzeroberfläche verwenden, und versuchen Sie es erneut.
+++

## Datensatzbeispiele

### Kann ich Beispiele für einen Systemdatensatz erstellen?

+++Antwort 
Nr. Schreibberechtigungen sind auf Systemdatensätze beschränkt, sodass keine Beispiele erstellt werden können.
+++

## Exportieren von Daten {#exporting-data}

Dieser Abschnitt enthält Informationen zum Exportieren von Daten und Einschränkungen.

### Gibt es eine Möglichkeit, Daten aus dem Abfrage-Service nach der Verarbeitung der Abfrage zu extrahieren und die Ergebnisse in einer CSV-Datei zu speichern? {#export-csv}

+++Antwort
Ja. Daten können aus dem Abfrage-Service extrahiert werden. Außerdem besteht die Möglichkeit, die Ergebnisse über einen SQL-Befehl im CSV-Format zu speichern.

Es gibt zwei Möglichkeiten, die Ergebnisse einer Abfrage bei der Verwendung eines PSQL-Clients zu speichern. Sie können den Befehl `COPY TO` verwenden oder eine Anweisung in folgendem Format erstellen:

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Hinweise zur Verwendung des Befehls `COPY TO` ](./sql/syntax.md#copy) finden Sie in der SQL-Syntaxreferenzdokumentation.
+++

### Kann ich den Inhalt des endgültigen Datensatzes, der durch CTAS-Abfragen aufgenommen wurde, extrahieren (unter der Annahme, es handelt sich um größere Datenmengen wie Terabytes)?

+++Antwort 
Nr. Es gibt derzeit keine Funktion für die Extraktion aufgenommener Daten.
+++

### Warum gibt der Analytics-Daten-Connector keine Daten zurück?

+++Antwort
Eine häufige Ursache für dieses Problem ist die Abfrage von Zeitreihendaten ohne Zeitfilter. Beispiel:

```sql
SELECT * FROM prod_table LIMIT 1;
```

Sollte wie folgt geschrieben werden:

```sql
SELECT * FROM prod_table
WHERE
timestamp >= to_timestamp('2022-07-22')
and timestamp < to_timestamp('2022-07-23');
```

+++

## SQL-Syntax

### Wird MERGE INTO von Data Distiller oder Query Service unterstützt?

+++Antwort
Das MERGE INTO SQL-Konstrukt wird von Data Distiller oder Query Service nicht unterstützt.
+++

## ITAS-Abfragen {#itas-queries}

### Was sind ITAS-Abfragen?

+++Antwort
INSERT INTO-Abfragen werden als ITAS-Abfragen bezeichnet. Beachten Sie, dass CREATE TABLE-Abfragen als CTAS-Abfragen bezeichnet werden.
+++

### Unterstützt Query Service Aktualisierungs- und Löschvorgänge?

+++Antwort
Nein, der Abfrage-Service unterstützt keine Aktualisierungs- oder Löschvorgänge. Es werden nur reine Append-Vorgänge mit ITAS unterstützt.
+++

## Drittanbieter-Tools {#third-party-tools}

Dieser Abschnitt enthält Informationen zur Verwendung von Drittanbieter-Tools wie PSQL und Power BI.

### Kann ich den Abfrage-Service mit einem Tool eines Drittanbieters verbinden?

+++Antwort
Ja, Sie können mehrere Desktop-Clients von Drittanbietern mit dem Abfrage-Service verbinden. In der Dokumentation finden Sie [ausführliche Informationen über die verfügbaren Clients und darüber, wie Sie sie mit dem Abfrage-Service verbinden](./clients/overview.md).
+++

### Gibt es eine Möglichkeit, den Abfrage-Service einmal für die kontinuierliche Verwendung mit einem Tool eines Drittanbieters zu verbinden?

+++Antwort
Ja, Desktop-Clients von Drittanbietern können über eine einmalige Einrichtung ohne ablaufende Anmeldedaten mit dem Abfrage-Service verbunden werden. Nicht ablaufende Anmeldedaten können von einem autorisierten Benutzer generiert und in einer JSON-Datei empfangen werden, die automatisch auf den lokalen Computer heruntergeladen wird. Eine vollständige [Anleitung zum Erstellen und Herunterladen von nicht ablaufenden Anmeldedaten](./ui/credentials.md#non-expiring-credentials) finden Sie in der Dokumentation.
+++

### Warum funktionieren meine nicht ablaufenden Anmeldedaten nicht?

+++Antwort
Der Wert für nicht ablaufende Anmeldedaten sind die verketteten Argumente aus der `technicalAccountID` und dem `credential` aus der JSON-Konfigurationsdatei. Der Kennwortwert hat folgende Form: `{{technicalAccountId}:{credential}}`.
In der Dokumentation finden Sie weitere Informationen zur [Verbindung mit externen Clients mit Anmeldedaten](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### Gibt es Einschränkungen für Sonderzeichen für nicht ablaufende Zugangsdaten und Kennwörter?

+++Antwort
Ja. Wenn Sie ein Kennwort für nicht ablaufende Anmeldeinformationen festlegen, müssen Sie mindestens eine Zahl, einen Kleinbuchstaben, einen Großbuchstaben und ein Sonderzeichen angeben. Das Dollarzeichen ($) wird nicht unterstützt. Verwenden Sie stattdessen Sonderzeichen wie !, @, #, ^ oder &amp;.
+++

### Welche Art von SQL-Editoren von Drittanbietern kann ich mit dem Abfrage-Service-Editor verbinden?

+++Antwort
Alle SQL-Editoren von Drittanbietern, die PSQL oder [!DNL Postgres] Client-kompatibel sind, können mit dem Abfrage-Service-Editor verbunden werden. In der Dokumentation zum [Verbinden von Clients mit dem Abfrage-Service](./clients/overview.md) finden Sie eine Liste der verfügbaren Anweisungen.
+++

### Kann ich das Power BI-Tool mit dem Abfrage-Service verbinden?

+++Antwort
Ja, Sie können Power BI mit dem Abfrage-Service verbinden. In der Dokumentation finden Sie [Anweisungen zum Verbinden der Power BI Desktop-Anwendung mit dem Abfrage-Service](./clients/power-bi.md).
+++

### Warum dauert das Laden der Dashboards bei der Verbindung mit dem Abfrage-Service so lange?

+++Antwort
Wenn das System mit dem Abfrage-Service verbunden ist, ist es mit einer interaktiven oder Batch-Verarbeitungs-Engine verbunden. Dies kann zu längeren Ladezeiten führen, um die verarbeiteten Daten widerzuspiegeln.

Wenn Sie die Antwortzeiten für Ihre Dashboards verbessern möchten, sollten Sie einen Business Intelligence-Server (BI) als Caching-Ebene zwischen dem Abfrage-Service und den BI-Tools implementieren. Im Allgemeinen bieten die meisten BI-Tools ein zusätzliches Angebot für einen Server.

Durch Hinzufügen der Cache-Server-Ebene werden die Daten aus dem Abfrage-Service zwischengespeichert, wodurch Dashboards die Antwort beschleunigen können. Dies ist möglich, da die Ergebnisse für ausgeführte Abfragen jeden Tag auf dem BI-Server zwischengespeichert werden. Der Caching-Server stellt diese Ergebnisse dann für jeden Benutzer mit derselben Abfrage bereit, um die Latenz zu verringern. Weitere Informationen zu dieser Einrichtung finden Sie in der Dokumentation des Dienstprogramms oder des Drittanbieter-Tools, das Sie verwenden.
+++

### Ist der Zugriff auf den Abfrage-Service über das pgAdmin-Verbindungs-Tool möglich?

+++Antwort
Nein, pgAdmin-Konnektivität wird nicht unterstützt. Eine [Liste der verfügbaren Drittanbieter-Clients und eine Anleitung, wie Sie diese mit dem Abfrage-Service](./clients/overview.md) verbinden können, finden Sie in der Dokumentation.
+++

## PostgreSQL-API-Fehler {#postgresql-api-errors}

Die folgende Tabelle enthält PSQL-Fehler-Codes und die möglichen Ursachen.

| Fehler-Code | Verbindungsstatus | Beschreibung | Mögliche Ursache |
|------------|---------------------------|-------------|----------------|
| **08P01** | K. A. | Nicht unterstützter Nachrichtentyp | Nicht unterstützter Nachrichtentyp |
| **28P01** | Start-up – Authentifizierung | Ungültiges Kennwort | Ungültiges Authentifizierungs-Token |
| **28000** | Start-up – Authentifizierung | Ungültiger Autorisierungstyp | Ungültiger Autorisierungstyp. Muss `AuthenticationCleartextPassword`sein. |
| **42P12** | Start-up – Authentifizierung | Keine Tabellen gefunden | Keine Tabellen zur Verwendung gefunden |
| **42601** | Abfrage | Syntaxfehler | Ungültiger Befehl- oder Syntaxfehler |
| **42P01** | Abfrage | Tabelle nicht gefunden | Die in der Abfrage angegebene Tabelle wurde nicht gefunden |
| **42P07** | Abfrage | Tabelle vorhanden | Eine Tabelle mit demselben Namen ist bereits vorhanden (TABELLE ERSTELLEN) |
| **53400** | Abfrage | LIMIT überschreitet den Maximalwert | Benutzer hat eine LIMIT-Klausel über 100.000 angegeben |
| **53400** | Abfrage | Anweisungs-Timeout | Die abgesendete Live-Anweisung dauerte mehr als 10 Minuten |
| **58000** | Abfrage | Systemfehler | Interner Systemfehler |
| **0A000** | Abfrage/Befehl | Nicht unterstützt | Die Funktion/Funktionalität in der Abfrage/dem Befehl wird nicht unterstützt |
| **42501** | TABELLE LÖSCHEN Abfrage | Tabelle löschen, die nicht vom Abfrage-Service erstellt wurde | Die Tabelle, die gelöscht werden soll, wurde nicht vom Abfrage-Service mit der Anweisung `CREATE TABLE` erstellt |
| **42501** | TABELLE LÖSCHEN Abfrage | Tabelle nicht vom authentifizierten Benutzer erstellt | Die Tabelle, die gelöscht werden soll, wurde nicht von dem aktuell angemeldeten Benutzer erstellt |
| **42P01** | TABELLE LÖSCHEN Abfrage | Tabelle nicht gefunden | Die in der Abfrage angegebene Tabelle wurde nicht gefunden |
| **42P12** | TABELLE LÖSCHEN Abfrage | Keine Tabelle für `dbName` gefunden: Bitte überprüfen Sie `dbName` | In der aktuellen Datenbank wurden keine Tabellen gefunden |

### Warum habe ich einen Fehlercode 58000 erhalten, als ich die Methode history_meta() für meine Tabelle verwendet habe?

+++Antwort
Die Methode `history_meta()` wird verwendet, um auf einen Schnappschuss eines Datensatzes zuzugreifen. Wenn Sie früher eine Abfrage über einen leeren Datensatz in Azure Data Lake Storage (ADLS) durchgeführt haben, erhielten Sie einen 58000-Fehler-Code, der besagte, dass der Datensatz nicht existiert. Nachfolgend finden Sie ein Beispiel für den alten Systemfehler.

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

Dieser Fehler war aufgetreten, weil für die Abfrage kein Rückgabewert vorhanden war. Dieses Verhalten wurde jetzt korrigiert und gibt nun die folgende Meldung zurück:

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## REST-API-Fehler {#rest-api-errors}

Die folgende Tabelle enthält HTTP-Fehler-Codes und die möglichen Ursachen.

| HTTP-Status-Code | Beschreibung | Mögliche Ursachen |
|------------------|-----------------------|----------------------------|
| 400 | Ungültige Anfrage | Falsch formulierte oder illegale Abfrage |
| 401 | Authentifizierung fehlgeschlagen | Ungültiges Authentifizierungs-Token |
| 500 | Interner Server-Fehler | Interner Systemfehler |
