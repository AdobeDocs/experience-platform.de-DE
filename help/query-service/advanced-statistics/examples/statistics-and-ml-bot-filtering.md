---
title: Bot-Filterung mithilfe von Statistiken und maschinellem Lernen
description: Erfahren Sie, wie Sie mit Data Distiller-Statistiken und maschinellem Lernen Bot-Aktivitäten identifizieren und filtern können, um genaue Analysen und eine verbesserte Datenintegrität sicherzustellen.
exl-id: 30d98281-7d15-47a6-b365-3baa07356010
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# Bot-Filterung mithilfe von Statistiken und maschinellem Lernen

Die praktischen Anwendungen der Bot-Filterung erstrecken sich über verschiedene Branchen. Im E-Commerce wird die Zuverlässigkeit von Konversionsratenmetriken verbessert, Nachrichten-Websites können von der Verringerung falscher Interaktionsmetriken profitieren, und Werbenetzwerke können eine faire Abrechnung sicherstellen. Um eine genaue Analyse zu gewährleisten und die Datenintegrität in Clickstream- oder Web-Traffic-Daten sicherzustellen, müssen Sie sich mit beiden Aktivitäten befassen. Sie können hochwertige Analysedaten sicherstellen, indem Sie Data Distiller verwenden, um eine effektive Bot-Filterung zu implementieren und unerwünschten Traffic zu vermeiden.

Dieses Dokument enthält eine umfassende Anleitung zum Identifizieren und Filtern von Bot-Aktivitäten mithilfe von SQL- und maschinellen Lerntechniken. Es stellt eine Reihe komplementärer Ansätze vor, angefangen bei der grundlegenden Filterung bis hin zur Erkennung und Auswertung durch maschinelles Lernen. Nutzen Sie dieses robuste Framework, um die Bot-Erkennung zu verbessern und die Integrität Ihrer Daten zu wahren.

## Bot-Aktivität verstehen {#understand-bot-activity}

Bot-Aktivitäten können identifiziert werden, indem Spitzen bei Benutzeraktionen innerhalb bestimmter Zeitintervalle erkannt werden. Beispielsweise könnten übermäßige Klicks, die ein einzelner Benutzer innerhalb eines kurzen Zeitraums ausführt, auf das Verhalten beider Benutzer hindeuten. Die beiden Schlüsselattribute, die bei der Filterung verwendet werden, sind:

- **ECID (Experience Cloud-Besucher-ID):** Eine universelle, beständige ID, die Besuchende identifiziert.
- **Zeitstempel:** Uhrzeit und Datum, an dem eine Aktivität auf der Website stattfindet.

Die folgenden Beispiele zeigen, wie Sie mit SQL- und maschinellen Lerntechniken Bot-Aktivitäten identifizieren, verfeinern und vorhersagen können. Verwenden Sie diese Methoden, um die Integrität Ihrer Daten zu verbessern und umsetzbare Analysen sicherzustellen.

## SQL-basierte Bot-Filterung {#sql-based-bot-filtering}

Dieses SQL-basierte Bot-Filterbeispiel zeigt, wie SQL-Abfragen verwendet werden, um Schwellenwerte zu definieren und Bot-Aktivitäten anhand vordefinierter Regeln zu erkennen. Dieser grundlegende Ansatz hilft bei der Identifizierung von Anomalien im Web-Traffic, indem ungewöhnliche Aktivitäten entfernt werden. Durch die Anpassung der Erkennungsregeln mit definierten Schwellenwerten und Intervallen können Sie die Bot-Filterung effektiv an Ihre spezifischen Traffic-Muster anpassen.

### Definieren von Schwellenwerten für Bot-Aktivitäten {#define-thresholds}

Analysieren Sie zunächst Ihren Datensatz, um das Benutzerverhalten zu identifizieren und zu kategorisieren. Konzentrieren Sie sich auf Attribute wie ECID, Zeitstempel und `webPageDetails.name` (den Namen der besuchten Web-Seite), um Benutzeraktionen zu gruppieren und Muster zu erkennen, die auf Bot-Aktivitäten hinweisen.

