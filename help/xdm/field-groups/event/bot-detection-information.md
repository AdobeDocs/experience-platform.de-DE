---
title: Feldergruppe „Bot-Erkennung“
description: Erfahren Sie mehr über die Schemafeldgruppe der Bot-Erkennungs-Feldergruppe (XDM).
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 8%

---

# [!UICONTROL Bot-Erkennung] Feldergruppe

[!UICONTROL Bot-Erkennung] ist eine standardmäßige Schemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Die Feldergruppe stellt Informationen zum von Bots generierten Traffic bereit.

![Ein Diagramm der Feldergruppe [!UICONTROL Bot-Erkennung].](../../images/field-groups/bot-detection-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Bot-Erkennung] | `botDetection` | Objekt | Enthält Informationen zum von Bots generierten Traffic. |
| [!UICONTROL Ergebnis] | `score` | number | Der Bot-Wahrscheinlichkeitswert von null bis eins. Ein Score von null bedeutet, dass der Traffic kein Bot ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
