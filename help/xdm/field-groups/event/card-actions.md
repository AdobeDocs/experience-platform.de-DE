---
title: Schemafeldgruppe für Kartenaktionen
description: Erfahren Sie mehr über die Feldgruppe Kartenaktionen .
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 24%

---

# [!UICONTROL Kartenaktionen] Schemafeldgruppe

[!UICONTROL Kartenaktionen] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Die Feldergruppe stellt ein einzelnes `personalFinances.cardActions` -Feld für ein Schema bereit, das Details zu einer Kartenaktion wie Kartentyp, Aktivierungsstatus und Sperrstatus erfasst.

![](../../images/field-groups/card-actions.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `cardActivated` | Ganzzahl | Verfolgt die erfolgreiche Aktivierung der Karte. |
| `cardActivationStart` | Ganzzahl | Verfolgt den Start des Kartenaktivierungsprozesses. |
| `cardCancelled` | Ganzzahl | Verfolgt, wann eine Karte storniert wurde. |
| `cardControlsLocked` | Ganzzahl | Verfolgt, wenn die Steuerelemente einer Karte gesperrt sind. |
| `cardControlsUnlocked` | Ganzzahl | Verfolgt, wenn die Steuerelemente einer Karte entsperrt wurden. |
| `cardID` | Zeichenfolge | Die Kennung für die zu aktivierende Karte. Dieser Wert kann sich von der Kartennummer unterscheiden. |
| `cardLocked` | Ganzzahl | Verfolgt, wann eine Karte gesperrt wurde. |
| `cardOrderNew` | Ganzzahl | Verfolgt, wann eine Karte angefordert wurde. |
| `cardOrderType` | Zeichenfolge | Die Art der Kartenreihenfolge, die mit einem Kartenbestellereignis verknüpft ist. |
| `cardType` | Zeichenfolge | Der Typ der Karte. |
| `cardUnlocked` | Ganzzahl | Verfolgt, wann eine Karte entsperrt wurde. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
