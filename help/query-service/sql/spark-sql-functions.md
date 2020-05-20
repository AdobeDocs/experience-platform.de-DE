---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Spark-SQL-Funktionen
topic: spark sql functions
translation-type: tm+mt
source-git-commit: a23ee02a9e801531a38b5ff70ef07497aa21b174
workflow-type: tm+mt
source-wordcount: '4903'
ht-degree: 6%

---


# Spark-SQL-Funktionen

Die SQL-Helfer von Spark bieten integrierte Spark-SQL-Funktionen, um die SQL-Funktionalität zu erweitern.

Referenz: [Dokumentation zu Spark-SQL-Funktionen](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE] Nicht alle Funktionen in der externen Dokumentation werden unterstützt.

## Kategorien

- [mathematische und statistische Operatoren und Funktionen](#math-and-statistical-operators-and-functions)
- [Logische Operatoren](#logical-operators)
- [Datums-/Uhrzeitfunktionen](#date/time-functions)
- [Aggregat-Funktionen](#aggregate-functions)
- [Arrays ](#arrays)
- [Datentyp-Castingfunktionen](#datatype-casting-functions)
- [Konvertierungs- und Formatierungsfunktionen](#conversion-and-formatting-functions)
- [Datenauswertung](#data-evaluation)
- [Aktuelle Informationen](#current-information)

### mathematische und statistische Operatoren und Funktionen

#### Modulo

`expr1 % expr2`: Gibt den Rest nach `expr1`/`expr2`zurück.

Beispiele:

```
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### Multiplizieren

`expr1 * expr2`: Rückgabe `expr1`*`expr2`.

Beispiel:

```
> SELECT 2 * 3;
 6
```

#### Neue

`expr1 + expr2`: Rückgabe `expr1`+`expr2`.

Beispiel:

```
> SELECT 1 + 2;
 3
```

#### Subtrahieren

`expr1 - expr2`: Rückgabe `expr1`-`expr2`.

Beispiel:

```
> SELECT 2 - 1;
 1
```

#### Teilung

`expr1 / expr2`: Rückgabe `expr1`/`expr2`. Er führt immer eine Gleitkommabteilung durch.

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

`acos(expr)`: Gibt den umgekehrten Kosinus (auch Bogen-Kosinus genannt) von zurück, `expr`als ob er von berechnet `java.lang.Math.acos`würde.

Beispiele:

```
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### ca_Perzentil

`approx_percentile(col, percentage [, accuracy])`: Gibt den ungefähren Perzentilwert der numerischen Spalte `col` zum angegebenen Prozentwert zurück. Der Wert des Prozentsatzes muss zwischen 0,0 und 1,0 liegen. Der `accuracy` Parameter (Standard: 10000) ist ein positives numerisches Literal, das die Genauigkeit der Annäherung auf Kosten des Speichers steuert. Höhere Werte für `accuracy` Erträge bessere Genauigkeit, `1.0/accuracy` ist der relative Fehler der Annäherung. Wenn `percentage` es sich um ein Array handelt, muss jeder Wert des Prozentarray zwischen 0,0 und 1,0 liegen. In diesem Fall wird das ungefähre Perzentil-Array der Spalte `col` am angegebenen Prozentarray zurückgegeben.

Beispiele:

```
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asin

`asin(expr)`: Gibt den Inverse-Sinus (auch als Bogen-Sinus bezeichnet) zurück, den Bogen-Sinus von `expr`, als ob berechnet von `java.lang.Math.asin`.

Beispiele:

```
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)`: Gibt die umgekehrte Tangente (auch als Bogen-Tangens bezeichnet) von zurück, `expr`als ob berechnet durch `java.lang.Math.atan`

Beispiel:

```
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`: Gibt den Winkel in Radianten zwischen der positiven X-Achse einer Ebene und dem Punkt, der durch die Koordinaten (`exprX`, `exprY`) angegeben wird, als ob er durch `java.lang.Math.atan2`berechnet wird, zurück.

Argumente:

`exprY`: Koordinieren auf der y-Achse`exprX`: Koordinieren auf der X-Achse

Beispiel:

```
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`: Gibt den aus den Werten einer Gruppe berechneten Mittelwert zurück.

#### Kardinalität

`cardinality(expr)`: Gibt die Größe eines Arrays oder einer Map zurück. Die Funktion gibt -1 zurück, wenn ihre Eingabe null ist und auf true (Standard) eingestellt `spark.sql.legacy.sizeOfNull` ist. Wenn `spark.sql.legacy.sizeOfNull` der Wert auf false festgelegt ist, gibt die Funktion null für die Null-Eingabe zurück.

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

`cbrt(expr)`: Gibt den Stammordner der Cube zurück `expr`.

Beispiel:

```
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`: Gibt die kleinste Ganzzahl zurück, die nicht kleiner als `expr`.

Beispiele:

```
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### Obergrenze

`ceiling(expr)`: Gibt die kleinste Ganzzahl zurück, die nicht kleiner als `expr`.

Beispiele:

```
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)`: Konvertieren `num` von `from_base` nach `to_base`

Beispiele:

```
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### corr

`corr(expr1, expr2)`: Gibt Pearson-Korrelationskoeffizient zwischen einer Reihe von Zahlenpaaren zurück.

#### cos

`cos(expr)`: Gibt den Kosinus von zurück, `expr`als ob er von berechnet `java.lang.Math.cos`.

Beispiel:

```
> SELECT cos(0);
 1.0
```

#### cosh

`cosh(expr)`: Gibt den Hyperbelkosinus von zurück, `expr`als ob er von berechnet `java.lang.Math.cosh`würde.

Argumente:
- `expr`: Hyperbelwinkel

Beispiel:

```
> SELECT cosh(0);
 1.0
```

#### cot

`cot(expr)`: Gibt den Cotangent von zurück, `expr`als ob berechnet von `1/java.lang.Math.cot`.

Argumente:
- `expr`: Winkel in Radianten

Beispiel:

```
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()`: Berechnet den Rang eines Werts in einer Gruppe von Werten. Das Ergebnis ist ein plus der zuvor zugewiesene Rangwert. Im Gegensatz zur Funktion `rank`entstehen `dense_rank` keine Lücken in der Rangfolge.

#### e

`e()`: Gibt Eulers Nummer zurück, z. B.

Beispiel:

```
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`: Gibt e bis zur Stärke von `expr`zurück.

Beispiel:

```
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)`: Gibt exp(`expr`) - 1 zurück.

Beispiel:

```
> SELECT expm1(0);
 0.0
```

#### factoriell

`factorial(expr)`: Gibt das Faktorium von `expr`zurück. `expr` ist [0.20]. Andernfalls null.

Beispiel:

```
> SELECT factorial(5);
 120
```

#### floor

`floor(expr)`: Gibt die größte Ganzzahl zurück, die nicht größer als `expr`.

Beispiele:

```
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### most

`greatest(expr, ...)`: Gibt den höchsten Wert aller Parameter zurück, wobei Null-Werte übersprungen werden.

Beispiel:

```
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### hypot

`hypot(expr1, expr2)`: Gibt sqrt(`expr1`<sup>2</sup> + `expr2`<sup>2</sup>) zurück.

Beispiel:

```
> SELECT hypot(3, 4);
 5.0
```

#### Kurtosis

`kurtosis(expr)`: Gibt den Kurtosewert zurück, der aus den Werten einer Gruppe berechnet wird.


#### least

`least(expr, ...)`: Gibt den geringsten Wert aller Parameter zurück, wobei Null-Werte übersprungen werden.

Beispiel:

```
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### Levenshtein

`levenshtein(str1, str2)`: Gibt den Levenshtein-Abstand zwischen den beiden angegebenen Zeichenfolgen zurück.

Beispiele:

```
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`: Gibt den natürlichen Logarithmus (Basis e) von `expr`zurück.

Beispiel:

```
> SELECT ln(1);
 0.0
```

#### log

`log(base, expr)`: Gibt den Logarithmus von `expr` mit zurück `base`.

Beispiel:

```
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`: Gibt den Logarithmus von `expr` mit Basis 10 zurück.

Beispiel:

```
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: Rückgabe `log(1 + expr)`.

Beispiel:

```
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`: Gibt den Logarithmus von `expr` Basis 2 zurück.

Beispiel:

```
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`: Gibt den Maximalwert von `expr`zurück.

#### mid

`mean(expr)`: Gibt den aus den Werten einer Gruppe berechneten Mittelwert zurück.

#### min

`min(expr)`: Gibt den Mindestwert von `expr`zurück.

#### monotonisch_zing_id

`monotonically_increasing_id()`: Gibt monotonisch steigende 64-Bit-Ganzzahlen zurück. Die generierte ID wird garantiert monoton erhöht und eindeutig, jedoch nicht fortlaufend. Die aktuelle Implementierung setzt die Partition-ID in die oberen 31 Bit und die unteren 33 Bit stellen die Datensatznummer in jeder Partition dar. Es wird angenommen, dass der Datenrahmen weniger als 1 Milliarde Partitionen hat und jede Partition weniger als 8 Milliarden Datensätze hat. Die Funktion ist nicht deterministisch, da ihr Ergebnis von Partition-IDs abhängt.

#### negative

`negative(expr)`: Gibt den negierten Wert von `expr`zurück.

Beispiel:

```
> SELECT negative(1);
 -1
```

#### percent_rank

`percent_rank()`: Berechnet die prozentuale Rangfolge eines Werts in einer Gruppe von Werten.

#### Perzentil

`percentile(col, percentage [, frequency])`: Gibt den exakten Perzentilwert der numerischen Spalte `col` zum angegebenen Prozentwert zurück. Der Wert von `percentage` muss zwischen 0,0 und 1,0 liegen. Der Wert von `frequency` sollte ein positiver integraler Wert sein.

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`: Gibt das exakte Perzentilwertarray der numerischen Spalte `col` mit den angegebenen Prozentwerten zurück. Jeder Wert des Prozentarray muss zwischen 0,0 und 1,0 liegen. Der Wert von `frequency` sollte ein positiver integraler Wert sein.

#### Perzentile_ca

`percentile_approx(col, percentage [, accuracy])`: Gibt den ungefähren Perzentilwert der numerischen Spalte `col` zum angegebenen Prozentwert zurück. Der Wert von `percentage` muss zwischen 0,0 und 1,0 liegen. Der `accuracy` Parameter (Standard: 10000) ist ein positives numerisches Literal, das die Genauigkeit der Annäherung auf Kosten des Speichers steuert. Höhere Werte für `accuracy` Erträge bessere Genauigkeit, `1.0/accuracy` ist der relative Fehler der Annäherung. Wenn `percentage` es sich um ein Array handelt, muss jeder Wert des Prozentarray zwischen 0,0 und 1,0 liegen. Gibt in diesem Fall das Array mit dem ungefähren Perzentil der Spalte `col` im angegebenen Prozentarray zurück.

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

`pmod(expr1, expr2)`: Gibt den positiven Wert von `expr1` mod zurück `expr2`.

Beispiele:

```
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### positiv

`positive(expr)`: Gibt den positiven Wert von `expr`

#### pow

`pow(expr1, expr2)`: Macht `expr1` von `expr2`.

Beispiel:

```
> SELECT pow(2, 3);
 8.0
```

#### power

`power(expr1, expr2)`: Macht `expr1` von `expr2`.

Beispiele:

```
> SELECT power(2, 3);
 8.0
```

#### Radianten

`radians(expr)`: Konvertiert Grad in Radianten.

Argumente:

- `expr`: Winkel in Grad

Beispiel:

```
> SELECT radians(180);
 3.141592653589793
```

#### rand

`rand([seed])`: Gibt einen zufälligen Wert mit unabhängigen und identisch verteilten (i.d.) gleichmäßig verteilten Werten in (0, 1) zurück.

Beispiele:

```
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE] Diese Funktion ist im Allgemeinen nicht deterministisch.

#### randn

`randn([seed])`: Gibt einen zufälligen Wert mit unabhängigen und identisch verteilten (i.d.) Werten zurück, die von der normalen Standardverteilung gezeichnet werden.

Beispiele:

```
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE] Diese Funktion ist im Allgemeinen nicht deterministisch.

#### rint

`rint(expr)`: Gibt den Dublette-Wert zurück, der dem Argument am nächsten kommt und mit einer mathematischen Ganzzahl identisch ist.

Beispiele:

```
> SELECT rint(12.3456);
 12.0
```

#### round

`round(expr, d)`: Gibt mithilfe des Rundungsmodus HALF_UP auf `expr` `d` Dezimalstellen gerundet zurück.

Beispiel:

```
> SELECT round(2.5, 0);
 3.0
```

#### sign

`sign(expr)`: Gibt -1.0, 0.0 oder 1.0 als negativ, 0 oder positiv `expr` zurück.

Beispiel:

```
> SELECT sign(40);
 1.0
```

#### signum

`signum(expr)`: Gibt -1.0, 0.0 oder 1.0 als negativ, 0 oder positiv `expr` zurück.

Beispiel:

```
> SELECT signum(40);
 1.0
```

#### sin

`sin(expr)`: Gibt den Sinus von zurück, `expr`als ob berechnet von `java.lang.Math.sin`.

Argumente:

- `expr`: Winkel in Radianten

Beispiel:

```
> SELECT sin(0);
 0.0
```

#### sinh

`sinh(expr)`: Gibt Hyperbelsinus von zurück, `expr`als ob berechnet von `java.lang.Math.sinh`.

Argumente:

- `expr`: Hyperbelwinkel

Beispiel:

```
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)`: Gibt die Quadratwurzel von `expr`zurück.

Beispiel:

```
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`: Gibt die aus den Werten einer Gruppe errechnete Standardabweichung zurück.

#### stddev_pop

`sttdev_pop(expr)`: Gibt die Populationsstandardabweichung zurück, berechnet aus Werten einer Gruppe.

#### stddev_samp

`stddev_samp(expr)`: Gibt die aus den Werten einer Gruppe errechnete Standardabweichung zurück.

#### sum

`sum(expr)`: Gibt die aus den Werten einer Gruppe berechnete Summe zurück.

#### tan

`tan(expr)`: Gibt den Tangens von zurück, `expr`als ob berechnet von `java.lang.Math.tan`.

Argumente:

- `expr`: Winkel in Radianten

Beispiel:

```
> SELECT tan(0);
 0.0
```

#### tanh

`tanh(expr)`: Gibt den hyperbolischen Tangens von zurück, `expr`als ob berechnet von `java.lang.Math.tanh`.

Argumente:

- `expr`: Hyperbelwinkel

Beispiel:

```
> SELECT tanh(0);
 0.0
```

#### var_pop

`var_pop(expr)`: Gibt die Populationsvarianz zurück, die aus den Werten einer Gruppe berechnet wird.

#### Var_samp

`var_samp(expr)`: Gibt die aus den Werten einer Gruppe errechnete Beispielvarianz zurück.

#### varianz

`variance(expr)`: Gibt die aus den Werten einer Gruppe errechnete Beispielvarianz zurück.

### Logische Operatoren

#### Logisch nicht

`! expr`: Logisch nicht.

#### Niedriger als

`expr1 < expr2`: Gibt TRUE zurück, wenn `expr1` kleiner als `expr2`.

Argumente:

- `expr1, expr2`: Die beiden Ausdruck müssen gleich sein, oder sie können in einen gemeinsamen Typ gegossen werden und müssen ein Typ sein, der geordnet werden kann. Zum Beispiel ist der Zuordnungstyp nicht geordnet, daher wird er nicht unterstützt. Bei komplexen Typen wie Array/Struktur müssen die Datentypen der Felder sortierbar sein.

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

`expr1 <= expr2`: Gibt TRUE zurück, wenn `expr1` kleiner oder gleich `expr2`ist.

Argumente:

- `expr1, expr2`: Die beiden Ausdruck müssen gleich sein oder in einen gemeinsamen Typ gegossen werden und müssen ein Typ sein, der geordnet werden kann. Zum Beispiel ist der Zuordnungstyp nicht geordnet, daher wird er nicht unterstützt. Bei komplexen Typen wie Array/Struktur müssen die Datentypen der Felder sortierbar sein.

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

`expr1 = expr2`: Gibt TRUE zurück, wenn `expr1` gleich `expr2`oder FALSE.

Argumente:

- `expr1, expr2`: Die beiden Ausdruck müssen gleich sein, oder sie können in einen gemeinsamen Typ umgewandelt werden und müssen ein Typ sein, der für Gleichheitsvergleiche verwendet werden kann. Der Zuordnungstyp wird nicht unterstützt. Bei komplexen Typen wie Array/Struktur müssen die Datentypen der Felder sortierbar sein.

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

`expr1 > expr2`: Gibt TRUE zurück, wenn `expr1` größer als `expr2`.

Argumente:

- `expr1, expr2`: Die beiden Ausdruck müssen gleich sein, oder sie können in einen gemeinsamen Typ gegossen werden und müssen ein Typ sein, der geordnet werden kann. Zum Beispiel ist der Zuordnungstyp nicht geordnet, daher wird er nicht unterstützt. Bei komplexen Typen wie Array/Struktur müssen die Datentypen der Felder sortierbar sein.

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

`expr1 >= expr2`: Gibt TRUE zurück, wenn größer als oder gleich `expr1` ist `expr2`.

Argumente:

- `expr1, expr2`: Die beiden Ausdruck müssen gleich sein, oder sie können in einen gemeinsamen Typ gegossen werden und müssen ein Typ sein, der geordnet werden kann. Zum Beispiel ist der Zuordnungstyp nicht geordnet, daher wird er nicht unterstützt. Bei komplexen Typen wie Array/Struktur müssen die Datentypen der Felder sortierbar sein.

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

#### Bitweise exklusiv oder

`expr1 ^ expr2`: Gibt das Ergebnis der bitweisen exklusiven ODER von `expr1` und `expr2`.

Beispiel:

```
> SELECT 3 ^ 5;
 2
```

#### und

`expr1 and expr2`: Logisches UND.

#### arrays_überlappung

`arrays_overlap(a1, a2)`: Gibt &quot;true&quot;zurück, wenn a1 mindestens ein Element enthält, das nicht null ist und auch in a2 vorhanden ist. Wenn die Arrays kein gemeinsames Element haben und beide nicht leer sind und beide ein Null-Element enthalten, wird null zurückgegeben. Andernfalls wird false zurückgegeben.

Beispiel:

```
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

Seit: 2.4.0

#### assert_true

`assert_true(expr)`: Gibt eine Ausnahme aus, wenn `expr` dies nicht der Fall ist.

Beispiel:

```
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)`: Wenn &quot;true&quot; `expr1` ausgewertet wird, wird zurückgegeben `expr2`; andernfalls wird `expr3`zurückgegeben.

Beispiel:

```
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### ifnull

`ifnull(expr1, expr2)`: Gibt `expr2` zurück, wenn `expr1` null oder `expr1` anders angegeben.

Beispiel:

```
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`: Gibt TRUE zurück, wenn `expr` gleich einer valN.

Argumente:
- `expr1, expr2, expr3, ...`: Die Argumente müssen vom gleichen Typ sein.

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

#### Isnan

`isnan(expr)`: Gibt TRUE zurück, wenn NaN `expr` ist, andernfalls FALSE.

Beispiel:

```
> SELECT isnan(cast('NaN' as double));
 true
```

#### isnotnull

`isnotnull(expr)`: Gibt true zurück, wenn `expr` nicht null, andernfalls false.

Beispiele:

```
> SELECT isnotnull(1);
 true
```

#### isnull

`isnull(expr)`: Gibt true zurück, wenn `expr` null ist, andernfalls false.

Beispiel:

```
> SELECT isnull(1);
 false
```

#### nanvl

`nanvl(expr1, expr2)`: Gibt zurück, `expr1` wenn es nicht NaN ist oder `expr2` anders.

Beispiel:

```
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr`: Logisch nicht.

#### oder

`expr1 or expr2`: Logisches oder.

#### xpath_boolean

`xpath_boolean(xml, xpath)`: Gibt &quot;true&quot;zurück, wenn der XPath-Ausdruck &quot;true&quot;ergibt oder ein übereinstimmender Knoten gefunden wird.

Beispiel:

```
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### Datums-/Uhrzeitfunktionen

#### add_month

`add_months(start_date, num_months)`: Gibt das Datum zurück, das `num_months` nach `start_date`.

Beispiel:

```
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

Seit: 1.5.0

#### date_add

`date_add(start_date, num_days)`: Gibt das Datum zurück, das `num_days` nach `start_date`.

Beispiel:

```
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

Seit: 1.5.0

#### date_format

`date_format(timestamp, fmt)`: Konvertiert `timestamp` den Wert in einen String in dem Format, das vom Datumsformat angegeben wird `fmt`.

Beispiel:

```
> SELECT date_format('2016-04-08', 'y');
 2016
```

Seit: 1.5.0

#### date_sub

`date_sub(start_date, num_days)`: Gibt das Datum zurück, das `num_days` vor dem Datum liegt `start_date`.

Beispiel:

```
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

Seit: 1.5.0

#### date_trunc

`date_trunc(fmt, ts)`: Gibt Zeitstempel zurück, die auf die vom Formatmodell angegebene Einheit abgeschnitten werden `fmt`. `fmt` sollte einer von [&quot;YEAR&quot;, &quot;YYYY&quot;, &quot;YY&quot;, &quot;MON&quot;, &quot;MONTH&quot;, &quot;MM&quot;, &quot;DAY&quot;, &quot;DD&quot;, &quot;HOUR&quot;, &quot;MINUTE&quot;, &quot;ZWEI&quot;, &quot;WOCHE&quot;, &quot;QUARTER&quot; sein.]

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

`datediff(endDate, startDate)`: Gibt die Anzahl der Tage von `startDate` bis `endDate`zu zurück.

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

`dayofweek(date)`: Gibt den Wochentag für Datum/Zeitstempel zurück (1 = Sonntag, 2 = Montag, ..., 7 = Samstag).

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

`from_unixtime(unix_time, format)`: Gibt `unix_time` in der angegebenen `format`Datei zurück.

Beispiel:

```
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

Seit: 1.5.0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`: Interpretiert einen Zeitstempel wie &quot;2017-07-14 02:40:00.0&quot;als Zeit in UTC und rendert diese Zeit als Zeitstempel in der angegebenen Zeitzone. Beispielsweise würde &quot;GMT+1&quot;zu &quot;2017-07-14 03:40:00.0&quot;führen.

Beispiel:

```
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

Seit: 1.5.0

#### Stunde

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

#### Minute

`minute(timestamp)`: Gibt die Minutenkomponente der Zeichenfolge/des Zeitstempels zurück.

Beispiel:

```
> SELECT minute('2009-07-30 12:58:59');
 58
```

Seit: 1.5.0

#### month

`month(date)` Gibt die Komponente Monat des Datums/Zeitstempels zurück.

Beispiel:

```
> SELECT month('2016-07-30');
 7
```

Seit: 1.5.0

#### month_between

`months_between(timestamp1, timestamp2[, roundOff])`: Ist `timestamp1` der Wert später als `timestamp2`, ist das Ergebnis positiv. Wenn `timestamp1` und `timestamp2` sich am gleichen Tag des Monats befinden oder beide der letzte Tag des Monats sind, wird die Tageszeit ignoriert. Andernfalls wird die Differenz auf der Grundlage von 31 Tagen pro Monat berechnet und auf 8 Stellen gerundet, es sei denn, `roundOff=false`es handelt sich um einen Zeitraum von 31 Tagen.

Beispiele:

```
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

Seit: 1.5.0

#### next_day

`next_day(start_date, day_of_week)`: Gibt das erste Datum zurück, das nach `start_date` dem angegebenen Datum liegt.

Beispiel:

```
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

Seit: 1.5.0

#### Quartal

`quarter(date)`: Gibt das Quartal des Jahres für das Datum im Bereich von 1 bis 4 zurück.

Beispiel:

```
> SELECT quarter('2016-08-31');
 3
```

Seit: 1.5.0

#### second

`second(timestamp)`: Gibt die zweite Komponente der Zeichenfolge/des Zeitstempels zurück.

Beispiel:

```
> SELECT second('2009-07-30 12:58:59');
 59
```

Seit: 1.5.0

#### to_date

`to_date(date_str[, fmt])`: Parst den `date_str` Ausdruck mit dem `fmt` Ausdruck auf ein Datum. Gibt null mit ungültiger Eingabe zurück. Standardmäßig werden bei Auslassung der Werte die Gießregeln auf ein Datum angewendet. `fmt`

Beispiele:

```
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

Seit: 1.5.0

#### to_timestamp

`to_timestamp(timestamp[, fmt])`: Parst den `timestamp` Ausdruck mit dem `fmt` Ausdruck auf einen Zeitstempel. Gibt null mit ungültiger Eingabe zurück. Standardmäßig werden bei Auslassung der Zeichenfolge die Gießregeln auf einen Zeitstempel `fmt` angewendet.

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

`to_utc_timestamp(timestamp, timezone)`: Interpretiert einen Zeitstempel wie &quot;2017-07-14 02:40:00.0&quot;als Zeit in der angegebenen Zeitzone und rendert diese Zeit als Zeitstempel in UTC. Beispielsweise würde &quot;GMT+1&quot;zu &quot;2017-07-14 01:40:00.0&quot;führen.

Beispiel:

```
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

Seit: 1.5.0

#### trunc

`trunc(date, fmt)`: Gibt das Datum zurück, wobei der Zeitraum des Tages auf die vom Formatmodell angegebene Einheit abgeschnitten wird `fmt`. `fmt` ist eins von [&quot;year&quot;, &quot;yyyy&quot;, &quot;yy&quot;, &quot;mon&quot;, &quot;month&quot;, &quot;mm&quot;]

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

#### Wochentag

`weekday(date)`: Gibt den Wochentag für Datum/Zeitstempel zurück (0 = Montag, 1 = Dienstag, ..., 6 = Sonntag).

Beispiel:

```
> SELECT weekday('2009-07-30');
 3
```

Seit: 2.4.0

#### week_of_year

`weekofyear(date)`: Gibt die Woche des Jahres des angegebenen Datums zurück. Eine Woche gilt als Beginn an einem Montag und Woche 1 ist die erste Woche mit >3 Tagen.

Beispiel:

```
> SELECT weekofyear('2008-02-20');
 8
```

Seit: 1.5.0

#### when

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`: Wenn `expr1` = true, gibt zurück `expr2`; else when `expr3` = true, gibt zurück `expr4`; else gibt zurück `expr5`.

Argumente:

- `expr1`, `expr3`: Die Ausdruck für die Zweigstellenbedingung sollten alle booleschen Typ sein.
- `expr2`, `expr4``expr5`: Die Ausdruck für den Zweigstellenwert und der Ausdruck für den anderen Wert sollten identisch sein oder zu einem gemeinsamen Typ konvertierbar sein.

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

`year(date)`: Gibt die Komponente Jahr des Datums/Zeitstempels zurück.

Beispiel:

```
> SELECT year('2016-07-30');
 2016
```

Seit: 1.5.0

### Aggregat-Funktionen

#### ca_count_different

`approx_count_distinct(expr[, relativeSD])`: Gibt die geschätzte Kardinalität von HyperLog++ zurück. `relativeSD` definiert den maximal zulässigen Schätzfehler.

### Arrays 

#### array

`array(expr, ...)`: Gibt ein Array mit den angegebenen Elementen zurück.

Beispiel:

```
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`: Gibt TRUE zurück, wenn das Array den Wert enthält.

Beispiel:

```
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_different

`array_distinct(array)`: Entfernt Duplikat-Werte aus dem Array.

Beispiel:

```
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

Seit: 2.4.0

#### array_exceptions

`array_except(array1, array2)`: Gibt ein Array der Elemente in, jedoch nicht in `array1` `array2`ohne Duplikat zurück.

Beispiel:

```
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

Seit: 2.4.0

#### array_intersect

`array_intersect(array1, array2)`: Gibt ein Array der Elemente im Schnittpunkt von und `array1` `array2`ohne Duplikat zurück.

Beispiel:

```
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

Seit: 2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])`: Verkettet die Elemente des angegebenen Arrays mit dem Trennzeichen und einer optionalen Zeichenfolge, um Nulls zu ersetzen. Wenn kein Wert für festgelegt ist, `nullReplacement`wird jeder Nullwert gefiltert.

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

`array_max(array)`: Gibt den Maximalwert im Array zurück. Null-Elemente werden übersprungen.

Beispiel:

```
> SELECT array_max(array(1, 20, null, 3));
 20
```

Seit: 2.4.0

#### array_min

`array_min(array)`: Gibt den Mindestwert im Array zurück. Null-Elemente werden übersprungen.

Beispiel:

```
> SELECT array_min(array(1, 20, null, 3));
 1
```

Seit: 2.4.0

#### array_position

`array_position(array, element)`: Gibt den (1-basierten) Index des ersten Elements des Arrays so lange zurück.

Beispiel:

```
> SELECT array_position(array(3, 2, 1), 1);
 3
```

Seit: 2.4.0

#### array_remove

`array_remove(array, element)`: Entfernen Sie alle Elemente, die dem Element entsprechen, aus dem Array.

Beispiel:

```
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

Seit: 2.4.0

#### array_repeat

`array_repeat(element, count)`: Gibt das Array mit den Elementzählzeiten zurück.

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

#### array_Vereinigung

`array_union(array1, array2)`: Gibt ein Array der Elemente in der Vereinigung von und `array1` `array2`ohne Duplikat zurück.

Beispiel:

```
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

Seit: 2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)`: Gibt ein zusammengeführtes Array von Strukturen zurück, in denen die N-te Struktur alle N-ten Werte von Eingabe-Arrays enthält.

Beispiele:

```
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

Seit: 2.4.0

#### element_at

`element_at(array, index)`: Gibt das Element des Arrays bei einem gegebenen (1-basierten) Index zurück. Wenn `index < 0`diese Option aktiviert ist, greift sie auf Elemente vom letzten zum ersten zu. Gibt NULL zurück, wenn der Index die Länge des Arrays überschreitet.

`element_at(map, key)`: Gibt den Wert für den angegebenen Schlüssel zurück oder NULL, wenn der Schlüssel nicht in der Zuordnung enthalten ist

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

`find_in_set(str, str_array)`: Gibt den Index (1-basiert) der angegebenen Zeichenfolge (`str`) in der kommagetrennten Liste (`str_array`) zurück. Gibt 0 zurück, wenn die Zeichenfolge nicht gefunden wurde oder wenn die angegebene Zeichenfolge (`str`) ein Komma enthält.

Beispiel:

```
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### reduzieren

`flatten(arrayOfArrays)`: Wandelt ein Array von Arrays in ein einzelnes Array um.

Beispiel:

```
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

Seit: 2.4.0

#### inline

`inline(expr)`: Explodiert ein Array von Strukturen in eine Tabelle.

Beispiel:

```
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inline_outer

`inline_outer(expr)`: Explodiert ein Array von Strukturen in eine Tabelle.

Beispiel:

```
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### posexplode

`posexplode(expr)`: Teilt die Elemente des Arrays `expr` in mehrere Zeilen mit Positionen oder die Elemente der Zuordnung in mehrere Zeilen und Spalten mit Positionen `expr` auf.

Beispiel:

```
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posexplode_outer

`posexplode_outer(expr)`: Teilt die Elemente des Arrays `expr` in mehrere Zeilen mit Positionen oder die Elemente der Zuordnung in mehrere Zeilen und Spalten mit Positionen `expr` auf.

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
>[!NOTE] rse logic for arrays ist seit 2.4.0 verfügbar.

#### Shuffle

`shuffle(array)`: Gibt eine zufällige Permutation des angegebenen Arrays zurück.

Beispiele:

```
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

Seit: 2.4.0
>[!NOTE] ist nicht deterministisch.

#### slice

`slice(x, start, length)`: Untergruppen-Array x, beginnend mit dem Index-Beginn (oder ausgehend vom Ende, wenn der Beginn negativ ist) mit der angegebenen Länge.

Beispiele:

```
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

Seit: 2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])`: Sortiert das Eingabe-Array in auf- oder absteigender Reihenfolge nach der natürlichen Reihenfolge der Array-Elemente. Null-Elemente werden am Anfang des zurückgegebenen Arrays in aufsteigender Reihenfolge oder am Ende des zurückgegebenen Arrays in absteigender Reihenfolge platziert.

Beispiele:

```
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`: Führt die beiden angegebenen Arrays elementweise mithilfe der Funktion in einem Array zusammen. Wenn ein Array kürzer ist, werden am Ende Nulls angehängt, um der Länge des längeren Arrays zu entsprechen, bevor die Funktion angewendet wird.

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

### Datentyp-Castingfunktionen

#### bigint

`bigint(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `bigint`.

#### binär

`binary(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `binary`.

#### Boolescher Wert

`boolean(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `boolean`.

#### cast

`cast(expr AS type)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `type`.

Beispiel:

```
> SELECT cast('10' as int);
 10
```

#### date

`date(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `date`.

#### decimal

`decimal(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `decimal`.

#### Dublette

`double(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `double`.

#### float

`float(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `float`.

#### int

`int(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `int`.

#### map

`map(key0, value0, key1, value1, ...)`: Erstellt eine Zuordnung mit den angegebenen Schlüssel/Wert-Paaren.

Beispiel:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### smallint

`smallint(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `smallint`.

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`: Erstellt eine Zuordnung, nachdem der Text mithilfe von Trennzeichen in Schlüssel/Wert-Paare aufgeteilt wurde. Die Standardtrennzeichen sind &quot;,&quot;für `pairDelim` und &quot;:&quot;für `keyValueDelim`.

Beispiele:

```
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### Zeichenfolge

`string(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `string`.

#### struct

`struct(col1, col2, col3, ...)`: Erstellt eine Struktur mit den angegebenen Feldwerten.

#### tinyint

`tinyint(expr)`: Stellt den Wert `expr` auf den Datentyp &quot;Zielgruppe&quot; `tinyint`.

### Konvertierungs- und Formatierungsfunktionen

#### ascii

`ascii(str)`: Gibt den numerischen Wert des ersten Zeichens von `str`zurück.

Beispiele:

```
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`: Konvertiert das Argument aus einer Binärdatei `bin` in eine Basis-64-Zeichenfolge.

Beispiel:

```
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### bin

`bin(expr)`: Gibt die Zeichenfolgendarstellung des im Binärformat `expr` dargestellten langen Werts zurück.

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

`bit_length(expr)`: Gibt die Bitlänge der Zeichenfolgendaten oder die Anzahl der Bit der Binärdaten zurück.

Beispiel:

```
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`: Gibt das ASCII-Zeichen zurück, das die binäre Entsprechung zu `expr`. Wenn n größer als 256 ist, entspricht das Ergebnis `chr(n % 256)`.

Beispiel:

```
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`: Gibt die Zeichenlänge der Zeichenfolgendaten oder die Anzahl der Byte der Binärdaten zurück. Die Länge der Zeichenfolgendaten umfasst die nachfolgenden Leerzeichen. Die Länge binärer Daten enthält binäre Nullen.

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

`character_length(expr)`: Gibt die Zeichenlänge der Zeichenfolgendaten oder die Anzahl der Byte der Binärdaten zurück. Die Länge der Zeichenfolgendaten umfasst die nachfolgenden Leerzeichen. Die Länge binärer Daten enthält binäre Nullen.

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

`chr(expr)`: Gibt das ASCII-Zeichen mit der binären Entsprechung zu expr zurück. Wenn n größer als 256 ist, entspricht das Ergebnis `chr(n % 256)`

Beispiel:

```
> SELECT chr(65);
 A
```

#### Grad

`degrees(expr)`: Wandelt Radianten in Grad um.

Argumente:
- `expr`: Winkel in Radianten

Beispiel:

```
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`: Formatiert die Zahl `expr1` wie &quot;#&quot;, &quot;##&quot;, &quot;##&quot;.##&#39;, auf `expr2` Dezimalstellen gerundet. Wenn `expr2` der Wert 0 beträgt, hat das Ergebnis keinen Dezimalpunkt oder Bruchteil. `expr2` akzeptiert auch ein vom Benutzer angegebenes Format. Diese Funktion soll wie die von MySQL funktionieren `FORMAT`.

Beispiele:

```
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`: Gibt einen Strukturwert mit der angegebenen `jsonStr` und `schema`zurück.

Beispiele:

```
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

Seit: 2.2.0

#### Hash

`hash(expr1, expr2, ...)`: Gibt einen Hashwert der Argumente zurück.

Beispiel:

```
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### hex

`hex(expr)`: Konvertiert `expr` in Hexadezimal.

Beispiele:

```
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`: Gibt `str` den ersten Buchstaben eines Wortes in Großbuchstaben zurück. Alle anderen Buchstaben sind in Kleinbuchstaben. Wörter werden durch Leerzeichen getrennt.

Beispiel:

```
> SELECT initcap('sPark sql');
 Spark Sql
```

#### lcase

`lcase(str)`: Gibt `str` zurück, wobei alle Zeichen in Kleinbuchstaben geändert werden.

Beispiel:

```
> SELECT lcase('SparkSql');
 sparksql
```

#### lower

`lower(str)`: Gibt `str` zurück, wobei alle Zeichen in Kleinbuchstaben geändert werden.

Beispiel:

```
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`: Gibt zurück `str`, links aufgefüllt mit `pad` einer Länge von `len`. Wenn `str` der Wert länger als `len`, wird der Rückgabewert auf `len` Zeichen gekürzt.

Beispiele:

```
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### map

`map(key0, value0, key1, value1, ...)`: Erstellt eine Zuordnung mit den angegebenen Schlüssel/Wert-Paaren.

Beispiel:

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_arrays

`map_from_arrays(keys, values)`: Erstellt eine Zuordnung mit einem Paar der angegebenen Schlüssel/Wert-Arrays. Elemente in Schlüsseln dürfen nicht null sein.

Beispiel:

```
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

Seit: 2.4.0

#### map_from_tries

`map_from_entries(arrayOfEntries)`: Gibt eine Map zurück, die aus dem angegebenen Array von Einträgen erstellt wurde.

Beispiel:

```
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

Seit: 2.4.0

#### md5

`md5(expr)`: Gibt eine MD5-128-Bit-Prüfsumme als Hex-Zeichenfolge `expr`zurück.

Beispiel:

```
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)`: Gibt zurück `str`, rechts aufgefüllt mit `pad` einer Länge von `len`. Wenn `str` der Wert länger als `len`, wird der Rückgabewert auf `len` Zeichen gekürzt.

Beispiele:

```
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rtrim

`rtrim(str)`: Entfernt die Leerzeichen am Ende `str`.

`rtrim(trimStr, str)`: Entfernt die nachgestellte Zeichenfolge, die die Zeichen aus der Zeichenfolge &quot;trim&quot;aus der `str`Zeichenfolge enthält.

Argumente:
- `str`: Ein String-Ausdruck
- `trimStr`: Die zu schneidenden Zeichenfolge. Der Standardwert ist ein Leerzeichen

Beispiele:

```
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)`: Gibt einen `sha1` Hashwert als Hex-String des `expr`Parameters zurück.

Beispiel:

```
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`: Gibt einen `sha1` Hashwert als Hex-String des `expr`Parameters zurück.

Beispiel:

```
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`: Gibt eine Prüfsumme der SHA-2-Familie als Hex-Zeichenfolge zurück `expr`. SHA-224, SHA-256, SHA-384 und SHA-512 werden unterstützt. Die Bit-Länge von 0 entspricht 256.

Beispiel:

```
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)`: Gibt Soundex-Code der Zeichenfolge zurück.

Beispiel:

```
> SELECT soundex('Miller');
 M460
```

#### stapeln

`stack(n, expr1, ..., exprk)`: Trennt `expr1`, ..., `exprk` in `n` Zeilen.

Beispiel:

```
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`: Gibt die Teilzeichenfolge `str` dieser Beginn mit `pos` und ist lang `len`oder das Bytearray zurück, das Beginn mit `pos` und ist länglich `len`.

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

`substring(str, pos[, len])`: Gibt die Teilzeichenfolge `str` dieser Beginn mit `pos` und ist lang `len`oder das Bytearray zurück, das Beginn mit `pos` und ist länglich `len`.

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

`translate(input, from, to)`: Übersetzt die `input` Zeichenfolge, indem die in der `from` Zeichenfolge vorhandenen Zeichen durch die entsprechenden Zeichen in der `to` Zeichenfolge ersetzt werden.

Beispiel:

```
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trim

`trim(str)`: Entfernt die Leerzeichen am Anfang und am Ende `str`.

`trim(BOTH trimStr FROM str)`: Entfernen Sie die führenden und nachfolgenden `trimStr` Zeichen `str`.

`trim(LEADING trimStr FROM str)`: Entfernen Sie die führenden `trimStr` Zeichen aus `str`.

`trim(TRAILING trimStr FROM str)`: Entfernen Sie die nachfolgenden `trimStr` Zeichen aus `str`.

Argumente:
- `str`: Ein String-Ausdruck
- `trimStr`: Die zu schneidenden Zeichen der Zeichenfolge, der Standardwert ist ein Leerzeichen
- `BOTH`, `FROM`: Dies sind Suchbegriffe, mit denen Sie die Zeichenfolgen an beiden Enden der Zeichenfolge zuschneiden
- `LEADING`, `FROM`: Dies sind Suchbegriffe zum Angeben von Beschneidungszeichenfolgen-Zeichen am linken Ende der Zeichenfolge
- `TRAILING`, `FROM`: Dies sind Suchbegriffe zum Angeben von Beschneidungszeichenfolgen-Zeichen am rechten Ende der Zeichenfolge

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

`ucase(str)`: Gibt zurück, `str` wobei alle Zeichen in Großbuchstaben geändert werden.

Beispiel:

```
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`: Konvertiert das Argument von einer Basis-64-Zeichenfolge `str` in eine Binärdatei.

Beispiel:

```
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### unhex

`unhex(expr)`: Konvertiert hexadezimal `expr` in binär.

Beispiel:

```
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### upper

`upper(str)`: Gibt zurück, `str` wobei alle Zeichen in Großbuchstaben geändert werden.

Beispiel:

```
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()`: Gibt eine UUID-Zeichenfolge (Universally Unique Identifier) zurück. Der Wert wird als kanonische UUID-Zeichenfolge mit 36 Zeichen zurückgegeben.

Beispiel:

```
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE] Funktion ist nicht deterministisch.

### Datenauswertung

#### Kohle

`coalesce(expr1, expr2, ...)`: Gibt das erste Nicht-Null-Argument zurück, falls vorhanden. Andernfalls null.

Beispiel:

```
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collection_Liste

`collect_list(expr)`: Erfasst und gibt eine Liste von nicht eindeutigen Elementen zurück.

#### collection_set

`collect_set(expr)`: Erfasst und gibt einen Satz von eindeutigen Elementen zurück.

#### concat

`concat(col1, col2, ..., colN)`: Gibt die Verkettung von col1, col2, ..., colN zurück.

Beispiele:

```
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE] `concat` Logik für Arrays ist seit 2.4.0 verfügbar.

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`: Gibt die Verkettung der Zeichenfolgen, durch `sep`.

Beispiel:

```
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### count

`count(*)`: Gibt die Gesamtanzahl der abgerufenen Zeilen einschließlich der Zeilen mit null zurück.

`count(expr[, expr...])`: Gibt die Anzahl der Zeilen zurück, für die die bereitgestellten Ausdruck alle ungleich null sind.

`count(DISTINCT expr[, expr...])`: Gibt die Anzahl der Zeilen zurück, für die die bereitgestellten Ausdruck eindeutig und nicht null sind.

#### crc32

`crc32(expr)`: Gibt einen zyklischen Redundanzprüfungswert des Parameters `expr` als bigint zurück.

Beispiel:

```
> SELECT crc32('Spark');
 1557323817
```

#### decode

`decode(bin, charset)`: Dekodiert das erste Argument mit dem zweiten Argumentzeichensatz.

Beispiel:

```
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### elt

`elt(n, input1, input2, ...)`: Gibt die `n`-. Eingabe zurück, z. B. wenn `input2` 2 `n` ist.

Beispiel:

```
> SELECT elt(1, 'scala', 'java');
 scala
```

#### encode

`encode(str, charset)`: Kodiert das erste Argument mit dem zweiten Argumentzeichensatz.

Beispiel:

```
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])`: Gibt den ersten Wert von `expr` für eine Gruppe von Zeilen zurück. Wenn &quot;true&quot; `isIgnoreNull` ist, werden nur Werte zurückgegeben, die nicht null sind.

#### first_value

`first_value(expr[, isIgnoreNull])`: Gibt den ersten Wert von `expr` für eine Gruppe von Zeilen zurück. Wenn &quot;true&quot; `isIgnoreNull` ist, werden nur Werte zurückgegeben, die nicht null sind.

#### get_json_object

`get_json_object(json_txt, path)`: Extrahiert ein JSON-Objekt aus `path`.

Beispiel:

```
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### gruppieren

<!-- was blank --->

#### grouping_id

<!-- was blank --->

#### instr

`instr(str, substr)`: Gibt den (1-basierten) Index des ersten Vorkommens von `substr` in zurück `str`.

Beispiel:

```
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`: Gibt ein Tupel wie die Funktion zurück, `get_json_object`es nimmt jedoch mehrere Namen. Alle Eingabungsparameter und Ausgabespaltentypen sind Zeichenfolgen.

Beispiel:

```
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### lag

`lag(input[, offset[, default]])`: Gibt den Wert von `input` an der `offset`ersten Zeile vor der aktuellen Zeile im Fenster zurück. Der Standardwert von `offset` ist 1 und der Standardwert von `default` null. Wenn der Wert von `input` an der `offset`dritten Zeile null ist, wird null zurückgegeben. Wenn keine solche Offset-Zeile vorhanden ist (z. B. wenn der Offset 1 ist, hat die erste Zeile des Fensters keine vorherige Zeile) und `default` wird zurückgegeben.

#### last

`last(expr[, isIgnoreNull])`: Gibt den letzten Wert von `expr` für eine Gruppe von Zeilen zurück. Wenn &quot;true&quot; `isIgnoreNull` ist, werden nur Werte zurückgegeben, die nicht null sind.

#### last_value

`last_value(expr[, isIgnoreNull])`: Gibt den letzten Wert von `expr` für eine Gruppe von Zeilen zurück. Wenn &quot;true&quot; `isIgnoreNull` ist, werden nur Werte zurückgegeben, die nicht null sind.

#### lead

`lead(input[, offset[, default]])`: Gibt den Wert von `input` an der `offset`dritten Zeile nach der aktuellen Zeile im Fenster zurück. Der Standardwert von `offset` ist 1 und der Standardwert von `default` null. Wenn der Wert von `input` an der `offset`dritten Zeile null ist, wird null zurückgegeben. Wenn keine solche Offset-Zeile vorhanden ist (z. B. wenn der Offset 1 ist, hat die letzte Zeile des Fensters keine nachfolgende Zeile) und `default` wird zurückgegeben.


#### left

`left(str, len)`: Gibt die Zeichen ganz links `len` (`len` kann Zeichenfolgen-Typ sein) aus der Zeichenfolge zurück `str`. Wenn `len` kleiner als oder gleich 0 ist, ist das Ergebnis eine leere Zeichenfolge.

Beispiel:

> SELECT left(&#39;Spark SQL&#39;, 3);
Spa


#### length

`length(expr)`: Gibt die Zeichenlänge der Zeichenfolgendaten oder die Anzahl der Byte der Binärdaten zurück. Die Länge der Zeichenfolgendaten umfasst die nachfolgenden Leerzeichen. Die Länge binärer Daten enthält binäre Nullen.

Beispiele:

```
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### suchen

`locate(substr, str[, pos])`: Gibt die Position des ersten Vorkommens von `substr` in `str` der Position nach `pos`. Der angegebene `pos` und der Rückgabewert sind 1-basiert.

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

`map_concat(map, ...)`: Gibt die Vereinigung aller angegebenen Maps zurück.

Beispiel:

```
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

Seit: 2.4.0

#### map_keys

`map_keys(map)`: Gibt ein ungeordnetes Array zurück, das die Schlüssel der Zuordnung enthält.

Beispiel:

```
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`: Gibt ein ungeordnetes Array mit den Werten der Zuordnung zurück.

Beispiel:

```
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### ntile

`ntile(n)`: Teilt die Zeilen für jede Fensterpartition in `n` Gruppen von 1 bis maximal `n`.

#### Nullif

`nullif(expr1, expr2)`: Gibt null zurück, wenn `expr1` gleich `expr2`oder `expr1` anders.

Beispiel:

```
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`: Gibt `expr2` zurück, wenn `expr1` null oder `expr1` anders angegeben.

Beispiel:

```
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`: Gibt zurück, `expr2` wenn `expr1` nicht null oder `expr3` nicht.

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

`position(substr, str[, pos])`: Gibt die Position des ersten Vorkommens von `substr` in `str` der Position nach `pos`. Der angegebene `pos` und der Rückgabewert sind 1-basiert.

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

`rank()`: Berechnet den Rang eines Werts in einer Gruppe von Werten. Das Ergebnis ist eins plus die Anzahl der Zeilen vor oder gleich der aktuellen Zeile in der Reihenfolge der Partition. Die Werte erzeugen Lücken in der Sequenz.

#### regexp_extract

`regexp_extract(str, regexp[, idx])`: Extrahiert eine passende Gruppe `regexp`.

Beispiel:

```
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`: Ersetzt alle Unterzeichenfolgen, `str` die `regexp` mit übereinstimmen `rep`.

Beispiel:

```
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### repeat

`repeat(str, n)`: Gibt die Zeichenfolge zurück, die den angegebenen Zeichenfolgenwert n Mal wiederholt.

Beispiel:

```
> SELECT repeat('123', 2);
 123123
```

#### replace

`replace(str, search[, replace])`: Ersetzt alle Vorkommen von `search` mit `replace`.

Argumente:
- `str`: Ein String-Ausdruck
- `search`: Ein String-Ausdruck. Wenn `search` nicht in gefunden `str`wird, wird `str` unverändert zurückgegeben.
- `replace`: Ein String-Ausdruck. Wenn `replace` keine Angabe gemacht wird oder eine leere Zeichenfolge vorliegt, wird die entfernte Zeichenfolge durch nichts ersetzt `str`.

Beispiel:

```
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### Datenaggregation

<!-- was blank -->

#### row_number

`row_number()`: Weist jeder Zeile eine eindeutige, sequenzielle Nummer zu, beginnend mit einer Zeile, entsprechend der Reihenfolge der Zeilen in der Fensterpartition.

#### Schema_der_json

`schema_of_json(json[, options])`: Gibt Schema im DDL-Format der JSON-Zeichenfolge zurück.

Beispiel:

```
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

Seit: 2.4.0

#### Sätze

`sentences(str[, lang, country])`: Teilt `str` sich in ein Array von Wörtern.

Beispiel:

```
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### Sequenz

`sequence(start, stop, step)`: Generiert ein Array von Elementen vom Beginn bis zum Stopp (einschließlich) und inkrementiert schrittweise. Der Typ der zurückgegebenen Elemente ist identisch mit dem Typ der Argument-Ausdruck.

Folgende Typen werden unterstützt: byte, short, integer, long, date, timestamp

Die `start` und die `stop` Ausdruck müssen auf denselben Typ aufgelöst werden. Wenn `start` und `stop` Ausdruck auf den Typ &quot;date&quot;oder &quot;timestamp&quot;aufgelöst werden, muss der `step` Ausdruck in den Typ &quot;interval&quot;aufgelöst werden. Andernfalls wird sie zum gleichen Typ wie die `start` und die `stop` Ausdruck aufgelöst.

Argumente:
- `start`: Ein Ausdruck. Der Beginn des Bereichs.
- `stop`: Ein Ausdruck. Das Ende des Bereichs (einschließlich).
- `step`: Ein optionaler Ausdruck. Der Schritt des Bereichs. Standardmäßig `step` ist 1, wenn `start` kleiner als oder gleich `stop`ist, andernfalls -1. Für die Zeitsequenzen ist es 1 Tag bzw. -1 Tag. Wenn `start` größer als `stop``step` , muss der Wert negativ sein und umgekehrt.

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

`shiftleft(base, expr)`: Bitweise Linksverschiebung.

Beispiel:

```
> SELECT shiftleft(2, 1);
 4
```

#### Shiftright

`shiftright(base, expr)`: Bitweise (signierte) Rechtsverschiebung.

Beispiel:

```
> SELECT shiftright(4, 1);
 2
```

#### shiftrighunsigned

`shiftrightunsigned(base, expr)`: Bitweise vorzeichenlose Rechtsverschiebung.

Beispiel:

```
> SELECT shiftrightunsigned(4, 1);
 2
```

#### size

`size(expr)`: Gibt die Größe eines Arrays oder einer Map zurück. Die Funktion gibt -1 zurück, wenn ihre Eingabe null ist und auf true festgelegt `spark.sql.legacy.sizeOfNull` ist. Wenn `spark.sql.legacy.sizeOfNull` der Wert auf false festgelegt ist, gibt die Funktion null für die Null-Eingabe zurück. Standardmäßig ist der `spark.sql.legacy.sizeOfNull` Parameter auf true gesetzt.

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

`space(n)`: Gibt eine Zeichenfolge zurück, die aus `n` Leerzeichen besteht.

Beispiel:

```
> SELECT concat(space(2), '1');
   1
```

#### split

`split(str, regex)`: Teilt `str` Ereignisse, die übereinstimmen `regex`.

Beispiel:

```
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)`: Gibt die Teilzeichenfolge `str` vor `count` Auftreten des Trennzeichens zurück `delim`. Bei `count` positivem Wert wird alles links neben dem endgültigen Trennzeichen (von links zählen) zurückgegeben. Wenn `count` der Wert negativ ist, wird alles rechts neben dem endgültigen Trennzeichen (Zählung von rechts) zurückgegeben. Die Funktion `substring_index` führt bei der Suche nach `delim`einer Groß-/Kleinschreibung eine Übereinstimmung aus.

Beispiel:

```
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### window

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`: Gibt ein Zeichenfolgenarray mit Werten innerhalb der Knoten von xml zurück, die dem XPath-Ausdruck entsprechen.

Beispiel:

```
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_Dublette

`xpath_double(xml, xpath)`: Gibt einen Wert für die Dublette zurück, den Wert Null, wenn keine Übereinstimmung gefunden wird, oder den Wert NaN, wenn eine Übereinstimmung gefunden wird, der Wert jedoch nicht numerisch ist.

Beispiel:

```
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`: Gibt einen Gleitkommawert, den Wert Null zurück, wenn keine Übereinstimmung gefunden wird, oder NaN, wenn eine Übereinstimmung gefunden wird, der Wert jedoch nicht numerisch ist.

Beispiel:

```
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`: Gibt einen ganzzahligen Wert oder den Wert Null zurück, wenn keine Übereinstimmung gefunden wird oder eine Übereinstimmung gefunden wird, der Wert jedoch nicht numerisch ist.

Beispiel:

```
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`: Gibt einen langen ganzzahligen Wert oder den Wert Null zurück, wenn keine Übereinstimmung gefunden wird oder eine Übereinstimmung gefunden wird, der Wert jedoch nicht numerisch ist.

Beispiel:

```
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`: Gibt einen Wert für die Dublette zurück, den Wert Null, wenn keine Übereinstimmung gefunden wird, oder den Wert NaN, wenn eine Übereinstimmung gefunden wird, der Wert jedoch nicht numerisch ist.

Beispiel:

```
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`: Gibt einen kurzen ganzzahligen Wert oder den Wert Null zurück, wenn keine Übereinstimmung gefunden wird oder eine Übereinstimmung gefunden wird, der Wert jedoch nicht numerisch ist.

Beispiel:

```
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`: Gibt den Textinhalt des ersten XML-Knotens zurück, der dem XPath-Ausdruck entspricht.

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

`current_date()`: Gibt das aktuelle Datum am Beginn der Auswertung der Abfrage zurück.

Seit: 1.5.0

#### current_timestamp

`current_timestamp()`: Gibt den aktuellen Zeitstempel zum Beginn der Auswertung der Abfrage zurück.

Seit: 1.5.0

#### now

`now()`: Gibt den aktuellen Zeitstempel zum Beginn der Auswertung der Abfrage zurück.

Seit: 1.5.0
