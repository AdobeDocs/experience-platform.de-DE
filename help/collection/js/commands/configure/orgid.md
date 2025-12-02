---
title: orgId
description: Die orgId-Eigenschaft ist eine Zeichenfolge, die Adobe mitteilt, an welches Unternehmen diese Daten gesendet werden.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# `orgId`

Die `orgId`-Eigenschaft ist eine Zeichenfolge, die Adobe mitteilt, an welches Unternehmen diese Daten gesendet werden. **Diese Eigenschaft ist für alle Daten erforderlich, die mit der Web-SDK gesendet werden.**

So suchen Sie Ihr `orgID`:

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Drücken Sie an einer beliebigen Stelle in der Adobe Experience Cloud **`[Ctrl]`** + **`[I]`**. Ein [!UICONTROL User Data Debugger] wird geöffnet.
1. Klicken Sie auf **[!UICONTROL Copy]** ![Kopieren](../../assets/copy.png) neben der [!UICONTROL Current Org ID] oder auf die Registerkarte **[!UICONTROL Assigned Orgs]** , um andere Organisations-IDs anzuzeigen, auf die Sie zugreifen können.
1. Wenn Sie die gewünschten Informationen gefunden haben, klicken Sie auf **[!UICONTROL Close]**.

Organisations-IDs sind immer alphanumerische Zeichenfolgen mit 24 Zeichen und enden immer auf `@AdobeOrg`.

Legen Sie die `orgId` beim Ausführen des `configure`-Befehls fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, gibt die Web-SDK einen Konsolenfehler aus und die Daten werden nicht an Adobe gesendet.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

## Festlegen der Organisations-ID mithilfe der Tag-Erweiterung „Web SDK&quot;

Diese Einstellung kann in der Tag-Erweiterung „Web SDK&quot; mithilfe der Konfigurationseinstellungen der [SDK-Instanz konfiguriert &#x200B;](/help/tags/extensions/client/web-sdk/configure/general.md). Das Feld wird automatisch basierend auf der Organisation ausgefüllt, unter der die Tag-Eigenschaft erstellt wurde.
