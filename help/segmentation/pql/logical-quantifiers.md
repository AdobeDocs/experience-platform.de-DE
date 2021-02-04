---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;pql;PQL;Sprache der Profil-Abfrage;Logische Quantifizierer;Logischer Quantifizierer;
solution: Experience Platform
title: Logische Quantoren
topic: developer guide
description: Logische Quantifizierer können verwendet werden, um Bedingungen mit Arrays in Profil Abfrage Language (PQL) zu erlangen.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 11%

---


# Logikquantifizierer-Funktionen

Logische Quantifizierer können verwendet werden, um Bedingungen mit Arrays in [!DNL Profile Query Language] (PQL) zu bestätigen. Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] overview](./overview.md).

## Exists

Die Funktion `exists` bestimmt, ob ein Element in einem Array vorhanden ist, sofern die angegebene Bedingung erfüllt ist.

**Format**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Beschreibung |
| ---------- | ----------- |
| `{VARIABLE}` | Der Name einer Variablen. |
| `{EXPRESSION}` | Das Array, das überprüft wird. |
| `{CONDITION}` | Ein optionaler Ausdruck, der die Werte im Array Filter. |

**Beispiel**

Die folgende PQL-Abfrage erhält alle Ereignis mit einem Preis von mehr als 50 USD oder einer SKU von &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Für alle

Die Funktion `forall` bestimmt alle Elemente in einem Array, die alle angegebenen Bedingungen erfüllen.

**Format**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Beschreibung |
| ---------- | ----------- |
| `{VARIABLE}` | Der Name einer Variablen. |
| `{EXPRESSION}` | Das Array, das überprüft wird. |
| `{CONDITION}` | Ein optionaler Ausdruck, der die Werte im Array Filter. |

**Beispiel**

Die folgende PQL-Abfrage erhält alle Ereignis, die einen Preis von mehr als 50 USD haben und eine SKU von &quot;PS&quot; haben.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Nächste Schritte

Jetzt, da Sie von logischen Quantifizierern gelernt haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
