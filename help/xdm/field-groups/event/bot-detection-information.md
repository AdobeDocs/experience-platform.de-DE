---
title: Feldergruppe "Bot Detection"
description: Erfahren Sie mehr über die Schemafeldgruppe "Bot Detection"(XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 8%

---

# [!UICONTROL Bot-Erkennung] Feldergruppe

[!UICONTROL Bot-Erkennung] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe enthält Informationen zum Bot-generierten Traffic.

![Ein Diagramm des [!UICONTROL Bot-Erkennung] Feldergruppe.](../../images/field-groups/bot-detection-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Bot-Erkennung] | `botDetection` | Objekt | Bietet Informationen zum Bot-generierten Traffic. |
| [!UICONTROL Ergebnis] | `score` | number | Die Bot-Wahrscheinlichkeitsbewertung von null bis eins. Eine Null bedeutet, dass der Traffic kein Bot ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)

