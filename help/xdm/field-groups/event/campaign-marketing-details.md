---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Feldergruppe;
solution: Experience Platform
title: Feldgruppe "Campaign Marketing Details"
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Schemakontrolle des Campaign-Marketing-Details-Schemas.
exl-id: be08b38b-68a0-4a74-9b8f-0344a0637395
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 5%

---

# [!UICONTROL Feldergruppe ] &quot;Campaign Marketing Details&quot;

>[!NOTE]
>
>Die Namen verschiedener Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md) .

[!UICONTROL Kampagnenmarketing-] Details sind eine Standardschemafeldgruppe für die  [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md), die zur Beschreibung von Marketingkampagneninformationen wie Kampagnengruppe, Name und Trackingcode verwendet wird.

![](../../images/field-groups/campaign-marketing-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `marketing` | [Marketing](../../data-types/marketing.md) | Ein Objekt, das Informationen zu Marketing-Kampagnen wie Kampagnengruppe, Name und Trackingcode beschreibt. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
