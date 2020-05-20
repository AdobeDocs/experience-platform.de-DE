---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Filterfunktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 4%

---


# Filterfunktionen

Filterfunktionen werden zum Filtern von Daten in Arrays in Profil Abfrage Language (PQL) verwendet. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).

## Filter

Mit der Funktion `[]` (filter) können Filter auf ein Array angewendet und eine Untergruppe des Arrays zurückgegeben werden, die der angegebenen Bedingung entspricht.

**Format**

```sql
{ARRAY}[filter]
```

**Beispiel**

Die folgende PQL-Abfrage ruft alle Ereignis ab, bei denen mindestens ein Produktelement mit einer SKU gleich &quot;PS&quot;vorhanden ist.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Up-Operator

Mit dem Operator `^` (up) können Sie auf Eigenschaften in oberen Ebenen von Filtern verweisen.

**Format**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argument | Beschreibung |
| -------- | ----------- |
| `{ARRAY}` | Das Array, das gefiltert wird. |
| `{FILTER_1}` | Die äußere Filterebene. |
| `{FILTER_2}` | Die innere Filterebene |
| `^{PROPERTY}` | Die Eigenschaft, auf der ebenfalls gefiltert wird. Aufgrund des `^`Problems prüft es eine Eigenschaft, die auf filter1 basiert. |

**Beispiel**

Die folgende PQL-Abfrage erhält alle Ereignis, die mindestens einen Produktartikel mit einer SKU gleich &quot;PS&quot; **oder** eine Person mit weiblichem Geschlecht haben.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Nächste Schritte

Jetzt, da Sie von Filterfunktionen erfahren haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).
