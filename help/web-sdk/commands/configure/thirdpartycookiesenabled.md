---
title: thirdPartyCookiesEnabled
description: Lassen Sie die Verwendung von Drittanbieter-Cookies zur Identifizierung von Besuchern zu.
exl-id: f241a9ae-a892-46a5-b0dd-5ac72a44d4ac
source-git-commit: bc48f45bd6b9b7f7cc446ae84d712376292718d2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# `thirdPartyCookiesEnabled`

>[!IMPORTANT]
>
>Google [hat angekündigt,](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout) werde die Chrome-Unterstützung für Drittanbieter-Cookies in der zweiten Jahreshälfte 2024 einstellen. Daher werden Drittanbieter-Cookies in keinem der wichtigsten Browser mehr unterstützt.
>
>Wenn diese Änderung implementiert ist, stellt Adobe die Unterstützung für das `demdex` -Cookie ein, das derzeit im Web SDK unterstützt wird.


Die Eigenschaft `thirdPartyCookiesEnabled` ist ein boolescher Wert, der bestimmt, ob das Web SDK Cookies in einem Drittanbieterkontext setzt. Die Aktivierung dieser Option ist nützlich, wenn Sie Besucher zwischen Subdomänen oder Domänen identifizieren möchten, deren Inhaber Ihre Organisation ist. Viele moderne Browser beschränken jedoch die Einstellung und Gültigkeit von Drittanbieter-Cookies.

Wenn diese Option aktiviert ist, verwendet das Web SDK Adobe Audience Manager zur Identifizierung eines Besuchers. Wenn diese Option deaktiviert ist, ist der Aufruf an Audience Manager deaktiviert. Weitere Informationen finden Sie unter [Aufrufe an die Domäne &quot;demdex.net&quot;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=de) im Audience Manager-Benutzerhandbuch.

## Drittanbieter-Cookies mithilfe der Web SDK-Tag-Erweiterung aktivieren

Aktivieren Sie das Kontrollkästchen **[!UICONTROL Drittanbieter-Cookies verwenden]** bei der Konfiguration der Tag-Erweiterung [.](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Identität] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL Drittanbieter-Cookies verwenden]** .
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Drittanbieter-Cookies mithilfe der Web SDK JavaScript-Bibliothek aktivieren

Legen Sie den booleschen Wert `thirdPartyCookiesEnabled` fest, wenn Sie den Befehl `configure` ausführen. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `true` verwendet. Setzen Sie diesen Wert auf &quot;`false`&quot;, wenn Sie nicht möchten, dass das Web SDK Audience Manager zur Besucheridentifizierung verwendet.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
