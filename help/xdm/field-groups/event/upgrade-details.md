---
title: Schemafeldgruppe "Details aktualisieren"
description: Dieses Dokument bietet einen Überblick über die Feldergruppe des Schemas "Upgrade-Details".
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 5%

---

# [!UICONTROL Aktualisieren Sie ] die Feldergruppe Detailschema .

[!UICONTROL Upgrade-] Details sind eine Standardschemafeldgruppe für die  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) Klasse, mit der Informationen zu einem Upgrade-Marketing-Ereignis erfasst werden, einschließlich Details zur Transaktion und den verschiedenen Arten der Anzeige des Angebots für einen Kunden.

Die Feldergruppe stellt ein einzelnes Objekt-Feld bereit, `upgrades`. Die in diesem Objekt enthaltenen Eigenschaften werden nachfolgend erläutert.

![Struktur der Upgrade-Details](../../images/field-groups/upgrade-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `upgradeImpressions` | Array von [Impressionen](../../data-types/impressions.md) | Ein Array, das die aufgezeichneten Impressionen (digitale Ansichten oder Interaktionen mit dem Upgrade-Angebot) für den Kunden auflistet. |
| `upgradeTransaction` | [Transaktion](../../data-types/transaction.md) | Beschreibt die Währungstransaktion für das Upgrade. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
