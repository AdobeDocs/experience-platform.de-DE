---
title: Datenerfassung
description: Erfahren Sie, wie die Adobe Experience Platform Edge Network Server-API die erfassten Daten strukturiert.
seo-description: Learn how the Adobe Experience Platform Edge Network Server API structures the collected data
keywords: Datenerfassung;Datenerfassung;Adobe Experience Platform Edge Network;API;Struktur
source-git-commit: 2b501c9384fecb016489a21a308a595186153f03
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 8%

---


# Datenerfassung

Die [!DNL Server API] bietet zwei Arten von Datenerfassungs-Endpunkten:

* [Endpunkte der interaktiven Datenerfassung](interactive-data-collection.md)verwendet wird, wenn der Client erwartet, dass eine Antwort vom Server zurückgegeben wird. Diese Endpunkte können bei der Datenerfassung auch Inhalte von anderen Edge Network-Diensten zurückgeben.
* [Nicht interaktive Ereignisdatenerfassung](non-interactive-data-collection.md)verwendet, wenn vom Server keine Antwort erwartet wird. Diese Endpunkte werden nur für die Datenerfassung verwendet.

## `Event` -Objekt {#event-object}

Von der [!DNL Server API] ist in der `Event` -Objekt. Die Struktur dieses Objekts wird nachfolgend beschrieben.

```json
{
   "xdm":{
      "identityMap":{
         "Email_LC_SHA256":[
            {
               "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
               "primary":true
            }
         ]
      },
      "eventType":"web.webpagedetails.pageViews",
      "web":{
         "webPageDetails":{
            "URL":"https://alloystore.dev/",
            "name":"home-demo-Home Page",
            "pageViews":{
               "value":1
            }
         }
      },
      "placeContext":{
         "localTime":"2021-08-09T17:09:20.859+03:00",
         "localTimezoneOffset":-180
      },
      "timestamp":"2021-08-09T14:09:20.859Z"
   },
   "data":{
      "prop1":"custom value",
      "var10":"search (organic)"
   }
}
```

| Attribut | Typ | Beschreibung |
| --- | --- | --- |
| `xdm` | Objekt | *Erforderlich*. JSON-Objekt, das Daten im XDM-Format enthält, die dem Datensatzschema entsprechen. |
| `data` | Objekt | *Optional*. JSON-Objekt mit Freiformdaten, die vom Edge Network XDM zugeordnet werden können. |

