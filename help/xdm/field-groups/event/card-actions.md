---
title: Schemafeldgruppe für Kartenaktionen
description: Erfahren Sie mehr über die Schemafeldgruppe „Kartenaktionen“.
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 24%

---

# [!UICONTROL Kartenaktionen] Schemafeldgruppe

[!UICONTROL Kartenaktionen] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Die Feldergruppe stellt ein einzelnes `personalFinances.cardActions` für ein Schema bereit, das Details zu einer Kartenaktion erfasst, z. B. Kartentyp, Aktivierungsstatus und Sperrstatus.

![](../../images/field-groups/card-actions.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `cardActivated` | Ganzzahl | Verfolgt, wann die Karte erfolgreich aktiviert wurde. |
| `cardActivationStart` | Ganzzahl | Verfolgt, wann der Kartenaktivierungsprozess gestartet wurde. |
| `cardCancelled` | Ganzzahl | Verfolgt, wann eine Karte storniert wurde. |
| `cardControlsLocked` | Ganzzahl | Verfolgt, wann die Steuerelemente einer Karte gesperrt wurden. |
| `cardControlsUnlocked` | Ganzzahl | Verfolgt, wann die Steuerelemente einer Karte entsperrt wurden. |
| `cardID` | String | Die Kennung für die Karte, die aktiviert wird. Dieser Wert kann sich von der Kartennummer unterscheiden. |
| `cardLocked` | Ganzzahl | Verfolgt, wann eine Karte gesperrt wurde. |
| `cardOrderNew` | Ganzzahl | Verfolgt, wann eine Karte angefordert wurde. |
| `cardOrderType` | String | Der Typ der Kartenbestellung, die mit einem Kartenbestellungsereignis verknüpft ist. |
| `cardType` | String | Der Kartentyp. |
| `cardUnlocked` | Ganzzahl | Verfolgt, wann eine Karte entsperrt wurde. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
