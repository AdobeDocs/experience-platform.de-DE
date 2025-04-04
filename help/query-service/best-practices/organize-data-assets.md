---
title: Best Practices für die Organisation von Daten-Assets in Query Service
description: In diesem Dokument wird eine logische Möglichkeit zur Organisation von Daten für eine einfache Verwendung mit dem Abfrage-Service beschrieben.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# Organisieren von Daten-Assets in Query Service

Dieses Dokument enthält Anleitungen zu Best Practices für die Organisation von Datenelementen, einschließlich Datensätzen, Ansichten und temporären Tabellen, zur Verwendung mit dem Abfrage-Service von Adobe Experience Platform. Es wird beschrieben, wie Sie Ihre Daten strukturieren und wie Sie auf diese Informationen zugreifen, sie aktualisieren und löschen können.

Es ist wichtig, Ihre Datenelemente beim Wachstum innerhalb der Experience Platform-[!DNL Data Lake] logisch zu organisieren. Query Service erweitert SQL-Konstrukte, mit denen Sie Datenelemente innerhalb einer Sandbox logisch gruppieren können. Diese Organisationsmethode ermöglicht die Freigabe von Daten-Assets zwischen Schemas, ohne dass sie physisch verschoben werden müssen.

## Erste Schritte

Bevor Sie mit diesem Dokument fortfahren, sollten Sie über gute Kenntnisse der Funktionen [Abfrage-Service](../home.md) verfügen und das [Handbuch zur Benutzeroberfläche) ](../ui/user-guide.md).

## Organisieren von Daten im Abfrage-Service

Die folgenden Beispiele zeigen die Konstrukte, die Ihnen über den Abfrage-Service von Adobe Experience Platform zur Verfügung stehen, um Ihre Daten logisch mit der standardmäßigen SQL-Syntax zu organisieren. Erstellen Sie zunächst eine Datenbank, die als Container für Ihre Datenpunkte fungiert. Eine Datenbank kann ein oder mehrere Schemata enthalten. Jedes Schema kann dann einen oder mehrere Verweise auf ein Daten-Asset haben (Datensätze, Ansichten, temporäre Tabellen usw.). Diese Verweise umfassen alle Beziehungen oder Zuordnungen zwischen den Datensätzen.

Ausführliche Anleitungen [ Verwendung der Abfrage-Service](../ui/user-guide.md)Benutzeroberfläche zum Erstellen von SQL-Abfragen finden Sie im Benutzerhandbuch zum Abfrage-Editor .

Die folgenden SQL-Konstrukte werden unterstützt, um Datensätze in einer Sandbox logisch zu organisieren.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

Das Beispiel (aus Gründen der Kürze leicht gekürzt) zeigt diese Methode, bei der `databaseA` Schemaelemente `schema1`.

## Verknüpfen von Daten-Assets mit einem Schema

Nachdem ein Schema als Container für die Daten-Assets erstellt wurde, kann jeder Datensatz mithilfe der standardmäßigen SQL ALTER TABLE-Syntax mit einem oder mehreren Schemas in der Datenbank verknüpft werden.

Im folgenden Beispiel werden `dataset1`, `dataset2`, `dataset3` und `v1` zu dem im vorherigen Beispiel erstellten `databaseA.schema1`-Container hinzugefügt.

```SQL
ALTER TABLE dataset1 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 ADD SCHEMA databaseA.schema1;
 
ALTER VIEW v1  ADD SCHEMA databaseA.schema1;
```

## Zugreifen auf Daten-Assets über den Daten-Container

