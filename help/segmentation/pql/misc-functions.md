---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verschiedene Funktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: d7ec6240864916d3b54db8bd641f4917a38f9480
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Verschiedene Funktionen

Die folgende Funktion ist eine verschiedene Funktion für Profil Abfrage Language (PQL). Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).

## Lasst

Die `let` Funktion ermöglicht die Speicherung eines Ausdrucks als Variable, die später in einer Abfrage verwendet werden kann.

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Beispiel**

Die folgende PQL-Abfrage erhält alle Summen der Produktsummen mit der Transaktion in USD, wobei die Summe mehr als 100 USD und weniger als 1000 USD beträgt.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Nächste Schritte

Jetzt, da Sie von verschiedenen Funktionen erfahren haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).
