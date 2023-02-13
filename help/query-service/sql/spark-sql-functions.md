---
keywords: Experience Platform;Startseite beliebte Themen;query service;Abfrage-Service;spark sql;Spark sql;spark;Spark SQL-Funktionen;Funktionen
solution: Experience Platform
title: Spark SQL-Funktionen in Query Service
description: Diese Dokumentation enthält Informationen zu Spark-SQL-Funktionen, die die SQL-Funktionalität erweitern.
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: ht
source-wordcount: '3866'
ht-degree: 100%

---

# [!DNL Spark] SQL-Funktionen

Adobe Experience Platform Query Service bietet mehrere integrierte Spark SQL-Funktionen, um die SQL-Funktionalität zu erweitern. In diesem Dokument werden die Spark SQL-Funktionen aufgelistet, die vom Abfrage-Service unterstützt werden.

Ausführlichere Informationen zu den Funktionen, einschließlich Syntax, Verwendung und Beispielen, finden Sie in der [Dokumentation zu Spark SQL-Funktionen](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>Es werden nicht alle in der externen Dokumentation aufgeführten Funktionen unterstützt.

## Mathematische und statistische Operatoren und Funktionen {#math}

| Operator/Funktion | Beschreibung |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_3) | Gibt den Rest der beiden Zahlen zurück. |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | Multipliziert die beiden Zahlen. |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | Addiert die beiden Zahlen. |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Subtrahiert die beiden Zahlen. |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Dividiert die beiden Zahlen. |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | Gibt den absoluten Wert der Eingabe zurück. |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | Gibt den umgekehrten Kosinuswert zurück. |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | Gibt die geschätzte Kardinalität nach HyperLogLog++ zurück. |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | Gibt den Perzentil-Näherungswert zum angegebenen Prozentsatz zurück. |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | Gibt den umgekehrten Sinuswert zurück. |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | Gibt den umgekehrten Tangenswert zurück. |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | Gibt den Winkel zwischen der positiven X-Achsenebene und den durch die Koordinaten gegebenen Punkten zurück. |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | Gibt den Durchschnittswert zurück. |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | Gibt die Kubikwurzel zurück. |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) oder [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | Gibt die kleinste Ganzzahl zurück, die nicht größer als der eingegebene Wert ist. |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | Rechnet von einer Basis in eine andere um. |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | Gibt den Pearson-Koeffizienten zwischen den Zahlen zurück. |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | Gibt den Kosinuswert zurück. |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | Gibt den hyperbolischen Kosinuswert zurück. |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | Gibt den Kotangenswert zurück. |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | Gibt den Rang eines Werts in einer Gruppe von Werten zurück. |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Gibt die Eulersche Zahl zurück. |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | Gibt e hoch dem Wert zurück. |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | Gibt e hoch dem Wert minus 1 zurück. |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | Gibt die Fakultät des Werts zurück. |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | Gibt die größte Ganzzahl zurück, die kleiner als der Wert ist. |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | Gibt den größten Wert aller Parameter zurück. |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | Gibt die Hypotenuse der beiden gegebenen Werte zurück. |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | Gibt den Kurtosis-Wert aus der Gruppe zurück. |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | Gibt den kleinsten Wert aller Parameter zurück. |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | Gibt den natürlichen Logarithmus des Werts zurück. |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | Gibt den Logarithmus des Werts zurück. |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | Gibt den Logarithmus des Werts zur Basis 10 zurück. |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | Gibt den Logarithmus des Werts plus 1 zurück. |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | Gibt den Logarithmus des Werts zur Basis 2 zurück. |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | Gibt den Maximalwert des Ausdrucks zurück. |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | Gibt den aus den Werten berechneten Mittelwert zurück. |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | Gibt den Minimalwert des Ausdrucks zurück. |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | Gibt monoton steigende IDs zurück. |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | Gibt den negierten Wert zurück. |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | Gibt die prozentuale Rangfolge eines Werts zurück. |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | Gibt das genaue Perzentil zu einem gegebenen Prozentsatz zurück. |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | Gibt den Perzentil-Näherungswert zu einem gegebenen Prozentsatz zurück. |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | Gibt die Zahl Pi zurück |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | Gibt das positive Modulo zwischen zwei Werten zurück. |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | Gibt den positiven Wert zurück. |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | Gibt den ersten Wert hoch dem zweiten zurück. |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | Rechnet den Wert in Radianten um. |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | Gibt eine zufällige Zahl zwischen 0 und 1 zurück. |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | Gibt einen zufälligen Wert zurück. |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | Gibt den nächstliegenden ganzzahligen Wert vom Typ „Double“ zurück. |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | Gibt den nächsten gerundeten Wert zurück. |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign), [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | Gibt das Vorzeichen der Zahl zurück. |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | Gibt den Sinus des Werts zurück. |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | Gibt den hyperbolischen Sinus des Werts zurück. |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | Gibt die Quadratwurzel des Werts zurück. |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | Gibt die Standardabweichung des Werts zurück. |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | Gibt die Populationsstandardabweichung des Werts zurück. |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | Gibt die Stichprobenstandardabweichung des Werts zurück. |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | Gibt die Summe der Werte zurück. |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | Gibt den Tangens des Werts zurück. |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | Gibt den hyperbolischen Tangens des Werts zurück. |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | Gibt die berechnete Populationsvarianz zurück. |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp), [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | Gibt die berechnete Stichprobenvarianz zurück. |

### Logische Operatoren und Funktionen {#logical-operators}

| Operator/Funktion | Beschreibung |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) oder [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | Logisches NOT |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Kleiner als |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_9) | Kleiner oder gleich |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Gleich |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Größer als |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | Größer oder gleich |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | Bitweises exklusives Oder |
| [`\|`](https://spark.apache.org/docs/latest/api/sql/index.html#_17) | Bitweises Oder |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_19) | Bitweises Nicht |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | Gibt die allgemeinen Elemente zurück. |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | Stellt fest, ob der Ausdruck wahr ist. |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | Wenn der Ausdruck „wahr“ ergibt, wird der zweite Ausdruck zurückgegeben. Andernfalls wird der dritte Ausdruck zurückgegeben. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | Wenn der Ausdruck null ist, wird der zweite Ausdruck zurückgegeben. Andernfalls wird der erste Ausdruck zurückgegeben. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | Gibt „wahr“ zurück, wenn der erste Ausdruck in einem der nachfolgenden Ausdrücke enthalten ist. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | Gibt „wahr“ zurück, wenn der Wert keine Zahl ist. |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | Gibt „wahr“ zurück, wenn der Wert nicht null ist |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | Gibt „wahr“ zurück, wenn der Wert null ist. |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | Gibt den ersten Ausdruck zurück, sofern es sich nicht um eine Zahl handelt, ansonsten den zweiten Ausdruck. |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | Logisches OR |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | „when“ kann verwendet werden, um Verzweigungsbedingungen für einen Vergleich zu erstellen. |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | Gibt „wahr“ zurück, wenn der XPath-Ausdruck „wahr“ ergibt oder ein übereinstimmender Knoten gefunden wird. |

### Funktionen für Datum/Uhrzeit {#datetime-functions}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | Addiert Monate zum Datum. |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | Addiert Tage zum Datum. |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | Ändert das Datumsformat. |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | Substrahiert Tage vom Datum. |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | Gibt das Datum zurück, das auf die angegebene Einheit gekürzt wurde. |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | Gibt die Differenz zwischen den Daten in Tagen zurück. |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day), [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | Gibt den Tag des Monats zurück. |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | Gibt den Wochentag (1–7) zurück. |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | Gibt den Tag des Jahres zurück. |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Gibt das Datum in Unix-Zeit zurück. |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | Gibt das Datum in UTC-Zeit zurück. |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | Gibt die Stunde der Eingabe zurück. |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | Gibt den letzten Tag des Monats zurück, zu dem das Datum gehört. |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | Gibt die Minute der Eingabe zurück. |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | Gibt den Monat der Eingabe zurück. |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | Gibt die Anzahl der dazwischenliegenden Monate zurück. |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | Gibt den ersten Tag nach der Eingabe zurück. |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | Gibt das Quartal der Eingabe zurück. |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | Gibt die Sekunde der Zeichenfolge zurück |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | Konvertiert die Zeichenfolge in ein Datum. **Hinweis:** Die Zeichenfolge **muss** das Format `yyyy-mm-ddTHH24:MM:SS` haben. |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | Konvertiert die Zeichenfolge in einen Zeitstempel. **Hinweis:** Die Zeichenfolge **muss** das Format `yyyy-mm-ddTHH24:MM:SS` haben. |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | Konvertiert die Zeichenfolge in einen Unix-Zeitstempel. |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | Konvertiert die Zeichenfolge in einen UTC-Zeitstempel. |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | Kürzt das Datum. |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Gibt den Unix-Zeitstempel zurück. |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | Gibt den Wochentag (0–6) zurück. |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | Gibt die Woche des Jahres für ein gegebenes Datum zurück. |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | Gibt das Jahr der Zeichenfolge zurück. |

### Arrays {#arrays}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | Gibt ein Array mit den gegebenen Elementen zurück. |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | Prüft, ob das Array den Wert enthält. |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | Entfernt doppelte Werte (Duplikate) aus dem Array. |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | Gibt ein Array der Elemente im ersten Array zurück, nicht jedoch im zweiten. |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | Gibt die Schnittmenge der beiden Arrays zurück. |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | Verbindet zwei Arrays. |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | Gibt den Maximalwert des Arrays zurück. |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | Gibt den Minimalwert des Arrays zurück. |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | Gibt die 1-basierte Position des Elements zurück. |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | Entfernt alle Elemente, die gleich dem Element sind. |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | Erstellt ein Array, das den Wert x-mal enthält. |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | Sortiert das Array. |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | Verbindet das Array ohne Duplikate. |
| [`arrays_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | Kombiniert die Werte der gegebenen Arrays mit den Werten der ursprünglichen Sammlung bei einem bestimmten Index. |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | Gibt die Größe des Arrays zurück. |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | Gibt das Element an einer Position zurück. |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | Trennt Elemente des Arrays in mehrere Zeilen, ausschließlich null. |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | Trennt Elemente des Arrays in mehrere Zeilen, einschließlich null. |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | Gibt die 1-basierte Position des Arrays zurück. |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | Reduziert ein Array von Arrays. |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | Trennt ein Array von Structs in eine Tabelle, ausschließlich null. |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | Trennt ein Array von Structs in eine Tabelle, einschließlich null. |
| [`posexplode`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplode) | Trennt Elemente des Arrays in mehrere Zeilen mit Positionen, ausschließlich null. |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | Kehrt Elemente des Arrays um. |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | Gibt eine zufällige Permutation des Arrays zurück. |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | Unterteilt ein Array. |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | Sortiert ein Array in einer bestimmten Reihenfolge. |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | Führt die beiden Arrays in einem Array zusammen, bevor eine Funktion angewendet wird. |

### Funktionen zur Umwandlung von Datentypen {#datatype-casting}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | Ändert den Datentyp in „Bigint“. |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | Ändert den Datentyp in „Binary“. |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | Ändert den Datentyp in „Boolean“. |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | Ändert den Datentyp in den angegebenen Typ. |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | Ändert den Datentyp in „Date“. |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | Ändert den Datentyp in „Decimal“. |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | Ändert den Datentyp in „Double“. |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | Ändert den Datentyp in „Float“. |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | Ändert den Datentyp in „Int“. |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | Ändert den Datentyp in „Smallint“. |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | Erstellt eine Zuordnung aus einer Zeichenfolge. |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | Ändert den Datentyp in „String“. |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | Erstellt einen Struct. |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | Ändert den Datentyp in „Tinyint“. |

### Konvertierungs- und Formatierungsfunktionen {#conversion}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | Gibt den numerischen Wert (ASCII) zurück. |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | Ändert das Argument in eine base64-Zeichenfolge. |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | Ändert das Argument in einen Binärwert. |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | Gibt die Bit-Länge zurück. |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char), [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | Gibt das ASCII-Zeichen zurück. |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length), [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | Gibt die Zeichenfolgenlänge zurück |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | Gibt den Wert der zyklischen Redundanzprüfung zurück. |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | Rechnet Radiant in Grad um. |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | Ändert das Zahlenformat. |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json), [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | Ruft Daten von JSON ab. |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | Gibt den Hash-Wert zurück. |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | Konvertiert das Argument in einen Hexadezimalwert. |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | Ändert die Zeichenfolge so, dass der erste Buchstabe jedes Worts großgeschrieben wird. |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase), [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | Ändert die Zeichenfolge so, dass alle Wörter kleingeschrieben werden. |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | Füllt die linke Seite einer Zeichenfolge auf. |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | Erstellt eine Zuordnung. |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | Erstellt eine Zuordnung aus einem Array. |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | Erstellt eine Zuordnung aus einem Array von Structs. |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | Gibt den md5-Wert zurück. |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | Füllt die rechte Seite einer Zeichenfolge auf. |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | Entfernt nachfolgende Leerzeichen. |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha), [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | Gibt den SHA1-Wert zurück. |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | Gibt den SHA2-Wert zurück. |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | Gibt den Soundex-Code zurück. |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | Trennt Werte in Zeilen. |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr), [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | Gibt die Unterzeichenfolge zurück. |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | Gibt eine JSON-Zeichenfolge zurück. |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | Ersetzt Werte in der Zeichenfolge. |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | Entfernt voranstehende und nachfolgende Zeichen. |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase), [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | Ändert die Zeichenfolge so, dass alles großgeschrieben wird. |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | Konvertiert die base64-Zeichenfolge in einen Binärwert. |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | Konvertiert den Hexadezimalwert in einen Binärwert. |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | Gibt eine UUID zurück. |

### Datenevaluierung {#data-evaluation}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | Gibt das erste Argument zurück, das nicht null ist. |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | Gibt eine Liste nicht eindeutiger Elemente zurück. |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | Gibt einen Satz eindeutiger Elemente zurück. |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | Verkettet Zeichenfolgen. |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | Verkettet mit Trennzeichen. |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | Gibt die Gesamtanzahl der Zeilen zurück. |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | Decodiert mit einem Zeichensatz. |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | Gibt die [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n). Eingabe zurück. |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | Codiert mit einem Zeichensatz. |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first), [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | Gibt den ersten Wert zurück. |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | Gibt an, ob eine Spalte gruppiert ist. |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | Gibt die Gruppierungsebene zurück. |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | Gibt einen 1-basierten Index des Vorkommens von Zeichen zurück. |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | Gibt einen Tupel aus einer JSON-Eingabe zurück. |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag), [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | Gibt den Wert vor dem Versatz zurück. |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last), [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | Gibt den letzten Wert zurück. |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | Gibt die ersten [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) Zeichen zurück. |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | Gibt die Länge der Zeichenfolge zurück |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | Gibt die Levenshtein-Distanz zwischen Zeichenfolgen zurück. |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate), [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | Gibt die Position des ersten Vorkommens einer Unterzeichenfolge zurück. |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | Verkettet eine Zuordnung. |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | Gibt die Schlüssel einer Zuordnung zurück. |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | Gibt die Werte einer Zuordnung zurück. |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | Teilt Zeilen in Partitionen auf. |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | Gibt null zurück, wenn „wahr“. |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | Gibt den Wert zurück, wenn null, |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | Gibt den Wert zurück, wenn nicht null. |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | Extrahiert einen Teil einer URL. |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | Berechnet den Rang eines Werts. |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | Extrahiert etwas, das dem regulären Ausdruck entspricht. |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | Ersetzt etwas, das dem regulären Ausdruck entspricht. |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | Gibt eine Zeichenfolge zurück, die sich wiederholt. |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | Ersetzt alle Instanzen einer Zeichenfolge. |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | Erstellt eine mehrdimensionale Datenaggregation. |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | Weist eine eindeutige Zeilennummer zu. |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | Gibt das JSON-Schema zurück. |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | Teilt eine Zeichenfolge in ein Array von Wörtern auf. |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | Generiert ein Array von Elementen. |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | Gibt einen Bit-weise nach links verschobenen Wert mit Vorzeichen zurück. |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | Gibt einen Bit-weise nach rechts verschobenen Wert mit Vorzeichen zurück. |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | Gibt einen Bit-weise nach rechts verschobenen Wert ohne Vorzeichen zurück. |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | Gibt die Größe des Arrays zurück. |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | Gibt eine Zeichenfolge mit [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) Leerzeichen zurück. |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | Teilt die Zeichenfolge auf. |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | Gibt den Index einer Unterzeichenfolge zurück. |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | Fenster |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | Analysiert XML-Knoten. |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double), [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | Analysiert XML-Knoten für „Double“. |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | Analysiert XML-Knoten für „Float“. |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | Analysiert XML-Knoten für „Integer“. |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | Analysiert XML-Knoten für „Long“. |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | Analysiert XML-Knoten für „Short Integer“. |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | Analysiert XML-Knoten für „String“. |

### Aktuelle Informationen {#current-information}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | Gibt die aktuelle Datenbank zurück. |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | Gibt das aktuelle Datum zurück. |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp), [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | Gibt den aktuellen Zeitstempel zurück. |

### Funktionen höherer Ordnung {#higher-order}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | Transformiert Elemente in einem Array. |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | Prüft, ob ein Element vorhanden ist. |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | Filtert das Eingabe-Array. |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | Wendet einen binären Operator auf alle Elemente an. |
