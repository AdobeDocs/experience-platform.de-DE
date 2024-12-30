---
title: Abrufen ähnlicher Datensätze mit Funktionen höherer Ordnung
description: Erfahren Sie, wie Sie ähnliche oder verwandte Datensätze aus einem oder mehreren Datensätzen basierend auf einer Ähnlichkeitsmetrik und einem Ähnlichkeitsschwellenwert identifizieren und abrufen können. Dieser Workflow kann aussagekräftige Beziehungen oder Überschneidungen zwischen unterschiedlichen Datensätzen hervorheben.
exl-id: 4810326a-a613-4e6a-9593-123a14927214
source-git-commit: 27eab04e409099450453a2a218659e576b8f6ab4
workflow-type: tm+mt
source-wordcount: '4031'
ht-degree: 3%

---

# Abrufen ähnlicher Datensätze mit Funktionen höherer Ordnung

Verwenden Sie Funktionen höherer Ordnung in Data Distiller, um eine Vielzahl gängiger Anwendungsfälle zu lösen. Um ähnliche oder verwandte Datensätze aus einem oder mehreren Datensätzen zu identifizieren und abzurufen, verwenden Sie die in diesem Handbuch beschriebenen Funktionen zum Filtern, Transformieren und Reduzieren. Informationen dazu, wie Funktionen höherer Ordnung zur Verarbeitung komplexer Datentypen verwendet werden können, finden Sie in der Dokumentation zu [Verwalten von Arrays und Zuordnen von Datentypen](../sql/higher-order-functions.md).

Verwenden Sie dieses Handbuch, um Produkte aus verschiedenen Datensätzen zu identifizieren, die in ihren Eigenschaften oder Attributen eine signifikante Ähnlichkeit aufweisen. Diese Methode bietet Lösungen für: Datendeduplizierung, Datensatzverknüpfung, Empfehlungssysteme, Informationsabruf und Textanalyse usw.

