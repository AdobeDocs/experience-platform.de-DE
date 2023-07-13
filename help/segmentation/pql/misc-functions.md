---
solution: Experience Platform
title: PQL - Verschiedene Funktionen
description: Die folgende Funktion ist eine sonstige Funktion für Profil Query Language (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 79%

---

# Sonstige Funktionen

Die folgende Funktion ist eine sonstige Funktion für [!DNL Profile Query Language] (PQL). Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] Übersicht](./overview.md).

## Zulassen

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

Nun kennen Sie sonstige Funktionen und können sie in Ihren PQL-Abfragen nutzen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
