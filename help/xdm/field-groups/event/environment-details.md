---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;ExperienceEvent;Felder;Schemas;Schemas;Schema-Design;Feldgruppe;Feldgruppe;Umgebung;Umgebung;
solution: Experience Platform
title: Umgebung Details Schema Feldgruppe
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über die Feldgruppe ExperienceEvent Umgebung Details Schema.
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 3%

---


# [!UICONTROL Feldgruppe &quot;] Umgebung Detailsschema&quot;

>[!NOTE]
>
>Die Namen mehrerer Schema-Feldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md).

[!UICONTROL Umgebung ] Details ist eine Standardfeldgruppe für Schema für die  [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) Klasse, mit der Informationen zu Umgebung in Bezug auf ein Erlebnis-Ereignis wie Gerätedetails, Browserinformationen, Ortszeit und andere geografische Informationen erfasst werden.

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `device` | [Gerät](../../data-types/device.md) | Beschreibt eine identifizierte Geräte-, Anwendungs- oder Gerätebrowserinstanz, die sitzungsübergreifend verfolgt werden kann (normalerweise mit Cookies). |
| `environment` | [Umgebung](../../data-types/environment.md) | Beschreibt Informationen zum situationsspezifischen Kontext der Ereignis-Beobachtung, insbesondere Informationen zu vorübergehenden Informationen wie Netzwerk- oder Softwareversionen. |
| `placeContext` | [Ortskontext](../../data-types/place-context.md) | Beschreibt die vorübergehenden Umstände im Zusammenhang mit der Ereignis-Beobachtung. Beispiele für Gebietsschemaspezifische Informationen wie Wetter, Ortszeit, Traffic, Wochentag, Arbeitstag oder Urlaub und Arbeitszeit. |

Weitere Informationen zur Feldgruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