In diesem Dokument wird der Prozess der Implementierung eines Ähnlichkeits-Joins beschrieben, der dann mithilfe von Data Distiller-Funktionen höherer Ordnung die Ähnlichkeit zwischen Datensätzen berechnet und anhand ausgewählter Attribute filtert. SQL-Code-Snippets und Erläuterungen werden für jeden Schritt des Prozesses bereitgestellt. Der Workflow implementiert Ähnlichkeits-Joins mithilfe des Jaccard-Ähnlichkeitsmaßes und der Tokenisierung mithilfe von Data Distiller-Funktionen höherer Ordnung. Diese Methoden werden dann verwendet, um ähnliche oder verwandte Datensätze aus einem oder mehreren Datensätzen basierend auf einer Ähnlichkeitsmetrik zu identifizieren und abzurufen. Zu den wichtigsten Abschnitten des Prozesses gehören: [Tokenisierung mithilfe von Funktionen höherer Ordnung](#data-transformation) der [Cross-Join von eindeutigen Elementen](#cross-join-unique-elements) die [Jaccard-](#compute-the-jaccard-similarity-measure) und die [Schwellenwert-basierte Filterung](#similarity-threshold-filter).

## Voraussetzungen

Bevor Sie mit diesem Dokument fortfahren, sollten Sie mit den folgenden Konzepten vertraut sein:

- Ein **Ähnlichkeits-Join** ist ein Vorgang, der Datensatzpaare aus einer oder mehreren Tabellen identifiziert und abruft, basierend auf einem Maß der Ähnlichkeit zwischen den Datensätzen. Die wichtigsten Anforderungen für einen Ähnlichkeits-Join sind wie folgt:
   - **Ähnlichkeitsmetrik**: Ein Ähnlichkeitsverbund beruht auf einer vordefinierten Ähnlichkeitsmetrik oder -kennzahl. Zu diesen Metriken gehören: die Jaccard-Ähnlichkeit, die Kosinus-Ähnlichkeit, die Bearbeitungsentfernung usw. Die Metrik hängt von der Art der Daten und dem Anwendungsfall ab. Diese Metrik quantifiziert, wie ähnlich oder unähnlich zwei Datensätze sind.
   - **Schwellenwert**: Ein Ähnlichkeitsschwellenwert wird verwendet, um zu bestimmen, wann die beiden Datensätze als ähnlich genug betrachtet werden, um in das Join-Ergebnis aufgenommen zu werden. Datensätze mit einem Ähnlichkeitswert über dem Schwellenwert werden als Übereinstimmungen betrachtet.
- Der **Jaccard-Ähnlichkeits**-Index oder die Jaccard-Ähnlichkeitsmessung ist eine Statistik, die verwendet wird, um die Ähnlichkeit und Vielfalt von Beispielsätzen zu messen. Sie wird definiert als die Größe der Schnittmenge dividiert durch die Größe der Vereinigung der Stichprobensätze. Die Jaccard-Ähnlichkeitsmessung erfolgt im Bereich von null bis eins. Eine Jaccard-Ähnlichkeit von null zeigt keine Ähnlichkeit zwischen den Sätzen an, und eine Jaccard-Ähnlichkeit von eins zeigt an, dass die Sätze identisch sind.
  ![Ein Venn-Diagramm zur Veranschaulichung der Jaccard-Ähnlichkeitsmessung.](../images/use-cases/jaccard-similarity.png)
- **Funktionen höherer Ordnung** in Data Distiller sind dynamische Inline-Tools, die Daten direkt in SQL-Anweisungen verarbeiten und transformieren. Diese vielseitigen Funktionen machen mehrere Schritte bei der Datenbearbeitung überflüssig, insbesondere beim [Umgang mit komplexen Typen wie Arrays und Karten](../sql/higher-order-functions.md). Durch die Verbesserung der Abfrageeffizienz und die Vereinfachung von Transformationen tragen Funktionen höherer Ordnung zu einer agileren Analyse und besseren Entscheidungsfindung in verschiedenen Geschäftsszenarien bei.

## Erste Schritte

Die Data Distiller SKU ist erforderlich, um die übergeordneten Funktionen für Ihre Adobe Experience Platform-Daten auszuführen. Wenn Sie nicht über die Data Distiller SKU verfügen, wenden Sie sich an den Kundendienst von Adobe, um weitere Informationen zu erhalten.

## Ähnlichkeit herstellen {#establish-similarity}

Dieser Anwendungsfall erfordert ein Ähnlichkeitsmaß zwischen Textzeichenfolgen, das später verwendet werden kann, um einen Schwellenwert für die Filterung festzulegen. In diesem Beispiel stellen die Produkte in Satz A und Satz B die Wörter in zwei Dokumenten dar.

Das Jaccard-Ähnlichkeitsmaß kann auf eine Vielzahl von Datentypen angewendet werden, darunter Textdaten, kategoriale Daten und Binärdaten. Es eignet sich auch für die Echtzeit- oder Batch-Verarbeitung, da es für große Datensätze rechnereffizient berechnet werden kann.

Die Produktgruppen A und B enthalten die Testdaten für diesen Workflow.

- Produktsatz A: `{iPhone, iPad, iWatch, iPad Mini}`
- Produktsatz B: `{iPhone, iPad, Macbook Pro}`

Um die Jaccard-Ähnlichkeit zwischen den Produktsätzen A und B zu berechnen, suchen Sie zunächst die **Schnittmenge** (gemeinsame Elemente) der Produktsätze. In diesem Fall, `{iPhone, iPad}`. Suchen Sie als Nächstes **Vereinigung** (alle eindeutigen Elemente) beider Produktsätze. In diesem Beispiel `{iPhone, iPad, iWatch, iPad Mini, Macbook Pro}`.

Verwenden Sie abschließend die Jaccard-Ähnlichkeitsformel: `J(A,B) = A∪B / A∩B`, um die Ähnlichkeit zu berechnen.

J = Jaccard-Abstand
A = Satz 1
B = Satz 2

Die Jaccard-Ähnlichkeit zwischen den Produktsätzen A und B beträgt 0,4. Dies deutet auf eine mäßige Ähnlichkeit zwischen den in den beiden Dokumenten verwendeten Wörtern hin. Diese Ähnlichkeit zwischen den beiden Sätzen definiert die Spalten im Ähnlichkeitsjoin. Diese Spalten stellen Informationen oder Merkmale dar, die mit den Daten verknüpft sind und in einer Tabelle gespeichert sind und zur Durchführung der Ähnlichkeitsberechnungen verwendet werden.

### Paarweise Jaccard-Berechnung mit Zeichenfolgen-Ähnlichkeit {#pairwise-similarity}

Um die Ähnlichkeiten zwischen Zeichenfolgen genauer zu vergleichen, muss die paarweise Ähnlichkeit berechnet werden. Durch die paarweise Ähnlichkeit werden hochdimensionale Objekte in kleinere dimensionale Objekte zum Vergleich und zur Analyse aufgeteilt. Dazu wird eine Textzeichenfolge in kleinere Teile oder Einheiten (Token) unterteilt. Dabei kann es sich um einzelne Buchstaben, Buchstabengruppen (wie Silben) oder ganze Wörter handeln. Die Ähnlichkeit wird für jedes Token-Paar zwischen jedem Element in Satz A und jedem Element in Satz B berechnet. Diese Tokenisierung bietet eine Grundlage für analytische und computergestützte Vergleiche, Beziehungen und Einblicke, die aus den Daten gewonnen werden können.

Für die paarweise Ähnlichkeitsberechnung verwendet dieses Beispiel Zeichenbingramme (zwei Zeichen-Token), um eine Ähnlichkeitsübereinstimmung zwischen den Textzeichenfolgen der Produkte in Satz A und Satz B zu vergleichen. Ein Bigramm ist eine aufeinander folgende Folge von zwei Elementen oder Elementen in einer bestimmten Folge oder einem bestimmten Text. Man kann das auf Ngramme verallgemeinern.

In diesem Beispiel wird davon ausgegangen, dass die Groß-/Kleinschreibung keine Rolle spielt und dass Leerzeichen nicht berücksichtigt werden sollten. Nach diesen Kriterien weisen Satz A und Satz B die folgenden Bigramme auf:

Bi-Gramm-Produktset A:

- iPhone (5): „IP“, „PH“, „HO“, „ON“, „NE“
- iPad (3): „IP“, „PA“, „AD“
- iWatch (5): „iw“, „wa“, „at“, „tc“, „ch“
- iPad Mini (7): „ip“, „pa“, „ad“, „dm“, „mi“, „in“, „ni“

Bi-Gramm-Produktgruppe B:

- iPhone (5): „IP“, „PH“, „HO“, „ON“, „NE“
- iPad (3): „IP“, „PA“, „AD“
- MacBook Pro (9): „Ma“, „ac“, „cb“, „bo“, „oo“, „ok“, „kp“, „pr“, „ro“

Als Nächstes berechnen Sie den Jaccard-Ähnlichkeitskoeffizienten für jedes Paar:

|                   | iPhone (Satz B) | iPad (Satz B) | MacBook Pro (Set B) |
|-------------------|----------------------------------------------|---------------------------------------------|-------------------------------------------|
| iPhone (Satz A) | (Schnittmenge: 5, Vereinigung: 5) = 5 / 5 = 1 | (Schnittmenge: 1, Vereinigung: 7) =1 / 7 ≈ 0,14 | (Schnittmenge: 0, Vereinigung: 14) = 0 / 14 = 0 |
| iPad (Satz A) | (Schnittmenge: 1, Vereinigung: 7) = 1 / 7 ≈ 0,14 | (Schnittmenge: 3, Vereinigung: 3) = 3 / 3 = 1 | (Schnittmenge: 0, Vereinigung: 12) = 0 / 12 = 0 |
| iWatch (Set A) | (Schnittmenge: 0, Vereinigung: 8) = 0 / 8 = 0 | (Schnittmenge: 0, Vereinigung: 8) = 0 / 8 = 0 | (Schnittmenge: 0, Vereinigung: 8) = 0 / 8 =0 |
| iPad Mini (Set A) | (Schnittmenge: 1, Vereinigung: 11) = 1 / 11 ≈ 0,09 | (Schnittmenge: 3, Vereinigung: 7) = 3 / 7 ≈ 0,43 | (Schnittmenge: 0, Vereinigung: 16) = 0 / 16 = 0 |

{style="table-layout:auto"}

## Erstellen der Testdaten mit SQL {#create-test-data}

Um manuell eine Testtabelle für die Produktsätze zu erstellen, verwenden Sie die SQL CREATE TABLE-Anweisung.

```SQL {line-numbers="true"}
CREATE TABLE featurevector1 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'iWatch'
     UNION ALL
    SELECT 'iPad Mini'
);
SELECT * FROM featurevector1;
```

Die folgenden Beschreibungen enthalten eine Aufschlüsselung des obigen SQL-Code-Blocks:

- Zeile 1: `CREATE TEMP TABLE featurevector1 AS`: Diese Anweisung erstellt eine temporäre Tabelle mit dem Namen `featurevector1`. Temporäre Tabellen sind in der Regel nur innerhalb der aktuellen Sitzung zugänglich und werden automatisch am Ende der Sitzung entfernt.
- Zeile 1 und 2: `SELECT * FROM (...)`: Dieser Teil des Codes ist eine Unterabfrage, die zum Generieren der Daten verwendet wird, die in die `featurevector1` eingefügt werden.
Innerhalb der Unterabfrage werden mehrere `SELECT`-Anweisungen mithilfe des `UNION ALL`-Befehls kombiniert. Jede `SELECT`-Anweisung generiert eine Datenzeile mit den angegebenen Werten für die `ProductName`.
- Zeile 3: `SELECT 'iPad' AS ProductName`: Dadurch wird eine Zeile mit dem in der `ProductName` Spalte `iPad` Wert generiert.
- Zeile 5: `SELECT 'iPhone'`: Dadurch wird eine Zeile mit dem in der `ProductName` Spalte `iPhone` Wert generiert.

Die SQL-Anweisung erstellt eine Tabelle, wie unten dargestellt:

|   | `ProductName` |
|---|---------------|
| 1 | iPad |
| 2 | iPhone |
| 3 | iWatch |
| 4 | iPad Mini |

{style="table-layout:auto"}

Um den zweiten Merkmalsvektor zu erstellen, verwenden Sie die folgende SQL-Anweisung:

```SQL
CREATE TABLE featurevector2 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'Macbook Pro'
);
SELECT * FROM featurevector2;
```

## Datenumwandlungen {#data-transformation}

In diesem Beispiel müssen mehrere Aktionen ausgeführt werden, um die Sätze genau zu vergleichen. Zunächst werden Leerzeichen aus den Merkmalsvektoren entfernt, da angenommen wird, dass sie nicht zum Ähnlichkeitsmaß beitragen. Dann werden alle Duplikate im Merkmalsvektor entfernt, da sie die Rechenverarbeitung verschwenden. Als Nächstes werden Token aus zwei Zeichen (Bigramm) aus den Merkmalsvektoren extrahiert. In diesem Beispiel wird von einer Überlappung ausgegangen.

>[!NOTE]
>
>Zu Illustrationszwecken werden die verarbeiteten Spalten für jeden Schritt neben dem Merkmalsvektor hinzugefügt.

Die folgenden Abschnitte veranschaulichen die erforderlichen Datenumwandlungen wie Deduplizierung, Entfernen von Leerzeichen und Konvertierung in Kleinbuchstaben, bevor der Prozess der Tokenisierung gestartet wird.

### Deduplizierung {#deduplication}

Verwenden Sie anschließend die `DISTINCT`-Klausel, um Duplikate zu entfernen. In diesem Beispiel gibt es keine Duplikate. Es ist jedoch ein wichtiger Schritt, die Genauigkeit eines Vergleichs zu verbessern. Die erforderliche SQL wird unten angezeigt:

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct FROM featurevector1
SELECT DISTINCT(ProductName) AS featurevector2_distinct FROM featurevector2
```

### Entfernung von Leerzeichen {#whitespace-removal}

In der folgenden SQL-Anweisung werden die Leerzeichen aus den Funktionsvektoren entfernt. Der `replace(ProductName, ' ', '') AS featurevector1_nospaces` Teil der Abfrage übernimmt die `ProductName` aus der `featurevector1` und verwendet die `replace()`. Die Funktion `REPLACE` ersetzt alle Vorkommen eines Leerzeichens (&#39; &#39;) durch eine leere Zeichenfolge (&#39;&#39;). Dadurch werden effektiv alle Leerzeichen aus den `ProductName` entfernt. Das Ergebnis wird als `featurevector1_nospaces` Alias angegeben.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, replace(ProductName, ' ', '') AS featurevector1_nospaces FROM featurevector1
```

Die Ergebnisse sind in der folgenden Tabelle aufgeführt:

|   | featureVector1_distinct | featureVector1_nospaces |
|---|---|---|
| 1 | iPad Mini | iPadMini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

Die SQL-Anweisung und ihre Ergebnisse für den zweiten Merkmalsvektor werden unten angezeigt:

+++Zum Erweitern auswählen

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, replace(ProductName, ' ', '') AS featurevector2_nospaces FROM featurevector2
```

Die Ergebnisse werden wie folgt angezeigt:

|   | featureVector2_distinct | featureVector2_nospaces |
|---|---|---|
| 1 | iPad | iPad |
| 2 | MacBook Pro | MacBookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### In Kleinbuchstaben umwandeln {#lowercase-conversion}

Anschließend wird die SQL verbessert, um die Produktnamen in Kleinbuchstaben zu konvertieren und alle Leerzeichen zu entfernen. Die untere Funktion (`lower(...)`) wird auf das Ergebnis der `replace()` angewendet. Die Funktion LOWER wandelt alle Zeichen der geänderten `ProductName` in Kleinbuchstaben um. Dadurch wird sichergestellt, dass die Werte unabhängig von ihrer ursprünglichen Groß-/Kleinschreibung in Kleinbuchstaben geschrieben werden.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform FROM featurevector1;
```

Das Ergebnis dieser Anweisung ist:

|   | featureVector1_distinct | featureVector1_transform |
|---|---|---|
| 1 | iPad Mini | IPadmini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

Die SQL-Anweisung und ihre Ergebnisse für den zweiten Merkmalsvektor werden unten angezeigt:

+++Zum Erweitern auswählen

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, lower(replace(ProductName, ' ', '')) AS featurevector2_transform FROM featurevector2
```

Die Ergebnisse werden wie folgt angezeigt:

|   | featureVector2_distinct | featureVector2_transform |
|---|---|---|
| 1 | iPad | iPad |
| 2 | MacBook Pro | macBookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### Extrahieren von Token mithilfe von SQL {#tokenization}

Der nächste Schritt ist Tokenisierung oder Textaufteilung. Bei der Tokenisierung wird Text in einzelne Begriffe aufgeteilt. Typischerweise beinhaltet dies, Sätze in Wörter aufzuteilen. In diesem Beispiel werden Zeichenfolgen in Bigramme (und höherrangige N-Gramme) aufgeteilt, indem Token mithilfe von SQL-Funktionen wie `regexp_extract_all` extrahiert werden. Für eine effektive Tokenisierung müssen sich überschneidende Bigramme generiert werden.

Die SQL-Abfrage wurde weiter verbessert, um `regexp_extract_all` zu verwenden. `regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0) AS tokens:` Dieser Teil der Abfrage verarbeitet die im vorherigen Schritt erstellten geänderten `ProductName` weiter. Es verwendet die `regexp_extract_all()`-Funktion, um alle nicht überlappenden Teilzeichenfolgen von einem bis zwei Zeichen aus den geänderten `ProductName` in Kleinbuchstaben zu extrahieren. Das Muster für `.{2}` reguläre Ausdrücke sucht nach Teilzeichenfolgen mit einer Länge von zwei Zeichen. Der `regexp_extract_all(..., '.{2}', 0)` Teil der Funktion extrahiert dann alle übereinstimmenden Teilzeichenfolgen aus dem Eingabetext.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
regexp_extract_all(lower(replace(ProductName, ' ', '')) , '.{2}', 0) AS tokens
FROM featurevector1;
```