Die folgende SQL-Abfrage zeigt, wie Sie den Schwellenwert von mehr als 60 Klicks in einer Minute anwenden können, um verdächtige Aktivitäten zu identifizieren:

```sql
SELECT *
FROM analytics_events_table
WHERE enduserids._experience.ecid NOT IN (
    SELECT enduserids._experience.ecid
    FROM analytics_events_table
    GROUP BY Unix_timestamp(timestamp) / 60, enduserids._experience.ecid
    HAVING Count(*) > 60
);
```

### Auf mehrere Intervalle erweitern {#expand-to-multiple-intervals}

Definieren Sie anschließend verschiedene Zeitintervalle für Schwellenwerte. Diese Intervalle können Folgendes umfassen:

- **1-Minuten-Intervall** Bis zu 60 Klicks.
- **5-Minuten-Intervall** Bis zu 300 Klicks.
- **30-Minuten-Intervall** Bis zu 1800 Klicks.

Die folgende SQL-Abfrage erstellt eine Ansicht mit dem Namen `analytics_events_clicks_count_criteria`, um Schwellenwerte über mehrere Intervalle hinweg zu verarbeiten. Die Anweisung fasst Klickzahlen für 1-, 5- und 30-Minuten-Intervalle in einem strukturierten Datensatz zusammen und kennzeichnet potenzielle Bot-Aktivitäten auf der Grundlage vordefinierter Schwellenwerte.

```sql
CREATE VIEW analytics_events_clicks_count_criteria as  
SELECT struct (
        cast(count_1_min AS int) one_minute,
        cast(count_5_mins AS int) five_minute,
        cast(count_30_mins AS int) thirty_minute
       ) count_per_id,
       id,
      struct (
        struct (name) webpagedetails
      ) web,
      CASE
        WHEN count.one_minute > 50 THEN 1
        ELSE 0
      END AS isBot
FROM (
  SELECT table_count_1_min.mcid AS id,
         count_1_min,
         count_5_mins,
         count_30_mins,
         table_count_1_min.name AS name
  FROM (
      (SELECT mcid, Max(count_1_min) AS count_1_min, name
       FROM (SELECT enduserids._experience.mcid.id AS mcid,
                    Count(*) AS count_1_min,
                    web.webPageDetails.name AS name
             FROM delta_table
             WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                               AND TO_TIMESTAMP('2019-09-01 23:00:00')
             GROUP BY UNIX_TIMESTAMP(timestamp) / 60,
                      enduserids._experience.mcid.id,
                      web.webPageDetails.name)
       GROUP BY mcid, name) AS table_count_1_min
       LEFT JOIN
       (SELECT mcid, Max(count_5_mins) AS count_5_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_5_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 300,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_5_mins
       ON table_count_1_min.mcid = table_count_5_mins.mcid
       LEFT JOIN
       (SELECT mcid, Max(count_30_mins) AS count_30_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_30_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 1800,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_30_mins
       ON table_count_1_min.mcid = table_count_30_mins.mcid
  )
)
```

Die Anweisung verknüpft Daten aus `table_count_1_min`, `table_count_5_mins` und `table_count_30_mins` mithilfe des `mcid` und der Webseite. Anschließend werden die Klickzahlen für jeden Benutzer über mehrere Zeitintervalle hinweg zusammengefasst, um einen vollständigen Überblick über die Benutzeraktivität zu erhalten. Schließlich identifiziert die Flagging-Logik dann Benutzer, die 50 Klicks in einer Minute überschreiten, und markiert sie als Bots (`isBot = 1`).

### Struktur des Ausgabedatensatzes

