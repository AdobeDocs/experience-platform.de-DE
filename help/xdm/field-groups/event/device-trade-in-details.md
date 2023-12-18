---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; ExperienceEvent; Felder; Schemas; Schemas; Schemadesign; Feldergruppe; Feldergruppe; Gerät; Handel; Handel; Handel; Handel; Handel;
solution: Experience Platform
title: Schema-Feldergruppe "Device Trade-in-Details"
description: Erfahren Sie mehr über die Schemafeldgruppe "Gerätehandelsdetails".
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 18%

---

# [!UICONTROL Details zum Gerätehandel] Schemafeldgruppe

>[!NOTE]
>
>Die Namen mehrerer Schemafeldgruppen wurden geändert. Weitere Informationen finden Sie im Dokument zu den [Namensaktualisierungen für Feldgruppen](../name-updates.md).

[!UICONTROL Details zum Gerätehandel] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Es bietet ein einzelnes Feld (`deviceTradeInDetails`), die eine Transaktion mit Geräten beschreibt, einschließlich des Handelswerts, der ursprünglichen Geräte-ID und der neuen Geräte-ID.

![Struktur der Details zum Geräteaustausch](../../images/field-groups/device-trade-in-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `tradeInValue` | [Währung](../../data-types/currency.md) | Der -Wert des Geräts, auf das gehandelt wird. |
| `newDeviceID` | Zeichenfolge | Die ID des neuen Geräts, für das gehandelt wird. |
| `originalDeviceID` | Zeichenfolge | Die ID des Geräts, auf dem gehandelt wird. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
