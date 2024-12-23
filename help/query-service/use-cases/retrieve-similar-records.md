---
title: Abrufen ähnlicher Datensätze mit Funktionen mit höherer Reihenfolge
description: Erfahren Sie, wie Sie anhand einer Ähnlichkeitsmetrik und eines Ähnlichkeitsschwellenwerts ähnliche oder verwandte Datensätze aus einem oder mehreren Datensätzen identifizieren und abrufen. Dieser Workflow kann aussagekräftige Beziehungen oder Überschneidungen zwischen verschiedenen Datensätzen hervorheben.
exl-id: 4810326a-a613-4e6a-9593-123a14927214
source-git-commit: 27eab04e409099450453a2a218659e576b8f6ab4
workflow-type: tm+mt
source-wordcount: '4031'
ht-degree: 3%

---

# Abrufen ähnlicher Datensätze mit Funktionen höherer Reihenfolge

Verwenden Sie Data Distiller-Funktionen in höherer Reihenfolge, um eine Vielzahl gängiger Anwendungsfälle zu lösen. Um ähnliche oder verwandte Datensätze aus einem oder mehreren Datensätzen zu identifizieren und abzurufen, verwenden Sie die Filter-, Transform- und Reduzierungsfunktionen, wie in diesem Handbuch beschrieben. Informationen dazu, wie Funktionen mit höherer Reihenfolge zur Verarbeitung komplexer Datentypen verwendet werden können, finden Sie in der Dokumentation zum Verwalten von Array- und Zuordnungsdatentypen ](../sql/higher-order-functions.md).[

Verwenden Sie dieses Handbuch, um Produkte aus verschiedenen Datensätzen zu identifizieren, die eine signifikante Ähnlichkeit in ihren Eigenschaften oder Attributen aufweisen. Diese Methode bietet u. a. Lösungen für Datendeduplizierung, Datensatzverknüpfung, Empfehlungssysteme, Informationsabruf und Textanalyse.

In diesem Dokument wird die Implementierung eines Ähnlichkeitsjoin beschrieben, bei dem dann die Data Distiller-Funktionen in höherer Reihenfolge verwendet werden, um die Ähnlichkeit zwischen Datensätzen zu berechnen und sie anhand ausgewählter Attribute zu filtern. Für jeden Schritt des Prozesses werden SQL-Code-Snippets und Erklärungen bereitgestellt. Der Workflow implementiert Ähnlichkeitsverbindungen mithilfe der Jaccard-Ähnlichkeitsmessung und -Tokenisierung mithilfe von Data Distiller-Funktionen höherer Reihenfolge. Diese Methoden werden dann verwendet, um ähnliche oder verwandte Datensätze basierend auf einer Ähnlichkeitsmetrik aus einem oder mehreren Datensätzen zu identifizieren und abzurufen. Zu den wichtigsten Abschnitten des Prozesses gehören: [Tokenisierung mit Funktionen höherer Reihenfolge](#data-transformation), der [Kreuzjoin der eindeutigen Elemente](#cross-join-unique-elements), die [Berechnung der Ähnlichkeit von Jaccard](#compute-the-jaccard-similarity-measure) und die [schwellenbasierte Filterung](#similarity-threshold-filter).

## Voraussetzungen

Bevor Sie mit diesem Dokument fortfahren, sollten Sie mit den folgenden Konzepten vertraut sein:

- Ein **Ähnlichkeitsjoin** ist ein Vorgang, der anhand eines Messwerts der Ähnlichkeit zwischen den Datensätzen Verweise aus einer oder mehreren Tabellen identifiziert und abruft. Die wichtigsten Voraussetzungen für einen Ähnlichkeitsjoin sind:
   - **Ähnlichkeitsmetrik**: Ein Ähnlichkeitsjoin beruht auf einer vordefinierten Ähnlichkeitsmetrik oder einem vordefinierten Maß. Zu diesen Metriken gehören: die Jaccard-Ähnlichkeit, die Ähnlichkeit von Kosinen, Bearbeitungsabstände usw. Die Metrik hängt von der Art der Daten und dem Anwendungsfall ab. Diese Metrik quantifiziert, wie ähnlich oder unähnlich zwei Datensätze sind.
   - **Schwellenwert**: Mit einem Schwellenwert für die Ähnlichkeit wird bestimmt, wann die beiden Datensätze als ähnlich genug angesehen werden, um in das Join-Ergebnis aufgenommen zu werden. Datensätze, deren Ähnlichkeitswert über dem Schwellenwert liegt, werden als Übereinstimmungen betrachtet.
- Der Index **Jaccard similarity** oder die Jaccard-Ähnlichkeitsmessung ist eine Statistik, mit der die Ähnlichkeit und Vielfalt von Stichprobensätzen gemessen wird. Dies ist definiert als die Größe der Schnittmenge geteilt durch die Größe der Vereinigung der Stichprobensätze. Die Jaccard-Ähnlichkeitsmessung liegt zwischen null und eins. Eine Jaccard-Ähnlichkeit von null zeigt an, dass keine Ähnlichkeit zwischen den Sets besteht, und eine Jaccard-Ähnlichkeit von eins zeigt an, dass die Sets identisch sind.
  ![Ein Venendiagramm zur Veranschaulichung der Jaccard-Ähnlichkeitsmessung.](../images/use-cases/jaccard-similarity.png)
- **Funktionen mit höherer Reihenfolge** in Data Distiller sind dynamische Inline-Tools, die Daten direkt in SQL-Anweisungen verarbeiten und umwandeln. Durch diese vielseitigen Funktionen entfällt die Notwendigkeit mehrerer Schritte bei der Datenbearbeitung, insbesondere bei [komplexen Typen wie Arrays und Maps](../sql/higher-order-functions.md). Durch die Steigerung der Abfragenerffizienz und die Vereinfachung von Umwandlungen tragen Funktionen mit höherer Reihenfolge zu einer agileren Analyse und besseren Entscheidungsfindung in verschiedenen Geschäftsszenarien bei.

## Erste Schritte

Die Data Distiller-SKU ist erforderlich, um die Funktionen mit höherer Reihenfolge für Ihre Adobe Experience Platform-Daten auszuführen. Wenn Sie nicht über die Data Distiller-SKU verfügen, wenden Sie sich für weitere Informationen an Ihren Adobe-Kundenbetreuer.

## Ähnlichkeit feststellen {#establish-similarity}

Dieser Anwendungsfall erfordert eine Kennzahl zur Ähnlichkeit von Textzeichenfolgen, die später verwendet werden können, um einen Schwellenwert für die Filterung festzulegen. In diesem Beispiel stellen die Produkte in Satz A und Satz B die Wörter in zwei Dokumenten dar.

Die Jaccard-Ähnlichkeitsmessung kann auf eine Vielzahl von Datentypen angewendet werden, einschließlich Textdaten, kategorischen Daten und Binärdaten. Sie eignet sich auch für die Echtzeit- oder Batch-Verarbeitung, da die Berechnung für große Datensätze rechnereffizient erfolgen kann.

Produktsatz A und Satz B enthalten die Testdaten für diesen Workflow.

- Produktsatz A: `{iPhone, iPad, iWatch, iPad Mini}`
- Produktsatz B: `{iPhone, iPad, Macbook Pro}`

Um die Jaccard-Ähnlichkeit zwischen den Produktsätzen A und B zu berechnen, suchen Sie zunächst die **Schnittmenge** (gemeinsame Elemente) der Produktsätze. In diesem Fall `{iPhone, iPad}`. Suchen Sie als Nächstes die **Vereinigung** (alle eindeutigen Elemente) beider Produktsätze. In diesem Beispiel `{iPhone, iPad, iWatch, iPad Mini, Macbook Pro}`.

Verwenden Sie abschließend die Jaccard-Ähnlichkeitsformel: `J(A,B) = A∪B / A∩B` , um die Ähnlichkeit zu berechnen.

J = Jaccard-Entfernung
A = Satz 1
B = Satz 2

Die Jaccard-Ähnlichkeit zwischen den Produktsätzen A und B beträgt 0,4. Dies weist auf eine mäßige Ähnlichkeit zwischen den in den beiden Dokumenten verwendeten Wörtern hin. Diese Ähnlichkeit zwischen den beiden Sätzen definiert die Spalten in der Ähnlichkeitsverknüpfung. Diese Spalten stellen Informationen oder mit den Daten verknüpfte Eigenschaften dar, die in einer Tabelle gespeichert sind und zur Durchführung der Ähnlichkeitsberechnungen verwendet werden.

### Paarweise Jaccard-Berechnung mit Zeichenfolgenähnlichkeit {#pairwise-similarity}

Um die Ähnlichkeiten zwischen Zeichenfolgen genauer zu vergleichen, muss die paarweise Ähnlichkeit berechnet werden. Die paarweise Ähnlichkeit teilt hochdimensionale Objekte zu kleineren dimensionalen Objekten zum Vergleich und zur Analyse auf. Dazu wird eine Textzeichenfolge in kleinere Teile oder Einheiten (Token) unterteilt. Dabei kann es sich um einzelne Briefe, Gruppen von Briefen (wie Silben) oder ganze Wörter handeln. Die Ähnlichkeit wird für jedes Token-Paar zwischen jedem Element in Satz A mit jedem Element in Satz B berechnet. Diese Tokenisierung bietet eine Grundlage für analytische und berechnete Vergleiche, Beziehungen und Erkenntnisse, die aus den Daten gezogen werden können.

Für die paarweise Berechnung der Ähnlichkeit verwendet dieses Beispiel Zeichen in bi-Gramm (zwei Zeichen-Token), um eine Ähnlichkeitsübereinstimmung zwischen den Textzeichenfolgen der Produkte in Satz A und Satz B zu vergleichen. Ein Bikro ist eine Folge von zwei Elementen oder Elementen in einer bestimmten Sequenz oder einem bestimmten Text. Sie können dies zu n Gramm verallgemeinern.

In diesem Beispiel wird davon ausgegangen, dass die Groß-/Kleinschreibung keine Rolle spielt und Leerzeichen nicht berücksichtigt werden sollten. Gemäß diesen Kriterien haben Set A und Set B die folgenden bi-Gramm:

Produktsatz A bi-Gramm:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- iWatch (5): &quot;iw&quot;, &quot;wa&quot;, &quot;at&quot;, &quot;tc&quot;, &quot;ch&quot;
- iPad Mini (7): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;, &quot;dm&quot;, &quot;mi&quot;, &quot;in&quot;, &quot;ni&quot;

Produktsatz B bi-Gramm:

- iPhone (5): &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3): &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- Macbook Pro (9): &quot;Ma&quot;, &quot;ac&quot;, &quot;cb&quot;, &quot;bo&quot;, &quot;oo&quot;, &quot;ok&quot;, &quot;kp&quot;, &quot;pr&quot;, &quot;ro&quot;

Als Nächstes berechnen Sie den Jaccard-Ähnlichkeitskoeffizienten für jedes Paar:

|                   | iPhone (Set B) | iPad (Set B) | Macbook Pro (Set B) |
|-------------------|----------------------------------------------|---------------------------------------------|-------------------------------------------|
| iPhone (Set A) | (Schnittmenge: 5, Vereinigung: 5) = 5 / 5 = 1 | (Schnittmenge: 1, Vereinigung: 7) =1 / 7 Mobi 0,14 | (Schnittmenge: 0, Vereinigung: 14) = 0 / 14 = 0 |
| iPad (Set A) | (Schnittmenge: 1, Vereinigung: 7) = 1 / 7 Über 0,14 | (Schnittmenge: 3, Vereinigung: 3) = 3 / 3 = 1 | (Schnittmenge: 0, Vereinigung: 12) = 0 / 12 = 0 |
| iWatch (Set A) | (Schnittmenge: 0, Vereinigung: 8) = 0 / 8 = 0 | (Schnittmenge: 0, Vereinigung: 8) = 0 / 8 = 0 | (Schnittmenge: 0, Vereinigung: 8) = 0 / 8 = 0 |
| iPad Mini (Set A) | (Schnittmenge: 1, Vereinigung: 11) = 1 / 11 Mobi 0,09 | (Schnittmenge: 3, Vereinigung: 7) = 3 / 7 Über 0,43 | (Schnittmenge: 0, Vereinigung: 16) = 0 / 16 = 0 |

{style="table-layout:auto"}

## Testdaten mit SQL erstellen {#create-test-data}

Verwenden Sie die Anweisung SQL CREATE TABLE , um manuell eine Testtabelle für die Produktsätze zu erstellen.

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

Die folgenden Beschreibungen enthalten eine Aufschlüsselung des obigen SQL-Codeblocks:

- Zeile 1: `CREATE TEMP TABLE featurevector1 AS`: Diese Anweisung erstellt eine temporäre Tabelle namens `featurevector1`. Temporäre Tabellen sind in der Regel nur innerhalb der aktuellen Sitzung verfügbar und werden automatisch am Ende der Sitzung abgelegt.
- Zeile 1 und 2: `SELECT * FROM (...)`: Dieser Teil des Codes ist eine Unterabfrage, mit der die in die Tabelle `featurevector1` eingefügten Daten generiert werden.
Innerhalb der Unterabfrage werden mehrere `SELECT` -Anweisungen mit dem Befehl `UNION ALL` kombiniert. Jede `SELECT` -Anweisung generiert eine Datenzeile mit den angegebenen Werten für die `ProductName` -Spalte.
- Zeile 3: `SELECT 'iPad' AS ProductName`: Dadurch wird eine Zeile mit dem Wert `iPad` in der Spalte `ProductName` generiert.
- Zeile 5: `SELECT 'iPhone'`: Dadurch wird eine Zeile mit dem Wert `iPhone` in der Spalte `ProductName` generiert.

Die SQL-Anweisung erstellt eine Tabelle wie unten dargestellt:

|   | `ProductName` |
|---|---------------|
| 1 | iPad |
| 2 | iPhone |
| 3 | iWatch |
| 4 | iPad Mini |

{style="table-layout:auto"}

Verwenden Sie die folgende SQL-Anweisung, um den zweiten Funktionsvektor zu erstellen:

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

In diesem Beispiel müssen mehrere Aktionen durchgeführt werden, um die Sets genau zu vergleichen. Zunächst werden alle Leerzeichen aus den Funktionsvektoren entfernt, da davon ausgegangen wird, dass sie nicht zur Ähnlichkeitsmessung beitragen. Anschließend werden alle im Funktionsvektor vorhandenen Duplikate entfernt, da sie die Rechenverarbeitung verschwenden. Als Nächstes werden Token mit zwei Zeichen (in Gramm) aus den Funktionsvektoren extrahiert. In diesem Beispiel wird davon ausgegangen, dass sie sich überschneiden.

>[!NOTE]
>
>Zu Veranschaulichungszwecken werden die verarbeiteten Spalten für jeden Schritt neben dem Funktionsvektor hinzugefügt.

Die folgenden Abschnitte veranschaulichen die erforderlichen Datenumwandlungen wie Deduplizierung, Entfernen von Leerzeichen und Konvertierung in Kleinbuchstaben, bevor der Tokenisierungsprozess gestartet wird.

### Deduplizierung {#deduplication}

Verwenden Sie als Nächstes die `DISTINCT` -Klausel, um Duplikate zu entfernen. In diesem Beispiel gibt es keine Duplikate. Es ist jedoch ein wichtiger Schritt, die Genauigkeit von Vergleichen zu verbessern. Die erforderliche SQL-Anweisung wird unten angezeigt:

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct FROM featurevector1
SELECT DISTINCT(ProductName) AS featurevector2_distinct FROM featurevector2
```

### Entfernen von Leerzeichen {#whitespace-removal}

In der folgenden SQL-Anweisung werden die Leerzeichen aus den Feature Vectors entfernt. Der Teil `replace(ProductName, ' ', '') AS featurevector1_nospaces` der Abfrage nimmt die Spalte `ProductName` aus der Tabelle `featurevector1` und verwendet die Funktion `replace()`. Die Funktion `REPLACE` ersetzt alle Vorkommnisse eines Leerzeichens (&#39; &#39;) durch eine leere Zeichenfolge (&#39;&#39;). Dadurch werden alle Leerzeichen aus den `ProductName` -Werten entfernt. Das Ergebnis wird als `featurevector1_nospaces` Alias angezeigt.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, replace(ProductName, ' ', '') AS featurevector1_nospaces FROM featurevector1
```

Die Ergebnisse sind in der folgenden Tabelle dargestellt:

|   | featurevektor1_distinct | featurevektor1_nospaces |
|---|---|---|
| 1 | iPad Mini | iPadMini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

Die SQL-Anweisung und ihre Ergebnisse für den zweiten Funktionsvektor sind unten dargestellt:

+++Auswählen zum Erweitern

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, replace(ProductName, ' ', '') AS featurevector2_nospaces FROM featurevector2
```

Die Ergebnisse werden wie folgt angezeigt:

|   | featurevektor2_distinct | featurevektor2_nospaces |
|---|---|---|
| 1 | iPad | iPad |
| 2 | Macbook Pro | MacbookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### In Kleinbuchstaben konvertieren {#lowercase-conversion}

Anschließend wird die SQL dahingehend verbessert, dass die Produktnamen in Kleinbuchstaben konvertiert und alle Leerzeichen entfernt werden. Die untere Funktion (`lower(...)`) wird auf das Ergebnis der Funktion `replace()` angewendet. Die untere Funktion konvertiert alle Zeichen in den geänderten `ProductName` -Werten in Kleinbuchstaben. Dadurch wird sichergestellt, dass die Werte unabhängig von der Originalschreibweise in Kleinbuchstaben geschrieben werden.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform FROM featurevector1;
```

Das Ergebnis dieser Aussage ist:

|   | featurevektor1_distinct | featurevektor1_transform |
|---|---|---|
| 1 | iPad Mini | ipadmini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

Die SQL-Anweisung und ihre Ergebnisse für den zweiten Funktionsvektor sind unten dargestellt:

+++Auswählen zum Erweitern

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, lower(replace(ProductName, ' ', '')) AS featurevector2_transform FROM featurevector2
```

Die Ergebnisse werden wie folgt angezeigt:

|   | featurevektor2_distinct | featurevektor2_transform |
|---|---|---|
| 1 | iPad | ipad |
| 2 | Macbook Pro | macbookpro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### Token mit SQL extrahieren {#tokenization}

Der nächste Schritt ist die Tokenisierung oder Textaufteilung. Tokenisierung ist der Prozess, Text in einzelne Begriffe zu unterteilen. In der Regel besteht dies darin, Sätze in Wörter zu unterteilen. In diesem Beispiel werden Zeichenfolgen in bi-Gramm (und in Gramm höherer Ordnung) aufgeteilt, indem Token mit SQL-Funktionen wie `regexp_extract_all` extrahiert werden. Für eine wirksame Tokenisierung müssen überschneidende bi-Gramm generiert werden.

Die SQL wurde weiter verbessert und verwendet nun `regexp_extract_all`. `regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0) AS tokens:` Dieser Teil der Abfrage verarbeitet die geänderten `ProductName` -Werte weiter, die im vorherigen Schritt erstellt wurden. Es verwendet die Funktion `regexp_extract_all()` , um alle nicht überlappenden Teilzeichenfolgen von ein bis zwei Zeichen aus den geänderten und kleingeschriebenen `ProductName` -Werten zu extrahieren. Das Muster für reguläre Ausdrücke `.{2}` entspricht Teilzeichenfolgen von zwei Zeichen in der Länge. Der Teil `regexp_extract_all(..., '.{2}', 0)` der Funktion extrahiert dann alle übereinstimmenden Unterzeichenfolgen aus dem Eingabetext.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
regexp_extract_all(lower(replace(ProductName, ' ', '')) , '.{2}', 0) AS tokens
FROM featurevector1;
```

