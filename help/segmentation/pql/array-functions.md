---
solution: Experience Platform
title: Array-, List- und Set PQL-Funktionen
description: Profile Query Language (PQL) bietet Funktionen, die die Interaktion mit Arrays, Listen und Zeichenfolgen erleichtern.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 97%

---

# Funktionen für Arrays, Listen und Sets

[!DNL Profile Query Language] (PQL) bietet Funktionen, die die Interaktion mit Arrays, Listen und Zeichenfolgen erleichtern. Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] Übersicht](./overview.md).

## Enthalten

Mit der `in`-Funktion wird bestimmt, ob ein Element einem Array oder einer Liste angehört.

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

Mit der `notIn`-Funktion wird bestimmt, ob ein Element einem Array oder einer Liste nicht angehört.

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

Mit der `intersects`-Funktion wird bestimmt, ob zwei Arrays oder Listen mindestens ein gemeinsames Element aufweisen.

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

Die `intersection`-Funktion dient zur Bestimmung der gemeinsamen Elemente von zwei Arrays oder Listen.

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

Mit der `subsetOf`-Funktion wird bestimmt, ob ein bestimmtes Array (Array A) eine Teilmenge eines anderen Arrays (Array B) ist. Mit anderen Worten: ob alle Elemente in Array A Elemente von Array B sind.

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

Mit der `supersetOf`-Funktion wird bestimmt, ob ein bestimmtes Array (Array A) eine Obermenge eines anderen Arrays (Array B) ist. Mit anderen Worten: ob Array A alle Elemente in Array B enthält.

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

Mit der `includes`-Funktion wird bestimmt, ob ein Array oder eine Liste ein bestimmtes Element enthält.

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

Die `distinct`-Funktion dient dazu, doppelt vorhandene Werte aus einem Array oder einer Liste zu entfernen.

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

Die `groupBy`-Funktion dient dazu, Werte eines Arrays oder einer Liste basierend auf dem Wert des Ausdrucks in eine Gruppe zu unterteilen.

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{ARRAY}` | Das zu gruppierende Array oder die zu gruppierende Liste. |
| `{EXPRESSION}` | Ein Ausdruck, der jedes Element im zurückgegebenen Array oder in der zurückgegebenen Liste zuordnet. |

**Beispiel**

Die folgende PQL-Abfrage gruppiert alle Bestellungen anhand des Geschäfts, in dem die Bestellung aufgegeben wurde.

```sql
orders.groupBy(storeId)
```

## Filter

Die `filter`-Funktion wird zum Filtern eines Arrays oder einer Liste anhand eines Ausdrucks verwendet.

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

Die `map`-Funktion wird zum Erstellen eines neuen Arrays verwendet, indem auf jedes Element in einem Array ein Ausdruck angewendet wird.

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

Die `topN`-Funktion gibt die ersten `N` Elemente in einem Array zurück, wenn sie anhand des angegebenen numerischen Ausdrucks in aufsteigender Reihenfolge sortiert werden.

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

Die `bottomN`-Funktion gibt die letzten `N` Elemente in einem Array zurück, wenn sie anhand des angegebenen numerischen Ausdrucks in aufsteigender Reihenfolge sortiert werden.

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

Mit der `head`-Funktion wird das erste Element im Array oder in der Liste zurückgegeben.

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
