---
title: Push-Benachrichtigungen
description: Konfigurieren Sie Push-Benachrichtigungen für Web SDK, um browserbasiertes Push-Messaging zu aktivieren.
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 5%

---

# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
>Push-Benachrichtigungen für die Web-SDK befinden sich derzeit in der **Beta**. Die Funktionalität und Dokumentation können sich ändern.

Mit der Eigenschaft `pushNotifications` können Sie Push-Benachrichtigungen für Web-Anwendungen konfigurieren. Mit dieser Funktion kann Ihre Web-Anwendung Nachrichten empfangen, die von einem Server gepusht werden, auch wenn die Website derzeit nicht im Browser geladen ist.

## Voraussetzungen {#prerequisites}

Stellen Sie vor dem Konfigurieren von Push-Benachrichtigungen Folgendes sicher:

1. **Benutzerberechtigung**: Benutzer müssen Benachrichtigungen explizit genehmigen
2. **Service Worker**: Ein registrierter Service Worker ist erforderlich, damit Push-Benachrichtigungen funktionieren
3. **VAPID keys**: Generieren von VAPID-Schlüsseln (Voluntary Application Server Identification) für eine sichere Kommunikation
4. **Anwendungs-ID**: Die App-ID, die beim Speichern der GÜLTIGEN Schlüssel in Adobe Journey Optimizer verwendet wird -> Kanäle -> Push-Einstellungen -> Push-Anmeldeinformationen
5. **Tracking-Datensatz-**: Die ID des Systemdatensatzes mit dem Namen &quot;AJO Push Tracking Experience Event Dataset“. Dies aus Adobe Journey Optimizer abrufen -> Datensätze

## Generieren von VAPID-Schlüsseln {#generate-vapid-keys}

Um VAPID-Schlüssel zu generieren, installieren Sie das `web-push` NPM-Paket und führen Sie Folgendes aus:

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Diese Aktion generiert ein Schlüsselpaar aus öffentlichem und privatem Schlüssel. Verwenden Sie den öffentlichen Schlüssel in Ihrer Web SDK-Konfiguration und speichern Sie den privaten Schlüssel im Adobe Journey Optimizer-Kanal für Push-Benachrichtigungen.

## Installieren des Service Workers

Der Service Worker-Code muss von derselben Domain wie die Website bereitgestellt werden. Laden Sie den Service Worker-Code aus dem CDN von Adobe herunter und hosten Sie die JavaScript-Datei von Ihrem eigenen Server. Der Web SDK Service Worker-Code ist über die folgende URL-Struktur verfügbar:

- **minifiziert**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **Voll**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

Im Folgenden finden Sie ein Beispiel für die Installation des Service Workers:

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## Implementierung

Legen Sie das `pushNotifications`-Objekt beim Ausführen des `configure`-Befehls fest:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey: "BEl62iUYgU[...]KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## Properties {#properties}

| Eigenschaft | Typ | Erforderlich | Beschreibung |
|---|---|---|---|
| **`vapidPublicKey`** | Zeichenfolge | Ja | Der gültige öffentliche Schlüssel für Push-Abonnements. Muss eine Base64-codierte Zeichenfolge sein. |
| **`applicationId`** | Zeichenfolge | Ja | Die mit dem gültigen öffentlichen Schlüssel verknüpfte Anwendungs-ID. |
| **`trackingDatasetId`** | Zeichenfolge | Ja | Die für das Tracking von Push-Benachrichtigungen verwendete Systemdatensatz-ID. |

## Wichtige Überlegungen {#important-considerations}

- **Sicherheit**: Push-Abonnements sind an den spezifischen gültigen öffentlichen Schlüssel gebunden, der während des Abonnements verwendet wird. Wenn Sie GÜLTIGE Schlüssel ändern, werden bestehende Abonnements automatisch abgemeldet und mit dem neuen Schlüssel neu erstellt.
- **Caching**: Die Web-SDK verwaltet Abonnementaktualisierungen automatisch, indem die aktuelle ECID- und Abonnementdetails mit zwischengespeicherten Werten verglichen werden. Abonnementdaten werden nur gesendet, wenn Änderungen erkannt werden.
- **Service Worker-Anforderung**: Push-Benachrichtigungen erfordern einen registrierten Service Worker. Stellen Sie sicher, dass Ihr Service Worker ordnungsgemäß für die Verarbeitung von Push-Ereignissen konfiguriert ist.

## Konfigurieren von Push-Benachrichtigungen mithilfe der Tag-Erweiterung „Web SDK&quot; {#configure-push-notifications-tag-extension}

Die dieser Eigenschaft entsprechende Web SDK-Tag-Erweiterung ist der [[!UICONTROL Push notifications]](/help/tags/extensions/client/web-sdk/configure/push-notifications.md) Abschnitt beim Konfigurieren der Erweiterung.

## Nächste Schritte {#next-steps}

Nachdem Sie Push-Benachrichtigungen konfiguriert haben, verwenden Sie den Befehl [sendPushSubscription](../sendpushsubscription.md), um Push-Abonnements bei Adobe Experience Platform zu registrieren.
