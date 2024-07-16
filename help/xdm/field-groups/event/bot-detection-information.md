---
title: Feldergruppe "Bot Detection"
description: Erfahren Sie mehr über die Schemafeldgruppe "Bot Detection"(XDM).
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 8%

---

# Feldergruppe [!UICONTROL Bot-Erkennung]

[!UICONTROL Bot-Erkennung] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Die Feldergruppe enthält Informationen zum Bot-generierten Traffic.

![Ein Diagramm der Feldergruppe [!UICONTROL Bot-Erkennung].](../../images/field-groups/bot-detection-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL Bot-Erkennung] | `botDetection` | Objekt | Bietet Informationen zum Bot-generierten Traffic. |
| [!UICONTROL Ergebnis] | `score` | number | Die Bot-Wahrscheinlichkeitsbewertung von null bis eins. Eine Null bedeutet, dass der Traffic kein Bot ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
