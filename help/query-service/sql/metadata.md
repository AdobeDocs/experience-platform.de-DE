---
keywords: Experience Platform;Home;beliebte Themen;PSQL;psql;Abfrage-Dienst;Abfrage-Dienst;Metadaten;Befehle;Metadaten-Befehle
solution: Experience Platform
title: Metadaten-PostgreSQL-Befehle im Abfrage-Dienst
topic-legacy: metadata
description: Eine Liste von PostgreSQL-Befehlen, die derzeit für die Abfrage von Metadaten im Adobe Experience Platform Abfrage Service unterstützt werden.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Metadaten-PostgreSQL-Befehle im Abfrage-Dienst

Für Metadaten in Ihrem Datensatz werden derzeit die folgenden PostgreSQL-Befehle zum Abfragen unterstützt:

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

Alle Befehle, die mit `\d` Beginn werden, können kombiniert werden. Beispielsweise können Sie `\dtsn` ausgeben, um eine Liste aller Tabellen, Sequenzen und Schema anzuzeigen. `\d` zeigt alle sichtbaren Tabellen, Ansichten, materialisierten Ansichten und Sequenzen an.

Weitere Informationen zu den oben aufgeführten Befehlen finden Sie in der Dokumentation unter [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Beachten Sie jedoch, dass nicht alle in der PostgreSQL-Dokumentation angezeigten Optionen von [!DNL Experience Platform] unterstützt werden.
