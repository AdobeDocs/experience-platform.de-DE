---
title: Verwalten von Array- und Zuordnungstypen mit Funktionen höherer Ordnung
description: Erfahren Sie, wie Sie im Abfrage-Service Array- und Zuordnungstypen mit Funktionen höherer Ordnung verwalten. Beispiele werden mit häufigen Anwendungsfällen bereitgestellt.
exl-id: dec4e4f6-ad6b-4482-ae8c-f10cc939a634
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 1%

---

# Verwalten von Array- und Zuordnungstypen mit Funktionen höherer Ordnung

Verwenden Sie dieses Handbuch, um zu erfahren, wie Funktionen höherer Ordnung komplexe Datentypen, wie Arrays und Zuordnungen, verarbeiten können. Diese Funktionen entfernen die Notwendigkeit, das Array aufzulösen, eine Funktion auszuführen und dann das Ergebnis zu kombinieren. Funktionen höherer Ordnung sind besonders nützlich für die Analyse oder Verarbeitung von Zeitreihendaten und Analysen, die häufig komplexe verschachtelte Strukturen, Arrays, Karten und verschiedene Anwendungsfälle aufweisen.

Die folgende Liste von Anwendungsfällen enthält Beispiele für Array- und Zuordnungsmanipulationsfunktionen höherer Ordnung.

## Verwenden Sie die Transformation , um den Gesamtpreis um n anzupassen. {#adjust-price-total}

`transform(array<T>, function<T, U>): array<U>`

Der obige Ausschnitt wendet eine Funktion auf jedes Element des Arrays an und gibt ein neues Array von umgewandelten Elementen zurück. Die Funktion `transform` verwendet ein Array vom Typ T und konvertiert jedes Element vom Typ T in den Typ U. Anschließend wird ein Array vom Typ „U“ zurückgegeben. Die tatsächlichen Typen T und U hängen von der spezifischen Verwendung der Transformationsfunktion ab.

`transform(array<T>, function<T, Int, U>): array<U>`

Diese Array-Umwandlungsfunktion ähnelt dem vorherigen Beispiel, es gibt jedoch zwei Argumente für die Funktion. Das zweite Argument in dieser Funktion empfängt neben der Transformation auch den Index des Elements im Array.

**Beispiel**

Das folgende SQL-Beispiel zeigt diesen Anwendungsfall. Die Abfrage ruft einen begrenzten Satz von Zeilen aus der angegebenen Tabelle ab und transformiert das `productListItems`-Array, indem das `priceTotal`-Attribut jedes Elements mit 73 multipliziert wird. Das Ergebnis umfasst die Spalten `_id`, `productListItems` und umgewandelte `price_in_inr`. Die Auswahl basiert auf einem bestimmten Zeitstempelbereich.

```sql
SELECT _id,
       productListItems,
       Transform(productListItems, value -> value.priceTotal * 73) AS
       price_in_inr
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
 productListItems | price_in_inr
|-------------------+----------------
(8376, NULL, NULL) | 611448.0
{(Burbank Hills Jeans, NULL, NULL), (Thermomax Steel, NULL, NULL), (Bruin Point Shearling Boots, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL), (Timberline Survival Knife, NULL, NULL), (Thermomax Steel, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Lost Prospector Beanie, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL)} | {0.0,0.0.0.0,0,0,0,0,0,0,0,0,0,0,0,0,0.0}
(84763,NULL, NULL) | 6187699.0
(843765, NULL, NULL) | 6.1594845E7
(199684, NULL, NULL) | 1.4576932E7

(10 rows)
```

## Verwenden Sie Exists , um herauszufinden, ob ein Produkt mit einer bestimmten SKU vorhanden ist. {#confirm-product-exists}

`exists(array<T>, function<T, boolean>): boolean`

Im obigen Ausschnitt wird die Funktion `exists` auf jedes Element des Arrays angewendet und gibt einen booleschen Wert zurück. Der boolesche Wert gibt an, ob das Array ein oder mehrere Elemente enthält, die eine bestimmte Bedingung erfüllen. In diesem Fall wird bestätigt, ob ein Produkt mit einer bestimmten SKU vorhanden ist.

**Beispiel**

Im folgenden SQL-Beispiel ruft die Abfrage `productListItems` aus der `geometrixxx_999_xdm_pqs_1batch_10k_rows` ab und bewertet, ob ein Element mit einer SKU gleich `123679` im `productListItems`-Array vorhanden ist. Anschließend werden die Ergebnisse anhand eines bestimmten Zeitstempelbereichs gefiltert und die endgültigen Ergebnisse auf zehn Zeilen begrenzt.

