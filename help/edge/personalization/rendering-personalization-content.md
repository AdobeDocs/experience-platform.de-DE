---
title: Rendern von personalisiertem Inhalt
seo-title: Adobe Experience Platform Web SDK – Rendern von personalisiertem Inhalt
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK rendern
seo-description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK rendern
keywords: personalization;renderDecisions;sendEvent;decisionScopes;result.decisions;
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 23%

---


# Übersicht über die Optionen zur Personalisierung

Das Adobe Experience Platform [!DNL Web SDK] unterstützt die Abfrage von Personalisierungslösungen bei der Adobe, einschließlich Adobe Target. Es gibt zwei Arten der Personalisierung: Abrufen von Inhalten, die automatisch wiedergegeben werden können, und von Inhalten, die vom Entwickler wiedergegeben werden müssen. Das SDK bietet außerdem Funktionen zum [Verwalten von Flackern](../personalization/manage-flicker.md).

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

Sie können die Liste von Entscheidungen als Versprechen auf dem `sendEvent` Befehl anfordern, indem Sie die `decisionScopes` Option angeben. Ein Gültigkeitsbereich ist eine Zeichenfolge, mit der die Personalisierungslösung wissen kann, welche Entscheidung Sie möchten.

```javascript
alloy("sendEvent",{
    xdm:{...},
    decisionScopes:['demo-1', 'demo-2']
  }).then(function(result){
    if (result.decisions){
      // Do something with the decisions.
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
> Wenn Sie Scopes verwenden [!DNL Target], werden sie auf dem Server zu mBoxes, nur sie werden sofort angefordert und nicht einzeln. Die globale Mbox wird immer gesendet.

### Abrufen von automatischem Inhalt

Wenn Sie möchten, dass die automatisch renderbaren Entscheidungen `result.decisions` in die Datei aufgenommen werden und sie NICHT automatisch gerendert werden dürfen, können Sie sie auf `renderDecisions` und den speziellen Bereich einschließen `false``__view__`.
