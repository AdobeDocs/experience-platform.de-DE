---
title: orgId
description: Die Eigenschaft orgId ist eine Zeichenfolge, die Adobe angibt, an welche Organisation die Daten gesendet werden.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

Die `orgId` -Eigenschaft ist eine Zeichenfolge, die Adobe angibt, an welche Organisation die Daten gesendet werden. **Diese Eigenschaft ist für alle Daten erforderlich, die mit dem Web SDK gesendet werden.**

So suchen Sie Ihre `orgID`:

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Drücken Sie an beliebiger Stelle in der Adobe Experience Cloud die Tastenkombination **`[Ctrl]`** + **`[I]`**. Das Fenster [!UICONTROL Debugger für Benutzerdaten] wird geöffnet.
1. Klicken Sie neben der [!UICONTROL aktuellen Organisations-ID] auf **[!UICONTROL Kopieren]** ![Kopieren](../../assets/copy.png) oder auf die Registerkarte **[!UICONTROL Zugewiesene Organisationen]** , um weitere Organisations-IDs anzuzeigen, auf die Sie zugreifen können.
1. Wenn Sie die gewünschten Informationen gefunden haben, klicken Sie auf **[!UICONTROL Schließen]**.

Organisations-IDs sind immer 24-stellige alphanumerische Zeichenfolgen und enden immer auf `@AdobeOrg`.

## Konfigurieren von `orgID` mithilfe der Web SDK-Tag-Erweiterung

Geben Sie die Organisations-ID im Textfeld **[!UICONTROL IMS-Organisations-ID]** ein, wenn [die Tag-Erweiterung konfigurieren](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Geben Sie die gewünschte Organisations-ID in das Textfeld [!UICONTROL IMS-Organisations-ID] oben ein.
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Konfigurieren von `orgID` mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie die Zeichenfolge `orgId` fest, wenn Sie den Befehl `configure` ausführen. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, gibt das Web SDK einen Konsolenfehler aus und die Daten werden nicht an Adobe gesendet.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
