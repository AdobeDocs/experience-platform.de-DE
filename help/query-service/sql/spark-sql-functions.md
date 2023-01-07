---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; spark sql; Spark sql; spark; spark sql-Funktionen; Funktionen
solution: Experience Platform
title: Spark SQL-Funktionen in Query Service
description: Diese Dokumentation enthält Informationen zu Spark-SQL-Funktionen, die die SQL-Funktionalität erweitern.
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '3866'
ht-degree: 2%

---

# [!DNL Spark] SQL-Funktionen

Adobe Experience Platform Query Service bietet mehrere integrierte Spark-SQL-Funktionen, um die SQL-Funktionalität zu erweitern. In diesem Dokument werden die Spark-SQL-Funktionen aufgelistet, die von Query Service unterstützt werden.

Weitere Informationen zu den Funktionen, einschließlich Syntax, Verwendung und Beispielen, finden Sie im Abschnitt [Dokumentation zu Spark-SQL-Funktionen](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>Es werden nicht alle in der externen Dokumentation aufgeführten Funktionen unterstützt.

## Mathematische und statistische Operatoren und Funktionen {#math}

| Operator/Funktion | Beschreibung |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_3) | Gibt den Rest der beiden Zahlen aus |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | Multipliziert die beiden Zahlen |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | Fügt die beiden Zahlen hinzu |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Zieht die beiden Zahlen ab |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Teilt die beiden Zahlen |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | Gibt den absoluten Wert der Eingabe aus |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | Gibt den umgekehrten Kosinuswert aus |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | Gibt die geschätzte Kardinalität nach HyperLogLog++ aus |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | Gibt den Näherungswert des Perzentils zum angegebenen Prozentsatz aus |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | Gibt den umgekehrten Sinuswert aus |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | Gibt den umgekehrten Tangenswert aus |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | Gibt den Winkel zwischen der positiven X-Achsenebene und den durch die Koordinaten angegebenen Punkten aus |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | Gibt den Durchschnittswert aus |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | Gibt den Kubikstamm aus |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) oder [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | Gibt die kleinste Ganzzahl aus, die nicht größer als der eingegebene Wert ist |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | Konvertieren von einer Basis in eine andere |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | Gibt den Pearson-Koeffizienten zwischen den Zahlen aus |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | Gibt den Kosinuswert aus |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | Gibt den hyperbolischen Kosinenwert aus |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | Gibt den Kotangenwert aus |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | Gibt den Rang eines Werts in einer Gruppe von Werten aus |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Gibt die Zahl des Eulers aus |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | Gibt e bis zum Wert zurück |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | Gibt e bis zum Wert minus 1 aus |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | Gibt das Faktorium des Werts aus |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | Gibt die größte Ganzzahl aus, die nicht kleiner als der Wert ist |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | Gibt den größten Wert aller Parameter aus |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | Gibt die Hypotonie der beiden angegebenen Werte aus |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | Gibt den Kurtosis-Wert aus der Gruppe aus |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | Gibt den kleinsten Wert aller Parameter aus |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | Gibt den natürlichen Logarithmus des Werts aus |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | Gibt den Logarithmus des Werts aus |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | Gibt den Logarithmus (Basis 10) des Werts aus |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | Gibt den Logarithmus des Werts plus 1 aus |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | Gibt den Logarithmus (Basis 2) des Werts aus |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | Gibt den Maximalwert des Ausdrucks aus |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | Gibt den aus den Werten berechneten Mittelwert aus |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | Gibt den Mindestwert des Ausdrucks aus |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | Gibt monoton steigende IDs zurück |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | Gibt den negativen Wert aus |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | Gibt die prozentuale Rangfolge eines Werts aus |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | Gibt das genaue Perzentil in Prozent aus |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | Gibt den Näherungswert des Perzentils in Prozent aus |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | Gibt pi zurück |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | Gibt das positive Modul zwischen zwei Werten aus |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | Gibt den positiven Wert aus |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | Gibt den ersten Wert bis zum Wert des zweiten aus |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | Konvertiert den Wert in Radiant |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | Gibt eine Zufallszahl zwischen 0 und 1 aus |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | Gibt einen zufälligen Wert aus |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | Gibt den nächsten doppelten Wert aus |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | Gibt den nächsten gerundeten Wert aus |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign), [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | Gibt das Zeichen der Zahl aus |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | Gibt den Sinus des Werts aus |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | Gibt den hyperbolischen Sinus des Werts aus |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | Gibt die Quadratwurzel des Werts aus |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | Gibt die Standardabweichung des Werts aus |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | Gibt die Standardabweichung der Population vom Wert aus |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | Gibt die Standardabweichung der Stichprobe des Werts aus |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | Gibt die Summe der Werte aus |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | Gibt den Tangens des Werts aus |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | Gibt den hyperbolischen Tangens des Werts aus |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | Gibt die berechnete Populationsvarianz aus |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp), [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | Gibt die berechnete Varianz der Stichprobe aus |

### Logische Operatoren und Funktionen {#logical-operators}

| Operator/Funktion | Beschreibung |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) oder [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | Logisches Nicht |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Kleiner als |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_9) | Kleiner oder gleich |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Gleich |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Größer als |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | Größer oder gleich |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | Bitweise exklusives Oder |
| [`\|`](https://spark.apache.org/docs/latest/api/sql/index.html#_17) | Bitweise oder |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_19) | Bitweise nicht |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | Gibt die allgemeinen Elemente aus |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | Legt fest, ob der Ausdruck wahr ist |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | Wenn der Ausdruck &quot;true&quot;ergibt, geben Sie den zweiten Ausdruck zurück. Geben Sie andernfalls den dritten Ausdruck zurück. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | Wenn der Ausdruck null ist, wird der zweite Ausdruck zurückgegeben. Andernfalls wird der erste Ausdruck zurückgegeben. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | Gibt &quot;true&quot;zurück, wenn der erste Ausdruck in einem der folgenden Ausdrücke enthalten ist. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | Gibt &quot;true&quot;zurück, wenn der Wert keine Zahl ist |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | Gibt &quot;true&quot;zurück, wenn der Wert nicht null ist |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | Gibt &quot;true&quot;zurück, wenn der Wert null ist |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | Gibt den ersten Ausdruck aus, wenn nicht eine Zahl, sonst den zweiten Ausdruck |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | Logisches Oder |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | Wann kann verwendet werden, um verzweigte Bedingungen für den Vergleich zu erstellen? |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | Gibt &quot;true&quot;zurück, wenn der XPath-Ausdruck &quot;true&quot;ergibt oder ein übereinstimmender Knoten gefunden wird |

### Funktionen für Datum/Uhrzeit {#datetime-functions}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | Monate zum Datum hinzufügen |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | Tage zum Datum hinzufügen |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | Datumsformat ändern |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | Tage vom Datum absetzen |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | Gibt das Datum aus, das auf die angegebene Einheit gekürzt wurde |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | Gibt die Differenz zwischen den Daten in Tagen aus |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day), [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | Gibt den Tag des Monats aus |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | Gibt den Wochentag aus (1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | Gibt den Tag des Jahres aus |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Gibt Datum in Unix-Zeit zurück |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | Gibt Datum in UTC-Zeit aus |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | Gibt die Stunde der Eingabe aus |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | Gibt den letzten Tag des Monats aus, zu dem das Datum gehört |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | Gibt die Minute der Eingabe aus |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | Gibt den Monat der Eingabe aus |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | Anzahl der Monate zwischen |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | Gibt den ersten Tag nach der Eingabe aus |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | Gibt das Quartal der Eingabe aus |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | Gibt die Sekunde des Strings aus |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | Konvertiert den String in ein Datum. **Hinweis:** Die Zeichenfolge **must** im Format `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | Konvertiert die Zeichenfolge in einen Zeitstempel. **Hinweis:** Die Zeichenfolge **must** im Format `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | Konvertiert die Zeichenfolge in einen Unix-Zeitstempel |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | Konvertiert die Zeichenfolge in einen UTC-Zeitstempel |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | Kürzt das Datum |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Gibt den Unix-Zeitstempel zurück |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | Wochentag (0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | Gibt die Woche des Jahres für ein bestimmtes Datum aus |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | Gibt das Jahr des Strings aus |

### Arrays {#arrays}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | Erstellt ein Array mit den angegebenen Elementen |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | Prüft, ob das Array den Wert enthält |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | Entfernt doppelte Werte (Duplikate) aus dem Array |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | Gibt ein Array der Elemente im ersten Array zurück, nicht jedoch im zweiten |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | Gibt die Schnittmenge der beiden Arrays aus |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | Verbindet zwei Arrays |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | Gibt den Maximalwert des Arrays aus |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | Gibt den Mindestwert des Arrays aus |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | Gibt die 1-basierte Position des Elements aus |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | Entfernt alle Elemente, die dem Element entsprechen |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | Erstellt ein Array, das die gezählten Werte-Zeiten enthält |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | Sortiert das Array |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | Verbindet das Array ohne Duplikate |
| [`arrays_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | Kombiniert die Werte der angegebenen Arrays mit den Werten der ursprünglichen Kollektion an einem bestimmten Index |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | Größe des Arrays zurückgeben |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | Element an Position zurückgeben |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | Trennt Elemente des Arrays in mehrere Zeilen, ohne null |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | Trennen Sie Elemente des Arrays in mehrere Zeilen, einschließlich null. |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | Gibt die 1-basierte Position des Arrays aus |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | Reduziert ein Array von Arrays |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | Trennen Sie ein Array von Strukturen in eine Tabelle, ohne Null |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | Trennen Sie das Array von Strukturen in eine Tabelle, einschließlich null. |
| [`posexplode`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplode) | Trennen Sie Elemente des Arrays in mehrere Zeilen mit Positionen, ausgenommen Null |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | Umkehrelemente des Arrays |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | Zufällige Permutation des Arrays zurückgeben |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | Teilt ein Array ein |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | Sortieren eines Arrays in einer bestimmten Reihenfolge |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | Führt die beiden Arrays in einem Array zusammen, bevor eine Funktion angewendet wird |

### Funktionen zur Umwandlung von Datentypen {#datatype-casting}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | Datentyp in bigint ändern |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | Datentyp in Binärdatei ändern |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | Datentyp in boolesch ändern |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | Datentyp in den angegebenen Typ ändern |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | Datentyp auf Datum ändern |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | Datentyp in Dezimalzahl ändern |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | Ändern Sie den Datentyp in |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | Datentyp ändern in Gleitkommazahl |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | Ändern Sie den Datentyp in int |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | Datentyp auf smallint ändern |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | Erstellen einer Zuordnung aus einer Zeichenfolge |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | Datentyp in Zeichenfolge ändern |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | Erstellen einer Struktur |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | Datentyp in tinyint ändern |

### Konvertierungs- und Formatierungsfunktionen {#conversion}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | Numerische Werte (ASCII) zurückgeben |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | Ändern des Arguments in eine base64-Zeichenfolge |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | Das Argument in einen Binärwert ändern |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | Bitlänge zurückgeben |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char), [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | ASCII-Zeichen zurückgeben |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length), [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | Länge des Strings zurückgeben |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | Gibt den Wert der zyklischen Redundanzprüfung aus |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | Radiant in Grad konvertieren |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | Format der Zahl ändern |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json), [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | Daten von JSON abrufen |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | Hashwert zurückgeben |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | Konvertieren des Arguments in einen Hexadezimalwert |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | Ändert die Zeichenfolge, die als Titel verwendet werden soll |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase), [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | Ändert den String in Kleinbuchstaben |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | Fügt die linke Seite einer Zeichenfolge ein |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | Erstellen einer Karte |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | Erstellen einer Zuordnung aus einem Array |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | Erstellen einer Zuordnung aus einem Array von Strukturen |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | md5-Wert zurückgeben |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | Fügt die rechte Seite einer Zeichenfolge ein |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | Entfernt nachfolgende Leerzeichen |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha), [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | SHA1-Wert zurückgeben |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | SHA2-Wert zurückgeben |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | Soundex-Code zurückgeben |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | Trennen von Werten in Zeilen |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr), [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | Teilzeichenfolge zurückgeben |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | Gibt eine JSON-Zeichenfolge aus |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | Werte in Zeichenfolge ersetzen |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | Vor- und Nachfolgende Zeichen entfernen |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase), [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | Zeichenfolge in Großbuchstaben ändern |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | Den base64-String in Binärkode konvertieren |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | Konvertieren des Hexadezimalwerts in Binärkode |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | Rückgabe einer UUID |

### Datenevaluierung {#data-evaluation}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | Das erste Argument zurückgeben, das nicht null ist |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | Liste nicht eindeutiger Elemente zurückgeben |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | Ausgeben eines Satzes eindeutiger Elemente |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | Verkettung |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | Verbindung mit Trennzeichen |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | Gibt die Gesamtanzahl der Zeilen aus |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | Dekodieren mit einem Zeichensatz |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | Rückgabe der [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)Eingabe |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | Kodieren mit einem Zeichensatz |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first), [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | Gibt den ersten Wert aus |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | Gibt an, ob eine Spalte gruppiert ist |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | Gibt die Gruppierungsebene aus |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | Gibt einen 1-basierten Index des Vorkommens von Zeichen aus |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | Gibt einen Tupel aus einer JSON-Eingabe zurück |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag), [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | Gibt den Wert vor dem Versatz aus |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last), [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | Gibt den letzten Wert aus |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | Gibt die erste [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) Zeichen |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | Gibt die Länge des Strings aus |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | Gibt den Levenshtein-Abstand zwischen Zeichenfolgen aus |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate), [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | Gibt die Position des ersten Vorkommens einer Teilzeichenfolge aus |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | Landkarte verketten |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | Schlüssel einer Karte zurückgeben |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | Werte einer Zuordnung zurückgeben |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | Zeilen in Partitionen aufteilen |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | Gibt null zurück, wenn true |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | Gibt den Wert aus, wenn null |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | Gibt den Wert aus, wenn nicht null |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | Extrahiert einen Teil einer URL |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | Berechnet den Rang eines Werts |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | Extrahiert etwas, das dem Regex entspricht |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | Ersetzt etwas, das dem Regex entspricht |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | Gibt eine Zeichenfolge zurück, die wiederholt |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | Alle Instanzen einer Zeichenfolge ersetzen |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | Mehrdimensionale Datenaggregation erstellen |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | Weist eine eindeutige Zeilennummer zu |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | Gibt das Schema der JSON-Datei aus |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | Teilt eine Zeichenfolge in ein Array von Wörtern |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | Generiert ein Array von Elementen |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | Signierte bitweise Verschiebung links |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | Signierte bitweise Verschiebung nach rechts |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | Unbedruckte bitweise Verschiebung nach rechts |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | Größe des Arrays zurückgeben |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | Gibt eine Zeichenfolge mit [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) Leerzeichen |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | Aufspaltungszeichenfolge |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | Rückgabeindex der Unterzeichenfolge |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | Fenster |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | Parsen von XML-Knoten |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double), [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | Parsen von XML-Knoten für doppelte |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | Parsen von XML-Knoten für float |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | Parsen von XML-Knoten für Integer |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | Parsen von XML-Knoten für lange |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | XML-Knoten für kurze Ganzzahlen analysieren |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | Parsen von XML-Knoten für Zeichenfolge |

### Aktuelle Informationen {#current-information}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | Gibt die aktuelle Datenbank aus |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | Gibt das aktuelle Datum aus |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp), [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | Gibt den aktuellen Zeitstempel zurück |

### Funktionen für höhere Reihenfolge {#higher-order}

| Funktion | Beschreibung |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | Elemente in einem Array umwandeln |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | Überprüfen, ob Element vorhanden ist |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | Filtern des Eingabe-Arrays |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | Anwenden eines binären Operators auf alle Elemente |
