---
title: Schema-Feldergruppe "Einlagendetails"
description: Erfahren Sie mehr über die Feldergruppe "Einlagendetails".
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 4%

---

# [!UICONTROL Einlagendetails] Schemafeldgruppe

[!UICONTROL Einlagendetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Die Feldergruppe stellt ein einzelnes `personalFinances.deposits` -Feld für ein Schema bereit, das Details zu einer finanziellen Einlage erfasst.

![](../../images/field-groups/deposit-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `account` | [[!UICONTROL Finanzkonto]](../../data-types/financial-account.md) | Beschreibt das mit der Einlage verbundene Finanzkonto. |
| `transaction` | [[!UICONTROL Transaktion]](../../data-types/transaction.md) | Beschreibt die mit der Einlage verbundene Finanztransaktion. |
| `mobileDeposit` | [!UICONTROL Boolean] | Gibt an, ob die Anzahlung über eine mobile Plattform erfolgt ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
