---
title: xdm
description: Das schemaorientierte Objekt, das an Adobe gesendet wird.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# `xdm`

Die `xdm` -Objekt enthält die an Adobe gesendete Daten-Payload. Die in diesem Objekt festgelegten Felder werden direkt den Elementen zugeordnet, die im Schema des Datensatzes definiert sind.

Adobe Experience Platform verwendet Schemas, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, die Bedeutung beizubehalten und somit aus Daten Nutzen zu ziehen.

Dieses Feld hat eine maximale Größe von 32 KB.

## Konfigurieren des XDM-Objekts mithilfe der Web SDK-Erweiterung

Legen Sie die **[!UICONTROL XDM]** in den Aktionen einer Tag-Regel. Die [XDM-Objekt](/help/tags/extensions/client/web-sdk/data-element-types.md#xdm-object) bietet eine intuitive Oberfläche, um andere Datenelemente ihren jeweiligen XDM-Feldern zuzuordnen.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Ereignis senden]**.
1. Stellen Sie das Datenelement bereit, das das gewünschte Objekt im **[!UICONTROL XDM]** -Feld.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## XDM-Objekt mithilfe der Web SDK-JavaScript-Bibliothek konfigurieren

Legen Sie die `xdm` -Objekt beim Ausführen der `sendEvent` Befehl. Stellen Sie sicher, dass die Hierarchie in diesem Objekt mit dem Schema für den konfigurierten Datensatz übereinstimmt. Sie können beide `xdm` und dem [`data`](data.md) -Objekt im selben `sendEvent` Befehl.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference)
});
```

Im folgenden Beispiel wird die [Feldergruppe &quot;Commerce-Details&quot;](/help/xdm/field-groups/event/commerce-details.md):

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
