---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;ExperienceEvent;Felder;Schemas;Schemas;Schemadesign;Schemafeldgruppe;Feldergruppe;
solution: Experience Platform
title: Schemafeldgruppe „Marketing-Details der Kampagne“
description: Erfahren Sie mehr über die Schemafeldgruppe „Campaign Marketing Details“.
exl-id: be08b38b-68a0-4a74-9b8f-0344a0637395
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 19%

---

# Schemafeldgruppe [!UICONTROL Campaign Marketing-])

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Marketing-Details für Kampagnen] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md), die zur Beschreibung von Marketing-Kampagneninformationen wie Kampagnengruppe, Name und Trackingcode verwendet wird.

![](../../images/field-groups/campaign-marketing-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `marketing` | [Marketing](../../data-types/marketing.md) | Ein Objekt, das Marketing-Kampagneninformationen wie Kampagnengruppe, Name und Trackingcode beschreibt. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
