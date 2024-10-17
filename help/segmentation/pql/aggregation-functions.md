---
solution: Experience Platform
title: PQL-Aggregationsfunktionen
description: Aggregationsfunktionen dienen dazu, mehrere Werte innerhalb von Profile Query Language (PQL)-Arrays zu gruppieren, um einen einzigen Zusammenfassungswert zu bilden.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 38%

---

# Aggregationsfunktionen

Aggregationsfunktionen dienen dazu, mehrere Werte innerhalb von [!DNL Profile Query Language] (PQL)-Arrays zu gruppieren, um einen einzigen Zusammenfassungswert zu bilden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md) .

## Anzahl

Die Funktion `count` gibt die Anzahl der Elemente im angegebenen Array als Zahl zurück.

**Format**

```sql
{ARRAY}.count()
```

**Beispiel**

Die folgende PQL-Abfrage gibt die Anzahl der Bestellungen im Array zurück.

```sql
orders.count()
```

## Summe

Die Funktion `sum` gibt die Summe aller im Array ausgewählten Werte als Zahl zurück.

**Format**

```sql
{ARRAY}.sum()
```

**Beispiel**

Die folgende PQL-Abfrage gibt die Summe aller Angebotspreise zurück.

```sql
orders.sum(order.price)
```

## Durchschnitt

Die Funktion `average` gibt das arithmetische Mittel aller im Array ausgewählten Werte als Zahl zurück.

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

Die Funktion `min` gibt die kleinste aller im Array ausgewählten Werte als Zahl zurück.

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

Die Funktion `max` gibt den größten Wert aller im Array ausgewählten Werte als Zahl zurück.

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

Nachdem Sie sich mit Aggregationsfunktionen vertraut gemacht haben, können Sie diese nun in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
