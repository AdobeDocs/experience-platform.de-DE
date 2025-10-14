---
title: orgId
description: Die orgId-Eigenschaft ist eine Zeichenfolge, die Adobe mitteilt, an welches Unternehmen diese Daten gesendet werden.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# `orgId`

Die `orgId`-Eigenschaft ist eine Zeichenfolge, die Adobe mitteilt, an welches Unternehmen diese Daten gesendet werden. **Diese Eigenschaft ist für alle Daten erforderlich, die mit der Web-SDK gesendet werden.**

So suchen Sie Ihr `orgID`:

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Drücken Sie an einer beliebigen Stelle in der Adobe Experience Cloud **`[Ctrl]`** + **`[I]`**. Ein Fenster [!UICONTROL User Data Debugger] wird geöffnet.
1. Klicken Sie **[!UICONTROL Kopieren]** ![Kopieren](../../assets/copy.png) neben der [!UICONTROL Aktuelle Organisations-ID] oder klicken Sie auf die Registerkarte **[!UICONTROL Zugewiesene Organisationen]**, um andere Organisations-IDs anzuzeigen, auf die Sie zugreifen können.
1. Wenn Sie die gewünschten Informationen gefunden haben, klicken Sie auf **[!UICONTROL Schließen]**.

Organisations-IDs sind immer alphanumerische Zeichenfolgen mit 24 Zeichen und enden immer auf `@AdobeOrg`.

## Konfigurieren eines `orgID` mithilfe der Tag-Erweiterung „Web SDK&quot;

Geben Sie die Organisations-ID im Textfeld **[!UICONTROL IMS-Organisations]** ein, wenn Sie [die Tag-Erweiterung konfigurieren](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Geben Sie die gewünschte Organisations-ID in das Textfeld [!UICONTROL IMS-Organisations]ID) oben ein.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

## Konfigurieren eines `orgID` mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie die `orgId` beim Ausführen des `configure`-Befehls fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, gibt die Web-SDK einen Konsolenfehler aus und die Daten werden nicht an den Adobe gesendet.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```
