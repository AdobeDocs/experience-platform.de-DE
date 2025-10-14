---
title: thirdPartyCookiesEnabled
description: Zulassen der Verwendung von Drittanbieter-Cookies zur Identifizierung von Besuchern.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: a884790aa48fb97eebe2421124fc5d5f76c8a79d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

Die `thirdPartyCookiesEnabled`-Eigenschaft ist ein boolescher Wert, der bestimmt, ob die Web-SDK Cookies in einem Drittanbieterkontext setzt. Die Aktivierung dieser Option ist nützlich, wenn Sie Besucher zwischen Subdomains oder Domains identifizieren möchten, deren Inhaber Ihr Unternehmen ist. Viele moderne Browser beschränken jedoch das Setzen und Ablaufen von Drittanbieter-Cookies.

Die `thirdPartyCookiesEnabled`-Eigenschaft steuert auch, ob eine [`CORE ID`](../../identity/overview.md#tracking-coreid-web-sdk) für [`getIdentity`](../getidentity.md)-Aufrufe angefordert werden kann.

Wenn diese Option aktiviert ist, verwendet die Web-SDK Adobe Audience Manager, um einen Besucher zu identifizieren. Wenn diese Option deaktiviert ist, ist der Aufruf von Audience Manager deaktiviert. Weitere Informationen finden [&#x200B; unter „Aufrufe an die &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=de)-Domain“ im Benutzerhandbuch für Audience Manager.

## Aktivieren von Drittanbieter-Cookies mithilfe der Tag-Erweiterung „Web SDK&quot;

Aktivieren Sie **[!UICONTROL Kontrollkästchen „Third-Party-Cookies verwenden]** beim [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Identität] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL Verwendung von Drittanbieter-Cookies]**.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

## Aktivieren von Drittanbieter-Cookies mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie beim Ausführen des `configure`-Befehls den booleschen Wert `thirdPartyCookiesEnabled` fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `true` gesetzt. Legen Sie diesen Wert auf `false` fest, wenn Sie nicht möchten, dass die Web-SDK Audience Manager zur Identifizierung von Besuchern verwendet.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```
