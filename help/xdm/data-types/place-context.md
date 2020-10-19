---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;place context;placeContext;datatype;data-type;data type;
solution: Experience Platform
title: Kontextdatentyp platzieren
topic: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp "Kontext platzieren".
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 6%

---


# [!UICONTROL Kontextdatentyp] platzieren

[!UICONTROL &quot;Place context] &quot;ist ein standardmäßiger XDM-Datentyp, der die Position eines beobachteten Ereignisses beschreibt, einschließlich Point-of-Interest-Informationen und geografischer Koordinaten.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interaktion mit Zielpunkt]](./poi-interaction.md) | Beschreibt Details zur POI-Interaktion. |
| `activePOIs` | Array mit Details zum [[!UICONTROL Point-of-Interest]](./poi-details.md) | Beschreibt die POIs, die das Ereignis verursacht haben. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beschreibt den geografischen Ort, an dem das Erlebnis bereitgestellt wurde. |
| `localTime` | DateTime | Ein Zeitstempel im Format [RFC 339](https://tools.ietf.org/html/rfc3339) , der die Ortszeit mit einem angegebenen Zeitzonenversatz angibt. Das Formatierungsmuster ist `yyyy-MM-dd'T'HH:mm:ssXXX` (z. B. `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Ganzzahl | Der aktuelle lokale Zeitzonenoffset in Minuten von UTC für den `localTime` Wert. Dies sollte gegebenenfalls den aktuellen DST-Offset enthalten. |

Weitere Informationen zum Mixin finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)