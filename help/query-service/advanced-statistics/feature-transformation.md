---
title: Verfahren zur Merkmalstransformation
description: Erfahren Sie mehr über wichtige Vorverarbeitungstechniken wie Datenumwandlung, Kodierung und Funktionsskalierung, die Daten für das Trainieren statistischer Modelle vorbereiten. Es behandelt die Bedeutung der Behandlung fehlender Werte und der Konvertierung kategorialer Daten, um die Modellleistung und -genauigkeit zu verbessern.
role: Developer
exl-id: ed7fa9b7-f74e-481b-afba-8690ce50c777
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '3450'
ht-degree: 9%

---

# Verfahren zur Merkmalstransformation

Umwandlungen sind wichtige Vorverarbeitungsschritte, die Daten in ein für Modellschulung und -analyse geeignetes Format konvertieren oder skalieren und so eine optimale Leistung und Genauigkeit gewährleisten. Dieses Dokument dient als ergänzende Syntaxressource und liefert detaillierte Details zu den wichtigsten Funktionstransformationstechniken für die Datenvorverarbeitung.

Modelle für maschinelles Lernen können Zeichenfolgenwerte oder Nullwerte nicht direkt verarbeiten, was die Vorverarbeitung von Daten unerlässlich macht. In diesem Handbuch wird erläutert, wie Sie verschiedene Transformationen verwenden können, um fehlende Werte zuzuordnen, kategoriale Daten in numerische Formate zu konvertieren und Funktionsskalierungstechniken wie One-Hot-Kodierung und Vektorisierung anzuwenden. Diese Methoden ermöglichen es Modellen, die Daten effektiv zu interpretieren und daraus zu lernen, was letztendlich die Leistung verbessert.

## Automatische Merkmalstransformation {#automatic-transformations}

Wenn Sie die `TRANSFORM`-Klausel in Ihrem `CREATE MODEL`-Befehl überspringen, wird die Funktionstransformation automatisch durchgeführt. Die automatische Datenvorverarbeitung umfasst einen Nullersatz und Standardfunktionstransformationen (basierend auf dem Datentyp). Numerische Spalten und Textspalten werden automatisch berechnet. Anschließend werden Merkmalstransformationen durchgeführt, um sicherzustellen, dass die Daten in einem für das Modell-Training des maschinellen Lernens geeigneten Format vorliegen. Dieser Prozess umfasst fehlende Datenimputation und kategoriale, numerische und boolesche Transformationen.

>[!IMPORTANT]
>
>Die zum Zeitpunkt des Trainings verwendete Merkmalstransformation wird auch zur Merkmalstransformation zum Zeitpunkt der Prognose und Auswertung verwendet.

In den folgenden Tabellen wird erläutert, wie verschiedene Datentypen verarbeitet werden, wenn die `TRANSFORM`-Klausel während des `CREATE MODEL`-Befehls weggelassen wird.

### Null-Ersatz {#automatic-null-replacement}

| Datentyp | Null-Ersatz |
|-----------------|-----------------------------------------------------|
| Numerisch | NULL werden durch den Mittelwert der Spalte ersetzt. |
| Kategorisch | NULL-Werte werden durch das `ml_unknown`-Schlüsselwort ersetzt. |
| Boolesch | NULL-Werte werden durch einen `FALSE` Wert ersetzt. |
| Zeitstempel | Es wird erwartet, dass dies ein kontinuierliches Feld ist. |
| Verschachtelt/STRUCT | Die Ersetzung hängt vom Datentyp des Blattknotens ab. |

### Funktionstransformation {#automatic-feature-transformation}

| Datentyp | Merkmalstransformation |
|-----------------|-----------------------------------------------------|
| Numerisch | NICHT ERFORDERLICH - Dieser Datentyp wird von Algorithmen des maschinellen Lernens verstanden. |
| String | Zeichenfolgen-Indizierung erfolgt. |
| Boolesch | Zeichenfolgen-Indizierung erfolgt. |
| Zeitstempel | Es wird kein Vorgang ausgeführt. |
| STRUKTUR | Der Wert wird auf seinen Endknoten erweitert. Die Umwandlung erfolgt basierend auf dem Datentyp des Blattknotens. |

**Beispiel**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## Manuelle Funktionstransformationen {#manual-transformations}