```sql
SELECT productListItems
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE EXISTS( productListItems, value -> value.sku == 123679)
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')limit 10;
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
productListItems
|-----------------
{(123679, NULL,NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL,NULL)}
{(123679,NULL, NULL)}

(10 rows)
```

## Verwenden Sie den Filter, um Produkte zu finden, bei denen die SKU > 100000 {#find-specific-products}

`filter(array<T>, function<T, boolean>): array<T>`

Diese Funktion filtert ein Array von Elementen basierend auf einer bestimmten Bedingung, die jedes Element als booleschen Wert auswertet. Anschließend wird ein neues -Array zurückgegeben, das nur Elemente enthält, bei denen die Bedingung einen Wert „true“ zurückgegeben hat.

**Beispiel**

Die nachstehende Abfrage wählt die Spalte `productListItems` aus, wendet einen Filter an, um nur Elemente mit einer SKU von mehr als 100000 einzuschließen, und beschränkt den Ergebnissatz auf Zeilen innerhalb eines bestimmten Zeitstempelbereichs. Das gefilterte Array wird dann in der Ausgabe als Alias `_filter`.

```sql
SELECT productListItems,
    Filter(productListItems, value -> value.sku > 100000) AS _filter
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
productListItems | _filter
|-----------------+---------
(123679, NULL, NULL) (123679, NULL, NULL)
(1346, NULL, NULL) |
(98347, NULL, NULL) |
(176015, NULL, NULL) | (176015, NULL, NULL)

(10 rows)
```

## Verwenden Sie Aggregat , um die SKUs aller Produktlistenelemente zu summieren, die mit einer bestimmten ID verknüpft sind, und verdoppeln Sie die resultierende Summe. {#sum-specific-skus-and-double-the-resulting-total}

`aggregate(array<T>, A, function<A, T, A>[, function<A, R>]): R`

Dieser Aggregatvorgang wendet einen binären Operator auf einen Anfangszustand und alle Elemente im Array an. Außerdem werden mehrere Werte auf einen einzelnen Status reduziert. Nach dieser Reduktion wird dann der Endzustand mithilfe einer Finish-Funktion in das Endergebnis umgewandelt. Die Finish-Funktion nimmt den letzten Status an, der nach dem Anwenden des binären Operators auf alle Array-Elemente erhalten wurde, und macht etwas mit ihr, um das Endergebnis zu erzeugen.

**Beispiel**

Dieses Abfragebeispiel berechnet den maximalen SKU-Wert aus dem `productListItems`-Array innerhalb des angegebenen Zeitstempelbereichs und verdoppelt das Ergebnis. Die Ausgabe enthält das ursprüngliche `productListItems`-Array und die berechnete `max_value`.

```sql
SELECT productListItems,
aggregate(productListItems, 0, (acc, value) ->
case
WHEN (
value.sku > acc) THEN cast(value.sku AS int)
ELSE cast(acc AS int)
END, acc -> acc * 2) AS max_value
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 50;
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
productListItems | max_value
|-----------------+---------
(123679, NULL, NULL) | 247358
(1346,NULL, NULL) | 2692
(98347, NULL, NULL) | 196694
(176015, NULL, NULL) | 352030

(10 rows)
```

## Verwenden Sie zip_with , um allen Elementen in der Produktliste eine Sequenznummer zuzuweisen {#assign-a-sequence-number}

`zip_with(array<T>, array<U>, function<T, U, R>): array<R>`

Dieses Snippet kombiniert die Elemente zweier Arrays zu einem einzigen neuen Array. Der Vorgang wird unabhängig für jedes Element des Arrays ausgeführt und erzeugt Wertpaare. Wenn ein Array kürzer ist, werden Null-Werte hinzugefügt, um die Länge des längeren Arrays zu berücksichtigen. Dies geschieht, bevor die Funktion angewendet wird.

**Beispiel**

Die folgende Abfrage verwendet die `zip_with`-Funktion, um Wertpaare aus zwei Arrays zu erstellen. Dies erfolgt durch Hinzufügen der SKU-Werte aus dem `productListItems`-Array zu einer ganzzahligen Sequenz, die mithilfe der `Sequence`-Funktion generiert wurde. Das Ergebnis wird neben der ursprünglichen `productListItems`-Spalte ausgewählt und ist auf der Grundlage eines Zeitstempelbereichs begrenzt.

```sql
SELECT productListItems,
zip_with(Sequence(1,5), Transform(productListItems, p -> p.sku), (x,y) -> struct(x, y)) AS zip_with
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
productListItems     | zip_with
|---------------------+---------
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(123679, NULL, NULL) | {(1,123679), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3, NULL),(4,NULL), (5,NULL)}
(1346,NULL, NULL)    | {(1,1346), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(98347, NULL, NULL)  | {(1,98347), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
(176015, NULL, NULL) | {(1,176015),(2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}

(10 rows)
```

