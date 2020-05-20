---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vorgefertigte Anweisungen
topic: prepared statements
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 8%

---


# Vorgefertigte Anweisungen

In SQL werden vorbereitete Anweisungen verwendet, um ähnliche Abfragen oder Aktualisierungen vorzubereiten. Der Adobe Experience Platform Abfrage Service unterstützt vorbereitete Anweisungen mithilfe einer parametrisierten Abfrage. Dies kann zur Leistungsoptimierung verwendet werden, da Sie eine Abfrage nicht mehr immer wieder neu analysieren müssen.

## Zubereitete Anweisungen verwenden

Bei der Verwendung vorbereiteter Anweisungen werden die folgenden Syntaxen unterstützt:

- [VORBEREITUNG](#prepare)
- [EXECUTE](#execute)
- [DEALLOCATE](#deallocate)

### Vorbereitung einer vorbereiteten Erklärung {#prepare}

Diese SQL-Abfrage speichert die geschriebene SELECT-Abfrage mit dem angegebenen Namen `PLAN_NAME`. Sie können Variablen verwenden, z. B. `$1` anstelle von tatsächlichen Werten. Diese vorbereitete Erklärung wird während der aktuellen Sitzung gespeichert. Beachten Sie, dass bei den Plannamen **nicht** zwischen Groß- und Kleinschreibung unterschieden wird.

#### SQL-Format

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### Beispiel-SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Eine vorbereitete Anweisung ausführen {#execute}

Diese SQL-Abfrage verwendet die vorbereitete Anweisung, die zuvor erstellt wurde.

#### SQL-Format

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### Beispiel-SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### Zubereitete Anweisung aufheben {#deallocate}

Diese SQL-Abfrage wird zum Löschen der benannten vorbereiteten Anweisung verwendet.

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

| id | firstname | lastname | Geburtstag | email | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | Alexander | davis | 1993-09-15 | example@example.com | Vancouver | Kanada |
| 10001 | Antoine | dubois | 1967-03-14 | example2@example.com | Paris | Frankreich |
| 10002 | kyoko | Sakura | 1999-11-26 | example3@example.com | Tokio | Japan |
| 10003 | Linus | Pettersson | 1982-06-03 | example4@example.com | Stockholm | Schweden |
| 10004 | aasir | Waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenia |
| 10005 | Farando | Rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Diese SQL-Abfrage kann mithilfe der folgenden vorbereiteten Anweisung parametrisiert werden:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Nun kann die vorbereitete Anweisung mithilfe des folgenden Aufrufs ausgeführt werden:

```sql
EXECUTE getIdRange(10000, 10005);
```

Wenn dies aufgerufen wird, sehen Sie genau die gleichen Ergebnisse wie zuvor:

| id | firstname | lastname | Geburtstag | email | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | Alexander | davis | 1993-09-15 | example@example.com | Vancouver | Kanada |
| 10001 | Antoine | dubois | 1967-03-14 | example2@example.com | Paris | Frankreich |
| 10002 | kyoko | Sakura | 1999-11-26 | example3@example.com | Tokio | Japan |
| 10003 | Linus | Pettersson | 1982-06-03 | example4@example.com | Stockholm | Schweden |
| 10004 | aasir | Waithaka | 1976-12-17 | example5@example.com | Nairobi | Kenia |
| 10005 | Farando | Rios | 2002-07-30 | example6@example.com | Santiago | Chile |

Nachdem Sie die vorbereitete Anweisung verwendet haben, können Sie die Zuweisung mithilfe des folgenden Aufrufs aufheben:

```sql
DEALLOCATE getIdRange;
```