Der Ausgabedatensatz ist mit flachen und verschachtelten Feldern strukturiert. Diese Struktur ermöglicht Flexibilität bei der Erkennung von anomalem Traffic und unterstützt erweiterte Filterstrategien, die SQL und maschinelles Lernen verwenden. Die verschachtelten Felder enthalten `count` und `web`, in denen granulare Details zu Aktivitätsschwellen und Web-Seiten eingekapselt sind. Die Erfassung dieser Metriken bedeutet, dass Funktionen für Trainings- und Prognoseaufgaben einfach extrahiert werden können.

Das folgende Schemadiagramm skizziert die Struktur des resultierenden Datensatzes und hebt hervor, wie verschachtelte und flache Felder für eine effiziente Verarbeitung und Bot-Erkennung verwendet werden können.

```console
root
 |-- count: struct (nullable = false)
 |    |-- one_minute: integer (nullable = true)
 |    |-- five_minute: integer (nullable = true)
 |    |-- thirty_minute: integer (nullable = true)
 |-- id: string (nullable = true)
 |-- web: struct (nullable = false)
 |    |-- webpagedetails: struct (nullable = false)
 |    |    |-- name: string (nullable = true)
 |-- isBot: integer (nullable = false)
```

### Der für das Training zu verwendende Ausgabedatensatz

Das Ergebnis dieses Ausdrucks könnte der unten angegebenen Tabelle ähneln. In der Tabelle dient die Spalte `isBot` als Bezeichnung, die zwischen Bot- und Nicht-Bot-Aktivität unterscheidet.

```console
| `id`         | `count_per_id`                                      |`isBot`| `web`                                                                                                                    |
|--------------|-----------------------------------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":99}| 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 1E+18        | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
| 1.00007E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"8DN0dM4rlvJxt4oByYLKZ/wuHyq/8CvsWNyXvGYnImytXn/bjUizfRSl86vmju7MFMXxnhTBoCWLHtyVSWro9LYg0MhN8jGbswLRLXoOIyh2wduVbc9XeN8yyQElkJm3AW3zcqC7iXNVv2eBS8vwGg=="}} |
| 1.00008E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
```

## Erweiterte statistische Funktionen für die Bot-Filterung {#statistical-functions-for-bot-filtering}

Dieses zweite Beispiel baut auf der grundlegenden SQL-Filterung auf, indem maschinelle Lerntechniken integriert werden, um Schwellenwerte zu verfeinern und die Filtergenauigkeit zu verbessern. Durch die Verwendung erweiterter statistischer Funktionen wie Regressionsanalyse oder Clustering-Algorithmen bietet dieser Ansatz prädiktive Funktionen, mit denen Sie Modelle zur präziseren Verarbeitung komplexer Datensätze entwickeln können.

### Erstellen eines Trainings-Datensatzes {#build-a-training-dataset}

Bereiten Sie zunächst einen Datensatz mit flachen und verschachtelten Strukturen vor, die das Modell für maschinelles Lernen verwenden kann (wie oben beschrieben). Weitere Anleitungen dazu finden Sie in der Dokumentation [Arbeiten mit verschachtelten Datenstrukturen](../../key-concepts/nested-data-structures.md). Gruppieren Sie die Daten nach Zeitstempel, Benutzer-ID und Webseitenname, um Muster in beiden Aktivitäten zu identifizieren.

### Verwenden von TRANSFORM- und OPTIONS-Klauseln für die Modellerstellung {#transform-and-preprocess}

Gehen Sie wie folgt vor, um Ihren Datensatz zu transformieren und Ihr Modell für maschinelles Lernen effektiv zu konfigurieren. Die Schritte beschreiben, wie Nullwerte verarbeitet, Funktionen vorbereitet und die Parameter des Modells für eine optimale Leistung definiert werden.

>[!TIP]
>
>Weitere Informationen zur Verwendung von Umwandlungen und zur Vorverarbeitung Ihrer Daten finden Sie in der [Dokumentation zu Funktionstransformationstechniken](../feature-transformation.md).