Durch die entsprechende Qualifizierung des Datenbanknamens kann jeder [!DNL PostgreSQL]-Client eine Verbindung zu jeder der Datenstrukturen herstellen, die Sie mit dem SHOW-Schlüsselwort erstellt haben. Weitere Informationen zum SHOW-Schlüsselwort finden Sie im Abschnitt [SHOW“ in der SQL-Syntaxdokumentation](../sql/syntax.md#show).

„all“ ist der standardmäßige Datenbankname, der alle Datenbanken und Schema-Container in einer Sandbox enthält. Wenn Sie eine [!DNL PostgreSQL] Verbindung mit `dbname="all"` herstellen, können Sie auf eine **Datenbank und ein** Schema zugreifen, die Sie erstellt haben, um Ihre Daten logisch zu organisieren.

Beim Auflisten aller Datenbanken unter `dbname="all"` werden drei verfügbare Datenbanken angezeigt.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

In der Liste aller Schemata unter `dbname="all"` werden die drei Schemata angezeigt, die sich auf jede Datenbank in der Sandbox beziehen.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

Wenn Sie eine [!DNL PostgreSQL] Verbindung mithilfe von `dbname="databaseA"` herstellen, können Sie auf jedes Schema zugreifen, das mit dieser spezifischen Datenbank verknüpft ist, wie im folgenden Beispiel gezeigt.

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

Mit der Punktnotation können Sie auf jede Tabelle zugreifen, die mit einem bestimmten Schema verknüpft ist, das mit Ihrer ausgewählten Datenbank verbunden ist. Durch Herstellen einer Verbindung zu `DBNAME = databaseA.schema1;` werden alle mit diesem spezifischen Schema (`schema1`) verknüpften Tabellen angezeigt. Dadurch erhalten Sie Informationen darüber, welcher Datensatz welche Tabelle enthält.

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

## Aktualisieren oder Entfernen von Datenelementen aus einem Daten-Container

Mit zunehmender Anzahl von Daten-Assets in Ihrer Organisation (oder Sandbox) wird es erforderlich, Daten-Assets zu aktualisieren oder aus einem Daten-Container zu entfernen. Einzelne Assets können aus dem Organisations-Container entfernt werden, indem mit der Punktnotation auf den entsprechenden Datenbank- und Schemanamen verwiesen wird. Die Tabelle und die Ansicht (`t1` bzw. `v1`), die `databaseA.schema1` im ersten Beispiel hinzugefügt wurden, werden mithilfe der Syntax im folgenden Beispiel entfernt.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### Entfernen von Daten-Assets

Die [DROP TABLE](../sql/syntax.md#drop-table)-Funktion entfernt ein Daten-Asset nur dann physisch aus dem [!DNL Data Lake], wenn in allen Datenbanken Ihres Unternehmens ein einzelner Verweis auf die Tabelle vorhanden ist.

```sql
DROP TABLE databaseA.schema2.t1;
```

### Entfernen eines Daten-Asset-Containers

Sowohl die Datenbank als auch das Schema können auch mit standardmäßigen SQL-Funktionen entfernt werden.

#### Entfernen einer Datenbank

Wenn andere Verweise auf mit der Datenbank verknüpfte Daten-Assets vorhanden sind, gibt die Funktion beim Versuch, die Datenbank zu entfernen, einen Fehler aus.

```sql
DROP DATABASE databaseA;
```

#### Entfernen eines Schemas

Beim Entfernen eines Schemas sind drei wichtige Aspekte zu beachten:

- Beim Entfernen eines Schemas werden keine Daten-Assets wie Tabellen, Ansichten oder temporären Tabellen physisch gelöscht.
- Wenn im Zielschema auf Daten-Assets verwiesen wird und der Modus „EINSCHRÄNKEN“ ist, wird eine Ausnahme ausgelöst.
- Wenn im Zielschema Datenelemente referenziert werden und der Modus KASKADIEREND ist, entfernt das System alle Datenelemente, auf die vom Schema-Container verwiesen wird, und löscht dann den Schema-Container.

```sql
DROP SCHEMA databaseA.schema2;
```

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie jetzt ein besseres Verständnis der Best Practices für die Organisation und Struktur Ihrer Datenelemente zur Verwendung mit dem Abfrage-Service von Adobe Experience Platform. Es wird empfohlen, sich weiter mit den Best Practices für den Abfrage-Service vertraut zu machen, indem Sie die [Dokumentation zur Datendeduplizierung](../key-concepts/deduplication.md) lesen.
