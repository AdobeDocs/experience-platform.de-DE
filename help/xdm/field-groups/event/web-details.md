---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Feldergruppe;
solution: Experience Platform
title: Feldgruppe "Webdetails-Schema"
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Feldergruppe Webdetails .
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 4%

---


# [!UICONTROL Feldergruppe &quot;Web-] Details-Schema&quot;

>[!NOTE]
>
>Die Namen verschiedener Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md) .

[!UICONTROL Webdetails ] sind eine Standardschemafeldgruppe für die  [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md), die zur Beschreibung von Informationen zu Webdetailereignissen wie Interaktion, Seitendetails und Referrer verwendet wird.

![](../../images/field-groups/web-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `web` | [Webinformationen](../../data-types/web-information.md) | Beschreibt Link-Klicks, Webseitendetails, Referrer-Informationen und Browserdetails. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-web.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-web.schema.json)
