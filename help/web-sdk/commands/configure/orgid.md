---
title: orgId
description: Die Eigenschaft orgId ist eine Zeichenfolge, die Adobe angibt, an welche Organisation die Daten gesendet werden.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

Die `orgId` -Eigenschaft ist eine Zeichenfolge, die Adobe angibt, an welche Organisation die Daten gesendet werden. **Diese Eigenschaft ist für alle Daten erforderlich, die mit dem Web SDK gesendet werden.**

So suchen Sie Ihre `orgID`:

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Drücken Sie überall in der Adobe Experience Cloud die **`[Ctrl]`** + **`[I]`**. A [!UICONTROL User Data Debugger] öffnet sich.
1. Klicks **[!UICONTROL Kopieren]** ![Kopieren](../../assets/copy.png) neben dem [!UICONTROL Aktuelle Organisations-ID]oder klicken Sie auf **[!UICONTROL Zugewiesene Organisationen]** um andere Organisations-IDs anzuzeigen, auf die Sie zugreifen können.
1. Wenn Sie die gewünschten Informationen gefunden haben, klicken Sie auf **[!UICONTROL Schließen]**.

Organisations-IDs sind immer 24-stellige alphanumerische Zeichenfolgen und enden immer in `@AdobeOrg`.

## Konfigurieren Sie eine `orgID` Verwenden der Web SDK-Tag-Erweiterung

Geben Sie die Organisations-ID in die **[!UICONTROL Kennung der IMS-Organisation]** Textfeld bei [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Geben Sie die gewünschte Organisations-ID in die [!UICONTROL Kennung der IMS-Organisation] Textfeld oben.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Konfigurieren Sie eine `orgID` Verwenden der JavaScript-Bibliothek des Web SDK

Legen Sie die `orgId` Zeichenfolge beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, gibt das Web SDK einen Konsolenfehler aus und die Daten werden nicht an Adobe gesendet.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
