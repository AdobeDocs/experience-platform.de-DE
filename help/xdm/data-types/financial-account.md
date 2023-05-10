---
title: Datentyp "Finanzkonto"
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp für Finanzkonten.
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 7%

---

# [!UICONTROL Finanzkonto] Datentyp

[!UICONTROL Finanzkonto] ist ein standardmäßiger XDM-Datentyp, der die Details eines Finanzkontos einschließlich Typ, Eigentümer und aktueller Saldo beschreibt.

![](../images/data-types/financial-account.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL Währung]](./currency.md) | Der Leistungsbilanzsaldo des Kontos. |
| `financialAccountId` | [!UICONTROL String] | Eine eindeutige ID für das Konto. |
| `financialAccountName` | [!UICONTROL String] | Der dem Konto zugewiesene Name. |
| `financialAccountType` | [!UICONTROL String] | Die Art des Finanzkontos, wie z. B. Kontrolle, Ersparnis oder Pensionierung. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json).
