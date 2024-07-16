---
title: targetMigrationEnabled
description: Erlauben Sie dem Web SDK, Adobe Target-Cookies zu lesen und zu schreiben.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

Die `targetMigrationEnabled` -Eigenschaft ist ein boolescher Wert, der es dem Web SDK ermöglicht, die von den Adobe Target 1.x- und 2.x-Bibliotheken verwendeten mbox- und mboxEdgeCluster-Cookies zu lesen und zu schreiben. Mit dieser Option können Sie das Besucherprofil zwischen Seiten, die frühere Adobe Target-Implementierungen verwenden, und Seiten, die das Web SDK verwenden, beibehalten.

## Aktivieren der Target-Migration von at.js mithilfe der Web SDK-Tag-Erweiterung

Aktivieren Sie das Kontrollkästchen **[!UICONTROL Target von at.js in das Web SDK migrieren]** , wenn [ die Tag-Erweiterung konfiguriert.](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Personalization] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL Target von at.js zum Web SDK migrieren]** .
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Aktivieren der Target-Migration von at.js mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie den booleschen Wert `targetMigrationEnabled` fest, wenn Sie den Befehl `configure` ausführen. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `false` verwendet. Setzen Sie diesen Wert auf `true` , wenn Sie einige Seiten haben, die noch die Adobe Target 1.x- oder 2.x-Bibliotheken verwenden.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
