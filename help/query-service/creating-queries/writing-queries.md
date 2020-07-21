---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Schreiben von Abfragen
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 2%

---


# Allgemeine Leitlinien für die Ausführung von Abfragen in [!DNL Query Service]

In diesem Dokument werden wichtige Details erläutert, die beim Schreiben von Abfragen in der Adobe Experience Platform zu beachten sind [!DNL Query Service].

Ausführliche Informationen zur in verwendeten SQL-Syntax [!DNL Query Service]finden Sie in der [SQL-Syntaxdokumentation](../sql/syntax.md).

## Ausführungsmodelle für Abfragen

Adobe Experience Platform [!DNL Query Service] verfügt über zwei Ausführungsmodelle von Abfragen: interaktiv und nicht interaktiv. Die interaktive Ausführung wird für die Entwicklung von Abfragen und die Erstellung von Berichten in Business Intelligence-Tools verwendet, während nicht interaktive Anwendungen für größere Aufträge und operative Abfragen als Teil eines Datenverarbeitungs-Workflows verwendet werden.

### Ausführung interaktiver Abfragen

Abfragen können interaktiv ausgeführt werden, indem sie über die [!DNL Query Service] Benutzeroberfläche oder [über einen angeschlossenen Client](../clients/overview.md)gesendet werden. Bei Ausführung [!DNL Query Service] [!DNL Query Service] über einen angeschlossenen Client wird eine aktive Sitzung zwischen dem Client und ausgeführt, bis entweder die gesendete Abfrage zurückgegeben wird oder eine Zeitüberschreitung eintritt.

Die Ausführung interaktiver Abfragen unterliegt folgenden Einschränkungen:

| Parameter | Einschränkung |
| --------- | ---------- |
| Abfrage-Timeout | 10 Minuten |
| Maximale Zeilenanzahl | 50,000 |
| Maximale gleichzeitige Abfragen | 5 |

>[!NOTE]
>
>Um die maximale Zeilenzahl zu überschreiben, nehmen Sie `LIMIT 0` in Ihre Abfrage auf. Die Zeitüberschreitung der Abfrage von 10 Minuten ist weiterhin gültig.

Standardmäßig werden die Ergebnisse interaktiver Abfragen an den Client zurückgegeben und **nicht** beibehalten. Damit die Ergebnisse als Datensatz beibehalten werden können, muss [!DNL Experience Platform]die Abfrage die `CREATE TABLE AS SELECT` Syntax verwenden.

### Ausführung nicht interaktiver Abfragen

Abfragen, die über die [!DNL Query Service] API gesendet werden, werden nicht interaktiv ausgeführt. Die nicht interaktive Ausführung bedeutet, dass der API-Aufruf [!DNL Query Service] empfangen und die Abfrage in der Reihenfolge ausgeführt wird, in der sie empfangen wird. Nicht interaktive Abfragen führen immer dazu, dass entweder ein neuer Datensatz generiert wird, um die Ergebnisse [!DNL Experience Platform] zu erhalten, oder dass neue Zeilen in einen vorhandenen Datensatz eingefügt werden.

## Zugreifen auf ein bestimmtes Feld in einem Objekt

Um auf ein Feld innerhalb eines Objekts in Ihrer Abfrage zuzugreifen, können Sie entweder die Punktnotation (`.`) oder die Klammern-Notation (`[]`) verwenden. Die folgende SQL-Anweisung verwendet die Punktnotation, um das `endUserIds` Objekt bis zum `mcid` Objekt zu durchlaufen.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Der Name der Analysetabelle. |

Die folgende SQL-Anweisung verwendet Klammern-Notation, um das `endUserIds` Objekt bis zum `mcid` Objekt zu durchlaufen.

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
>Da jeder Notationstyp die gleichen Ergebnisse zurückgibt, haben Sie die Wahl, das zu verwendende zu verwenden.

Beide obigen Beispielwerte geben ein reduziertes Objekt anstelle eines einzelnen Abfrage zurück:

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

Das zurückgegebene `endUserIds._experience.mcid` Objekt enthält die entsprechenden Werte für die folgenden Parameter:

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

## Verwenden von einfachen Anführungszeichen, Dubletten- und Rückführungszeichen

In diesem Abschnitt wird erläutert, wann einfache Anführungszeichen, Anführungszeichen für Dubletten und Backquotes in Abfragen verwendet werden.

### Einfache Anführungszeichen

Das einfache Anführungszeichen (`'`) wird zum Erstellen von Textzeichenfolgen verwendet. Sie kann beispielsweise in der `SELECT` Anweisung verwendet werden, um einen statischen Textwert im Ergebnis zurückzugeben, und in der `WHERE` Klausel, um den Inhalt einer Spalte auszuwerten.

In der folgenden Abfrage wird ein statischer Textwert (`'datasetA'`) für eine Spalte deklariert:

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

In der folgenden Abfrage wird eine Zeichenfolge (`'homepage'`) mit einem einfachen Anführungszeichen in der WHE-Klausel verwendet, um Ereignis für eine bestimmte Seite zurückzugeben.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### Anführungszeichen für Dubletten

Das Anführungszeichen (`"`) der Dublette wird verwendet, um einen Bezeichner mit Leerzeichen zu deklarieren.

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
>Dubletten-Anführungszeichen **können nicht** mit Punktnotation-Feldzugriff verwendet werden.

### Rücke Anführungszeichen

Das Backquote-Anführungszeichen `` ` `` dient **nur** zur Escape-Funktion reservierter Spaltennamen. Da `order` in SQL beispielsweise ein reserviertes Wort vorhanden ist, müssen Sie Backquotes verwenden, um auf das Feld zuzugreifen `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Mit den Backquotes können Sie auch auf ein Feld zugreifen, das Beginn mit einer Nummer enthält. Um beispielsweise auf das Feld zugreifen zu können, `30_day_value`müssen Sie eine Backquote-Notation verwenden.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

Wenn Sie Klammern verwenden, sind **keine** Backquotes erforderlich.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## Nächste Schritte

Durch das Lesen dieses Dokuments wurden Sie bei der Erstellung von Abfragen mit [!DNL Query Service]einigen wichtigen Aspekten vorgestellt. Weitere Informationen zur Verwendung der SQL-Syntax zum Schreiben eigener Abfragen finden Sie in der [SQL-Syntaxdokumentation](../sql/syntax.md).