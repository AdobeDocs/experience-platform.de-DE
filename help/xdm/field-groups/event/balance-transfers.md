---
title: Schemafeldergruppe "Balancetransfers"
description: Erfahren Sie mehr über die Schemafeldgruppe Balance-Übertragungen .
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 3%

---

# [!UICONTROL Bilanzübertragungen] Schemafeldgruppe

[!UICONTROL Bilanzübertragungen] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe stellt eine einzelne `personalFinances.balanceTransfers` -Objekt zu einem Schema, das Details zu einer Übertragung des finanziellen Saldos zwischen Konten erfasst.

![](../../images/field-groups/balance-transfers.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL Finanzkonto]](../../data-types/financial-account.md) | Beschreibt das Finanzkonto, von dem der Saldo übertragen wird. |
| `accountTo` | [[!UICONTROL Finanzkonto]](../../data-types/financial-account.md) | Beschreibt das Finanzkonto, auf das der Saldo übertragen wird. |
| `transaction` | [[!UICONTROL Transaktion]](../../data-types/transaction.md) | Beschreibt die Finanztransaktion im Zusammenhang mit der Bilanzübertragung. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
