---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Ortskontext;PlaceContext;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Kontextdatentyp platzieren
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp "Kontext platzieren".
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# [!UICONTROL Datentyp ] &quot;contextData&quot;platzieren

[!UICONTROL Platzieren Sie ] contextis einen standardmäßigen XDM-Datentyp, der die Position eines beobachteten Ereignisses beschreibt, einschließlich Point-of-Interest-Informationen und geografischen Koordinaten.

<img src="../images/data-types/place-context.png" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL Interaktion mit Zielpunkt]](./poi-interaction.md) | Beschreibt Details zur POI-Interaktion. |
| `activePOIs` | Array von [[!UICONTROL Details zum Zielpunkt]](./poi-details.md) | Beschreibt die POIs, die das Ereignis verursacht haben. |
| `geo` | [[!UICONTROL Geo]](./geo.md) | Beschreibt den geografischen Ort, an dem das Erlebnis bereitgestellt wurde. |
| `localTime` | DateTime | Ein Zeitstempel im Format [RFC 3339](https://tools.ietf.org/html/rfc3339), der die Ortszeit mit einem angegebenen Zeitzonenversatz angibt. Das Formatierungsmuster ist `yyyy-MM-dd'T'HH:mm:ssXXX` (z. B. `2001-07-04T12:08:56-07:00`). |
| `localTimezoneOffset` | Ganzzahl | Der aktuelle lokale Zeitzonenoffset in Minuten von UTC für den Wert `localTime`. Dies sollte gegebenenfalls den aktuellen DST-Offset enthalten. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
