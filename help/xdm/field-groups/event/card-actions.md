---
title: Schemafeldgruppe für Kartenaktionen
description: Dieses Dokument bietet einen Überblick über die Feldgruppe Kartenaktionen .
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%

---

# [!UICONTROL Kartenaktionen] Schemafeldgruppe

[!UICONTROL Kartenaktionen] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe stellt eine `personalFinances.cardActions` -Feld in ein Schema, das Details zu einer Kartenaktion wie Kartentyp, Aktivierungsstatus und Sperrstatus erfasst.

![](../../images/field-groups/card-actions.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `cardActivated` | Ganzzahl | Verfolgt, wann die Karte erfolgreich aktiviert wurde. |
| `cardActivationStart` | Ganzzahl | Verfolgt, wann der Kartenaktivierungsprozess gestartet wurde. |
| `cardCancelled` | Ganzzahl | Verfolgt den Abbruch einer Karte. |
| `cardControlsLocked` | Ganzzahl | Verfolgt, wenn die Steuerelemente einer Karte gesperrt sind. |
| `cardControlsUnlocked` | Ganzzahl | Verfolgt, wenn die Steuerelemente einer Karte entsperrt wurden. |
| `cardID` | Zeichenfolge | Die Kennung für die zu aktivierende Karte. Dieser Wert kann sich von der Kartennummer unterscheiden. |
| `cardLocked` | Ganzzahl | Verfolgt, wenn eine Karte gesperrt wurde. |
| `cardOrderNew` | Ganzzahl | Verfolgt, wann eine Karte angefordert wurde. |
| `cardOrderType` | Zeichenfolge | Die Art der Kartenreihenfolge, die mit einem Kartenbestellereignis verknüpft ist. |
| `cardType` | Zeichenfolge | Der Typ der Karte. |
| `cardUnlocked` | Ganzzahl | Verfolgt, wenn eine Karte entsperrt wurde. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