## Verwenden Sie map_from_entries, um jedem Element in der Produktliste eine Sequenznummer zuzuweisen und das Endergebnis als Zuordnung zu erhalten {#assign-a-sequence-number-return-result-as-map}

`map_from_entries(array<struct<K, V>>): map<K, V>`

Dieses Snippet konvertiert ein Array von Schlüssel-Wert-Paaren in eine Zuordnung. Dies ist nützlich, wenn es um Daten mit Schlüssel-Wert-Paaren geht, die von einer besser organisierten und effizienteren Struktur profitieren könnten.

**Beispiel**

Die folgende Abfrage erstellt Wertpaare aus einer Sequenz und dem productListItems-Array, wandelt diese Paare mithilfe von map_from_entries in eine Zuordnung um und wählt dann die ursprüngliche productListItems-Spalte zusammen mit der neu erstellten map_from_entries-Spalte aus. Das Ergebnis wird basierend auf dem angegebenen Zeitstempelbereich gefiltert und eingeschränkt.

```sql
SELECT productListItems,      map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))) AS map_from_entries
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > to_timestamp('2017-11-01 00:00:00')
AND    timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
productListItems     | map_from_entries
|---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Verwenden Sie map_form_arrays , um Elementen in der Produktliste Sequenznummern zuzuweisen und das Ergebnis als Zuordnung zurückzugeben {#assign-sequence-numbers-to-items-return-the-result-as-a-map}

`map_form_arrays(array<K>, array<V>): map<K, V>`

Die `map_form_arrays`-Funktion erstellt eine Zuordnung mit paarweisen Werten aus zwei Arrays.

>[!IMPORTANT]
>
>Die Schlüssel dürfen keine Null-Elemente enthalten.

**Beispiel**

Der folgende SQL-Code erstellt eine Zuordnung, bei der die Schlüssel aus sequenziellen Zahlen bestehen, die mithilfe der `Sequence`-Funktion generiert wurden, und bei der die Werte Elemente aus dem `productListItems`-Array sind. Die Abfrage wählt die Spalte `productListItems` aus und verwendet die Funktion `Map_from_arrays` , um die Zuordnung basierend auf der generierten Zahlensequenz und den Elementen des Arrays zu erstellen. Das Ergebnis ist auf zehn Zeilen beschränkt und basierend auf einem Zeitstempelbereich gefiltert.

```sql
SELECT productListItems,
       Map_from_arrays(Sequence(1, Size(productListItems)), productListItems) AS
       map_from_arrays
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  Size(productListItems) > 0
       AND timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
