---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; Handbuch zur Fehlerbehebung; FAQ; Fehlerbehebung
solution: Experience Platform
title: Anleitung zur Fehlerbehebung bei Query Service
topic-legacy: troubleshooting
description: Dieses Dokument enthält häufig gestellte Fragen und Antworten zu Query Service. Zu den Themen gehören der Datenexport, Tools von Drittanbietern und PSQL-Fehler.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: deb9f314d5eaadebe2f3866340629bad5f39c60d
workflow-type: tm+mt
source-wordcount: '4362'
ht-degree: 3%

---

# [!DNL Query Service] Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Query Service und eine Liste der häufig verwendeten Fehlercodes bei Verwendung von Query Service. Fragen und Antworten zur Fehlerbehebung bei anderen Diensten in Adobe Experience Platform finden Sie im Abschnitt [Handbuch zur Fehlerbehebung bei Experience Platformen](../landing/troubleshooting.md).

Die folgende Liste von Antworten auf häufig gestellte Fragen ist in folgende Kategorien unterteilt:

- [Allgemein](#general)
- [Exportieren von Daten](#exporting-data)
- [Drittanbieter-Tools](#third-party-tools)
- [PostgreSQL-API-Fehler](#postgresql-api-errors)
- [REST-API-Fehler](#rest-api-errors)

## Allgemeine Fragen zu Query Service {#general}

Dieser Abschnitt enthält Informationen zu Leistung, Beschränkungen und Prozessen.

### Kann ich die Funktion zur automatischen Vervollständigung im Abfragedienst-Editor deaktivieren?

+++Antwort Nr. Das Deaktivieren der Funktion zur automatischen Vervollständigung wird derzeit vom Editor nicht unterstützt.
+++

### Warum wird der Abfrage-Editor manchmal langsam, wenn ich eine Abfrage eingebe?

+++Antwort Eine potenzielle Ursache ist die Funktion zur automatischen Vervollständigung. Die Funktion verarbeitet bestimmte Metadatenbefehle, die den Editor gelegentlich bei der Abfragebearbeitung verlangsamen können.
+++

### Kann ich [!DNL Postman] für die Query Service-API?

++ + Antwort Ja: Sie können alle Adobe-API-Dienste mithilfe von visualisieren und mit ihnen interagieren. [!DNL Postman] (kostenlose Drittanbieteranwendung). Beobachten Sie die [[!DNL Postman] Setup-Handbuch](https://video.tv.adobe.com/v/28832) Schrittweise Anleitungen zum Einrichten eines Projekts in der Adobe Developer Console und zum Abrufen aller erforderlichen Anmeldeinformationen für die Verwendung mit [!DNL Postman]. Die offizielle Dokumentation finden Sie unter [Anleitung zum Starten, Ausführen und Freigeben [!DNL Postman] Sammlungen](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### Gibt es eine Begrenzung für die maximale Anzahl von Zeilen, die von einer Abfrage über die Benutzeroberfläche zurückgegeben werden?

++ + Antwort Ja, Query Service wendet intern eine Beschränkung von 50.000 Zeilen an, es sei denn, extern wird eine explizite Begrenzung angegeben. Siehe die Leitlinien zu [interaktive Abfrageausführung](./best-practices/writing-queries.md#interactive-query-execution) für weitere Details.
+++

### Kann ich Abfragen verwenden, um Zeilen zu aktualisieren?

+++Antwort In Batch-Abfragen wird das Aktualisieren einer Zeile im Datensatz nicht unterstützt.
+++

### Gibt es eine Größenbeschränkung für die resultierende Ausgabe aus einer Abfrage?

+++Antwort Nr. Die Datengröße ist nicht begrenzt, aber eine interaktive Sitzung hat eine Zeitüberschreitung der Abfrage von 10 Minuten. Wenn die Abfrage als Batch-CTAS ausgeführt wird, gilt kein 10-minütiges Timeout. Siehe die Leitlinien zu [interaktive Abfrageausführung](./best-practices/writing-queries.md#interactive-query-execution) für weitere Details.
+++

### Wie umgehe ich die Begrenzung der Ausgabenanzahl von Zeilen aus einer SELECT-Abfrage?

+++Antwort Wenden Sie &quot;LIMIT 0&quot;in der Abfrage an, um die Beschränkung für die Ausgabezeilen zu umgehen. Beispiel:

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### Wie kann ich verhindern, dass meine Abfragen in 10 Minuten ablaufen?

+++ Antwort Eine oder mehrere der folgenden Lösungen werden empfohlen, wenn bei Abfragen eine Zeitüberschreitung auftritt.

- [Konvertieren der Abfrage in eine CTAS-Abfrage](./sql/syntax.md#create-table-as-select) und die Ausführung planen. Die Planung einer Ausführung kann entweder [über die Benutzeroberfläche](./ui/user-guide.md#scheduled-queries) oder [API](./api/scheduled-queries.md#create).
- Führen Sie die Abfrage in einem kleineren Datenblock aus, indem Sie zusätzliche [Filterbedingungen](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [Ausführen des Befehls &quot;EXPLAIN&quot;](./sql/syntax.md#explain) , um weitere Details zu sammeln.
- Überprüfen Sie die Statistiken der Daten im Datensatz.
- Konvertieren Sie die Abfrage in ein vereinfachtes Formular und führen Sie sie erneut mit [vorbereitete Anweisungen](./sql/prepared-statements.md).
+++

### Gibt es Probleme oder Auswirkungen auf die Leistung von Query Service, wenn mehrere Abfragen gleichzeitig ausgeführt werden?

+++Antwort Nr. Query Service verfügt über eine Funktion zur automatischen Skalierung, die sicherstellt, dass gleichzeitige Abfragen keine merklichen Auswirkungen auf die Leistung des Dienstes haben.
+++

### Kann ich reservierte Schlüsselwörter als Spaltennamen verwenden?

+++Antwort Es gibt bestimmte reservierte Schlüsselwörter, die nicht als Spaltenname verwendet werden können, z. B.: `ORDER`, `GROUP BY`, `WHERE`, `DISTINCT`. Wenn Sie diese Suchbegriffe verwenden möchten, müssen Sie diese Spalten maskieren.
+++

### Wie finde ich einen Spaltennamen aus einem hierarchischen Datensatz?

+++Antwort Die folgenden Schritte beschreiben, wie Sie eine tabellarische Ansicht eines Datensatzes über die Benutzeroberfläche anzeigen, einschließlich aller verschachtelten Felder und Spalten in einem reduzierten Formular.

- Wählen Sie nach der Anmeldung bei Experience Platform die Option **[!UICONTROL Datensätze]** im linken Navigationsbereich der Benutzeroberfläche, um zu navigieren [!UICONTROL Datensätze] Dashboard.
- Die Datensätze [!UICONTROL Durchsuchen] -Registerkarte geöffnet. Sie können die Suchleiste verwenden, um die verfügbaren Optionen zu verfeinern. Wählen Sie einen Datensatz aus der angezeigten Liste aus.

![Das Dashboard &quot;Datensätze&quot;in der Platform-Benutzeroberfläche mit hervorgehobener Suchleiste und Datensatz.](./images/troubleshooting/dataset-selection.png)

- Die [!UICONTROL Datensatzaktivität] angezeigt. Auswählen **[!UICONTROL Vorschau des Datensatzes anzeigen]** , um ein Dialogfeld des XDM-Schemas und eine tabellarische Ansicht von reduzierten Daten aus dem ausgewählten Datensatz zu öffnen. Weitere Informationen finden Sie im [Vorschau einer Datensatzdokumentation anzeigen](../catalog/datasets/user-guide.md#preview-a-dataset)

![Die Registerkarte Datensatzaktivität im Dashboard &quot;Datensätze&quot;mit hervorgehobener Vorschau des Datensatzes.](./images/troubleshooting/dataset-preview.png)

- Wählen Sie ein beliebiges Feld aus dem Schema aus, um seinen Inhalt in einer reduzierten Spalte anzuzeigen. Der Name der Spalte wird oberhalb ihres Inhalts auf der rechten Seite angezeigt. Sie sollten diesen Namen kopieren, um diesen Datensatz abzufragen.

![Das XDM-Schema und die Tabellenansicht der reduzierten Daten. Der Spaltenname eines verschachtelten Datensatzes wird in der Benutzeroberfläche hervorgehoben.](./images/troubleshooting/column-name.png)

Die vollständige Anleitung finden Sie in der Dokumentation zu [Arbeiten mit verschachtelten Datenstrukturen](./best-practices/nested-data-structures.md) mit dem Abfrage-Editor oder einem Client eines Drittanbieters.
+++

### Wie beschleunige ich eine Abfrage für einen Datensatz, der Arrays enthält?

+++Antwort Um die Leistung von Abfragen für Datensätze zu verbessern, die Arrays enthalten, sollten Sie [explodieren](https://spark.apache.org/docs/latest/api/sql/index.html#explode) as a [CTAS-Abfrage](./sql/syntax.md#create-table-as-select) auf Laufzeitumgebung, und untersuchen Sie sie dann, um weitere Möglichkeiten zur Verbesserung der Verarbeitungszeit zu erhalten.
+++

### Warum wird meine CTAS-Abfrage nach vielen Stunden nur für eine kleine Anzahl von Zeilen verarbeitet?

+++Antwort Wenn die Abfrage für einen sehr kleinen Datensatz lange gedauert hat, wenden Sie sich an den Support.

Es kann verschiedene Gründe dafür geben, dass eine Abfrage bei der Verarbeitung hängenbleibt. Um die genaue Ursache zu ermitteln, muss von Fall zu Fall eingehend analysiert werden. [Support für Adobe kontaktieren](#customer-support) zu diesem Prozess gehören.
+++

### Wie kontaktiere ich den Adobe-Support? {#customer-support}

+++Antwort
[Eine vollständige Liste der Telefonnummern des Adobe-Kundendienstes](https://helpx.adobe.com/ca/contact/phone.html) ist auf der Hilfeseite zur Adobe verfügbar. Alternativ können Sie Hilfe online finden, indem Sie die folgenden Schritte ausführen:

- Navigieren Sie zu [https://www.adobe.com/](https://www.adobe.com/) in Ihrem Webbrowser.
- Wählen Sie rechts in der oberen Navigationsleiste die Option **[!UICONTROL Anmelden]**.

![Die Adobe-Website mit Anmeldung hervorgehoben.](./images/troubleshooting/adobe-sign-in.png)

- Verwenden Sie Ihre Adobe ID und Ihr Kennwort, die mit Ihrer Adobe-Lizenz registriert sind.
- Auswählen **[!UICONTROL Hilfe und Support]** über die Navigationsleiste am oberen Bildschirmrand.

![Das Dropdown-Menü der oberen Navigationsleiste mit Hilfe und Support, Enterprise-Support und Kontakt wurde hervorgehoben.](./images/troubleshooting/help-and-support.png)

Es wird ein Dropdown-Banner mit einem [!UICONTROL Hilfe und Support] Abschnitt. Auswählen **[!UICONTROL Kontakt]** , um die Adobe Customer Care Virtual Assistant zu öffnen, oder wählen Sie **[!UICONTROL Enterprise-Support]** für spezielle Hilfe für große Organisationen.
+++

### Wie implementiere ich eine sequenzielle Vorgangsreihe, ohne nachfolgende Aufträge auszuführen, wenn der vorherige Auftrag nicht erfolgreich abgeschlossen wurde?

+++Antwort Mit der Funktion für anonyme Bausteine können Sie eine oder mehrere SQL-Anweisungen ketten, die nacheinander ausgeführt werden. Sie ermöglichen auch die Möglichkeit der Ausnahmebehandlung.

Siehe [Anonyme Blockdokumentation](./best-practices/anonymous-block.md) für weitere Details.
+++

### Wie implementiere ich eine benutzerdefinierte Attribution in Query Service?

+++Antwort Es gibt zwei Möglichkeiten, benutzerdefinierte Attribution zu implementieren:

1. Verwenden Sie eine Kombination aus vorhandenem [Adobe-definierte Funktionen](./sql/adobe-defined-functions.md) um festzustellen, ob die Anforderungen des Anwendungsfalls erfüllt sind.
1. Wenn der vorherige Vorschlag Ihren Anwendungsfall nicht erfüllt, sollten Sie eine Kombination aus [Fensterfunktionen](./sql/adobe-defined-functions.md#window-functions). Window-Funktionen betrachten alle Ereignisse in einer Sequenz. Sie ermöglichen es Ihnen auch, die historischen Daten zu überprüfen und können in jeder beliebigen Kombination verwendet werden.
+++

### Kann ich meine Abfragen als Vorlage verwenden, damit ich sie einfach wiederverwenden kann?

++ + Antwort Ja, Sie können Abfragen mithilfe vorbereiteter Anweisungen als Vorlage verwenden. Vorbereitete Anweisungen können die Leistung optimieren und das wiederholte erneute Parsen einer Abfrage vermeiden. Siehe [Vorbereitete Anweisungen - Dokumentation](./sql/prepared-statements.md) für weitere Details.
+++

### Wie erhalte ich Fehlerprotokolle für eine Abfrage? {#error-logs}

+++Antwort Um Fehlerprotokolle für eine bestimmte Abfrage abzurufen, müssen Sie zunächst die Query Service-API verwenden, um die Details des Abfrageprotokolls abzurufen. Die HTTP-Antwort enthält die Abfrage-IDs, die zur Untersuchung eines Abfragefehlers erforderlich sind.

Verwenden Sie den Befehl GET , um mehrere Abfragen abzurufen. Informationen dazu, wie Sie die API aufrufen, finden Sie im Abschnitt [Beispieldokumentation zu API-Aufrufen](./api/queries.md#sample-api-calls).

Identifizieren Sie in der Antwort die Abfrage, die Sie untersuchen möchten, und stellen Sie eine weitere GET-Anfrage mithilfe ihrer `id` -Wert. Vollständige Anweisungen finden Sie im [Abfrage nach ID-Dokumentation abrufen](./api/queries.md#retrieve-a-query-by-id).

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zurück und enthält die `errors` Array. Die Antwort wurde aus Gründen der Kürze gekürzt.

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

Die [Referenzdokumentation zur Query Service API](https://www.adobe.io/experience-platform-apis/references/query-service/) bietet weitere Informationen zu allen verfügbaren Endpunkten.
+++

### Was bedeutet &quot;Fehler beim Validieren des Schemas&quot;?

+++Antwort Die Meldung &quot;Fehler bei Validierung des Schemas&quot;bedeutet, dass das System ein Feld im Schema nicht finden kann. Sie sollten das Best Practice-Dokument für [Organisieren von Daten-Assets in Query Service](./best-practices/organize-data-assets.md) gefolgt von [Erstellen von Tabellen als ausgewählte Dokumentation](./sql/syntax.md#create-table-as-select).

Das folgende Beispiel zeigt die Verwendung einer CTAS-Syntax und eines Strukturdatentyps:

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

++ + Antwort auf die [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) -Klausel verwendet werden, um Daten einer Tabelle basierend auf einer Snapshot-ID inkrementell zu lesen. Dies eignet sich ideal für die Verwendung mit dem [inkrementelle Auslastung](./best-practices/incremental-load.md) Designmuster, das nur Informationen im Datensatz verarbeitet, die seit der letzten Ausführung des Ladevorgangs erstellt oder geändert wurden. Dadurch wird die Verarbeitungseffizienz erhöht und kann sowohl mit Streaming- als auch mit der Batch-Datenverarbeitung verwendet werden.
+++

### Warum unterscheiden sich die in der Profil-Benutzeroberfläche angezeigten Zahlen von den aus dem Profil-Exportdatensatz berechneten Zahlen?

+++Antwort Die im Profil-Dashboard angezeigten Zahlen sind ab dem letzten Schnappschuss korrekt. Die in der Tabelle für den Profilexport erzeugten Zahlen hängen vollständig von der Exportabfrage ab. Daher ist die Abfrage der Anzahl der Profile, die für ein bestimmtes Segment qualifiziert sind, häufig eine Ursache für diese Diskrepanz.

>[!NOTE]
>
>Die Abfrage umfasst historische Daten, während in der Benutzeroberfläche nur die aktuellen Profildaten angezeigt werden.

+++

### Warum hat meine Abfrage eine leere Teilmenge zurückgegeben und was soll ich tun?

+++Antwort Die wahrscheinlichste Ursache ist, dass Ihre Abfrage im Umfang zu eng ist. Sie sollten systematisch einen Abschnitt der `WHERE` -Klausel, bis Sie beginnen, einige Daten anzuzeigen.

Sie können auch mithilfe einer kleinen Abfrage bestätigen, dass Ihr Datensatz Daten enthält, z. B.:

```sql
SELECT count(1) FROM myTableName
```

+++

### Kann ich meine Daten stichprobenweise überprüfen?

+++Antwort Diese Funktion wird derzeit bearbeitet. Details werden im [Versionshinweise](../release-notes/latest/latest.md) und über die Platform-UI-Dialogfelder, sobald die Funktion zur Veröffentlichung bereit ist.
+++

### Welche Hilfsfunktionen werden von Query Service unterstützt?

+++ Query Service bietet mehrere integrierte SQL-Hilfsfunktionen zur Erweiterung der SQL-Funktionalität. Eine vollständige Liste der [Von Query Service unterstützte SQL-Funktionen](./sql/spark-sql-functions.md).
+++

### sind alle nativen [!DNL Spark SQL] Unterstützte Funktionen oder Benutzer, die nur auf den Wrapper beschränkt sind [!DNL Spark SQL] Funktionen der Adobe?

+++Antwort Noch nicht alle Open-Source-Formulare [!DNL Spark SQL] -Funktionen wurden anhand von Daten aus Seeseiden getestet. Nach dem Test und der Bestätigung werden sie der unterstützten Liste hinzugefügt. Lesen Sie hierzu den Abschnitt [Liste der unterstützten [!DNL Spark SQL] Funktionen](./sql/spark-sql-functions.md) , um nach einer bestimmten Funktion zu suchen.
+++

### Können Benutzer ihre eigenen benutzerdefinierten Funktionen (UDF) definieren, die über andere Abfragen hinweg verwendet werden können?

++ + Antwort Aufgrund von Sicherheitsüberlegungen bei der Datensicherheit ist die benutzerdefinierte Definition von UDFs nicht zulässig.
+++

### Was sollte ich tun, wenn meine geplante Abfrage fehlschlägt?

+++Antwort Zunächst überprüfen Sie die Protokolle, um die Details des Fehlers zu ermitteln. Der Abschnitt &quot;FAQ&quot;zu [Fehler in Protokollen suchen](#error-logs) enthält weitere Informationen dazu.

Sie sollten auch die Dokumentation lesen, um Anleitungen zur Leistung zu erhalten [Geplante Abfragen in der Benutzeroberfläche](./ui/user-guide.md#scheduled-queries) und [die API](./api/scheduled-queries.md).

Im Folgenden finden Sie eine Liste von Überlegungen zu geplanten Abfragen bei Verwendung der [!DNL Query Editor]. Sie gelten nicht für die [!DNL Query Service] API:<br/>Sie können einen Zeitplan nur zu einer Abfrage hinzufügen, die bereits erstellt, gespeichert und ausgeführt wurde.<br/>You **cannot** einen Zeitplan zu einer parametrisierten Abfrage hinzufügen.<br/>Geplante Abfragen **cannot** einen anonymen Block enthalten.<br/>Sie können **one** Abfragevorlage, die die Benutzeroberfläche verwendet. Wenn Sie einer Abfragevorlage zusätzliche Zeitpläne hinzufügen möchten, müssen Sie die API verwenden. Wenn ein Zeitplan bereits mithilfe der API hinzugefügt wurde, können Sie keine zusätzlichen Zeitpläne über die Benutzeroberfläche hinzufügen.
+++

### Was bedeutet der Fehler &quot;Sitzungsbegrenzung erreicht&quot;?

+++Antwort &quot;Sitzungsbegrenzung erreicht&quot;bedeutet, dass die für Ihr Unternehmen maximal zulässige Anzahl von Query Service-Sitzungen erreicht wurde. Wenden Sie sich an den Adobe Experience Platform-Administrator Ihrer Organisation.
+++

### Wie behandelt das Abfrageprotokoll Abfragen, die sich auf einen gelöschten Datensatz beziehen?

+++ Query Service löscht den Abfrageverlauf nie. Das bedeutet, dass alle Abfragen, die auf einen gelöschten Datensatz verweisen, als Ergebnis &quot;Kein gültiger Datensatz&quot;zurückgeben.
+++

### Wie erhalte ich nur die Metadaten für eine Abfrage?

+++Antwort Sie können eine Abfrage ausführen, die null Zeilen zurückgibt, um nur die Metadaten in der Antwort zu erhalten. Diese Beispielabfrage gibt nur die Metadaten für die angegebene Tabelle zurück.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### Wie kann ich eine CTAS-Abfrage (Tabelle als Auswahl erstellen) schnell durchlaufen, ohne sie zu materialisieren?

+++Antwort Sie können temporäre Tabellen erstellen, um eine Abfrage schnell zu iterieren und zu experimentieren, bevor sie zur Verwendung materialisiert wird. Sie können auch temporäre Tabellen verwenden, um zu überprüfen, ob eine Abfrage funktioniert.

Sie können beispielsweise eine temporäre Tabelle erstellen:

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

++ + Antwort Adobe Experience Platform behält Daten im UTC-Zeitstempelformat (Coordinated Universal Time) bei. Ein Beispiel für das UTC-Format ist `2021-12-22T19:52:05Z`

Query Service unterstützt integrierte SQL-Funktionen zum Konvertieren eines bestimmten Zeitstempels in das und aus dem UTC-Format. Beide `to_utc_timestamp()` und `from_utc_timestamp()` -Methoden haben zwei Parameter: Zeitstempel und Zeitzone.

| Parameter | Beschreibung |
|-----------|---------------|
| Zeitstempel | Der Zeitstempel kann entweder im UTC-Format oder einfach geschrieben werden `{year-month-day}` Format. Wenn keine Zeit angegeben wird, ist der Standardwert Mitternacht am Morgen des angegebenen Tages. |
| Zeitzone | Die Zeitzone wird in einer `{continent/city})` Format. Es muss sich um einen der anerkannten Zeitzonen-Codes handeln, die im [Public-Domain-TZ-Datenbank](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### In den UTC-Zeitstempel konvertieren

Die `to_utc_timestamp()` -Methode interpretiert die angegebenen Parameter und konvertiert sie **zum Zeitstempel Ihrer lokalen Zeitzone** im UTC-Format. Beispielsweise ist die Zeitzone in Seoul, Südkorea UTC/GMT +9 Stunden. Durch Angabe eines reinen Datums-Zeitstempels verwendet die Methode den Standardwert Mitternacht am Morgen. Der Zeitstempel und die Zeitzone werden vom Zeitpunkt dieser Region in einen UTC-Zeitstempel Ihrer lokalen Region in das UTC-Format konvertiert.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

Die Abfrage gibt einen Zeitstempel in der Ortszeit des Benutzers zurück. In diesem Fall 15 Uhr am Vortag, da Seoul neun Stunden vor uns liegt.

```
2021-08-30 15:00:00
```

Ein weiteres Beispiel: Wenn der angegebene Zeitstempel `2021-07-14 12:40:00.0` für `Asia/Seoul` timezone, würde der zurückgegebene UTC-Zeitstempel `2021-07-14 03:40:00.0`

Die in der Benutzeroberfläche von Query Service bereitgestellte Konsolenausgabe ist ein für Menschen lesbareres Format:

```
8/30/2021, 3:00 PM
```

#### Aus UTC-Zeitstempel konvertieren

Die `from_utc_timestamp()` -Methode interpretiert die angegebenen Parameter **aus dem Zeitstempel Ihrer lokalen Zeitzone** und stellt den entsprechenden Zeitstempel der gewünschten Region im UTC-Format bereit. Im folgenden Beispiel ist die Stunde 14:40 Uhr in der lokalen Zeitzone des Benutzers. Die Seoul-Zeitzone, die als Variable übergeben wird, liegt neun Stunden vor der lokalen Zeitzone.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

Die Abfrage gibt einen Zeitstempel im UTC-Format für die Zeitzone zurück, die als Parameter übergeben wird. Das Ergebnis liegt neun Stunden vor der Zeitzone, die die Abfrage ausgeführt hat.

```
8/31/2021, 11:40 PM
```

### Wie sollte ich meine Zeitreihendaten filtern?

+++Antwort Bei Abfragen mit Zeitreihendaten sollten Sie den Zeitstempelfilter verwenden, wann immer dies möglich ist, um eine genauere Analyse zu ermöglichen.

>[!NOTE]
>
> Die Datums-Zeichenfolge **must** im Format `yyyy-mm-ddTHH24:MM:SS`.

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

### Wie verwende ich die `CAST` Operator zum Konvertieren meiner Zeitstempel in SQL-Abfragen?

+++Antwort Bei Verwendung der `CAST` zum Konvertieren eines Zeitstempels verwenden, müssen Sie beide das Datum angeben **und** Zeit.

Wenn beispielsweise die Zeitkomponente fehlt, wie unten dargestellt, wird ein Fehler ausgegeben:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

Die korrekte Verwendung der `CAST` -Operator finden Sie unten:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### Sollte ich Platzhalter verwenden, z. B. * , um alle Zeilen aus meinen Datensätzen zu erhalten?

+++Antwort Sie können keine Platzhalter verwenden, um alle Daten aus Ihren Zeilen abzurufen, da Query Service als **columnar-store** anstatt eines herkömmlichen Zeilenspeichersystems.
+++

### Sollte ich `NOT IN` in meiner SQL-Abfrage?

++ + Antwort auf die `NOT IN` -Operator wird häufig zum Abrufen von Zeilen verwendet, die nicht in einer anderen Tabelle oder SQL-Anweisung gefunden werden. Dieser Operator kann die Leistung verlangsamen und unerwartete Ergebnisse zurückgeben, wenn die verglichenen Spalten akzeptiert werden `NOT NULL`oder Sie haben eine große Anzahl von Datensätzen.

anstelle von `NOT IN`können Sie entweder `NOT EXISTS` oder `LEFT OUTER JOIN`.

Wenn Sie beispielsweise die folgenden Tabellen erstellt haben:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Wenn Sie die `NOT EXISTS` -Operator verwenden, können Sie die `NOT IN` -Operator mithilfe der folgenden Abfrage verwenden:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Wenn Sie die `LEFT OUTER JOIN` -Operator verwenden, können Sie die `NOT IN` -Operator mithilfe der folgenden Abfrage verwenden:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### Kann ich einen Datensatz mit einer CTAS-Abfrage mit einem doppelten Unterstrich erstellen, wie er in der Benutzeroberfläche angezeigt wird? Beispiel: `test_table_001`.

++ + Antwort Nein, dies ist eine absichtliche Einschränkung in der gesamten Experience Platform, die für alle Adobe-Dienste gilt, einschließlich Query Service. Ein Name mit zwei Unterstrichen ist als Schema- und Datensatzname zulässig, der Tabellenname für den Datensatz darf jedoch nur einen Unterstrich enthalten.
+++

### Wie viele gleichzeitige Abfragen können gleichzeitig ausgeführt werden?

+++Antwort Es gibt keine Zeitbeschränkung für Abfragen, da Batch-Abfragen als Back-End-Aufträge ausgeführt werden. Es gibt jedoch eine Zeitüberschreitungsbegrenzung für Abfragen, die auf 24 Stunden festgelegt ist.
+++

### Gibt es ein Aktivitäts-Dashboard, in dem Sie Abfrageaktivitäten und -status sehen können?

+++Antwort Es gibt Überwachungs- und Warnfunktionen, mit denen Sie sich über Abfrageaktivitäten und -status informieren können. Siehe [Auditprotokollintegration für Query Service](./data-governance/audit-log-guide.md) und [Abfrageprotokolle](./ui/overview.md#log) Dokumente für weitere Informationen.
+++

### Gibt es eine Möglichkeit, Aktualisierungen rückgängig zu machen? Wenn beispielsweise ein Fehler auftritt oder einige Berechnungen beim Zurückschreiben von Daten in Platform neu konfiguriert werden müssen, wie sollte dieses Szenario behandelt werden?

+++Antwort Derzeit unterstützen wir keine Rollbacks oder Aktualisierungen auf diese Weise.
+++

### Wie können Abfragen in Adobe Experience Platform optimiert werden?

+++Antwort Das System hat keine Indizes, da es keine Datenbank ist, aber andere Optimierungen an Ort und Stelle an den Datenspeicher gebunden sind. Die folgenden Optionen stehen zur Abstimmung Ihrer Abfragen zur Verfügung:

- Ein zeitbasierter Filter für Zeitreihendaten.
- Optimierter Push-Down für den strukturierten Datentyp.
- Optimiertes Kosten- und Arbeitsspeicher-Push-down für Arrays und Zuordnungs-Datentypen.
- Inkrementelle Verarbeitung mit Momentaufnahmen.
- Ein beibehaltenes Datenformat.
+++

### Können Anmeldungen auf bestimmte Aspekte von Query Service beschränkt werden oder ist dies eine &quot;alles oder nichts&quot;-Lösung?

+++ Query Service ist eine &quot;alles oder nichts&quot;-Lösung. Teilzugriff kann nicht gewährt werden.
+++

### Kann ich einschränken, welche Daten Query Service verwenden kann, oder greift er einfach auf den gesamten Adobe Experience Platform Data Lake zu?

+++Antwort Ja, Sie können die Abfrage auf Datensätze mit schreibgeschütztem Zugriff beschränken.
+++

### Welche anderen Optionen gibt es zum Einschränken der Daten, auf die Query Service zugreifen kann?

+++Antwort Es gibt drei Möglichkeiten, den Zugriff zu beschränken. Sie lauten wie folgt:

- Verwenden Sie ausschließlich SELECT-Anweisungen und gewähren Sie Datensätzen Lesezugriff. Weisen Sie außerdem die Berechtigung zum Verwalten von Abfragen zu.
- Verwenden Sie SELECT/INSERT/CREATE -Anweisungen und geben Sie Datensätzen Schreibzugriff. Weisen Sie außerdem die Berechtigung zur Verwaltung von Abfragen zu.
- Verwenden Sie ein Integrationskonto mit den oben genannten Vorschlägen und weisen Sie die Berechtigung für die Abfrageintegration zu.

+++

### Gibt es nach Rückgabe der Daten durch Query Service irgendwelche Prüfungen, die von Platform ausgeführt werden können, um sicherzustellen, dass keine geschützten Daten zurückgegeben wurden?

- Query Service unterstützt eine attributbasierte Zugriffskontrolle. Sie können den Zugriff auf Daten auf Spalten-/Blattebene und/oder Strukturebene einschränken. Weitere Informationen zur attributbasierten Zugriffskontrolle finden Sie in der Dokumentation .

### Kann ich einen SSL-Modus für die Verbindung zu einem Drittanbieter-Client angeben? Kann ich beispielsweise &quot;verify-full&quot;mit Power BI verwenden?

++ + Antwort Ja, SSL-Modi werden unterstützt. Siehe [Dokumentation zu SSL-Modi](./clients/ssl-modes.md) für eine Aufschlüsselung der verschiedenen verfügbaren SSL-Modi und des Schutzniveaus, das sie bieten.
+++

### Verwenden wir TLS 1.2 für alle Verbindungen von Power BI-Clients zum Abfragedienst?

+++Antwort Ja. Daten-in-Transit sind immer HTTPS-konform. Die derzeit unterstützte Version ist TLS1.2.
+++

### Verwendet eine Verbindung, die an Port 80 hergestellt wurde, weiterhin HTTPS?

+++Antwort Ja, eine Verbindung, die an Port 80 hergestellt wird, verwendet weiterhin SSL. Sie können auch Port 5432 verwenden.
+++

### Kann ich den Zugriff auf bestimmte Datensätze und Spalten für eine bestimmte Verbindung steuern? Wie ist dies konfiguriert?

++ + Antwort Ja, die attributbasierte Zugriffssteuerung wird erzwungen, wenn konfiguriert. Siehe [Attributbasierte Zugriffskontrolle - Übersicht](../access-control/abac/overview.md) für weitere Informationen.
+++

## Exportieren von Daten {#exporting-data}

Dieser Abschnitt enthält Informationen zum Exportieren von Daten und Einschränkungen.

### Gibt es eine Möglichkeit, Daten aus Query Service nach der Abfrageverarbeitung zu extrahieren und die Ergebnisse in einer CSV-Datei zu speichern? {#export-csv}

+++Antwort Ja. Daten können aus Query Service extrahiert werden. Außerdem besteht die Möglichkeit, die Ergebnisse über einen SQL-Befehl im CSV-Format zu speichern.

Es gibt zwei Möglichkeiten, die Ergebnisse einer Abfrage bei der Verwendung eines PSQL-Clients zu speichern. Sie können die `COPY TO` -Befehl oder erstellen Sie eine -Anweisung im folgenden Format:

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Leitlinien für die Verwendung der `COPY TO` command](./sql/syntax.md#copy) finden Sie in der SQL-Syntaxreferenz-Dokumentation.
+++

### Kann ich den Inhalt des endgültigen Datensatzes extrahieren, der über CTAS-Abfragen erfasst wurde (vorausgesetzt, es handelt sich um größere Datenmengen wie Terabytes)?

+++Antwort Nr. Es gibt derzeit keine Funktion für die Extraktion erfasster Daten.
+++

### Warum gibt der Analytics-Data Connector keine Daten zurück?

+++Antwort Eine häufige Ursache für dieses Problem ist die Abfrage von Zeitreihendaten ohne Zeitfilter. Beispiel:

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

## Drittanbieter-Tools {#third-party-tools}

Dieser Abschnitt enthält Informationen zur Verwendung von Drittanbieter-Tools wie PSQL und Power BI.

### Kann ich Query Service mit einem Tool eines Drittanbieters verbinden?

++ + Antwort Ja, Sie können mehrere Desktop-Clients von Drittanbietern mit Query Service verbinden. Weitere Informationen finden Sie in der Dokumentation für [Vollständige Details zu den verfügbaren Clients und wie sie mit Query Service verbunden werden](./clients/overview.md).
+++

### Gibt es eine Möglichkeit, Query Service einmal für die kontinuierliche Verwendung mit einem Tool eines Drittanbieters zu verbinden?

++ + Antwort Ja, Desktop-Clients von Drittanbietern können über eine einmalige Einrichtung ohne ablaufende Anmeldeinformationen mit Query Service verbunden werden. Nicht ablaufende Anmeldeinformationen können von einem autorisierten Benutzer generiert und in einer JSON-Datei empfangen werden, die automatisch auf den lokalen Computer heruntergeladen wird. Voll [Anleitung zum Erstellen und Herunterladen nicht ablaufender Anmeldedaten](./ui/credentials.md#non-expiring-credentials) finden Sie in der Dokumentation.
+++

### Warum funktionieren meine nicht ablaufenden Anmeldeinformationen nicht?

+++Antwort Der Wert für nicht ablaufende Anmeldeinformationen sind die verketteten Argumente aus dem `technicalAccountID` und `credential` aus der JSON-Konfigurationsdatei übernommen. Der Kennwortwert hat folgende Form: `{{technicalAccountId}:{credential}}`.
Weitere Informationen zum [Verbindung zu externen Clients mit Anmeldeinformationen herstellen](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### Welche Art von SQL-Editoren von Drittanbietern kann ich mit dem Query Service Editor verbinden?

+++Antwort Alle SQL-Editoren von Drittanbietern, die PSQL oder [!DNL Postgres] Client-kompatibel ist, kann mit dem Query Service Editor verbunden werden. Weitere Informationen finden Sie in der Dokumentation für [Clients mit Query Service verbinden](./clients/overview.md) für eine Liste der verfügbaren Anweisungen.
+++

### Kann ich das Power BI-Tool mit Query Service verbinden?

++ + Antwort Ja, Sie können Power BI mit Query Service verbinden. Weitere Informationen finden Sie in der Dokumentation für [Anweisungen zum Verbinden des Power BI-Desktop-Programms mit Query Service](./clients/power-bi.md).
+++

### Warum dauert das Laden der Dashboards bei der Verbindung mit Query Service lange?

++ + Antwort Wenn das System mit Query Service verbunden ist, ist es mit einer interaktiven oder Batch-Verarbeitungs-Engine verbunden. Dies kann zu längeren Ladezeiten führen, um die verarbeiteten Daten widerzuspiegeln.

Wenn Sie die Antwortzeiten für Ihre Dashboards verbessern möchten, sollten Sie einen Business Intelligence-Server (BI) als Zwischenspeicherungsschicht zwischen Query Service- und BI-Tools implementieren. Im Allgemeinen bieten die meisten BI-Tools ein zusätzliches Angebot für einen Server.

Durch Hinzufügen der Cacheserver-Ebene werden die Daten aus Query Service zwischengespeichert und Dashboards können die Antwort auf diese Weise beschleunigen. Dies ist möglich, da die Ergebnisse für ausgeführte Abfragen jeden Tag auf dem BI-Server zwischengespeichert werden. Der Caching-Server stellt diese Ergebnisse dann für jeden Benutzer mit derselben Abfrage bereit, um die Latenz zu verringern. Weitere Informationen zu dieser Einrichtung finden Sie in der Dokumentation zum Dienstprogramm oder Tool von Drittanbietern, das Sie verwenden.
+++

### Ist der Zugriff auf Query Service über das pgAdmin-Verbindungstool möglich?

++ + Antwort Nein, pgAdmin-Konnektivität wird nicht unterstützt. A [Liste der verfügbaren Clients von Drittanbietern und Anweisungen zur Verbindung dieser Clients mit Query Service](./clients/overview.md) finden Sie in der Dokumentation.
+++

## PostgreSQL-API-Fehler {#postgresql-api-errors}

Die folgende Tabelle enthält PSQL-Fehlercodes und die möglichen Ursachen.

| Fehler-Code | Verbindungsstatus | Beschreibung | Mögliche Ursache |
|------------|---------------------------|-------------|----------------|
| **08P01** | K. A. | Nicht unterstützter Nachrichtentyp | Nicht unterstützter Nachrichtentyp |
| **28P01** | Start-up - Authentifizierung | Ungültiges Kennwort | Ungültiges Authentifizierungs-Token |
| **28000** | Start-up - Authentifizierung | Ungültiger Autorisierungstyp | Ungültiger Autorisierungstyp. Muss `AuthenticationCleartextPassword`sein. |
| **42P12** | Start-up - Authentifizierung | Keine Tabellen gefunden | Keine Tabellen zur Verwendung gefunden |
| **42601** | Abfrage | Syntaxfehler | Ungültiger Befehl- oder Syntaxfehler |
| **42P01** | Abfrage | Tabelle nicht gefunden | Die in der Abfrage angegebene Tabelle wurde nicht gefunden |
| **42P07** | Abfrage | Tabelle vorhanden | Eine Tabelle mit demselben Namen ist bereits vorhanden (CREATE TABLE) |
| **53400** | Abfrage | LIMIT überschreitet den Maximalwert | Benutzer hat eine LIMIT-Klausel über 100.000 angegeben |
| **53400** | Abfrage | Anweisungs-Timeout | Die abgesendete Live-Anweisung dauerte mehr als 10 Minuten |
| **58000** | Abfrage | Systemfehler | Interner Systemfehler |
| **0A000** | Abfrage/Befehl | Nicht unterstützt | Die Funktion/Funktion in der Abfrage/dem Befehl wird nicht unterstützt |
| **42501** | DROP TABLE Query | Dropdown-Tabelle, die nicht von Query Service erstellt wurde | Die abgelegte Tabelle wurde nicht von Query Service mit dem `CREATE TABLE` statement |
| **42501** | DROP TABLE Query | Vom authentifizierten Benutzer nicht erstellte Tabelle | Die abgelegte Tabelle wurde nicht vom aktuell angemeldeten Benutzer erstellt |
| **42P01** | DROP TABLE Query | Tabelle nicht gefunden | Die in der Abfrage angegebene Tabelle wurde nicht gefunden |
| **42P12** | DROP TABLE Query | Keine Tabelle gefunden für `dbName`: Bitte überprüfen Sie die `dbName` | In der aktuellen Datenbank wurden keine Tabellen gefunden |

### Warum habe ich einen Fehlercode 58000 erhalten, wenn ich die history_meta() -Methode in meiner Tabelle verwende?

++ + Antwort auf die `history_meta()` -Methode verwendet wird, um auf einen Schnappschuss aus einem Datensatz zuzugreifen. Wenn Sie zuvor eine Abfrage für einen leeren Datensatz in Azure Data Lake Storage (ADLS) ausführen würden, würden Sie einen Fehlercode 58000 erhalten, der besagt, dass der Datensatz nicht vorhanden ist. Nachfolgend finden Sie ein Beispiel für den alten Systemfehler.

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

Dieser Fehler ist aufgetreten, weil für die Abfrage kein Rückgabewert vorhanden war. Dieses Verhalten wurde behoben, um die folgende Meldung zurückzugeben:

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## REST-API-Fehler {#rest-api-errors}

Die folgende Tabelle enthält HTTP-Fehlercodes und die möglichen Ursachen.

| HTTP-Statuscode | Beschreibung | Mögliche Ursachen |
|------------------|-----------------------|----------------------------|
| 400 | Ungültige Anfrage | Falsch formulierte oder illegale Abfrage |
| 401 | Authentifizierung fehlgeschlagen | Ungültiges Authentifizierungs-Token |
| 500 | Interner Server-Fehler | Interner Systemfehler |