Die Ergebnisse sind in der folgenden Tabelle dargestellt:

+++Auswählen zum Erweitern

|   | featurevektor1_distinct | featurevektor1_transform | Token |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;, &quot;ch&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Um die Genauigkeit weiter zu verbessern, muss SQL zur Erstellung überlappender Token verwendet werden. Beispielsweise fehlt in der obigen Zeichenfolge &quot;iPad&quot;das Token &quot;pa&quot;. Um dies zu beheben, verschieben Sie den Lookahead-Operator (mit `substring`) um einen Schritt und generieren Sie die bi-Gramm.

Ähnlich wie im vorherigen Schritt extrahiert `regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0):` aus dem modifizierten Produktnamen aus zwei Zeichen, beginnt jedoch mit dem zweiten Zeichen mit der `substring` -Methode, um überlappende Token zu erstellen. Anschließend kombiniert die Funktion `array_union()` in den Zeilen 3-7 (`array_union(...) AS tokens`) die Arrays von zweistelligen Sequenzen, die von den beiden Extraktionen des regulären Ausdrucks erhalten werden. Dadurch wird sichergestellt, dass das Ergebnis eindeutige Token aus nicht überlappenden und überlappenden Sequenzen enthält.

```SQL {line-numbers="true"}
SELECT DISTINCT(ProductName) AS featurevector1_distinct, 
       lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
       array_union(
           regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0),
           regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0)
       ) AS tokens
FROM featurevector1;
```

