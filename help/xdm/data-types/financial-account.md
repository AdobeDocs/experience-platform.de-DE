---
title: Datentyp "Finanzkonto"
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp für Finanzkonten.
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 10%

---

# [!UICONTROL Finanzkonto] Datentyp

[!UICONTROL Finanzkonto] ist ein standardmäßiger XDM-Datentyp, der die Details eines Finanzkontos einschließlich Typ, Eigentümer und aktueller Saldo beschreibt.

![](../images/data-types/financial-account.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Währung]](./currency.md) | Der Leistungsbilanzsaldo des Kontos. |
| `financialAccountId` | [!UICONTROL Zeichenfolge] | Eine eindeutige ID für das Konto. |
| `financialAccountName` | [!UICONTROL Zeichenfolge] | Der dem Konto zugewiesene Name. |
| `financialAccountType` | [!UICONTROL Zeichenfolge] | Die Art des Finanzkontos, wie z. B. Kontrolle, Ersparnis oder Pensionierung. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
