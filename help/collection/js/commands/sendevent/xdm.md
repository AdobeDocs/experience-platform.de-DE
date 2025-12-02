---
title: XDM
description: Erfahren Sie, wie Sie Daten über das XDM-Schema-Alignment-Objekt an Adobe senden.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# `xdm`

Das `xdm`-Objekt enthält die Daten-Payload, die an Adobe gesendet werden. Felder, die in diesem Objekt festgelegt sind, werden direkt Elementen zugeordnet, die im Schema des Datensatzes definiert sind.

Adobe Experience Platform verwendet Schemata, um die Struktur von Daten konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, deren Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Legen Sie das `xdm` beim Ausführen des `sendEvent` fest. Stellen Sie sicher, dass die Hierarchie in diesem Objekt mit dem Schema für den konfigurierten Datensatz übereinstimmt. Sie können sowohl das `xdm`- als auch das [`data`](data.md)-Objekt in denselben `sendEvent`-Befehl aufnehmen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

Im folgenden Beispiel wird die Schemafeldgruppe [Commerce-Details verwendet](/help/xdm/field-groups/event/commerce-details.md):

```javascript
alloy("sendEvent",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large field hat",
      },
      {
        "SKU":"HT104",
        "name":"Small field hat",
      }
    ]
  }
});
```

## Verwenden des `xdm`-Objekts mithilfe der Tag-Erweiterung „Web SDK&quot;

Das `xdm`-Objekt ist bei Verwendung [&#x200B; Tag-Erweiterung „Web SDK](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) entweder als [Variablendatenelement“ oder &#x200B;](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object)XDM-Objektdatenelement“ verfügbar. Adobe empfiehlt in den meisten Fällen die Verwendung eines variablen Datenelements.
