---
title: Effiziente Big-Data-Analyse mit Hypercubes im Experience Query Service
description: Erfahren Sie, wie Sie Hypercubes im Abfrage-Service von Adobe Experience Platform verwenden, um die Analyse von Big Data mit annähernder eindeutiger Zählung zu optimieren und so den Bedarf an vollständiger Neuverarbeitung von Daten zu reduzieren.
exl-id: 48af0003-0677-4828-982c-ebcbd9583e11
source-git-commit: 5550e757eae95e529d74115df9bbe9b635d25ec8
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 2%

---

# Effiziente Big-Data-Analyse mit Hypercubes

>[!AVAILABILITY]
>
>Diese Funktion steht nur Benutzenden zur Verfügung, die die [Data Distiller SKU](../data-distiller/overview.md) erworben haben. Weitere Informationen erhalten Sie von Ihrem Adobe-Support-Mitarbeiter.

Erfahren Sie, wie Sie im Experience Query Service von Adobe Experience Platform Hypercubes verwenden können, um eine erweiterte Datenanalyse mit verbesserter Effizienz durchzuführen. In diesem Dokument wird beschrieben, wie Sie erweiterte Funktionen aus der [[!DNL Apache Datasketches] Bibliothek](https://datasketches.apache.org/) verwenden können, um einzelne Zählungen und komplexe Berechnungen inkrementell zu verarbeiten, ohne historische Daten jedes Mal neu verarbeiten zu müssen.

In der Big-Data-Analyse umfasst das Generieren von Metriken wie eindeutige Zählungen, Quantile, häufigste Elemente, Joins und Diagrammanalysen häufig nicht-additive Zählungen (wobei die Ergebnisse nicht einfach aus Untergruppen zusammengefasst werden können). Herkömmliche Methoden erfordern die erneute Verarbeitung aller historischen Daten, was ressourcenintensiv und zeitaufwendig sein kann. Verwenden Sie Zeichnungen, bei denen es sich um kompakte Zusammenfassungen handelt, die Wahrscheinlichkeiten zur Darstellung großer Datensätze verwenden, und erweiterte Abfrage-Service-Funktionen, um diesen Prozess zu optimieren, indem Sie die Notwendigkeit der Neuberechnung reduzieren.

## Schlüsselfunktionen von Hyperwürfeln {#key-functions}

Hypercubes bieten mehrere leistungsstarke Funktionen zur Verbesserung der Effizienz und Flexibilität der Datenanalyse.

1. **Einzelne Benutzer oder einzelne Abfragen zählen**: Verwenden Sie SQL-Funktionen, um eine eindeutige Anzahl von Benutzern zu generieren, die mit verschiedenen Dimensionen von Daten interagieren, z. B. Produktansichten, Site-Besuche oder Commerce-Aktivitäten, ohne wiederholt Rohdaten erneut zu analysieren.
2. **Inkrementelle Verarbeitung**: Inkrementelle Aktualisierungen durchführen, um Datenpunkte über Dimensionen und Zeit hinweg zu falten und zusammenzuführen, ohne alles von Grund auf neu zu berechnen.
3. **Mehrdimensionale Analyse**: Hypercubes ermöglichen das mehrdimensionale Filtern und Neuanordnen von Daten, um Zusammenfassungszeilen zu erstellen, die Kombinationen von Dimensionen darstellen. Diese Zusammenfassungen können dann verwendet werden, um Einblicke mit minimalem Rechenaufwand zu generieren.

## Anwendungsbeispiele für Hyperwürfel {#use-cases}

Verwenden Sie Hypercubes, um effizient verschiedene Zählungen für verschiedene Benutzerinteraktionen zu generieren, ohne die Daten jedes Mal vollständig neu zu berechnen. Im Folgenden finden Sie einige praktische Szenarien für ihre Verwendung:

- Analysieren Sie Unique Visitors, die bestimmte Produkte während eines bestimmten Zeitraums anzeigen.
- Identifizieren Sie Benutzer, die in einem bestimmten Zeitraum mit mehreren Produkten interagieren, um die Crosssell-Analyse zu verbessern.
- Unterscheiden Sie Benutzer, die mit einem Produkt interagieren, aber mit der Zeit kein anderes, um Präferenzmuster zu entdecken.
- Kombinieren Sie Online- und Offline-Interaktionsdaten, um einen umfassenden Überblick über das Benutzerverhalten über einen bestimmten Zeitraum zu erhalten.
- Verfolgen Sie Benutzerbewegungen über verschiedene Aktivitäten innerhalb eines Ereignisses hinweg, um das Layout und die Services zu optimieren.

## Vorteile der Verwendung von Hypercubes

In diesen Situationen können Sie grundlegende Informationen für bestimmte Kategorien vorberechnen. Wenn Sie jedoch Daten über mehrere Dimensionen und Zeiträume hinweg analysieren, müssen Sie entweder alles aus den Rohdaten neu berechnen oder einen Abfrage-Service-Hypercube verwenden. Hypercubes optimieren den Prozess durch eine effiziente Organisation von Daten, die eine flexible Filterung und mehrdimensionale Analyse ohne erneute Verarbeitung ermöglicht. Sie nutzen erweiterte Funktionen für die schnelle und präzise Schätzung von Ergebnissen und bieten wichtige Vorteile wie verbesserte Verarbeitungseffizienz, Skalierbarkeit und Anpassungsfähigkeit für komplexe Analyseaufgaben.

### Datengrößeneffizienz bei der Abfrageverarbeitung

Query Service kann Millionen oder Milliarden von Datenpunkten (z. B. Benutzer-IDs) in eine kompakte Form komprimieren, die als Skizze bezeichnet wird. Diese Skizze hat eine erheblich reduzierte Datengröße für die Abfrageverarbeitung, was die Skalierbarkeit aufrechterhält und die Arbeit viel einfacher und schneller macht. Egal, wie groß die Originaldaten werden, die Größe der Skizze bleibt klein, was die Analyse von Big Data viel leichter handhabbar und effizienter macht.

Die folgende Abbildung zeigt, wie Commerce-, Produktinfo- und Web-Dimensions-ExperienceEvents in Zeichnungen verarbeitet werden, mit denen dann eindeutige Zahlen angenähert werden.

![Infografik, die die Erstellung von Zeichnungen mithilfe des Abfrage-Service zeigt. Das Diagramm veranschaulicht, wie ExperienceEvents mit Commerce, Produktinformationen und Web-Dimensionen in Zeichnungen verarbeitet werden, mit denen dann eindeutige Zahlen angenähert werden.](../images/hypercubes/hypercube-overview.png)

### Zusammenführen von Skizzen zur schnelleren und einfacheren Datenanalyse

Um Neuberechnungen zu vermeiden und die Verarbeitungsgeschwindigkeit zu erhöhen, können Sie Zeichnungen aus verschiedenen Kategorien oder Gruppen zusammenführen. Query Service vereinfacht auch das Design, indem es Ihre Daten in einem Hyperwürfel organisiert, wobei jede Zeile zu einer Zusammenfassung ihrer Partition (einer Sammlung von Dimensionen) neben der Skizzenspalte wird. Jede Zeile des Hyper-Cubes enthält die Dimensionskombination, verfügt jedoch über keine Rohdaten. Geben Sie beim Ausführen einer Abfrage die Dimensionsspalten an, die Sie zum Erstellen additiver Metriken verwenden möchten, und führen Sie die Skizzen für diese Zeilen zusammen.

![Das Diagramm zeigt, wie Zeichnungen aus verschiedenen ExperienceEvents zusammengeführt werden, um eine ungefähre eindeutige Anzahl über verschiedene Dimensionen hinweg zu erstellen.](../images/hypercubes/merge-sketches.png)

### Wirtschaftlichkeit {#cost-effectiveness}

Kundendaten sind oft sehr umfangreich, aber Sie können die Notwendigkeit beseitigen, historische Daten durch inkrementelle Verarbeitung erneut zu verarbeiten. Skizzen sind viel kleiner und ermöglichen schnellere Echtzeit-Ergebnisse bei gleichzeitiger Einsparung von Rechenressourcen und Kosten. Diese Datenumwandlung macht interaktive Abfragen praktikabler und effizienter.

## Funktionsübersicht

In diesem Abschnitt wird beschrieben, wie jede Funktion die Datenverarbeitung optimiert und die Analysefunktionen durch die effiziente Verwendung von Skizzen und Hyperwürfeln verbessert. Dort werden ihr Zweck, die Beispielsyntax, die Parameter und die erwartete Ausgabe beschrieben.

### Eindeutige Zählungsschätzungen mit HLL-Skizzen erstellen

`hll_build_agg` ist eine Aggregatfunktion, die eine HLL-Skizze (HyperLogLog) erstellt. Diese Funktion ist eine kompakte, probabilistische Methode zur Schätzung der Anzahl eindeutiger Werte innerhalb einer Spalte oder eines Ausdrucks in einem gruppierten Datensatz.

#### Definition der Funktion

```sql
hll_build_agg(column [, lgConfigK])
```

**Nutzung:**

Das folgende Beispiel zeigt, wie die Funktion in einer Abfrage strukturiert werden kann.

```sql
SELECT
   [dim1, dim2 ... ,] hll_build_agg(coalesce(col1, col2, col3)) AS sketch_col
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Parameter

| Parameter | Beschreibung |
|---------------------------|---------------------------------------|
| `column` | Die Spalte oder der Spaltenname, für die bzw. den eine Zeichnung erstellt werden soll. |
| `lgConfigK` | *Int* (Optional) Die log-base-2 von K, wobei K die Anzahl der Buckets oder Slots für die HLL-Skizze ist. Mindestwert: 4. Maximaler Wert: 12. Standardwert: 12. |

#### Ausgabe

| Ausgabespalte | Beschreibung |
|---------------------------|---------------------------------------|
| `sketch_res` | Eine Spalte vom Typ Zeichenfolge, die die stringisierte HLL-Skizze enthält. |

#### SQL-Beispiel

Im folgenden Beispiel wird eine Aggregatskizze für die `customer_id` erstellt:

```sql
SELECT
  country,
  hll_build_agg(customer_id, 10) AS sketch
FROM
  EXPLODE(
    ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
      ('UA', 'customer_id_1', 'invoice_id_11'),
      ('CZ', 'customer_id_2', 'invoice_id_22'),
      ('CZ', 'customer_id_2', 'invoice_id_23'),
      ('BR', 'customer_id_3', 'invoice_id_31'),
      ('UA', 'customer_id_2', 'invoice_id_24')
    ])
