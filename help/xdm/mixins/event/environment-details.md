---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;environment;environment details;
solution: Experience Platform
title: ExperienceEvent-Umgebung-Details-Mixin
topic: overview
description: Dieses Dokument bietet einen Überblick über das ExperienceEvent Umgebung Details-Mixin.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 4%

---


# [!UICONTROL ExperienceEvent Umgebung Details] mixen

[!UICONTROL Die ExperienceEvent-Umgebung-Details] ist ein Standardmixin für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/individual-profile.md) , mit der Informationen zu Umgebung in Bezug auf ein Experience-Ereignis erfasst werden, z. B. Gerätedetails, Browserinformationen, Ortszeit und andere geografische Informationen.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `device` | [Gerät](../../data-types/device.md) | Beschreibt eine identifizierte Geräte-, Anwendungs- oder Gerätebrowserinstanz, die sitzungsübergreifend verfolgt werden kann (normalerweise mit Cookies). |
| `environment` | [Umgebung](../../data-types/environment.md) | Beschreibt Informationen zum situationsspezifischen Kontext der Ereignis-Beobachtung, insbesondere Informationen zu vorübergehenden Informationen wie Netzwerk- oder Softwareversionen. |
| `placeContext` | [Ortskontext](../../data-types/place-context.md) | Beschreibt die vorübergehenden Umstände im Zusammenhang mit der Ereignis-Beobachtung. Beispiele für Gebietsschemaspezifische Informationen wie Wetter, Ortszeit, Traffic, Wochentag, Arbeitstag oder Urlaub und Arbeitszeit. |

Weitere Informationen zum Mixin finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
