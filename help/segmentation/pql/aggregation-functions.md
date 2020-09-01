---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;aggregation functions;aggregation;
solution: Experience Platform
title: Aggregationsfunktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 17%

---


# Aggregationsfunktionen

Aggregationsfunktionen werden verwendet, um mehrere Werte innerhalb von [!DNL Profile Query Language] (PQL-)Arrays zu gruppieren und einen einzigen Zusammenfassungswert zu bilden. More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

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

Nachdem Sie nun von Aggregationsfunktionen Kenntnis erhalten haben, können Sie diese in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
