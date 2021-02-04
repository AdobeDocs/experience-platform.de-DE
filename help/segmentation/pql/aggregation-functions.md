---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;pql;PQL;Sprache der Profil-Abfrage;Aggregationsfunktionen;Aggregation;
solution: Experience Platform
title: Aggregationsfunktionen
topic: developer guide
description: 'Aggregationsfunktionen werden verwendet, um mehrere Werte in PQL-Arrays (Profil Abfrage Language) zu gruppieren und so einen Zusammenfassungswert zu bilden. '
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 14%

---


# Aggregationsfunktionen

Aggregationsfunktionen werden verwendet, um mehrere Werte innerhalb von [!DNL Profile Query Language] (PQL)-Arrays zu gruppieren, um einen einzigen Zusammenfassungswert zu bilden. Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] overview](./overview.md).

## Anzahl

Die Funktion `count` gibt die Anzahl der Elemente innerhalb des angegebenen Arrays zurück.

**Format**

```sql
{ARRAY}.count()
```

**Beispiel**

Die folgende PQL-Abfrage gibt die Anzahl der Bestellungen im Array zurück.

```sql
orders.count()
```

## Sum

Die Funktion `sum` gibt die Summe aller ausgewählten Werte im Array zurück.

**Format**

```sql
{ARRAY}.sum()
```

**Beispiel**

Die folgende PQL-Abfrage gibt die Summe aller Bestellpreise zurück.

```sql
orders.sum(order.price)
```

## Durchschnitt

Die Funktion `average` gibt das arithmetische Mittel aller ausgewählten Werte im Array zurück.

**Format**

```sql
{ARRAY}.average()
```

**Beispiel**

Die folgende PQL-Abfrage gibt den Durchschnittspreis aller Bestellungen zurück.

```sql
orders.average(order.price)
```

## Minimum

Die Funktion `min` gibt die kleinsten aller ausgewählten Werte im Array zurück.

**Format**

```sql
{ARRAY}.min()
```

**Beispiel**

Die folgende PQL-Abfrage gibt den niedrigsten Preis aller Bestellungen zurück.

```sql
orders.min(order.price)
```

## Maximum

Die Funktion `max` gibt den größten der ausgewählten Werte im Array zurück.

**Format**

```sql
{ARRAY}.max()
```

**Beispiel**

Die folgende PQL-Abfrage gibt den höchsten Preis aller Bestellungen zurück.

```sql
orders.max(order.price)
```

## Nächste Schritte

Nachdem Sie nun von Aggregationsfunktionen Kenntnis erhalten haben, können Sie diese in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
