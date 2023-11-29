---
keywords: Experience Platform;Abfrage-Service;Abfrage-Service;verschachtelte Datenstrukturen;verschachtelte Daten;reduzieren;verschachtelte Daten reduzieren;
title: Reduzieren verschachtelter Datenstrukturen für die Verwendung mit BI-Tools
description: In diesem Dokument wird erläutert, wie Sie XDM-Schemata für alle Tabellen und Ansichten während einer Sitzung reduzieren, wenn Sie BI-Tools von Drittanbieterfirmen mit dem Abfrage-Service verwenden.
exl-id: 7e534c0a-db6c-463e-85da-88d7b2534ece
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 100%

---

# Reduzieren verschachtelter Datenstrukturen für die Verwendung mit BI-Tools von Drittanbieterfirmen

Der Abfrage-Service von Adobe Experience Platform unterstützt die `FLATTEN`-Einstellung für die Verbindung zu einer Datenbank über BI-Tools von Drittanbieterfirmen. Verschachtelte Datenstrukturen in BI-Tools von Drittanbieterfirmen können durch diese Funktion reduziert werden, um ihre Benutzungsfreundlichkeit zu verbessern und den erforderlichen Arbeitsaufwand für das Abrufen, Analysieren, Transformieren und Berichten von Daten zu reduzieren.

Viele BI-Tools wie [!DNL Tableau] und [!DNL Power BI] unterstützen standardmäßig keine verschachtelten Datenstrukturen. Durch die `FLATTEN`-Einstellung entfällt die Notwendigkeit, SQL-Ansichten über Ihren Daten zu erstellen, um eine reduzierte Version bereitzustellen, oder Abfrage-Service-`CTAS` oder `INSERT INTO`-Vorgänge zum Duplizieren Ihrer Datensätze in reduzierte Versionen bei Verwendung von Ad-hoc-Schemata einzusetzen.

Die `FLATTEN`-Einstellung zieht die Struktur der einzelnen Blattfelder in den Stamm der Tabelle und benennt das Feld nach dem ursprünglichen Namespace. Auf diese Weise können Sie Punktnotation verwenden, um ein Feld mit dem Experience-Datenmodell(XDM)-Pfad abzugleichen, während der Kontext des Felds beibehalten wird.

## Voraussetzungen

Die Nutzung der `FLATTEN`-Einstellung setzt ein Praxisverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [XDM-System](../../xdm/home.md): Allgemeine Übersicht über XDM und die Implementierung in Experience Platform.

   * [Erstellen eines Ad-hoc-Schemas](../../xdm/tutorials/ad-hoc.md): Ein XDM-Schema mit Feldern, die gemäß ihrem Namespace nur für die Verwendung durch einen einzigen Datensatz vorgesehen sind, wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schemata werden in verschiedenen Datenaufnahme-Workflows in Experience Platform und zur Erstellung bestimmter Quellverbindungen verwendet.

* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

* [Verschachtelte Datenstrukturen](./nested-data-structures.md): Dieses Dokument enthält Beispiele zum Erstellen, Verarbeiten oder Transformieren von Datensätzen mit komplexen Datentypen, einschließlich verschachtelter Datenstrukturen.

## Herstellen einer Verbindung zu einer Datenbank über die FLATTEN-Einstellung {#connect-with-flatten}

Durch die `FLATTEN`-Einstellung werden verschachtelte Datenstrukturen in separate Spalten reduziert, wobei der Attributname zum Spaltennamen wird, der die Zeilenwerte enthält. Beim Arbeiten mit Daten in BI-Tools, die keine verschachtelten Datenstrukturen unterstützen, verbessert diese Einstellung die Benutzerfreundlichkeit von Ad-hoc-Schemata und reduziert den erforderlichen Arbeitsaufwand.

Wenn Sie eine Verbindung zum Abfrage-Service mit Ihrem ausgewählten Drittanbieterfirma-Client herstellen, hängen Sie die `FLATTEN`-Einstellung an den Datenbanknamen an. Informationen zum Verbinden eines bestimmten BI-Tools finden Sie in der entsprechenden Dokumentation in der [Übersicht zum Verbinden von Clients mit dem Abfrage-Service](../clients/overview.md). Die Verbindungszeichenfolge sollte Folgendes enthalten:

* den Sandbox-Namen.
* einen Doppelpunkt gefolgt von `all` oder einer bestimmten Datensatz-ID, Anzeigen-ID oder einem Datenbanknamen.
* ein Fragezeichen (?) gefolgt vom Keyword `FLATTEN`.