Die Ergebnisse sind in der folgenden Tabelle dargestellt:

+++Auswählen zum Erweitern

|   | featurevektor1_distinct | featurevektor1_transform | Token |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;,&quot;pa&quot;,&quot;dm&quot;,&quot;in&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;,&quot;pa&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;,&quot;ch&quot;,&quot;wa&quot;,&quot;tc&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;,&quot;ph&quot;,&quot;on&quot;} |

{style="table-layout:auto"}

+++

Die Verwendung von `substring` als Lösung des Problems hat jedoch Einschränkungen. Wenn Sie Token aus dem Text basierend auf Tri-Gramm (drei Zeichen) erstellen würden, würde die Verwendung von zwei `substrings` erforderlich sein, um zweimal nach vorne zu suchen, um die erforderlichen Verschiebungen zu erhalten. Für 10 Gramm benötigen Sie neun `substring` Ausdrücke. Dies würde den Code aufblasen und unhaltbar machen. Die Verwendung von einfachen regulären Ausdrücken ist nicht geeignet. Es bedarf eines neuen Ansatzes.

### Anpassen der Länge des Produktnamens {#length-adjustment}

Das SQl kann mit der Sequenz- und Längenfunktion verbessert werden. Im folgenden Beispiel generiert `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3)` eine Zahlenfolge von eins bis zur Länge des modifizierten Produktnamen abzüglich drei. Wenn der geänderte Produktname beispielsweise &quot;ipadmini&quot;mit einer Zeichenlänge von acht Zeichen ist, werden Zahlen von einem bis fünf (acht bis drei) generiert.

