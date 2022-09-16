---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Feldergruppe;
solution: Experience Platform
title: Feldgruppe "Webdetails-Schema"
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Feldergruppe Webdetails .
exl-id: eb42606b-ade4-4d72-b601-c560009c98e8
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 13%

---

# [!UICONTROL Webdetails] Schemafeldgruppe

>[!NOTE]
>
>Die Namen verschiedener Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Webdetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md)verwendet, um Informationen zu Webdetailereignissen wie Interaktion, Seitendetails und Referrer zu beschreiben.

![](../../images/field-groups/web-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `web` | [Web-Informationen](../../data-types/web-information.md) | Beschreibt Link-Klicks, Webseitendetails, Referrer-Informationen und Browserdetails. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.schema.json)
