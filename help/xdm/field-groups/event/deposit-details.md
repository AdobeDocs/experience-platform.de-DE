---
title: Feldgruppe „Einzahlungsdetails“
description: Erfahren Sie mehr über die Schemafeldgruppe „Einzahlungsdetails“.
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 4%

---

# [!UICONTROL Einzahlungsdetails] Schemafeldgruppe

[!UICONTROL Einzahlungsdetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe stellt ein einzelnes `personalFinances.deposits` für ein Schema bereit, das Details zu einer Finanzeinzahlung erfasst.

![](../../images/field-groups/deposit-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `account` | [[!UICONTROL Finanzkonto]](../../data-types/financial-account.md) | Beschreibt das mit der Einzahlung verknüpfte Finanzkonto. |
| `transaction` | [[!UICONTROL Transaktion]](../../data-types/transaction.md) | Beschreibt die Finanztransaktion, die mit der Einlage verbunden ist. |
| `mobileDeposit` | [!UICONTROL Boolesch] | Gibt an, ob die Einzahlung über eine mobile Plattform erfolgt ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
