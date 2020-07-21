---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sonstige Funktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 91%

---


# Sonstige Funktionen

The following function is a miscellaneous function for [!DNL Profile Query Language] (PQL). Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).

## Let

Die `let`-Funktion ermöglicht das Speichern eines Ausdrucks als Variable, die später in einer Abfrage verwendet werden kann.

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Beispiel**

Die folgende PQL-Abfrage ruft alle Beträge von Produktsummen mit einer Transaktion in USD ab, wobei sich die Beträge auf mehr als 100 $ und weniger als 1.000 $ belaufen.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Nächste Schritte

Nun kennen Sie sonstige Funktionen und können sie in Ihren PQL-Abfragen nutzen. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).