Die nachstehende Anweisung extrahiert eindeutige Produktnamen und unterteilt jeden Namen in Zeichenfolgen (Token) mit einer Länge von vier Zeichen, ohne Leerzeichen, und stellt sie in zwei Spalten dar. Eine Spalte zeigt die eindeutigen Produktnamen und die andere Spalte die generierten Token.

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

Die Ergebnisse sind in der folgenden Tabelle dargestellt:

+++Auswählen zum Erweitern

|   | featurevektor1_distinct | Token |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipad&quot;,&quot;padm&quot;,&quot;admi&quot;,&quot;dmin&quot;,&quot;mini&quot;} |
| 2 | iPad | {&quot;ipad&quot;} |
| 3 | iWatch | {&quot;iwat&quot;,&quot;watc&quot;,&quot;atch&quot;} |
| 4 | iPhone | {&quot;ipho&quot;,&quot;phon&quot;,&quot;hone&quot;} |

{style="table-layout:auto"}

+++

### Festlegen der Token-Länge {#ensure-set-token-length}

Der Anweisung können zusätzliche Bedingungen hinzugefügt werden, um sicherzustellen, dass die erzeugten Sequenzen eine bestimmte Länge aufweisen. Die folgende SQL-Anweisung erweitert die Logik der Tokenerstellung, indem die Funktion `transform` komplexer wird. Die Anweisung verwendet die Funktion `filter` innerhalb von `transform`, um sicherzustellen, dass die generierten Sequenzen eine Länge von sechs Zeichen haben. Sie behandelt die Fälle, in denen dies nicht möglich ist, indem sie diesen Positionen NULL-Werte zuweist.

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

