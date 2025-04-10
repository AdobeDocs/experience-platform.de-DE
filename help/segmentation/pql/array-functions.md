---
solution: Experience Platform
title: Funktionen für Arrays, Listen und Sets in PQL
description: Profile Query Language (PQL) bietet Funktionen, die die Interaktion mit Arrays, Listen und Zeichenfolgen erleichtern.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 57%

---

# Funktionen für Arrays, Listen und Sets

[!DNL Profile Query Language] (PQL) bietet Funktionen, die die Interaktion mit Arrays, Listen und Zeichenfolgen erleichtern. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md).

## Enthalten

Mit der Funktion `in` wird bestimmt, ob ein Element als boolescher Wert Mitglied eines Arrays oder einer Liste ist.

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

Mit der Funktion `notIn` wird bestimmt, ob ein Element nicht als boolescher Wert Mitglied eines Arrays oder einer Liste ist.

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

Mit der Funktion `intersects` wird bestimmt, ob zwei Arrays oder Listen mindestens einen gemeinsamen Member als booleschen Wert aufweisen.

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

Mit der Funktion `intersection` werden die gemeinsamen Elemente zweier Arrays oder Listen als Liste bestimmt.

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

Mit der `subsetOf`-Funktion wird bestimmt, ob ein bestimmtes Array (Array A) eine Teilmenge eines anderen Arrays (Array B) ist. Mit anderen Worten, alle Elemente in Array A sind Elemente von Array B als boolescher Wert.

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

Mit der `supersetOf`-Funktion wird bestimmt, ob ein bestimmtes Array (Array A) eine Obermenge eines anderen Arrays (Array B) ist. Mit anderen Worten: Array A enthält alle Elemente in Array B als Boolescher Wert.

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

Mit der Funktion `includes` wird bestimmt, ob ein Array oder eine Liste ein bestimmtes Element als boolesch enthält.

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

Die Funktion `distinct` wird verwendet, um doppelte Werte aus einem Array oder einer Liste als Array zu entfernen.

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

Die Funktion `groupBy` wird verwendet, um Werte eines Arrays oder einer Liste basierend auf dem Wert des Ausdrucks als Zuordnung von eindeutigen Werten des Gruppierungsausdrucks zu Arrays, die Partitionen des Werts des Array-Ausdrucks sind, in eine Gruppe zu unterteilen.

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

Die Funktion `filter` wird verwendet, um ein Array oder eine Liste je nach Eingabe auf der Grundlage eines Ausdrucks als Array oder Liste zu filtern.

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

Die Funktion `map` wird verwendet, um ein neues Array zu erstellen, indem ein Ausdruck als Array auf jedes Element in einem bestimmten Array angewendet wird.

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

Die Funktion `topN` wird verwendet, um die ersten `N` Elemente in einem Array zurückzugeben, wenn sie in aufsteigender Reihenfolge auf der Grundlage des angegebenen numerischen Ausdrucks als Array sortiert werden.

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

Die Funktion `bottomN` wird verwendet, um die letzten `N` Elemente in einem Array zurückzugeben, wenn sie in aufsteigender Reihenfolge auf der Grundlage des angegebenen numerischen Ausdrucks als Array sortiert werden.

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

Die Funktion `head` wird verwendet, um das erste Element im Array oder der Liste als -Objekt zurückzugeben.

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
