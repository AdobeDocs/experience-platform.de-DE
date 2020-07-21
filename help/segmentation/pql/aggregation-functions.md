---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aggregationsfunktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 24%

---


# Aggregationsfunktionen

Aggregationsfunktionen werden verwendet, um mehrere Werte innerhalb von [!DNL Profile Query Language] (PQL-)Arrays zu gruppieren und einen einzigen Zusammenfassungswert zu bilden. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).

## Anzahl

Die `count` Funktion gibt die Anzahl der Elemente innerhalb des angegebenen Arrays zurück.

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

Die `sum` Funktion gibt die Summe aller ausgewählten Werte im Array zurück.

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

Die `average` Funktion gibt das arithmetische Mittel aller ausgewählten Werte im Array zurück.

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

Die `min` Funktion gibt die kleinsten aller ausgewählten Werte im Array zurück.

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

Die `max` Funktion gibt den größten der ausgewählten Werte im Array zurück.

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

Nachdem Sie nun von Aggregationsfunktionen Kenntnis erhalten haben, können Sie diese in Ihren PQL-Abfragen verwenden. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).