1. Verwenden Sie zum Ausfüllen von Nullwerten in numerischen, String- und booleschen Spalten die Funktionen `numeric_imputer`, `string_imputer` bzw. `boolean_imputer`. Dieser Schritt stellt sicher, dass der Algorithmus für maschinelles Lernen die Daten fehlerfrei verarbeiten kann.
2. Wenden Sie Elementtransformationen an, um die Daten für die Modellierung vorzubereiten. Wenden Sie `binarized`, `quantile_discretizer` oder `string_indexer` an, um die Spalten zu kategorisieren oder zu standardisieren. Führen Sie anschließend die Ausgabe der Computer (`numeric_imputer` und `string_imputer`) in nachfolgende Transformatoren wie `string_indexer` oder `quantile_discretizer` ein, um aussagekräftige Funktionen zu erstellen.
3. Verwenden Sie die Funktion `vector_assembler` , um die umgewandelten Spalten zu einer einzigen Elementspalte zu kombinieren. Skalieren Sie dann die Funktionen mithilfe von `min_max_scaler`, um die Werte zu normalisieren und so die Modellleistung zu verbessern. Hinweis: Im SQL-Beispiel wird die letzte Transformation, die in der TRANSFORM-Klausel erwähnt wird, zur Funktionsspalte, die vom Modell für maschinelles Lernen verwendet wird.
4. Geben Sie den Modelltyp und alle anderen Hyperparameter in der OPTIONS-Klausel an. Hier wurde beispielsweise `decision_tree_classifier` ausgewählt, da es sich um ein Klassifizierungsproblem handelt. Andere Parameter wie `max_depth` wurden angepasst (`MAX_DEPTH=4`), um das Modell für eine bessere Leistung abzustimmen.
5. Kombinieren Sie Funktionen und beschriften Sie die Ausgabedaten. Verwenden Sie die SELECT-Klausel, um den Datensatz für das Training anzugeben. Diese Klausel sollte sowohl die Funktionsspalten (`count_per_id`, `web`, `id`) als auch die Bezeichnungsspalte (`isBot`) enthalten, die angibt, ob eine Aktion wahrscheinlich ein Bot ist.

Ihre Anweisung könnte dem folgenden Beispiel ähneln.

```sql
CREATE MODEL bot_filtering_model
TRANSFORM (
  numeric_imputer(count_per_id.one_minute, 'mean') imputed_one_minute,
  numeric_imputer(count_per_id.five_minute, 'mode') imputed_five_minute,
  numeric_imputer(count_per_id.thirty_minute) imputed_thirty_minute,
  string_imputer(id, 'unknown') imputed_id,
  string_indexer(imputed_id) si_id,
  quantile_discretizer(imputed_five_minute) buckets_five,
  string_indexer(web.webpagedetails.NAME) si_name,
  quantile_discretizer(imputed_thirty_minute) buckets_thirty,
  vector_assembler(array(si_id, imputed_one_minute, buckets_five, si_name, buckets_thirty)) features,
  min_max_scaler(features) scaled_features
)
OPTIONS (model_type='decision_tree_classifier', max_depth=4, label='isBot')
AS
SELECT count_per_id, isBot, web, id FROM analytics_events_clicks_count_criteria;
```

**Ergebnis**

In den unten angezeigten Ergebnissen wird der `bot_filtering_model` mit einer eindeutigen ID, einem eindeutigen Namen und einer eindeutigen Version erstellt. Diese Ausgabe dient als Referenz für das Tracking und die Verwaltung von Modellen. Verwenden Sie diese Verweise, um die genaue Konfiguration und Version zu ermitteln, die für Prognosen oder Auswertungen erforderlich sind.

```console
           Created Model ID           |       Created Model       | Version
|--------------------------------------+---------------------------+---------
 2fb4b49e-d35c-44cf-af19-cc210e7dc72c | bot_filtering_model       |       1
```

### Trainiertes Modell auswerten {#evaluate-trained-model}

Nachdem Sie das Modell erstellt haben, verwenden Sie den Befehl `MODEL_EVALUATE` , um dessen Leistung zu bewerten. Dieser Schritt stellt sicher, dass das Modell die Genauigkeits- und Leistungsanforderungen zur Erkennung von Bot-Aktivitäten erfüllt.

