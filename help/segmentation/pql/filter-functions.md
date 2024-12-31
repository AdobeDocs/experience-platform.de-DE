---
solution: Experience Platform
title: PQL-Filterfunktionen
description: Filterfunktionen werden zum Filtern von Daten innerhalb von Arrays in Profile Query Language (PQL) verwendet.
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 7c282594e66c8c7700471a94947448fd91596814
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 66%

---

# Filterfunktionen

Filterfunktionen werden zum Filtern von Daten innerhalb von Arrays in [!DNL Profile Query Language] (PQL) verwendet. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md).

## Filter

Mit der Funktion `[]` (Filter) können Filter auf ein Array angewendet werden und eine Teilmenge des Arrays zurückgeben, die der angegebenen Bedingung entsprechen. Daher gibt diese Funktion ein Array zurück.

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
