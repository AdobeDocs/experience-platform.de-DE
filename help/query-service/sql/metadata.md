---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Metadaten, Befehle
topic: metadata
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Metadaten, Befehle

Für Metadaten in Ihrem Datensatz werden derzeit die folgenden PSQL-Befehle zum Abfragen unterstützt:

>[!NOTE]
>
>Bei den unten aufgeführten Befehlen wird zwischen Groß- und Kleinschreibung unterschieden.

| Befehl | Beschreibung |
|------- | ------------|
| `\conninfo` | Gibt Informationen zur aktuellen Datenbankverbindung aus. |
| `\d` | Zeigt eine Liste aller sichtbaren Tabellen, Ansichten, materialisierten Ansichten, Sequenzen und Fremdtabellen an. |
| `\dE` | Zeigt eine Liste mit ausländischen Tabellen an. |
| `\df or \df+` | Zeigt eine Liste der Funktionen an. |
| `\di` | Zeigt eine Liste von Indizes an. |
| `\dm` | Zeigt eine Liste der materialisierten Ansichten an. |
| `\dn` | Zeigt eine Liste der Schema (Namensraum) an. |
| `\ds` | Zeigt eine Liste von Sequenzen an. |
| `\dS` | Zeigt eine Liste von PostgreSQL-definierten Tabellen an. |
| `\dt` | Zeigt eine Liste von Tabellen an. |
| `\dT` | Zeigt eine Liste der Datentypen an. |
| `\dv` | Zeigt eine Liste der Ansichten an. |
| `\encoding` | Liste der aktuellen Client-Zeichensatzkodierung. |
| `\errverbose` | Wiederholt die letzte Serverfehlermeldung mit maximaler Ausführlichkeit. |
| `\l or \list` | Zeigt eine Liste von Datenbanken auf dem Server an. |
| `\set` | Zeigt die Namen und Werte aller aktuellen psql-Variablen an. |
| `\showtables` | Zeigt die folgenden Informationen an: <br>name: Der Name, unter dem auf die Tabelle verwiesen wird.<br>datasetId: Die ID des gespeicherten Datensatzes.<br>Datensatz: Der Name des gespeicherten Datensatzes.<br>description: Eine Beschreibung des Datensatzes.<br>gelöst: Ein boolescher Wert, der angibt, ob der Datensatz in der aktuellen Sitzung aufgelöst wird. |
| `\timing` | Schaltet die Anzeige zwischen ein und aus um. Die Anzeige erfolgt in Millisekunden. Zeiträume von mehr als einer Sekunde werden im Format Minuten:Sekunden angezeigt, wobei bei Bedarf Stunden- und Tagesfelder hinzugefügt werden. |

Alle Befehle, mit denen Beginn kombiniert werden `\d` kann. Beispielsweise können Sie eine Liste aller Tabellen, Sequenzen und Schema anzeigen `\dtsn` lassen. `\d` zeigt alle sichtbaren Tabellen, Ansichten, materialisierten Ansichten und Sequenzen an.

Weitere Informationen zu den oben aufgeführten Befehlen finden Sie in der Dokumentation unter [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Beachten Sie jedoch, dass nicht alle in der PostgreSQL-Dokumentation aufgeführten Optionen von der Experience Platform unterstützt werden.

