---
keywords: Experience Platform; Startseite; beliebte Themen; PSQL; psql; Query Service; Query Service; Metadaten; Befehle; Metadatenbefehle
solution: Experience Platform
title: Metadaten-PostgreSQL-Befehle in Query Service
topic-legacy: metadata
description: Eine Liste der PostgreSQL-Befehle, die derzeit für die Abfrage von Metadaten in Adobe Experience Platform Query Service unterstützt werden.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Metadaten [!DNL PostgreSQL] Befehle in Query Service

Für Metadaten in Ihrem Datensatz gilt Folgendes: [!DNL PostgreSQL] -Befehle werden derzeit für Abfragen unterstützt:

>[!NOTE]
>
>Bei den folgenden Befehlen wird zwischen Groß- und Kleinschreibung unterschieden.

| Befehl | Beschreibung |
|------- | ------------|
| `\conninfo` | Gibt Informationen zur aktuellen Datenbankverbindung aus. |
| `\d` | Zeigt eine Liste aller sichtbaren Tabellen, Ansichten, materialisierten Ansichten, Sequenzen und fremden Tabellen an. |
| `\dE` | Zeigt eine Liste mit ausländischen Tabellen an. |
| `\df or \df+` | Zeigt eine Liste der Funktionen an. |
| `\di` | Zeigt eine Liste von Indizes an. |
| `\dm` | Zeigt eine Liste der materialisierten Ansichten an. |
| `\dn` | Zeigt eine Liste von Schemas (Namespaces) an. |
| `\ds` | Zeigt eine Liste von Sequenzen an. |
| `\dS` | Zeigt eine Liste der von PostgreSQL definierten Tabellen an. |
| `\dt` | Zeigt eine Liste von Tabellen an. |
| `\dT` | Zeigt eine Liste der Datentypen an. |
| `\dv` | Zeigt eine Liste der Ansichten an. |
| `\encoding` | Listet die aktuelle Client-Zeichensatzkodierung auf. |
| `\errverbose` | Wiederholt die neueste Server-Fehlermeldung mit maximaler Ausführlichkeit. |
| `\l or \list` | Zeigt eine Liste der Datenbanken auf dem Server an. |
| `\set` | Zeigt die Namen und Werte aller aktuellen psql-Variablen an. |
| `\showtables` | Zeigt die folgenden Informationen an: <br>name: Der Name, mit dem auf die Tabelle verwiesen wird.<br>datasetId: Die ID des Datensatzes, der gespeichert wird.<br>Datensatz: Der Name des Datensatzes, der gespeichert wird.<br>description: Eine Beschreibung des Datensatzes.<br>aufgelöst: Ein boolean -Wert, der angibt, ob der Datensatz in der aktuellen Sitzung aufgelöst wurde. |
| `\timing` | Schaltet die Anzeige zwischen ein und aus. Die Anzeige wird in Millisekunden dargestellt. Zeiträume von mehr als einer Sekunde werden im Format Minuten:Sekunden angezeigt, wobei bei Bedarf Stunden- und Tagesfelder hinzugefügt werden. |

Alle Befehle, die mit `\d` kann kombiniert werden. Beispielsweise können Sie `\dtsn` , um eine Liste aller Tabellen, Sequenzen und Schemas anzuzeigen. `\d` zeigt selbst alle sichtbaren Tabellen, Ansichten, materialisierten Ansichten und Sequenzen an.

Weitere Informationen zu den oben aufgeführten Befehlen finden Sie in der Dokumentation unter [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Beachten Sie jedoch, dass nicht alle Optionen in der [!DNL PostgreSQL] -Dokumentation unterstützt von [!DNL Experience Platform].
