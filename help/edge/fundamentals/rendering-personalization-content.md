---
title: Rendern von personalisiertem Inhalt
seo-title: Adobe Experience Platform Web SDK – Rendern von personalisiertem Inhalt
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK rendern
seo-description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK rendern
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 24%

---


# Übersicht über die Personalisierungsoptionen

Die Adobe Experience Platform [!DNL Web SDK] unterstützt die Abfrage der Personalisierungslösungen bei Adobe, einschließlich Adobe Target. Es gibt zwei Arten der Personalisierung: Abrufen von Inhalten, die automatisch wiedergegeben werden können, und von Inhalten, die vom Entwickler wiedergegeben werden müssen. Das SDK bietet außerdem Funktionen zum [Verwalten von Flackern](../../edge/solution-specific/target/flicker-management.md).

## Inhalt automatisch wiedergeben

Das SDK rendert automatisch personalisierte Inhalte, wenn Sie ein Ereignis an den Server senden und `renderDecisions` als Option des Ereignisses auf `true` festlegen.

```javascript
alloy("sendEvent", {
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

Das Rendern personalisierter Inhalte erfolgt asynchron. Daher sollte es keine Annahme geben, wenn ein bestimmtes Inhaltselement Teil der Seite ist.

## Manuelles Wiedergeben von Inhalten

Sie können die Liste der Entscheidungen als Versprechen auf dem `event` Befehl anfordern, indem Sie `scopes`. Ein Gültigkeitsbereich ist eine Zeichenfolge, mit der die Personalisierungslösung wissen kann, welche Entscheidung Sie möchten.

```javascript
alloy("sendEvent",{
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

>[!TIP]
>
> Wenn Sie [!DNL Target] Scopes auf dem Server zu mBoxes machen, sind nur diese alle Anforderungen gleichzeitig und nicht einzeln. Die globale Mbox wird immer gesendet.

### Automatische Inhalte abrufen

Wenn Sie möchten, dass die automatisch renderbaren Entscheidungen `result.decisions` in den Bericht aufgenommen werden, können Sie `renderDecisions` auf &quot;false&quot;setzen und den speziellen Bereich einschließen `__view__`.
