---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; Handbuch zur Fehlerbehebung; FAQ; Fehlerbehebung
solution: Experience Platform
title: Anleitung zur Fehlerbehebung bei Query Service
topic-legacy: troubleshooting
description: Dieses Dokument enthält Informationen zu häufigen Fehlercodes, auf die Sie stoßen, sowie zu den möglichen Ursachen.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: ac313e2a23037507c95d6713a83ad5ca07e1cd85
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 17%

---

# [!DNL Query Service] Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Query Service und eine Liste der häufig verwendeten Fehlercodes bei Verwendung von Query Service. Fragen und Antworten zur Fehlerbehebung bei anderen Diensten in Adobe Experience Platform finden Sie im Abschnitt [Handbuch zur Fehlerbehebung bei Experience Platformen](../landing/troubleshooting.md).

## Häufig gestellte Fragen

Im Folgenden finden Sie eine Liste von Antworten auf häufig gestellte Fragen zu Query Service.

### Wie erhalte ich nur die Metadaten für eine Abfrage?

Um nur die Metadaten für eine Abfrage abzurufen, können Sie wie folgt eine Abfrage ausführen, die null Zeilen zurückgibt:

```sql
SELECT * FROM <table> WHERE 1=0
```

Diese Abfrage gibt nur die Metadaten für die angegebene Tabelle zurück.

### Wie kann ich eine CTAS-Abfrage (Tabelle als Auswahl erstellen) schnell durchlaufen, ohne sie zu materialisieren?

Sie können temporäre Tabellen erstellen, um eine Abfrage schnell zu iterieren und zu experimentieren, bevor sie zur Verwendung materialisiert wird. Sie können auch temporäre Tabellen verwenden, um zu überprüfen, ob eine Abfrage funktioniert.

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

### Wie sollte ich meine Zeitreihendaten filtern?

Bei Abfragen mit Zeitreihendaten sollten Sie nach Möglichkeit den Zeitstempelfilter verwenden, um eine genauere Analyse zu ermöglichen.

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

### Sollte ich Platzhalter verwenden, z. B. * , um alle Zeilen aus meinen Datensätzen zu erhalten?

Sie können nicht mit Platzhaltern alle Daten aus Ihren Zeilen abrufen, da Query Service als **columnar-store** anstatt eines herkömmlichen Zeilenspeichersystems.

### Sollte ich `NOT IN` in meiner SQL-Abfrage?

Die `NOT IN` -Operator wird häufig zum Abrufen von Zeilen verwendet, die nicht in einer anderen Tabelle oder SQL-Anweisung gefunden werden. Dieser Operator kann die Leistung verlangsamen und unerwartete Ergebnisse zurückgeben, wenn die verglichenen Spalten akzeptiert werden `NOT NULL`oder Sie haben eine große Anzahl von Datensätzen.

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

### Was ist die korrekte Verwendung der `OR` und `UNION` Operatoren?

### Wie verwende ich die `CAST` Operator zum Konvertieren meiner Zeitstempel in SQL-Abfragen?

Bei Verwendung von `CAST` zum Konvertieren eines Zeitstempels verwenden, müssen Sie beide das Datum angeben **und** Zeit.

Wenn beispielsweise die Zeitkomponente fehlt, wie unten dargestellt, wird ein Fehler ausgegeben:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

eine korrekte Verwendung der `CAST` -Operator finden Sie unten:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

### Wie kann ich meine Abfrageergebnisse als CSV-Datei herunterladen?

Dies ist keine Funktion, die Query Service direkt anbietet. Wenn die [!DNL PostgreSQL] Client, der für die Verbindung mit dem Datenbankserver verwendet wird, verfügt über die Möglichkeit, die Antwort einer SELECT-Abfrage zu schreiben und als CSV-Datei herunterzuladen. Weitere Informationen zu diesem Prozess finden Sie in der Dokumentation zum Dienstprogramm oder Tool von Drittanbietern, das Sie verwenden.

## REST-API-Fehler

| HTTP-Statuscode | Beschreibung | Mögliche Ursachen |
| ---------------- | ----------- | --------------- |
| 400 | Ungültige Anfrage | Falsch formulierte oder illegale Abfrage |
| 401 | Authentifizierung fehlgeschlagen | Ungültiges Authentifizierungs-Token |
| 500 | Interner Server-Fehler | Interner Systemfehler |

## PostgreSQL-API-Fehler

| Fehler-Code | Verbindungsstatus | Beschreibung | Mögliche Ursache |
| ---------- | ---------------- | ----------- | -------------- |
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
