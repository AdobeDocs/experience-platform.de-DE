---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Feldergruppe;
solution: Experience Platform
title: Feldergruppe "Kanaldetails"
description: Dieses Dokument bietet einen Überblick über die Feldergruppe Kanal-Details .
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 18%

---

# [!UICONTROL Kanaldetails] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Kanaldetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), mit dem Kanalinformationen wie ID, Kanaltyp, Medientyp und Standorttyp beschrieben werden.

![](../../images/field-groups/channel-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `channel` | [Erlebniskanal](../../data-types/experience-channel.md) | Ein Objekt, das die Produktrückgabe, die Registrierung der Garantie und die Warenkorb-/Bestellvorgänge beschreibt. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
