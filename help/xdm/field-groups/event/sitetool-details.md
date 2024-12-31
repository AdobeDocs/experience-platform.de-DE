---
title: Schemafeldgruppe Sitetool-Details
description: Erfahren Sie mehr über die Schemafeldgruppe „Sitetool-Details“.
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 6%

---

# [!UICONTROL Sitetool-Details] Schemafeldgruppe

[!UICONTROL Sitetool Details] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Die Feldergruppe stellt ein einzelnes `sitetool` für ein Schema bereit, das von einem Sitetool erfasste Informationen erfasst.

![Feldergruppenstruktur](../../images/field-groups/sitetool-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `dataGatheringEvent` | Objekt | Gibt an, ob dieses Ereignis ein Datenerfassungsereignis ist, zusammen mit anderen zugehörigen Details. Enthält die folgenden Eigenschaften:<ul><li>`data`: (Zuordnung) Enthält die JSON-Daten, die im Rahmen des Quiz-, Umfrage- oder Umfrageübermittlungsereignisses erfasst und gesendet werden.</li><li>`isTrue`: (Boolesch) Gibt an, ob dieses Ereignis ein Datenerfassungsereignis wie ein Quiz, eine Umfrage oder eine Abfrage ist.</li><li>`score`: (Ganzzahl) Der vom Akteur basierend auf Ereignisantworten gesicherte Wert.</li></ul> |
| `actor` | String | Eine Person/ein Mitglied, die/das die Aktion ausgeführt hat. |
| `actorID` | String | Eine eindeutige Kennung für die Person/das Mitglied, die/das die Aktion ausgeführt hat. |
| `isKeyEvent` | Boolesch | Gibt an, ob dieses Ereignis ein Schlüsselereignis ist. |
| `name` | String | Der Name des Sitetools, z. B. Chatbot, Umfrage usw. |
| `section` | String | Der relevante Abschnitt des Sitetools wie Main oder Sub. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
