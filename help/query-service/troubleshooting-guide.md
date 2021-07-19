---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; Handbuch zur Fehlerbehebung; FAQ; Fehlerbehebung
solution: Experience Platform
title: Anleitung zur Fehlerbehebung bei Query Service
topic-legacy: troubleshooting
description: Dieses Dokument enthält Informationen zu häufigen Fehlercodes, auf die Sie stoßen, sowie zu den möglichen Ursachen.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: e3557fe75680153f051b8a864ad8f6aca5f743ee
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 35%

---

# [!DNL Query Service] Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Query Service und eine Liste der häufig verwendeten Fehlercodes bei Verwendung von Query Service. Fragen und Informationen zur Fehlerbehebung bei anderen Diensten in Adobe Experience Platform finden Sie im [Handbuch zur Fehlerbehebung bei Experience Platformen](../landing/troubleshooting.md).

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
WHERE timestamp >= To_timestamp('2021-01-21 12:00:00')
AND timestamp < To_timestamp('2021-01-21 13:00:00')
LIMIT 100;
```

### Wie sollte ich meine Zeitreihendaten filtern?

Bei Abfragen mit Zeitreihendaten sollten Sie nach Möglichkeit den Zeitstempelfilter verwenden, um eine genauere Analyse zu ermöglichen.

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

Sie können keine Platzhalterzeichen verwenden, um alle Daten aus Ihren Zeilen abzurufen, da Query Service nicht als herkömmliches Zeilenbasiertes Speichersystem, sondern als **columnar-store** behandelt werden sollte.

## REST-API-Fehler

| HTTP-Status-Code | Beschreibung | Mögliche Ursachen |
| ---------------- | ----------- | --------------- |
| 400 | Ungültige Anfrage | Falsch formulierte oder illegale Abfrage |
| 401 | Authentifizierung fehlgeschlagen | Ungültiges Authentifizierungs-Token |
| 500 | Interner Server-Fehler | Interner Systemfehler |

## PostgreSQL-API-Fehler

| Fehlercode und Verbindungsstatus | Beschreibung | Mögliche Ursache |
| ------------------------------- | ----------- | -------------- |
| **28P01** Start-up – Authentifizierung | Ungültiges Kennwort | Ungültiges Authentifizierungs-Token |
| **28000** Start-up – Authentifizierung | Ungültiger Autorisierungstyp | Ungültiger Autorisierungstyp. Muss `AuthenticationCleartextPassword`sein. |
| **42P12** Start-up – Authentifizierung | Keine Tabellen gefunden | Keine Tabellen zur Verwendung gefunden |
| **42601** Abfrage | Syntaxfehler | Ungültiger Befehl- oder Syntaxfehler |
| **58000** Abfrage | Systemfehler | Interner Systemfehler |
| **42P01** Abfrage | Tabelle nicht gefunden | Die in der Abfrage angegebene Tabelle wurde nicht gefunden |
| **42P07** Abfrage | Tabelle vorhanden | Tabelle ist bereits mit demselben Namen vorhanden (CREATE TABLE) |
| **53400** Abfrage | LIMIT überschreitet den Maximalwert | Benutzer hat eine LIMIT-Klausel über 100.000 angegeben |
| **53400** Abfrage | Anweisungs-Timeout | Die abgesendete Live-Anweisung dauerte mehr als 10 Minuten |
| **08P01** K. A. | Nicht unterstützter Nachrichtentyp | Nicht unterstützter Nachrichtentyp |
