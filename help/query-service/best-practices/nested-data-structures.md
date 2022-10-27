---
keywords: Experience Platform; Query Service; Query Service; verschachtelte Datenstrukturen; verschachtelte Daten;
title: Arbeiten mit verschachtelten Datenstrukturen in Query Service
description: Dieses Dokument bietet ein Arbeitsbeispiel für die Verarbeitung und Transformation verschachtelter Datenfelder mithilfe von CTAS- und INSERT INTO-Anweisungen.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 2%

---

# Arbeiten mit verschachtelten Datenstrukturen in Query Service

Adobe Experience Platform Query Service unterstützt die Verwendung verschachtelter Datenfelder. Die Komplexität der Datenstrukturen eines Unternehmens kann die Umwandlung oder Verarbeitung dieser Daten erschweren. Dieses Dokument enthält Beispiele zum Erstellen, Verarbeiten oder Transformieren von Datensätzen mit komplexen Datentypen, einschließlich verschachtelter Datenstrukturen.

Query Service stellt eine [!DNL PostgreSQL] -Schnittstelle zum Ausführen von SQL-Abfragen für alle von Experience Platform verwalteten Datensätze. Platform unterstützt die Verwendung von primitiven oder komplexen Datentypen in Tabellenspalten wie Struktur, Arrays, Karten und tief verschachtelten Strukturen, Arrays und Maps. Datensätze können auch verschachtelte Strukturen enthalten, bei denen der Spaltendatentyp so komplex sein kann wie ein Array verschachtelter Strukturen oder eine Zuordnung von Karten, wobei der Wert eines Schlüssel-Wert-Paares eine Struktur mit mehreren Verschachtelungsebenen sein kann.

## Erste Schritte

Für dieses Tutorial ist die Verwendung eines PSQL-Clients eines Drittanbieters oder des Abfrage-Editors erforderlich, um Abfragen in der Experience Platform-Benutzeroberfläche (UI) zu schreiben, zu validieren und auszuführen. Ausführliche Informationen zum Ausführen von Abfragen über die Benutzeroberfläche finden Sie im Abschnitt [Anleitung zur Benutzeroberfläche des Abfrage-Editors](../ui/user-guide.md). Eine detaillierte Liste der Desktop-Clients von Drittanbietern, die eine Verbindung zu Query Service herstellen können, finden Sie unter [Übersicht über Client-Verbindungen](../clients/overview.md).

