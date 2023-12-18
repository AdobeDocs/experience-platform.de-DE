---
title: Datentyp "Finanzkonto"
description: Erfahren Sie mehr über den XDM-Datentyp für Finanzkonten.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 8%

---

# [!UICONTROL Finanzkonto] Datentyp

[!UICONTROL Finanzkonto] ist ein standardmäßiger XDM-Datentyp, der die Details eines Finanzkontos einschließlich Typ, Eigentümer und aktueller Saldo beschreibt.

![](../images/data-types/financial-account.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Währung]](./currency.md) | Der aktuelle Kontostand. |
| `financialAccountId` | [!UICONTROL String] | Eine eindeutige ID für das Konto. |
| `financialAccountName` | [!UICONTROL String] | Der dem Konto zugewiesene Name. |
| `financialAccountType` | [!UICONTROL String] | Die Art des Finanzkontos, wie z. B. Kontrolle, Ersparnis oder Pensionierung. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
