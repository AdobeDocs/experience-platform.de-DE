---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;ExperienceEvent;Felder;Schemata;Schemata;Schemadesign;Feldergruppe;Feldergruppe;Gerät;Handel;Handel in;Handel in;
solution: Experience Platform
title: Schemafeldgruppe „Details zum Gerätehandel“
description: Erfahren Sie mehr über die Schemafeldgruppe „Details zum Gerätehandel“.
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

[!UICONTROL Details zum Gerätehandel] ist eine standardmäßige Schemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Es bietet ein einzelnes Feld (`deviceTradeInDetails`), das eine Transaktion zum Inzahlungnehmen eines Geräts beschreibt, einschließlich Inzahlungswert, ursprünglicher Geräte-ID und neuer Geräte-ID.

![Struktur der Inzahlungsdetails für Geräte](../../images/field-groups/device-trade-in-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `tradeInValue` | [Währung](../../data-types/currency.md) | Der Wert des zu tauschenden Geräts. |
| `newDeviceID` | String | Die ID des neuen Geräts, für das eingetauscht wird. |
| `originalDeviceID` | String | Die ID des zu tauschenden Geräts. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
