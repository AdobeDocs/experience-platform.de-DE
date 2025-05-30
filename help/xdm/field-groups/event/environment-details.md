---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;ExperienceEvent;Felder;Schemata;Schemata;Schemadesign;Feldergruppe;Feldergruppe;Umgebung;Umgebungsdetails;
solution: Experience Platform
title: Schemafeldgruppe „Umgebungsdetails“
description: Erfahren Sie mehr über die Schemafeldgruppe „ExperienceEvent-Umgebungsdetails“.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 13%

---


# [!UICONTROL Umgebungsdetails] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Umgebungsdetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md), mit der Informationen zu Umgebungsdetails im Zusammenhang mit einem Erlebnisereignis wie Gerätedetails, Browser-Informationen, Ortszeit und andere geografische Informationen erfasst werden.

![](../../images/field-groups/environment-details.png){width=500}

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `device` | [Gerät](../../data-types/device.md) | Beschreibt eine identifizierte Geräte-, Anwendungs- oder Geräte-Browser-Instanz, die sitzungsübergreifend verfolgt werden kann, normalerweise durch Cookies. |
| `environment` | [Umgebung](../../data-types/environment.md) | Beschreibt Informationen zum situativen Kontext der Ereignisbeobachtung, insbesondere mit Details zu vorübergehenden Informationen wie Netzwerk- oder Softwareversionen. |
| `placeContext` | [Ortskontext](../../data-types/place-context.md) | Beschreibt die vorübergehenden Umstände im Zusammenhang mit der Ereignisbeobachtung. Beispiele sind gebietsschemaspezifische Informationen wie Wetter, Ortszeit, Verkehr, Wochentag, Werktag vs. Urlaub und Arbeitszeit. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
