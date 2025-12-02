---
title: Einstellungen der Identitätskonfiguration
description: Definieren, wie die Tag-Erweiterung Besucher identifiziert.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 2%

---

# Einstellungen der Identitätskonfiguration

In diesem Konfigurationsabschnitt können Sie das Verhalten der Web-SDK bei der Handhabung der Benutzeridentifizierung definieren.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Identity]** .

![Bild mit den Identitätseinstellungen der Web SDK-Tag-Erweiterung in der Tags-Benutzeroberfläche](../assets/web-sdk-ext-identity.png)

Die folgenden Optionen sind verfügbar:

## [!UICONTROL Migrate ECID from VisitorAPI]

Ein Kontrollkästchen, mit dem Web SDK die `AMCV` und `s_ecid` Cookies lesen und das von `AMCV` verwendete `Visitor.js`-Cookie festlegen kann. Diese Funktion ist bei der Migration von Bibliotheken, die `VisitorAPI.js` verwenden, auf die Web-SDK wichtig, da einige Seiten möglicherweise noch `Visitor.js` verwenden. Mit dieser Option kann SDK dieselbe ECID weiterhin verwenden, sodass Benutzende nicht als zwei separate Benutzende identifiziert werden. Die JavaScript-Bibliothek, die diesem Kontrollkästchen entspricht, ist [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md).

## [!UICONTROL Use third-party cookies]

Wenn diese Option aktiviert ist, versucht Web SDK, eine Benutzerkennung in einem Drittanbieter-Cookie zu speichern. Bei erfolgreicher Ausführung wird der Benutzer bei der Navigation durch mehrere Domains als ein einzelner Benutzer identifiziert, anstatt in jeder Domain als separater Benutzer identifiziert zu werden. Wenn diese Option aktiviert ist, kann die SDK die Benutzerkennung möglicherweise immer noch nicht in einem Drittanbieter-Cookie speichern, wenn der Browser keine Drittanbieter-Cookies unterstützt oder vom Benutzer so konfiguriert wurde, dass keine Drittanbieter-Cookies zugelassen werden. In diesem Fall speichert die SDK die Kennung nur in der Erstanbieter-Domain. Die JavaScript-Bibliothek, die diesem Kontrollkästchen entspricht, ist [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md).

>[!IMPORTANT]
>
>Drittanbieter-Cookies sind nicht mit der Funktion [Erstanbieter-Geräte-ID](/help/collection/use-cases/identity/first-party-device-ids.md) in Web SDK kompatibel. Sie können entweder Erstanbieter-Geräte-IDs oder Drittanbieter-Cookies verwenden. Sie können nicht beide Funktionen gleichzeitig verwenden.
