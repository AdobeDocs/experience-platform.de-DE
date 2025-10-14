---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;Abfragen schreiben;Abfrage schreiben;
solution: Experience Platform
title: Allgemeine Leitlinien für die Ausführung von Abfragen im Abfrage-Service
type: Tutorial
description: In diesem Dokument werden wichtige Informationen beschrieben, die Sie beim Schreiben von Abfragen in Adobe Experience Platform Query Service beachten sollten.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 4%

---

# Allgemeine Leitlinien für die Ausführung von Abfragen in [!DNL Query Service]

In diesem Dokument werden wichtige Informationen beschrieben, die Sie beim Schreiben von Abfragen in Adobe Experience Platform [!DNL Query Service] beachten sollten.

Ausführliche Informationen zur in [!DNL Query Service] verwendeten SQL-Syntax finden Sie in der [SQL-Syntax-Dokumentation](../sql/syntax.md).

## Abfrageausführungsmodelle

Adobe Experience Platform [!DNL Query Service] verfügt über zwei Modelle der Abfrageausführung: interaktiv und nicht interaktiv. Die interaktive Ausführung wird für die Abfrageentwicklung und die Berichterstellung in Business Intelligence-Tools verwendet, während die nicht interaktive Ausführung für größere Aufträge und operative Abfragen als Teil eines Datenverarbeitungs-Workflows verwendet wird.

### Interaktive Abfrageausführung

Abfragen können interaktiv ausgeführt werden, indem sie über die [!DNL Query Service]-Benutzeroberfläche oder [über einen verbundenen Client) gesendet &#x200B;](../clients/overview.md). Wenn [!DNL Query Service] über einen verbundenen Client ausgeführt wird, wird eine aktive Sitzung zwischen dem Client und [!DNL Query Service] ausgeführt, bis entweder die gesendete Abfrage zurückgegeben wird oder eine Zeitüberschreitung auftritt.

Die interaktive Ausführung von Abfragen hat die folgenden Einschränkungen:

| Parameter | Einschränkung |
| --------- | ---------- |
| Zeitüberschreitung der Abfrage | 10 Minuten |
| Maximal zurückgegebene Zeilen | 50.000 |
| Maximale Anzahl gleichzeitiger Abfragen | 5 |

>[!NOTE]
>
>Um die Begrenzung der maximalen Zeilen zu überschreiben, fügen Sie `LIMIT 0` in Ihre Abfrage ein. Die maximale Wartezeit von 10 Minuten für die Abfrage gilt weiterhin.

Standardmäßig werden die Ergebnisse interaktiver Abfragen an den Client zurückgegeben und **nicht** beibehalten. Um die Ergebnisse als Datensatz in [!DNL Experience Platform] beizubehalten, muss die Abfrage die `CREATE TABLE AS SELECT` Syntax verwenden.

### Nicht interaktive Abfrageausführung

Über die [!DNL Query Service]-API gesendete Abfragen werden nicht interaktiv ausgeführt. Eine nicht interaktive Ausführung bedeutet, dass [!DNL Query Service] den API-Aufruf erhält und die Abfrage in der Reihenfolge ausführt, in der sie empfangen wird. Nicht interaktive Abfragen führen immer entweder zur Generierung eines neuen Datensatzes, [!DNL Experience Platform] die Ergebnisse zu erhalten, oder zur Einfügung neuer Zeilen in einen vorhandenen Datensatz.

## Zugriff auf ein bestimmtes Feld innerhalb eines Objekts

Um auf ein Feld innerhalb eines Objekts in Ihrer Abfrage zuzugreifen, können Sie entweder die Punktnotation (`.`) oder die Klammernotation (`[]`) verwenden. Die folgende SQL-Anweisung verwendet Punktnotation, um das `endUserIds` Objekt bis zum `mcid` Objekt zu durchlaufen.

