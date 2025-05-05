---
title: downloadLinkQualifier
description: Hilft bei der Bestimmung, wie die automatische Linkverfolgung Download-Links qualifiziert.
exl-id: ef4f0ed4-83fc-485f-866d-f9ca15447ac8
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# `downloadLinkQualifier`

Wenn Sie die automatische Link-Überwachung mithilfe von [`clickCollectionEnabled`](clickcollectionenabled.md) aktivieren, hilft Ihnen die `downloadLinkQualifier`-Eigenschaft bei der Bestimmung der Kriterien, anhand derer eine URL als Download-Link betrachtet werden kann.

Diese Eigenschaft ist eine Regex-Zeichenfolge. Wenn die angeklickte URL mit diesem Regex übereinstimmt, wird `xdm.web.webInteraction.type` auf `"download"` gesetzt. Links werden auch sofort als Downloadlink klassifiziert, wenn sie ein `download` HTML-Attribut enthalten. Wenn `clickCollectionEnabled` nicht aktiviert ist, hat diese Eigenschaft keine Auswirkung.

## Herunterladen des Link-Qualifizierers mithilfe der Tag-Erweiterung „Web SDK&quot;

Aktivieren Sie das Kontrollkästchen **[!UICONTROL Click-Datenerfassung aktivieren]** und geben Sie dann beim Konfigurieren der Tag **[!UICONTROL Erweiterung den gewünschten Text unter]** Link-Qualifizierer [&#128279;](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenerfassung] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL Aktivieren und auf Datenerfassung klicken]**.
1. Nach der Aktivierung **[!UICONTROL das Textfeld]** Downloadlink-Qualifizierer“ angezeigt. Geben Sie den gewünschten Wert ein. Schaltflächen sind auch verfügbar, um den Regex zu testen und den Standardwert wiederherzustellen.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

## Herunterladen des Link-Qualifizierers mithilfe der Web SDK JavaScript-Bibliothek

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