Um die benutzerdefinierte Datenvorverarbeitung in Ihrer `CREATE MODEL`-Anweisung zu definieren, verwenden Sie die `TRANSFORM`-Klausel in Kombination mit einer beliebigen Anzahl der verfügbaren Umwandlungsfunktionen. Diese manuellen Vorverarbeitungsfunktionen können auch außerhalb der `TRANSFORM`-Klausel verwendet werden. Alle im Abschnitt [Transformator unten“ beschriebenen Transformationen &#x200B;](#available-transformations) zur manuellen Vorverarbeitung der Daten verwendet werden.

### Hauptmerkmale {#key-characteristics}

Bei der Definition der Vorverarbeitungsfunktionen sind die folgenden Hauptmerkmale der Funktionstransformation zu berücksichtigen:

- **Syntax**: `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - Der Aliasname ist in der Syntax obligatorisch. Sie müssen einen Aliasnamen angeben, da sonst die Abfrage fehlschlägt.

- **Parameter**: Die Parameter sind Positionsargumente. Das bedeutet, dass jeder Parameter nur bestimmte Werte annehmen kann und alle vorangehenden Parameter angeben muss, wenn benutzerdefinierte Werte bereitgestellt werden. Einzelheiten dazu, welche Funktion welches Argument verwendet, finden Sie in der entsprechenden Dokumentation.

- **Kettentransformatoren**: Die Ausgabe eines Transformators kann als Eingabe für einen anderen Transformator verwendet werden.

- **Funktionsnutzung**: Die letzte Merkmalstransformation wird als Feature des Modells für maschinelles Lernen verwendet.

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

## Verfügbare Umwandlungen {#available-transformations}

Es gibt 19 verfügbare Transformationen. Diese Transformationen sind unterteilt in [Allgemeine Transformationen](#general-transformations), [Numerische Transformationen](#numeric-transformations), [Kategoriale Transformationen](#categorical-transformations) und [Texttransformationen](#textual-transformations).

### Allgemeine Transformationen {#general-transformations}

Lesen Sie diesen Abschnitt für Details zu den Transformatoren, die für eine Vielzahl von Datentypen verwendet werden. Diese Informationen sind wichtig, wenn Sie Umwandlungen anwenden müssen, die nicht spezifisch für kategoriale oder textuelle Daten sind.

>[!NOTE]
>
>Der Eingabedatentyp bezieht sich auf die Spalte, auf die die Imputation angewendet wird. Der Ausgabedatentyp bezieht sich auf die Spalte, die nach Wirksamwerden der Transformation als Ausgabe erzeugt wird.

#### numerischer Computer {#numeric-imputer}

Der Transformator **Numerischer**) vervollständigt fehlende Werte in einem Datensatz. Dabei wird entweder der Mittelwert, Median oder Modus der Spalten verwendet, in denen sich die fehlenden Werte befinden. Die Eingabespalten sollten entweder `DoubleType` oder `FloatType` sein. Weitere Informationen und Beispiele finden Sie in der Dokumentation zum [-Algorithmus &#x200B;](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer).

>[!NOTE]
>
>Alle Nullwerte in Eingabespalten werden als fehlend behandelt und daher ebenfalls unterstellt.

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
| `STRATEGY` | Eine Imputationsstrategie. Die verfügbaren Werte sind: [`mean`, `median`, `mode`]. | Zeichenfolge | mean | fakultativ |

{style="table-layout:auto"}

**Beispiel vor der Imputation**

| id | hour |
|---|---|
| 0 | 18,0 |
| 1 | null |
| 2 | 8,0 |

**Beispiel nach Imputation (mit Mittelwertstrategie)**

| id | hour |
|---|---|
| 0 | 18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

#### Streichrechner {#string-imputer}

Der **String-**) vervollständigt fehlende Werte in einem Datensatz mithilfe einer vom Benutzer als Funktionsargument bereitgestellten Zeichenfolge. Die Eingabe- und Ausgabespalten sollten vom `string` Datentyp sein.

>[!NOTE]
>
>Alle Nullwerte in Eingabespalten werden als fehlend behandelt und durch die angegebene Zeichenfolge ersetzt.

**Datentypen**

- Eingabedatentyp: Zeichenfolge
- Ausgabedatentyp: Zeichenfolge

**Definition**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Der Wert, der NULL ersetzt. | Zeichenfolge | ml_unknown | fakultativ |

{style="table-layout:auto"}

**Beispiel vor der Imputation**

| id | name |
|---|---|
| 0 | John |
| 1 | null |
| 2 | Alice |

**Beispiel nach der Imputation (mit &#39;ml_unknown&#39; als Ersatz)**

| id | name |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### Boolescher Rechner {#boolean-imputer}

Der **boolesche Computer**-Transformator vervollständigt fehlende Werte in einem Datensatz für eine boolesche Spalte. Die Eingabe- und Ausgabespalten müssen vom `Boolean` Typ sein.

>[!NOTE]
>
>Alle Nullwerte in Eingabespalten werden als fehlend behandelt und durch den angegebenen booleschen Wert ersetzt.

**Datentypen**

- Eingabedatentyp: Boolean
- Ausgabedatentyp: Boolean

**Definition**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | Boolescher Computer. Zulässige Werte: [`true`, `false`]. | Boolescher Wert | false | fakultativ |

**Beispiel vor der Imputation**

| id | Markierung |
|---|---|
| 0 | wahr |
| 1 | null |
| 2 | false |

**Beispiel nach der Imputation (mit „true“ als Ersatz)**

| id | Markierung |
|---|---|
| 0 | wahr |
| 1 | wahr |
| 2 | false |

#### Vektor-Assembler {#vector-assembler}

Der `VectorAssembler`-Transformator kombiniert eine bestimmte Liste von Eingabespalten zu einer einzigen Vektorspalte, was die Verwaltung mehrerer Funktionen in Modellen für maschinelles Lernen erleichtert. Dies ist besonders nützlich für die Zusammenführung von Rohmerkmalen und von verschiedenen Merkmalstransformatoren generierten Merkmalen zu einem einheitlichen Merkmalsvektor. `VectorAssembler` akzeptiert Eingabespalten von numerischen, booleschen und Vektortypen. In jeder Zeile werden die Werte der Eingabespalten zu einem Vektor in der angegebenen Reihenfolge verkettet.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**Datentypen**

- Eingabedatentyp: `array[string]` (Spaltennamen mit numerischen/Array[numerischen ])
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

| id | hour | mobile | userFeatures | Geklickt |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1,0 | [0,0, 10,0, 0,5 ] | 1,0 |

{style="table-layout:auto"}

**Beispiel nach der Umwandlung**

| id | hour | mobile | userFeatures | Geklickt | Funktionen |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1,0 | [0,0, 10,0, 0,5 ] | 1,0 | [18.0, 1.0, 0.0, 10.0, 0.5] |

{style="table-layout:auto"}

### Numerische Transformationen {#numeric-transformations}

Lesen Sie diesen Abschnitt, um mehr über die verfügbaren Transformatoren zur Verarbeitung und Skalierung numerischer Daten zu erfahren. Diese Transformatoren sind erforderlich, um numerische Funktionen in Ihren Datensätzen zu verarbeiten und zu optimieren.

#### Binarisierer {#binarizer}

Der `Binarizer`-Transformator wandelt numerische Merkmale in binäre (0/1) Merkmale durch einen Prozess, der als Binarisierung bezeichnet wird. Funktionswerte, die größer als der angegebene Schwellenwert sind, werden in 1,0 konvertiert, während Werte, die gleich oder kleiner als der Schwellenwert sind, in 0,0 konvertiert werden. Der `Binarizer` unterstützt sowohl `Vector`- als auch `Double` für die Eingabespalte.

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
| `THRESHOLD` | Parameter für den Schwellenwert, der zum Binarisieren kontinuierlicher Funktionen verwendet wird. Funktionen, die größer als der Schwellenwert sind, werden auf 1,0 binarisiert, während Funktionen, die gleich oder kleiner als der Schwellenwert sind, auf 0,0 binarisiert werden. | int/double | 0,0 | fakultativ |

{style="table-layout:auto"}

**Beispieleingabe vor der Binarisierung**

| id | Bewertung |
|---|---------|
| 0 | -18,0 |
| 1 | 13,0 |
| 2 | 8,0 |

**Beispielausgabe nach der Binarisierung (Standardschwellenwert 0,0)**

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

#### Eimer {#bucketizer}

Der `Bucketizer`-Transformator wandelt eine Spalte mit fortlaufenden Funktionen in eine Spalte mit Funktions-Buckets um, basierend auf benutzerspezifizierten Schwellenwerten. Dieser Prozess ist nützlich für die Segmentierung kontinuierlicher Daten in separate Behälter oder Behälter. Die `Bucketizer` erfordert einen `splits`, der die Grenzen der Buckets definiert.

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
| `splits` | Ein Parameter zum Zuordnen kontinuierlicher Funktionen in Buckets. Mit `n+1` Splits gibt es `n` Eimer. Die Aufspaltung muss in steigender Reihenfolge erfolgen, und der Bereich (x,y) wird für jeden Behälter mit Ausnahme des letzten verwendet, der y enthält. | Array(double) | K. A. | fakultativ |

{style="table-layout:auto"}

**Beispiele für Aufspaltungen**

- Array(Double.NegativeInfinity, 0.0, 1.0, Double.PositiveInfinity)
- Array(0.0, 1.0, 2.0)

Die Aufspaltung sollte den gesamten Bereich doppelter Werte abdecken. Andernfalls werden Werte außerhalb der angegebenen Aufspaltung als Fehler behandelt.

**Beispieltransformation**

In diesem Beispiel wird eine Spalte mit fortlaufenden Elementen (`course_duration`) genommen, gemäß den bereitgestellten `splits` abgelegt und dann die resultierenden Behälter mit anderen Elementen zusammengestellt.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

Der `MinMaxScaler`-Transformator skaliert jedes Feature in einem Datensatz mit Vektorzeilen in einen bestimmten Bereich neu, normalerweise [0, 1]. Dadurch wird sichergestellt, dass alle Funktionen gleichermaßen zum Modell beitragen. Dies ist besonders nützlich für Modelle, die empfindlich auf die Skalierung von Funktionen reagieren, wie z. B. Algorithmen auf der Basis von Gradientenabstiegen. Die `MinMaxScaler` arbeitet mit den folgenden Parametern:

- **min**: Die Untergrenze der Transformation, die für alle Funktionen gilt. Der Standardwert ist `0.0`.
- **max**: Die obere Grenze der Transformation, die für alle Funktionen gilt. Der Standardwert ist `1.0`.

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
| `min` | Untergrenze nach der Transformation, die von allen Funktionen gemeinsam genutzt wird | double | 0,0 | fakultativ |
| `max` | Obergrenze nach der Transformation, die für alle Funktionen gilt. | double | 1,0 | fakultativ |

**Beispieltransformation**

In diesem Beispiel wird ein Satz von Funktionen umgewandelt und nach Anwendung mehrerer anderer Umwandlungen mit MinMaxScaler auf den angegebenen Bereich skaliert.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

Der `MaxAbsScaler`-Transformator skaliert jedes Merkmal in einem Datensatz von Vektorzeilen auf den Bereich [-1, ], indem er durch den maximalen absoluten Wert jedes Merkmals dividiert. Diese Transformation ist ideal, um eine geringe Dichte in Datensätzen mit sowohl positiven als auch negativen Werten zu erhalten, da dadurch die Daten nicht verschoben oder zentriert werden. Dadurch eignet sich die `MaxAbsScaler` besonders für Modelle, die empfindlich auf die Skalierung von Eingabefunktionen reagieren, wie z.B. bei Abstandsberechnungen.

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
| Nicht zutreffend | MaxAbsScaler benötigt keine zusätzlichen Parameter für seinen Betrieb. | Nicht zutreffend | Nicht zutreffend | Nicht zutreffend |

**Beispieltransformation**

In diesem Beispiel werden mehrere Transformationen, einschließlich `MaxAbsScaler`, angewendet, um Funktionen in den Bereich [-1, 1 ].

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### Normalisierer {#normalizer}

Der `Normalizer` ist ein Transformator, der jeden Vektor in einem Datensatz von Vektorzeilen normalisiert, sodass er eine Einheitennorm hat. Dieses Verfahren gewährleistet eine gleichbleibende Skalierung, ohne die Richtung der Vektoren zu verändern. Diese Transformation ist besonders nützlich bei Modellen des maschinellen Lernens, die auf Entfernungsmessungen oder anderen vektorbasierten Berechnungen basieren, insbesondere wenn die Größe von Vektoren signifikant variiert.

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
| `p` | Gibt die für die Normalisierung verwendete `p-norm` an (z. B. `1-norm`, `2-norm` usw.). | integer | 2 | fakultativ |

**Beispieltransformation**

In diesem Beispiel wird veranschaulicht, wie mehrere Umwandlungen, einschließlich der `Normalizer`, angewendet werden, um einen Satz von Funktionen mithilfe der angegebenen `p-norm` zu normalisieren.

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### QuantileDiscretizer {#quantilediscretizer}

Der `QuantileDiscretizer` ist ein Transformator, der eine Spalte mit fortlaufenden Elementen in kategoriale Elemente mit Klassen umwandelt, wobei die Anzahl der Klassen durch den `numBuckets` bestimmt wird. In einigen Fällen kann die tatsächliche Anzahl der Buckets kleiner als diese angegebene Anzahl sein, wenn zu wenige eindeutige Werte vorhanden sind, um genügend Quantile zu erstellen.

Diese Transformation ist besonders nützlich, um die Darstellung von kontinuierlichen Daten zu vereinfachen oder sie für Algorithmen vorzubereiten, die mit kategorialer Eingabe besser funktionieren.

**Datentypen**

- Eingabedatentyp: Numerische Spalte
- Ausgabedatentyp: Numerische Spalte (kategorial)

**Definition**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | Die Anzahl der Behälter (Quantile oder Kategorien), in denen Datenpunkte gruppiert werden. Diese Zahl muss größer oder gleich zwei sein. | integer | 2 | fakultativ |

**Beispieltransformation**

Dieses Beispiel zeigt, wie die `QuantileDiscretizer` eine Spalte mit kontinuierlichen Funktionen (`hour`) in drei kategoriale Behälter bindet.

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**Beispiel vor und nach der Diskretisierung**

| id | hour | Ergebnis |
|---|------|--------|
| 0 | 18,0 | 2.0 |
| 1 | 19,0 | 2.0 |
| 2 | 8,0 | 1,0 |
| 3 | 5.0 | 1,0 |
| 4 | 2,2 | 0,0 |

#### StandardScaler {#standardscaler}

Die `StandardScaler` ist ein Transformator, der jedes Merkmal in einem Datensatz von Vektorzeilen normalisiert, sodass es eine Standardabweichung und/oder einen Nullmittelwert aufweist. Durch diesen Prozess eignen sich die Daten besser für Algorithmen, bei denen davon ausgegangen wird, dass die Merkmale auf einer gleichbleibenden Skala um null zentriert sind. Diese Transformation ist besonders wichtig für Modelle des maschinellen Lernens wie SVM, logistische Regression und neuronale Netzwerke, bei denen nicht standardisierte Daten zu Konvergenzproblemen oder geringerer Genauigkeit führen könnten.

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
| `withStd` | Skaliert die Daten so, dass sie die Standardabweichung von der Einheit aufweisen. | Boolescher Wert | True | fakultativ |
| `withMean` | Zentriert die Daten mit dem Mittelwert vor der Skalierung. Diese Option erzeugt eine dichte Ausgabe. Seien Sie daher vorsichtig bei einer spärlichen Eingabe. | Boolescher Wert | False | fakultativ |

**Beispieltransformation**

Dieses Beispiel zeigt, wie der StandardScaler auf eine Reihe von Funktionen angewendet und diese mit der Standardabweichung der Einheit und dem Nullmittelwert normalisiert werden.

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### Kategorieumwandlungen {#categorical-transformations}

In diesem Abschnitt finden Sie einen Überblick über die verfügbaren Transformatoren zum Konvertieren und Vorverarbeiten kategorialer Daten für Modelle für maschinelles Lernen. Diese Umwandlungen wurden für Datenpunkte entwickelt, die anstelle von numerischen Werten einzelne Kategorien oder Beschriftungen darstellen.

#### StringIndexer {#stringindexer}

Der `StringIndexer` ist ein Transformator, der eine Zeichenfolgenspalte von Kennzeichnungen in eine Spalte numerischer Indizes kodiert. Die Indizes liegen im Bereich von 0 bis `numLabels` und sind nach Kennzeichnungsfrequenz geordnet (die häufigste Kennzeichnung erhält einen Index von 0). Wenn die Eingabespalte numerisch ist, wird sie vor der Indizierung in eine Zeichenfolge umgewandelt. Nicht sichtbare Kennzeichnungen können dem `numLabels` zugewiesen werden, wenn sie vom Benutzer angegeben wurden.

Diese Umwandlung ist besonders nützlich, um kategoriale Zeichenfolgendaten in numerische Formulare zu konvertieren, sodass sie für Modelle des maschinellen Lernens geeignet sind, die eine numerische Eingabe erfordern.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**Datentypen**

- Eingabedatentyp: Zeichenfolge
- Ausgabedatentyp: Numerisch

**Definition**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|-------------|------|---------|----------|
| Nicht zutreffend | `StringIndexer` erfordert keine zusätzlichen Parameter für seinen Betrieb. | Nicht zutreffend | Nicht zutreffend | Nicht zutreffend |

**Beispieltransformation**

In diesem Beispiel wird gezeigt, wie die `StringIndexer` auf eine kategoriale Funktion angewendet und in einen numerischen Index konvertiert wird.

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

Der `OneHotEncoder` ist ein Transformator, der eine Spalte von Kennzeichnungsindizes in eine Spalte von dünnen binären Vektoren umwandelt, wobei jeder Vektor höchstens einen einzigen Wert hat. Diese Kodierung ist besonders nützlich, um Algorithmen, die eine numerische Eingabe erfordern, wie z. B. die logistische Regression, die Möglichkeit zu geben, kategoriale Daten effektiv einzubinden.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**Datentypen**

- Eingabedatentyp: Numerisch
- Ausgabedatentyp: vector[int]

**Definition**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|-------------|------|---------|----------|
| Nicht zutreffend | Für den Betrieb von OneHotEncoder sind keine zusätzlichen Parameter erforderlich. | Nicht zutreffend | Nicht zutreffend | Nicht zutreffend |

**Beispieltransformation**

Dieses Beispiel zeigt, wie Sie die `StringIndexer` zuerst auf eine kategoriale Funktion anwenden und dann die `OneHotEncoder` verwenden, um die indizierten Werte in einen binären Vektor zu konvertieren.

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### Textumwandlungen {#textual-transformations}

In diesem Abschnitt finden Sie Details zu den Transformatoren, die für die Verarbeitung und Konvertierung von Textdaten in Formate verfügbar sind, die von Modellen für maschinelles Lernen verwendet werden können. Dieser Abschnitt ist für Entwickler, die mit Daten in natürlicher Sprache und Textanalyse arbeiten, von entscheidender Bedeutung.

#### CountVectorizer {#countvectorizer}

Der `CountVectorizer` ist ein Transformator, der eine Sammlung von Textdokumenten in Vektoren der Token-Anzahl konvertiert und so spärliche Darstellungen basierend auf dem aus dem Korpus extrahierten Vokabular erzeugt. Diese Umwandlung ist wichtig, um Textdaten in ein numerisches Format zu konvertieren, das von Algorithmen für maschinelles Lernen wie LDA (Latent Dirichlet Allocation) verwendet werden kann, indem die Häufigkeit der Token in jedem Dokument dargestellt wird.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**Datentypen**

- Eingabedatentyp: Array[String]
- Ausgabedatentyp: Dichter Vektor

**Definition**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | Maximale Größe des Vokabulars. CountVectorizer erstellt ein Vokabular, das nur die `vocabSize` Begriffe berücksichtigt, die nach der Häufigkeit der Begriffe im gesamten Korpus sortiert sind. | Int | 218 | fakultativ |
| `MIN_DOC_FREQ` | Gibt die Mindestanzahl verschiedener Dokumente an, in denen ein Begriff enthalten sein muss, damit er in das Vokabular aufgenommen wird. Kann eine absolute Zahl oder ein Bruchteil von Dokumenten sein (wenn es sich um eine doppelte Zahl handelt). | Double | 1,0 | fakultativ |
| `MAX_DOC_FREQ` | Gibt die maximale Anzahl verschiedener Dokumente an, in denen ein Begriff in das Vokabular aufgenommen werden könnte. Kann eine absolute Zahl oder ein Bruchteil von Dokumenten sein (wenn es sich um eine doppelte Zahl handelt). | Double | (263)-1 | fakultativ |
| `MIN_TERM_FREQ` | Filtert seltene Wörter in einem Dokument heraus. Begriffe mit einer Häufigkeit/Anzahl kleiner als der angegebene Schwellenwert werden ignoriert. Kann eine absolute Zahl oder ein Bruchteil der Token-Anzahl des Dokuments sein. | Double | 1,0 | fakultativ |

{style="table-layout:auto"}

**Beispieltransformation**

Dieses Beispiel zeigt, wie der CountVectorizer eine Auflistung von Text-Arrays in Vektoren der Token-Anzahl konvertiert und so eine spärliche Darstellung erzeugt.

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**Beispiel vor und nach der Vektorisierung**

| id | Texte | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(„a“, „b“, „c„) | (3,[0,1,2],[1,0,1,0,1,0]) |
| 1 | Array(„a“, „b“, „b“, „c“, „a„) | (3,[0,1,2],[2,0,2,0,1,0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

Der `NGram` ist ein Transformator, der eine Sequenz von n-Gramm erzeugt, wobei ein n-Gramm eine Sequenz von (&#39;??&#39;) Token (typischerweise Wörter) für eine ganze Zahl (`𝑛`) ist. Die Ausgabe besteht aus durch Leerzeichen getrennten Zeichenfolgen aus &quot;??“ aufeinander folgenden Wörtern, die als Funktionen in Modellen für maschinelles Lernen verwendet werden können, insbesondere solche, die sich auf die Verarbeitung natürlicher Sprachen konzentrieren.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**Datentypen**

- Eingabedatentyp: Array[String]
- Ausgabedatentyp: array[string]

**Definition**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | Die Mindestlänge von n-Gramm, muss größer oder gleich 1 sein. | integer | 2 (Bigram-Funktionen) | fakultativ |

{style="table-layout:auto"}

**Beispieltransformation**

Dieses Beispiel zeigt, wie der NGram-Transformator eine Sequenz von 3-Gramm aus einer Liste von Token erstellt, die aus Textdaten abgeleitet wurden.

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**Beispiel vor und nach der n-Gramm-Transformation**

| id | Texte | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [„This“, „Was“, „An“, „Entertainment“, „Movie“] | [„Das war ein“, „war ein unterhaltsamer“, „ein unterhaltsamer Film“] |

{style="table-layout:auto"}

#### StopwordsRemover {#stopwordsremover}

Der `StopWordsRemover` ist ein Transformator, der Stoppwörter aus einer Sequenz von Zeichenfolgen entfernt und dabei gängige Wörter herausfiltert, die keine signifikante Bedeutung haben. Als Eingabe dient eine Sequenz von Zeichenfolgen (z. B. die Ausgabe eines Tokenizers) und entfernt alle Stoppwörter, die durch den `stopWords`-Parameter angegeben wurden.

Diese Umwandlung ist nützlich für die Vorverarbeitung von Textdaten und verbessert die Effektivität nachgelagerter Modelle für maschinelles Lernen, indem Wörter eliminiert werden, die nicht viel zur Gesamtbedeutung beitragen.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**Datentypen**

- Eingabedatentyp: Array[String]
- Ausgabedatentyp: array[string]

**Definition**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | Die zu filternden Wörter. | Array [Zeichenfolge] | Standard: Englisch Stoppwörter | fakultativ |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**Beispieltransformation**

Dieses Beispiel zeigt, wie die `StopWordsRemover` gängige englische Stoppwörter aus einer Liste von Token herausfiltert.

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**Beispiel vor und nach dem Entfernen von Stoppwörtern**

| id | Roh | gefiltert |
|----|------------------------------|--------------------------|
| 0 | [Ich, sah, die, rot, Ballon] | [Säge, rot, Ballon] |
| 1 | [Maria, ein kleines Lamm] | [Maria, kleines Lamm] |

**Beispiel mit benutzerdefinierten Stoppwörtern**

Dieses Beispiel zeigt, wie eine benutzerdefinierte Liste von Stoppwörtern verwendet wird, um bestimmte Wörter aus den Eingabesequenzen herauszufiltern.

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**Beispiel vor und nach dem Entfernen benutzerdefinierter Stoppwörter**

| id | Roh | gefiltert |
|----|------------------------------|--------------------------|
| 0 | [Ich, sah, die, rot, Ballon] | [Säge, der Ballon] |
| 1 | [Maria, ein kleines Lamm] | [Maria, ein kleines Lamm] |

#### TF-IDF {#tf-idf}

Der `TF-IDF` (Begriff Frequency-Inverse Document Frequency) ist ein Transformator, der verwendet wird, um die Bedeutung eines Wortes in einem Dokument relativ zu einem Korpus zu messen. Term Frequency (TF) bezieht sich auf die Anzahl, wie oft ein Term \(t\) in einem Dokument angezeigt wird \(d\), während Document Frequency (DF) misst, wie viele Dokumente im Korpus \(D\) den Term \(t\) enthalten. Diese Methode wird im Text-Mining häufig verwendet, um den Einfluss häufig vorkommender Wörter wie „a“, „the“ und „of“ zu reduzieren, die wenig eindeutige Informationen enthalten.

Diese Umwandlung ist besonders wertvoll bei der Textsuche und bei der Verarbeitung natürlicher Sprachen, da sie der Bedeutung jedes Wortes innerhalb eines Dokuments und im gesamten Korpus einen numerischen Wert zuweist.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**Datentypen**

- Eingabedatentyp: Array[String]
- Ausgabedatentyp: vector[int]

**Definition**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | Die Anzahl der zu generierenden Funktionen. Muss größer als 0 sein. | Int | 262144 | fakultativ |
| `MIN_DOC_FREQ` | Die Mindestanzahl von Dokumenten, in denen ein Begriff im Modell enthalten sein muss. | Int | 0 | fakultativ |

{style="table-layout:auto"}

**Beispieltransformation**

Dieses Beispiel zeigt, wie Sie mit TF-IDF tokenisierte Sätze in einen Merkmalsvektor verwandeln können, der die Bedeutung jedes Begriffs im Kontext des gesamten Korpus darstellt.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenizer {#tokenizer}

Der `Tokenizer` ist ein Transformator, der Text, z. B. einen Satz, in einzelne Begriffe (normalerweise Wörter) aufteilt. Er wandelt Sätze in Token-Arrays um und stellt so einen grundlegenden Schritt in der Textvorverarbeitung dar, mit dem die Daten für weitere Textanalysen oder Modellierungsprozesse vorbereitet werden.

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**Datentypen**

- Eingabedatentyp: Textsatz
- Ausgabedatentyp: array[string]

**Definition**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**Parameter**

| Parameter | Beschreibung | Typ | Standard | Optional |
|-----------|-------------|------|---------|----------|
| Nicht zutreffend | Die `Tokenizer` erfordert keine zusätzlichen Parameter für ihren Betrieb. | Nicht zutreffend | Nicht zutreffend | Nicht zutreffend |

**Beispieltransformation**

Dieses Beispiel zeigt, wie der `Tokenizer` Sätze als Teil einer Textverarbeitungs-Pipeline in einzelne Wörter (Token) aufteilt.

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2VEC {#word2vec}

Der `Word2Vec` ist ein Schätzer, der Wortfolgen verarbeitet, die Dokumente repräsentieren, und einen `Word2VecModel` trainiert. Dieses Modell ordnet jedes Wort einem eindeutigen Vektor fester Größe zu und transformiert jedes Dokument in einen Vektor, indem es die Vektoren aller Wörter im Dokument mittelt. `Word2Vec` ist bei der Verarbeitung natürlicher Sprachen weit verbreitet und schafft Worteinbettungen, die semantische Bedeutung erfassen, Textdaten in numerische Vektoren konvertieren, die die Beziehungen zwischen Wörtern darstellen und effektivere Textanalysen und Modelle für maschinelles Lernen ermöglichen.

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
| `VECTOR_SIZE` | Die Dimension des Vektors, in den jedes Wort transformiert wird. | Ganzzahl | 100 | fakultativ |
| `MIN_COUNT` | Die Mindestanzahl von Malen, wie oft ein Token im Vokabular des `Word2Vec`-Modells enthalten sein muss. | Ganzzahl | 5 | fakultativ |

{style="table-layout:auto"}

**Beispieltransformation**

Dieses Beispiel zeigt, wie `Word2Vec` eine mit einem Token versehene Überprüfung in einen Vektor mit fester Größe konvertiert, der den Durchschnitt der Wortvektoren im Dokument darstellt.

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Beispiel vor und nach der Word2Vec-Transformation**

| Überprüfung | mit einem Token versehen | Word2VEC |
|-------------------------------|--------------------------------------|---------------------------------|
| Das war ein unterhaltsamer Film | [Das war, ein, unterhaltsamer, Film] | [-0.025713888928294182,0.00818799751577899,0.0092235435731709,-0.01515385233797133,0.012175946310162545,3.1129065901041035E-4,0.0025145105042611252,0.005757019785232843,-0.021328244300093502,0.009335877187550069] |

{style="table-layout:auto"}
