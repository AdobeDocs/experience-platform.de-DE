---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Transaktion; Datentyp; Datentyp; Datentyp;
title: Transaktionsdatentyp
description: Dieses Dokument bietet einen Überblick über den Datentyp "Transaction Experience Data Model"(XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 11%

---

#  Transaktionsdatentyp

 Transactionist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die Details einer monetären Transaktion beschreibt.

![Transaktionsstruktur](../images/data-types/transaction.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Währung]](./currency.md) | Beschreibt den Währungsbetrag, der im Rahmen der Transaktion umgetauscht wird. |
| `transactionDate` | [!UICONTROL DateTime] | Ein Zeitstempel, der angibt, wann die Transaktion stattgefunden hat. |
| `transactionId` | [!UICONTROL Zeichenfolge] | Eine eindeutige Kennung für die Transaktion. |
| `transactionType` | [!UICONTROL Zeichenfolge] | Der vom Besucher verwendete Transaktionstyp. |

{style=&quot;table-layout:auto&quot;}
