---
title: Schema-Feldergruppe "Einlagendetails"
description: Dieses Dokument bietet einen Überblick über die Feldergruppe "Einlagendetails".
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 7%

---

# [!UICONTROL Einlagendetails] Schemafeldgruppe

[!UICONTROL Einlagendetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe stellt eine `personalFinances.deposits` -Feld in ein Schema, das Details zu einer finanziellen Einlage erfasst.

![](../../images/field-groups/deposit-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `account` | [[!UICONTROL Finanzkonto]](../../data-types/financial-account.md) | Beschreibt das mit der Einlage verbundene Finanzkonto. |
| `transaction` | [[!UICONTROL Transaktion]](../../data-types/transaction.md) | Beschreibt die mit der Einlage verbundene Finanztransaktion. |
| `mobileDeposit` | [!UICONTROL Boolesch] | Gibt an, ob die Anzahlung über eine mobile Plattform erfolgt ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
