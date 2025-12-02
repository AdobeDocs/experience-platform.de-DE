---
title: thirdPartyCookiesEnabled
description: Zulassen der Verwendung von Drittanbieter-Cookies zur Identifizierung von Besuchern.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

Die `thirdPartyCookiesEnabled`-Eigenschaft ist ein boolescher Wert, der bestimmt, ob die Web-SDK Cookies in einem Drittanbieterkontext setzt. Die Aktivierung dieser Option ist nützlich, wenn Sie Besucher zwischen Subdomains oder Domains identifizieren möchten, deren Inhaber Ihr Unternehmen ist. Viele moderne Browser beschränken jedoch das Setzen und Ablaufen von Drittanbieter-Cookies. Wenn der Browser eines Besuchers keine Cookies von Drittanbietern unterstützt, hat diese Eigenschaft keine Auswirkungen.

Die `thirdPartyCookiesEnabled`-Eigenschaft steuert auch, ob eine [`CORE ID`](/help/collection/use-cases/identity/id-overview.md#tracking-coreid-web-sdk) für [`getIdentity`](../getidentity.md)-Aufrufe angefordert werden kann.

Wenn diese Option aktiviert ist, verwendet die Web-SDK Adobe Audience Manager, um einen Besucher zu identifizieren. Wenn diese Option deaktiviert ist, ist der Aufruf von Audience Manager deaktiviert. Weitere Informationen finden [ im Audience Manager-Benutzerhandbuch unter „Aufrufe an ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=de) Domain „demdex.net“.

Legen Sie beim Ausführen des `thirdPartyCookiesEnabled`-Befehls den booleschen Wert `configure` fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `true` gesetzt. Legen Sie diesen Wert auf `false` fest, wenn Sie nicht möchten, dass die Web-SDK Audience Manager zur Identifizierung von Besuchern verwendet.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  thirdPartyCookiesEnabled: false
});
```

## Aktivieren von Drittanbieter-Cookies mithilfe der Tag-Erweiterung „Web SDK&quot;

Diese Einstellung kann in der Tag-Erweiterung „Web SDK&quot; mithilfe von [Identitätskonfigurationseinstellungen](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies) konfiguriert werden.
