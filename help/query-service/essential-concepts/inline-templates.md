---
title: Inline-Vorlagen
description: Erfahren Sie, wie Sie mehrere Bedingungen in zahlreichen Abfragen mit Inline-Vorlagen wiederverwenden können.
source-git-commit: f8ec94b4c93e3b36667bdb179ce12c10d20fa30f
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Inline-Vorlagen

Mit Inline-Vorlagen können Sie mehrere Bedingungen in zahlreichen Abfragen wiederverwenden. Sie können Kriterien in einer Vorlage speichern und sie dann in mehreren Abfragen wiederverwenden. Wiederverwendbare SQL-Vorlagen reduzieren den Entwicklungsaufwand und auch das Risiko von Fehlern beim Kopieren langer Anweisungen zwischen Abfragen. Mit Inline-Vorlagen können Sie Änderungen an einem Ort vornehmen und diese Änderungen in jeder Abfrage übernehmen lassen, die auf diese Vorlage verweist.

In diesem Dokument werden die Verwendung und die Einschränkungen von Inline-Vorlagen im Abfrage-Editor behandelt.

## Voraussetzungen

Inline-Vorlagen werden sowohl von der Benutzeroberfläche als auch von der Query Service-API unterstützt. Bevor Sie mit diesem Handbuch fortfahren, lesen Sie die Dokumentation zu [eine Abfragevorlage über die API erstellen](../api/query-templates.md#create-a-query-template) oder mit [Abfrage-Editor](../ui/user-guide.md#query-authoring).

## Inline-Vorlagensyntax {#syntax}

Nach dem Speichern einer Abfrage wird sie als Vorlage bezeichnet. Wenn die Vorlage auf eine andere Vorlage in der Anweisung verweist, wird sie als Inline-Vorlage bezeichnet. Inline-Vorlagen werden in Ihrer SQL mit dem Hash-Symbol (#) gefolgt vom Vorlagennamen gekennzeichnet. Ein Beispiel für diese Syntax ist `#YOUR_TEMPLATE_NAME`.

## Anwendungsfall {#use-case}

Die folgenden SQL-Vorlagen veranschaulichen die Nützlichkeit von Inline-Vorlagen mit einem Beispiel zur Zählung der US-Kunden aus allen Regionen, die mehr als den &quot;maximalen Umsatz&quot;ausgegeben und vor Juni 2023 bestellt haben. Der Vorteil der Inline-Vorlage besteht darin, dass Sie die untergeordnete Vorlage (in diesem Fall das maximale Umsatz- und Bestelldatum) einfach bearbeiten und die übergeordnete Vorlage nicht ändern müssen.

**Beispiel**

```sql
#parent_template : SELECT count(*) FROM customer WHERE region=NA AND country=US AND revenue > #revenue_max
#revenue_max: SELECT max(revenue) FROM revenue_table WHERE order_date > '01-06-2023'
```

Beim Ausführen der Abfrage ersetzt Query Service den Vorlagennamen, der vom Hash-Symbol beginnt, durch die SQL-Anweisung der benannten Vorlage.

>[!NOTE]
>
>Abfragevorlagen können eine beliebige Anzahl anderer Inline-Vorlagen aufrufen. Die Anzahl der Inline-Vorlagen, die Sie aus einer einzigen Abfrage aufrufen können, ist nicht beschränkt. Vorlagen können auch in anderen Inline-Vorlagen verschachtelt werden.

Sie können Vorlagen verwenden, um eine oder mehrere Bedingungen zu speichern. Sie müssen keine vollständige Abfrage sein. Wenn Ihre Vorlage eine gültige Abfrage enthält, können Sie die Abfrage ausführen, indem Sie einfach den Vorlagennamen aufrufen, dem ein Hash-Symbol vorangestellt ist. Wenn Sie beispielsweise `SELECT * FROM JUNE_2023_LOYALTY_MEMBERS;` als Vorlage mit dem Namen `JUNE_2023_LOYALTY_MEMBERS`, den Befehl  `#JUNE_2023_LOYALTY_MEMBERS;` die in der Vorlage enthaltene gültige Abfrage ausführen.

>
>
>In der Adobe Experience Platform-Benutzeroberfläche werden Inline-Vorlagen in Form parametrisierter Abfragen nur auf der übergeordneten Ebene unterstützt. Dies bedeutet, dass parametrisierte Abfragen nur bei Verwendung in der ursprünglichen Vorlage funktionieren. Die untergeordnete Vorlage muss eine statische Vorlage sein und darf keine dynamischen Parameter aufweisen.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie andere Vorlagen in Ihrer SQL referenzieren können, entweder im Abfrage-Editor oder über die Query Service-API.

Darüber hinaus sollten Sie die [Anonyme Blockanleitung](./anonymous-block.md)erläutert, wie Sie den Entwicklungsaufwand minimieren können, indem Sie eine oder mehrere SQL-Anweisungen verketten, die nacheinander ausgeführt werden.
