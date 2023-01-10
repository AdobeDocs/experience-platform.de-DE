---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Feldergruppe;
solution: Experience Platform
title: Feldgruppe "Campaign Marketing Details"
description: Dieses Dokument bietet einen Überblick über die Schemakontrolle des Campaign-Marketing-Details-Schemas.
exl-id: be08b38b-68a0-4a74-9b8f-0344a0637395
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 18%

---

# [!UICONTROL Kampagnen-Marketingdetails] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Kampagnen-Marketingdetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md)verwendet, um Marketing-Kampagneninformationen wie Kampagnengruppe, Name und Trackingcode zu beschreiben.

![](../../images/field-groups/campaign-marketing-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `marketing` | [Marketing](../../data-types/marketing.md) | Ein Objekt, das Informationen zu Marketing-Kampagnen wie Kampagnengruppe, Name und Trackingcode beschreibt. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)
