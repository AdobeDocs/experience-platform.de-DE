---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Gerät; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Marketing-Datentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Marketing-XDM-Datentyp.
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 7%

---


#  Marketing-Datentyp

 Marketing ist ein Standard-XDM-Datentyp, der Marketing-Aktivitäten beschreibt, die mit einem bestimmten Touchpoint aktiv sind.

![](../images/data-types/marketing.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `campaignGroup` | Zeichenfolge | Der Name der Kampagnengruppe (in Fällen, in denen mehrere Kampagnen gruppiert sind, z. B. `50%_DISCOUNT`). |
| `campaignName` | Zeichenfolge | Der Name der Marketing-Kampagne, z. B. `50%_DISCOUNT_USA` oder `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Zeichenfolge | Der Trackingcode, mit dem die Marketing-Kampagne identifiziert werden kann, mit der das Ereignis verknüpft ist. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
