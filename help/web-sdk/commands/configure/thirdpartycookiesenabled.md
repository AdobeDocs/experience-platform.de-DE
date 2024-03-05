---
title: thirdPartyCookiesEnabled
description: Lassen Sie die Verwendung von Drittanbieter-Cookies zur Identifizierung von Besuchern zu.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `thirdPartyCookiesEnabled`

Die `thirdPartyCookiesEnabled` -Eigenschaft ist ein boolescher Wert, der bestimmt, ob das Web SDK Cookies in einem Drittanbieterkontext setzt. Die Aktivierung dieser Option ist nützlich, wenn Sie Besucher zwischen Subdomänen oder Domänen identifizieren möchten, deren Inhaber Ihre Organisation ist. Viele moderne Browser beschränken jedoch die Einstellung und Gültigkeit von Drittanbieter-Cookies.

Wenn diese Option aktiviert ist, verwendet das Web SDK Adobe Audience Manager zur Identifizierung eines Besuchers. Wenn diese Option deaktiviert ist, ist der Aufruf an Audience Manager deaktiviert. Siehe [Aufrufe an die Domäne &quot;demdex.net&quot;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/demdex-calls.html?lang=de) im Benutzerhandbuch für Audience Manager finden Sie weitere Informationen.

## Drittanbieter-Cookies mithilfe der Web SDK-Tag-Erweiterung aktivieren

Wählen Sie die **[!UICONTROL Verwenden von Drittanbieter-Cookies]** Kontrollkästchen, wenn [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Identität] und wählen Sie das Kontrollkästchen aus. **[!UICONTROL Verwenden von Drittanbieter-Cookies]**.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Drittanbieter-Cookies mithilfe der JavaScript-Bibliothek des Web SDK aktivieren

Legen Sie die `thirdPartyCookiesEnabled` boolean beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `true`. Setzen Sie diesen Wert auf `false` wenn Sie nicht möchten, dass das Web SDK Audience Manager zur Besucheridentifizierung verwendet.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "thirdPartyCookiesEnabled": false
});
```