Die Ergebnisse sind in der folgenden Tabelle dargestellt:

+++Auswählen zum Erweitern

|   | featurevektor1_distinct | Token |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipadmi&quot;,&quot;padmin&quot;,&quot;admini&quot;} |
| 2 | iPad | {null} |
| 3 | iWatch | {&quot;iwatch&quot;} |
| 4 | iPhone | {&quot;iphone&quot;} |

{style="table-layout:auto"}

+++

## Lösungen mit Data Distiller-Funktionen in höherer Reihenfolge durchsuchen {#higher-order-function-solutions}

Funktionen mit höherer Reihenfolge sind leistungsstarke Konstrukte, mit denen Sie &quot;Programmierung&quot;wie Syntax in Data Distiller implementieren können. Sie können verwendet werden, um eine Funktion über mehrere Werte in einem Array zu iterieren.

Im Kontext von Data Distiller eignen sich Funktionen mit höherer Reihenfolge ideal zum Erstellen von n Gramm und Iterieren von Zeichensatzsequenzen.

Die Funktion &quot;`reduce`&quot;, insbesondere wenn sie in durch `transform` generierten Sequenzen verwendet wird, bietet eine Möglichkeit, kumulative Werte oder Aggregate abzuleiten, die in verschiedenen Analyse- und Planungsprozessen ausschlaggebend sein können.

In der unten stehenden SQl-Anweisung aggregiert die Funktion `reduce()` beispielsweise Elemente in einem Array mithilfe eines benutzerdefinierten Aggregators. Es simuliert eine for -Schleife, um die kumulativen Summen aller Ganzzahlen zu erstellen, die **von 1 bis 5. 2.**`1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4`

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

