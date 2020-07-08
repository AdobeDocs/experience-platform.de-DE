---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Array-, Liste- und Set-Funktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 5%

---


# Array-, Liste- und Set-Funktionen

PQL-Angebote (Profil Abfrage Language) erleichtern die Interaktion mit Arrays, Listen und Zeichenfolgen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).

## Mit

Mit der `in` Funktion wird bestimmt, ob ein Element Mitglied eines Arrays oder einer Liste ist.

**Format**

```sql
{VALUE} in {ARRAY}
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen mit Geburtstagen im März, Juni oder September.

```sql
person.birthMonth in [3, 6, 9]
```

## Not in

Mit der `notIn` Funktion wird bestimmt, ob ein Element kein Mitglied eines Arrays oder einer Liste ist.

>[!NOTE]
>
>Die `notIn` Funktion stellt *auch* sicher, dass keiner der Werte null ist. Die Ergebnisse sind daher keine exakte Negation der `in` Funktion.

**Format**

```sql
{VALUE} notIn {ARRAY}
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen mit Geburtstagen, die nicht im März, Juni oder September leben.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersekten

Mit der `intersects` Funktion wird bestimmt, ob zwei Arrays oder Listen mindestens ein gemeinsames Mitglied haben.

**Format**

```sql
{ARRAY}.intersects({ARRAY})
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, deren Lieblingsfarben mindestens eine Farbe Rot, Blau oder Grün enthalten.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Schnittmenge

Die `intersection` Funktion dient zur Bestimmung der gemeinsamen Elemente von zwei Arrays oder Listen.

**Format**

```sql
{ARRAY}.intersection({ARRAY})
```

**Beispiel**

Die folgende PQL-Abfrage definiert, ob die Farben Rot, Blau und Grün von Person 1 und Person 2 jeweils am liebsten sind.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Untergruppe von

Mit der `subsetOf` Funktion wird bestimmt, ob ein bestimmtes Array (Array A) eine Untergruppe eines anderen Arrays (Array B) ist. Anders ausgedrückt, dass alle Elemente im Array A Elemente des Arrays B sind.

**Format**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, die alle ihre Lieblingsstädte besucht haben.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superset

Mit der `supersetOf` Funktion wird bestimmt, ob ein bestimmtes Array (Array A) eine Übermenge eines anderen Arrays (Array B) ist. Mit anderen Worten, dieses Array A enthält alle Elemente im Array B.

**Format**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, die mindestens einmal Sushi und Pizza gegessen haben.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Enthält

Mit der `includes` Funktion wird bestimmt, ob ein Array oder eine Liste ein bestimmtes Element enthält.

**Format**

```sql
{ARRAY}.includes({ITEM})
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, deren Lieblingsfarbe Rot enthält.

```sql
person.favoriteColors.includes("red")
```

## Unterscheiden

Die `distinct` Funktion wird verwendet, um Duplikat-Werte aus einem Array oder einer Liste zu entfernen.

**Format**

```sql
{ARRAY}.distinct()
```

**Beispiel**

Die folgende PQL-Abfrage gibt Personen an, die Bestellungen in mehr als einem Store aufgegeben haben.

```sql
person.orders.storeId.distinct().count() > 1
```

## Gruppe nach

Die `groupBy` Funktion wird verwendet, um die Werte eines Arrays oder einer Liste basierend auf dem Wert des Ausdrucks in eine Gruppe zu unterteilen.

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{ARRAY}` | Das zu gruppierende Array oder die zu gruppierende Liste. |
| `{EXPRESSION}` | Ein Ausdruck, der jedes Element im zurückgegebenen Array oder in der zurückgegebenen Liste zuordnet. |

**Beispiel**

Die folgende PQL-Abfrage gruppiert alle Bestellungen, bei denen die Bestellung gespeichert wurde.

```sql
orders.groupBy(storeId)
```

## Filter

Die `filter` Funktion wird zum Filtern eines Arrays oder einer Liste auf der Grundlage eines Ausdrucks verwendet.

**Format**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{ARRAY}` | Das zu filternde Array oder die zu filternde Liste. |
| `{EXPRESSION}` | Ein Ausdruck, nach dem gefiltert werden soll. |

**Beispiel**

Die folgende PQL-Abfrage definiert alle Personen ab 21 Jahren.

```sql
person.filter(age >= 21)
```

## Landkarte

Die `map` Funktion wird verwendet, um ein neues Array zu erstellen, indem auf jedes Element in einem Array ein Ausdruck angewendet wird.

**Format**

```sql
array.map(expression)
```

**Beispiel**

Mit der folgenden PQL-Abfrage wird ein neues Zahlenarray erstellt und der Wert der Originalzahlen quadriert.

```sql
numbers.map(square)
```

## Erste `n` im Array

Die `topN` Funktion gibt die ersten `N` Elemente in einem Array zurück, wenn sie in aufsteigender Reihenfolge nach dem angegebenen numerischen Ausdruck sortiert werden.

**Format**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{ARRAY}` | Das zu sortierende Array oder die zu sortierende Liste. |
| `{VALUE}` | Die Eigenschaft, in der das Array oder die Liste sortiert werden soll. |
| `{AMOUNT}` | Die Anzahl der zurückzugebenden Elemente. |

**Beispiel**

Die folgende PQL-Abfrage gibt die fünf wichtigsten Bestellungen mit dem höchsten Preis zurück.

```sql
orders.topN(price, 5)
```

## Letzte `n` im Array

Die `bottomN` Funktion gibt die letzten `N` Elemente in einem Array zurück, wenn sie in aufsteigender Reihenfolge nach dem angegebenen numerischen Ausdruck sortiert werden.

**Format**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argument | Beschreibung |
| --------- | ----------- | 
| `{ARRAY}` | Das zu sortierende Array oder die zu sortierende Liste. |
| `{VALUE}` | Die Eigenschaft, in der das Array oder die Liste sortiert werden soll. |
| `{AMOUNT}` | Die Anzahl der zurückzugebenden Elemente. |

**Beispiel**

Die folgende PQL-Abfrage gibt die fünf wichtigsten Bestellungen mit dem niedrigsten Preis zurück.

```sql
orders.bottomN(price, 5)
```

## Erster Posten

Mit der `head` Funktion wird das erste Element im Array oder in der Liste zurückgegeben.

**Format**

```sql
{ARRAY}.head()
```

**Beispiel**

Die folgende PQL-Abfrage gibt die erste der fünf Top-Bestellungen mit dem höchsten Preis zurück. Weitere Informationen zur `topN` Funktion finden Sie im [ersten Abschnitt `n` im Array](#first-n-in-array) .

```sql
orders.topN(price, 5).head()
```

## Nächste Schritte

Nachdem Sie nun Informationen zu Array-, Liste- und Set-Funktionen erhalten haben, können Sie diese in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).
