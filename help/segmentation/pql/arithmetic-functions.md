---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Arithmetik-Funktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 5%

---


# Arithmetik-Funktionen

Arithmetische Funktionen werden verwendet, um Basisberechnungen für Profil Abfrage Language (PQL) durchzuführen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).

## Neue

Die `+` (Addition)-Funktion wird verwendet, um die Summe von zwei Argument-Ausdrücken zu finden.

**Format**

```sql
{NUMBER} + {NUMBER}
```

**Beispiel**

Die folgende PQL-Abfrage fasst den Preis von zwei verschiedenen Produkten zusammen.

```sql
product1.price + product2.price
```

## Multiplizieren

Die `*` (Multiplikations-)Funktion wird verwendet, um das Produkt zweier Argument-Ausdruck zu finden.

**Format**

```sql
{NUMBER} * {NUMBER}
```

**Beispiel**

Die folgende PQL-Abfrage findet das Produkt des Bestandes und den Produktpreis, um den Bruttowert des Produkts zu ermitteln.

```sql
product.inventory * product.price
```

## Subtrahieren

Die `-` (Subtraktion-)Funktion wird verwendet, um den Unterschied von zwei Argument-Ausdrücken zu ermitteln.

**Format**

```sql
{NUMBER} - {NUMBER}
```

**Beispiel**

Die folgende PQL-Abfrage ermittelt den Preisunterschied zwischen zwei verschiedenen Produkten.

```sql
product1.price - product2.price
```

## Teilung

Die Funktion `/` (Division) wird verwendet, um den Quotienten zweier Argument-Ausdruck zu finden.

**Format**

```sql
{NUMBER} / {NUMBER}
```

**Beispiel**

Die folgende PQL-Abfrage findet den Quotienten zwischen den insgesamt verkauften Produkten und dem gesamten verdienten Geld, um die durchschnittlichen Kosten pro Artikel zu sehen.

```sql
totalProduct.price / totalProduct.sold
```

## Remainer

Die `%` (Modulo/Rest)-Funktion wird verwendet, um den Rest nach der Teilung der beiden Argument-Ausdruck zu finden.

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

Jetzt, da Sie von Arithmetik-Funktionen gelernt haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).
