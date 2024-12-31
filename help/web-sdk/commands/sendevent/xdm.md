---
title: XDM
description: Erfahren Sie, wie Sie Daten über das XDM-Schema-Alignment-Objekt an Adobe senden.
exl-id: 1d8ef191-aed6-4c8b-a1fd-614bd8ed73da
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# `xdm`

Das `xdm`-Objekt enthält die Daten-Payload, die an Adobe gesendet wird. Felder, die in diesem Objekt festgelegt sind, werden direkt Elementen zugeordnet, die im Schema des Datensatzes definiert sind.

Adobe Experience Platform verwendet Schemata, um die Struktur von Daten konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, deren Bedeutung beizubehalten und somit Wert aus Daten zu ziehen.

Dieses Objekt hat eine maximale Größe von 32 KB.

## Konfigurieren des XDM-Objekts mithilfe der Web SDK-Erweiterung

Legen Sie das **[!UICONTROL XDM]**-Objekt in den Aktionen einer Tag-Regel fest. Das [XDM-Objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) bietet eine intuitive Benutzeroberfläche zum Zuordnen anderer Datenelemente zu ihren jeweiligen XDM-Feldern.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL  unter &quot;]&quot; eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das [!UICONTROL Erweiterung] Dropdown-Feld auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und legen Sie den [!UICONTROL Aktionstyp] auf **[!UICONTROL Ereignis senden]**.
1. Geben Sie das Datenelement an, das das gewünschte Objekt im Feld **[!UICONTROL XDM]** enthält.
1. Klicken Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

## Konfigurieren des XDM-Objekts mithilfe der Web SDK JavaScript-Bibliothek

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
