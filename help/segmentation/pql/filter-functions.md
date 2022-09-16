---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; pql; PQL; Profile Query Language; Filterfunktionen; Filter;
solution: Experience Platform
title: PQL-Filterfunktionen
topic-legacy: developer guide
description: Filterfunktionen dienen zum Filtern von Daten innerhalb von Arrays in Profil Query Language (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 81%

---

# Filterfunktionen

Filterfunktionen werden verwendet, um Daten in Arrays in zu filtern. [!DNL Profile Query Language] (PQL). Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] Übersicht](./overview.md).

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
