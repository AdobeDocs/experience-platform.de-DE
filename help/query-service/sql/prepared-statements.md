---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; vorbereitete Anweisungen; vorbereitet; sql
solution: Experience Platform
title: Vorbereitete Anweisungen in Query Service
description: In SQL werden vorbereitete Anweisungen verwendet, um ähnliche Abfragen oder Aktualisierungen als Vorlage zu verwenden. Adobe Experience Platform Query Service unterstützt vorbereitete Anweisungen durch Einsatz einer parametrisierten Abfrage.
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 85%

---

# Vorbereitete Anweisungen

In SQL dienen vorbereitete Anweisungen dazu, ähnliche Abfragen oder Aktualisierungen als Vorlagen zu erstellen. Adobe Experience Platform [!DNL Query Service] unterstützt vorbereitete Anweisungen mithilfe einer parametrisierten Abfrage. Dies kann die Leistung optimieren, da Sie eine Abfrage nicht mehr wiederholt erneut analysieren müssen.

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
