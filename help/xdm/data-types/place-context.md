---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;XDM;Felder;Schemata;Schemata;Ortskontext;placeContext;datatype;Datentyp;Datentyp;
solution: Experience Platform
title: Kontextdatentyp platzieren
description: Erfahren Sie mehr über den XDM-Datentyp „Ortskontext“.
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 3%

---

# [!UICONTROL Ortskontext] Datentyp

[!UICONTROL Ortskontext] ist ein standardmäßiger XDM-Datentyp, der den Ort eines beobachteten Ereignisses beschreibt, einschließlich POI-Informationen und geografischer Koordinaten.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interaktion mit Point of Interest]](./poi-interaction.md) | Beschreibt Details zur POI-Interaktion (Point of Interest). |
| `activePOIs` | Array [[!UICONTROL Point of Interest-Details]](./poi-details.md) | Beschreibt die POIs, die das Ereignis verursacht haben. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beschreibt den geografischen Ort, an dem das Erlebnis bereitgestellt wurde. |
| `localTime` | DateTime | Ein Zeitstempel im [RFC 3339](https://tools.ietf.org/html/rfc3339)-Format, der die lokale Zeit mit einem angegebenen Zeitzonenversatz angibt. Das Formatierungsmuster ist `yyyy-MM-dd'T'HH:mm:ssXXX` (z. B. `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Ganzzahl | Der aktuelle lokale Zeitzonenversatz in Minuten von UTC für den `localTime`. Dies sollte gegebenenfalls den aktuellen DST-Offset enthalten. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
