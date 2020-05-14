---
title: Rendern von personalisiertem Inhalt
seo-title: Adobe Experience Platform Web SDK – Rendern von personalisiertem Inhalt
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK rendern
seo-description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK rendern
translation-type: tm+mt
source-git-commit: 4bea14d18ce119bdec0d428f885d240f92244cfc
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 34%

---


# Übersicht über die Personalisierungsoptionen

Das Adobe Experience Platform Web SDK unterstützt die Abfrage der Personalisierungslösungen bei Adobe einschließlich Adobe Zielgruppe. Es gibt zwei Arten der Personalisierung: Abrufen von Inhalten, die automatisch wiedergegeben werden können, und von Inhalten, die vom Entwickler wiedergegeben werden müssen. Das SDK bietet außerdem Funktionen zum [Verwalten von Flackern](../../edge/solution-specific/target/flicker-management.md).

## Inhalt automatisch wiedergeben

Das SDK rendert automatisch personalisierte Inhalte, wenn Sie ein Ereignis an den Server senden und `renderDecisions` als Option des Ereignisses auf `true` festlegen.

```javascript
alloy("event", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

Die Wiedergabe personalisierter Inhalte erfolgt asynchron, sodass keine Annahme dazu möglich ist, wann ein bestimmtes Inhaltselement Teil der Seite ist.

## Manuelles Wiedergeben von Inhalten

Sie können die Liste der Entscheidungen als Versprechen auf dem `event` Befehl anfordern, indem Sie `scopes`. Ein Gültigkeitsbereich ist eine Zeichenfolge, mit der die Personalisierungslösung wissen kann, welche Entscheidung Sie möchten.

```javascript
alloy("event",{
    xdm:{...},
    scopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      //do something with the decisions
    }
  })
```

Dadurch wird eine Liste von Entscheidungen als JSON-Objekt für jede Entscheidung zurückgegeben.

```javascript
{
  "decisions": [
    {
      "id": "TNT:123456:0",
      "scope": "demo-1",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/html-content-item",
          "data": {
            "id": "11223344",
            "content": "<h2 style=\"color: yellow\">Scoped Decision for location \"alloy-location-1\"</h2>"
          }
        }
      ]
    },
    {
      "id": "TNT:654321:1",
      "scope": "demo-2",
      "items": [
        {
          "schema": "https://ns.adobe.com/personalization/json-content-item",
          "data": {
            "id": "4433221",
            "content": {
              "name":"Scoped decision in JSON"
            }
          }
        }
      ]
    }
  ]
}
```

{info}Wenn Sie Zielgruppen-Scopes verwenden, werden sie auf dem Server zu mBoxes, dann sind nur sie alle Anforderungen gleichzeitig und nicht einzeln. Die globale Mbox wird immer gesendet.
{info}

### Automatische Inhalte abrufen

Wenn Sie möchten, dass die automatischen `result.decisions` Rendering-Entscheidungen `renderDecisions` auf &quot;false&quot;gesetzt werden, können Sie den speziellen Bereich einschließen `__view__`
