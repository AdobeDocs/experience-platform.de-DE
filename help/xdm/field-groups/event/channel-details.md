---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Feldergruppe;
solution: Experience Platform
title: Feldergruppe "Kanaldetails"
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Feldergruppe Kanal-Details .
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# [!UICONTROL Feldergruppe ] &quot;Channel Details Schema&quot;

>[!NOTE]
>
>Die Namen verschiedener Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md) .

[!UICONTROL Kanaldetails ] sind eine Standardschemafeldgruppe für die  [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md), die zur Beschreibung von Kanalinformationen wie ID, Kanaltyp, Medientyp und Standorttyp verwendet wird.

![](../../images/field-groups/channel-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `channel` | [Experience-Kanal](../../data-types/experience-channel.md) | Ein Objekt, das die Produktrückgabe, die Registrierung der Garantie und die Warenkorb-/Bestellvorgänge beschreibt. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
