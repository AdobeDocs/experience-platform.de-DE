---
title: Festlegen Primärer Identitäten in einem Ad-hoc-Datensatz
description: Mit Adobe Experience Platform Query Service können Sie eine Identität oder eine primäre Identität für Ad-hoc-Schemadatesatzfelder direkt über den Befehl SQL ALTER TABLE festlegen. In diesem Dokument wird erläutert, wie Sie mit dem Befehl ALTER TABLE eine primäre Identität oder eine sekundäre Identität festlegen können.
source-git-commit: bf51fc3e0c9635c0555f87f3389fb4a9542c092d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Festlegen von primären Identitäten in einem Ad-hoc-Datensatz

Mit Adobe Experience Platform Query Service können Sie Datensatzspalten mit Begrenzungen für SQL als primäre oder sekundäre Identitäten markieren. `ALTER TABLE` Befehl. Mit dieser Funktion können Sie sicherstellen, dass gekennzeichnete Felder den Datenschutzanforderungen entsprechen. Mit diesem Befehl können Sie über SQL direkt Begrenzungen für primäre und sekundäre Identitätstabelle-Spalten hinzufügen oder löschen.

## Erste Schritte

Die Beschriftung von Datensatzspalten als primäre oder sekundäre Identität erfordert ein Verständnis der `ALTER TABLE` SQL-Befehl und ein gutes Verständnis der Datenschutzanforderungen. Bevor Sie mit diesem Dokument fortfahren, lesen Sie bitte die folgende Dokumentation:

* [SQL-Syntaxleitfaden für die `ALTER TABLE` command](../sql/syntax.md).
* [Übersicht über Data Governance](../../data-governance/home.md) für weitere Informationen.

## Hinzufügen von Einschränkungen {#add-constraints}

Die `ALTER TABLE` -Befehl können Sie eine Datensatzspalte als Identität einer Person beschriften und diese Bezeichnung dann als primäre Identität verwenden, indem Sie die zugehörigen Metadaten mit SQL aktualisieren. Dies ist besonders nützlich, wenn Datensätze über SQL erstellt werden und nicht direkt über die Platform-Benutzeroberfläche von einem Schema aus. Mit dem -Befehl können Sie sicherstellen, dass Ihre Datenvorgänge in Platform mit Datennutzungsrichtlinien konform sind.

**Beispiele**

Im folgenden Beispiel wird der vorhandenen `t1` Tabelle. Die Werte der `id` -Spalte sind nun als primäre Identitäten unter der `IDFA` Namespace. Ein Identitäts-Namespace ist ein Schlüsselwort, das den Typ der Identitätsdaten deklariert, die das Feld darstellt.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Das zweite Beispiel stellt sicher, dass die Variable `id` -Spalte wird als sekundäre Identität markiert.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Dropbegrenzungen {#drop-constraints}

Begrenzungen können auch mithilfe der `ALTER TABLE` Befehl.

**Beispiele**

Im folgenden Beispiel wird die Anforderung entfernt, dass die Variable `c1` -Spalte eine primäre Identität in der vorhandenen `t1` Tabelle.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Wie unten dargestellt, wird dieselbe Syntax beim Entfernen einer Identitätsbegrenzung verwendet.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Identitäten anzeigen

Verwenden des Metadaten-Befehls `show identities` über die Befehlszeilenschnittstelle, um eine Tabelle mit allen Attributen anzuzeigen, die als Identität zugewiesen sind.

```shell
> show identities;
```

Nachfolgend finden Sie ein Beispiel einer zurückgegebenen Tabelle.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM-Beschränkungen {#limitations}

In der folgenden Liste werden wichtige Überlegungen zum Aktualisieren von Identitäten in vorhandenen Datensätzen bei der Verwendung von XDM erläutert.

* Um eine Spalte als Identität anzugeben, müssen Sie **must** definieren auch den Namespace, der als Metadaten für die Spalte beibehalten werden soll.
* XDM unterstützt nicht die Angabe eines Spaltennamens im Namespace-Attribut.
* Wenn Ihr Schema die `identityMap` XDM-Feld, der Stamm oder die oberste Ebene `identityMap` Objekt **must** als Identität oder primäre Identität gekennzeichnet sein.