Die Eingabe sollte das folgende Format aufweisen:

```terminal
{sandbox_name}:{all/ID/database_name}?FLATTEN
```

Eine Beispielverbindungszeichenfolge könnte wie folgt aussehen:

```terminal
prod:all?FLATTEN
```

## Beispiel {#example}

Das in diesem Handbuch verwendete Beispielschema verwendet die Standardfeldergruppe [!UICONTROL Commerce-Details], das die `commerce`-Objektstruktur und das `productListItems`-Array nutzt. Siehe XDM-Dokumentation für [weitere Informationen zur [!UICONTROL Commerce-Details]-Feldergruppe](../../xdm/field-groups/event/commerce-details.md). Eine Darstellung der Schemastruktur finden Sie in der Abbildung unten.

![Ein Schemadiagramm für die Commerce-Details-Feldergruppe, einschließlich der Strukturen `commerce` und `productListItems`.](../images/essential-concepts/commerce-details.png)

Wenn Ihr BI-Tool verschachtelte Datenstrukturen nicht unterstützt, kann es schwierig sein, verschachtelte Felder zu referenzieren, sofern sie serialisierte Werte enthalten (z. B. `commerce` und `productListItems` im Beispielschema). Diese Werte können als Teile eines einzelnen codierten `commerce`-Zeichenfolgenfelds auftreten und sind nicht realistisch unbenutzbar.

Die folgenden Werte stellen Folgendes dar: `commerce.order.priceTotal` (3018.0), `commerce.order.purchaseID` (c9b5aff9-25de-450b-98f4-4484a2170180) und `commerce.purchases.value`(1.0) in schlecht formatierten verschachtelten Feldern.

```terminal
("(3018.0,c9b5aff9-25de-450b-98f4-4484a2170180)","(1.0)")
```

Durch Verwendung der `FLATTEN`-Einstellung können Sie mithilfe der Punktnotation und des ursprünglichen Pfadnamens auf separate Felder innerhalb Ihres Schemas oder ganze Abschnitte der verschachtelten Datenstruktur zugreifen. Ein Beispiel für dieses Format mit der `commerce`-Feldergruppe finden Sie unten.

```terminal
commerce.order.priceTotal
commerce.order.purchaseID
commerce.purchases.value
```

Die `FLATTEN`-Einstellung hat beim Umgang mit anderen Datenstrukturen gewisse Einschränkungen. Ausführliche Informationen finden Sie im Abschnitt [Einschränkungen](#limitations).

### Verwenden von Anführungszeichen für Felder in Abfragen {#quotation-marks}

Die reduzierten Stammfelder verwenden jetzt Punktnotation, um ihren XDM-Pfaden zu entsprechen. Bei Verwendung in einer Abfrage müssen die Felder in Anführungszeichen (&quot; &quot;) gesetzt werden.

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

Die `FLATTEN`-Einstellung reduziert derzeit nicht die folgenden Datenstrukturen:

| Datenstruktur | Einschränkung |
|---|---|
| Arrays | Verwenden Sie einen expliziten Array-Index oder die `EXPLODE`-Funktion, um auf Arrays zuzugreifen. |
| Karten | Verwenden Sie den Zeichenfolgenschlüssel, um auf einen Wert unter einer Zuordnung und auf Zuordnungen zuzugreifen. |

Um sowohl Zuordnungs- als auch Array-Einschränkungen aufzuheben, müssen Sie die BI-Tools für die SQL-Rohbearbeitung wie die erweiterten Optionen -> SQL-Anweisung in Power BI verwenden.

BI-Tools wie die SQL-Rohbearbeitung sind erforderlich, um sowohl Zuordnungs- als auch Array-Einschränkungen zu beheben. Informationen finden Sie im Handbuch [Verwenden erweiterter Power BI-Optionen zur Eingabe einer benutzerdefinierten SQL-Abfrage](../clients/power-bi.md#import-tables-using-custom-sql) im Abschnitt mit den SQL-Anweisungen.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie verschachtelte Datenstrukturen für die Verwendung mit BI-Tools von Drittanbieterfirmen reduziert werden können. Wenn Sie noch keine Verbindung mit Ihrem Client hergestellt haben, finden Sie in der [Übersicht über Client-Verbindungen](../clients/overview.md) eine Liste unterstützter Drittanbieter-Clients.
