---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;pql;PQL;Profil-Abfrage-Sprache;Filterfunktionen;Filter;
solution: Experience Platform
title: Filterfunktionen
topic: developer guide
description: Filterfunktionen werden zum Filtern von Daten in Arrays in Profil Abfrage Language (PQL) verwendet.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 77%

---


# Filterfunktionen

Filterfunktionen werden zum Filtern von Daten innerhalb von Arrays in [!DNL Profile Query Language] (PQL) verwendet. Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] overview](./overview.md).

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
