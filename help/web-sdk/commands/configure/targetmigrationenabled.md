---
title: targetMigrationEnabled
description: Erlauben Sie dem Web SDK, Adobe Target-Cookies zu lesen und zu schreiben.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

Die `targetMigrationEnabled` -Eigenschaft ist ein boolescher Wert, der es dem Web SDK ermöglicht, die von den Adobe Target 1.x- und 2.x-Bibliotheken verwendeten mbox- und mboxEdgeCluster-Cookies zu lesen und zu schreiben. Mit dieser Option können Sie das Besucherprofil zwischen Seiten, die frühere Adobe Target-Implementierungen verwenden, und Seiten, die das Web SDK verwenden, beibehalten.

## Aktivieren der Target-Migration von at.js mithilfe der Web SDK-Tag-Erweiterung

Wählen Sie die **[!UICONTROL Migrieren von Target von at.js zum Web SDK]** Kontrollkästchen, wenn [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Personalisierung] und wählen Sie das Kontrollkästchen aus. **[!UICONTROL Migrieren von Target von at.js zum Web SDK]**.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Aktivieren der Target-Migration von at.js mithilfe der Web SDK-JavaScript-Bibliothek

Legen Sie die `targetMigrationEnabled` boolean beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `false`. Setzen Sie diesen Wert auf `true` wenn Sie einige Seiten haben, die weiterhin die Adobe Target 1.x- oder 2.x-Bibliotheken verwenden.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled": true
});
```
