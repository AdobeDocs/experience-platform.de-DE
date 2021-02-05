---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;pql;PQL;Sprache der Profil-Abfrage;Arithmetik;
solution: Experience Platform
title: PAL Arithmetic-Funktionen
topic: developer guide
description: Mit arithmetischen Funktionen lassen sich Basisberechnungen für Werte in Profile Query Language (PQL) durchführen.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 83%

---


# Arithmetische Funktionen

Arithmetische Funktionen werden verwendet, um grundlegende Berechnungen für Werte in [!DNL Profile Query Language] (PQL) durchzuführen. Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] overview](./overview.md).

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

## Dividieren

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

Nachdem Sie sich mit arithmetischen Funktionen vertraut gemacht haben, können Sie sie nun in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
