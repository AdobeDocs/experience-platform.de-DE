---
title: Festlegen Primärer Identitäten in einem Ad-hoc-Datensatz
description: Mit Adobe Experience Platform Query Service können Sie eine Identität oder eine primäre Identität für Ad-hoc-Schema-Datensatzfelder direkt über den SQL-Befehl ALTER TABLE festlegen. In diesem Dokument wird erläutert, wie Sie mit dem Befehl ALTER TABLE eine primäre Identität oder eine sekundäre Identität festlegen können.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Festlegen primärer Identitäten in einem Ad-hoc-Datensatz

Mit Adobe Experience Platform Query Service können Sie Datensatzspalten entweder als primäre oder sekundäre Identitäten markieren, indem Sie Einschränkungen für den SQL-`ALTER TABLE`-Befehl verwenden. Mit dieser Funktion können Sie sicherstellen, dass gekennzeichnete Felder den Datenschutzanforderungen entsprechen. Mit diesem Befehl können Sie Begrenzungen für primäre und sekundäre Identitätstabellenspalten direkt über SQL hinzufügen oder löschen.

## Erste Schritte

Das Kennzeichnen von Datensatzspalten als primäre oder sekundäre Identität erfordert ein Verständnis des `ALTER TABLE` SQL-Befehls und ein gutes Verständnis der Datenschutzanforderungen. Bevor Sie mit diesem Dokument fortfahren, lesen Sie bitte die folgende Dokumentation:

* [Das SQL-Syntaxhandbuch für den `ALTER TABLE`-Befehl](../sql/syntax.md).
* [Die Übersicht zu Data Governance](../../data-governance/home.md) für weitere Informationen.

## Hinzufügen von Einschränkungen {#add-constraints}

Mit dem Befehl `ALTER TABLE` können Sie eine Datensatzspalte als Identität einer Person beschriften und diese Kennzeichnung dann als primäre Identität verwenden, indem Sie die zugehörigen Metadaten mithilfe von SQL aktualisieren. Dies ist besonders nützlich, wenn Datensätze über SQL und nicht direkt über die Experience Platform-Benutzeroberfläche aus einem Schema erstellt werden. Mit dem Befehl können Sie sicherstellen, dass Ihre Datenvorgänge in Experience Platform mit Datennutzungsrichtlinien konform sind.

**Beispiele**

Im folgenden Beispiel wird eine Einschränkung zur vorhandenen `t1`-Tabelle hinzugefügt. Die Werte der Spalte `id` sind jetzt als primäre Identitäten unter dem Namespace `IDFA` gekennzeichnet. Ein Identity-Namespace ist ein Schlüsselwort, das den Typ der Identitätsdaten deklariert, die das Feld darstellt.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Das zweite Beispiel stellt sicher, dass die `id` Spalte als sekundäre Identität markiert ist.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Einschränkungen ignorieren {#drop-constraints}

Beschränkungen können auch mithilfe des Befehls `ALTER TABLE` aus Tabellenspalten entfernt werden.

**Beispiele**

Das folgende Beispiel entfernt die Anforderung, dass die Spalte `c1` in der vorhandenen `t1` als primäre Identität bezeichnet werden muss.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Wie unten gezeigt, wird beim Entfernen einer Identitätsbeschränkung dieselbe Syntax für verwendet.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Anzeigen von Identitäten

Verwenden Sie den Metadaten-`show identities` der Befehlszeilenschnittstelle, um eine Tabelle mit allen Attributen anzuzeigen, die als Identität zugewiesen sind.

```shell
> show identities;
```

Nachfolgend finden Sie ein Beispiel für eine zurückgegebene Tabelle.

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM-Einschränkungen {#limitations}

In der folgenden Liste werden wichtige Überlegungen zum Aktualisieren von Identitäten in vorhandenen Datensätzen bei der Verwendung von XDM erläutert.

* Um eine Spalte als Identität anzugeben, **müssen** Sie auch den Namespace definieren, der als Metadaten für die Spalte beibehalten werden soll.
* XDM unterstützt nicht die Angabe eines Spaltennamens im Namespace-Attribut.
* Wenn Ihr Schema das XDM-Feld `identityMap` verwendet, muss das Stamm- oder `identityMap`-Objekt **oberster Ebene** Identität oder primäre Identität gekennzeichnet sein.
