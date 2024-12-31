---
solution: Experience Platform
title: Logische Quantoren in PQL
description: Logische Quantoren können verwendet werden, um Bedingungen mit Arrays in Profile Query Language (PQL) durchzusetzen.
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 12%

---

# Funktionen logischer Quantoren

Logische Quantoren können verwendet werden, um Bedingungen mit Arrays in [!DNL Profile Query Language] (PQL) durchzusetzen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md).

## Existiert

Die `exists` bestimmt, ob ein Element in einem Array vorhanden ist, sofern die angegebene Bedingung erfüllt ist.

**Format**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Beschreibung |
| ---------- | ----------- |
| `{VARIABLE}` | Ein Name einer Variablen. |
| `{EXPRESSION}` | Das Array, das überprüft wird. |
| `{CONDITION}` | Ein optionaler Ausdruck, der die Werte im zurückgegebenen -Array filtert. |

**Beispiel**

Die folgende PQL-Abfrage ruft alle Ereignisse ab, deren Preis größer als 50 $ oder deren SKU „PS“ lautet.

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
| `{CONDITION}` | Ein optionaler Ausdruck, der die Werte im zurückgegebenen -Array filtert. |

**Beispiel**

Die folgende PQL-Abfrage ruft alle Ereignisse ab, deren Preis größer als 50 $ ist und deren SKU „PS“ lautet.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Nächste Schritte

Nachdem Sie sich mit logischen Quantoren vertraut gemacht haben, können Sie diese in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
