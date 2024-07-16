---
title: xdm
description: Erfahren Sie, wie Sie Daten über das schemaorientierte XDM-Objekt an Adobe senden.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# `xdm`

Das Objekt `xdm` enthält die an Adobe gesendete Daten-Payload. Die in diesem Objekt festgelegten Felder werden direkt den Elementen zugeordnet, die im Schema des Datensatzes definiert sind.

Adobe Experience Platform verwendet Schemas, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, die Bedeutung beizubehalten und somit aus Daten Nutzen zu ziehen.

Dieses Objekt hat eine maximale Größe von 32 KB.

## Konfigurieren des XDM-Objekts mithilfe der Web SDK-Erweiterung

Legen Sie das Objekt **[!UICONTROL XDM]** innerhalb der Aktionen einer Tag-Regel fest. Das [XDM-Objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) bietet eine intuitive Benutzeroberfläche zum Zuordnen anderer Datenelemente zu ihren jeweiligen XDM-Feldern.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Aktionen] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den Aktionstyp ] auf **[!UICONTROL Ereignis senden]** fest.[!UICONTROL 
1. Stellen Sie das Datenelement bereit, das das gewünschte Objekt im Feld **[!UICONTROL XDM]** enthält.
1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Konfigurieren des XDM-Objekts mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie das Objekt `xdm` beim Ausführen des Befehls `sendEvent` fest. Stellen Sie sicher, dass die Hierarchie in diesem Objekt mit dem Schema für den konfigurierten Datensatz übereinstimmt. Sie können sowohl das Objekt `xdm` als auch das Objekt [`data`](data.md) im selben Befehl `sendEvent` einbeziehen.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

Im folgenden Beispiel wird die Schemafeldergruppe [Commerce Details ](/help/xdm/field-groups/event/commerce-details.md) verwendet:

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