>[!NOTE]
>
>Die Experience Cloud ID (ECID) wird auch als MCID bezeichnet und weiterhin in Namespaces verwendet.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Der Name Ihrer Analytics-Tabelle. |

Die folgende SQL-Anweisung verwendet die Klammernotation, um das `endUserIds` Objekt bis zum `mcid` Objekt zu durchlaufen.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Der Name Ihrer Analytics-Tabelle. |

>[!NOTE]
>
>Da jeder Notierungstyp dieselben Ergebnisse zurückgibt, entspricht die von Ihnen gewählte Methode Ihren Vorlieben.

Beide obigen Beispielabfragen geben ein reduziertes Objekt anstelle eines einzelnen Werts zurück:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

Das zurückgegebene `endUserIds._experience.mcid`-Objekt enthält die entsprechenden Werte für die folgenden Parameter:

- `id`
- `namespace`
- `primary`

Wenn die Spalte nur für das -Objekt deklariert wird, wird das gesamte -Objekt als Zeichenfolge zurückgegeben. Um nur die ID anzuzeigen, verwenden Sie:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Anführungszeichen

Einfache Anführungszeichen, doppelte Anführungszeichen und rückwärtige Anführungszeichen werden in Abfragen des Abfrage-Service unterschiedlich verwendet.

### Einfache Anführungszeichen

Das einfache Anführungszeichen (`'`) wird verwendet, um Textzeichenfolgen zu erstellen. Beispielsweise kann sie in der `SELECT`-Anweisung verwendet werden, um einen statischen Textwert im Ergebnis zurückzugeben, und in der `WHERE`-Klausel, um den Inhalt einer Spalte auszuwerten.

Die folgende Abfrage deklariert einen statischen Textwert (`'datasetA'`) für eine Spalte:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Die folgende Abfrage verwendet eine Zeichenfolge in einfachen Anführungszeichen (`'homepage'`) in ihrer WHERE-Klausel, um Ereignisse für eine bestimmte Seite zurückzugeben.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

### Doppelte Anführungszeichen

Das doppelte Anführungszeichen (`"`) wird verwendet, um eine Kennung mit Leerzeichen zu deklarieren.

Die folgende Abfrage verwendet doppelte Anführungszeichen, um Werte aus angegebenen Spalten zurückzugeben, wenn eine Spalte ein Leerzeichen in ihrer Kennung enthält:

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>Doppelte Anführungszeichen **können nicht** mit der Punktnotation verwendet werden.

### Zurück Anführungszeichen

