---
title: Best Practices für die Organisation von Daten-Assets in Query Service
description: In diesem Dokument wird eine logische Methode zur Organisation von Daten beschrieben, um die Verwendung von Query Service zu vereinfachen.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# Organisieren von Daten-Assets in Query Service

Dieses Dokument enthält Anleitungen zu Best Practices für die Organisation von Daten-Assets, einschließlich Datensätzen, Ansichten und temporären Tabellen, die mit Adobe Experience Platform Query Service verwendet werden können. Sie behandelt die Struktur Ihrer Daten sowie Informationen zum Zugriff, zur Aktualisierung und zum Löschen dieser Informationen.

Es ist wichtig, Ihre Daten-Assets beim Wachstum logisch in Platform [!DNL Data Lake] zu organisieren. Query Service erweitert SQL-Konstrukte, mit denen Sie Daten-Assets logisch in einer Sandbox gruppieren können. Diese Organisationsmethode ermöglicht die Freigabe von Daten-Assets zwischen Schemas, ohne dass diese physisch verschoben werden müssen.

## Erste Schritte

Bevor Sie mit diesem Dokument fortfahren, sollten Sie über gute Kenntnisse der Funktionen von [Query Service](../home.md) verfügen und das [Benutzerhandbuch für die Benutzeroberfläche](../ui/user-guide.md) gelesen haben.

## Daten in Query Service organisieren

Die folgenden Beispiele zeigen die Konstrukte, die Ihnen über Adobe Experience Platform Query Service zur logischen Organisation Ihrer Daten mithilfe der SQL-Standardsyntax zur Verfügung stehen. Erstellen Sie zunächst eine Datenbank, die als Container für Ihre Datenpunkte fungiert. Eine Datenbank kann ein oder mehrere Schemas enthalten, und jedes Schema kann dann einen oder mehrere Verweise auf ein Daten-Asset (Datensätze, Ansichten, temporäre Tabellen usw.) enthalten. Diese Verweise umfassen alle Beziehungen oder Verknüpfungen zwischen den Datensätzen.

Detaillierte Anweisungen zur Verwendung der Query Service-Benutzeroberfläche zum Erstellen von SQL-Abfragen finden Sie im [Benutzerhandbuch für den Abfrage-Editor](../ui/user-guide.md) .

Die folgenden SQL-Konstrukte zum logischen Organisieren von Datensätzen in einer Sandbox werden unterstützt.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Das Beispiel (für die Kürze leicht abgeschnitten) zeigt diese Methode, bei der `databaseA` das Schema `schema1` enthält.

## Zuordnen von Daten-Assets zu einem Schema

Nachdem ein Schema erstellt wurde, um als Container für die Daten-Assets zu fungieren, kann jeder Datensatz mithilfe der SQL ALTER TABLE-Standardsyntax mit einem oder mehreren Schemas in der Datenbank verknüpft werden.

Im folgenden Beispiel werden `dataset1`, `dataset2`, `dataset3` und `v1` zum im vorherigen Beispiel erstellten `databaseA.schema1` Container hinzugefügt.

```SQL
ALTER TABLE dataset1 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 ADD SCHEMA databaseA.schema1;
 
ALTER VIEW v1  ADD SCHEMA databaseA.schema1;
```

## Zugreifen auf Daten-Assets aus dem Datencontainer

