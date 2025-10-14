---
title: idMigrationEnabled
description: Ermöglicht dem Web-SDK, AMCV-Cookies zu lesen.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

Die `idMigrationEnabled`-Eigenschaft ermöglicht es dem Web-SDK, AMCV-Cookies zu lesen, die von vorherigen Adobe Experience Cloud-Implementierungen festgelegt wurden. Wenn Ihr Unternehmen Ihre Implementierung auf Web SDK aktualisiert, ermöglicht diese Einstellung einen reibungsloseren Übergang zum aktuellen Adobe Experience Cloud ID-Service. Diese Einstellung ist nützlich, damit beim Upgrade auf Web SDK keine starke Zunahme von Unique Visitors auftritt.

Wenn Ihr Unternehmen eine neue Web SDK-Implementierung ausführt, hat die Aktivierung dieser Einstellung keine Auswirkungen auf die Datenerfassung oder Besucheridentifizierung. Es hat keine Nachteile, wenn es für alle Implementierungen aktiviert bleibt.

## Aktivieren der ID-Migration mithilfe der Tag-Erweiterung „Web SDK&quot;

Aktivieren Sie das Kontrollkästchen **[!UICONTROL ECID von VisitorAPI in die Web-SDK migrieren]** beim [&#x200B; der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Suchen Sie den Abschnitt [!UICONTROL Identität] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL ECID von VisitorAPI in die Web-SDK migrieren]**.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

## Aktivieren der ID-Migration mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie beim Ausführen des `configure`-Befehls den booleschen Wert `idMigrationEnabled` fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `true` gesetzt. Legen Sie diese Eigenschaft fest, wenn Sie die Möglichkeit deaktivieren möchten, AMCV-Cookies zu lesen, die von der Besucher-API festgelegt werden. Die meisten Organisationen müssen diese Eigenschaft nicht festlegen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```
