---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Schreiben von Abfragen;Schreiben von Abfrage;
solution: Experience Platform
title: Allgemeine Leitlinien für die Ausführung von Abfragen im Dienst Abfrage
topic-legacy: queries
type: Tutorial
description: In diesem Dokument werden wichtige Informationen zum Schreiben von Abfragen im Adobe Experience Platform Abfrage Service beschrieben.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 3%

---

# Allgemeine Anleitung zur Ausführung von Abfragen in [!DNL Query Service]

In diesem Dokument werden wichtige Informationen zum Schreiben von Abfragen in Adobe Experience Platform beschrieben.[!DNL Query Service]

Ausführliche Informationen zur SQL-Syntax, die in [!DNL Query Service] verwendet wird, finden Sie in der [SQL-Syntaxdokumentation](../sql/syntax.md).

## Ausführungsmodelle für Abfragen

Adobe Experience Platform [!DNL Query Service] verfügt über zwei Ausführungsmodelle der Abfrage: interaktiv und nicht interaktiv. Die interaktive Ausführung wird für die Entwicklung von Abfragen und die Erstellung von Berichten in Business Intelligence-Tools verwendet, während nicht interaktive Anwendungen für größere Aufträge und operative Abfragen als Teil eines Datenverarbeitungs-Workflows verwendet werden.

### Ausführung interaktiver Abfragen

Abfragen können interaktiv ausgeführt werden, indem sie über die [!DNL Query Service]-Benutzeroberfläche oder [über einen angeschlossenen Client](../clients/overview.md) gesendet werden. Wenn [!DNL Query Service] über einen angeschlossenen Client ausgeführt wird, wird eine aktive Sitzung zwischen dem Client und [!DNL Query Service] ausgeführt, bis entweder die gesendete Abfrage zurückgegeben wird oder eine Zeitüberschreitung eintritt.

Die Ausführung interaktiver Abfragen unterliegt folgenden Einschränkungen:

| Parameter | Einschränkung |
| --------- | ---------- |
| Abfrage-Timeout | 10 Minuten |
| Maximale Zeilenanzahl | 50.000 |
| Maximale gleichzeitige Abfragen | 5 |

>[!NOTE]
>
>Um die maximale Zeilenbeschränkung zu überschreiben, fügen Sie `LIMIT 0` in Ihre Abfrage ein. Die Zeitüberschreitung der Abfrage von 10 Minuten ist weiterhin gültig.

Standardmäßig werden die Ergebnisse interaktiver Abfragen an den Client zurückgegeben und bleiben **nicht** erhalten. Um die Ergebnisse als Datensatz in [!DNL Experience Platform] zu erhalten, muss die Abfrage die Syntax `CREATE TABLE AS SELECT` verwenden.

### Ausführung nicht interaktiver Abfragen

Abfragen, die über die API gesendet werden, werden nicht interaktiv ausgeführt. [!DNL Query Service] Die nicht interaktive Ausführung bedeutet, dass [!DNL Query Service] den API-Aufruf erhält und die Abfrage in der Reihenfolge ausführt, in der sie empfangen wird. Nicht interaktive Abfragen führen immer dazu, dass entweder ein neuer Datensatz in [!DNL Experience Platform] generiert wird, um die Ergebnisse zu erhalten, oder dass neue Zeilen in einen vorhandenen Datensatz eingefügt werden.

## Zugreifen auf ein bestimmtes Feld in einem Objekt

Um auf ein Feld innerhalb eines Objekts in Ihrer Abfrage zuzugreifen, können Sie die Punktnotation (`.`) oder die Klammer (`[]`) verwenden. Die folgende SQL-Anweisung verwendet die Punktnotation, um das `endUserIds`-Objekt bis zum `mcid`-Objekt zu durchlaufen.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Der Name der Analysetabelle. |

Die folgende SQL-Anweisung verwendet Klammern, um das `endUserIds`-Objekt bis zum `mcid`-Objekt zu durchlaufen.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Der Name der Analysetabelle. |

>[!NOTE]
>
>Da jeder Notationstyp die gleichen Ergebnisse zurückgibt, haben Sie die Wahl, das Ergebnis zu verwenden.

Beide obigen Beispielwerte geben ein reduziertes Objekt anstelle eines einzelnen Abfrage zurück:

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

Wenn die Spalte nur bis zum Objekt deklariert wird, gibt sie das gesamte Objekt als Zeichenfolge zurück. Um nur die ID Ansicht, verwenden Sie:

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## Angebote

Einzelne Anführungszeichen, Dubletten- und Rückkurse werden in Abfrage Service-Abfragen unterschiedlich verwendet.

### Einfache Anführungszeichen

Das einfache Anführungszeichen (`'`) wird zum Erstellen von Textzeichenfolgen verwendet. Sie kann beispielsweise in der `SELECT`-Anweisung verwendet werden, um einen statischen Textwert im Ergebnis zurückzugeben, und in der `WHERE`-Klausel, um den Inhalt einer Spalte auszuwerten.

