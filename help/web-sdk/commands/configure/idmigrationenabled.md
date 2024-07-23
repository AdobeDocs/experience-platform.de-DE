---
title: idMigrationEnabled
description: Lässt das Web SDK AMCV-Cookies lesen.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# `idMigrationEnabled`

Mit der Eigenschaft `idMigrationEnabled` kann das Web SDK AMCV-Cookies lesen, die von früheren Adobe Experience Cloud-Implementierungen gesetzt wurden. Wenn Ihr Unternehmen Ihre Implementierung auf das Web SDK aktualisiert, ermöglicht diese Einstellung einen reibungsloseren Übergang zum aktuellen Adobe Experience Cloud ID-Dienst. Diese Einstellung ist nützlich, damit Sie keine deutliche Zunahme an Unique Visitors sehen, wenn Sie auf das Web SDK aktualisieren.

Wenn Ihr Unternehmen eine neue Web SDK-Implementierung ausführt, hat die Aktivierung dieser Einstellung keine Auswirkungen auf die Datenerfassung oder Besucheridentifizierung. Es gibt keine Nachteile, wenn Sie sie für alle Implementierungen aktivieren lassen.

## Aktivieren der ID-Migration mithilfe der Web SDK-Tag-Erweiterung

Aktivieren Sie das Kontrollkästchen **[!UICONTROL ECID von VisitorAPI in das Web-SDK migrieren]** , wenn [ die Tag-Erweiterung konfigurieren](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) soll.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Suchen Sie den Abschnitt [!UICONTROL Identität] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL ECID von VisitorAPI in das Web-SDK migrieren]** .
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Aktivieren der ID-Migration mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie den booleschen Wert `idMigrationEnabled` fest, wenn Sie den Befehl `configure` ausführen. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `true` verwendet. Legen Sie diese Eigenschaft fest, wenn Sie die Möglichkeit zum Lesen von AMCV-Cookies deaktivieren möchten, die von der Besucher-API gesetzt werden. Die meisten Unternehmen müssen diese Eigenschaft nicht festlegen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```
