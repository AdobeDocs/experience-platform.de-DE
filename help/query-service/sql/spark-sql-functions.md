---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Spark SQL-Funktionen
topic: spark sql functions
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '4900'
ht-degree: 99%

---


# [!DNL Spark] SQL-Funktionen

The [!DNL Spark] SQL helpers provide built-in [!DNL Spark] SQL functions to extend SQL functionality.

Referenz: [Dokumentation zu SQL-Funktionen](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE]
>
>Es werden nicht alle in der externen Dokumentation aufgeführten Funktionen unterstützt.

## Kategorien

- [Mathematische und statistische Operatoren und Funktionen](#math-and-statistical-operators-and-functions)
- [Logische Operatoren](#logical-operators)
- [Funktionen für Datum/Uhrzeit](#date/time-functions)
- [Aggregat-Funktionen](#aggregate-functions)
- [Arrays](#arrays)
- [Funktionen zur Umwandlung von Datentypen](#datatype-casting-functions)
- [Konvertierungs- und Formatierungsfunktionen](#conversion-and-formatting-functions)
- [Datenevaluierung](#data-evaluation)
- [Aktuelle Informationen](#current-information)

### Mathematische und statistische Operatoren und Funktionen

#### Modulo

`expr1 % expr2`: Gibt den Rest nach `expr1`/`expr2` zurück.

Beispiele:

```
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### Multiplikation

`expr1 * expr2`: Gibt `expr1`*`expr2` zurück.

Beispiel:

```
> SELECT 2 * 3;
 6
```

#### Addition

`expr1 + expr2`: Gibt `expr1`+`expr2` zurück.

Beispiel:

```
> SELECT 1 + 2;
 3
```

#### Subtraktion

`expr1 - expr2`: Gibt `expr1`-`expr2` zurück.

Beispiel:

```
> SELECT 2 - 1;
 1
```

#### Division

`expr1 / expr2`: Gibt `expr1`/`expr2` zurück. Führt immer eine Gleitkommadivision durch.

Beispiele:

```
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)`: Gibt den absoluten Wert des numerischen Werts zurück.

Beispiel:

```
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)`: Gibt den umgekehrten Kosinus (auch Arkuskosinus genannt) von `expr` zurück, wie bei der Berechnung durch `java.lang.Math.acos`.

Beispiele:

```
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### approx_percentile

`approx_percentile(col, percentage [, accuracy])`: Gibt einen Näherungswert des Perzentils der numerischen Spalte `col` zum angegebenen Prozentsatz zurück. Der Prozentwert muss zwischen 0,0 und 1,0 liegen. Der Parameter `accuracy` (Standard: 10000) ist ein positives numerisches Literal, das die Genauigkeit der Annäherung auf Kosten des Speichers kontrolliert. Höhere Werte für `accuracy` liefern eine höhere Genauigkeit, `1.0/accuracy` ist der relative Fehler der Annäherung. Wenn `percentage` ein Array ist, muss jeder Wert des Prozent-Arrays zwischen 0,0 und 1,0 liegen. In diesem Fall wird der Näherungswert des Perzentil-Arrays der Spalte `col` zum angegebenen Prozent-Array zurückgegeben.

Beispiele:

```
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asin

`asin(expr)`: Gibt den umgekehrten Sinus (auch Arkussinus genannt) von `expr` zurück, wie bei der Berechnung durch `java.lang.Math.asin`.

Beispiele:

```
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)`: Gibt den umgekehrten Tangens (auch Arkustangens genannt) von `expr` zurück, wie bei der Berechnung durch `java.lang.Math.atan`.

Beispiel:

```
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`: Gibt den Winkel im Bogenmaß Radiant zwischen der positiven x-Achse eines Koordinatensystems und dem durch die Koordinaten (`exprX`, `exprY`) festgelegten Punkt zurück, wie bei der Berechnung durch `java.lang.Math.atan2`.

Argumente:

`exprY`: Koordinate auf der y-Achse
`exprX`: Koordinate auf der x-Achse

Beispiel:

```
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`: Gibt den aus den Werten einer Gruppe berechneten Mittelwert zurück.

#### Kardinalität

`cardinality(expr)`: Gibt die Größe eines Arrays oder einer Zuordnung zurück. Die Funktion gibt -1 zurück, wenn ihre Eingabe null ist und `spark.sql.legacy.sizeOfNull` auf „true“ festgelegt ist (Standard). Wenn `spark.sql.legacy.sizeOfNull` auf „false“ festgelegt ist, gibt die Funktion für eine Null-Eingabe null zurück.

Beispiele:

```
> SELECT cardinality(array('b', 'd', 'c', 'a'));
 4
> SELECT cardinality(map('a', 1, 'b', 2));
 2
> SELECT cardinality(NULL);
 -1
```

#### cbrt

`cbrt(expr)`: Gibt den Würfel-Stamm von `expr` zurück.

Beispiel:

```
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`: Gibt die kleinste Ganzzahl zurück, die nicht kleiner ist als `expr`.

Beispiele:

```
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### ceiling

`ceiling(expr)`: Gibt die kleinste Ganzzahl zurück, die nicht kleiner ist als `expr`.

Beispiele:

```
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)`: Konvertiert `num` von `from_base` in `to_base`.

Beispiele:

```
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### corr

`corr(expr1, expr2)`: Gibt den Pearson-Koeffizienten der Korrelation zwischen einem Satz von Zahlenpaaren zurück.

#### cos

`cos(expr)`: Gibt den Kosinus von `expr` zurück, wie bei der Berechnung durch `java.lang.Math.cos`.

Beispiel:

```
> SELECT cos(0);
 1.0
```

#### cosh

`cosh(expr)`: Gibt den hyperbolischen Kosinus von `expr` zurück, wie bei der Berechnung durch `java.lang.Math.cosh`.

Argumente:
- `expr`: Hyperbolischer Winkel

Beispiel:

```
> SELECT cosh(0);
 1.0
```

#### cot

`cot(expr)`: Gibt den Kotangens von `expr` zurück, wie bei der Berechnung durch `1/java.lang.Math.cot`.

Argumente:
- `expr`: Winkel im Bogenmaß Radiant

Beispiel:

```
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()`: Berechnet den Rang eines Werts in einer Gruppe von Werten. Das Ergebnis ist 1 plus der zuvor zugewiesene Rangwert. Im Gegensatz zum `rank` der Funktion ergibt `dense_rank` keine Lücken in der Rangfolge.

#### e

`e()`: Gibt die Eulersche Zahl e zurück.

Beispiel:

```
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`: Gibt e hoch `expr` zurück.

Beispiel:

```
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)`: Gibt exp(`expr`) - 1 zurück.

Beispiel:

```
> SELECT expm1(0);
 0.0
```

#### factorial

`factorial(expr)`: Gibt die Fakultät von `expr` zurück. `expr` ist [0..20]. Andernfalls null.

Beispiel:

```
> SELECT factorial(5);
 120
```

#### floor

`floor(expr)`: Gibt die größte Ganzzahl zurück, die nicht größer ist als `expr`.

Beispiele:

```
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### greatest

`greatest(expr, ...)`: Gibt den höchsten Wert aller Parameter zurück, wobei Null-Werte übersprungen werden.

Beispiel:

```
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### hypot

`hypot(expr1, expr2)`: Gibt die Quadratwurzel aus (`expr1`<sup>2</sup> + `expr2`<sup>2</sup>) zurück.

Beispiel:

```
> SELECT hypot(3, 4);
 5.0
```

#### kurtosis

`kurtosis(expr)`: Gibt den aus den Werten einer Gruppe berechneten Kurtosis-Wert (auch Wölbung genannt) zurück.


#### least

`least(expr, ...)`: Gibt den geringsten Wert aller Parameter zurück, wobei Null-Werte übersprungen werden.

Beispiel:

```
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### levenshtein

`levenshtein(str1, str2)`: Gibt die Levenshtein-Distanz zwischen zwei angegebenen Zeichenfolgen zurück.

Beispiele:

```
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`: Gibt den natürlichen Logarithmus (Basis e) von `expr` zurück.

Beispiel:

```
> SELECT ln(1);
 0.0
```

#### log

`log(base, expr)`: Gibt den Logarithmus von `expr` mit `base` zurück.

Beispiel:

```
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`: Gibt den Logarithmus von `expr` mit Basis 10 zurück.

Beispiel:

```
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: Gibt `log(1 + expr)` zurück.

Beispiel:

```
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`: Gibt den Logarithmus von `expr` mit Basis 2 zurück.

Beispiel:

```
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`: Gibt den Maximalwert von `expr` zurück.

#### mean

`mean(expr)`: Gibt den aus den Werten einer Gruppe berechneten Mittelwert zurück.

#### min

`min(expr)`: Gibt den Minimalwert von `expr` zurück.

#### monotonically_increasing_id

`monotonically_increasing_id()`: Gibt monoton steigende 64-Bit-Ganzzahlen zurück. Es ist garantiert, dass die generierte ID monoton zunimmt und eindeutig ist, nicht aber fortlaufend. Die aktuelle Implementierung setzt die Partitions-ID in die oberen 31 Bit. Die unteren 33 Bit stellen die Datensatznummer in jeder Partition dar. Es wird angenommen, dass der Data Frame weniger als 1 Milliarde Partitionen umfasst und jede Partition weniger als 8 Milliarden Datensätze aufweist. Die Funktion ist nicht deterministisch, da ihr Ergebnis von Partitions-IDs abhängig ist.

#### negative

`negative(expr)`: Gibt den negativen Wert von `expr` zurück.

Beispiel:

```
> SELECT negative(1);
 -1
```

#### percent_rank

`percent_rank()`: Berechnet die prozentuale Rangfolge eines Werts in einer Gruppe von Werten.

#### percentile

`percentile(col, percentage [, frequency])`: Gibt den exakten Wert des Perzentils der numerischen Spalte `col` zum angegebenen Prozentsatz zurück. Der Wert von `percentage` muss zwischen 0,0 und 1,0 liegen. Der Wert von `frequency` sollte ein positiver ganzzahliger Wert sein.

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`: Gibt den exakten Wert des Perzentils der numerischen Spalte `col` zu den angegebenen Prozentsätzen zurück. Der Wert des Prozent-Arrays muss zwischen 0,0 und 1,0 liegen. Der Wert von `frequency` sollte ein positiver ganzzahliger Wert sein.

#### percentile_approx

`percentile_approx(col, percentage [, accuracy])`: Gibt einen Näherungswert des Perzentils der numerischen Spalte `col` zum angegebenen Prozentsatz zurück. Der Wert von `percentage` muss zwischen 0,0 und 1,0 liegen. Der Parameter `accuracy` (Standard: 10000) ist ein positives numerisches Literal, das die Genauigkeit der Annäherung auf Kosten des Speichers kontrolliert. Höhere Werte für `accuracy` liefern eine höhere Genauigkeit, `1.0/accuracy` ist der relative Fehler der Annäherung. Wenn `percentage` ein Array ist, muss jeder Wert des Prozent-Arrays zwischen 0,0 und 1,0 liegen. In diesem Fall wird der Näherungswert des Perzentil-Arrays der Spalte `col` zum angegebenen Prozent-Array zurückgegeben.

Beispiele:

```
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()`: Gibt pi zurück.

Beispiel:

```
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)`: Gibt den positiven Wert von `expr1` mod-`expr2` zurück.

Beispiele:

```
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### positive

`positive(expr)`: Gibt den positiven Wert von `expr` zurück.

#### pow

`pow(expr1, expr2)`: Bildet die Potenz von `expr1` hoch `expr2`.

Beispiel:

```
> SELECT pow(2, 3);
 8.0
```

#### power

`power(expr1, expr2)`: Bildet die Potenz von `expr1` hoch `expr2`.

Beispiele:

```
> SELECT power(2, 3);
 8.0
```

#### radians

`radians(expr)`: Konvertiert Grad ins Bogenmaß Radiant.

Argumente:

- `expr`: Winkel in Grad.

Beispiel:

```
> SELECT radians(180);
 3.141592653589793
```

#### rand

`rand([seed])`: Gibt einen zufälligen Wert mit unabhängigen und identisch verteilten (u. i. v.) gleichverteilten Werten in (0, 1) zurück.

Beispiele:

```
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE]
>
>Diese Funktion ist im Allgemeinen nicht deterministisch.

#### randn

`randn([seed])`: Gibt einen zufälligen Wert mit unabhängigen und identisch verteilten (u. i. v.) Werten zurück, die aus der Standardnormalverteilung entnommen werden.

Beispiele:

```
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE]
>
>Diese Funktion ist im Allgemeinen nicht deterministisch.

#### rint

`rint(expr)`: Gibt den Dublettenwert zurück, der am nächsten am Wert des Arguments liegt und gleich einer mathematischen Ganzzahl ist.

Beispiele:

```
> SELECT rint(12.3456);
 12.0
```

#### round

`round(expr, d)`: Gibt `expr` unter Verwendung des Rundungsmodus HALF_UP auf `d` Dezimalstellen gerundet zurück.

Beispiel:

```
> SELECT round(2.5, 0);
 3.0
```

#### sign

`sign(expr)`: Gibt -1,0, 0,0 oder 1,0 zurück, wenn `expr` negativ, 0 oder positiv ist.

Beispiel:

```
> SELECT sign(40);
 1.0
```

#### signum

`signum(expr)`: Gibt -1,0, 0,0 oder 1,0 zurück, wenn `expr` negativ, 0 oder positiv ist.

Beispiel:

```
> SELECT signum(40);
 1.0
```

#### sin

`sin(expr)`: Gibt den Sinus von `expr` zurück, wie bei der Berechnung durch `java.lang.Math.sin`.

Argumente:

- `expr`: Winkel im Bogenmaß Radiant

Beispiel:

```
> SELECT sin(0);
 0.0
```

#### sinh

`sinh(expr)`: Gibt den hyperbolischen Sinus von `expr` zurück, wie bei der Berechnung durch `java.lang.Math.sinh`.

Argumente:

- `expr`: Hyperbolischer Winkel

Beispiel:

```
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)`: Gibt die Quadratwurzel von `expr` zurück.

Beispiel:

```
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`: Gibt die aus den Werten einer Gruppe berechnete Standardabweichung der Stichprobe zurück.

#### stddev_pop

`sttdev_pop(expr)`: Gibt die aus den Werten einer Gruppe berechnete Standardabweichung der Population zurück.

#### stddev_samp

`stddev_samp(expr)`: Gibt die aus den Werten einer Gruppe berechnete Standardabweichung der Stichprobe zurück.

#### sum

`sum(expr)`: Gibt die aus den Werten einer Gruppe berechnete Summe zurück.

#### tan

`tan(expr)`: Gibt den Tangens von `expr` zurück, wie bei der Berechnung durch `java.lang.Math.tan`.

Argumente:

- `expr`: Winkel im Bogenmaß Radiant

Beispiel:

```
> SELECT tan(0);
 0.0
```

#### tanh

`tanh(expr)`: Gibt den hyperbolischen Tangens von `expr` zurück, wie bei der Berechnung durch `java.lang.Math.tanh`.

Argumente:

- `expr`: Hyperbolischer Winkel

Beispiel:

```
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)`: Gibt die aus den Werten einer Gruppe berechnete Varianz der Population zurück.

#### Var_samp

`var_samp(expr)`: Gibt die aus den Werten einer Gruppe berechnete Varianz der Stichprobe zurück.

#### variance

`variance(expr)`: Gibt die aus den Werten einer Gruppe berechnete Varianz der Stichprobe zurück.

### Logische Operatoren

#### Logisches Nicht

`! expr`: Logisches Nicht.

#### Kleiner als

`expr1 < expr2`: Gibt „true“ zurück, wenn `expr1` kleiner ist als `expr2`.

Argumente:

- `expr1, expr2`: Die beiden Ausdrücke müssen denselben Typ aufweisen oder in einen gemeinsamen Typ umgewandelt werden, und es muss sich um einen Typ handeln, der sortiert werden kann. So ist etwa der Zuordnungstyp nicht sortierbar, daher wird er nicht unterstützt. Bei komplexen Typen wie Array/Struktur müssen die Datentypen der Felder sortierbar sein.

Beispiele:

```
> SELECT 1 < 2;
 true
> SELECT 1.1 < '1';
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-08-01 04:17:52');
 true
> SELECT 1 < NULL;
 NULL
```

#### Kleiner oder gleich

`expr1 <= expr2`: Gibt „true“ zurück, wenn `expr1` kleiner oder gleich `expr2` ist.

Argumente:

- `expr1, expr2`: Die beiden Ausdrücke müssen denselben Typ aufweisen oder in einen gemeinsamen Typ umgewandelt werden, und es muss sich um einen Typ handeln, der sortiert werden kann. So ist etwa der Zuordnungstyp nicht sortierbar, daher wird er nicht unterstützt. Bei komplexen Typen wie Array/Struktur müssen die Datentypen der Felder sortierbar sein.

Beispiele:

```
> SELECT 2 <= 2;
 true
> SELECT 1.0 <= '1';
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-08-01 04:17:52');
 true
> SELECT 1 <= NULL;
 NULL
```

#### Gleich

`expr1 = expr2`: Gibt „true“ zurück, wenn `expr1` gleich `expr2` ist. Andernfalls wird „false“ zurückgegeben.

Argumente:

- `expr1, expr2`: Die beiden Ausdrücke müssen denselben Typ aufweisen oder in einen gemeinsamen Typ umgewandelt werden, und es muss sich um einen Typ handeln, bei dem Gleichheit vorliegen kann. Der Typ Zuordnung wird nicht unterstützt. Bei komplexen Typen wie Array/Struktur müssen die Datentypen der Felder sortierbar sein.

Beispiele:

```
> SELECT 2 = 2;
 true
> SELECT 1 = '1';
 true
> SELECT true = NULL;
 NULL
> SELECT NULL = NULL;
 NULL
```

#### Größer als

`expr1 > expr2`: Gibt „true“ zurück, wenn `expr1` größer ist als `expr2`.

Argumente:

- `expr1, expr2`: Die beiden Ausdrücke müssen denselben Typ aufweisen oder in einen gemeinsamen Typ umgewandelt werden, und es muss sich um einen Typ handeln, der sortiert werden kann. So ist etwa der Zuordnungstyp nicht sortierbar, daher wird er nicht unterstützt. Bei komplexen Typen wie Array/Struktur müssen die Datentypen der Felder sortierbar sein.

Beispiele:

```
> SELECT 2 > 1;
 true
> SELECT 2 > '1.1';
 true
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-08-01 04:17:52');
 false
> SELECT 1 > NULL;
 NULL
```

#### Größer oder gleich

`expr1 >= expr2`: Gibt „true“ zurück, wenn `expr1` größer oder gleich `expr2` ist.

Argumente:

- `expr1, expr2`: Die beiden Ausdrücke müssen denselben Typ aufweisen oder in einen gemeinsamen Typ umgewandelt werden, und es muss sich um einen Typ handeln, der sortiert werden kann. So ist etwa der Zuordnungstyp nicht sortierbar, daher wird er nicht unterstützt. Bei komplexen Typen wie Array/Struktur müssen die Datentypen der Felder sortierbar sein.

Beispiele:

```
> SELECT 2 >= 1;
 true
> SELECT 2.0 >= '2.1';
 false
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-08-01 04:17:52');
 false
> SELECT 1 >= NULL;
 NULL
```

#### Bitweise exklusives Oder

`expr1 ^ expr2`: Gibt das Ergebnis des bitweise exklusiven ODER von `expr1` und `expr2` zurück.

Beispiel:

```
> SELECT 3 ^ 5;
 2
```

#### und

`expr1 and expr2`: Logisches UND.

#### arrays_overlap

`arrays_overlap(a1, a2)`: Gibt „true“ zurück, wenn a1 mindestens ein Element enthält, das nicht null ist und in a2 ebenfalls vorhanden ist. Wenn die Arrays kein gemeinsames Element aufweisen, beide nicht leer sind und beide ein Null-Element enthalten, wird null zurückgegeben. Andernfalls wird „false“ zurückgegeben.

Beispiel:

```
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

Seit: 2.4.0

#### assert_true

`assert_true(expr)`: Löst eine Ausnahme aus, wenn `expr` nicht „true“ ist.

Beispiel:

```
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)`: Wenn `expr1` als „true“ ausgewertet wird, wird `expr2` zurückgegeben. Andernfalls wird `expr3` zurückgegeben.

Beispiel:

```
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### ifnull

`ifnull(expr1, expr2)`: Gibt `expr2` zurück, wenn `expr1` null ist. Andernfalls wird `expr1` zurückgegeben.

Beispiel:

```
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`: Gibt „true“ zurück, wenn `expr` einem beliebigen valN-Wert entspricht.

Argumente:
- `expr1, expr2, expr3, ...`: Die Argumente müssen den gleichen Typ aufweisen.

Beispiele:

```
> SELECT 1 in(1, 2, 3);
 true
> SELECT 1 in(2, 3, 4);
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 1), named_struct('a', 1, 'b', 3));
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 2), named_struct('a', 1, 'b', 3));
 true