- Zeile 1: `transform` wendet die Funktion `x -> reduce` auf jedes in der Sequenz generierte Element an.
- Zeile 2: `sequence(1, 5)` generiert eine Folge von Zahlen von 1 bis 5.
- Zeile 3: `x -> reduce(sequence(1, x), 0, (acc, y) -> acc + y)` führt einen Reduzierungsvorgang für jedes Element x in der Sequenz durch (von 1 bis 5).
   - Die Funktion `reduce` verwendet einen anfänglichen Akkumulatorwert von 0, eine Sequenz von 1 bis zum aktuellen Wert von `x` und eine Funktion der höheren Reihenfolge `(acc, y) -> acc + y`, um die Zahlen hinzuzufügen.
   - Die Funktion der höheren Reihenfolge `acc + y` kumuliert die Summe, indem der aktuelle Wert `y` zum Akkumulator `acc` hinzugefügt wird.
- Zeile 8: `AS sum_result` benennt die resultierende Spalte in sum_result um.

Zusammenfassend lässt sich sagen, dass diese Funktion mit höherer Reihenfolge zwei Parameter (`acc` und `y`) akzeptiert und den auszuführenden Vorgang definiert, in diesem Fall also `y` zum Akkumulator `acc` hinzufügt. Diese Funktion in höherer Reihenfolge wird für jedes Element in der Sequenz während des Reduzierungsprozesses ausgeführt.

Die Ausgabe dieser Anweisung ist eine einzelne Spalte (`sum_result`), die die kumulativen Summen der Zahlen von einer bis fünf enthält.

### Der Wert von Funktionen mit höherer Reihenfolge {#value-of-higher-order-functions}

In diesem Abschnitt wird eine reduzierte Version einer tri-Gramm-SQL-Anweisung analysiert, um den Wert von Funktionen mit höherer Reihenfolge in Data Distiller besser zu verstehen, um n-Gramm effizienter zu erstellen.

Die folgende Anweisung arbeitet mit der Spalte `ProductName` in der Tabelle `featurevector1`. Es wird ein Satz aus dreistelligen Unterzeichenfolgen erzeugt, die aus den modifizierten Produktnamen in der Tabelle abgeleitet werden, wobei Positionen aus der erzeugten Sequenz verwendet werden.

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

- Zeile 2: `transform` wendet eine Funktion höherer Reihenfolge auf jede Ganzzahl in der Sequenz an.
- Zeile 3: `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2)` generiert eine Folge von Ganzzahlen von `1` bis zur Länge des modifizierten Produktnamen abzüglich zwei.
   - `length(lower(replace(ProductName, ' ', '')))` berechnet die Länge des `ProductName`, nachdem es in Kleinbuchstaben geschrieben und Leerzeichen entfernt wurde.
   - `- 2` subtrahiert zwei von der Länge, um sicherzustellen, dass die Sequenz gültige Startpositionen für 3-stellige Unterzeichenfolgen generiert. Durch Subtraktion 2 wird sichergestellt, dass Sie an jeder Startposition genügend Zeichen haben, um eine 3-stellige Unterzeichenfolge zu extrahieren. Die Teilzeichenfolgen-Funktion funktioniert hier wie ein Suchvorgangsoperator.
- Zeile 4: `i -> substring(lower(replace(ProductName, ' ', '')), i, 3)` ist eine Funktion höherer Reihenfolge, die auf jeder Integer `i` in der generierten Sequenz ausgeführt wird.
   - Die Funktion `substring(...)` extrahiert eine 3-stellige Unterzeichenfolge aus der Spalte `ProductName`.
   - Vor dem Extrahieren der Teilzeichenfolge konvertiert `lower(replace(ProductName, ' ', ''))` die `ProductName` in Kleinbuchstaben und entfernt Leerzeichen, um Konsistenz zu gewährleisten.

Die Ausgabe ist eine Liste von Teilzeichenfolgen mit einer Länge von drei Zeichen, die aus den modifizierten Produktnamen extrahiert werden, basierend auf den in der Sequenz angegebenen Positionen.

## Ergebnisse filtern {#filter-results}