GROUP BY country;
```

**SQL-Beispielausgabe:**

| Land | Skizze |
|---------|------------------------------------------------------------|
| UA | AgEHBAMAAgCR9mUEulKKCQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| CZ | AgEHBAMAAQC6UooJAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| BR | AgEHBAMAAQCcmH0HAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |

### Schätzen der eindeutigen Anzahl mit HLL-Skizzen

`hll_estimate` ist eine Skalarfunktion, die eine Schätzung der eindeutigen Anzahl innerhalb jeder Zeile eines Datensatzes bereitstellt. Im Gegensatz zu Aggregatfunktionen arbeitet `hll_estimate` zeilenweise und wird für die Schätzung der eindeutigen Anzahl aus einer Skizze innerhalb einzelner Zeilen verwendet.

>[!NOTE]
>
>Diese Funktion kann nicht als aggregierte Funktion verwendet werden. Verwenden Sie für aggregierte Zählungen `sketch_count`.

#### Definition der Funktion

```sql
hll_estimate(sketch_col)
```

**Nutzung:**

Das folgende Beispiel zeigt, wie die Funktion in einer Abfrage strukturiert werden kann.

```sql
SELECT
   [col1, col2 ... ,] hll_estimate(sketch_column) AS estimate
FROM fact_sketch_table
```

#### Parameter

| Parameter | Beschreibung |
|---------------------------|---------------------------------------|
| `sketch_column` | Spalte, die eine stringisierte HLL-Skizze enthält. Es wird die eindeutige Anzahl für die Zeichnung in jeder Zeile geschätzt. |

#### Ausgabe

| Ausgabespalte | Beschreibung |
|---------------------------|---------------------------------------|
| `estimate` | Eine Spalte vom Typ double, die die Schätzung der Zeichnung liefert, gerundet auf zwei Dezimalstellen. |

#### SQL-Beispiel

Im folgenden Beispiel wird mithilfe der `hll_estimate` in einer HLL-Skizze die Anzahl der Kunden nach Land geschätzt:

```sql
SELECT
  country,
  hll_estimate(hll_build_agg(customer_id, 10)) AS distinct_customers_by_country
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id, 10) AS sketch
    FROM 
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
  );
