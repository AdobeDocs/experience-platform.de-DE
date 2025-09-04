---
title: Push-Benachrichtigungen
description: Konfigurieren Sie Push-Benachrichtigungen für Web SDK, um browserbasiertes Push-Messaging zu aktivieren.
source-git-commit: 9c3f19cc2b32ab70869584b620f5a55d5b808751
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---


# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
> Push-Benachrichtigungen für die Web-SDK befinden sich derzeit in der **Beta**. Die Funktionalität und Dokumentation können sich ändern.

Mit der Eigenschaft `pushNotifications` können Sie Push-Benachrichtigungen für Web-Anwendungen konfigurieren. Mit dieser Funktion kann Ihre Web-Anwendung Nachrichten empfangen, die von einem Server gepusht werden, selbst wenn die Website derzeit nicht im Browser geladen ist oder wenn der Browser nicht ausgeführt wird.

## Voraussetzungen {#prerequisites}

Stellen Sie vor dem Konfigurieren von Push-Benachrichtigungen Folgendes sicher:

1. **Benutzerberechtigung**: Benutzer müssen Benachrichtigungen explizit genehmigen
2. **Service Worker**: Ein registrierter Service Worker ist erforderlich, damit Push-Benachrichtigungen funktionieren
3. **VAPID keys**: Generieren von VAPID-Schlüsseln (Voluntary Application Server Identification) für eine sichere Kommunikation

## Generieren von VAPID-Schlüsseln {#generate-vapid-keys}

Um VAPID-Schlüssel zu generieren, installieren Sie das `web-push` NPM-Paket und führen Sie Folgendes aus:

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Dadurch wird ein Schlüsselpaar aus öffentlichem und privatem Schlüssel generiert. Verwenden Sie den öffentlichen Schlüssel in Ihrer Web SDK-Konfiguration und speichern Sie den privaten Schlüssel im Adobe Journey Optimizer-Kanal für Push-Benachrichtigungen.

## Konfigurieren von Push-Benachrichtigungen mithilfe der Tag-Erweiterung „Web SDK&quot; {#configure-push-notifications-tag-extension}

Führen Sie die folgenden Schritte aus, um Push-Benachrichtigungen zu aktivieren und zu konfigurieren:

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. **Aktivieren von Push** Benachrichtigungen über den Abschnitt „Benutzerdefinierte Build-Komponenten“.
1. Scrollen Sie nach unten, um den Abschnitt [!UICONTROL Push-Benachrichtigungen] zu finden.
1. Geben Sie im Feld **[!UICONTROL VAPID Public Key]** Ihren gültigen öffentlichen Schlüssel ein.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

>[!NOTE]
>
> Push-Benachrichtigungen müssen in der Tag-Erweiterungskonfiguration explizit aktiviert werden. Die Funktion ist standardmäßig deaktiviert.

## Konfigurieren von Push-Benachrichtigungen mithilfe der Web SDK JavaScript-Bibliothek {#configure-push-notifications-javascript}

Legen Sie das `pushNotifications`-Objekt beim Ausführen des `configure`-Befehls fest:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey:
      "BEl62iUYgUivElbkzaBgNL3r3vOAhvJyFXjS6FjjRRojYD4NElJkLBJKZvS3xAAh4_gE3WnMaZNu_KGP4jAQlJz",
  },
});
```

## Properties {#properties}

| Eigenschaft | Typ | Erforderlich | Beschreibung |
| ------ | ------ | -------- | ----- |
| `vapidPublicKey` | Zeichenfolge | Ja | Der gültige öffentliche Schlüssel für das Push-Abonnement. Muss eine Base64-codierte Zeichenfolge sein. |

## Wichtige Überlegungen {#important-considerations}

- **Sicherheit**: Push-Abonnements sind an den spezifischen gültigen öffentlichen Schlüssel gebunden, der während des Abonnements verwendet wird. Wenn Sie GÜLTIGE Schlüssel ändern, werden bestehende Abonnements automatisch abgemeldet und mit dem neuen Schlüssel neu erstellt.
- **Caching**: Die Web-SDK verwaltet Abonnementaktualisierungen automatisch, indem die aktuelle ECID- und Abonnementdetails mit zwischengespeicherten Werten verglichen werden. Abonnementdaten werden nur gesendet, wenn Änderungen erkannt werden.
- **Service Worker-Anforderung**: Push-Benachrichtigungen erfordern einen registrierten Service Worker. Stellen Sie sicher, dass Ihr Service Worker ordnungsgemäß für die Verarbeitung von Push-Ereignissen konfiguriert ist.

## Nächste Schritte {#next-steps}

Nachdem Sie Push-Benachrichtigungen konfiguriert haben, verwenden Sie den Befehl [`sendPushSubscription`](../sendPushSubscription.md) , um Push-Abonnements bei Adobe Experience Platform zu registrieren.
