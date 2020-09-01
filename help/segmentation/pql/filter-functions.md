---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;filter functions;filter;
solution: Experience Platform
title: Filterfunktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 87%

---


# Filterfunktionen

Filter functions are used to filter data within arrays in [!DNL Profile Query Language] (PQL). More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

## Filter

Mit der Funktion `[]` (filter) können Filter auf ein Array angewendet und eine Teilmenge des Arrays zurückgegeben werden, die der angegebenen Bedingung entspricht.

**Format**

```sql
{ARRAY}[filter]
```

**Beispiel**

Die folgende PQL-Abfrage ruft alle Ereignisse ab, bei denen mindestens ein Produktartikel mit der SKU „PS“ vorhanden ist.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Up-Operator

Mit dem Operator `^` (up) können Sie auf Eigenschaften in höheren Ebenen von Filtern verweisen.

**Format**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argument | Beschreibung |
| -------- | ----------- |
| `{ARRAY}` | Das Array, das gefiltert wird. |
| `{FILTER_1}` | Die äußere Filterebene. |
| `{FILTER_2}` | Die innere Filterebene. |
| `^{PROPERTY}` | Die Eigenschaft, anhand der ebenfalls gefiltert wird. Aufgrund von `^` wird eine Eigenschaft geprüft, die auf „filter1“ basiert. |

**Beispiel**

Folgende PQL-Abfrage ruft alle Ereignisse ab, bei denen mindestens ein Produktartikel mit der SKU „PS“ **oder** eine Person vorhanden ist, deren Geschlecht weiblich ist.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Nächste Schritte

Nachdem Sie sich mit Filterfunktionen vertraut gemacht haben, können Sie sie nun in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
