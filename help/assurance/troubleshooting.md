---
title: Handbuch zur Fehlerbehebung bei Adobe Experience Platform Assurance
description: In diesem Dokument werden Lösungen für häufige Probleme bei der Verwendung von Adobe Experience Platform Assurance beschrieben.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 6%

---

# Fehlerbehebung bei Adobe Experience Platform Assurance

Wenn Sie Probleme haben, Assurance zu verwenden, lesen Sie die Vorschläge unter den folgenden Problemthemen, um häufig aufgetretene Probleme zu beheben.

Um eine reibungslosere Implementierung zu ermöglichen und potenzielle Probleme zu erkennen, stellen Sie sicher, dass die SDK-Protokollierung gemäß [Debug-Protokollierung aktivieren](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) im Abschnitt Erste Schritte aktiviert ist.

Sie können die SDK-Protokollebenen mithilfe der [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel)-API ändern.

## Probleme auf dem Gerät und in der App

### QR-Code öffnet keine App

* Greifen Sie direkt auf den Link zu. Kopieren Sie den Link aus **Sitzungsdetails**. Fügen Sie es in die Adressleiste des Browsers des Geräts ein, um es zu öffnen. Falls er sich nicht öffnet, lesen Sie bitte den Abschnitt [App öffnet keinen Link](#app-does-not-open-link).
* Verwenden Sie einen anderen QR-Reader. Verwenden Sie für iOS 11 oder höher die Foto-App, um den QR-Code zu lesen.

### App öffnet den Link nicht

* Überprüfen Sie, ob die Deep-Link-Implementierung in der App korrekt konfiguriert ist.
   * **Android:** Deep-Links (App-Links)
      * [Erstellen von Deep-Links zum App-Kontext](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** Benutzerdefiniertes URL-Schema oder universelle Links
      * [Definieren eines benutzerdefinierten URL-Schemas für Ihre App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Unterstützung universeller Links in Ihrer App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Für Android muss die `startSession`-API nicht explizit aufgerufen werden. Verwenden Sie für iOS die API wie in [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core) beschrieben.

### Authentifizierungsüberlagerung wird angezeigt, aber App kann keine Verbindung herstellen

* Stellen Sie die Internetverbindung des Geräts über den Geräte-Webbrowser sicher.
* Wenn die App noch nie erfolgreich eine Verbindung zum Assurance-Service hergestellt hat, stellen Sie sicher, dass sie ordnungsgemäß für Assurance eingerichtet ist. Siehe Anweisungen zum Installieren der SDK-Bibliothek {](./tutorials/implement-assurance.md)}Adobe Experience Platform Assurance.[
* Stellen Sie sicher, dass die Sitzung mit dem Link übereinstimmt und korrekt für die erwartete Sitzung eingegeben wird. Siehe [Protokollmeldung „OrgID-Informationen sind nicht verfügbar“](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (dies ist ungewöhnlich und nur relevant, wenn Sie Zugriff auf mehr als eine ORG-Instanz haben).

### Adobe Analytics-Debugging

**Status der Nachbearbeitung - Keine Debugging-Markierung**

Wenn in Ihrer Analytics-Ereignisansicht Ereignisse mit dem Nachbearbeitungsstatus „Keine Debugging-Markierung“ fehlschlagen, unterstützt Ihre aktuelle Adobe Analytics- oder Assurance SDK-Version möglicherweise nicht die Analytics-Debugging-Funktion.
Aktualisieren Sie die Erweiterungen Adobe Analytics und Assurance SDK auf die neuesten Versionen, um dieses Problem zu beheben.

| Mindestanforderung an die Version | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### Kompatibilität von React Native MobileCore und AEPAssurance

| AEP Assurance-Version | Mobile-Kernversion | Installationsanweisung |
| --------------------- | ------------------- | ------------------- |
| react-native-aepAssurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepAssurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Wenn Sie `react-native-acpcore` mit Assurance verwenden, kann das React Native-Programm mit einer der folgenden Fehlermeldungen fehlschlagen:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

oder

```
AppDelegate: AEPAssurance.h file not found
```

**Lösung**

In diesem Fall stufen Sie Ihre `react-native-aepassurance` mit dem folgenden npm-Befehl herunter:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Dieser Fehler tritt auf, weil die `react-native-acpcore`-Erweiterung **nur** mit `react-native-aepassurance` Versionen 2.x.x und darunter kompatibel ist.