Die `` ` `` für rückwärts gerichtete Anführungszeichen wird verwendet, um reservierte Spaltennamen (nur **) bei** Verwendung der Punktnotation-Syntax mit Escape-Zeichen zu versehen. Da `order` beispielsweise ein reserviertes Wort in SQL ist, müssen Sie für den Zugriff auf das Feld `commerce.order` Anführungszeichen verwenden:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Backquotes werden auch verwendet, um auf ein Feld zuzugreifen, das mit einer Zahl beginnt. Um beispielsweise auf die `30_day_value` zuzugreifen, müssten Sie die Notation „Zurück“ verwenden.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

Wenn Sie Klammernotation verwenden **sind** Anführungszeichen erforderlich.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## Anzeigen von Tabelleninformationen

Nachdem Sie eine Verbindung zum Abfrage-Service hergestellt haben, können Sie alle verfügbaren Tabellen in Experience Platform mit den Befehlen `\d` oder `SHOW TABLES` anzeigen.

### Standard-Tabellenansicht

Der Befehl `\d` zeigt die standardmäßige [!DNL PostgreSQL] für die Auflistung von Tabellen an. Nachfolgend finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Detaillierte Tabellenansicht

`SHOW TABLES` Befehl ist ein benutzerdefinierter Befehl, der detailliertere Informationen zu den Tabellen bereitstellt. Nachfolgend finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Schemainformationen

Um detailliertere Informationen über die Schemata in der Tabelle anzuzeigen, können Sie den Befehl `\d {TABLE_NAME}` verwenden, wobei `{TABLE_NAME}` der Name der Tabelle ist, deren Schemainformationen angezeigt werden sollen.

Das folgende Beispiel zeigt die Schemainformationen für die `luma_midvalues`, die durch Verwendung von `\d luma_midvalues` angezeigt würden:

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Darüber hinaus können Sie weitere Informationen zu einer bestimmten Spalte erhalten, indem Sie den Namen der Spalte an den Tabellennamen anhängen. Dies würde im Format `\d {TABLE_NAME}_{COLUMN}` geschrieben.

Das folgende Beispiel zeigt zusätzliche Informationen für die `web` Spalte und wird mithilfe des folgenden Befehls aufgerufen: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Datensätze verknüpfen

Sie können mehrere Datensätze verbinden, um Daten aus anderen Datensätzen in Ihre Abfrage aufzunehmen.

Das folgende Beispiel würde die beiden folgenden Datensätze (`your_analytics_table` und `custom_operating_system_lookup`) verbinden und eine `SELECT`-Anweisung für die 50 wichtigsten Betriebssysteme nach Anzahl der Seitenansichten erstellen.

**Abfrage**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**Ergebnisse**

| Betriebssystem | Seitenansichten |
| --------------- | --------- |
| Windows 7 | 2781979,0 |
| Windows XP | 1669824,0 |
| Windows 8 | 420024,0 |
| Adobe AIR | 315032,0 |
| Windows Vista | 173566,0 |
| Mobile iOS 6.1.3 | 119069,0 |
| Linux | 56516,0 |
| OSX 10.6.8 | 53652,0 |
| Android 4.0.4 | 46167,0 |
| Android 4.0.3 | 31852,0 |
| Windows Server 2003 und XP x64 Edition | 28883,0 |
| Android 4.1.1 | 24336,0 |
| Android 2.3.6 | 15735,0 |
| OSX 10.6 | 13357,0 |
| Windows Phone 7.5 | 11054,0 |
| Android 4.3 | 9221,0 |

## Deduplizierung

Der Abfrage-Service unterstützt die Datendeduplizierung oder das Entfernen doppelter Zeilen aus Daten. Weitere Informationen zur Deduplizierung finden Sie im [Handbuch zur Deduplizierung des Abfrage-Service](../key-concepts/deduplication.md).

## Zeitzonenberechnungen im Abfrage-Service

Query Service standardisiert persistierte Daten in Adobe Experience Platform mithilfe des UTC-Zeitstempelformats. Weitere Informationen zur Übersetzung Ihrer Zeitzonenanforderungen in und aus einem UTC-Zeitstempel finden Sie im [FAQ-Abschnitt zum Ändern der Zeitzone in und von einem UTC-Zeitstempel](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## Nächste Schritte

In diesem Dokument haben Sie eine Einleitung zu wichtigen Überlegungen beim Schreiben von Abfragen mit [!DNL Query Service] erhalten. Weitere Informationen zur Verwendung der SQL-Syntax zum Schreiben eigener Abfragen finden Sie in der [SQL-Syntax-Dokumentation](../sql/syntax.md).

Weitere Beispiele für Abfragen, die im Abfrage-Service verwendet werden können, finden Sie in der Dokumentation zu folgenden Anwendungsfällen:

- [Analytics Insights](../use-cases/analytics-insights.md)
- [Erstellen eines Trendberichts mit Ereignissen](../use-cases/trended-report-of-events.md)
- [Anzeigen eines Datenaggregationsberichts eines Besuchers](../use-cases/roll-up-report-of-a-visitor.md)
- [Auflisten der Seitenansichten von Benutzenden](../use-cases/list-visitor-sessions.md)
- [Besuchende nach Anzahl der Seitenansichten auflisten](../use-cases/visitors-by-number-of-page-views.md)
