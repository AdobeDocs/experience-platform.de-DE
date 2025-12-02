---
title: idMigrationEnabled
description: Ermöglicht dem Web-SDK, AMCV-Cookies zu lesen.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `idMigrationEnabled`

Die `idMigrationEnabled`-Eigenschaft ermöglicht es dem Web-SDK, AMCV-Cookies zu lesen, die von vorherigen Adobe Experience Cloud-Implementierungen festgelegt wurden. Wenn Ihr Unternehmen Ihre Implementierung auf Web SDK aktualisiert, ermöglicht diese Einstellung einen reibungsloseren Übergang zum aktuellen Adobe Experience Cloud ID-Service. Diese Einstellung ist nützlich, damit beim Upgrade auf Web SDK keine starke Zunahme von Unique Visitors auftritt.

Wenn Ihr Unternehmen eine neue Web SDK-Implementierung ausführt, hat die Aktivierung dieser Einstellung keine Auswirkungen auf die Datenerfassung oder Besucheridentifizierung. Es hat keine Nachteile, wenn es für alle Implementierungen aktiviert bleibt.

Legen Sie beim Ausführen des `idMigrationEnabled`-Befehls den booleschen Wert `configure` fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `true` gesetzt. Legen Sie diese Eigenschaft fest, wenn Sie die Möglichkeit deaktivieren möchten, AMCV-Cookies zu lesen, die von der Besucher-API festgelegt werden. Die meisten Organisationen müssen diese Eigenschaft nicht festlegen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Aktivieren der Migration von Besucher-IDs mithilfe der Tag-Erweiterung von Web SDK

Diese Einstellungen können in der Tag-Erweiterung „Web SDK&quot; mithilfe von [Identitätskonfigurationseinstellungen](/help/tags/extensions/client/web-sdk/configure/identity.md) konfiguriert werden.