```

#### isnan

`isnan(expr)`: Gibt „true“ zurück, wenn `expr` NaN ist. Andernfalls wird „false“ zurückgegeben.

Beispiel:

```
> SELECT isnan(cast('NaN' as double));
 true
```

#### isnotnull

`isnotnull(expr)`: Gibt „true“ zurück, wenn `expr` nicht null ist. Andernfalls wird „false“ zurückgegeben.

Beispiele:

```
> SELECT isnotnull(1);
 true
```

#### isnull

`isnull(expr)`: Gibt „true“ zurück, wenn `expr` null ist. Andernfalls wird „false“ zurückgegeben.

Beispiel:

```
> SELECT isnull(1);
 false
```

#### nanvl

`nanvl(expr1, expr2)`: Gibt `expr1` zurück, wenn es nicht NaN ist. Andernfalls wird `expr2` zurückgegeben.

Beispiel:

```
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr`: Logisches Nicht.

#### oder

`expr1 or expr2`: Logisches Oder.

#### xpath_boolean

`xpath_boolean(xml, xpath)`: Gibt „true“ zurück, wenn der XPath-Ausdruck „true“ ergibt oder ein übereinstimmender Knoten gefunden wird.

Beispiel:

```
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### Funktionen für Datum/Uhrzeit

