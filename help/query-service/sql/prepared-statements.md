---
keywords: Experience Platform;home;popular topics;query service;Query service;prepared statements;prepared;sql;
solution: Experience Platform
title: Vorbereitete Anweisungen
topic: prepared statements
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 96%

---


# Vorbereitete Anweisungen

In SQL dienen vorbereitete Anweisungen dazu, ähnliche Abfragen oder Aktualisierungen als Vorlagen zu erstellen. Adobe Experience Platform [!DNL Query Service] supports prepared statements by using a parameterized query. Dies kann zur Leistungsoptimierung beitragen, da Sie Abfragen nicht mehr immer wieder neu analysieren müssen.

## Verwenden von vorbereiteten Anweisungen

Bei Verwendung vorbereiteter Anweisungen werden die folgenden Syntaxen unterstützt:

- [PREPARE](#prepare)
- [EXECUTE](#execute)
- [DEALLOCATE](#deallocate)

### Eine vorbereitete Anweisung vorbereiten {#prepare}

Diese SQL-Abfrage speichert die geschriebene SELECT-Abfrage mit dem Namen `PLAN_NAME`. Sie können Variablen, z. B. `$1`, anstelle von tatsächlichen Werten nutzen. Diese vorbereitete Erklärung wird während der aktuellen Sitzung gespeichert. Beachten Sie, dass bei den Plannamen **nicht** zwischen Groß- und Kleinschreibung unterschieden wird.

#### SQL-Format

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### Beispiel-SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Vorbereitete Anweisung ausführen {#execute}

Diese SQL-Abfrage verwendet die vorbereitete Anweisung, die zuvor erstellt wurde.

#### SQL-Format

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### Beispiel-SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### Zuweisung einer vorbereiteten Anweisung aufheben {#deallocate}

Diese SQL-Abfrage dient zum Löschen der benannten vorbereiteten Anweisung.

#### SQL-Format

```sql
DEALLOCATE {PLAN_NAME}
```

#### Beispiel-SQL

```sql
DEALLOCATE test;
```

## Beispielfluss mit vorbereiteten Anweisungen

Zunächst können Sie eine SQL-Abfrage wie die folgende verwenden:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

Die obige SQL-Abfrage gibt folgende Antwort zurück:

| id | firstname | lastname | birthdate | email | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 15.09.1993 | example@example.com | Vancouver | Kanada |
| 10001 | antoine | dubois | 14.03.1967 | example2@example.com | Paris | Frankreich |
| 10002 | kyoko | sakura | 26.11.1999 | example3@example.com | Tokio | Japan |
| 10003 | linus | pettersson | 03.06.1982 | example4@example.com | Stockholm | Schweden |
| 10004 | aasir | waithaka | 17.12.1976 | example5@example.com | Nairobi | Kenia |
| 10005 | fernando | rios | 30.07.2002 | example6@example.com | Santiago | Chile |

Diese SQL-Abfrage kann mithilfe der folgenden vorbereiteten Anweisung parametrisiert werden:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Nun kann die vorbereitete Anweisung mithilfe des folgenden Aufrufs ausgeführt werden:

```sql
EXECUTE getIdRange(10000, 10005);
```

Bei diesem Aufruf sehen Sie genau die gleichen Ergebnisse wie zuvor:

| id | firstname | lastname | birthdate | email | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 15.09.1993 | example@example.com | Vancouver | Kanada |
| 10001 | antoine | dubois | 14.03.1967 | example2@example.com | Paris | Frankreich |
| 10002 | kyoko | sakura | 26.11.1999 | example3@example.com | Tokio | Japan |
| 10003 | linus | pettersson | 03.06.1982 | example4@example.com | Stockholm | Schweden |
| 10004 | aasir | waithaka | 17.12.1976 | example5@example.com | Nairobi | Kenia |
| 10005 | fernando | rios | 30.07.2002 | example6@example.com | Santiago | Chile |

Nachdem Sie die vorbereitete Anweisung fertig verwendet haben, können Sie die Zuweisung mithilfe des folgenden Aufrufs aufheben:

```sql
DEALLOCATE getIdRange;
```
