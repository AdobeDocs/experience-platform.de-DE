---
title: Media Analytics-Tracker abrufen
description: Exportiert die ältere Media-API in ein Fensterobjekt.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---

# Abrufen von Media Analytics Tracker

Die **[!UICONTROL Get Media Analytics tracker]** Aktion wird verwendet, um die veraltete Media Analytics-API abzurufen. Wenn Sie die Aktion konfigurieren und einen Objektnamen angeben, wird die veraltete Media Analytics-API in dieses Fensterobjekt exportiert. Diese Aktion ist nützlich, um von veralteten Media Analytics zu Streaming Media Analytics zu wechseln.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Rules]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Actions] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das Dropdown-Feld [!UICONTROL Extension] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und dann den [!UICONTROL Action type] auf **[!UICONTROL Get Media Analytics tracker]** fest.

![Bild der Experience Platform-Benutzeroberfläche mit dem Aktionstyp „Media Analytics-Tracker abrufen“](../assets/get-media-analytics-tracker.png)

Diese Aktion enthält ein einzelnes Feld, das Sie konfigurieren können:

* **[!UICONTROL Export the Media Legacy API to this window object]**: Wählt das gewünschte Objekt für den Export der Media Legacy-API aus. Wenn keine angegeben wird, exportiert die Aktion die API nach `window.Media`.
