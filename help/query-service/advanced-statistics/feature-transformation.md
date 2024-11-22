---
title: Techniken zur Funktionsumwandlung
description: Erfahren Sie mehr über die wichtigsten Verfahren zur Vorverarbeitung von Daten wie Transformation, Kodierung und Funktionsskalierung, die die Daten für das Trainieren statistischer Modelle vorbereiten. Es geht um die Wichtigkeit des Umgangs mit fehlenden Werten und der Konvertierung kategorischer Daten, um die Modellleistung und -genauigkeit zu verbessern.
role: Developer
exl-id: ed7fa9b7-f74e-481b-afba-8690ce50c777
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '3450'
ht-degree: 9%

---

# Umwandlungsmethoden für Funktionen

Umwandlungen sind wichtige Vorverarbeitungsschritte, die Daten in ein für Modellschulung und -analyse geeignetes Format konvertieren oder skalieren und so eine optimale Leistung und Genauigkeit gewährleisten. Dieses Dokument dient als zusätzliche Syntaxressource und bietet detaillierte Informationen zu wichtigen Techniken zur Merkmalumwandlung für die Datenvorverarbeitung.

Modelle für maschinelles Lernen können keine Zeichenfolgenwerte oder Nullwerte direkt verarbeiten, sodass die Datenvorverarbeitung wesentlich ist. In diesem Handbuch wird erläutert, wie Sie verschiedene Transformationen verwenden können, um fehlende Werte zu implizieren, kategorische Daten in numerische Formate zu konvertieren und Funktionsskalierungstechniken wie Einheits-Kodierung und Vectorisierung anzuwenden. Diese Methoden ermöglichen es den Modellen, die Daten effektiv zu interpretieren und zu lernen und dadurch letztlich ihre Leistung zu verbessern.

## Automatische Funktionsumwandlung {#automatic-transformations}

Wenn Sie die `TRANSFORM`-Klausel in Ihrem `CREATE MODEL`-Befehl überspringen, erfolgt die Merkmalumwandlung automatisch. Die automatische Datenvorverarbeitung umfasst Null-Ersetzung und standardmäßige Funktionsumwandlungen (basierend auf dem Datentyp). Numerische Spalten und Textspalten werden automatisch berechnet. Anschließend werden Merkmalumwandlungen durchgeführt, um sicherzustellen, dass die Daten in einem für das Trainieren des Modells für maschinelles Lernen geeigneten Format vorliegen. Dieser Prozess umfasst fehlende Daten-Imputation sowie kategorische, numerische und boolesche Transformationen.

>[!IMPORTANT]
>
>Die zum Zeitpunkt des Trainings verwendete Merkmalumwandlung wird auch für die Merkmalumwandlung zum Zeitpunkt der Vorhersage und Auswertung verwendet.

Die folgenden Tabellen erläutern, wie verschiedene Datentypen verarbeitet werden, wenn die `TRANSFORM`-Klausel während des `CREATE MODEL`-Befehls weggelassen wird.

### Null-Ersatz {#automatic-null-replacement}

| Datentyp | Null-Ersatz |
|-----------------|-----------------------------------------------------|
| Numerisch | Nullen werden durch den Mittelwert der Spalte ersetzt. |
| Kategorisch | Nullen werden durch das Schlüsselwort `ml_unknown` ersetzt. |
| Boolesch | Nullen werden durch den Wert `FALSE` ersetzt. |
| Zeitstempel | Es wird erwartet, dass es sich um ein kontinuierliches Feld handelt. |
| Verschachtelt/STRUKT | Die Ersetzung hängt vom Datentyp des Leaf-Knotens ab. |

### Merkmalumwandlung {#automatic-feature-transformation}

| Datentyp | Merkmalumwandlung |
|-----------------|-----------------------------------------------------|
| Numerisch | NICHT ERFORDERLICH - Da dieser Datentyp von maschinellen Lernalgorithmen verstanden wird. |
| String | Die Zeichenfolgenindizierung erfolgt. |
| Boolesch | Die Zeichenfolgenindizierung erfolgt. |
| Zeitstempel | Es wird kein Vorgang ausgeführt. |
| STRUKT | Der Wert wird auf den zugehörigen Blattknoten erweitert. Die Umwandlung erfolgt basierend auf dem Datentyp des Blattknotens. |

**Beispiel**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## Transformationen manueller Funktionen {#manual-transformations}