Verwenden Sie die folgenden Argumente in Ihrem SQL-Befehl, um das Modell auszuwerten:

1. Geben Sie den Modellnamen (`bot_filtering_model`) an, um anzugeben, welches Modell ausgewertet werden soll. Dieser Name muss mit dem Namen übereinstimmen, den Sie zuvor mit dem Befehl `CREATE MODEL` erstellt haben.
2. Geben Sie die Modellversion (`1`) im zweiten Argument an, um die Version des Modells anzugeben, das Sie auswerten möchten. Wenn mehrere Versionen vorhanden sind, wird sichergestellt, dass die richtige Version verwendet wird.
3. Schließen Sie den Auswertungsdatensatz ein, um den Datensatz für die Auswertung zu definieren. Stellen Sie sicher, dass der Datensatz dieselben Funktionsspalten (`count_per_id`, `web`, `id`) und die Beschriftungsspalte (`isBot`) enthält, die beim Training verwendet wurden.

>[!NOTE]
>
>Die beim Modell-Training angewendeten Transformationen werden während der Auswertung automatisch angewendet.

```sql
SELECT *
FROM   model_evaluate(bot_filtering_model, 1,
                      SELECT count_per_id, isBot, web, id
                      FROM   analytics_events_clicks_count_criteria);
```

**Ergebnis**

Die Antwort enthält Metriken wie Genauigkeit, Präzision, Rückruf und AUC-ROC. Die Ergebnisse bestätigen, ob das Modell eine gute Leistung erzielt hat.

>[!NOTE]
>
>Werte im Bereich von 0-1 stellen Proportionen oder Wahrscheinlichkeiten dar, wobei 1,0 die perfekte Leistung angibt.

```console
auc_roc | accuracy | precision | recall
|---------+----------+-----------+--------
     1.0 |      1.0 |       1.0 |    1.0
```

| **Metrik** | **Beschreibung** |
|--------------|-----------------------------------------------------------------------------------------------------|
| `auc_roc` | Diese Metrik gibt an, wie effektiv Ihr Modell Bots und Nicht-Bots klassifizieren kann. Sie wird häufig für die Bewertung von Klassifizierungsmodellen verwendet. |
| `accuracy` | Der Prozentsatz der richtigen Prognosen, die vom Modell gemacht wurden. |
| `precision` | Der Anteil der wahren Bot-Vorhersagen unter allen prognostizierten Bots. |
| `recall` | Der Anteil der echten Bots, der von allen tatsächlichen Bots erkannt wurde. |

>[!TIP]
>
>Zur Verwendung in Produktions-Sandboxes sollten Sie das Modell mit Testdatensätzen evaluieren, um sicherzustellen, dass es effektiv generalisiert wird.

### Bot-Aktivität vorhersagen {#predict-bot-activity}

Verwenden Sie den `MODEL_PREDICT`-Befehl mit dem trainierten Modell, um zu ermitteln, welche Benutzer (`id`) Bots sind. Gehen Sie wie folgt vor, um Prognosen zur Identifizierung der Bot-Aktivität zu generieren:

1. Verwenden Sie den Modellnamen (`bot_filtering_model`) im ersten Argument, um anzugeben, welches Modell für Prognosen verwendet werden soll.
2. Geben Sie die Modellversion (`1`) im zweiten Argument an, um sicherzustellen, dass die richtige Version des Modells verwendet wird.
3. Um die richtigen Daten für Prognosen bereitzustellen, verwenden Sie eine SELECT-Anweisung, um die Funktionsspalten (`count_per_id`, `web`, `id`) anzugeben. Binden Sie die Titelspalte (`isBot`) nicht ein, da das Modell Prognosen für dieses Feld generieren wird.

```sql
SELECT *
FROM model_predict(bot_filtering_model, 1,
    SELECT count_per_id, web, id FROM analytics_events_clicks_count_criteria
);
```