#### add_month

`add_months(start_date, num_months)`: Gibt das Datum zurück, das `num_months` nach `start_date` liegt.

Beispiel:

```
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

Seit: 1.5.0

#### date_add

`date_add(start_date, num_days)`: Gibt das Datum zurück, das `num_days` nach `start_date` liegt.

Beispiel:

```
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

Seit: 1.5.0

#### date_format

`date_format(timestamp, fmt)`: Konvertiert `timestamp` in einen Zeichenfolgenwert des Formats, das durch das Datumsformat `fmt` angegeben wird.

Beispiel:

```
> SELECT date_format('2016-04-08', 'y');
 2016
```

Seit: 1.5.0

#### date_sub

`date_sub(start_date, num_days)`: Gibt das Datum zurück, das `num_days` vor `start_date` liegt.

Beispiel:

```
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

Seit: 1.5.0

#### date_trunc

`date_trunc(fmt, ts)`: Gibt den Zeitstempel ts zugeschnitten auf die durch das Formatmodell `fmt` angegebene Einheit zurück. `fmt` sollte einer der Werte [„YEAR“, „YYYY“, „YY“, „MON“, „MONTH“, „MM“, „DAY“, „DD“, „HOUR“, „MINUTE“, „SECOND“, „WEEK“, „QUARTER“] sein.

Beispiele:

```
> SELECT date_trunc('YEAR', '2015-03-05T09:32:05.359');
 2015-01-01 00:00:00
> SELECT date_trunc('MM', '2015-03-05T09:32:05.359');
 2015-03-01 00:00:00
> SELECT date_trunc('DD', '2015-03-05T09:32:05.359');
 2015-03-05 00:00:00
> SELECT date_trunc('HOUR', '2015-03-05T09:32:05.359');
 2015-03-05 09:00:00
```

Seit: 2.3.0

#### datediff

`datediff(endDate, startDate)`: Gibt die Anzahl der Tage von `startDate` bis `endDate` zurück.

Beispiele:

```
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

Seit: 1.5.0

#### day

`day(date)`: Gibt den Tag des Monats des Datums/Zeitstempels zurück.