Durch die entsprechende Qualifizierung des Datenbanknamens kann jeder [!DNL PostgreSQL]-Client eine Verbindung zu einer beliebigen Datenstruktur herstellen, die Sie mithilfe des SHOW-Suchbegriffs erstellt haben. Weitere Informationen zum SHOW-Schlüsselwort finden Sie im Abschnitt [SHOW&quot;in der SQL-Syntaxdokumentation](../sql/syntax.md#show).

&quot;all&quot;ist der standardmäßige Datenbankname, der alle Datenbank- und Schema-Container in einer Sandbox enthält. Wenn Sie eine [!DNL PostgreSQL] -Verbindung mit `dbname="all"` herstellen, können Sie auf die **beliebige** -Datenbank und das Schema zugreifen, die Sie zum logischen Organisieren Ihrer Daten erstellt haben.

Wenn Sie alle Datenbanken unter `dbname="all"` auflisten, werden drei verfügbare Datenbanken angezeigt.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

Wenn Sie das gesamte Schema unter `dbname="all"` auflisten, werden die drei Schemas angezeigt, die sich auf jede Datenbank in der Sandbox beziehen.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Wenn Sie eine [!DNL PostgreSQL] -Verbindung mit `dbname="databaseA"` herstellen, können Sie auf jedes Schema zugreifen, das mit dieser bestimmten Datenbank verknüpft ist, wie im folgenden Beispiel gezeigt.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
```

Mit der Punktnotation können Sie auf alle Tabellen zugreifen, die mit einem bestimmten Schema verknüpft sind, das mit Ihrer ausgewählten Datenbank verbunden ist. Durch Verbindung zu `DBNAME = databaseA.schema1;` werden alle mit diesem spezifischen Schema (`schema1`) verknüpften Tabellen angezeigt. Dadurch erhalten Sie Informationen darüber, welcher Datensatz welche Tabelle enthält.

```sql
SHOW DATABASES;
  
name     
---------
databaseA


SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1


SHOW tables;
name       | type
----------------------
dataset1| table
dataset2| table
dataset3| table
```

## Aktualisieren oder Entfernen von Daten-Assets aus einem Datencontainer

Wenn die Anzahl der Daten-Assets in Ihrer Organisation (oder Sandbox) zunimmt, ist es erforderlich, Daten-Assets aus einem Datencontainer zu aktualisieren oder zu entfernen. Einzelne Assets können aus dem Organisations-Container entfernt werden, indem mithilfe der Punktnotation auf die entsprechende Datenbank und den entsprechenden Schemanamen verwiesen wird. Die Tabelle und Ansicht (`t1` bzw. `v1`), die im ersten Beispiel zu `databaseA.schema1` hinzugefügt wurden, werden mithilfe der Syntax im folgenden Beispiel entfernt.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Entfernen von Datenelementen

Die Funktion [DROP TABLE](../sql/syntax.md#drop-table) entfernt ein Daten-Asset nur dann physisch aus dem [!DNL Data Lake], wenn eine einzige Referenz auf die Tabelle in allen Datenbanken Ihres Unternehmens vorhanden ist.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Entfernen eines Daten-Asset-Containers

Sowohl die Datenbank als auch das Schema können auch mit SQL-Standardfunktionen entfernt werden.

#### Entfernen von Datenbanken

Wenn andere Verweise auf Daten-Assets vorhanden sind, die mit der Datenbank verknüpft sind, gibt die Funktion beim Versuch, die Datenbank zu entfernen, einen Fehler aus.

```sql
DROP DATABASE databaseA;
```

#### Schema entfernen

Beim Entfernen eines Schemas sind drei wichtige Aspekte zu beachten:

- Beim Entfernen eines Schemas werden keine Daten-Assets wie Tabellen, Ansichten oder temporären Tabellen physisch gelöscht.
- Wenn im Zielschema auf Daten-Assets verwiesen wird und der Modus RESTRICT lautet, wird eine Ausnahme ausgelöst.
- Wenn im Zielschema auf Daten-Assets verwiesen wird und der Modus CASCADE lautet, entfernt das System alle vom Schema-Container referenzierten Daten-Assets und löscht dann den Schema-Container.

```sql
DROP SCHEMA databaseA.schema2;
```

## Nächste Schritte

Durch Lesen dieses Dokuments erhalten Sie jetzt ein besseres Verständnis der Best Practices in Bezug auf die Organisation und Struktur Ihrer Daten-Assets zur Verwendung mit Adobe Experience Platform Query Service. Es wird empfohlen, die Best Practices für Query Service weiterhin zu erlernen, indem Sie die [Dokumentation zur Datendeduplizierung](../key-concepts/deduplication.md) lesen.
