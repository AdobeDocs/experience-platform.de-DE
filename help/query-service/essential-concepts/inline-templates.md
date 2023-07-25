---
title: Inline-Vorlagen
description: Erfahren Sie, wie Sie mehrere Bedingungen in zahlreichen Abfragen mit Inline-Vorlagen wiederverwenden können.
source-git-commit: e9deabe1e0514f44be085e558fd2fdbf54956f3e
workflow-type: ht
source-wordcount: '485'
ht-degree: 100%

---

# Inline-Vorlagen

Mit Inline-Vorlagen können Sie mehrere Bedingungen in zahlreichen Abfragen wiederverwenden. Sie können Kriterien in einer Vorlage speichern und sie dann in mehreren Abfragen wiederverwenden. Wiederverwendbare SQL-Vorlagen reduzieren den Entwicklungsaufwand und auch das Fehlerrisiko beim Kopieren langer Anweisungen zwischen Abfragen. Mit Inline-Vorlagen können Sie Änderungen an einer Stelle vornehmen und diese Änderungen für jede Abfrage übernehmen lassen, die auf diese Vorlage verweist.

In diesem Dokument werden die Verwendung und die Einschränkungen von Inline-Vorlagen im Abfrage-Editor behandelt.

## Voraussetzungen

Inline-Vorlagen werden sowohl von der Benutzeroberfläche als auch von der Query Service-API unterstützt. Bevor Sie mit diesem Handbuch fortfahren, lesen Sie die Dokumentation zum [Erstellen einer Abfragevorlage über die API](../api/query-templates.md#create-a-query-template) oder mit dem [Abfrage-Editor](../ui/user-guide.md#query-authoring).

## Inline-Vorlagensyntax {#syntax}

Eine gespeicherte Abfrage wird als Vorlage bezeichnet. Wenn die Vorlage auf eine andere Vorlage in der Anweisung verweist, wird sie als Inline-Vorlage bezeichnet. Inline-Vorlagen sind in Ihrer SQL mit dem Hash-Symbol (#) gefolgt vom Vorlagennamen angegeben. Ein Beispiel für diese Syntax ist `#YOUR_TEMPLATE_NAME`.

## Anwendungsfall {#use-case}

Die folgenden SQL-Vorlagen veranschaulichen die Nützlichkeit von Inline-Vorlagen mit einem Beispiel zur Zählung der US-amerikanischen Kundinnen und Kunden aus allen Regionen, die mehr als den „maximalen Umsatz“ ausgegeben und vor Juni 2023 bestellt haben. Der Vorteil der Inline-Vorlage besteht darin, dass Sie die untergeordnete Vorlage (in diesem Fall der maximale Umsatz und das Bestelldatum) einfach bearbeiten können und die übergeordnete Vorlage nicht ändern müssen.

**Beispiel**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

Beim Ausführen der Abfrage ersetzt Query Service den Vorlagennamen ab dem Hash-Symbol durch die SQL-Anweisung der benannten Vorlage.

>[!NOTE]
>
>Abfragevorlagen können eine beliebige Anzahl anderer Inline-Vorlagen aufrufen. Die Anzahl der Inline-Vorlagen, die Sie aus einer einzigen Abfrage aufrufen können, ist nicht beschränkt. Vorlagen können auch in anderen Inline-Vorlagen verschachtelt werden.

Sie können Vorlagen verwenden, um eine oder mehrere Bedingungen zu speichern. Es muss sich nicht um eine vollständige Abfrage handeln. Wenn Ihre Vorlage eine gültige Abfrage enthält, können Sie die Abfrage ausführen, indem Sie einfach den Vorlagennamen mit einem vorangestellten Hash-Symbol aufrufen. Wenn Sie beispielsweise `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` als Vorlage mit dem Namen `JUNE_2023_LOYALTY_MEMBERS` gespeichert haben, wird mit dem Befehl  `#JUNE_2023_LOYALTY_MEMBERS;` die in der Vorlage enthaltene gültige Abfrage ausgeführt.

>
>
>In der Adobe Experience Platform-Benutzeroberfläche werden Inline-Vorlagen in Form parametrisierter Abfragen nur auf übergeordneter Ebene unterstützt. Dies bedeutet, dass parametrisierte Abfragen nur bei Verwendung in der ursprünglichen Vorlage funktionieren. Die untergeordnete Vorlage muss eine statische Vorlage sein und darf keine dynamischen Parameter aufweisen. Weitere Informationen finden Sie in der [Dokumentation zu parametrisierten Abfragen](../ui/parameterized-queries.md).

## Nächste Schritte

Nachdem Sie dieses Dokuments gelesen haben, wissen Sie nun, wie Sie auf andere Vorlagen in Ihrer SQL verweisen können – entweder im Abfrage-Editor oder über die Query Service-API.

Darüber hinaus sollten Sie das [Handbuch zu anonymen Blöcken](./anonymous-block.md) lesen. Darin wird erläutert, wie Sie den Entwicklungsaufwand minimieren können, indem Sie eine oder mehrere SQL-Anweisungen verketten, die nacheinander ausgeführt werden.