Beispiel:

```
> SELECT day('2009-07-30');
 30
```

Seit: 1.5.0

#### dayofmonth

`dayofmonth(date)`: Gibt den Tag des Monats des Datums/Zeitstempels zurück.

Beispiel:

```
> SELECT dayofmonth('2009-07-30');
 30
```

Seit: 1.5.0

#### dayofweek

`dayofweek(date)`: Gibt den Wochentag für Datum/Zeitstempel zurück (1 = Sonntag, 2 = Montag, ..., 7 = Samstag).

Beispiel:

```
> SELECT dayofweek('2009-07-30');
 5
```

Seit: 2.3.0

#### dayofyear

`dayofyear(date)`: Gibt den Tag des Jahres des Datums/Zeitstempels zurück.

Beispiel:

```
> SELECT dayofyear('2016-04-09');
 100
```

Seit: 1.5.0

#### from_unixtime

`from_unixtime(unix_time, format)`: Gibt `unix_time` im angegebenen `format` zurück.

Beispiel:

```
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

Seit: 1.5.0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`: Interpretiert einen Zeitstempel wie „2017-07-14 02:40:00.0“ als Zeit in UTC und stellt diese Zeit als Zeitstempel in der angegebenen Zeitzone dar. Beispielsweise würde „GMT+1“ „2017-07-14 03:40:00.0“ ergeben.

Beispiel:

```
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

Seit: 1.5.0

#### hour

`hour(timestamp)`: Gibt die Stundenkomponente der Zeichenfolge/des Zeitstempels zurück.

Beispiel:

```
> SELECT hour('2009-07-30 12:58:59');
 12
```

Seit: 1.5.0

#### last_day

`last_day(date):` Gibt den letzten Tag des Monats zurück, zu dem das Datum gehört.

Beispiel:

```
> SELECT last_day('2009-01-12');
 2009-01-31
```

Seit: 1.5.0

#### minute

`minute(timestamp)`: Gibt die Minutenkomponente der Zeichenfolge/des Zeitstempels zurück.

Beispiel:

```
> SELECT minute('2009-07-30 12:58:59');
 58
```

Seit: 1.5.0

#### month

`month(date)`: Gibt die Monatskomponente der Zeichenfolge/des Zeitstempels zurück.

Beispiel:

```
> SELECT month('2016-07-30');
 7
```

Seit: 1.5.0

#### month_between

`months_between(timestamp1, timestamp2[, roundOff])`: Wenn `timestamp1` nach `timestamp2` liegt, ist das Ergebnis positiv. Wenn `timestamp1` und `timestamp2` am gleichen Tag des Monats liegen oder beide der letzte Tag des Monats sind, wird die Tageszeit ignoriert. Andernfalls wird die Differenz auf Grundlage von 31 Tagen pro Monat berechnet und auf 8 Stellen gerundet, es sei denn `roundOff=false`.

Beispiele:

```
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

Seit: 1.5.0

#### next_day

`next_day(start_date, day_of_week)`: Gibt das erste Datum zurück, das nach `start_date` liegt und wie angegebenen benannt ist.

Beispiel:

```
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

Seit: 1.5.0

#### quarter

`quarter(date)`: Gibt das Quartal des Jahres für das Datum im Bereich 1 bis 4 zurück.

Beispiel:

```
> SELECT quarter('2016-08-31');
 3
```

Seit: 1.5.0

#### second

`second(timestamp)`: Gibt die Sekundenkomponente der Zeichenfolge/des Zeitstempels zurück.

Beispiel:

```
> SELECT second('2009-07-30 12:58:59');
 59
```

Seit: 1.5.0

#### to_date

`to_date(date_str[, fmt])`: Analysiert den Ausdruck `date_str` mit dem Ausdruck `fmt` zu einem Datum. Gibt null mit ungültiger Eingabe zurück. Standardmäßig werden die Umwandlungsregeln für Datumswerte verwendet, wenn `fmt` nicht angegeben wird.

Beispiele:

```
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

Seit: 1.5.0

#### to_timestamp

`to_timestamp(timestamp[, fmt])`: Analysiert den Ausdruck `timestamp` mit dem Ausdruck `fmt` zu einem Zeitstempel. Gibt null mit ungültiger Eingabe zurück. Standardmäßig werden die Umwandlungsregeln für Zeitstempel verwendet, wenn `fmt` nicht angegeben wird.

Beispiele:

```
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

Seit: 2.2.0

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])`: Gibt den UNIX-Zeitstempel der angegebenen Zeit zurück.

Beispiel:

```
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Seit: 1.6.0

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)`: Interpretiert einen Zeitstempel wie „2017-07-14 02:40:00.0“ entsprechend der angegebenen Zeit und stellt diese als Zeitstempel in UTC dar. Beispielsweise würde „GMT+1“ „2017-07-14 01:40:00.0“ ergeben.

Beispiel:

```
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

Seit: 1.5.0

#### trunc

`trunc(date, fmt)`: Gibt das Datum mit dem Zeitanteil des Tages gekürzt auf die vom Formatmodell `fmt` angegebene Einheit. `fmt` ist ein Wert von [„year“, „yyyy“, „yy“, „mon“, „month“, „mm“].

Beispiele:

```
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

Seit: 1.5.0

#### unix_timestamp

`unix_timestamp([expr[, pattern]])`: Gibt den UNIX-Zeitstempel der aktuellen oder angegebenen Zeit zurück.

Beispiele:

```
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Seit: 1.5.0

#### weekday

`weekday(date)`: Gibt den Wochentag für Datum/Zeitstempel zurück (0 = Montag, 1 = Dienstag, ..., 6 = Samstag).

Beispiel:

```
> SELECT weekday('2009-07-30');
 3
```

Seit: 2.4.0

#### week_of_year

`weekofyear(date)`: Gibt die Woche des Jahres für ein angegebenes Datums zurück. Der Beginn einer Woche wird ab Montag gerechnet und Woche 1 ist die erste Woche mit >3 Tagen.

Beispiel:

```
> SELECT weekofyear('2008-02-20');
 8
```

Seit: 1.5.0

#### when

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`: Wenn `expr1` = „true“, wird `expr2` zurückgegeben. Wenn dagegen `expr3` = „true“, wird `expr4` zurückgegeben. Andernfalls wird `expr5` zurückgegeben.

Argumente:

- `expr1`, `expr3`: Die Ausdrücke mit verzweigten Bedingungen sollten alle vom Typ Boolean sein.
- `expr2`, `expr4`, `expr5`: Die Werte der Ausdrücke mit verzweigten Bedingungen und der Ausdruck mit dem Else-Wert sollten vom selben Typ sein oder in den gleichen Typ konvertierbar sein.

Beispiele:

```
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### year

`year(date)`: Gibt die Jahreskomponente der Zeichenfolge/des Zeitstempels zurück.

Beispiel:

```
> SELECT year('2016-07-30');
 2016
```

Seit: 1.5.0

### Aggregat-Funktionen

#### approx_count_distinct

`approx_count_distinct(expr[, relativeSD])`: Gibt die geschätzte Kardinalität nach HyperLogLog++ zurück. `relativeSD` definiert den maximal zulässigen Schätzfehler.

### Arrays

#### array

`array(expr, ...)`: Gibt ein Array mit den angegebenen Elementen zurück.

Beispiel:

```
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`: Gibt „true“ zurück, wenn das Array den Wert enthält.

Beispiel:

```
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_different

`array_distinct(array)`: Entfernt doppelte Werte (Duplikate) aus dem Array.

Beispiel:

```
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

Seit: 2.4.0

#### array_exceptions

`array_except(array1, array2)`: Gibt ein Array der Elemente in `array1` zurück, jedoch nicht in `array2`, ohne Duplikate zurück.

Beispiel:

```
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

Seit: 2.4.0

#### array_intersect

`array_intersect(array1, array2)`: Gibt ein Array der Elemente in der Schnittmenge von `array1` und `array2` ohne Duplikate zurück.

Beispiel:

```
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

Seit: 2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])`: Verkettet die Elemente des angegebenen Arrays über das Trennzeichen und eine optionale Zeichenfolge zum Ersetzen von Nullen. Wenn kein Wert für `nullReplacement` festgelegt ist, werden alle Nullwerte gefiltert.

