---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Ortskontext; placeContext; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Kontextdatentyp platzieren
description: Erfahren Sie mehr über den XDM-Datentyp "Kontext".
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 3%

---

# Datentyp [!UICONTROL Kontext platzieren]

[!UICONTROL Ortskontext] ist ein standardmäßiger XDM-Datentyp, der den Standort eines beobachteten Ereignisses beschreibt, einschließlich Point-of-Interest-Informationen und geografischen Koordinaten.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interaktion mit Zielpunkten]](./poi-interaction.md) | Beschreibt Details zur POI-Interaktion. |
| `activePOIs` | Array von [[!UICONTROL Details zum POI]](./poi-details.md) | Beschreibt die POIs, die das Ereignis verursacht haben. |
| `geo` | [[!UICONTROL geo]](./geo.md) | Beschreibt den geografischen Ort, an dem das Erlebnis bereitgestellt wurde. |
| `localTime` | DateTime | Ein Zeitstempel im Format [RFC 339](https://tools.ietf.org/html/rfc3339), der die lokale Zeit angibt, die mit einem angegebenen Zeitzonenversatz verwendet wird. Das Formatierungsmuster ist `yyyy-MM-dd'T'HH:mm:ssXXX` (z. B. `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Ganzzahl | Der aktuelle lokale Zeitzonenversatz in Minuten von UTC für den Wert `localTime`. Dies sollte ggf. den aktuellen DST-Versatz enthalten. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