Die Ergebnisse sind in der folgenden Tabelle aufgeführt:

+++Zum Erweitern auswählen

|   | featureVector1_distinct | featureVector1_transform | Token |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | IPadmini | {„IP“,„AD“,„MI“,„NI“} |
| 2 | iPad | iPad | {„IP“,„AD“} |
| 3 | iWatch | iWatch | {„iw“,„at“, „ch“} |
| 4 | iPhone | iPhone | {„IP“,„HO“,„NE“} |

{style="table-layout:auto"}

+++

Um die Genauigkeit weiter zu verbessern, muss die SQL verwendet werden, um sich überschneidende Token zu erstellen. Bei der obigen Zeichenfolge &quot;iPad&quot; fehlt beispielsweise das Token „pa“. Um dies zu beheben, verschieben Sie den Lookahead-Operator (mit `substring`) um einen Schritt und generieren Sie die Bi-Gramme.

Ähnlich wie im vorherigen Schritt extrahiert `regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0):` aus dem geänderten Produktnamen zweistellige Sequenzen, beginnt jedoch mit dem zweiten Zeichen unter Verwendung der `substring`-Methode, um überlappende Token zu erstellen. Als Nächstes kombiniert die Funktion `array_union()` in den Zeilen 3-7 (`array_union(...) AS tokens`) die Arrays von zweistelligen Sequenzen, die durch die beiden Extraktionen regulärer Ausdrücke erhalten werden. Dadurch wird sichergestellt, dass das Ergebnis eindeutige Token aus nicht überlappenden und überlappenden Sequenzen enthält.