Beispiele:

```
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

Seit: 2.4.0

#### array_max

`array_max(array)`: Gibt den Maximalwert der im Array enthaltenen Werte zurück. Null-Elemente werden übersprungen.

Beispiel:

```
> SELECT array_max(array(1, 20, null, 3));
 20
```

Seit: 2.4.0

#### array_min

`array_min(array)`: Gibt den Minimalwert der im Array enthaltenen Werte zurück. Null-Elemente werden übersprungen.

Beispiel:

```
> SELECT array_min(array(1, 20, null, 3));
 1
```

Seit: 2.4.0

#### array_position

`array_position(array, element)`: Gibt den (1-basierten) Index des ersten Elements des Arrays als Long zurück.

Beispiel:

```
> SELECT array_position(array(3, 2, 1), 1);
 3
```

Seit: 2.4.0

#### array_remove

`array_remove(array, element)`: Entfernt alle Elemente, die gleich dem Element im Array sind.

Beispiel:

```
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

Seit: 2.4.0

#### array_repeat

`array_repeat(element, count)`: Gibt das Array zurück, das die Anzahl der Elemente enthält.

Beispiel:

```
> SELECT array_repeat('123', 2);
 ["123","123"]
```

Seit: 2.4.0

#### array_sort

`array_sort(array)`: Sortiert das Eingabe-Array in aufsteigender Reihenfolge. Die Elemente des Eingabe-Arrays müssen sortierbar sein. Null-Elemente werden am Ende des zurückgegebenen Arrays platziert.

Beispiel:

```
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

Seit: 2.4.0

#### array_union

`array_union(array1, array2)`: Gibt ein Array der Elemente in der Vereinigung von `array1` und `array2` ohne Duplikate zurück.

Beispiel:

```
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

Seit: 2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)`: Gibt ein zusammengeführtes Array von Strukturen zurück, in denen die n-te Struktur alle n-ten Werte von Eingabe-Arrays enthält.

Beispiele:

```
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

Seit: 2.4.0

#### element_at

`element_at(array, index)`: Gibt das Element des Arrays mit dem angegebenen (1-basierten) Index zurück. Wenn `index < 0`, wird auf die Elemente in der Reihenfolge vom letzten zum ersten zugegriffen. Gibt NULL zurück, wenn der Index die Länge des Arrays überschreitet.

`element_at(map, key)`: Gibt den Wert für den angegebenen Schlüssel oder NULL zurück, wenn der Schlüssel nicht in der Zuordnung enthalten ist.

Beispiele:

```
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

Seit: 2.4.0

#### explode

`explode(expr)`: Trennt die Elemente des Arrays `expr` in mehrere Zeilen oder die Elemente der Zuordnung `expr` in mehrere Zeilen und Spalten.

Beispiele:

```
> SELECT explode(array(10, 20));
 10
 20
```

#### explode_outer

`explode_outer(expr)`: Trennt die Elemente des Arrays `expr` in mehrere Zeilen oder die Elemente der Zuordnung `expr` in mehrere Zeilen und Spalten.

Beispiel:

```
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)`: Gibt den Index (1-basiert) der angegebenen Zeichenfolge (`str`) in einer kommagetrennten Liste (`str_array`) zurück. Gibt 0 zurück, wenn die Zeichenfolge nicht gefunden wurde oder wenn die angegebene Zeichenfolge (`str`) ein Komma enthält.

Beispiel:

```
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### flatten

`flatten(arrayOfArrays)`: Wandelt ein Array aus Arrays in ein einzelnes Array um.

Beispiel:

```
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

Seit: 2.4.0

#### inline

`inline(expr)`: Trennt ein aus Strukturen bestehendes Array in eine Tabelle.

Beispiel:

```
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inline_outer

`inline_outer(expr)`: Trennt ein aus Strukturen bestehendes Array in eine Tabelle.

Beispiel:

```
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### posexplode

`posexplode(expr)`: Trennt die Elemente des Arrays `expr` in mehrere Zeilen mit Positionen oder die Elemente der Zuordnung `expr` in mehrere Zeilen und Spalten mit Positionen.

Beispiel:

```
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posexplode_outer

`posexplode_outer(expr)`: Trennt die Elemente des Arrays `expr` in mehrere Zeilen mit Positionen oder die Elemente der Zuordnung `expr` in mehrere Zeilen und Spalten mit Positionen.

Beispiel:

```
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### reverse

`reverse(array)`: Gibt eine umgekehrte Zeichenfolge oder ein Array mit umgekehrter Reihenfolge der Elemente zurück.

Beispiele:

```
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

Seit: 1.5.0
>[!NOTE]
>
>Die Umkehrlogik ist für Arrays seit 2.4.0 verfügbar.

#### shuffle

`shuffle(array)`: Gibt eine zufällige Permutation des angegebenen Arrays zurück.

Beispiele:

```
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

Seit: 2.4.0
>[!NOTE]
>
>Funktion ist nicht deterministisch.

#### slice

`slice(x, start, length)`: Teilt ein Array x ab dem Index-Beginn (oder ausgehend vom Ende, wenn der Beginn negativ ist) in Teilmengen mit der angegebenen Länge.

Beispiele:

```
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

Seit: 2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])`: Sortiert das Eingabe-Array in auf- oder absteigender Reihenfolge entsprechend der natürlichen Reihenfolge der Array-Elemente. Null-Elemente werden am Anfang des zurückgegebenen Arrays in aufsteigender Reihenfolge oder am Ende des zurückgegebenen Arrays in absteigender Reihenfolge platziert.

Beispiele:

```
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`: Führt zwei angegebene Arrays elementweise anhand der Funktion in einem Array zusammen. Ist eines der beiden Arrays kürzer, werden ihm entsprechend der Länge des längeren Arrays am Ende Nullen angehängt, bevor die Funktion angewendet wird.

Beispiele:

```
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

Seit: 2.4.0

### Funktionen zur Umwandlung von Datentypen

#### bigint

