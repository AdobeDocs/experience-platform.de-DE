---
title: downloadLinkQualifier
description: Hilft festzustellen, wie das automatische Linktracking Downloadlinks qualifiziert.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Wenn Sie das automatische Linktracking mit [`clickCollectionEnabled`](clickcollectionenabled.md), die `downloadLinkQualifier` -Eigenschaft hilft bei der Bestimmung der Kriterien für eine URL, die als Downloadlink betrachtet werden soll.

Diese Eigenschaft ist eine Regex-Zeichenfolge. Wenn die angeklickte URL diesem Regex entspricht, `xdm.web.webInteraction.type` auf `"download"`. Links werden auch sofort als Downloadlink klassifiziert, wenn sie eine `download` HTML-Attribut. Wenn `clickCollectionEnabled` nicht aktiviert ist, hat diese Eigenschaft keine Auswirkung.

## Downloadlink-Qualifizierer mit der Web SDK-Tag-Erweiterung

Aktivieren Sie die **[!UICONTROL Aktivieren der Klickdatenerfassung]** und geben Sie den gewünschten Text unter ein. **[!UICONTROL Downloadlink-Qualifizierer]** when [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Datenerfassung] und wählen Sie das Kontrollkästchen aus. **[!UICONTROL Aktivieren der Klickdatenerfassung]**.
1. Nach der Aktivierung wird die **[!UICONTROL Downloadlink-Qualifizierer]** Textfeld angezeigt. Geben Sie den gewünschten Wert ein. Außerdem stehen Schaltflächen zum Testen des Regex und Wiederherstellen des Standardwerts zur Verfügung.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Downloadlink-Qualifizierer mit der JavaScript-Bibliothek des Web SDK

Legen Sie die `downloadLinkQualifier` Zeichenfolge beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft weglassen, wird standardmäßig der folgende Wert verwendet:

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