In der folgenden Abfrage wird ein statischer Textwert (`'datasetA'`) für eine Spalte deklariert:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

In der folgenden Abfrage wird eine Zeichenfolge mit einem einfachen Anführungszeichen (`'homepage'`) in der WHE-Klausel verwendet, um Ereignis für eine bestimmte Seite zurückzugeben.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### Anführungszeichen für Dubletten

Das Anführungszeichen (`"`) wird verwendet, um einen Bezeichner mit Leerzeichen zu deklarieren.

In der folgenden Abfrage werden Dubletten-Anführungszeichen verwendet, um Werte aus angegebenen Spalten zurückzugeben, wenn eine Spalte einen Leerzeichen in ihrem Bezeichner enthält:

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
>Dubletten-Anführungszeichen **können nicht mit Punktnotation-Feldzugriff verwendet werden.**

### Rücke Anführungszeichen

Das Backquote `` ` `` wird verwendet, um reservierten Spaltennamen **nur** zu entkommen, wenn die Punktnotation-Syntax verwendet wird. Da `order` beispielsweise ein reserviertes Wort in SQL ist, müssen Sie Backquotes verwenden, um auf das Feld `commerce.order` zuzugreifen:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Mit den Backquotes können Sie auch auf ein Feld zugreifen, das Beginn mit einer Nummer enthält. Um beispielsweise auf das Feld `30_day_value` zuzugreifen, müssen Sie die Notation &quot;Zurück&quot;verwenden.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Die Backquotes sind **nicht** erforderlich, wenn Sie Klammern verwenden.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Anzeigen von Tabelleninformationen

Nachdem Sie eine Verbindung zum Abfrage Service hergestellt haben, können Sie alle verfügbaren Tabellen auf der Plattform anzeigen, indem Sie entweder die Befehle `\d` oder `SHOW TABLES` verwenden.

### Standard-Ansicht

Der Befehl `\d` zeigt die standardmäßige PostgreSQL-Ansicht für die Tabellenerstellung an. Nachfolgend finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### Detaillierte Ansicht der Tabelle

`SHOW TABLES` ist ein benutzerdefinierter Befehl, der detailliertere Informationen zu den Tabellen enthält. Nachfolgend finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### Informationen zum Schema

Um detailliertere Informationen zu den Schemas in der Tabelle Ansicht, können Sie den Befehl `\d {TABLE_NAME}` verwenden, wobei `{TABLE_NAME}` der Name der Tabelle ist, deren Schema-Informationen Sie Ansicht haben möchten.

Das folgende Beispiel zeigt die Schema-Informationen für die Tabelle `luma_midvalues`, die mit `\d luma_midvalues` angezeigt werden:

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

Außerdem können Sie weitere Informationen zu einer bestimmten Spalte abrufen, indem Sie den Namen der Spalte an den Tabellennamen anhängen. Dies würde im Format `\d {TABLE_NAME}_{COLUMN}` geschrieben.

Das folgende Beispiel zeigt zusätzliche Informationen für die Spalte `web` und wird mit dem folgenden Befehl aufgerufen: `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## Datensätze verknüpfen

Sie können mehrere Datensätze zusammenführen, um Daten aus anderen Datensätzen in Ihre Abfrage aufzunehmen.

Das folgende Beispiel würde die folgenden beiden Datensätze (`your_analytics_table` und `custom_operating_system_lookup`) verbinden und eine `SELECT`-Anweisung für die 50 obersten Betriebssysteme nach Anzahl der Ansichten erstellen.

**Abfrage**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**Ergebnisse**

| OperatingSystem | PageViews |
| --------------- | --------- |
| Windows 7 | 2781979,0 |
| Windows XP | 1669824,0 |
| Windows 8 | 420024,0 |
| Adobe AIR | 315032,0 |
| Windows Vista | 173.566,0 |
| Mobile iOS 6.1.3 | 119069,0 |
| Linux | 56.516,0 |
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

Abfrage Service unterstützt das Deduplizierung-Duplikate von Daten oder das Entfernen von Duplikat-Zeilen aus Daten. Weitere Informationen zu Deduplizierung-Duplikate finden Sie im Handbuch [Abfrage Service Deduplizierung-Duplikate Guide](./deduplication.md).

## Nächste Schritte

Durch Lesen dieses Dokuments wurden Sie mit einigen wichtigen Überlegungen beim Schreiben von Abfragen mit [!DNL Query Service] vertraut gemacht. Weitere Informationen zur Verwendung der SQL-Syntax zum Schreiben eigener Abfragen finden Sie in der [SQL-Syntaxdokumentation](../sql/syntax.md).

Weitere Beispiele von Abfragen, die im Abfrage Service verwendet werden können, finden Sie in den Handbüchern zu den Abfragen [Adobe Analytics sample](./adobe-analytics.md), [Adobe Target sample Abfragen](./adobe-target.md) oder [ExperienceEvent sample Abfragen](./experience-event-queries.md).
