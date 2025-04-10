---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Gerät;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Marketing-Datentyp
description: Erfahren Sie mehr über den XDM-Datentyp Marketing.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---

# [!UICONTROL Marketing] Datentyp

[!UICONTROL Marketing] ist ein standardmäßiger XDM-Datentyp, der Marketing-Aktivitäten beschreibt, die mit einem bestimmten Touchpoint aktiv sind.

![](../images/data-types/marketing.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `campaignGroup` | Zeichenfolge | Der Name der Kampagnengruppe (wenn mehrere Kampagnen wie `50%_DISCOUNT` gruppiert sind). |
| `campaignName` | String | Der Name der Marketing-Kampagne, z. B. `50%_DISCOUNT_USA` oder `50%_DISCOUNT_ASIA`. |
| `trackingCode` | String | Der Trackingcode, mit dem die Marketing-Kampagne identifiziert werden kann, mit der das Ereignis verknüpft ist. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
