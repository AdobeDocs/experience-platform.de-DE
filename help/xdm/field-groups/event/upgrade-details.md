---
title: Schemafeldgruppe „Upgrade-Details“
description: Erfahren Sie mehr über die Schemafeldgruppe „Upgrade-Details“.
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL Upgrade-Details] Schemafeldgruppe

[!UICONTROL Upgrade-Details] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md), mit der Informationen zu einem Upgrade-Marketing-Ereignis erfasst werden, einschließlich Details zur Transaktion und den verschiedenen Möglichkeiten, wie das Angebot einem Kunden angezeigt wurde.

Die Feldergruppe stellt `upgrades` ein einzelnes Feld vom Typ „Objekt“ bereit. Die in diesem Objekt enthaltenen Eigenschaften werden nachfolgend erläutert.

![Struktur der Upgrade-](../../images/field-groups/upgrade-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `upgradeImpressions` | Array von [Impressions](../../data-types/impressions.md) | Ein Array, das die aufgezeichneten Impressionen (digitale Ansichten oder Interaktionen mit dem Upgrade-Angebot) für den Kunden auflistet. |
| `upgradeTransaction` | [Transaktion](../../data-types/transaction.md) | Beschreibt die Währungstransaktion für das Upgrade. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
