---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;ExperienceEvent;Felder;Schemas;Schemas;Schema-Design;mixin;mixin;Umgebung;Umgebung Details;
solution: Experience Platform
title: Umgebung Details Mixin
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über das ExperienceEvent Umgebung Details-Mixin.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 4%

---

# [!UICONTROL Umgebung ] Detailsmixin

>[!NOTE]
>
>Die Namen mehrerer Mixins haben sich geändert. Weitere Informationen finden Sie im Dokument [mixin name updates](../name-updates.md).

[!UICONTROL Umgebung ] Details ist ein Standardmixin für die  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) Klasse, mit der Informationen zu Umgebung in Bezug auf ein Experience Ereignis erfasst werden, z. B. Gerätedetails, Browserinformationen, Ortszeit und andere geografische Informationen.

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `device` | [Gerät](../../data-types/device.md) | Beschreibt eine identifizierte Geräte-, Anwendungs- oder Gerätebrowserinstanz, die sitzungsübergreifend verfolgt werden kann (normalerweise mit Cookies). |
| `environment` | [Umgebung](../../data-types/environment.md) | Beschreibt Informationen zum situationsspezifischen Kontext der Ereignis-Beobachtung, insbesondere Informationen zu vorübergehenden Informationen wie Netzwerk- oder Softwareversionen. |
| `placeContext` | [Ortskontext](../../data-types/place-context.md) | Beschreibt die vorübergehenden Umstände im Zusammenhang mit der Ereignis-Beobachtung. Beispiele für Gebietsschemaspezifische Informationen wie Wetter, Ortszeit, Traffic, Wochentag, Arbeitstag oder Urlaub und Arbeitszeit. |

Weitere Informationen zum Mixin finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
