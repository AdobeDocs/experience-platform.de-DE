---
title: downloadLinkQualifier
description: Hilft bei der Bestimmung, wie die automatische Linkverfolgung Download-Links qualifiziert.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# `downloadLinkQualifier`

Wenn Sie die automatische Link-Überwachung mithilfe von [`clickCollectionEnabled`](clickcollectionenabled.md) aktivieren, hilft Ihnen die `downloadLinkQualifier`-Eigenschaft bei der Bestimmung der Kriterien, anhand derer eine URL als Download-Link betrachtet werden kann.

Diese Eigenschaft ist eine Regex-Zeichenfolge. Wenn die angeklickte URL mit diesem Regex übereinstimmt, wird `xdm.web.webInteraction.type` auf `"download"` gesetzt. Links werden auch sofort als Downloadlink klassifiziert, wenn sie ein `download` HTML-Attribut enthalten. Wenn `clickCollectionEnabled` nicht aktiviert ist, hat diese Eigenschaft keine Auswirkung.

Legen Sie die `downloadLinkQualifier` beim Ausführen des `configure`-Befehls fest. Wenn Sie diese Eigenschaft auslassen, wird standardmäßig der folgende Wert verwendet:

`\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$`

Wenn Sie verschiedene Kriterien verwenden möchten, um Downloadlinks zu qualifizieren, setzen Sie diese Eigenschaft auf den gewünschten Regex-Wert.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  downloadLinkQualifier: "\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
});
```

## Herunterladen des Link-Qualifizierers mithilfe der Tag-Erweiterung „Web SDK&quot;

Die Web SDK-Tag-Erweiterung, die diesem Feld entspricht, befindet sich bei [ Konfiguration der Tag](/help/tags/extensions/client/web-sdk/configure/data-collection.md#download-link-qualifier)Erweiterung unter „Konfigurationseinstellungen für die Datenerfassung“.
