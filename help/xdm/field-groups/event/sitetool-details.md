---
title: SiteTool-Details-Schema-Feldergruppe
description: Erfahren Sie mehr über die Feldergruppe Sitetool-Details .
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 6%

---

# [!UICONTROL Sitetool-Details] Schemafeldgruppe

[!UICONTROL Sitetool-Details] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe stellt eine einzelne `sitetool` -Objekt auf ein Schema verweist, das Informationen erfasst, die von einem Sitetool erfasst werden.

![Feldgruppenstruktur](../../images/field-groups/sitetool-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `dataGatheringEvent` | Objekt | Gibt an, ob es sich bei diesem Ereignis um ein Datenerfassungsereignis zusammen mit anderen zugehörigen Details handelt. Enthält die folgenden Eigenschaften:<ul><li>`data`: (Zuordnung) Enthält die JSON-Daten, die im Rahmen des Umfrage-, Umfrage- oder Umfrageeinreichungsereignisses erfasst und gesendet werden.</li><li>`isTrue`: (Boolesch) Gibt an, ob es sich bei diesem Ereignis um ein Datenerfassungsereignis wie Quiz, Umfrage oder Umfrage handelt.</li><li>`score`: (Integer) Die durch den Schauspieler anhand von Ereignisantworten gesicherte Punktzahl.</li></ul> |
| `actor` | Zeichenfolge | Eine Person/ein Mitglied, die/das die Aktion ausgeführt hat. |
| `actorID` | Zeichenfolge | Eine eindeutige Kennung für die Person/das Mitglied, die die Aktion ausgeführt hat. |
| `isKeyEvent` | Boolesch | Gibt an, ob dieses Ereignis ein Schlüsselereignis ist. |
| `name` | Zeichenfolge | Der Name des Sitetools, z. B. Chat-Bot, Umfrage usw. |
| `section` | Zeichenfolge | Der relevante Abschnitt des Sitetools wie Haupt- oder Unterabschnitt. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