```

**SQL-Beispielausgabe:**

| Land | distinct_customers_by_country |
|---------|-------------------------------|
| UA | 2,00 |
| CZ | 1,00 |
| BR | 1,00 |

### Zusammenführen mehrerer HLL-Skizzen mit `hll_merge_agg`

`hll_merge_agg` ist eine Aggregatfunktion, die mehrere HLL-Skizzen innerhalb einer Gruppe zusammenführt und eine neue Skizze als Ausgabe erzeugt. Es ermöglicht die Kombination von Skizzen über Partitionen oder Dimensionen hinweg, was die Flexibilität der Datenanalyse erhöht.

#### Definition der Funktion

```sql
hll_merge_agg(sketch_col [, allowDifferentLgConfigK])
```

**Nutzung:**

Das folgende Beispiel zeigt, wie die Funktion in einer Abfrage strukturiert werden kann.

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_agg(sketch_column.sketch) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Parameter

| Parameter | Beschreibung |
|---------------------------|---------------------------------------|
| `sketch_column` | Spalte, die die stringisierte HLL-Skizze enthält. |
| `allowDifferentLgConfigK` | *Boolesch* (Optional) Wenn „true“ festgelegt ist, können Zeichnungen mit unterschiedlichen `lgConfigK` zusammengeführt werden. Der Standardwert ist „false“. Es wird eine Ausnahme ausgelöst, wenn der Wert „false“ ist und Zeichnungen unterschiedliche `lgConfigK` haben. |

>[!NOTE]
>
>Wenn `allowDifferentLgConfigK` auf „false“ gesetzt ist, führt das Zusammenführen von Zeichnungen mit unterschiedlichen `lgConfigK` zu einem `UnsupportedOperationException`.

#### Ausgabe

| Ausgabespalte | Beschreibung |
|----------------|-------------------------------------------------|
| `sketch_res` | Eine Spalte vom Typ HLL-Skizze, die die stringierte zusammengeführte HLL-Skizze enthält. |

#### SQL-Beispiel

Im folgenden Beispiel werden mehrere HLL-Skizzen in der `customer_id` zusammengeführt:

```sql
SELECT
   hll_merge_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**SQL-Beispielausgabe:**