Verwenden Sie zum Definieren der benutzerdefinierten Datenvorverarbeitung in Ihrer `CREATE MODEL` -Anweisung die `TRANSFORM` -Klausel in Kombination mit einer beliebigen Anzahl der verfügbaren Umwandlungsfunktionen. Diese manuellen Vorverarbeitungsfunktionen können auch außerhalb der `TRANSFORM` -Klausel verwendet werden. Alle Umwandlungen, die im Abschnitt [Transformator unter](#available-transformations) beschrieben werden, können verwendet werden, um die Daten manuell vorab zu verarbeiten.

### Schlüsselmerkmale {#key-characteristics}

Die folgenden Hauptmerkmale der Merkmalumwandlung sind bei der Definition der Vorverarbeitungsfunktionen zu beachten:

- **Syntax**: `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - Der Aliasname ist in der Syntax obligatorisch. Sie müssen einen Aliasnamen angeben, sonst schlägt die Abfrage fehl.

- **Parameter**: Die Parameter sind positionelle Argumente. Das bedeutet, dass jeder Parameter nur bestimmte Werte annehmen kann und dass alle vorangehenden Parameter angegeben werden müssen, wenn benutzerdefinierte Werte angegeben werden. Weitere Informationen dazu, welche Funktion welches Argument verwendet, finden Sie in der entsprechenden Dokumentation.

- **Transformatoren verketten**: Die Ausgabe eines Transformators kann zur Eingabe in einen anderen Transformator werden.

- **Funktionsnutzung**: Die letzte Merkmalumwandlung wird als Funktion des maschinellen Lernmodells verwendet.

**Beispiel**

```sql
CREATE MODEL modelname 
TRANSFORM(
  string_imputer(language, 'adding_null') AS imp_language, 
  numeric_imputer(users_count, 'mode') AS imp_users_count, 
  string_indexer(imp_language) AS si_lang,  
  vector_assembler(array(imp_users_count, si_lang, watch_minutes)) AS features
)  
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='rating') 
AS SELECT * FROM df;
```

## Verfügbare Transformationen {#available-transformations}

Es stehen 19 Umwandlungen zur Verfügung. Diese Transformationen werden in [allgemeine Transformationen](#general-transformations), [Numerische Transformationen](#numeric-transformations), [Kategorische Transformationen](#categorical-transformations) und [Texttransformationen](#textual-transformations) aufgeteilt.

### Allgemeine Umwandlungen {#general-transformations}

In diesem Abschnitt finden Sie Details zu den Transformatoren, die für eine Vielzahl von Datentypen verwendet werden. Diese Informationen sind erforderlich, wenn Sie Umwandlungen vornehmen müssen, die nicht spezifisch für kategorische oder textuelle Daten sind.

>[!NOTE]
>
>Der Eingabedatentyp bezieht sich auf die Spalte, auf die die Imputation angewendet wird. Der Ausgabedatentyp bezieht sich auf die Spalte, die nach dem Inkrafttreten der Umwandlung als Ausgabe erzeugt wird.

#### Numerischer Imputer {#numeric-imputer}

Der Transformator **Numeric Imputer** schließt fehlende Werte in einem Datensatz ab. Hierbei wird entweder der Mittelwert, der Median oder der Modus der Spalten verwendet, in denen sich die fehlenden Werte befinden. Die Eingabespalten sollten entweder `DoubleType` oder `FloatType` sein. Weitere Informationen und Beispiele finden Sie in der Dokumentation zum Spark-Algorithmus ](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer).[

>[!NOTE]
>
>Alle Nullwerte in Eingabespalten werden als fehlend behandelt und daher auch als impliziert.

**Datentypen**

- Eingabedatentyp: Numerisch
- Ausgabedatentyp: Numerisch

**Definition**

```sql
transformer(numeric_imputer(hour, 'mean') hour_imputed)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
| -------- | ------------ | ----- | -------- | -------- |
| `STRATEGY` | Eine Imputationsstrategie. Die verfügbaren Werte sind: [`mean`, `median`, `mode`]. | Zeichenfolge | mean | optional |

{style="table-layout:auto"}

**Beispiel vor Imputation**

| id | hour |
|---|---|
| 0 | 18,0 |
| 1 | null |
| 2 | 8,0 |

**Beispiel nach Imputation (unter Verwendung der mittleren Strategie)**

| id | hour |
|---|---|
| 0 | 18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

#### Zeichenfolgen-Imputer {#string-imputer}

Der Transformator **String imputer** schließt fehlende Werte in einem Datensatz ab, indem eine vom Benutzer als Funktionsargument bereitgestellte Zeichenfolge verwendet wird. Die Eingabe- und Ausgabespalten sollten dem Datentyp `string` entsprechen.

>[!NOTE]
>
>Alle Nullwerte in den Eingabespalten werden als fehlend behandelt und durch die angegebene Zeichenfolge ersetzt.

**Datentypen**

- Eingabedatentyp: String
- Ausgabedatentyp: Zeichenfolge

