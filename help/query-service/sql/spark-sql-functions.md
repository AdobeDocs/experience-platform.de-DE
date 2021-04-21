---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Spark-SQL;Spark-SQL;Spark;Zwiebelfunktionen;Funktionen
solution: Experience Platform
title: Spark SQL-Funktionen im Abfrage-Dienst
topic-legacy: spark sql functions
description: Diese Dokumentation enthält Informationen zu Spark-SQL-Funktionen, die die SQL-Funktionalität erweitern.
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '3893'
ht-degree: 2%

---

# [!DNL Spark] SQL-Funktionen

Adobe Experience Platform Abfrage Service bietet mehrere integrierte Spark SQL-Funktionen, um die SQL-Funktionalität zu erweitern. Dieses Dokument Liste die Spark-SQL-Funktionen, die vom Abfrage Service unterstützt werden.

Ausführlichere Informationen zu den Funktionen, einschließlich Syntax, Verwendung und Beispielen, finden Sie in der [SQL-Funktionsdokumentation](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>Es werden nicht alle in der externen Dokumentation aufgeführten Funktionen unterstützt.

## Kategorien

- [Mathematische und statistische Operatoren und Funktionen](#math)
- [Logische Operatoren](#logical-operators)
- [Funktionen für Datum/Uhrzeit](#datetime-functions)
- [Arrays](#arrays)
- [Funktionen zur Umwandlung von Datentypen](#datatype-casting)
- [Konvertierungs- und Formatierungsfunktionen](#conversion)
- [Datenevaluierung](#data-evaluation)
- [Aktuelle Informationen](#current-information)
- [Funktionen für höhere Reihenfolge](#higher-order)

## Mathematische und statistische Operatoren und Funktionen {#math}

| Operator/Funktion | Beschreibung |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_2) | Gibt den Rest der beiden Zahlen zurück |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_4) | Multipliziert die beiden Zahlen |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | Fügt die beiden Zahlen hinzu |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | Subtrahiert die beiden Zahlen |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Teilt die beiden Zahlen |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | Gibt den absoluten Wert der Eingabe zurück |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | Gibt den Wert für den umgekehrten Kosinus zurück |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | Gibt die geschätzte Kardinalität von HyperLog++ zurück |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | Gibt den ungefähren Perzentil-Wert zum angegebenen Prozentsatz zurück |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | Gibt den Wert für den umgekehrten Sinus zurück |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | Gibt den Wert für die umgekehrte Tangente zurück |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | Gibt den Winkel zwischen der positiven X-Achsen-Ebene und den Punkten zurück, die durch die Koordinaten angegeben werden |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | Gibt den Durchschnittswert zurück |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | Gibt den Stammordner der Cube zurück |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) oder [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | Gibt die kleinste Ganzzahl zurück, die nicht größer als der eingegebene Wert ist |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | Konvertieren von einer Basis in eine andere |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | Gibt den Pearson-Koeffizienten zwischen den Zahlen zurück |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | Gibt den Kosinuswert zurück |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | Gibt den Wert für den Hyperbelkosinus zurück |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | Gibt den Konstantenwert zurück |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | Gibt den Rang eines Werts in einer Gruppe von Werten zurück |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Gibt Euler-Nummer zurück |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | Gibt e zur Stärke des Werts zurück |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | Gibt e zur Stärke des Werts minus 1 zurück |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | Gibt das Faktorium des Werts zurück |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | Gibt die größte Ganzzahl zurück, die nicht kleiner als der Wert ist |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | Gibt den größten Wert aller Parameter zurück |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | Gibt die Hypotonie der beiden angegebenen Werte zurück |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | Gibt den Kurtosewert aus der Gruppe zurück |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | Gibt den kleinsten Wert aller Parameter zurück |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | Gibt den natürlichen Logarithmus des Werts zurück |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | Gibt den Logarithmus des Werts zurück |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | Gibt den Logarithmus (Basis 10) des Werts zurück |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | Gibt den Logarithmus des Werts plus 1 zurück |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | Gibt den Logarithmus (Basis 2) des Werts zurück |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | Gibt den Maximalwert des Ausdrucks zurück |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | Gibt den aus den Werten errechneten Mittelwert zurück |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | Gibt den Mindestwert des Ausdrucks zurück |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | Gibt monotonisch steigende IDs zurück |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | Gibt den negierten Wert zurück |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | Gibt die prozentuale Rangfolge eines Werts zurück |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | Gibt das genaue Perzentil in einem bestimmten Prozentsatz zurück |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | Gibt das ungefähre Perzentil in einem bestimmten Prozentsatz zurück |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | Gibt pi zurück |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | Gibt das positive Modul zwischen zwei Werten zurück |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | Gibt den positiven Wert zurück |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | Gibt den ersten Wert zur Stärke des zweiten Werts zurück |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | Konvertiert den Wert in Radianten |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | Gibt eine Zufallszahl zwischen 0 und 1 zurück |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | Gibt einen Zufallswert zurück |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | Gibt den Wert für die nächste Dublette zurück |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | Gibt den nächsten gerundeten Wert zurück |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign),  [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | Gibt das Zeichen der Nummer zurück |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | Gibt Sinus des Werts zurück |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | Gibt Hyperbelsinus des Werts zurück |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | Gibt die Quadratwurzel des Werts zurück |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | Gibt die Standardabweichung des Werts zurück |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | Gibt die Populationsstandardabweichung des Werts zurück |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | Gibt die Standardabweichung des Beispielwerts zurück |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | Gibt die Summe der Werte zurück |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | Gibt Tangens des Werts zurück |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | Gibt den Hyperbeltangens des Werts zurück |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | Gibt die berechnete Populationsabweichung zurück |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp),  [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | Gibt die berechnete Beispielabweichung zurück |

### Logische Operatoren und Funktionen {#logical-operators}

| Operator/Funktion | Beschreibung |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) oder [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | Logisches Nicht |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Kleiner als |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Kleiner oder gleich |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_10) | Gleich |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Größer als |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | Größer oder gleich |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Bitweise exklusives Oder |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_13) | Größer oder gleich |
| [`|`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | Bitweise oder |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | Bitweise nicht |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | Gibt die allgemeinen Elemente zurück |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | Legt fest, ob der Ausdruck &quot;true&quot;ist |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | Wenn der Ausdruck true ergibt, geben Sie den zweiten Ausdruck zurück. Andernfalls geben Sie den dritten Ausdruck zurück. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | Wenn der Ausdruck null ist, wird der zweite Ausdruck zurückgegeben. Andernfalls wird der erste Ausdruck zurückgegeben. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | Gibt TRUE zurück, wenn sich der erste Ausdruck in einem der folgenden Ausdruck befindet. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | Gibt TRUE zurück, wenn der Wert keine Zahl ist |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | Gibt TRUE zurück, wenn der Wert nicht null ist |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | Gibt TRUE zurück, wenn der Wert null ist |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | Gibt den ersten Ausdruck zurück, wenn nicht eine Zahl, andernfalls den zweiten Ausdruck |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | Logisches Oder |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | Wann können Verzweigungsbedingungen für einen Vergleich erstellt werden? |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | Gibt &quot;true&quot;zurück, wenn der XPath-Ausdruck &quot;true&quot;ergibt oder ein übereinstimmender Knoten gefunden wird |

### Funktionen für Datum/Uhrzeit {#datetime-functions}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | hinzufügen Monate |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | hinzufügen Tage bis dato |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | Datumsformat ändern |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | Tage vom Datum abziehen |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | Gibt das Datum zurück, das auf die angegebene Einheit abgeschnitten wurde |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | Gibt den Unterschied zwischen den Daten in Tagen zurück |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day),  [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | Gibt den Tag des Monats zurück |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | Gibt den Wochentag (1-7) zurück |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | Gibt den Tag des Jahres zurück |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Rückgabedatum in Unix-Zeit |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | Gibt Datum in UTC-Zeit zurück |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | Gibt die Stunde der Eingabe zurück |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | Gibt den letzten Tag des Monats zurück, zu dem das Datum gehört |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | Gibt die Minute der Eingabe zurück |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | Gibt den Monat der Eingabe zurück |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | Anzahl der Monate zwischen |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | Gibt den ersten Tag nach der Eingabe zurück |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | Gibt das Quartal der Eingabe zurück |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | Gibt die Sekunde der Zeichenfolge zurück |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | Konvertiert die Zeichenfolge in ein Datum |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | Konvertiert die Zeichenfolge in einen Zeitstempel |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | Konvertiert die Zeichenfolge in einen Unix-Zeitstempel |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | Konvertiert die Zeichenfolge in einen UTC-Zeitstempel |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | Verkürzt das Datum |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Gibt den Unix-Zeitstempel zurück |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | Wochentag (0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | Gibt die Woche des Jahres für ein bestimmtes Datum zurück |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | Gibt das Jahr der Zeichenfolge zurück |

### Arrays {#arrays}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | Erstellt ein Array mit den angegebenen Elementen |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | Überprüft, ob das Array den Wert enthält |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | Entfernt doppelte Werte (Duplikate) aus dem Array |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | Gibt ein Array der Elemente im ersten Array zurück, nicht jedoch das zweite |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | Gibt den Schnittpunkt der beiden Arrays zurück |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | Verbindet zwei Arrays |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | Gibt den Maximalwert des Arrays zurück |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | Gibt den Mindestwert des Arrays zurück |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | Gibt die 1-basierte Position des Elements zurück |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | Entfernt alle Elemente, die dem Element entsprechen |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | Erstellt ein Array, das die gezählten Werte enthält |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | Sortiert das Array |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | Verbindet das Array ohne Duplikate |
| [`array_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | PLZ |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | Gibt die Größe des Arrays zurück |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | Element an Position zurückgeben |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | Trennen Sie Array-Elemente in mehrere Zeilen, ohne Null |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | Trennen Sie Array-Elemente in mehrere Zeilen, einschließlich null |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | Gibt die 1-basierte Position des Arrays zurück |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | Reduziert ein Array von Arrays |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | Trennen Sie ein Array von Strukturen in eine Tabelle, ohne Null |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | Trennen Sie ein Array von Strukturen in eine Tabelle, einschließlich Null |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | Trennen Sie Array-Elemente in mehrere Zeilen mit Positionen, ohne Null |
| [`posexplod`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplod) | Trennen Sie Array-Elemente in mehrere Zeilen mit Positionen, einschließlich null |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | Elemente des Arrays umkehren |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | Gibt eine zufällige Permutation des Arrays zurück |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | Untergruppen eines Arrays |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | Sortieren eines Arrays in einer bestimmten Reihenfolge |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | Führt die beiden Arrays in einem Array zusammen, bevor eine Funktion angewendet wird |

### Funktionen zur Umwandlung von Datentypen {#datatype-casting}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | Datentyp zu bigint ändern |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | Datentyp in binär ändern |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | Datentyp in boolesch ändern |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | Datentyp auf den angegebenen Typ ändern |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | Datentyp auf Datum ändern |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | Datentyp in Dezimalzahl ändern |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | Datentyp in Dublette ändern |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | Datentyp in float ändern |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | Datentyp in &quot;int&quot;ändern |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | Datentyp in kleinste ändern |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | Erstellen einer Zuordnung aus einer Zeichenfolge |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | Datentyp in Zeichenfolge ändern |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | Erstellen einer Struktur |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | Datentyp in tinyint ändern |

### Konvertierungs- und Formatierungsfunktionen {#conversion}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | Den numerischen Wert (ASCII) zurückgeben |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | Ändern des Arguments in eine base64-Zeichenfolge |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | Ändern des Arguments in einen binären Wert |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | Bit-Länge zurückgeben |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char),  [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | ASCII-Zeichen zurückgeben |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length),  [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | Gibt die Zeichenfolgenlänge zurück |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | Gibt den Wert für die Prüfung der zyklischen Redundanz zurück |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | Radianten in Grad konvertieren |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | Format der Nummer ändern |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json),  [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | Daten von JSON abrufen |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | Hashwert zurückgeben |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | Konvertieren des Arguments in einen Hexadezimalwert |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | Ändert die Zeichenfolge, die als &quot;title cale&quot;bezeichnet werden soll |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase),  [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | Ändert die Zeichenfolge in Kleinbuchstaben |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | Fügt die linke Seite einer Zeichenfolge ein |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | Erstellen einer Map |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | Erstellen einer Zuordnung aus einem Array |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | Erstellen einer Map aus einem Array von Strukturen |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | md5-Wert zurückgeben |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | Fügt die rechte Seite einer Zeichenfolge ein |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | Entfernt nachgestellte Leerzeichen |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha),  [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | SHA1-Wert zurückgeben |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | SHA2-Wert zurückgeben |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | Gibt den SOUNDEX-Code zurück |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | Trennen von Werten in Zeilen |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr),  [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | Teilzeichenfolge zurückgeben |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | Gibt eine JSON-Zeichenfolge zurück |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | Werte in Zeichenfolge ersetzen |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | Entfernen von führenden und nachfolgenden Zeichen |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase),  [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | Ändern Sie die Zeichenfolge in Großbuchstaben |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | Die base64-Zeichenfolge in binäre |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | Hexadezimal in Binärdatei konvertieren |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | UUID zurückgeben |

### Datenevaluierung {#data-evaluation}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | Gibt das erste Argument ohne null zurück |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | Liste nicht eindeutiger Elemente zurückgeben |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | Zurückgeben eines Satzes eindeutiger Elemente |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | Verkettung |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | Verkettung mit Trennzeichen |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | Gibt die Gesamtanzahl der Zeilen zurück |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | Dekodieren mit einem Zeichensatz |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | Rückgabe der [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)Eingabe |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | Kodieren mit einem Zeichensatz |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first),  [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | Gibt den ersten Wert zurück |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | Gibt an, ob eine Spalte gruppiert ist |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | Gibt die Ebene der Gruppierung zurück |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | Gibt einen 1-basierten Index für das Auftreten von Zeichen zurück |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | Gibt ein Tupel aus einer JSON-Eingabe zurück |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag),  [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | Gibt den Wert vor dem Offset zurück |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last),  [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | Gibt den letzten Wert zurück |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | Gibt das erste [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)-Zeichen zurück |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | Gibt die Länge des Strings aus |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | Gibt den Levenshtein-Abstand zwischen Zeichenfolgen zurück |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate),  [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | Gibt die Position des ersten Vorkommens einer Teilzeichenfolge zurück |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | Verknüpfen einer Map |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | Schlüssel einer Karte zurückgeben |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | Werte einer Map zurückgeben |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | Zeilen in Partitionen unterteilen |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | Gibt null zurück, wenn true |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | Gibt Wert zurück, wenn null |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | Gibt Wert zurück, wenn nicht null |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | Extrahiert einen Teil einer URL |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | Berechnet Rang eines Werts |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | Extrahiert etwas, das dem Regex entspricht |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | Ersetzt etwas, das dem Regex entspricht |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | Gibt eine Zeichenfolge zurück, die wiederholt wird |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | Alle Instanzen einer Zeichenfolge ersetzen |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | Erstellen einer mehrdimensionalen Datenaggregation |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | Weist eine eindeutige Zeilennummer zu |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | Gibt das Schema der JSON-Datei zurück |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | Teilt eine Zeichenfolge in ein Array von Wörtern |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | Generiert ein Array von Elementen |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | Signierte bitweise Verschiebung links |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | Signierte bitweise Verschiebung nach rechts |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | Unbegrenzte bitweise Verschiebung nach rechts |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | Gibt die Größe des Arrays zurück |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | Gibt eine Zeichenfolge mit [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) Leerzeichen zurück |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | Zeichenfolge teilen |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | Rückkehrindex der Unterzeichenfolge |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | Fenster |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | XML-Nodes analysieren |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double),  [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | XML-Nodes für die Dublette analysieren |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | XML-Nodes für float analysieren |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | XML-Knoten für Ganzzahl analysieren |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | Analysieren von XML-Nodes für lange Zeit |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | XML-Knoten für kurze Ganzzahl analysieren |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | XML-Knoten für Zeichenfolge analysieren |

### Aktuelle Informationen {#current-information}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | Gibt die aktuelle Datenbank zurück |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | Gibt das aktuelle Datum zurück |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp),  [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | Gibt den aktuellen Zeitstempel zurück |

### Funktionen mit höherer Reihenfolge {#higher-order}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | Elemente in einem Array transformieren |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | Überprüfen, ob Element vorhanden ist |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | Filtern des Eingaberasters |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | Anwenden eines binären Operators auf alle Elemente |
