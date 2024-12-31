---
title: Schemafeldgruppe „Saldoübertragungen“
description: Erfahren Sie mehr über die Schemafeldgruppe „Saldoübertragungen“.
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 3%

---

# Schemafeldgruppe [!UICONTROL Saldoübertragungen]

[!UICONTROL Saldoübertragungen] ist eine Standardschemafeldgruppe für die Klasse [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md). Die Feldergruppe stellt ein einzelnes `personalFinances.balanceTransfers` für ein Schema bereit, das Details zu einem Finanzsaldo-Transfer zwischen Konten erfasst.

![](../../images/field-groups/balance-transfers.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Finanzkonto]](../../data-types/financial-account.md) | Beschreibt das Finanzkonto, von dem der Saldo übertragen wird. |
| `accountTo` | [[!UICONTROL Finanzkonto]](../../data-types/financial-account.md) | Beschreibt das Finanzkonto, auf das der Saldo übertragen wird. |
| `transaction` | [[!UICONTROL Transaktion]](../../data-types/transaction.md) | Beschreibt die finanzielle Transaktion, die mit der Saldoübertragung verbunden ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