```SQL {line-numbers="true"}
SELECT DISTINCT(ProductName) AS featurevector1_distinct, 
       lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
       array_union(
           regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0),
           regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0)
       ) AS tokens
FROM featurevector1;
```

Die Ergebnisse sind in der folgenden Tabelle aufgeführt:

+++Zum Erweitern auswählen

|   | featureVector1_distinct | featureVector1_transform | Token |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | IPadmini | {„IP“,„AD“,„MI“,„NI“,„PA“,„DM“,„IN“} |
| 2 | iPad | iPad | {„IP“,„AD“,„PA“} |
| 3 | iWatch | iWatch | {„iw“,„at“,„ch“,„wa“,„tc“} |
| 4 | iPhone | iPhone | {„IP“,„HO“,„NE“,„PH“,„ON“} |

{style="table-layout:auto"}

+++

Die Verwendung von `substring` als Lösung des Problems weist jedoch Einschränkungen auf. Wenn Sie Token aus dem Text erstellen würden, der auf Dreigrammen (drei Zeichen) basiert, würde es die Verwendung von zwei `substrings` erfordern, zweimal nach vorne zu schauen, um die erforderlichen Verschiebungen zu erhalten. Um 10 Gramm zu machen, bräuchte man neun `substring`. Dadurch würde der Code aufgebläht und unhaltbar werden. Die Verwendung einfacher regulärer Ausdrücke ist nicht geeignet. Wir brauchen einen neuen Ansatz.

### Anpassen der Länge des Produktnamens {#length-adjustment}

Mit den Abfolge- und Längenfunktionen lässt sich der SQl verbessern. Im folgenden Beispiel generiert `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3)` eine Zahlenfolge von 1 bis zur Länge des geänderten Produktnamens minus 3. Wenn der geänderte Produktname beispielsweise „ipadmini“ mit einer Zeichenlänge von acht lautet, werden Zahlen von eins bis fünf (acht bis drei) generiert.

Die nachstehende Anweisung extrahiert eindeutige Produktnamen und unterteilt dann jeden Namen in Sequenzen von Zeichen (Token) mit vier Zeichenlängen, wobei Leerzeichen ausgeschlossen werden, und stellt sie als zwei Spalten dar. Eine Spalte zeigt die eindeutigen Produktnamen und die andere Spalte zeigt die generierten Token.

```SQL
SELECT
   DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 4)
  ) AS tokens
FROM
  featurevector1;
```

Die Ergebnisse sind in der folgenden Tabelle aufgeführt:

+++Zum Erweitern auswählen

|   | featureVector1_distinct | Token |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {„iPad“,„padm“,„admin“,„admin“,„mini“} |
| 2 | iPad | {„iPad“} |
| 3 | iWatch | {„iwat“,„watch“,„watch“} |
| 4 | iPhone | {„ipho“,„phon“,„phone“} |

{style="table-layout:auto"}

+++