productListItems     | map_from_entries
|---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Verwenden Sie map_concat , um zwei Karten als einzelne Zuordnung zu verketten. {#concatenate-two-maps-into-as-single-map}

`map_concat(map<K, V>, ...): map<K, V>`

Die `map_concat` Funktion im obigen Ausschnitt nimmt mehrere Zuordnungen als Argumente und gibt eine neue Zuordnung zurück, die alle Schlüssel-Wert-Paare aus den Eingabe-Zuordnungen kombiniert. Die Funktion verkettet mehrere Zuordnungen zu einer einzigen Zuordnung, und die resultierende Zuordnung enthält alle Schlüssel-Wert-Paare aus den Eingabezuordnungen.

**Beispiel**

Die folgende SQL-Anweisung erstellt eine Zuordnung, bei der jedes Element in `productListItems` mit einer Sequenznummer verknüpft ist, die dann mit einer anderen Zuordnung verkettet wird, bei der Schlüssel in einem bestimmten Sequenzbereich generiert werden.

```sql
SELECT productListItems,
      map_concat(           
         map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))),
         map_from_arrays(sequence(size(productListItems) + 1, size(productListItems) + size(productListItems)), productListItems) )
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE size(productListItems) > 0
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
productListItems     | map_from_entries
|---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)",2 -> "(123679, NULL, NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)",2 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)",2 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)",2 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)",2 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)",2 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)",2 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)",2 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Verwenden Sie element_at, um einen Wert abzurufen, der &#39;AAID&#39; in der Identitätszuordnung entspricht, um weitere Berechnungen durchzuführen {#retrieve-a-corresponding-value}

`element_at(array<T>, Int): T / element_at(map<K, V>, K): V`

Bei Arrays gibt der Ausschnitt das Element mit einem angegebenen (1-basierten) Index oder den Wert zurück, der mit einem Schlüssel in einer Zuordnung verknüpft ist. Wenn der Index &lt; 0 ist, greift er auf Elemente vom letzten zum ersten zu und gibt null zurück, wenn der Index die Länge des Arrays überschreitet.

Bei Zuordnungen wird entweder ein Wert für den angegebenen Schlüssel oder null zurückgegeben, wenn der Schlüssel nicht in der Zuordnung enthalten ist.

**Beispiel**

Die Abfrage wählt die Spalte `identitymap` aus der `geometrixxx_999_xdm_pqs_1batch_10k_rows` aus und extrahiert den Wert, der mit dem `AAID` für jede Zeile verknüpft ist. Die Ergebnisse sind auf Zeilen beschränkt, die innerhalb des angegebenen Zeitstempelbereichs liegen, und die Abfrage beschränkt die Ausgabe auf zehn Zeilen.

```sql
SELECT identitymap,
              Element_at(identitymap, 'AAID')
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
                                                                  identitymap                                            |  element_at(identitymap, AAID) 
|-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            | (3617FBB942466D79-5433F727AD6A0AD, false) 
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] | (533F56A682C059B1-396437F68879F61D, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             | (6A60527B9D66CCB9-29638A632B45E9, false) 
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           | (64FB4DC317E21B59-2A23602D234647E7, false) 
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           | (2E70E8CF6DB1DE86-270E55BBBA58B9C1, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           | (1CFB3297C3146F2F-28D6902A610BA3B1, false) 
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           | (533F56A682C059B1-396437F68879F61D, false) 
(10 rows)
```

## Verwenden der Kardinalität, um die Anzahl der Identitäten in der Identitätszuordnung zu finden {#find-the-number-of-identities-in-the-identity-map}

`cardinality(array<T>): Int / cardinality(map<K, V>): Int`

Dieses Snippet gibt die Größe eines bestimmten Arrays oder einer bestimmten Zuordnung zurück und stellt einen Alias bereit. Gibt -1 zurück, wenn der Wert null ist.

**Beispiel**

Die nachstehende Abfrage ruft die Spalte `identitymap` ab, und die Funktion `Cardinality` berechnet die Anzahl der Elemente in jeder Zuordnung innerhalb der `identitymap`. Die Ergebnisse sind auf zehn Zeilen beschränkt und werden anhand eines angegebenen Zeitstempelbereichs gefiltert.

```sql
SELECT identitymap,
       Cardinality(identitymap)
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
                                                                  identitymap                                            |  size(identitymap) 
|-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            |      2  
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             |      2  
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           |      2  
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           |      2  
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           |      2  
(10 rows)
```

## Verwenden Sie array_distinct, um die einzelnen Elemente in productListItems zu finden. {#find-distinct-elements}

`array_distinct(array<T>): array<T>`

Der obige Ausschnitt entfernt doppelte Werte aus dem angegebenen Array.

**Beispiel**

Die nachstehende Abfrage wählt die Spalte `productListItems` aus, entfernt alle doppelten Elemente aus den Arrays und beschränkt die Ausgabe auf zehn Zeilen basierend auf einem angegebenen Zeitstempelbereich.

```sql
SELECT productListItems,
              Array_distinct(productListItems)
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Ergebnis**

Die Ergebnisse für diese SQL-Abfrage ähneln denen unten.

```console
productListItems     | array_distinct(productListItems)
|---------------------+---------------------------------
                     |
(123679, NULL, NULL) | (123679, NULL, NULL)
                     |
                     |
(1346,NULL, NULL)    | (1346,NULL, NULL)
                     |
(98347, NULL, NULL)  | (98347, NULL, NULL)
                     |
(176015, NULL, NULL) | (176015, NULL, NULL)
                     |

(10 rows)
```

### Zusätzliche Funktionen höherer Ordnung {#additional-higher-order-functions}

Die folgenden Beispiele für Funktionen höherer Ordnung werden im Rahmen des Anwendungsfalls zum Abrufen ähnlicher Datensätze erläutert. Ein Beispiel und eine Erläuterung der Verwendung jeder Funktion finden Sie im entsprechenden Abschnitt dieses Dokuments.

Das [`transform` Beispiel &#x200B;](../use-cases/retrieve-similar-records.md#length-adjustment) die Tokenisierung einer Produktliste.

Das Beispiel der [`filter`-Funktion &#x200B;](../use-cases/retrieve-similar-records.md#filter-results) eine verfeinerte und präzisere Extraktion relevanter Informationen aus Textdaten.

Die [`reduce` Funktion &#x200B;](../use-cases/retrieve-similar-records.md#higher-order-function-solutions) die Ableitung von kumulierten Werten oder Aggregaten, die in verschiedenen Analyse- und Planungsprozessen von zentraler Bedeutung sein können.
