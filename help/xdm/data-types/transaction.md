---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Transaktion; Datentyp; Datentyp; Datentyp
title: Transaktionsdatentyp
description: Erfahren Sie mehr über den Datentyp "Transaction Experience Data Model"(XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 7%

---

# [!UICONTROL Transaktion] Datentyp

[!UICONTROL Transaktion] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die Details einer monetären Transaktion beschreibt.

![Transaktionsstruktur](../images/data-types/transaction.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Währung]](./currency.md) | Beschreibt den Währungsbetrag, der im Rahmen der Transaktion umgetauscht wird. |
| `transactionDate` | [!UICONTROL DateTime] | Ein Zeitstempel, der angibt, wann die Transaktion erfolgte. |
| `transactionId` | [!UICONTROL String] | Eine eindeutige Kennung für die Transaktion. |
| `transactionType` | [!UICONTROL String] | Der vom Besucher verwendete Transaktionstyp. |

{style="table-layout:auto"}
