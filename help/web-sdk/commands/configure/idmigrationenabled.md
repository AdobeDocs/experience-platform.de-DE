---
title: idMigrationEnabled
description: Lässt das Web SDK AMCV-Cookies lesen.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

Die `idMigrationEnabled` -Eigenschaft ermöglicht es dem Web SDK, AMCV-Cookies zu lesen, die von früheren Adobe Experience Cloud-Implementierungen gesetzt wurden. Wenn Ihr Unternehmen Ihre Implementierung auf das Web SDK aktualisiert, ermöglicht diese Einstellung einen reibungsloseren Übergang zum aktuellen Adobe Experience Cloud ID-Dienst. Diese Einstellung ist nützlich, damit Sie keine deutliche Zunahme an Unique Visitors sehen, wenn Sie auf das Web SDK aktualisieren.

Wenn Ihr Unternehmen eine neue Web SDK-Implementierung ausführt, hat die Aktivierung dieser Einstellung keine Auswirkungen auf die Datenerfassung oder Besucheridentifizierung. Es gibt keine Nachteile, wenn Sie sie für alle Implementierungen aktivieren lassen.

## Aktivieren der ID-Migration mithilfe der Web SDK-Tag-Erweiterung

Wählen Sie die **[!UICONTROL Migrieren der ECID von der VisitorAPI zum Web SDK]** Kontrollkästchen, wenn [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Suchen Sie die [!UICONTROL Identität] und wählen Sie das Kontrollkästchen aus. **[!UICONTROL Migrieren der ECID von der VisitorAPI zum Web SDK]**.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Aktivieren der ID-Migration mithilfe der JavaScript-Bibliothek des Web SDK

Legen Sie die `idMigrationEnabled` boolean beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `true`. Legen Sie diese Eigenschaft fest, wenn Sie die Möglichkeit zum Lesen von AMCV-Cookies deaktivieren möchten, die von der Besucher-API gesetzt werden. Die meisten Unternehmen müssen diese Eigenschaft nicht festlegen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "idMigrationEnabled": false
});
```
