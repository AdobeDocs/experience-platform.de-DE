---
title: Best Practices für die Organisation von Daten-Assets in Query Service
description: In diesem Dokument wird eine logische Methode zur Organisation von Daten beschrieben, um die Verwendung von Query Service zu erleichtern.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Organisieren von Daten-Assets in Query Service

Dieses Dokument enthält Anleitungen zu Best Practices für die Organisation von Daten-Assets, einschließlich Datensätzen, Ansichten und temporären Tabellen, die mit Adobe Experience Platform Query Service verwendet werden können. Sie behandelt die Struktur Ihrer Daten sowie Informationen zum Zugriff, zur Aktualisierung und zum Löschen dieser Informationen.

Es ist wichtig, Ihre Daten-Assets in Platform logisch zu organisieren [!DNL Data Lake] während sie wachsen. Query Service erweitert SQL-Konstrukte, mit denen Sie Daten-Assets logisch in einer Sandbox gruppieren können. Diese Organisationsmethode ermöglicht die Freigabe von Daten-Assets zwischen Schemas, ohne dass diese physisch verschoben werden müssen.

## Erste Schritte

Bevor Sie mit diesem Dokument fortfahren, sollten Sie [Query Service](../home.md) Funktionen und haben die [Benutzerhandbuch](../ui/user-guide.md).

## Daten in Query Service organisieren

Die folgenden Beispiele zeigen die Konstrukte, die Ihnen über Adobe Experience Platform Query Service zur logischen Organisation Ihrer Daten mithilfe der SQL-Standardsyntax zur Verfügung stehen. Erstellen Sie zunächst eine Datenbank, die als Container für Ihre Datenpunkte fungiert. Eine Datenbank kann ein oder mehrere Schemas enthalten, und jedes Schema kann dann einen oder mehrere Verweise auf ein Daten-Asset (Datensätze, Ansichten, temporäre Tabellen usw.) enthalten. Diese Verweise umfassen alle Beziehungen oder Verknüpfungen zwischen den Datensätzen.

Siehe [Benutzerhandbuch zum Abfrage-Editor](../ui/user-guide.md) für ausführliche Anleitungen zur Verwendung der Query Service-Benutzeroberfläche zum Erstellen von SQL-Abfragen.

Die folgenden SQL-Konstrukte zum logischen Organisieren von Datensätzen in einer Sandbox werden unterstützt.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Das Beispiel (für die Kürze leicht abgeschnitten) zeigt diese Methode, bei der `databaseA` Schema enthält `schema1`.

## Zuordnen von Daten-Assets zu einem Schema

Nachdem ein Schema erstellt wurde, um als Container für die Daten-Assets zu fungieren, kann jeder Datensatz mithilfe der SQL ALTER TABLE-Standardsyntax mit einem oder mehreren Schemas in der Datenbank verknüpft werden.

Im folgenden Beispiel werden `dataset1`, `dataset2`, `dataset3` und `v1` der `databaseA.schema1` -Container, der im vorherigen Beispiel erstellt wurde.

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## Zugreifen auf Daten-Assets aus dem Datencontainer

Durch die entsprechende Qualifizierung des Datenbanknamens können alle [!DNL PostgreSQL] -Client kann eine Verbindung zu einer beliebigen Datenstruktur herstellen, die Sie mithilfe des SHOW-Suchbegriffs erstellt haben. Weitere Informationen zum Keyword SHOW finden Sie im [Abschnitt &quot;SHOW&quot;in der SQL-Syntaxdokumentation](../sql/syntax.md#show).

&quot;all&quot;ist der standardmäßige Datenbankname, der alle Datenbank- und Schema-Container in einer Sandbox enthält. Wenn Sie [!DNL PostgreSQL] Verbindung verwenden `dbname="all"`können Sie **any** Datenbank und Schema, die Sie zur logischen Organisation Ihrer Daten erstellt haben.

Auflisten aller Datenbanken unter `dbname="all"` zeigt drei verfügbare Datenbanken an.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

Auflisten des gesamten Schemas unter `dbname="all"` zeigt die drei Schemas an, die sich auf jede Datenbank in der Sandbox beziehen.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Wenn Sie [!DNL PostgreSQL] Verbindung verwenden `dbname="databaseA"`können Sie auf jedes mit dieser Datenbank verknüpfte Schema zugreifen, wie im folgenden Beispiel gezeigt.

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

Mit der Punktnotation können Sie auf alle Tabellen zugreifen, die mit einem bestimmten Schema verknüpft sind, das mit Ihrer ausgewählten Datenbank verbunden ist. Durch Verbinden mit `DBNAME = databaseA.schema1;`alle mit diesem spezifischen Schema verknüpften Tabellen (`schema1`) angezeigt. Dadurch erhalten Sie Informationen darüber, welcher Datensatz welche Tabelle enthält.

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

Wenn die Anzahl der Daten-Assets in Ihrer IMS-Organisation (oder Sandbox) zunimmt, ist es erforderlich, Daten-Assets aus einem Datencontainer zu aktualisieren oder zu entfernen. Einzelne Assets können aus dem Organisations-Container entfernt werden, indem mithilfe der Punktnotation auf die entsprechende Datenbank und den entsprechenden Schemanamen verwiesen wird. Die Tabelle und Ansicht (`t1` und `v1` bzw. hinzugefügt zu `databaseA.schema1` im ersten Beispiel werden mithilfe der Syntax im folgenden Beispiel entfernt.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Entfernen von Daten-Assets

Die [DROP TABLE](../sql/syntax.md#drop-table) -Funktion entfernt ein Daten-Asset nur physisch aus der [!DNL Data Lake] wenn eine einzige Referenz auf die Tabelle in allen Datenbanken Ihrer IMS-Organisation vorhanden ist.

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

Durch Lesen dieses Dokuments erhalten Sie jetzt ein besseres Verständnis der Best Practices in Bezug auf die Organisation und Struktur Ihrer Daten-Assets zur Verwendung mit Adobe Experience Platform Query Service. Es wird empfohlen, sich weiter mit Best Practices für Query Service vertraut zu machen, indem Sie mehr über [Dokumentation zur Datendeduplizierung](../essential-concepts/deduplication.md).
