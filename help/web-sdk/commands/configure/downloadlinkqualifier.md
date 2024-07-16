---
title: downloadLinkQualifier
description: Hilft festzustellen, wie das automatische Linktracking Downloadlinks qualifiziert.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Wenn Sie das automatische Linktracking mit [`clickCollectionEnabled`](clickcollectionenabled.md) aktivieren, hilft die Eigenschaft `downloadLinkQualifier` bei der Bestimmung der Kriterien für eine URL, die als Downloadlink betrachtet werden soll.

Diese Eigenschaft ist eine Regex-Zeichenfolge. Wenn die angeklickte URL mit diesem Regex übereinstimmt, wird `xdm.web.webInteraction.type` auf `"download"` gesetzt. Links werden auch sofort als Downloadlink klassifiziert, wenn sie ein HTML-Attribut `download` enthalten. Wenn `clickCollectionEnabled` nicht aktiviert ist, hat diese Eigenschaft keine Auswirkung.

## Downloadlink-Qualifizierer mit der Web SDK-Tag-Erweiterung

Aktivieren Sie das Kontrollkästchen **[!UICONTROL Klick-Datenerfassung aktivieren]** und geben Sie dann den gewünschten Text unter **[!UICONTROL Link-Qualifizierer herunterladen]** ein, wenn [die Tag-Erweiterung konfigurieren](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenerfassung] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL Klick-Datenerfassung aktivieren]** .
1. Nach der Aktivierung wird das Textfeld **[!UICONTROL Link-Qualifizierer herunterladen]** angezeigt. Geben Sie den gewünschten Wert ein. Außerdem stehen Schaltflächen zum Testen des Regex und Wiederherstellen des Standardwerts zur Verfügung.
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Downloadlink-Qualifizierer mit der Web SDK JavaScript-Bibliothek

Legen Sie die Zeichenfolge `downloadLinkQualifier` fest, wenn Sie den Befehl `configure` ausführen. Wenn Sie diese Eigenschaft weglassen, wird standardmäßig der folgende Wert verwendet:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Wenn Sie zum Qualifizieren von Downloadlinks andere Kriterien verwenden möchten, setzen Sie diese Eigenschaft auf den gewünschten Regex-Wert.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": true,
  "downloadLinkQualifier": "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```
