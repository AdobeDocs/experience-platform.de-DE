---
keywords: Experience Platform; Abfragedienst; Query Service; verschachtelte Datenstrukturen; verschachtelte Daten; reduzieren; reduzieren verschachtelte Daten;
title: Reduzieren verschachtelter Datenstrukturen für die Verwendung mit BI-Tools
description: In diesem Dokument wird erläutert, wie Sie XDM-Schemas für alle Tabellen und Ansichten während einer Sitzung reduzieren, wenn Sie BI-Tools von Drittanbietern mit Query Service verwenden.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 1c590350c9d519dba60375b92de7bbbbd77961dc
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 1%

---

# Reduzieren verschachtelter Datenstrukturen für die Verwendung mit BI-Tools von Drittanbietern

Adobe Experience Platform Query Service unterstützt `FLATTEN` Einstellung für die Verbindung zu einer Datenbank über BI-Tools von Drittanbietern. Diese Funktion reduziert verschachtelte Datenstrukturen in BI-Tools von Drittanbietern, um deren Benutzerfreundlichkeit zu verbessern und den erforderlichen Arbeitsaufwand zum Abrufen, Analysieren, Transformieren und Berichten von Daten zu reduzieren.

Viele BI-Tools wie [!DNL Tableau] und [!DNL Power BI] nativ keine verschachtelten Datenstrukturen unterstützen. Die `FLATTEN` entfällt die Notwendigkeit, SQL-Ansichten zusätzlich zu Ihren Daten zu erstellen, um eine flache Version bereitzustellen, oder Query Service zu verwenden `CTAS` oder `INSERT INTO` Aufträge zum Duplizieren Ihrer Datensätze in reduzierte Versionen bei Verwendung von Ad-hoc-Schemas.

Die `FLATTEN` -Einstellung zieht die Struktur der einzelnen Blattfelder in den Stamm der Tabelle und benennt das Feld nach dem ursprünglichen Namespace. Auf diese Weise können Sie Punktnotation verwenden, um ein Feld mit dem Experience-Datenmodell (XDM)-Pfad abzugleichen, während der Kontext des Felds beibehalten wird.

## Voraussetzungen

Verwenden der `FLATTEN` -Einstellung erfordert ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [XDM-System](../../xdm/home.md): Eine allgemeine Übersicht über XDM und dessen Implementierung in Experience Platform.

   * [Erstellen eines Ad-hoc-Schemas](../../xdm/tutorials/ad-hoc.md): Ein XDM-Schema mit Feldern, die nur für die Verwendung durch einen einzigen Datensatz benannt sind, wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schemata werden in verschiedenen Datenerfassungs-Workflows zur Experience Platform und Erstellung bestimmter Quellverbindungen verwendet.

* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

* [Verschachtelte Datenstrukturen](./nested-data-structures.md): Dieses Dokument enthält Beispiele zum Erstellen, Verarbeiten oder Transformieren von Datensätzen mit komplexen Datentypen, einschließlich verschachtelter Datenstrukturen.

## Verbindung zu einer Datenbank über die FLATTEN-Einstellung herstellen {#connect-with-flatten}

Die `FLATTEN` Durch die Einstellung werden verschachtelte Datenstrukturen in separate Spalten reduziert, wobei der Attributname zum Spaltennamen wird, der die Zeilenwerte enthält. Beim Arbeiten mit Daten in BI-Tools, die keine verschachtelten Datenstrukturen unterstützen, verbessert diese Einstellung die Benutzerfreundlichkeit von Ad-hoc-Schemata und reduziert den erforderlichen Arbeitsaufwand.

Wenn Sie eine Verbindung zu Query Service mit Ihrem ausgewählten Drittanbieter-Client herstellen, hängen Sie die `FLATTEN` auf den Datenbanknamen. Informationen zum Verbinden eines bestimmten BI-Tools finden Sie in der entsprechenden Dokumentation im [Clients mit Query Service verbinden - Übersicht](../clients/overview.md). Die Verbindungszeichenfolge sollte Folgendes enthalten:

* Der Sandbox-Name.
* Ein Doppelpunkt, gefolgt von `all` oder eine bestimmte Datensatz-ID, Anzeigen-ID oder Datenbankname.
* Ein Fragezeichen (?) gefolgt von `FLATTEN` Keyword.

Die Eingabe sollte das folgende Format aufweisen:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Eine Beispiel-Verbindungszeichenfolge könnte wie folgt aussehen:

