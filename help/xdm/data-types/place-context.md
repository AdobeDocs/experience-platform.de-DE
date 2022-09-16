---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Ortskontext; placeContext; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Kontextdatentyp platzieren
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den XDM-Datentyp "Kontext platzieren".
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 14%

---

# [!UICONTROL Ortskontext] Datentyp

[!UICONTROL Ortskontext] ist ein standardmäßiger XDM-Datentyp, der den Standort eines beobachteten Ereignisses beschreibt, einschließlich Point-of-Interest-Informationen und geografischen Koordinaten.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interaktion mit Zielpunkten]](./poi-interaction.md) | Beschreibt Details zur POI-Interaktion. |
| `activePOIs` | Array von [[!UICONTROL Details zum POI]](./poi-details.md) | Beschreibt die POIs, die das Ereignis verursacht haben. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beschreibt den geografischen Ort, an dem das Erlebnis bereitgestellt wurde. |
| `localTime` | DateTime | Ein Zeitstempel in [RFC 3339](https://tools.ietf.org/html/rfc3339) Format, das die Ortszeit mit einem angegebenen Zeitzonenversatz angibt. Das Formatierungsmuster lautet `yyyy-MM-dd'T'HH:mm:ssXXX` (z. B. `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Ganzzahl | Der aktuelle lokale Zeitzonenversatz in Minuten von UTC für die `localTime` -Wert. Dies sollte ggf. den aktuellen DST-Versatz enthalten. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
