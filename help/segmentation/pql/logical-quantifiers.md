---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Logische Quantoren
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 21%

---


# Logikquantifizierer-Funktionen

Logische Quantifizierer können verwendet werden, um Bedingungen mit Arrays in [!DNL Profile Query Language] (PQL) zu erlangen. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).

## Exists

Die `exists` Funktion bestimmt, ob ein Element in einem Array vorhanden ist, vorausgesetzt, es erfüllt die bereitgestellte Bedingung.

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

Die `forall` Funktion bestimmt alle Elemente in einem Array, die alle angegebenen Bedingungen erfüllen.

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

Jetzt, da Sie von logischen Quantifizierern gelernt haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).
