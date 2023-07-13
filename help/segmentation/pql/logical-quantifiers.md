---
solution: Experience Platform
title: Logische PQL-Quantifizierer
description: Logische Quantifizierer können verwendet werden, um Bedingungen mit Arrays in der Profile Query Language (PQL) zu erteilen.
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 11%

---

# Logikquantifizierer-Funktionen

Logische Quantifizierer können verwendet werden, um Bedingungen mit Arrays in [!DNL Profile Query Language] (PQL). Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] Übersicht](./overview.md).

## Exists

Die `exists` bestimmt, ob ein Element in einem Array vorhanden ist, vorausgesetzt, es erfüllt die bereitgestellte Bedingung.

**Format**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Beschreibung |
| ---------- | ----------- |
| `{VARIABLE}` | Ein Name einer Variablen. |
| `{EXPRESSION}` | Das Array, das überprüft wird. |
| `{CONDITION}` | Ein optionaler Ausdruck, der die Werte im zurückgegebenen Array filtert. |

**Beispiel**

Die folgende PQL-Abfrage ruft alle Ereignisse ab, die einen Preis von mehr als 50 USD oder eine SKU von &quot;PS&quot;haben.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Für alle

Die `forall` bestimmt alle Elemente in einem Array, die alle angegebenen Bedingungen erfüllen.

**Format**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Beschreibung |
| ---------- | ----------- |
| `{VARIABLE}` | Ein Name einer Variablen. |
| `{EXPRESSION}` | Das Array, das überprüft wird. |
| `{CONDITION}` | Ein optionaler Ausdruck, der die Werte im zurückgegebenen Array filtert. |

**Beispiel**

Die folgende PQL-Abfrage ruft alle Ereignisse ab, deren Preis 50 USD übersteigt und deren SKU &quot;PS&quot;lautet.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Nächste Schritte

Nachdem Sie sich mit logischen Quantifizierern vertraut gemacht haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