Die Funktion `filter` mit nachfolgenden [Datenumwandlungen](#data-transformation) ermöglicht eine verfeinerte und präzisere Extraktion relevanter Informationen aus Textdaten. Auf diese Weise können Sie Einblicke gewinnen, die Datenqualität verbessern und bessere Entscheidungsprozesse erleichtern.

Die Funktion `filter` in der folgenden SQL-Anweisung dient dazu, die Reihenfolge der Positionen innerhalb der Zeichenfolge, aus der Unterzeichenfolgen mithilfe der nachfolgenden Transformationsfunktion extrahiert werden, zu verfeinern und zu begrenzen.

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

Die Funktion `filter` generiert eine Sequenz gültiger Startpositionen innerhalb des modifizierten `ProductName` und extrahiert Teilzeichenfolgen einer bestimmten Länge. Es sind nur Startpositionen zulässig, die die Extraktion einer siebenstelligen Unterzeichenfolge ermöglichen.

Die Bedingung `i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))` stellt sicher, dass die Startposition `i` plus `6` (die Länge der gewünschten siebenstelligen Unterzeichenfolge minus 1) nicht die Länge der modifizierten `ProductName` überschreitet.

Die Anweisung `CASE` wird verwendet, um Unterzeichenfolgen basierend auf ihrer Länge bedingt ein- oder auszuschließen. Es sind nur siebenstellige Unterzeichenfolgen enthalten, andere werden durch NULL ersetzt. Diese Unterzeichenfolgen werden dann von der Funktion `transform` verwendet, um eine Sequenz von Unterzeichenfolgen aus der Spalte `ProductName` in der Tabelle `featurevector1` zu erstellen.

>[!TIP]
>
>Sie können die Funktion [parametrisierte Vorlagen](../ui/parameterized-queries.md) verwenden, um Logik in Ihren Abfragen wiederzuverwenden und abzustrakte Logik zu verwenden. Wenn Sie beispielsweise Funktionen von Dienstprogrammen für allgemeine Zwecke erstellen (z. B. die oben für die Tokenisierung von Zeichenfolgen angezeigte), können Sie mit Data Distiller parametrierte Vorlagen verwenden, bei denen die Zeichenanzahl ein Parameter wäre.

## Berechnen der Cross-Join-Funktion für eindeutige Elemente über zwei Funktionsvektoren hinweg {#cross-join-unique-elements}

Die Identifizierung der Unterschiede oder Diskrepanzen zwischen den beiden Datensätzen basierend auf einer spezifischen Datenumwandlung ist ein gängiger Prozess, um die Datengenauigkeit zu wahren, die Datenqualität zu verbessern und die Konsistenz über Datensätze hinweg sicherzustellen.

Diese SQL-Anweisung unten extrahiert die eindeutigen Produktnamen, die in &quot;`featurevector2`&quot;, aber nicht in &quot;`featurevector1`&quot;vorhanden sind, nachdem die Transformationen angewendet wurden.

```SQL
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector2
EXCEPT
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector1;
```

>[!TIP]
>
>Zusätzlich zu `EXCEPT` können Sie je nach Anwendungsfall auch `UNION` und `INTERSECT` verwenden. Außerdem können Sie mit `ALL` - oder `DISTINCT` -Klauseln experimentieren, um den Unterschied zwischen dem Einschließen aller Werte und der Rückgabe nur der eindeutigen Werte für die angegebenen Spalten anzuzeigen.

Die Ergebnisse sind in der folgenden Tabelle dargestellt:

+++Auswählen zum Erweitern

|   | lower(replace(ProductName, &#39;, &#39;&#39;)) |
|---|---------------------------------------|
| 1 | macbookpro |

{style="table-layout:auto"}

+++

Führen Sie als Nächstes einen Join durch, um Elemente aus den beiden Funktionsvektoren zu kombinieren und so Elementpaare zum Vergleich zu erstellen. Der erste Schritt in diesem Prozess besteht darin, einen tokenisierten Vektor zu erstellen.

Ein tokenisierter Vektor ist eine strukturierte Darstellung von Textdaten, bei der jedes Wort, jeder Satz oder jede Einheit der Bedeutung (Token) in ein numerisches Format konvertiert wird. Diese Konvertierung ermöglicht es den Algorithmen zur Verarbeitung natürlicher Sprachen, Textinformationen zu verstehen und zu analysieren.

Der nachstehende SQl erstellt einen tokenisierten Vektor.

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
>Wenn Sie [!DNL DbVisualizer] verwenden, aktualisieren Sie nach dem Erstellen oder Löschen einer Tabelle die Datenbankverbindung, sodass der Metadaten-Cache der Tabelle aktualisiert wird. Data Distiller gibt keine Metadaten-Aktualisierungen aus.

Die Ergebnisse sind in der folgenden Tabelle dargestellt:

+++Auswählen zum Erweitern

|   | featurevektor1_distinct | Token |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} |
| 2 | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 3 | iwatch | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} |
| 4 | iPhone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Wiederholen Sie dann den Prozess für `featurevector2`:

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

Die Ergebnisse sind in der folgenden Tabelle dargestellt:

+++Auswählen zum Erweitern

|   | featurevektor2_distinct | Token |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | macbookpro | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | iPhone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Nachdem beide tokenisierten Vektoren abgeschlossen sind, können Sie nun den Cross-Join erstellen. Dies wird in der folgenden SQL angezeigt:

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

Im Folgenden finden Sie eine Zusammenfassung des SQl, das zum Erstellen des Joins verwendet wird:

- Zeile 2: `A.featurevector1_distinct AS SetA_ProductNames` wählt die Spalte `featurevector1_distinct` aus der Tabelle `A` aus und weist ihr den Alias `SetA_ProductNames` zu. Dieser Abschnitt von SQL führt zu einer Liste unterschiedlicher Produktnamen aus dem ersten Datensatz.
- Zeile 4: `A.tokens AS SetA_tokens1` wählt die Spalte `tokens` aus der Tabelle oder Unterabfrage `A` aus und weist ihr den Alias `SetA_tokens1` zu. Dieser Abschnitt von SQL führt zu einer Liste tokenisierter Werte, die mit den Produktnamen aus dem ersten Datensatz verknüpft sind.
- Zeile 8: Der Vorgang `CROSS JOIN` kombiniert alle möglichen Kombinationen von Zeilen aus den beiden Datensätzen. Anders ausgedrückt: Jeder Produktname und die zugehörigen Token aus der ersten Tabelle (`A`) werden mit jedem Produktnamen und den zugehörigen Token aus der zweiten Tabelle (`B`) verknüpft. Dies führt zu einem kartesischen Produkt der beiden Datensätze, wobei jede Zeile in der Ausgabe eine Kombination aus einem Produktnamen und den zugehörigen Token aus beiden Datensätzen darstellt.

Die Ergebnisse sind in der folgenden Tabelle dargestellt:

+++Auswählen zum Erweitern

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 |
|---|---------------------|-------------------|---|---|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | ipadmini | iPhone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 6 | ipad | iPhone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 9 | iwatch | iPhone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 10 | iPhone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 11 | iPhone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 12 | iPhone | iPhone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

## Berechnung der Jaccard-Ähnlichkeitsmessung {#compute-the-jaccard-similarity-measure}

Als Nächstes berechnen Sie den Jaccard-Ähnlichkeitskoeffizienten, um eine Ähnlichkeitsanalyse zwischen den beiden Sätzen von Produktnamen durchzuführen, indem Sie deren tokenisierte Darstellungen vergleichen. Die Ausgabe des unten stehenden SQL-Skripts liefert Folgendes: Produktnamen aus beiden Sets, ihre tokenisierten Darstellungen, die Anzahl der gemeinsamen und gesamten eindeutigen Token und den berechneten Jaccard-Ähnlichkeitskoeffizienten für jedes Paar von Datensätzen.


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

Im Folgenden finden Sie eine Zusammenfassung der SQL, die zur Berechnung des Jaccard-Ähnlichkeitskoeffizienten verwendet wird:

- Zeile 6: `size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count` berechnet die Anzahl der Token, die sowohl für `SetA_tokens1` als auch für `SetB_tokens2` verwendet werden. Diese Berechnung erfolgt durch Berechnung der Größe der Schnittmenge der beiden Token-Arrays.
- Zeile 7: `size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count` berechnet die Gesamtanzahl der eindeutigen Token sowohl für `SetA_tokens1` als auch für `SetB_tokens2`. Diese Zeile berechnet die Größe der Vereinigung der beiden Arrays von Token.
- Zeile 8-10: `ROUND(CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity` berechnet die Jaccard-Ähnlichkeit zwischen den Token-Sets. Diese Zeilen teilen die Größe der Token-Schnittmenge durch die Größe der Token-Vereinigung und runden das Ergebnis auf zwei Dezimalstellen. Das Ergebnis ist ein Wert zwischen null und eins, wobei einer die vollständige Ähnlichkeit anzeigt.

Die Ergebnisse sind in der folgenden Tabelle dargestellt:

+++Auswählen zum Erweitern

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 | token_intersect_count | token_intersect_count | Ähnlichkeit von Jaccard |
|---|---------------------|-------------------|---------------------------------------|-------------------------------------------------|----|----|----|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 7 | 0,43 |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 16 | 0,0 |
| 3 | ipadmini | iPhone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 11 | 0,09 |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 3 | 1,0 |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 12 | 0,0 |
| 6 | ipad | iPhone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 7 | 0,14 |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 0 | 8 | 0,0 |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 9 | iwatch | iPhone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 0 | 10 | 0,0 |
| 10 | iPhone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 1 | 7 | 0,14 |
| 11 | iPhone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 12 | iPhone | iPhone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 5 | 5 | 1,0 |

{style="table-layout:auto"}

+++

## Filtern von Ergebnissen basierend auf dem Jaccard-Schwellenwert für Ähnlichkeit {#similarity-threshold-filter}

Filtern Sie schließlich die Ergebnisse anhand eines vordefinierten Schwellenwerts, um nur die Paare auszuwählen, die den Ähnlichkeitskriterien entsprechen. Die folgende SQL-Anweisung filtert die Produkte mit einem Jaccard-Ähnlichkeitskoeffizienten von mindestens 0,4. Dadurch werden die Ergebnisse auf Paare reduziert, die einen erheblichen Grad an Ähnlichkeit aufweisen.

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

Die Ergebnisse dieser Abfrage geben die Spalten für die Ähnlichkeitsverknüpfung an, wie unten dargestellt:

+++Auswählen zum Erweitern

|   | SetA_ProductNames | SetA_ProductNames |
|---|--------------------------|------------------------|
| 1 | ipadmini | ipad |
| 2 | ipad | ipad |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++:

### Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments können Sie diese Logik jetzt verwenden, um aussagekräftige Beziehungen oder Überschneidungen zwischen verschiedenen Datensätzen hervorzuheben. Die Möglichkeit, Produkte aus verschiedenen Datensätzen zu identifizieren, die sich in ihren Eigenschaften oder Attributen erheblich ähneln, bietet zahlreiche reale Anwendungen. Diese Logik kann für Szenarien wie die folgenden verwendet werden:

- Produktabgleich: Um ähnliche Produkte für Kunden zu gruppieren oder zu empfehlen.
- Datenbereinigung: Verbesserung der Datenqualität.
- Korbanalyse für den Markt: Hier erhalten Sie Einblicke in das Kundenverhalten, die Präferenzen und potenzielle Crossselling-Möglichkeiten.

Wenn Sie dies noch nicht getan haben, sollten Sie die [AI/ML Feature Pipeline - Übersicht ](../data-distiller/ml-feature-pipelines/overview.md) lesen. In dieser Übersicht erfahren Sie, wie Data Distiller und Ihr bevorzugtes maschinelles Lernen benutzerdefinierte Datenmodelle erstellen können, die Ihre Marketing-Anwendungsfälle mit Experience Platform-Daten unterstützen.