Sie sollten auch ein gutes Verständnis der `INSERT INTO` und `CTAS` Syntax. Spezifische Informationen zu ihrer Verwendung finden Sie im [`INSERT INTO`](../sql/syntax.md#insert-into) und [`CTAS`](../sql/syntax.md#create-table-as-select) der [Referenzdokumentation zur SQL-Syntax](../sql/syntax.md).

## Erstellen eines Datensatzes

Der Query-Dienst stellt Tabelle als Auswahl erstellen (`CTAS`) verwenden, um eine Tabelle basierend auf der Ausgabe eines `SELECT` -Anweisung oder wie in diesem Fall durch Verwendung eines Verweises auf ein vorhandenes XDM-Schema in Adobe Experience Platform. Im Folgenden wird das XDM-Schema für `Final_subscription` für dieses Beispiel erstellt wurde.

![Ein Diagramm des Schemas final_subscription .](../images/best-practices/final-subscription-schema.png)

Das folgende Beispiel zeigt die SQL, die zum Erstellen der `final_subscription_test2` Datensatz. `final_subscription_test2` wird mithilfe der `Final_subscription` Schema. Die Daten werden mithilfe einer `SELECT` -Klausel, um einige Zeilen zu füllen.

```sql
CREATE TABLE final_subscription_test2 with(schema='Final_subscription') AS (
        SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM (
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

Im ursprünglichen Datensatz `final_subscription_test2`, wird der strukturierte Datentyp verwendet, um beide `subscription` und `userid` die für jeden Benutzer eindeutig ist. Die `subscription` -Feld beschreibt die Produktanmeldungen für einen Benutzer. Es kann mehrere Abonnements geben, eine Tabelle kann jedoch nur die Informationen für ein Abonnement pro Zeile enthalten.

## Verwenden Sie &quot;EINFÜGEN IN&quot;, um verschachtelte Datenfelder zu aktualisieren

Nach dem `final_subscription_test2` -Datensatz erstellt wurde, wird die `INSERT INTO` -Anweisung wird verwendet, um zusätzliche Daten an die Tabelle anzuhängen. Beim Kopieren von Daten müssen die Datentypen in Quelle und Ziel übereinstimmen. Alternativ kann der Quelldatentyp `CAST` zum Zieldatentyp hinzugefügt. Die inkrementellen Daten werden dann mithilfe der folgenden SQL zum Zieldatensatz hinzugefügt.

```sql
INSERT INTO final_subscription_test
      SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM  SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , timestamp eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

## Daten aus einem verschachtelten Datensatz verarbeiten

Um die Liste der aktiven Abonnements eines Benutzers aus einem Datensatz herauszufinden, müssen Sie eine Abfrage schreiben, die die Elemente eines Arrays in mehrere Zeilen und Spalten aufteilt. Dazu müssen Sie zunächst die Form des Datenmodells verstehen, da die Abonnementinformationen in einem innerhalb des Datensatzes verschachtelten Array aufbewahrt werden.

PSQL `\d` -Befehl wird verwendet, um von Ebene zu Ebene zu den erforderlichen Abonnementdaten zu navigieren. Die Tabellen veranschaulichen die Struktur der `final_subscription_test2` Datensatz. Komplexe Datentypen können auf einen Blick erkannt werden, da es sich nicht um typische Typwerte wie Text, boolescher Wert, Zeitstempel usw. handelt.

| Spalte | Typ |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

Die Felder der nächsten Spalte werden mithilfe der Variablen `\d final_subscription_test2__lumaservices3` Befehl.

| Spalte | Typ |
|---------|-------|
| `userid` | text |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` ist ein Array von Strukturelementen. Die Felder werden mithilfe der Variablen `\d _lumaservices3_subscription_e[]` Befehl.

| Spalte | Typ |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | text |
| `offer_id` | text |
| `subscription_id` | text |

Um die verschachtelten Felder des Abonnements abzufragen, müssen Sie zunächst die Elemente der `subscription` -Array in mehrere Zeilen einschließen und die Ergebnisse mithilfe der Explode-Funktion zurückgeben. Das folgende SQL-Beispiel gibt das aktive Abonnement für einen Benutzer basierend auf `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

Diese vereinfachte Beispiellösung ermöglicht nur ein aktives Benutzerabonnement. Realistisch betrachtet kann es viele aktive Abonnements für einen einzelnen Benutzer geben. Im folgenden Beispiel wird die vorherige Abfrage geändert, um mehrere gleichzeitige aktive Abonnements zu ermöglichen.

```sql
SELECT userid, collect_list(subs) AS active_subscriptions FROM (
     SELECT
          _lumaservices3.userid AS userid,
          explode(_lumaservices3.subscription) AS subs
     FROM final_subscription_test2
     )
WHERE subs.last_status='Active' 
GROUP BY userid ;
```

Trotz der zunehmenden Komplexität dieses SQL-Beispiels wird die `collect_list` für aktive Abonnements nicht garantieren, dass die Ausgabe in derselben Reihenfolge wie die Quelle erfolgt. Um eine Liste aktiver Abonnements für einen Benutzer zu erstellen, müssen Sie GROUP BY oder shuffling verwenden, um die Ergebnisse der Liste zu aggregieren.

## Nächste Schritte

Durch Lesen dieses Dokuments wissen Sie jetzt, wie Sie Datensätze verarbeiten oder transformieren können, die komplexe Datentypen in Adobe Experience Platform Query Service verwenden. Siehe [Ausführungsleitfaden für Abfragen](./writing-queries.md) für weitere Informationen zum Ausführen von SQL-Abfragen für Datensätze im Data Lake.
