---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;pql;PQL;Sprache der Profil-Abfrage;Verschiedene Funktionen;misc;
solution: Experience Platform
title: Sonstige Funktionen
topic: developer guide
description: Die folgende Funktion ist eine sonstige Funktion für Profil Query Language (PQL).
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 70%

---


# Sonstige Funktionen

Die folgende Funktion ist eine verschiedene Funktion für [!DNL Profile Query Language] (PQL). Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] overview](./overview.md).

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

Nun kennen Sie sonstige Funktionen und können sie in Ihren PQL-Abfragen nutzen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
