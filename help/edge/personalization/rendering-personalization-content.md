---
title: Rendern von personalisiertem Inhalt
seo-title: Adobe Experience Platform Web SDK – Rendern von personalisiertem Inhalt
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK rendern
seo-description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK rendern
keywords: personalization;renderDecision;sendEvent;DecisionScopes;result.Decision;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 23%

---


# Übersicht über die Optionen zur Personalisierung

Adobe Experience Platform [!DNL Web SDK] unterstützt die Abfrage der Personalisierungslösungen bei der Adobe, einschließlich Adobe Target. Es gibt zwei Arten der Personalisierung: Abrufen von Inhalten, die automatisch wiedergegeben werden können, und von Inhalten, die vom Entwickler wiedergegeben werden müssen. Das SDK bietet außerdem Funktionen für [Flicker](../personalization/manage-flicker.md) verwalten.

## Automatisches Wiedergeben von Inhalten

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

## Manuelles Rendern von Inhalten

Sie können die Liste von Entscheidungen anfordern, die als Versprechen für den Befehl `sendEvent` zurückgegeben werden, indem Sie die Option `decisionScopes` angeben. Ein Gültigkeitsbereich ist eine Zeichenfolge, mit der die Personalisierungslösung wissen kann, welche Entscheidung Sie möchten.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
    }
  });
```

Dadurch wird eine Liste von Entscheidungen als JSON-Objekt für jede Entscheidung zurückgegeben.

```json
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
> Wenn Sie [!DNL Target] verwenden, werden Scopes auf dem Server zu mBoxes, nur sie werden gleichzeitig angefordert und nicht einzeln. Die globale Mbox wird immer gesendet.

### Abrufen von automatischem Inhalt

Wenn Sie möchten, dass `result.decisions` die automatisch renderbaren Entscheidungen enthält und sie NICHT automatisch wiedergegeben werden dürfen, können Sie `renderDecisions` auf `false` setzen und den Sonderbereich `__view__` einschließen.