### Festlegen der Token-Länge {#ensure-set-token-length}

Der Anweisung können zusätzliche Bedingungen hinzugefügt werden, um sicherzustellen, dass die generierten Sequenzen eine bestimmte Länge aufweisen. Die folgende SQL-Anweisung erweitert die Token-Generierungslogik, indem sie die `transform` komplexer macht. Die Anweisung verwendet die Funktion `filter` in `transform`, um sicherzustellen, dass die generierten Sequenzen sechs Zeichen lang sind. Es behandelt die Fälle, in denen dies nicht möglich ist, indem NULL-Werte diesen Positionen zugewiesen werden.

```SQL
SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 5),
      i -> i + 5 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 6)) = 6
               THEN substring(lower(replace(ProductName, ' ', '')), i, 6)
               ELSE NULL
          END
  ) AS tokens
FROM
  featurevector1;
```

Die Ergebnisse sind in der folgenden Tabelle aufgeführt:

+++Zum Erweitern auswählen

|   | featureVector1_distinct | Token |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {„ipadmin“,„padmin“,„admin“} |
| 2 | iPad | {null} |
| 3 | iWatch | {„iWatch“} |
| 4 | iPhone | {„iPhone“} |

{style="table-layout:auto"}

+++

## Erkunden von Lösungen mit Data Distiller-Funktionen höherer Ordnung {#higher-order-function-solutions}

Funktionen höherer Ordnung sind leistungsstarke Konstrukte, mit denen Sie „Programmierung“ wie Syntax in Data Distiller implementieren können. Sie können verwendet werden, um eine Funktion über mehrere Werte in einem Array zu iterieren.

Im Kontext von Data Distiller eignen sich Funktionen höherer Ordnung ideal für die Erstellung von N-Grammen und die Iteration über Zeichenfolgen.

Die `reduce` Funktion bietet insbesondere bei Verwendung in von `transform` erzeugten Sequenzen die Möglichkeit, kumulative Werte oder Aggregate abzuleiten, die in verschiedenen Analyse- und Planungsprozessen von zentraler Bedeutung sein können.

In der folgenden SQL-Anweisung aggregiert die Funktion `reduce()` beispielsweise Elemente in einem Array mithilfe eines benutzerdefinierten Aggregators. Es simuliert eine for-Schleife, um **die kumulativen Summen aller Ganzzahlen zu erstellen** von 1 bis 5. `1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4`.

```SQL {line-numbers="true"}
SELECT transform(
    sequence(1, 5), 
    x -> reduce(
        sequence(1, x),  
        0,  -- Initial accumulator value
        (acc, y) -> acc + y  -- Higher-order function to add numbers
    )
) AS sum_result;
```

Im Folgenden finden Sie eine Analyse der SQL-Anweisung:

- Zeile 1: `transform` wendet die Funktion `x -> reduce` auf jedes Element an, das in der Sequenz generiert wurde.
- Zeile 2: `sequence(1, 5)` generiert eine Zahlenfolge von 1 bis 5.
- Zeile 3: `x -> reduce(sequence(1, x), 0, (acc, y) -> acc + y)` führt für jedes Element x in der Sequenz (von 1 bis 5) einen Reduktionsvorgang durch.
   - Die Funktion `reduce` benötigt einen anfänglichen Akkumulatorwert von 0, eine Sequenz von 1 bis zum aktuellen Wert von `x` und eine Funktion höherer Ordnung, `(acc, y) -> acc + y` die Zahlen hinzuzufügen.
   - Die Funktion höherer Ordnung sammelt `acc + y` Summe durch Addition des aktuellen `y` zum `acc`.
- Zeile 8: `AS sum_result` benennt die resultierende Spalte in „sum_result“ um.

Zusammenfassend lässt sich sagen, dass diese Funktion höherer Ordnung zwei Parameter (`acc` und `y`) annimmt und den auszuführenden Vorgang definiert, der in diesem Fall das Hinzufügen von `y` zur `acc` des Akkumulators ist. Diese Funktion höherer Ordnung wird für jedes Element in der Sequenz während des Reduktionsprozesses ausgeführt.

Die Ausgabe dieser Anweisung ist eine einzelne Spalte (`sum_result`), die die kumulativen Summen von Zahlen von 1 bis 5 enthält.

### Der Wert von Funktionen höherer Ordnung {#value-of-higher-order-functions}

In diesem Abschnitt wird eine abgespeckte Version einer Drei-Gramm-SQL-Anweisung analysiert, um den Wert von Funktionen höherer Ordnung in Data Distiller besser zu verstehen, um N-Gramm effizienter zu erstellen.

Die folgende Anweisung bezieht sich auf die `ProductName` in der `featurevector1`. Es erzeugt einen Satz von dreistelligen Teilzeichenfolgen, die aus den geänderten Produktnamen innerhalb der Tabelle abgeleitet werden, wobei Positionen verwendet werden, die aus der generierten Sequenz erhalten wurden.

```SQL {line-numbers="true"}
SELECT
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 3)
  ) 
FROM
  featurevector1
```

Im Folgenden finden Sie eine Analyse der SQL-Anweisung:

- Zeile 2: `transform` wendet auf jede Ganzzahl in der Sequenz eine Funktion höherer Ordnung an.
- Zeile 3: `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2)` generiert eine Sequenz von Ganzzahlen von `1` bis zur Länge des geänderten Produktnamens minus zwei.
   - `length(lower(replace(ProductName, ' ', '')))` berechnet die Länge des `ProductName`, nachdem er in Kleinbuchstaben geschrieben und Leerzeichen entfernt wurde.
   - `- 2` subtrahiert zwei von der Länge, um sicherzustellen, dass die Sequenz gültige Startpositionen für 3-stellige Teilzeichenfolgen erzeugt. Durch die Subtraktion von 2 wird sichergestellt, dass jeder Startposition genügend Zeichen folgen, um eine 3-stellige Teilzeichenfolge zu extrahieren. Die Teilzeichenfolgen-Funktion funktioniert hier wie ein Lookahead-Operator.
