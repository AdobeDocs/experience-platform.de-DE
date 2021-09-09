---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Transaktion; Datentyp; Datentyp; Datentyp;
title: Transaktionsdatentyp
description: Dieses Dokument bietet einen Überblick über den Datentyp "Transaction Experience Data Model"(XDM).
source-git-commit: bbe5456ddba1db9044b8a7f94a7ba8e450f89f0f
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 11%

---

#  Transaktionsdatentyp

 Transactionist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der die Details einer Geldtransaktion beschreibt.

![Transaktionsstruktur](../images/data-types/transaction.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Währung]](./currency.md) | Beschreibt den Währungsbetrag, der im Rahmen der Transaktion umgetauscht wird. |
| `transactionDate` | [!UICONTROL DateTime] | Ein Zeitstempel, der angibt, wann die Transaktion stattgefunden hat. |
| `transactionId` | [!UICONTROL Zeichenfolge] | Eine eindeutige Kennung für die Transaktion. |
| `transactionType` | [!UICONTROL Zeichenfolge] | Der vom Besucher verwendete Transaktionstyp. |

{style=&quot;table-layout:auto&quot;}
