---
title: Upsell Details Schema Field Group
description: Erfahren Sie mehr über die Feldergruppe Upsell Details .
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 3%

---

# [!UICONTROL Upsell-Details] Schemafeldgruppe

[!UICONTROL Upsell-Details] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) zur Erfassung von Informationen zu einem Upsell-Marketing-Ereignis verwendet wird, einschließlich Details zur Transaktion und der verschiedenen Arten der Anzeige des Angebots für einen Kunden.

Die Feldergruppe stellt ein einzelnes Feld vom Typ Objekt bereit, `upsells`. Die in diesem Objekt enthaltenen Eigenschaften werden nachfolgend erläutert.

![Struktur der Upsell-Details](../../images/field-groups/upsell-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `upsellImpressions` | Array von [Impressionen](../../data-types/impressions.md) | Ein Array, das die aufgezeichneten Impressionen (digitale Ansichten oder Interaktionen mit dem Upsell-Angebot) für den Kunden auflistet. |
| `upsellTransaction` | [Transaktion](../../data-types/transaction.md) | Beschreibt die Währungstransaktion für den Upsell. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
