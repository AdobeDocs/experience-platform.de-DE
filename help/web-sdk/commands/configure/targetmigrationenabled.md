---
title: targetMigrationEnabled
description: Der Web-SDK darf Adobe Target-Cookies lesen und schreiben.
exl-id: 4b9203c6-31b7-45af-a6a6-a206d7edac3f
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# `targetMigrationEnabled`

Die `targetMigrationEnabled`-Eigenschaft ist ein boolescher Wert, der es der Web-SDK ermöglicht, die von den Adobe Target 1.x- und 2.x-Bibliotheken verwendeten mbox- und mboxEdgeCluster-Cookies zu lesen und zu schreiben. Mit dieser Option können Sie das Besucherprofil zwischen Seiten beibehalten, die frühere Adobe Target-Implementierungen verwendet haben, und Seiten, die Web SDK verwenden.

## Aktivieren der Target-Migration aus at.js mithilfe der Tag-Erweiterung „Web SDK&quot;

Aktivieren Sie **[!UICONTROL Kontrollkästchen „Target von at.js in den Web-SDK migrieren]** beim [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Personalization] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL Target von at.js in die Web-SDK migrieren]**.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

## Aktivieren der Target-Migration aus at.js mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie beim Ausführen des `configure`-Befehls den booleschen Wert `targetMigrationEnabled` fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `false` gesetzt. Legen Sie diesen Wert auf `true` fest, wenn einige Seiten weiterhin die Adobe Target 1.x- oder 2.x-Bibliotheken verwenden.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  targetMigrationEnabled: true
});
```
