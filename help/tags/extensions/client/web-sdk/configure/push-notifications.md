---
title: Einstellungen für Push-Benachrichtigungen
description: Konfigurieren Sie Push-Benachrichtigungseinstellungen für die Tag-Erweiterung „Web SDK".
source-git-commit: 0b3f4ec51cac182b637c79b9fcb883e5f8f78d02
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---

# Einstellungen für Push-Benachrichtigungen

>[!AVAILABILITY]
>
>Push-Benachrichtigungen für die Web-SDK befinden sich derzeit in der **Beta**. Die Funktionalität und Dokumentation können sich ändern.

In diesem Konfigurationsabschnitt können Sie einen gültigen öffentlichen Schlüssel für die Push-Benachrichtigungsauthentifizierung festlegen.

>[!NOTE]
>
>Diese Funktion muss zuerst mithilfe von [Benutzerdefinierte Build-Komponenten](custom-build-components.md) aktiviert werden; sie ist standardmäßig deaktiviert.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und klicken Sie dann auf der **[!UICONTROL Configure]** auf [!UICONTROL Adobe Experience Platform Web SDK] .
1. Erweitern Sie **[!UICONTROL Custom build components]** und aktivieren Sie dann **[!UICONTROL Push notifications]**.
1. Scrollen Sie unter [!UICONTROL SDK instances] nach unten, um den Abschnitt [!UICONTROL Push Notifications] zu finden.
1. Geben Sie im Feld **[!UICONTROL VAPID Public Key]** Ihren gültigen öffentlichen Schlüssel ein.

![Bild mit den Push-Benachrichtigungseinstellungen unter Verwendung der Tag-Erweiterung „Web SDK&quot;](../assets/push-notifications.png)

Die folgenden Felder sind verfügbar:

## [!UICONTROL VAPID public key]

Der gültige öffentliche Schlüssel für Push-Abonnements. Es handelt sich um eine Base64-codierte Zeichenfolge.

## [!UICONTROL Application ID]

Die mit dem gültigen öffentlichen Schlüssel verknüpfte Anwendungs-ID.

## [!UICONTROL Tracking dataset ID]

Die Datensatz-ID für das Tracking und die Analyse von Push-Benachrichtigungen.

## Push-Benachrichtigungen unter Verwendung der JavaScript-Bibliothek

Dieser Abschnitt entspricht dem -Tag-[`pushNotifications`](/help/collection/js/commands/configure/pushnotifications.md) beim Konfigurieren der JavaScript-Bibliothek. Die verknüpfte Seite enthält auch Informationen zu Voraussetzungen und zum Generieren eines gültigen öffentlichen Schlüssels.