- Zeile 4: `i -> substring(lower(replace(ProductName, ' ', '')), i, 3)` ist eine Funktion höherer Ordnung, die auf jede ganzzahlige `i` in der generierten Sequenz angewendet wird.
   - Die `substring(...)`-Funktion extrahiert eine 3-stellige Teilzeichenfolge aus der `ProductName`.
   - Vor dem Extrahieren der Teilzeichenfolge wandelt `lower(replace(ProductName, ' ', ''))` die `ProductName` in Kleinbuchstaben um und entfernt Leerzeichen, um die Konsistenz sicherzustellen.

Die Ausgabe ist eine Liste von Unterzeichenfolgen mit drei Zeichen Länge, die aus den geänderten Produktnamen extrahiert werden, basierend auf den in der Sequenz angegebenen Positionen.

## Filtern der Ergebnisse {#filter-results}

Die `filter`-Funktion mit anschließenden [Datenumwandlungen](#data-transformation) ermöglicht eine verfeinerte und präzisere Extraktion relevanter Informationen aus Textdaten. Auf diese Weise können Sie Erkenntnisse gewinnen, die Datenqualität verbessern und bessere Entscheidungsprozesse ermöglichen.

Die Funktion `filter` in der folgenden SQL-Anweisung dient dazu, die Sequenz von Positionen innerhalb der Zeichenfolge, aus denen Teilzeichenfolgen mit der nachfolgenden Transformationsfunktion extrahiert werden, zu verfeinern und zu begrenzen.

```SQL
SELECT
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 6),
      i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 7)) = 7
               THEN substring(lower(replace(ProductName, ' ', '')), i, 7)
               ELSE NULL
          END
  )
FROM
  featurevector1;
```

Die `filter`-Funktion erzeugt eine Sequenz gültiger Startpositionen innerhalb der modifizierten `ProductName` und extrahiert Teilzeichenfolgen einer bestimmten Länge. Es sind nur Startpositionen zulässig, die die Extraktion einer siebenstelligen Teilzeichenfolge ermöglichen.

Die Bedingung `i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))` stellt sicher, dass die Startposition `i` plus `6` (die Länge der gewünschten siebenstelligen Teilzeichenfolge minus eins) die Länge der geänderten `ProductName` nicht überschreitet.

Die `CASE` Anweisung wird verwendet, um Teilzeichenfolgen basierend auf ihrer Länge bedingt ein- oder auszuschließen. Nur siebenteilige Unterzeichenfolgen sind enthalten; andere werden durch NULL ersetzt. Diese Unterzeichenfolgen werden dann von der Funktion `transform` verwendet, um eine Sequenz von Unterzeichenfolgen aus der Spalte `ProductName` in der `featurevector1` zu erstellen.

>[!TIP]
>
>Sie können die Funktion [parametrisierte Vorlagen](../ui/parameterized-queries.md) verwenden, um Logik in Ihren Abfragen wiederzuverwenden und zu abstrahieren. Wenn Sie beispielsweise allgemeine Dienstprogrammfunktionen (wie die oben für das Tokenisieren von Zeichenfolgen angezeigte) erstellen, können Sie parametrisierte Data Distiller-Vorlagen verwenden, bei denen die Anzahl der Zeichen ein Parameter wäre.

## Berechnung der Kreuzverbindung eindeutiger Elemente über zwei Merkmalsvektoren {#cross-join-unique-elements}

Das Identifizieren der Unterschiede oder Diskrepanzen zwischen den beiden Datensätzen auf der Grundlage einer bestimmten Transformation der Daten ist ein gängiger Prozess, um die Datengenauigkeit aufrechtzuerhalten, die Datenqualität zu verbessern und die Konsistenz über Datensätze hinweg sicherzustellen.

Mit der folgenden SQL-Anweisung werden die eindeutigen Produktnamen extrahiert, die nach der Anwendung der Transformationen in `featurevector2`, aber nicht in `featurevector1` vorhanden sind.

```SQL
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector2
EXCEPT
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector1;
```

>[!TIP]
>
>Zusätzlich zu `EXCEPT` können Sie je nach Anwendungsfall auch `UNION` und `INTERSECT` verwenden. Außerdem können Sie mit `ALL`- oder `DISTINCT`-Klauseln experimentieren, um den Unterschied zwischen dem Einschließen aller Werte und dem Zurückgeben nur der eindeutigen Werte für die angegebenen Spalten zu sehen.

Die Ergebnisse sind in der folgenden Tabelle aufgeführt:

+++Zum Erweitern auswählen

|   | lower(replace(ProductName, &#39; &#39;, &#39;&#39;)) |
|---|---------------------------------------|
| 1 | macBookPro |

{style="table-layout:auto"}

+++

Führen Sie anschließend eine Kreuzverknüpfung durch, um Elemente aus den beiden Elementvektoren zu kombinieren und Elementpaare für einen Vergleich zu erstellen. Der erste Schritt in diesem Prozess besteht darin, einen Token-basierten Vektor zu erstellen.

Ein Token-Vektor ist eine strukturierte Darstellung von Textdaten, bei der jedes Wort, jede Wortgruppe oder jede Bedeutungseinheit (Token) in ein numerisches Format konvertiert wird. Diese Konversion ermöglicht es Algorithmen zur Verarbeitung natürlicher Sprachen, Textinformationen zu verstehen und zu analysieren.

Der unten stehende SQL-Code erstellt einen Token-Vektor.

```SQL
CREATE TABLE featurevector1tokenized AS SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
  (SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector1);
SELECT * FROM featurevector1tokenized;
```

>[!NOTE]
>
>Wenn Sie [!DNL DbVisualizer] verwenden, aktualisieren Sie nach dem Erstellen oder Löschen einer Tabelle die Datenbankverbindung, damit der Metadaten-Cache der Tabelle aktualisiert wird. Data Distiller sendet keine Metadatenaktualisierungen.

Die Ergebnisse sind in der folgenden Tabelle aufgeführt:

+++Zum Erweitern auswählen

|   | featureVector1_distinct | Token |
|---|--------------------------|------------------------|
| 1 | IPadmini | {„IP“,„PA“,„AD“,„DM“,„MI“,„IN“,„NI“} |
| 2 | iPad | {„IP“,„PA“,„AD“} |
| 3 | iWatch | {„iw“,„wa“,„at“,„tc“,„ch“} |
| 4 | iPhone | {„IP“,„PH“,„HO“,„ON“,„NE“} |

{style="table-layout:auto"}

+++

Wiederholen Sie dann den Vorgang für `featurevector2`:

```SQL
CREATE TABLE featurevector2tokenized AS 
SELECT
  DISTINCT(ProductName) AS featurevector2_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
(SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector2
);
SELECT * FROM featurevector2tokenized;
```

Die Ergebnisse sind in der folgenden Tabelle aufgeführt:

+++Zum Erweitern auswählen

|   | featureVector2_distinct | Token |
|---|--------------------------|------------------------|
| 1 | IPadmini | {„IP“,„PA“,„AD“} |
| 2 | macBookPro | {„ma“,„ac“,„cb“,„bo“,„oo“,„ok“,„kp“,„pr“,„ro“} |
| 3 | iPhone | {„IP“,„PH“,„HO“,„ON“,„NE“} |

{style="table-layout:auto"}

+++

Nachdem beide Token-Vektoren abgeschlossen sind, können Sie jetzt die Kreuzverknüpfung erstellen. Dies wird in der folgenden SQL angezeigt:

```SQL {line-numbers="true"}
SELECT
    A.featurevector1_distinct AS SetA_ProductNames,
    B.featurevector2_distinct AS SetB_ProductNames,
    A.tokens AS SetA_tokens1,
    B.tokens AS SetB_tokens2
FROM
    featurevector1tokenized A
CROSS JOIN
    featurevector2tokenized B;
```

Im Folgenden finden Sie eine Zusammenfassung des SQL-Codes, der zum Erstellen des Querverweises verwendet wurde:

- Zeile 2: `A.featurevector1_distinct AS SetA_ProductNames` wählt die Spalte `featurevector1_distinct` aus der `A` aus und weist ihr einen `SetA_ProductNames` zu. Dieser Abschnitt von SQL führt zu einer Liste mit unterschiedlichen Produktnamen aus dem ersten Datensatz.
- Zeile 4: `A.tokens AS SetA_tokens1` wählt die `tokens` aus der Tabelle oder der `A` aus und weist ihr einen `SetA_tokens1` zu. Dieser Abschnitt von SQL führt zu einer Liste von Token-Werten, die mit den Produktnamen aus dem ersten Datensatz verknüpft sind.
- Zeile 8: Der `CROSS JOIN` Vorgang kombiniert alle möglichen Kombinationen von Zeilen aus den beiden Datensätzen. Mit anderen Worten: Es paart jeden Produktnamen und seine zugehörigen Token aus der ersten Tabelle (`A`) mit jedem Produktnamen und seinen zugehörigen Token aus der zweiten Tabelle (`B`). Dies führt zu einem kartesischen Produkt der beiden Datensätze, wobei jede Zeile in der Ausgabe eine Kombination aus einem Produktnamen und den zugehörigen Token aus beiden Datensätzen darstellt.

Die Ergebnisse sind in der folgenden Tabelle aufgeführt:

+++Zum Erweitern auswählen

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 |
|---|---------------------|-------------------|---|---|
| 1 | IPadmini | iPad | {„IP“,„PA“,„AD“,„DM“,„MI“,„IN“,„NI“} | {„IP“,„PA“,„AD“} |
| 2 | IPadmini | macBookPro | {„IP“,„PA“,„AD“,„DM“,„MI“,„IN“,„NI“} | {„ma“,„ac“,„cb“,„bo“,„oo“,„ok“,„kp“,„pr“,„ro“} |
| 3 | IPadmini | iPhone | {„IP“,„PA“,„AD“,„DM“,„MI“,„IN“,„NI“} | {„IP“,„PH“,„HO“,„ON“,„NE“} |
| 4 | iPad | iPad | {„IP“,„PA“,„AD“} | {„IP“,„PA“,„AD“} |
| 5 | iPad | macBookPro | {„IP“,„PA“,„AD“} | {„ma“,„ac“,„cb“,„bo“,„oo“,„ok“,„kp“,„pr“,„ro“} |
| 6 | iPad | iPhone | {„IP“,„PA“,„AD“} | {„IP“,„PH“,„HO“,„ON“,„NE“} |
| 7 | iWatch | iPad | {„iw“,„wa“,„at“,„tc“,„ch“} | {„IP“,„PA“,„AD“} |
| 8 | iWatch | macBookPro | {„iw“,„wa“,„at“,„tc“,„ch“} | {„ma“,„ac“,„cb“,„bo“,„oo“,„ok“,„kp“,„pr“,„ro“} |
| 9 | iWatch | iPhone | {„iw“,„wa“,„at“,„tc“,„ch“} | {„IP“,„PH“,„HO“,„ON“,„NE“} |
| 10 | iPhone | iPad | {„IP“,„PH“,„HO“,„ON“,„NE“} | {„IP“,„PA“,„AD“} |
| 11 | iPhone | macBookPro | {„IP“,„PH“,„HO“,„ON“,„NE“} | {„ma“,„ac“,„cb“,„bo“,„oo“,„ok“,„kp“,„pr“,„ro“} |
| 12 | iPhone | iPhone | {„IP“,„PH“,„HO“,„ON“,„NE“} | {„IP“,„PH“,„HO“,„ON“,„NE“} |

{style="table-layout:auto"}

+++

## Jaccard-Ähnlichkeitsmessung berechnen {#compute-the-jaccard-similarity-measure}

Als Nächstes berechnen Sie mithilfe des Jaccard-Ähnlichkeitskoeffizienten, wie Sie eine Ähnlichkeitsanalyse zwischen den beiden Sätzen von Produktnamen durchführen, indem Sie ihre Token-Darstellungen vergleichen. Die Ausgabe des unten stehenden SQL-Scripts liefert die folgenden Informationen: Produktnamen aus beiden Sätzen, ihre Token-Darstellung, die Anzahl der allgemeinen und der gesamten eindeutigen Token und der berechnete Jaccard-Ähnlichkeitskoeffizient für jedes Paar von Datensätzen.


```SQL {line-numbers="true"}
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) /    size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    );
```

Im Folgenden finden Sie eine Zusammenfassung des SQL-Codes, der zur Berechnung des Jaccard-Ähnlichkeitskoeffizienten verwendet wird:

- Zeile 6: `size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count` berechnet die Anzahl von Token, die sowohl für `SetA_tokens1` als auch für `SetB_tokens2` gelten. Diese Berechnung wird durch die Berechnung der Größe der Schnittmenge der beiden Token-Arrays erreicht.
- Zeile 7: `size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count` berechnet die Gesamtzahl der eindeutigen Token für `SetA_tokens1` und `SetB_tokens2`. Diese Zeile berechnet die Größe der Vereinigung der beiden Token-Arrays.
- Zeile 8-10: `ROUND(CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity` berechnet die Jaccard-Ähnlichkeit zwischen den Token-Sätzen. Diese Linien teilen die Größe der Token-Schnittmenge durch die Größe der Token-Vereinigung und runden das Ergebnis auf zwei Dezimalstellen. Das Ergebnis ist ein Wert zwischen null und eins, wobei eins eine vollständige Ähnlichkeit anzeigt.

Die Ergebnisse sind in der folgenden Tabelle aufgeführt:

+++Zum Erweitern auswählen

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 | token_intersect_count | token_intersect_count | Jaccard-Ähnlichkeit |
|---|---------------------|-------------------|---------------------------------------|-------------------------------------------------|----|----|----|
| 1 | IPadmini | iPad | {„IP“,„PA“,„AD“,„DM“,„MI“,„IN“,„NI“} | {„IP“,„PA“,„AD“} | 3 | 7 | 0,43 |
| 2 | IPadmini | macBookPro | {„IP“,„PA“,„AD“,„DM“,„MI“,„IN“,„NI“} | {„ma“,„ac“,„cb“,„bo“,„oo“,„ok“,„kp“,„pr“,„ro“} | 0 | 16 | 0,0 |
| 3 | IPadmini | iPhone | {„IP“,„PA“,„AD“,„DM“,„MI“,„IN“,„NI“} | {„IP“,„PH“,„HO“,„ON“,„NE“} | 1 | 11 | 0,09 |
| 4 | iPad | iPad | {„IP“,„PA“,„AD“} | {„IP“,„PA“,„AD“} | 3 | 3 | 1,0 |
| 5 | iPad | macBookPro | {„IP“,„PA“,„AD“} | {„ma“,„ac“,„cb“,„bo“,„oo“,„ok“,„kp“,„pr“,„ro“} | 0 | 12 | 0,0 |
| 6 | iPad | iPhone | {„IP“,„PA“,„AD“} | {„IP“,„PH“,„HO“,„ON“,„NE“} | 1 | 7 | 0,14 |
| 7 | iWatch | iPad | {„iw“,„wa“,„at“,„tc“,„ch“} | {„IP“,„PA“,„AD“} | 0 | 8 | 0,0 |
| 8 | iWatch | macBookPro | {„iw“,„wa“,„at“,„tc“,„ch“} | {„ma“,„ac“,„cb“,„bo“,„oo“,„ok“,„kp“,„pr“,„ro“} | 0 | 14 | 0,0 |
| 9 | iWatch | iPhone | {„iw“,„wa“,„at“,„tc“,„ch“} | {„IP“,„PH“,„HO“,„ON“,„NE“} | 0 | 10 | 0,0 |
| 10 | iPhone | iPad | {„IP“,„PH“,„HO“,„ON“,„NE“} | {„IP“,„PA“,„AD“} | 1 | 7 | 0,14 |
| 11 | iPhone | macBookPro | {„IP“,„PH“,„HO“,„ON“,„NE“} | {„ma“,„ac“,„cb“,„bo“,„oo“,„ok“,„kp“,„pr“,„ro“} | 0 | 14 | 0,0 |
| 12 | iPhone | iPhone | {„IP“,„PH“,„HO“,„ON“,„NE“} | {„IP“,„PH“,„HO“,„ON“,„NE“} | 5 | 5 | 1,0 |

{style="table-layout:auto"}

+++

## Filtern von Ergebnissen nach dem Jaccard-Ähnlichkeitsschwellenwert {#similarity-threshold-filter}

Filtern Sie die Ergebnisse schließlich nach einem vordefinierten Schwellenwert, um nur die Paare auszuwählen, die die Ähnlichkeitskriterien erfüllen. Die folgende SQL-Anweisung filtert die Produkte mit einem Jaccard-Ähnlichkeitskoeffizienten von mindestens 0,4. Dadurch werden die Ergebnisse auf Paare eingegrenzt, die einen wesentlichen Ähnlichkeitsgrad aufweisen.

```SQL
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames
FROM 
(SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)),
        2
    ) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    )
)
WHERE jaccard_similarity>=0.4
```

Die Ergebnisse dieser Abfrage geben die Spalten für den Ähnlichkeits-Join an, wie unten dargestellt:

+++Zum Erweitern auswählen

|   | SetA_ProductNames | SetA_ProductNames |
|---|--------------------------|------------------------|
| 1 | IPadmini | iPad |
| 2 | iPad | iPad |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++:

### Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments können Sie jetzt diese Logik verwenden, um aussagekräftige Beziehungen oder Überschneidungen zwischen unterschiedlichen Datensätzen hervorzuheben. Die Möglichkeit, Produkte aus verschiedenen Datensätzen zu identifizieren, deren Merkmale oder Attribute sich stark ähneln, hat zahlreiche reale Anwendungen. Diese Logik kann für Szenarien wie die folgenden verwendet werden:

- Produktabgleich: Um ähnliche Produkte zu gruppieren oder Kunden zu empfehlen.
- Datenbereinigung: zur Verbesserung der Datenqualität.
- Warenkorbanalyse: Um Einblicke in das Kundenverhalten, die Vorlieben und potenzielle Cross-Selling-Möglichkeiten zu erhalten.

Wenn Sie dies noch nicht getan haben, empfehlen wir, die [Übersicht über die KI/ML-Feature-Pipeline](../data-distiller/ml-feature-pipelines/overview.md) zu lesen. Verwenden Sie diese Übersicht, um zu erfahren, wie Data Distiller und Ihr bevorzugtes maschinelles Lernen benutzerdefinierte Datenmodelle erstellen können, die Ihre Marketing-Anwendungsfälle mit Experience Platform-Daten unterstützen.