**Definition**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Der Wert, der Nullen ersetzt. | Zeichenfolge | ml_unknown | optional |

{style="table-layout:auto"}

**Beispiel vor Imputation**

| id | name |
|---|---|
| 0 | John |
| 1 | null |
| 2 | Alice |

**Beispiel nach Imputation (Verwendung von &#39;ml_unknown&#39; als Ersatz)**

| id | name |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### Boolescher Fehler {#boolean-imputer}

Der Transformator **Boolescher Imputer** schließt fehlende Werte in einem Datensatz für eine boolesche Spalte ab. Die Eingabe- und Ausgabespalten sollten den Typ `Boolean` aufweisen.

>[!NOTE]
>
>Alle Nullwerte in Eingabespalten werden als fehlend behandelt und durch den angegebenen booleschen Wert ersetzt.

**Datentypen**

- Eingabedatyp: Boolesch
- Ausgabedatyp: Boolesch

**Definition**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Boolescher Fehler. Zulässige Werte: [`true`, `false`]. | Boolescher Wert | false | optional |

**Beispiel vor Imputation**

| id | Markierung |
|---|---|
| 0 | wahr |
| 1 | null |
| 2 | false |

**Beispiel nach Imputation (Verwendung von &quot;true&quot;als Ersatz)**

| id | Markierung |
|---|---|
| 0 | wahr |
| 1 | wahr |
| 2 | false |

#### Vektormonteur {#vector-assembler}

Der Transformator `VectorAssembler` kombiniert eine angegebene Liste von Eingabespalten in einer einzigen Vektorspalte, wodurch die Verwaltung mehrerer Funktionen in Modellen für maschinelles Lernen vereinfacht wird. Dies ist besonders nützlich für die Zusammenführung von Rohfunktionen und Funktionen, die von verschiedenen Feature Transformatoren generiert wurden, in einen einheitlichen Funktionsvektor. `VectorAssembler` akzeptiert Eingabespalten von numerischen, booleschen und Vektortypen. In jeder Zeile werden die Werte der Eingabespalten in der angegebenen Reihenfolge zu einem Vektor verkettet.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**Datentypen**

- Eingabedatentyp: `array[string]` (Spaltennamen mit numerischen/Array[numerischen] Werten)
- Ausgabedatentyp: `Vector[double]`

**Definition**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
| -------- | ------------ | ----- | -------- | -------- |
| Nicht zutreffend | Für diesen Transformator sind keine zusätzlichen Parameter erforderlich. | Nicht zutreffend | Nicht zutreffend | Nicht zutreffend |

{style="table-layout:auto"}

**Beispiel vor der Umwandlung**

| id | hour | mobile | userFeatures | geklickt |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1,0 | [0.0, 10.0, 0.5] | 1,0 |

{style="table-layout:auto"}

**Beispiel nach der Umwandlung**

| id | hour | mobile | userFeatures | geklickt | Funktionen |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1,0 | [0.0, 10.0, 0.5] | 1,0 | [18.0, 1.0, 0.0, 10.0, 0.5] |

{style="table-layout:auto"}

### Numerische Transformationen {#numeric-transformations}

In diesem Abschnitt erfahren Sie mehr über die verfügbaren Transformatoren zur Verarbeitung und Skalierung numerischer Daten. Diese Transformatoren sind erforderlich, um numerische Funktionen in Ihren Datensätzen zu handhaben und zu optimieren.

#### Binarizer {#binarizer}

Der Transformator `Binarizer` konvertiert numerische Funktionen durch einen Prozess, der als Binarisierung bezeichnet wird, in binäre Funktionen (0/1). Funktionswerte, die über dem festgelegten Schwellenwert liegen, werden in 1,0 umgewandelt, Werte, die kleiner oder gleich dem Schwellenwert sind, in 0,0. Der `Binarizer` unterstützt sowohl den Typ `Vector` als auch den Typ `Double` für die Eingabespalte.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#binarizer). -->

**Datentypen**

- Eingabedatentyp: Numerische Spalte
- Ausgabedatentyp: Numerisch

**Definition**

```sql
transform(numeric_imputer(rating, 'mode') rating_imp, binarizer(rating_imp) rating_binarizer)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|------------|----------------------------------------------------------------------------------------------------------|----------|----------|----------|
| `THRESHOLD` | Parameter für den Schwellenwert, mit dem kontinuierliche Funktionen binarisiert werden. Funktionen, die größer als der Schwellenwert sind, werden auf 1.0 binarisiert, während Funktionen, die kleiner oder gleich dem Schwellenwert sind, auf 0.0 binarisiert werden. | int/double | 0,0 | optional |

{style="table-layout:auto"}

**Beispieleingabe vor der Binarisierung**

| id | Bewertung |
|---|---------|
| 0 | -18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

**Beispielausgabe nach der Binarisierung (Standardschwellenwert 0.0)**

| id | Bewertung |
|---|---------|
| 0 | 0,0 |
| 1 | 1,0 |
| 2 | 1,0 |

**Definition mit benutzerdefiniertem Schwellenwert**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**Beispielausgabe nach der Binarisierung (mit einem Schwellenwert von 14,0)**

| id | age |
|---|-------|
| 0 | 0,0 |
| 1 | 0,0 |
| 2 | 1,0 |

#### Bucketizer {#bucketizer}

Der Transformator `Bucketizer` konvertiert eine Spalte mit kontinuierlichen Funktionen basierend auf benutzerdefinierten Schwellenwerten in eine Spalte mit Funktionsbuckets. Dieser Prozess ist nützlich für die Segmentierung von kontinuierlichen Daten in separate Behälter oder Behälter. Für den `Bucketizer` ist ein `splits` -Parameter erforderlich, der die Grenzen der Behälter definiert.

**Datentypen**

- Eingabedatentyp: Numerische Spalte
- Ausgabedatentyp: Numerisch (gebundene Werte)

**Definition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | Ein Parameter für die Zuordnung von kontinuierlichen Funktionen zu Buckets. Bei `n+1` -Aufspaltungen gibt es `n` Behälter. Die Aufspaltung muss in streng steigender Reihenfolge erfolgen, und der Bereich (x,y) wird für jeden Behälter verwendet, mit Ausnahme des letzten, der y enthält. | array(double) | K. A. | optional |

{style="table-layout:auto"}

**Beispiele für Aufspaltungen**

- Array(Double.NegativeInfinity, 0.0, 1.0, Double.PositiveInfinity)
- Array(0.0, 1.0, 2.0)

Aufspaltungen sollten den gesamten Bereich von Doppelwerten abdecken. Andernfalls werden Werte außerhalb der angegebenen Aufspaltungen als Fehler behandelt.

**Beispielumwandlung**

In diesem Beispiel wird eine Spalte mit kontinuierlichen Funktionen (`course_duration`) verwendet, gemäß dem bereitgestellten `splits` gebunden und dann die resultierenden Behälter mit anderen Funktionen zusammengestellt.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

Der Transformator `MinMaxScaler` skaliert jede Funktion in einem Datensatz mit Vektorzeilen in einen bestimmten Bereich, in der Regel [0, 1]. Dadurch wird sichergestellt, dass alle Funktionen gleichermaßen zum Modell beitragen. Dies ist insbesondere bei Modellen nützlich, die für die Funktionsskalierung sensibel sind, wie z. B. Algorithmen, die auf der Grundlage von Farbabständen arbeiten. Der `MinMaxScaler` arbeitet mit den folgenden Parametern:

- **min**: Die untere Grenze der Transformation, die von allen Funktionen gemeinsam genutzt wird. Der Standardwert ist `0.0`.
- **max**: Die obere Grenze der Transformation, die von allen Funktionen gemeinsam genutzt wird. Der Standardwert ist `1.0`.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#minmaxscaler).  -->

**Datentypen**

- Eingabedatentyp: `Array[Double]`
- Ausgabedatentyp: `Array[Double]`

**Definition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|--------------------------------------------------------------------------------------------------|------|---------|----------|
| `min` | Untergrenze nach der Transformation, freigegeben für alle Funktionen. | double | 0,0 | optional |
| `max` | Obere Grenze nach der Transformation, freigegeben für alle Funktionen. | double | 1,0 | optional |

**Beispielumwandlung**

In diesem Beispiel wird eine Reihe von Funktionen transformiert, indem sie mithilfe von MinMaxScaler nach mehreren anderen Transformationen auf den angegebenen Bereich skaliert werden.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

Der Transformator `MaxAbsScaler` skaliert jede Funktion in einem Datensatz mit Vektorzeilen in den Bereich [-1, 1], indem er durch den maximalen absoluten Wert jeder Funktion dividiert wird. Diese Umwandlung eignet sich ideal zur Beibehaltung der Sparsamkeit in Datensätzen mit positiven und negativen Werten, da die Daten nicht verschoben oder zentriert werden. Dadurch ist der `MaxAbsScaler` besonders für Modelle geeignet, die für die Skalierung der Eingabefunktionen sensibel sind, z. B. für Entfernungsberechnungen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#maxabsscaler). -->

**Datentypen**

- Eingabedatentyp: `Array[Double]`
- Ausgabedatentyp: `Array[Double]`

**Definition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|---------------------------------------------------------------------------------------------------------|------|---------|----------|
| Nicht zutreffend | MaxAbsScaler benötigt für seinen Betrieb keine zusätzlichen Parameter. | Nicht zutreffend | Nicht zutreffend | Nicht zutreffend |

**Beispielumwandlung**

In diesem Beispiel werden mehrere Umwandlungen angewendet, einschließlich `MaxAbsScaler`, um Funktionen in den Bereich [-1, 1] neu zu skalieren.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### Normalizer {#normalizer}

Die `Normalizer` ist ein Transformator, der jeden Vektor in einem Datensatz mit Vektorzeilen normalisiert, sodass er über eine Einheitennorm verfügt. Dieser Prozess gewährleistet eine konsistente Skalierung, ohne die Richtung der Vektoren zu verändern. Diese Umwandlung ist besonders bei maschinellen Lernmodellen nützlich, die auf Entfernungsmessungen oder anderen vektorbasierten Berechnungen beruhen, insbesondere wenn die Größe der Vektoren stark variiert.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#normalizer) -->

**Datentypen**

- Eingabedatentyp: `array[double]` / `vector[double]`
- Ausgabedatentyp: `vector[double]`

**Definition**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|----------------------------------------------------------------------------------------|---------|---------|----------|
| `p` | Gibt die für die Normalisierung verwendete `p-norm` an (z. B. `1-norm`, `2-norm` usw.). | integer | 2 | optional |

**Beispielumwandlung**

In diesem Beispiel wird gezeigt, wie mehrere Transformationen angewendet werden, einschließlich der `Normalizer`, um eine Reihe von Funktionen mit dem angegebenen `p-norm` zu normalisieren.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### QuantileDiscretizer {#quantilediscretizer}

Der `QuantileDiscretizer` ist ein Transformator, der eine Spalte mit kontinuierlichen Funktionen in feste kategorische Merkmale konvertiert, wobei die Anzahl der Klassen durch den Parameter `numBuckets` bestimmt wird. In einigen Fällen kann die tatsächliche Anzahl der Behälter kleiner als die angegebene Zahl sein, wenn es zu wenige eindeutige Werte gibt, um genügend Mengen zu erstellen.

Diese Umwandlung ist besonders nützlich, um die Darstellung kontinuierlicher Daten zu vereinfachen oder sie für Algorithmen vorzubereiten, die mit kategorischen Eingaben besser funktionieren.

**Datentypen**

- Eingabedatentyp: Numerische Spalte
- Ausgabedatentyp: Numerische Spalte (kategorisch)

**Definition**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | Die Anzahl der Behälter (Mengen oder Kategorien), in die Datenpunkte gruppiert werden. Diese Zahl muss größer oder gleich zwei sein. | integer | 2 | optional |

**Beispielumwandlung**

Dieses Beispiel zeigt, wie die `QuantileDiscretizer` eine Spalte mit kontinuierlichen Funktionen (`hour`) in drei kategorische Behälter einbindet.

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Beispiel vor und nach der Diskretisierung**

| id | hour | result |
|---|------|--------|
| 0 | 18,0 | 2.0 |
| 1 | 19,0 | 2.0 |
| 2 | 8,0 | 1,0 |
| 3 | 5.0 | 1,0 |
| 4 | 2,2 | 0,0 |

#### StandardScaler {#standardscaler}

Der `StandardScaler` ist ein Transformator, der jedes Feature in einem Datensatz mit Vektorzeilen normalisiert, sodass eine Standardabweichung und/oder ein Nullmittelwert vorliegen. Dadurch werden die Daten für Algorithmen besser geeignet, bei denen davon ausgegangen wird, dass die Funktionen mit einer konsistenten Skalierung um null zentriert sind. Diese Transformation ist besonders wichtig für Modelle des maschinellen Lernens wie SVM, logistische Regression und neuronale Netzwerke, bei denen nicht standardisierte Daten zu Konvergenzproblemen oder einer geringeren Genauigkeit führen könnten.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**Datentypen**

- Eingabedatentyp: Vektor
- Ausgabedatentyp: Vektor

**Definition**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | Skaliert die Daten auf Standardabweichung. | Boolescher Wert | True | optional |
| `withMean` | Zentriert die Daten mit dem arithmetischen Mittel vor der Skalierung. Diese Option erzeugt eine dichte Ausgabe, daher sollten Sie bei geringer Eingabe vorsichtig sein. | Boolescher Wert | False | optional |

**Beispielumwandlung**

In diesem Beispiel wird gezeigt, wie der StandardScaler auf eine Reihe von Funktionen angewendet und mit Standardabweichung und Nullmittelwert normalisiert wird.

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### Kategorische Umwandlungen {#categorical-transformations}

In diesem Abschnitt erhalten Sie einen Überblick über die verfügbaren Transformatoren zur Konvertierung und Vorverarbeitung kategorischer Daten für Modelle des maschinellen Lernens. Diese Umwandlungen sind für Datenpunkte konzipiert, die unterschiedliche Kategorien oder Bezeichnungen und nicht numerische Werte darstellen.

#### StringIndexer {#stringindexer}

Der `StringIndexer` ist ein Transformator, der eine Zeichenfolgenspalte mit Bezeichnungen in eine Spalte mit numerischen Indizes kodiert. Die Indizes reichen von 0 bis `numLabels` und werden nach Beschriftungsfrequenz geordnet (der häufigste Titel erhält den Index von 0). Wenn die Eingabespalte numerisch ist, wird sie vor der Indizierung in eine Zeichenfolge umgewandelt. Unsichtbare Beschriftungen können dem Index `numLabels` zugewiesen werden, wenn vom Benutzer angegeben.

Diese Umwandlung ist besonders nützlich, um kategorische Zeichenfolgendaten in numerische Formulare zu konvertieren und sie für maschinelle Lernmodelle mit numerischer Eingabe zu verwenden.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**Datentypen**

- Eingabedatentyp: String
- Ausgabedatentyp: Numerisch

**Definition**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|-------------|------|---------|----------|
| Nicht zutreffend | `StringIndexer` benötigt keine zusätzlichen Parameter für den Vorgang. | Nicht zutreffend | Nicht zutreffend | Nicht zutreffend |

**Beispielumwandlung**

In diesem Beispiel wird gezeigt, wie Sie die `StringIndexer` auf eine kategorische Funktion anwenden und in einen numerischen Index konvertieren.

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

Der `OneHotEncoder` ist ein Transformator, der eine Spalte mit Bezeichnungsindizes in eine Spalte mit spärlichen Binärvektoren konvertiert, wobei jeder Vektor höchstens einen einzigen Wert hat. Diese Kodierung ist besonders nützlich, um es Algorithmen, die numerische Eingaben erfordern, wie z. B. Logistische Regression, zu ermöglichen, kategorische Daten effektiv zu integrieren.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**Datentypen**

- Eingabedatentyp: Numerisch
- Ausgabedatentyp: Vector[Int]

**Definition**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|-------------|------|---------|----------|
| Nicht zutreffend | OneHotEncoder benötigt für seinen Betrieb keine zusätzlichen Parameter. | Nicht zutreffend | Nicht zutreffend | Nicht zutreffend |

**Beispielumwandlung**

Dieses Beispiel zeigt, wie Sie zunächst den `StringIndexer` auf eine kategorische Funktion anwenden und dann mit dem `OneHotEncoder` die indizierten Werte in einen binären Vektor konvertieren.

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### Textumwandlungen {#textual-transformations}

Dieser Abschnitt enthält Details zu den Transformatoren, die zur Verarbeitung und Konvertierung von Textdaten in Formate verfügbar sind, die von Modellen für maschinelles Lernen verwendet werden können. Dieser Abschnitt ist für Entwickler von entscheidender Bedeutung, die mit natürlichen Sprachdaten und Textanalysen arbeiten.

#### CountVectorizer {#countvectorizer}

Der `CountVectorizer` ist ein Transformator, der eine Sammlung von Textdokumenten in Vektoren von Token-Zählungen konvertiert und anhand des aus dem Korpus extrahierten Vokabulars spärliche Darstellungen erzeugt. Diese Umwandlung ist für die Konvertierung von Textdaten in ein numerisches Format unerlässlich, das von maschinellen Lernalgorithmen wie LDA (Latent Dirichlet Allocation) verwendet werden kann, indem die Häufigkeit der Token in jedem Dokument dargestellt wird.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**Datentypen**

- Eingabedatentyp: Array[String]
- Ausgabedatyp: Dense Vector

**Definition**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | Maximale Größe des Vokabulars. CountVectorizer erstellt ein Vokabular, das nur die wichtigsten `vocabSize` Begriffe berücksichtigt, die nach der Häufigkeit des Begriffs im gesamten Korpus angeordnet sind. | Int | 218 | optional |
| `MIN_DOC_FREQ` | Gibt die Mindestanzahl verschiedener Dokumente an, in denen ein Begriff erscheinen muss, um in das Vokabular aufgenommen zu werden. Kann eine absolute Zahl oder ein Bruchteil von Dokumenten sein (wenn ein Doppelpunkt verwendet wird). | Double | 1,0 | optional |
| `MAX_DOC_FREQ` | Gibt die maximale Anzahl verschiedener Dokumente an, in denen ein Begriff erscheinen könnte, um in das Vokabular aufgenommen zu werden. Kann eine absolute Zahl oder ein Bruchteil von Dokumenten sein (wenn ein Doppelpunkt verwendet wird). | Double | (263)-1 | optional |
| `MIN_TERM_FREQ` | Filtert seltene Wörter in einem Dokument heraus. Begriffe mit einer Häufigkeit/Anzahl, die unter der angegebenen Schwelle liegt, werden ignoriert. Kann eine absolute Zahl oder ein Bruchteil der Tokenanzahl des Dokuments sein. | Double | 1,0 | optional |

{style="table-layout:auto"}

**Beispielumwandlung**

In diesem Beispiel wird gezeigt, wie der CountVectorizer eine Sammlung von Text-Arrays in Vektoren von Token-Zählungen konvertiert, was zu einer geringen Darstellung führt.

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Beispiel vor und nach der Vectorisierung**

| id | Texte | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(&quot;a&quot;, &quot;b&quot;, &quot;c&quot;) | (3,[0,1,2],[1.0,1.0,1.0]) |
| 1 | Array(&quot;a&quot;, &quot;b&quot;, &quot;b&quot;, &quot;c&quot;, &quot;a&quot;) | (3,[0,1,2],[2.0,2.0,1.0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

Der Transformator `NGram` ist ein Transformator, der eine Sequenz von n Gramm generiert, wobei ein n Gramm eine Sequenz von (&#39;?&#39;) Token (normalerweise Wörter) für eine ganze Zahl (`𝑛`) ist. Die Ausgabe besteht aus durch Leerzeichen getrennten Zeichenfolgen aufeinander folgender Wörter, die als Funktionen in Modellen für maschinelles Lernen verwendet werden können, insbesondere solche, die sich auf die Verarbeitung natürlicher Sprachen konzentrieren.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**Datentypen**

- Eingabedatentyp: Array[String]
- Ausgabedatentyp: Array[String]

**Definition**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | Die n-Gramm-Mindestlänge muss größer oder gleich 1 sein. | integer | 2 (bigram-Funktionen) | optional |

{style="table-layout:auto"}

**Beispielumwandlung**

Dieses Beispiel zeigt, wie der NGram-Transformator eine Sequenz von 3 Gramm aus einer Liste von Token erstellt, die aus Textdaten abgeleitet wurden.

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Beispiel vor und nach der n-Gramm-Transformation**

| id | Texte | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [&quot;this&quot;, &quot;was&quot;, &quot;an&quot;, &quot;unterhaltsam&quot;, &quot;movie&quot;] | [&quot;dies war ein&quot;, &quot;war ein unterhaltsamer&quot;, &quot;unterhaltsamer Film&quot;] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

Der `StopWordsRemover` ist ein Transformator, der Stoppwörter aus einer Folge von Zeichenfolgen entfernt und häufig verwendete Wörter herausfiltert, die keine bedeutende Bedeutung haben. Als Eingabe dient eine Folge von Zeichenfolgen (z. B. die Ausgabe eines Tokenizers) und entfernt alle Stoppwörter, die vom Parameter `stopWords` angegeben werden.

Diese Umwandlung ist nützlich für die Vorverarbeitung von Textdaten, wodurch die Effektivität nachgelagerter Modelle des maschinellen Lernens verbessert wird, indem Wörter eliminiert werden, die nicht viel zur allgemeinen Bedeutung beitragen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**Datentypen**

- Eingabedatentyp: Array[String]
- Ausgabedatentyp: Array[String]

**Definition**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | Die zu filternden Wörter. | array [string] | Standard: English stop words | optional |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**Beispielumwandlung**

Dieses Beispiel zeigt, wie die `StopWordsRemover` gängige englische Stoppwörter aus einer Token-Liste herausfiltert.

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Beispiel vor und nach dem Entfernen von Stoppwörtern**

| id | raw | filtern |
|----|------------------------------|--------------------------|
| 0 | [I, sah, the, red, ballon] | [Säge, rot, Ballon] |
| 1 | [Mary, hatte, ein, kleines, Lamm] | [Mary, small, lamb] |

**Beispiel mit benutzerdefinierten Stoppwörtern**

In diesem Beispiel wird gezeigt, wie mithilfe einer benutzerdefinierten Liste von Stoppwörtern bestimmte Wörter aus den Eingabesequenzen herausgefiltert werden.

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**Beispiel vor und nach dem Entfernen benutzerdefinierter Stoppwörter**

| id | raw | filtern |
|----|------------------------------|--------------------------|
| 0 | [I, sah, the, red, ballon] | [sah, the, ballon] |
| 1 | [Mary, hatte, ein, kleines, Lamm] | [Mary, a, small, lamb] |

#### TF-IDF {#tf-idf}

Die &quot;`TF-IDF`&quot;(Term Frequency-Inverse Document Frequency) ist ein Transformator, mit dem die Bedeutung eines Wortes in einem Dokument in Bezug auf einen Korpus gemessen wird. Die Begriffsfrequenz (TF) bezeichnet die Häufigkeit, mit der ein Begriff \(t\) in einem Dokument angezeigt wird \(d\), während die Dokumentfrequenz (DF) misst, wie viele Dokumente im Korpus \(D\) den Begriff \(t\) enthalten. Diese Methode wird im Text-Mining häufig verwendet, um den Einfluss häufig auftretender Wörter wie &quot;a&quot;, &quot;the&quot;und &quot;of&quot;zu reduzieren, die wenig eindeutige Informationen enthalten.

Diese Transformation ist besonders bei der Textgewinnung und der Verarbeitung natürlicher Sprachen nützlich, da sie der Bedeutung jedes Wortes innerhalb eines Dokuments und im gesamten Korpus einen numerischen Wert zuweist.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**Datentypen**

- Eingabedatentyp: Array[String]
- Ausgabedatentyp: Vector[Int]

**Definition**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | Die Anzahl der zu generierenden Funktionen. Muss größer als 0 sein. | Int | 262144 | optional |
| `MIN_DOC_FREQ` | Die Mindestanzahl von Dokumenten, in denen ein Begriff im Modell enthalten sein muss. | Int | 0 | optional |

{style="table-layout:auto"}

**Beispielumwandlung**

Dieses Beispiel zeigt, wie man mit TF-IDF tokenisierte Sätze in einen Funktionsvektor umwandelt, der die Bedeutung jedes Begriffs im Kontext des gesamten Korpus darstellt.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenizer {#tokenizer}

Die `Tokenizer` ist ein Transformator, der Text, wie z. B. einen Satz, in einzelne Begriffe, normalerweise Wörter, aufteilt. Er konvertiert Sätze in Token-Arrays und stellt einen grundlegenden Schritt in der Textvorverarbeitung dar, der die Daten für weitere Textanalyse- oder Modellierungsprozesse vorbereitet.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**Datentypen**

- Eingabedatentyp: Textsatz
- Ausgabedatentyp: Array[String]

**Definition**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|-------------|------|---------|----------|
| Nicht zutreffend | Die `Tokenizer` benötigt keine zusätzlichen Parameter für den Vorgang. | Nicht zutreffend | Nicht zutreffend | Nicht zutreffend |

**Beispielumwandlung**

Dieses Beispiel zeigt, wie der `Tokenizer` Sätze im Rahmen einer Textverarbeitungs-Pipeline in einzelne Wörter (Token) unterteilt.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vc {#word2vec}

Die `Word2Vec` ist ein Schätzer, der eine Sequenz von Wörtern verarbeitet, die Dokumente darstellen, und eine `Word2VecModel` trainiert. Dieses Modell ordnet jedes Wort einem eindeutigen Vektor fester Größe zu und wandelt jedes Dokument in einen Vektor um, indem die Vektoren aller Wörter im Dokument gemittelt werden. `Word2Vec` wird in Aufgaben zur Verarbeitung natürlicher Sprachen verwendet und erstellt Worteinbettungen, die die semantische Bedeutung erfassen. Dabei werden Textdaten in numerische Vektoren umgewandelt, die die Beziehungen zwischen Wörtern darstellen und effizientere Textanalysen und Modelle für maschinelles Lernen ermöglichen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#word2vec) -->

**Datentypen**

- Eingabedatentyp: Array[String]
- Ausgabedatentyp: Vector[Double]

**Definition**

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|--------------|-----------------------------------------------------------------------------------------------------|---------|---------|----------|
| `VECTOR_SIZE` | Die Dimension des Vektors, in den jedes Wort umgewandelt wird. | Ganzzahl | 100 | optional |
| `MIN_COUNT` | Die Mindestanzahl, mit der ein Token im Vokabular des `Word2Vec`-Modells enthalten zu sein scheint. | Ganzzahl | 5 | optional |

{style="table-layout:auto"}

**Beispielumwandlung**

Dieses Beispiel zeigt, wie `Word2Vec` einen tokenisierten Review in einen Vektor mit fester Größe konvertiert, der den Durchschnitt der Wortvektoren im Dokument darstellt.

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Beispiel vor und nach der Word2VEC-Umwandlung**

| Überprüfung | tokenized | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| das war ein unterhaltsamer Film | [this, was, an, Entertainment, movie] | [-0.025713888928294182,0.0081879751577899,0.0092235435 731709,-0.0151538523797133,0.012175946310162545,3.112906 5901041035E-4,0.0025145105042611252,0.00575701978523284 3,-0.021328244300093502,0.00933587187550069] |

{style="table-layout:auto"}
