---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schema-Design; Feldergruppe; Feldergruppe; Gerät; Handel; Handel; Handel; Handel in;
solution: Experience Platform
title: Schema-Feldergruppe "Device Trade-in-Details"
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Schemakonferenz für das Schema "Device Trade-In Details".
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 5%

---

# [!UICONTROL Feldgruppe &quot;Device Trade-In ] Detailsschema&quot;

>[!NOTE]
>
>Die Namen verschiedener Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu [Feldgruppennamenupdates](../name-updates.md) .

[!UICONTROL Device Trade-In-] Details sind eine Standardschemafeldgruppe für die  [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Es wird ein einzelnes Feld (`deviceTradeInDetails`) bereitgestellt, in dem eine Transaktion zwischen Geräten beschrieben wird, einschließlich des Handelswerts, der ursprünglichen Geräte-ID und der neuen Geräte-ID.

![Struktur der Details zum Geräteaustausch](../../images/field-groups/device-trade-in-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `tradeInValue` | [Währung](../../data-types/currency.md) | Der -Wert des Geräts, auf das gehandelt wird. |
| `newDeviceID` | Zeichenfolge | Die ID des neuen Geräts, für das gehandelt wird. |
| `originalDeviceID` | Zeichenfolge | Die ID des Geräts, auf dem gehandelt wird. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
