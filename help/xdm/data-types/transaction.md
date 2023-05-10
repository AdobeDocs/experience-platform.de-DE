---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Transaktion; Datentyp; Datentyp; Datentyp;
title: Transaktionsdatentyp
description: Dieses Dokument bietet einen Überblick über den Datentyp "Transaction Experience Data Model"(XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 8%

---

# [!UICONTROL Transaktion] Datentyp

[!UICONTROL Transaktion] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der die Details einer monetären Transaktion beschreibt.

![Transaktionsstruktur](../images/data-types/transaction.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Währung]](./currency.md) | Beschreibt den Währungsbetrag, der im Rahmen der Transaktion umgetauscht wird. |
| `transactionDate` | [!UICONTROL DateTime] | Ein Zeitstempel, der angibt, wann die Transaktion stattgefunden hat. |
| `transactionId` | [!UICONTROL String] | Eine eindeutige Kennung für die Transaktion. |
| `transactionType` | [!UICONTROL String] | Der vom Besucher verwendete Transaktionstyp. |

{style="table-layout:auto"}