| Land | hll_merge_ag(Zeichnung, wahr) |
|---------|--------------------------------------------|
| UA | AgEHDAMAAwiR9mUEulKKCQAAAAAAAAAAAAAAAAAAAAAA== |
| CZ | AgEHDAMAAQi6UooJAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| BR | AgEHDAMAAQicmH0HAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| MX | AgEHFQMAAgiGL/kNdAAAAAAAAAAAAAAAAAAAAAAA== |

### Kardinalität mit `hll_merge_count_agg` schätzen

`hll_merge_count_agg` ist eine Aggregatfunktion, mit der die Kardinalität (Anzahl der eindeutigen Elemente) einer oder mehrerer Skizzen innerhalb einer Spalte geschätzt wird. Es wird eine einzelne Schätzung für alle in der Gruppierung auftretenden Zeichnungen zurückgegeben. Diese Funktion wird zum Aggregieren von Zeichnungen verwendet und kann nicht als zeilenweise Umwandlung verwendet werden. Verwenden Sie für zeilenweise Schätzungen `sketch_estimate`.

#### Definition der Funktion

```sql
hll_merge_count_agg(sketch_col [, allowDifferentLgConfigK])
```

**Nutzung:**

Das folgende Beispiel zeigt, wie die Funktion in einer Abfrage strukturiert werden kann.

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_count_agg(sketch_column) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Parameter

| Parameter | Beschreibung |
|-------------------------|----------------------------------------------|
| `sketch_column` | Eine Spalte, die die stringisierte HLL-Skizze enthält. |
| `allowDifferentLgConfigK` | *Boolesch* (optional) Der Standardwert ist „false“. Bei Wert „true“ können Zeichnungen mit unterschiedlichen `lgConfigK` zusammengeführt werden. Andernfalls wird eine `UnsupportedOperationException` ausgelöst. |

#### Ausgabe

| Ausgabespalte | Beschreibung |
|---------------|----------------------------------------------------------|
| `estimate` | Eine Spalte vom Typ Double, die die Schätzung der Skizze liefert. |

#### SQL-Beispiel

Im folgenden Beispiel wird die Anzahl der Unique Customers mit Rechnungen mithilfe der `hll_merge_count_agg`-Funktion geschätzt:

```sql
SELECT
   hll_merge_count_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**SQL-Beispielausgabe:**

| Land | hll_merge_count_ag(Zeichnung, wahr) |
|---------|----------------------------------|
| UA | 2.0 |
| CZ | 1,0 |
| BR | 1,0 |
| MX | 2.0 |

## Einschränkungen

Derzeit können Zeichnungen nach der Erstellung nicht aktualisiert werden. Bei zukünftigen Aktualisierungen wird die Funktion zum Aktualisieren von Zeichnungen eingeführt. Mit dieser Funktion können Sie verpasste Durchgänge und spät ankommende Daten effektiver verarbeiten.

## Nächste Schritte

Durch das Lesen dieses Dokuments wissen Sie jetzt, wie Sie Hyperwürfel und zugehörige Skizzenfunktionen verwenden können, um eine effiziente Datenverarbeitung für komplexe, mehrdimensionale Analysen durchzuführen, ohne historische Daten erneut verarbeiten zu müssen. Dieser Ansatz spart Zeit, senkt Kosten und bietet die Flexibilität, die für interaktive Abfragen in Echtzeit erforderlich ist. Dadurch ist er ein wertvolles Tool für die Analyse von Big Data in Adobe Experience Platform.

Erkunden Sie anschließend andere Schlüsselkonzepte wie [inkrementelles Laden](../key-concepts/incremental-load.md) und [Datendeduplizierung](../key-concepts/deduplication.md), um Ihr Verständnis dafür zu vertiefen, wie Sie diese Funktionen effektiv für Ihre spezifischen Datenanforderungen verwenden können.
