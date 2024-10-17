---
solution: Experience Platform
title: Array-, List- und Set PQL Functions
description: Profile Query Language (PQL) bietet Funktionen, die die Interaktion mit Arrays, Listen und Zeichenfolgen vereinfachen.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 57%

---

# Funktionen für Arrays, Listen und Sets

[!DNL Profile Query Language] (PQL) bietet Funktionen, die die Interaktion mit Arrays, Listen und Zeichenfolgen vereinfachen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md) .

## Enthalten

Mit der Funktion `in` wird bestimmt, ob ein Element einem Array oder einer Liste als boolescher Wert angehört.

**Format**

```sql
{VALUE} in {ARRAY}
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, die im März, Juni oder September Geburtstag haben.

```sql
person.birthMonth in [3, 6, 9]
```

## Nicht enthalten

Mit der Funktion `notIn` wird bestimmt, ob ein Element nicht Mitglied eines Arrays oder einer Liste als boolescher Wert ist.

>[!NOTE]
>
> Die `notIn`-Funktion stellt *außerdem* sicher, dass keiner der Werte null ist. Daher sind die Ergebnisse keine exakte Negation der `in`-Funktion.

**Format**

```sql
{VALUE} notIn {ARRAY}
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, die nicht im März, Juni oder September Geburtstag haben.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Schnittmengen

Mit der Funktion `intersects` wird bestimmt, ob zwei Arrays oder Listen mindestens ein gemeinsames Element als boolescher Wert aufweisen.

**Format**

```sql
{ARRAY}.intersects({ARRAY})
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, deren Lieblingsfarben mindestens eine der folgenden Farben beinhalten: Rot, Blau oder Grün.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Schnittmenge

Mit der Funktion `intersection` werden die gemeinsamen Elemente von zwei Arrays oder Listen als Liste bestimmt.

**Format**

```sql
{ARRAY}.intersection({ARRAY})
```

**Beispiel**

Die folgende PQL-Abfrage definiert, ob unter den Lieblingsfarben von Person 1 und auch Person 2 die Farben Rot, Blau und Grün sind.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Teilmenge von

Mit der `subsetOf`-Funktion wird bestimmt, ob ein bestimmtes Array (Array A) eine Teilmenge eines anderen Arrays (Array B) ist. Mit anderen Worten, dass alle Elemente in Array A Elemente von Array B als boolescher Wert sind.

**Format**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, die alle ihrer Lieblingsstädte besucht haben.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Obermenge

Mit der `supersetOf`-Funktion wird bestimmt, ob ein bestimmtes Array (Array A) eine Obermenge eines anderen Arrays (Array B) ist. Mit anderen Worten, dieses Array A enthält alle Elemente in Array B als booleschen Wert.

**Format**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, die mindestens einmal Sushi und mindestens einmal Pizza gegessen haben.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Enthält

Mit der Funktion `includes` wird bestimmt, ob ein Array oder eine Liste ein bestimmtes Element als boolescher Wert enthält.

**Format**

```sql
{ARRAY}.includes({ITEM})
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, zu deren Lieblingsfarben Rot gehört.

```sql
person.favoriteColors.includes("red")
```

## Verschieden

Mit der Funktion `distinct` werden doppelte Werte aus einem Array oder einer Liste als Array entfernt.

**Format**

```sql
{ARRAY}.distinct()
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, die Bestellungen in mehr als einem Geschäft aufgegeben haben.

```sql
person.orders.storeId.distinct().count() > 1
```

## Gruppieren nach

Die Funktion `groupBy` wird verwendet, um Werte eines Arrays oder einer Liste basierend auf dem Wert des Ausdrucks als Zuordnung von eindeutigen Werten des Gruppierungsausdrucks zu Arrays zu unterteilen, die Partitionen des Werts des Array-Ausdrucks sind.

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{ARRAY}` | Das zu gruppierende Array oder die zu gruppierende Liste. |
| `{EXPRESSION}` | Ein Ausdruck, der jedes Element im zurückgegebenen Array oder in der zurückgegebenen Liste zuordnet. |

**Beispiel**

Die folgende PQL-Abfrage gruppiert alle Bestellungen anhand des Geschäfts, in dem die Bestellung aufgegeben wurde.

```sql
xEvent[type="order"].groupBy(storeId)
```

## Filter

Die Funktion `filter` wird zum Filtern eines Arrays oder einer Liste anhand eines Ausdrucks als Array oder Liste verwendet, je nach Eingabe.

**Format**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{ARRAY}` | Das zu filternde Array oder die zu filternde Liste. |
| `{EXPRESSION}` | Ein Ausdruck, nach dem gefiltert werden soll. |

**Beispiel**

Die folgende PQL-Abfrage definiert alle Personen, die mindestens 21 Jahre alt sind.

```sql
person.filter(age >= 21)
```

## Zuordnung

Mit der Funktion `map` wird ein neues Array erstellt, indem ein Ausdruck auf jedes Element in einem Array als Array angewendet wird.

**Format**

```sql
array.map(expression)
```

**Beispiel**

Mit der folgenden PQL-Abfrage wird ein neues Array mit Zahlen erstellt und der Wert der Originalzahlen quadriert.

```sql
numbers.map(square)
```

## Erste `n` in Array {#first-n}

Die Funktion `topN` gibt die ersten `N` Elemente in einem Array zurück, wenn sie anhand des angegebenen numerischen Ausdrucks in aufsteigender Reihenfolge als Array sortiert werden.

**Format**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{ARRAY}` | Das zu sortierende Array oder die zu sortierende Liste. |
| `{VALUE}` | Die Eigenschaft, in der das Array oder die Liste sortiert werden soll. |
| `{AMOUNT}` | Die Zahl der zurückzugebenden Elemente. |

**Beispiel**

Die folgende PQL-Abfrage gibt die fünf häufigsten Bestellungen mit dem höchsten Preis zurück.

```sql
orders.topN(price, 5)
```

## Letzte `n` in Array

Die Funktion `bottomN` gibt die letzten `N` Elemente in einem Array zurück, wenn sie anhand des angegebenen numerischen Ausdrucks in aufsteigender Reihenfolge als Array sortiert werden.

**Format**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argument | Beschreibung |
| --------- | ----------- | 
| `{ARRAY}` | Das zu sortierende Array oder die zu sortierende Liste. |
| `{VALUE}` | Die Eigenschaft, in der das Array oder die Liste sortiert werden soll. |
| `{AMOUNT}` | Die Zahl der zurückzugebenden Elemente. |

**Beispiel**

Die folgende PQL-Abfrage gibt die fünf häufigsten Bestellungen mit dem niedrigsten Preis zurück.

```sql
orders.bottomN(price, 5)
```

## Erstes Element

Mit der Funktion `head` wird das erste Element im Array oder in der Liste als Objekt zurückgegeben.

**Format**

```sql
{ARRAY}.head()
```

**Beispiel**

Die folgende PQL-Abfrage gibt die erste der fünf häufigsten Bestellungen mit dem höchsten Preis zurück. Weiterführende Informationen zur `topN`-Funktion finden Sie im Abschnitt [Erste `n` in Array](#first-n).

```sql
orders.topN(price, 5).head()
```

## Nächste Schritte

Nachdem Sie sich mit array-, list- und set-Funktionen vertraut gemacht haben, können Sie diese nun in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
