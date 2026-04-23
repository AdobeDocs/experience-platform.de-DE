---
title: Einstellungen für Push-Benachrichtigungen
description: Konfigurieren Sie Push-Benachrichtigungseinstellungen für die Tag-Erweiterung „Web SDK".
exl-id: 96ab7ea8-7180-46bb-9c15-eecba2009c52
source-git-commit: d38cfb7d2ace7c1bb45dcb584a2cdf10063da06a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 11%

---

# Einstellungen für Push-Benachrichtigungen {#push-notifications}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_pushnotifications"
>title="Push-Benachrichtigungen "
>abstract="Legt einen gültigen öffentlichen Schlüssel für die Push-Benachrichtigungsauthentifizierung fest."

In diesem Konfigurationsabschnitt können Sie einen gültigen öffentlichen Schlüssel für die Push-Benachrichtigungsauthentifizierung festlegen.

>[!NOTE]
>
>Diese Funktion muss zuerst mithilfe von [Benutzerdefinierte Build-Komponenten](custom-build-components.md) aktiviert werden; sie ist standardmäßig deaktiviert.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
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
