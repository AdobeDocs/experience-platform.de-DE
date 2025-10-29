---
title: sendPushSubscription
description: Registrieren von Push-Benachrichtigungs-Abonnements bei Adobe Experience Platform.
source-git-commit: 84faff58bac199c1113d7451f8cc865b6a870680
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
> Push-Benachrichtigungen für die Web-SDK befinden sich derzeit in der **Beta**. Die Funktionalität und Dokumentation können sich ändern.

Der Befehl `sendPushSubscription` registriert Push-Benachrichtigungs-Abonnements bei Adobe Experience Platform. Dieser Befehl verarbeitet das Abrufen von Push-Abonnementdetails aus dem Browser und sendet sie an Ihren konfigurierten Datenstrom.

## Voraussetzungen {#prerequisites}

Stellen Sie vor der Verwendung von `sendPushSubscription` Folgendes sicher:

1. **Konfigurierte Push-**: Richten Sie die [`pushNotifications`](configure/pushnotifications.md) Konfigurationseigenschaft mit Ihrem öffentlichen VAPID-Schlüssel ein.
2. **Benutzerberechtigung**: Benutzer müssen über die Berechtigung „Benachrichtigung“ verfügen (`Notification.permission === "granted"`)
3. **Service Worker**: Ein registrierter Service Worker muss auf Ihrer Site verfügbar sein
4. **Push-Manager-Unterstützung**: Der Browser muss Push-Benachrichtigungen unterstützen und die PushManager-API verfügbar haben

## Registrieren eines Push-Abonnements über die Tag-Erweiterung „Web SDK&quot; {#register-push-subscription-tag-extension}

Das Senden von Push-Abonnementdaten wird als Aktion innerhalb einer Regel in der Benutzeroberfläche der Datenerfassungs-Tags von Adobe Experience Platform ausgeführt.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Rules]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Actions] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das Dropdown-Feld [!UICONTROL Extension] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und das [!UICONTROL Action Type] auf **[!UICONTROL Send Push Subscription]** fest.
1. Klicken Sie auf **[!UICONTROL Keep Changes]** und führen Sie dann den Veröffentlichungs-Workflow aus.

## Registrieren eines Push-Abonnements über die Web SDK JavaScript-Bibliothek {#register-push-subscription-javascript}

Führen Sie den `sendPushSubscription` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Stellen Sie sicher, dass Sie den [`configure`](configure/overview.md)-Befehl mit konfigurierten Push-Benachrichtigungen aufrufen, bevor Sie den `sendPushSubscription`-Befehl aufrufen.

```js
alloy("sendPushSubscription")
  .then(() => {
    console.log("Push subscription recorded successfully");
  })
  .catch((error) => {
    console.error("Failed to send push subscription:", error);
  });
```

## Empfohlene Ausführungshäufigkeit {#recommended-execution-frequency}

Für eine optimale Push-Benachrichtigungsfunktion empfiehlt Adobe die Ausführung des `sendPushSubscription` Befehls **einmal täglich**. Dadurch wird Folgendes sichergestellt:

- Abonnementdetails bleiben in Adobe Experience Platform aktuell
- Alle Änderungen an Push-Token oder Abonnementstatus werden erfasst
- Das Profil des Benutzers wird weiterhin mit den neuesten Push-Benachrichtigungseinstellungen aktualisiert

Sie können dies mit einem ähnlichen Ansatz wie dem folgenden implementieren:

```js
// Check if we've sent subscription data today
const lastSent = localStorage.getItem("alloy_push_last_sent");
const today = new Date().toDateString();

if (lastSent !== today) {
  alloy("sendPushSubscription").then(() => {
    localStorage.setItem("alloy_push_last_sent", today);
  });
}
```

## Funktionsweise {#how-it-works}

Der Befehl `sendPushSubscription` führt die folgenden Aktionen aus:

1. **Validiert Voraussetzungen**: Überprüft, ob Push-Benachrichtigungen konfiguriert sind und die Benutzerberechtigung gewährt wird
2. **Wartet auf Identität**: Wartet, bis die ECID des Benutzers verfügbar ist
3. **Ruft das Abonnement ab**: Ruft das aktive Push-Abonnement vom Service Worker mithilfe des konfigurierten VAPID-Schlüssels ab
4. **Auf Änderungen prüfen**: Vergleicht aktuelle Abonnementdetails mit zwischengespeicherten Werten (ECID + Abonnementdetails). Wenn sich die Abonnementdetails nicht geändert haben, protokolliert der Befehl eine Informationsmeldung und gibt sie zurück, ohne eine Netzwerkanfrage zu stellen
5. **Wird an Datenstrom gesendet**: Wenn Änderungen erkannt werden, überträgt die Abonnementdaten an Ihren konfigurierten Adobe Experience Platform-Datenstrom
6. **Cache-Aktualisierungen**: Speichert die neuen Abonnementdetails für zukünftige Vergleiche

## Umgang mit Fehlern {#error-handling}

Häufige Fehlerbedingungen und deren Meldungen:

| Fehler | Ursache |
| ------- | ---- |
| `"Push notifications module is not configured. No VAPID public key was provided."` | Fehlende oder ungültige Konfiguration von Push-Benachrichtigungen |
| `"Service workers are not supported in this browser."` | Browser unterstützt keine Service Worker |
| `"Push notifications are not supported in this browser."` | Browser unterstützt keine Push-Benachrichtigungen oder Benachrichtigungs-API |
| `"The user has not given permission to send push notifications."` | Benutzer hat Benachrichtigungsberechtigung nicht erteilt |
| `"No service worker registration was found."` | Für die aktuelle Herkunft ist kein Service Worker registriert |
| `"No VAPID public key was provided."` | In der Konfiguration fehlt ein gültiger öffentlicher Schlüssel |

## Daten-Payload {#data-payload}

Der Befehl sendet Push-Benachrichtigungsdaten im folgenden Format:

```js
{
  pushNotificationDetails: [
    {
      appID: "example.com", // Current domain
      token: "...", // Serialized subscription details + ECID
      platform: "web", // Always "web" for Web SDK
      denylisted: false, // Always false
      identity: {
        namespace: {
          code: "ECID",
        },
        id: "12345678901234567890", // User's ECID
      },
    },
  ],
}
```

## Verwandte Dokumentation

- [Konfigurieren von Push-Benachrichtigungen](configure/pushnotifications.md)
- [Web Push API-Spezifikation](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
- [Service Worker-API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
