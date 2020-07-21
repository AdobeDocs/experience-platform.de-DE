---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Arithmetische Funktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 94%

---


# Arithmetische Funktionen

Arithmetic functions are used to perform basic calculations on values in [!DNL Profile Query Language] (PQL). Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Profile Query Language-Übersicht](./overview.md).

## Addieren

Mit der Funktion `+` (Addition) wird die Summe zweier Argumentausdrücke ermittelt.

**Format**

```sql
{NUMBER} + {NUMBER}
```

**Beispiel**

Die folgende PQL-Abfrage addiert die Preise von zwei verschiedenen Produkten.

```sql
product1.price + product2.price
```

## Multiplizieren

Mit der Funktion `*` (Multiplikation) wird das Produkt zweier Argumentausdrücke ermittelt.

**Format**

```sql
{NUMBER} * {NUMBER}
```

**Beispiel**

Die folgende PQL-Abfrage ermittelt das Produkt im Bestand sowie den Preis eines Produkts, um den Bruttowert des Produkts zu berechnen.

```sql
product.inventory * product.price
```

## Subtrahieren

Mit der Funktion `-` (Subtraktion) wird der Unterschied zwischen zwei Argumentausdrücken ermittelt.

**Format**

```sql
{NUMBER} - {NUMBER}
```

**Beispiel**

Die folgende PQL-Abfrage ermittelt den Preisunterschied zwischen zwei verschiedenen Produkten.

```sql
product1.price - product2.price
```

## Teilen

Mit der Funktion `/` (Division) wird der Quotient zweier Argumentausdrücke ermittelt.

**Format**

```sql
{NUMBER} / {NUMBER}
```

**Beispiel**

Die folgende PQL-Abfrage ermittelt den Quotienten zwischen den insgesamt verkauften Produkten und dem insgesamt verdienten Geld, um so die durchschnittlichen Kosten pro Artikel zu berechnen.

```sql
totalProduct.price / totalProduct.sold
```

## Rest

Mit der Funktion `%` (Modulo/Rest) wird nach der Division der beiden Argumentausdrücke der Rest ermittelt.

**Format**

```sql
{NUMBER} % {NUMBER}
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob das Alter der Person durch fünf teilbar ist.

```sql
person.age % 5 = 0
```

## Nächste Schritte

Nachdem Sie sich mit arithmetischen Funktionen vertraut gemacht haben, können Sie sie nun in Ihren PQL-Abfragen verwenden. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Profile Query Language-Übersicht](./overview.md).