`bigint(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `bigint` um.

#### binary

`binary(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `binary` um.

#### boolean

`boolean(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `boolean` um.

#### cast

`cast(expr AS type)`: Wandelt den Wert `expr` in den Zieldatentyp `type` um.

Beispiel:

```
> SELECT cast('10' as int);
 10
```

#### date

`date(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `date` um.

#### decimal

`decimal(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `decimal` um.

#### Doppelt

`double(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `double` um.

#### float

`float(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `float` um.

#### int

`int(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `int` um.

#### map

`map(key0, value0, key1, value1, ...)`: Erstellt eine Zuordnung mit den angegebenen Schlüssel-Wert-Paaren.

Beispiel:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### smallint

`smallint(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `smallint` um.

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`: Erstellt eine Zuordnung aus mithilfe von Trennzeichen in Schlüssel-Wert-Paare zerteiltem Text. Die Standard-Trennzeichen sind Komma (,) für `pairDelim` und Doppelpunkt (:) für `keyValueDelim`.

Beispiele:

```
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### Zeichenfolge

`string(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `string` um.

#### struct

`struct(col1, col2, col3, ...)`: Erstellt eine Struktur mit den angegebenen Feldwerten.

#### tinyint

`tinyint(expr)`: Wandelt den Wert `expr` in den Zieldatentyp `tinyint` um.

### Konvertierungs- und Formatierungsfunktionen

#### ascii

`ascii(str)`: Gibt den numerischen Wert des ersten Zeichens von `str` zurück.

Beispiele:

```
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`: Konvertiert das Argument von einer binären `bin`- in eine Base64-Zeichenfolge.

Beispiel:

```
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### bin

`bin(expr)`: Gibt die Zeichenfolgendarstellung des Long-Werts `expr` als Binärcode zurück.

Beispiele:

```
> SELECT bin(13);
 1101
> SELECT bin(-13);
 1111111111111111111111111111111111111111111111111111111111110011
> SELECT bin(13.3);
 1101
```

#### bit_length

`bit_length(expr)`: Gibt die Bit-Länge von Zeichenfolgendaten oder die Anzahl der Bits von Binärdaten zurück.

Beispiel:

```
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`: Gibt das dem Binärcode von `expr` entsprechende ASCII-Zeichen zurück. Wenn n größer ist als 256, entspricht das Ergebnis `chr(n % 256)`.

Beispiel:

```
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`: Gibt die Zeichenlänge von Zeichenfolgendaten oder die Anzahl der Byte von Binärdaten zurück. Bei der Länge der Zeichenfolgendaten werden auf sie folgende Leerzeichen mitgezählt. Bei der Länge binärer Daten werden binäre Nullen mitgezählt.

Beispiele:

```
> SELECT char_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### character_length

`character_length(expr)`: Gibt die Zeichenlänge von Zeichenfolgendaten oder die Anzahl der Byte von Binärdaten zurück. Bei der Länge der Zeichenfolgendaten werden auf sie folgende Leerzeichen mitgezählt. Bei der Länge binärer Daten werden binäre Nullen mitgezählt.

Beispiele:

```
> SELECT character_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### chr

`chr(expr)`: Gibt das dem Binärcode des Ausdrucks entsprechende ASCII-Zeichen zurück. Wenn n größer ist als 256, entspricht das Ergebnis `chr(n % 256)`.

Beispiel:

```
> SELECT chr(65);
 A
```

#### degrees

`degrees(expr)`: Wandelt das Bogenmaß Radiant in Grad um.

Argumente:
- `expr`: Winkel im Bogenmaß Radiant

Beispiel:

```
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`: Formatiert den Zahlenwert von `expr1`, z. B. „#.###.###,##“, auf `expr2` Dezimalstellen gerundet. Wenn der Wert von `expr2` 0 beträgt, weist das Ergebnis keinen Dezimalpunkt oder Bruchteil auf. Für `expr2` wird auch ein benutzerspezifisches Format akzeptiert. Die Funktionsweise ist `FORMAT` von MySQL nachempfunden.

Beispiele:

```
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`: Gibt einen Strukturwert auf Basis der Angaben für `jsonStr` und `schema` zurück.

Beispiele:

```
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

Seit: 2.2.0

#### hash

`hash(expr1, expr2, ...)`: Gibt einen Hashwert der Argumente zurück.

Beispiel:

```
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### hex

`hex(expr)`: Konvertiert `expr` in Hexadezimalcode.

Beispiele:

```
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`: Gibt `str` mit dem ersten Buchstaben jedes Wortes in Großbuchstaben zurück. Alle anderen Buchstaben werden in Kleinbuchstaben zurückgegeben. Die Wörter werden durch Leerzeichen getrennt.

Beispiel:

```
> SELECT initcap('sPark sql');
 Spark Sql
```

#### lcase

`lcase(str)`: Gibt `str` mit allen Zeichen in Kleinbuchstaben zurück.

Beispiel:

```
> SELECT lcase('SparkSql');
 sparksql
```

#### lower

`lower(str)`: Gibt `str` mit allen Zeichen in Kleinbuchstaben zurück.

Beispiel:

```
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`: Gibt `str` mit `pad` linksseitig auf eine Länge von `len` aufgefüllt zurück. Wenn `str` länger ist als `len`, wird der Rückgabewert auf `len` Zeichen gekürzt.

Beispiele:

```
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### map

`map(key0, value0, key1, value1, ...)`: Erstellt eine Zuordnung mit den angegebenen Schlüssel-Wert-Paaren.

Beispiel:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_arrays

`map_from_arrays(keys, values)`: Erstellt eine Zuordnung mit einem Paar der angegebenen Schlüssel-Wert-Arrays. Elemente in Schlüsseln dürfen nicht null sein.

Beispiel:

```
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

Seit: 2.4.0

#### map_from_tries

`map_from_entries(arrayOfEntries)`: Gibt eine aus dem angegebenen Array von Einträgen erstellte Zuordnung zurück.

Beispiel:

```
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

Seit: 2.4.0

#### md5

`md5(expr)`: Gibt eine MD5-128-Bit-Prüfsumme als hexadezimale Zeichenfolge von `expr` zurück.

Beispiel:

```
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)`: Gibt `str` mit `pad` rechtsseitig auf eine Länge von `len` aufgefüllt zurück. Wenn `str` länger ist als `len`, wird der Rückgabewert auf `len` Zeichen gekürzt.

Beispiele:

```
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rtrim

`rtrim(str)`: Entfernt die auf `str` folgenden Leerzeichen.

`rtrim(trimStr, str)`: Entfernt die nachfolgende Zeichenfolge, die die Zeichen der gekürzten Zeichenfolge aus `str` enthält.

Argumente:
- `str`: Ein Zeichenfolgen-Ausdruck.
- `trimStr`: Die zu kürzende Zeichenfolge. Der Standardwert ist ein einzelnes Leerzeichen.

Beispiele:

```
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)`: Gibt einen `sha1`-Hashwert als hexadezimale Zeichenfolge von `expr` zurück.

Beispiel:

```
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`: Gibt einen `sha1`-Hashwert als hexadezimale Zeichenfolge von `expr` zurück.

Beispiel:

```
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`: Gibt eine Prüfsumme der SHA-2-Familie als hexadezimale Zeichenfolge von `expr` zurück. Unterstützt werden SHA-224, SHA-256, SHA-384 und SHA-512. Eine Bit-Länge von 0 entspricht 256.

Beispiel:

```
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)`: Gibt die Zeichenfolge als Soundex-Code zurück.

Beispiel:

```
> SELECT soundex('Miller');
 M460
```

#### stack

`stack(n, expr1, ..., exprk)`: Trennt `expr1`, ..., `exprk` in `n` Zeilen.

Beispiel:

```
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`: Gibt die Teilzeichenfolge von `str` zurück, die bei `pos` beginnt und der Länge `len` ist, oder den Slice des Byte-Arrays, der bei `pos` beginnt und der Länge `len` ist.

Beispiele:

```
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### substring

`substring(str, pos[, len])`: Gibt die Teilzeichenfolge von `str` zurück, die bei `pos` beginnt und der Länge `len` ist, oder den Slice des Byte-Arrays, der bei `pos` beginnt und der Länge `len` ist.

Beispiele:

```
> SELECT substring('Spark SQL', 5);
 k SQL
> SELECT substring('Spark SQL', -3);
 SQL
> SELECT substring('Spark SQL', 5, 1);
 k
```

#### to_json

`to_json(expr[, options])`: Gibt eine JSON-Zeichenfolge mit einem angegebenen Strukturwert zurück.

Beispiele:

```
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2)));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

Seit: 2.2.0

#### translate

`translate(input, from, to)`: Übersetzt die `input`-Zeichenfolge, indem die in der `from`-Zeichenfolge vorhandenen Zeichen durch die entsprechenden Zeichen in der `to`-Zeichenfolge ersetzt werden.

Beispiel:

```
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trim

`trim(str)`: Entfernt die `str` vorangehenden und nachfolgenden Leerzeichen.

`trim(BOTH trimStr FROM str)`: Entfernt die `trimStr`-Zeichen, die `str` vorangehen und darauf folgen.

`trim(LEADING trimStr FROM str)`: Entfernt `trimStr`-Zeichen, die `str` vorangehen.

`trim(TRAILING trimStr FROM str)`: Entfernt die `trimStr`-Zeichen, die auf `str` folgen.

Argumente:
- `str`: Ein Zeichenfolgen-Ausdruck.
- `trimStr`: Die aus der Zeichenfolge auszuschneidenden Zeichen. Der Standardwert ist ein einzelnes Leerzeichen.
- `BOTH`, `FROM`: Anhand dieser Schlüsselwörter (bzw. Keywords) werden die angegebenen Zeichen an beiden Enden der Zeichenfolge abgeschnitten.
- `LEADING`, `FROM`: Anhand dieser Schlüsselwörter (bzw. Keywords) werden die angegebenen Zeichen am linken Ende der Zeichenfolge abgeschnitten.
- `TRAILING`, `FROM`: Anhand dieser Schlüsselwörter (bzw. Keywords) werden die angegebenen Zeichen am rechten Ende der Zeichenfolge abgeschnitten.

Beispiele:

```
> SELECT trim('    SparkSQL   ');
 SparkSQL
> SELECT trim('SL', 'SSparkSQLS');
 parkSQ
> SELECT trim(BOTH 'SL' FROM 'SSparkSQLS');
 parkSQ
> SELECT trim(LEADING 'SL' FROM 'SSparkSQLS');
 parkSQLS
> SELECT trim(TRAILING 'SL' FROM 'SSparkSQLS');
 SSparkSQ
```

#### ucase

`ucase(str)`: Gibt `str` mit allen Zeichen in Großbuchstaben zurück.

Beispiel:

```
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`: Konvertiert das Argument von einer Base64-codierten Zeichenfolge `str` in Binärcode.

Beispiel:

```
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### unhex

`unhex(expr)`: Konvertiert einen hexadezimal codierten `expr` in Binärcode.

Beispiel:

```
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### upper

`upper(str)`: Gibt `str` mit allen Zeichen in Großbuchstaben zurück.

Beispiel:

```
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()`: Gibt eine UUID-Zeichenfolge (Universally Unique Identifier) zurück. Der Wert wird als kanonische UUID-Zeichenfolge mit einer Länge von 36 Zeichen zurückgegeben.

Beispiel:

```
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE]
>
>Funktion ist nicht deterministisch.

### Datenevaluierung

#### coalesce

`coalesce(expr1, expr2, ...)`: Gibt das erste Argument zurück, das nicht null ist (sofern vorhanden). Andernfalls null.

Beispiel:

```
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collect_list

`collect_list(expr)`: Erfasst eine Liste nicht eindeutiger Elemente und gibt diese zurück.

#### collect_set

`collect_set(expr)`: Erfasst einen Satz eindeutiger Elemente und gibt diesen zurück.

#### concat

`concat(col1, col2, ..., colN)`: Gibt die Verkettung von col1, col2, ..., colN zurück.

Beispiele:

```
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE]
>
>`concat` Die -Logik ist für Arrays seit 2.4.0 verfügbar.

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`: Gibt die Verkettung von durch `sep` getrennten Zeichenfolgen zurück.

Beispiel:

```
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### count

`count(*)`: Gibt die Gesamtanzahl der abgerufenen Zeilen einschließlich der Zeilen, die null enthalten, zurück.

`count(expr[, expr...])`: Gibt die Anzahl der Zeilen zurück, für die die bereitgestellten Ausdrücke alle nicht null sind.

`count(DISTINCT expr[, expr...])`: Gibt die Anzahl der Zeilen zurück, für die die bereitgestellten Ausdrücke eindeutig und nicht null sind.

#### crc32

`crc32(expr)`: Gibt den Wert einer zyklischen Redundanzprüfung von `expr` als bigint zurück.

Beispiel:

```
> SELECT crc32('Spark');
 1557323817
```

#### decode

`decode(bin, charset)`: Decodiert das erste Argument unter Verwendung des Zeichensatzes des zweiten Arguments.

Beispiel:

```
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### elt

`elt(n, input1, input2, ...)`: Gibt die `n`-te Eingabe zurück, z. B. `input2`, wenn `n` 2 ist.

Beispiel:

```
> SELECT elt(1, 'scala', 'java');
 scala
```

#### encode

`encode(str, charset)`: Codiert das erste Argument unter Verwendung des Zeichensatzes des zweiten Arguments.

Beispiel:

```
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])`: Gibt den ersten Wert von `expr` für eine Gruppe von Zeilen zurück. Wenn `isIgnoreNull` wahr ist, werden nur Werte zurückgegeben, die nicht null sind.

#### first_value

`first_value(expr[, isIgnoreNull])`: Gibt den ersten Wert von `expr` für eine Gruppe von Zeilen zurück. Wenn `isIgnoreNull` wahr ist, werden nur Werte zurückgegeben, die nicht null sind.

#### get_json_object

`get_json_object(json_txt, path)`: Extrahiert ein JSON-Objekt aus `path`.

Beispiel:

```
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### grouping

<!-- was blank --->

#### grouping_id

<!-- was blank --->

#### instr

`instr(str, substr)`: Gibt den (1-basierten) Index der ersten Instanz von `substr` in `str` zurück.

Beispiel:

```
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`: Gibt dasselbe Tupel zurück wie die Funktion `get_json_object`, nimmt jedoch mehrere Namen an. Alle Eingabeparameter und Ausgabespalten-Typen sind Zeichenfolgen.

Beispiel:

```
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### lag

`lag(input[, offset[, default]])`: Gibt den Wert von `input` an der Zeile, die `offset` vor der aktuellen Zeile im Fenster liegt, zurück. Der Standardwert von `offset` ist 1, der Standardwert von `default` ist null. Wenn der Wert von `input` an der Zeile an `offset` null ist, wird null zurückgegeben. Wenn keine solche Offset-Zeile vorhanden ist (z. B. wenn der Offset 1 lautet, weist die erste Zeile des Fensters keine vorherige Zeile auf), wird `default` zurückgegeben.

#### last

`last(expr[, isIgnoreNull])`: Gibt den letzten Wert von `expr` für eine Gruppe von Zeilen zurück. Wenn `isIgnoreNull` wahr ist, werden nur Werte zurückgegeben, die nicht null sind.

#### last_value

`last_value(expr[, isIgnoreNull])`: Gibt den letzten Wert von `expr` für eine Gruppe von Zeilen zurück. Wenn `isIgnoreNull` „true“ ist, werden nur Werte zurückgegeben, die nicht null sind.

#### lead

`lead(input[, offset[, default]])`: Gibt den Wert von `input` an der Zeile, die `offset` nach der aktuellen Zeile im Fenster liegt, zurück. Der Standardwert von `offset` ist 1, der Standardwert von `default` ist null. Wenn der Wert von `input` an der Zeile an `offset` null ist, wird null zurückgegeben. Wenn keine solche Offset-Zeile vorhanden ist (z. B. wenn der Offset 1 lautet, weist die letzte Zeile des Fensters keine auf sie folgende Zeile auf), wird `default` zurückgegeben.


#### left

`left(str, len)`: Gibt die am weitesten links liegenden `len`-Zeichen (`len` kann vom Typ Zeichenfolge sein) aus der Zeichenfolge `str` zurück. Wenn `len` kleiner als oder gleich 0 ist, ist das Ergebnis eine leere Zeichenfolge.

Beispiel:

> SELECT left(&#39;Spark SQL&#39;, 3);
Spa


#### length

`length(expr)`: Gibt die Zeichenlänge von Zeichenfolgendaten oder die Anzahl der Byte von Binärdaten zurück. Bei der Länge der Zeichenfolgendaten werden auf sie folgende Leerzeichen mitgezählt. Bei der Länge binärer Daten werden binäre Nullen mitgezählt.

Beispiele:

```
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### locate

`locate(substr, str[, pos])`: Gibt die Position der ersten Instanz von `substr` in `str` nach Position `pos` zurück. Der angegebene Wert für `pos` und der Rückgabewert sind 1-basiert.

Beispiele:

```
> SELECT locate('bar', 'foobarbar');
 4
> SELECT locate('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### map_concat

`map_concat(map, ...)`: Gibt die Vereinigung aller angegebenen Zuordnungen zurück.

Beispiel:

```
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

Seit: 2.4.0

#### map_keys

`map_keys(map)`: Gibt ein unsortiertes Array zurück, das die Schlüssel der Zuordnung enthält.

Beispiel:

```
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`: Gibt ein unsortiertes Array zurück, das die Werte der Zuordnung enthält.

Beispiel:

```
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### ntile

`ntile(n)`: Teilt die Zeilen für jede Fensterpartition in `n` Buckets von 1 bis maximal `n`.

#### nullif

`nullif(expr1, expr2)`: Gibt null zurück, wenn `expr1` gleich `expr2` ist. Andernfalls wird `expr1` zurückgegeben.

Beispiel:

```
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`: Gibt `expr2` zurück, wenn `expr1` null ist. Andernfalls wird `expr1` zurückgegeben.

Beispiel:

```
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`: Gibt `expr2` zurück, wenn `expr1` nicht null ist. Andernfalls wird `expr3` zurückgegeben.

Beispiel:

```
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])`: Extrahiert einen Teil aus einer URL.

Beispiele:

```
> SELECT parse_url('http://spark.apache.org/path?query=1', 'HOST')
 spark.apache.org
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY')
 query=1
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY', 'query')
 1
```

#### position

`position(substr, str[, pos])`: Gibt die Position der ersten Instanz von `substr` in `str` nach Position `pos` zurück. Der angegebene Wert für `pos` und der Rückgabewert sind 1-basiert.

Beispiele:

```
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### rank

`rank()`: Berechnet den Rang eines Werts in einer Gruppe von Werten. Das Ergebnis ist 1 plus der Anzahl der Zeilen, die vor der aktuellen Zeile in der Partitionsreihenfolge liegen oder die gleich dieser Zeile sind. Die Werte erzeugen Lücken in der Sequenz.

#### regexp_extract

`regexp_extract(str, regexp[, idx])`: Extrahiert eine mit `regexp` übereinstimmende Gruppe.

Beispiel:

```
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`: Ersetzt alle Teilzeichenfolgen von `str`, die `regexp` mit `rep` entsprechen.

Beispiel:

```
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### repeat

`repeat(str, n)`: Gibt eine Zeichenfolge zurück, die den angegebenen Zeichenfolgenwert n-Mal wiederholt.

Beispiel:

```
> SELECT repeat('123', 2);
 123123
```

#### replace

`replace(str, search[, replace])`: Ersetzt alle Instanzen von `search` durch `replace`.

Argumente:
- `str`: Ein Zeichenfolgen-Ausdruck.
- `search`: Ein Zeichenfolgen-Ausdruck. Wenn `search` nicht in `str` gefunden wird, wird `str` unverändert zurückgegeben.
- `replace`: Ein Zeichenfolgen-Ausdruck. Wenn `replace` nicht angegeben oder eine leere Zeichenfolge ist, wird die aus `str` entfernte Zeichenfolge durch nichts ersetzt.

Beispiel:

```
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### Datenaggregation

<!-- was blank -->

#### row_number

`row_number()`: Weist jeder Zeile eine eindeutige, sequenzielle Zahl zu, beginnend bei 1 und entsprechend der Reihenfolge der Zeilen in der Fensterpartition.

#### schema_of_json

`schema_of_json(json[, options])`: Gibt das Schema im DDL-Format der JSON-Zeichenfolge zurück.

Beispiel:

```
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

Seit: 2.4.0

#### sentences

`sentences(str[, lang, country])`: Teilt `str` in ein Array eines Arrays von Wörtern.

Beispiel:

```
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### sequence

`sequence(start, stop, step)`: Generiert ein Array von Elementen vom Beginn bis zum Stopp (mit einbezogen), wobei schrittweise inkrementiert wird. Der Typ der zurückgegebenen Elemente ist identisch mit dem Typ der Argument-Ausdrücke.

Folgende Typen werden unterstützt: byte, short, integer, long, date, timestamp.

Die `start`- und `stop`-Ausdrücke müssen in demselben Typ aufgelöst werden. Wenn die `start`- und `stop`-Ausdrücke in den Typ „date“ oder „timestamp“ aufgelöst werden, muss der `step`-Ausdruck in den Typ „interval“ aufgelöst werden. Andernfalls wird er im gleichen Typ wie die `start`- und `stop`-Ausdrücke aufgelöst.

Argumente:
- `start`: Ein Ausdruck. Der Beginn der Spanne.
- `stop`: Ein Ausdruck. Das Ende der Spanne (mit einbezogen).
- `step`: Ein optionaler Ausdruck. Die Schrittweite der Spanne. Standardmäßig ist `step` 1, wenn `start` kleiner oder gleich `stop` ist, andernfalls -1. Für temporale Sequenzen ist der Wert 1 Tag bzw. -1 Tag. Wenn `start` größer ist als `stop`, muss `step` negativ sein. Umgekehrt gilt das gleiche.

Beispiele:

```
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval 1 month);
 [2018-01-01,2018-02-01,2018-03-01]
```

Seit: 2.4.0

#### shiftleft

`shiftleft(base, expr)`: Bitweise Verschiebung nach links.

Beispiel:

```
> SELECT shiftleft(2, 1);
 4
```

#### shiftright

`shiftright(base, expr)`: Bitweise (signierte) Verschiebung nach rechts.

Beispiel:

```
> SELECT shiftright(4, 1);
 2
```

#### shiftrightunsigned

`shiftrightunsigned(base, expr)`: Bitweise (nicht signierte) Verschiebung nach rechts.

Beispiel:

```
> SELECT shiftrightunsigned(4, 1);
 2
```

#### size

`size(expr)`: Gibt die Größe eines Arrays oder einer Zuordnung zurück. Die Funktion gibt -1 zurück, wenn ihre Eingabe null ist und `spark.sql.legacy.sizeOfNull` auf „true“ festgelegt ist. Wenn `spark.sql.legacy.sizeOfNull` auf „false“ festgelegt ist, gibt die Funktion für eine Null-Eingabe null zurück. Standardmäßig ist der Parameter `spark.sql.legacy.sizeOfNull` auf „true“ festgelegt.

Beispiele:

```
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### space

`space(n)`: Gibt eine Zeichenfolge bestehend aus `n` Leerzeichen zurück.

Beispiel:

```
> SELECT concat(space(2), '1');
   1
```

#### split

`split(str, regex)`: Teilt `str` um mit `regex` übereinstimmende Instanzen.

Beispiel:

```
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)`: Gibt die Teilzeichenfolge von `str` vor `count` Instanzen des Trennzeichens `delim` zurück. Wenn `count` positiv ist, wird alles, das (von links aus gezählt) links vom letzten Trennzeichen liegt, zurückgegeben. Wenn `count` negativ ist, wird alles, das (von rechts aus gezählt) rechts vom letzten Trennzeichen liegt, zurückgegeben. Die Funktion `substring_index` führt einen Abgleich von Groß-/Kleinschreibung aus, wenn nach `delim` gesucht wird.

Beispiel:

```
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### Fenster

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`: Gibt ein Zeichenfolgen-Array mit Werten innerhalb der Knoten von xml zurück, die mit dem XPath-Ausdruck übereinstimmen.

Beispiel:

```
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_double

`xpath_double(xml, xpath)`: Gibt einen Dublettenwert zurück oder den Wert 0, wenn keine Übereinstimmung gefunden wird, oder den Wert NaN, wenn eine Übereinstimmung gefunden wird, der Wert jedoch nicht numerisch ist.

Beispiel:

```
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`: Gibt einen Gleitkommawert zurück oder den Wert 0, wenn keine Übereinstimmung gefunden wird, oder den Wert NaN, wenn eine Übereinstimmung gefunden wird, der Wert jedoch nicht numerisch ist.

Beispiel:

```
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`: Gibt einen Integer-Wert (Ganzzahl) zurück oder den Wert 0, wenn keine Übereinstimmung oder eine Übereinstimmung, bei der der Wert nicht numerisch ist, gefunden wird.

Beispiel:

```
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`: Gibt einen Long Integer-Wert (lange Ganzzahl) zurück oder den Wert 0, wenn keine Übereinstimmung oder eine Übereinstimmung, bei der der Wert nicht numerisch ist, gefunden wird.

Beispiel:

```
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`: Gibt einen Dublettenwert zurück oder den Wert 0, wenn keine Übereinstimmung gefunden wird, oder den Wert NaN, wenn eine Übereinstimmung gefunden wird, der Wert jedoch nicht numerisch ist.

Beispiel:

```
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`: Gibt einen Short Integer-Wert (kurze Ganzzahl) zurück oder den Wert 0, wenn keine Übereinstimmung oder eine Übereinstimmung, bei der der Wert nicht numerisch ist, gefunden wird.

Beispiel:

```
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`: Gibt den Textinhalt des ersten XML-Knotens zurück, der mit dem XPath-Ausdruck übereinstimmt.

Beispiel:

```
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### Aktuelle Informationen

#### current_database

`current_database()`: Gibt die aktuelle Datenbank zurück.

Beispiel:

```
> SELECT current_database();
 default
```

#### current_date

`current_date()`: Gibt das aktuelle Datum am Beginn der Abfrage-Evaluierung zurück.

Seit: 1.5.0

#### current_timestamp

`current_timestamp()`: Gibt den aktuellen Zeitstempel am Beginn der Abfrage-Evaluierung zurück.

Seit: 1.5.0

#### now

`now()`: Gibt den aktuellen Zeitstempel am Beginn der Abfrage-Evaluierung zurück.

Seit: 1.5.0
