---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Umgebung; Umgebungsdetails;
solution: Experience Platform
title: Feldergruppe "Umgebungsdetails"
description: Erfahren Sie mehr über die Feldergruppe ExperienceEvent Environment Details .
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 13%

---


# [!UICONTROL Umgebungsdetails] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Umgebungsdetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) zum Erfassen von Informationen zu Umgebungsdetails im Zusammenhang mit einem Erlebnisereignis wie Gerätedetails, Browserinformationen, lokaler Zeit und anderen geografischen Informationen.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `device` | [Gerät](../../data-types/device.md) | Beschreibt eine identifizierte Geräte-, Anwendungs- oder Geräte-Browser-Instanz, die sitzungsübergreifend verfolgt werden kann, normalerweise durch Cookies. |
| `environment` | [Umgebung](../../data-types/environment.md) | Beschreibt Informationen zum situationsspezifischen Kontext der Ereignisüberwachung, insbesondere mit detaillierten Informationen zu vorübergehenden Informationen wie Netzwerk- oder Softwareversionen. |
| `placeContext` | [Ortskontext](../../data-types/place-context.md) | Beschreibt die vorübergehenden Umstände im Zusammenhang mit der Ereignisbeobachtung. Beispiele sind gebietsschemaspezifische Informationen wie Wetter, Ortszeit, Traffic, Wochentag, Werktag vs. Urlaub und Arbeitszeit. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
