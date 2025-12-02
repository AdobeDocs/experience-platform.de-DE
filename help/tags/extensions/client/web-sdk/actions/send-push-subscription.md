---
title: Push-Abonnement senden
description: Daten für Browser-Push-Abonnements registrieren, senden und erfassen.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 7%

---

# Push-Abonnement senden

>[!AVAILABILITY]
>
>Push-Benachrichtigungen für die Web-SDK befinden sich derzeit in der **Beta**. Die Funktionalität und Dokumentation können sich ändern.

Die **[!UICONTROL Send push subscription]**-Aktion registriert Push-Benachrichtigungs-Abonnements bei Adobe Experience Platform. Es übernimmt das Abrufen von Push-Abonnementdetails aus dem Browser und sendet sie an Ihren konfigurierten Datenstrom. Sie ist in den Web SDK-Erweiterungsversionen 2.32.0 oder höher verfügbar.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Rules]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Actions] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das Dropdown-Feld [!UICONTROL Extension] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und das [!UICONTROL Action Type] auf **[!UICONTROL Send push subscription]** fest.

Die Aktion verfügt über keine Konfigurationseinstellungen außer der Auswahl einer SDK-Instanz.

Stellen Sie sicher, dass Sie beim Konfigurieren [&#x200B; Erweiterung einen gültigen &#x200B;](../configure/push-notifications.md)VAPID Public Key) festlegen, bevor Sie diesen Befehl verwenden.

Diese Aktion ist die Tag-Erweiterung, die dem [`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md)-Befehl entspricht. Informationen zu den Voraussetzungen, der empfohlenen Ausführungsfrequenz, der Funktionsweise des Befehls und der Fehlerbehandlung finden Sie auf der verknüpften Seite .

>[!MORELIKETHIS]
>
>* [Konfigurieren von Push-Benachrichtigungen](../configure/push-notifications.md)
>* [Web Push API-Spezifikation](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [Service Worker-API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
