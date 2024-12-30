---
keywords: Experience Platform;Startseite;beliebte Themen;PSQL;psql;Abfrage-Service;Abfrage-Service;Metadaten;Befehle;Metadatenbefehle;
solution: Experience Platform
title: Metadaten-PostgreSQL-Befehle im Abfrage-Service
description: Eine Liste der PostgreSQL-Befehle, die derzeit für die Abfrage von Metadaten im Abfrage-Service von Adobe Experience Platform unterstützt werden.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Metadaten [!DNL PostgreSQL] Befehle im Abfrage-Service

Für Metadaten in Ihrem Datensatz werden derzeit die folgenden [!DNL PostgreSQL]-Befehle für die Abfrage unterstützt:

>[!NOTE]
>
>Bei den unten aufgeführten Befehlen wird zwischen Groß- und Kleinschreibung unterschieden.

| Befehl | Beschreibung |
|------- | ------------|
| `\conninfo` | Gibt Informationen zur aktuellen Datenbankverbindung aus. |
| `\d` | Zeigt eine Liste aller sichtbaren Tabellen, Ansichten, materialisierten Ansichten, Sequenzen und Fremdtabellen an. |
| `\dE` | Zeigt eine Liste der Fremdtabellen an. |
| `\df or \df+` | Zeigt eine Liste der Funktionen an. |
| `\di` | Zeigt eine Liste von Indizes an. |
| `\dm` | Zeigt eine Liste materialisierter Ansichten an. |
| `\dn` | Zeigt eine Liste von Schemas (Namespaces) an. |
| `\ds` | Zeigt eine Liste von Sequenzen an. |
| `\dS` | Zeigt eine Liste der von PostgreSQL definierten Tabellen an. |
| `\dt` | Zeigt eine Liste von Tabellen an. |
| `\dT` | Zeigt eine Liste der Datentypen an. |
| `\dv` | Zeigt eine Liste von Ansichten an. |
| `\encoding` | Listet die aktuelle Clientzeichensatzkodierung auf. |
| `\errverbose` | Wiederholt die letzte Server-Fehlermeldung mit maximaler Ausführlichkeit. |
| `\l or \list` | Zeigt eine Liste der Datenbanken auf dem Server an. |
| `\set` | Zeigt die Namen und Werte aller aktuellen PSQL-Variablen an. |
| `\showtables` | Zeigt die folgenden Informationen an: <br>name: Der Name, mit dem auf die Tabelle verwiesen wird.<br>datasetId: Die ID des Datensatzes, der gespeichert wird.<br>dataset: Der Name des Datensatzes, der gespeichert wird.<br>description: Eine Beschreibung des Datensatzes.<br>resolved: Ein boolescher Wert, der angibt, ob der Datensatz in der aktuellen Sitzung aufgelöst wird oder nicht. |
| `\timing` | Schaltet die Anzeige ein und aus. Die Anzeige ist in Millisekunden. Intervalle, die länger als eine Sekunde sind, werden im Format Minuten:Sekunden angezeigt, wobei die Felder Stunden und Tage bei Bedarf hinzugefügt werden. |

Alle Befehle, die mit `\d` beginnen, können kombiniert werden. Sie können beispielsweise `\dtsn` ausgeben, um eine Liste aller Tabellen, Sequenzen und Schemata anzuzeigen. `\d` zeigt alle sichtbaren Tabellen, Ansichten, materialisierten Ansichten und Sequenzen.

Weitere Informationen zu den oben aufgeführten Befehlen finden Sie in der Dokumentation unter [postgreSQL.org](https://www.postgresql.org/docs/10/app-psql.html). Beachten Sie jedoch, dass nicht alle in der [!DNL PostgreSQL] Dokumentation aufgeführten Optionen von [!DNL Experience Platform] unterstützt werden.