```terminal
prod:all?FLATTEN
```

## Beispiel {#example}

Das in diesem Handbuch verwendete Beispielschema verwendet die Standardfeldgruppe [!UICONTROL Commerce-Details], das die `commerce` Objektstruktur und `productListItems` Array. Siehe XDM-Dokumentation für [Weitere Informationen über [!UICONTROL Commerce-Details] Feldergruppe](../../xdm/field-groups/event/commerce-details.md). Eine Darstellung der Schemastruktur finden Sie in der Abbildung unten.

![Ein Schemadiagramm für die Feldergruppe &quot;Commerce-Details&quot;, einschließlich der `commerce` und `productListItems` Strukturen.](../images/essential-concepts/commerce-details.png)

Wenn Ihr BI-Tool verschachtelte Datenstrukturen nicht unterstützt, kann es schwierig sein, verschachtelte Felder zu referenzieren, wenn sie serialisierte Werte enthalten (z. B. `commerce` und `productListItems` im Beispielschema). Diese Werte können als Teile eines einzelnen kodierten `commerce` Zeichenfolgenfeld und sind realistisch nicht verwendbar.

Die folgenden Werte stellen Folgendes dar: `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180) und `commerce.purchases.value`(1.0) in schlecht formatierten verschachtelten Feldern.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Durch Verwendung der Variablen `FLATTEN` -Einstellung können Sie mithilfe der Punktnotation und des ursprünglichen Pfadnamens auf separate Felder innerhalb Ihres Schemas oder ganze Abschnitte der verschachtelten Datenstruktur zugreifen. Ein Beispiel für dieses Format mit `commerce` Feldergruppe finden Sie unten.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

Die `FLATTEN` -Einstellung hat beim Umgang mit anderen Datenstrukturen gewisse Einschränkungen. Ausführliche Informationen finden Sie unter [Einschränkungen](#limitations).

### Anführungszeichen für Felder in Abfragen verwenden {#quotation-marks}

Die reduzierten Stammfelder verwenden jetzt Punktnotation, um ihren XDM-Pfaden zu entsprechen. Bei Verwendung in einer Abfrage müssen die Felder in Anführungszeichen (&quot;&quot;&quot;) gesetzt werden.

Im folgenden SQL-Beispiel wird der Originalzustand der verschachtelten Abfrage angezeigt:

```sql
SELECT YEAR(timestamp) AS year,
       SUM(commerce.order.priceTotal) AS revenue
FROM purchase_events_dataset
WHERE commerce.purchases.value > 0
GROUP BY 1;
```

Bei Verwendung der reduzierten Datenfelder wird die Abfrage mit Punktnotation geschrieben und in Anführungszeichen gesetzt, wie unten dargestellt:

```sql
SELECT YEAR(timestamp) AS year,
       SUM("commerce.order.priceTotal") AS revenue
FROM purchase_events_dataset
WHERE "commerce.purchases.value" > 0
GROUP BY 1;
```

## Einschränkungen {#limitations}

Die `FLATTEN` -Einstellung reduziert derzeit nicht die folgenden Datenstrukturen:

| Datenstruktur | Einschränkung |
|---|---|
| Arrays | Verwenden Sie einen expliziten Array-Index oder `EXPLODE` -Funktion, um auf Arrays zuzugreifen. |
| Karten | Verwenden Sie den Zeichenfolgenschlüssel, um auf einen Wert unter einer Zuordnung zuzugreifen und auf Zuordnungen zuzugreifen. |

Um sowohl Map- als auch Array-Einschränkungen zu beheben, müssen Sie die BI-Tools für die SQL-Rohbearbeitung wie die Erweiterte Optionen -> SQL-Anweisung in Power BI verwenden.

BI-Tools wie die Rohbearbeitung von SQL sind erforderlich, um sowohl Zuordnungs- als auch Array-Einschränkungen zu beheben. Informationen finden Sie im Handbuch [Verwenden Sie erweiterte Power BI-Optionen zur Eingabe einer benutzerdefinierten SQL-Abfrage](../clients/power-bi.md#import-tables-using-custom-sql) im Abschnitt SQL-Anweisung .

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie verschachtelte Datenstrukturen für die Verwendung mit BI-Tools von Drittanbietern reduziert werden. Wenn Sie noch keine Verbindung zu Ihrem Client hergestellt haben, lesen Sie [Übersicht über die Client-Verbindung](../clients/overview.md) für eine Liste unterstützter Drittanbieter-Clients.
