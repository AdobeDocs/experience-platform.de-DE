---
title: Festlegen Primärer Identitäten in einem Ad-hoc-Datensatz
description: Mit Adobe Experience Platform Query Service können Sie eine Identität oder eine primäre Identität für Ad-hoc-Schemadatensatzfelder direkt über den Befehl SQL ALTER TABLE festlegen. In diesem Dokument wird erläutert, wie Sie mit dem Befehl ALTER TABLE eine primäre Identität oder eine sekundäre Identität festlegen können.
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: d9c3ccdf0c0e191af1ab18e894688f301378156d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Festlegen von primären Identitäten in einem Ad-hoc-Datensatz

Mit Adobe Experience Platform Query Service können Sie Datensatzspalten mit Begrenzungen für den SQL `ALTER TABLE`-Befehl entweder als primäre oder sekundäre Identitäten markieren. Mit dieser Funktion können Sie sicherstellen, dass gekennzeichnete Felder den Datenschutzanforderungen entsprechen. Mit diesem Befehl können Sie über SQL direkt Begrenzungen für primäre und sekundäre Identitätstabelle-Spalten hinzufügen oder löschen.

## Erste Schritte

Die Beschriftung von Datensatzspalten als primäre oder sekundäre Identität erfordert ein Verständnis des SQL-Befehls `ALTER TABLE` und ein gutes Verständnis der Datenschutzanforderungen. Bevor Sie mit diesem Dokument fortfahren, lesen Sie bitte die folgende Dokumentation:

* [Das SQL-Syntaxhandbuch für den Befehl `ALTER TABLE`](../sql/syntax.md).
* [Die Übersicht über Data Governance](../../data-governance/home.md) für weitere Informationen.

## Hinzufügen von Einschränkungen {#add-constraints}

Mit dem Befehl `ALTER TABLE` können Sie eine Datensatzspalte als Identität einer Person beschriften und diese Bezeichnung dann als primäre Identität verwenden, indem Sie die zugehörigen Metadaten mit SQL aktualisieren. Dies ist besonders nützlich, wenn Datensätze über SQL erstellt werden und nicht direkt über die Platform-Benutzeroberfläche von einem Schema aus. Mit dem -Befehl können Sie sicherstellen, dass Ihre Datenvorgänge in Platform mit Datennutzungsrichtlinien konform sind.

**Beispiele**

Im folgenden Beispiel wird der vorhandenen Tabelle `t1` eine Einschränkung hinzugefügt. Die Werte der Spalte `id` sind jetzt unter dem Namespace `IDFA` als primäre Identitäten markiert. Ein Identitäts-Namespace ist ein Schlüsselwort, das den Typ der Identitätsdaten deklariert, die das Feld darstellt.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

Das zweite Beispiel stellt sicher, dass die Spalte `id` als sekundäre Identität markiert ist.

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## Dropbegrenzungen {#drop-constraints}

Einschränkungen können auch mit dem Befehl `ALTER TABLE` aus Tabellenspalten entfernt werden.

**Beispiele**

Im folgenden Beispiel wird die Anforderung entfernt, dass die Spalte `c1` in der vorhandenen Tabelle `t1` als primäre Identität gekennzeichnet sein muss.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

Wie unten dargestellt, wird dieselbe Syntax beim Entfernen einer Identitätsbegrenzung verwendet.

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## Identitäten anzeigen

Verwenden Sie den Metadatenbefehl &quot;`show identities`&quot;in der Befehlszeilenschnittstelle, um eine Tabelle mit allen Attributen anzuzeigen, die als Identität zugewiesen sind.

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

* Um eine Spalte als Identität anzugeben, müssen Sie **** auch den Namespace definieren, der als Metadaten für die Spalte beibehalten werden soll.
* XDM unterstützt nicht die Angabe eines Spaltennamens im Namespace-Attribut.
* Wenn Ihr Schema das XDM-Feld `identityMap` verwendet, muss das `identityMap` -Objekt der Stammebene oder der obersten Ebene **** als Identität oder primäre Identität gekennzeichnet sein.
