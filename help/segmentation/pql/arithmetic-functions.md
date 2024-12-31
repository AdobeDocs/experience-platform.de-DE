---
solution: Experience Platform
title: Arithmetische PAL-Funktionen
description: Mit arithmetischen Funktionen lassen sich einfache Berechnungen für Werte in Profile Query Language (PQL) durchführen.
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 51%

---

# Arithmetische Funktionen

Mit arithmetischen Funktionen lassen sich einfache Berechnungen für Werte in [!DNL Profile Query Language] (PQL) durchführen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md).

## Hinzufügen

Die Funktion `+` (Addition) wird verwendet, um die Summe zweier Argumentausdrücke als Zahl zu ermitteln.

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

Die Funktion `*` (Multiplikation) wird verwendet, um das Produkt zweier Argumentausdrücke als Zahl zu finden.

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

Mit der Funktion `-` (Subtraktion) wird die Differenz zweier Argumentausdrücke als Zahl ermittelt.

**Format**

```sql
{NUMBER} - {NUMBER}
```

**Beispiel**

Die folgende PQL-Abfrage ermittelt den Preisunterschied zwischen zwei verschiedenen Produkten.

```sql
product1.price - product2.price
```

## Dividieren

Mit der Funktion `/` (Division) wird der Quotient zweier Argumentausdrücke als Zahl ermittelt.

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

Die Funktion `%` (modulo/rest) wird verwendet, um den Rest zu finden, nachdem die beiden Argumentausdrücke als Zahl dividiert wurden.

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

Nachdem Sie sich mit arithmetischen Funktionen vertraut gemacht haben, können Sie sie nun in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