**Ergebnis**

Die Antwort enthält Prognosen für jeden Benutzer (`id`) sowie Details zu seiner Aktivität und dem Klassifizierungsergebnis des Modells. Diese Ausgabe ermöglicht eine detaillierte Untersuchung des Benutzerverhaltens und der Klassifizierung der Bot-Aktivität durch das Modell.

<!-- Q) Anil, why is there no ID in the first two rows? Can we get that info? Or should it be the same as the other IDs? -->

```console
         id          | count.one_minute | count.five_minute | count.thirty_minute |                                                                  web.webpagedetails.name                                                                  | prediction
|---------------------+------------------+-------------------+---------------------+-------+----------------------------------------------------------------------------------------------------------------------------------------------------+------------
                     |              110 |                   |                     |   4UNDilcY5VAgu2pRmX4/gtVnj+YxDDQaJd1G8p8WX46//wYcrHy+APUN0I556E80j1gIzFmilA6DV4s0Zcs4ruiP36gLgC7bj4TH0q6LU0E=                                             |        1.0  
                     |              105 |                   |                     |   lrSaZk04Yq+5P9+6l4BohwXik0s0/XeW9X28ZgWt1yj1QQztiAt9Qgt2WYrWcAeoGZChAJw/l8e4ojZDT5WHCjteSt35S01Vv1JzDGPAg+IyhIzMTsVyLpW8WWpXjJoMCt6Tv7fFdF73EIH+IrK5fA== |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
```

In der folgenden Tabelle werden die einzelnen Metriken erläutert:

| Spaltenname | Beschreibung |
|---------------------------|----------------------------------------------------------------------------------------------------------|
| `id` | Die eindeutige Kennung für jeden Benutzer. |
| `count.one_minute` | Die aggregierten Klickzahlen für 1-Minuten-Intervalle. |
| `count.five_minute` | Die aggregierten Klickzahlen für 5-Minuten-Intervalle. |
| `count.thirty_minute` | Die aggregierte Klickanzahl beträgt 30-Minuten-Intervalle. |
| `web.webpagedetails.name` | Der Name der besuchten Webseite. Dies bietet den Kontext für Benutzeraktivitäten. |
| `prediction` | Die Prognose des Modells. Ein `1.0` Ergebnis zeigt an, dass der Benutzer basierend auf seinen Aktivitätsmustern als Bot gekennzeichnet wird. |

## Modelle verwalten {#manage-models}

Verwenden Sie die im folgenden Abschnitt aufgeführten SQL-Schlüsselwörter, um Ihre Modelle für maschinelles Lernen zu verwalten.

### Verfügbare Modelle auflisten {#list-available-models}

Verwalten und überprüfen Sie die Modelle effizient mit dem Befehl `SHOW MODELS;` . Dieser Befehl listet alle Modelle für maschinelles Lernen auf, die im aktuellen Arbeitsbereich erstellt wurden. Die Ausgabe bietet einen Überblick über die verfügbaren Modelle und enthält deren Namen, Versionen und andere Metadaten.

```sql
SHOW MODELS;
```

### Modelle löschen {#delete-models}

Um Ressourcen freizugeben und sicherzustellen, dass nur relevante Modelle gepflegt werden, verwenden Sie den Befehl `DROP MODEL` , um veraltete oder unnötige Modelle zu entfernen. Dieser Befehl löscht alle Modelle für maschinelles Lernen, die nach den Schlüsselwörtern angegeben wurden. Im folgenden Beispiel wird die `bot_filtering_model` aus dem System entfernt.

```sql
DROP MODEL bot_filtering_model;
```

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie sowohl -Aktivitäten mithilfe von SQL- als auch maschinelle Lerntechniken mithilfe von Data Distiller-Methoden identifizieren und filtern können. Wenden Sie diese Konzepte anschließend auf Ihre Datensätze an und automatisieren Sie die Modellneuerziehung zur kontinuierlichen Verbesserung.
