---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Filterfunktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 94%

---


# Filterfunktionen

Filter functions are used to filter data within arrays in [!DNL Profile Query Language] (PQL). Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).

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

Nachdem Sie sich mit Filterfunktionen vertraut gemacht haben, können Sie sie nun in Ihren PQL-Abfragen verwenden. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).
