---
title: Handbuch zur Fehlerbehebung bei Adobe Experience Platform Assurance
description: In diesem Dokument werden Lösungen für häufige Probleme bei der Verwendung von Adobe Experience Platform Assurance beschrieben.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---


# Fehlerbehebung bei Adobe Experience Platform Assurance

Wenn Sie Schwierigkeiten haben, die Zuverlässigkeitserklärung zu verwenden, sehen Sie sich die Vorschläge in den folgenden Problemthemen an, um häufig aufgetretene Probleme zu beheben.

Um eine reibungslosere Implementierung zu ermöglichen und potenzielle Probleme zu erkennen, stellen Sie sicher, dass die SDK-Protokollierung pro [Aktivieren der Debug-Protokollierung](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) im Abschnitt &quot;Erste Schritte&quot;.

Sie können die SDK-Protokollebenen mithilfe der Variablen [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API.

## Auf dem Gerät, App-Probleme

### QR-Code öffnet die App nicht

* Greifen Sie direkt auf den Link zu. Link kopieren aus **Sitzungsdetails**. Fügen Sie ihn in die Adressleiste des Geräts ein, um ihn zu öffnen. Wenn es nicht geöffnet wird, lesen Sie den Abschnitt . [Der Link zum Öffnen der App wird nicht geöffnet](#app-does-not-open-link).
* Verwenden Sie einen anderen QR-Reader. Verwenden Sie für iOS 11 oder höher die Foto-App, um den QR-Code zu lesen.

### Link wird nicht von der Anwendung geöffnet

* Überprüfen Sie, ob die Deep-Link-Implementierung in der App richtig konfiguriert ist.
   * **Android:** Deep-Links (App-Links)
      * [Erstellen von Deep-Links zum App-Kontext](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** Benutzerdefiniertes URL-Schema oder universelle Links
      * [Definieren eines benutzerdefinierten URL-Schemas für Ihre App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Unterstützung universeller Links in Ihrer App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Bei Android wird die `startSession` API muss nicht explizit aufgerufen werden. Verwenden Sie für iOS die -API wie in [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### Die Authentifizierungsüberlagerung wird angezeigt, aber die App kann keine Verbindung herstellen

* Stellen Sie die Internetverbindung des Geräts über den Geräte-Webbrowser sicher.
* Wenn die App noch nie erfolgreich eine Verbindung zum Assurance-Dienst hergestellt hat, stellen Sie sicher, dass die App ordnungsgemäß für Assurance eingerichtet ist. Siehe Anweisungen zur Installation der [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) SDK-Bibliothek.
* Überprüfen Sie, ob die Sitzung mit dem Link übereinstimmt und für die erwartete Sitzung korrekt eingegeben wird. Siehe [Protokollmeldung &quot;OrgID-Informationen sind nicht verfügbar&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (Dies ist nur gelegentlich und relevant, wenn Sie Zugriff auf mehr als eine ORG-Instanz haben).

### Adobe Analytics Debugging

**Status der Nachbearbeitung - kein Debug-Flag**

Wenn in Ihrer Analytics-Ereignisansicht Ereignisse mit dem Status &quot;Keine Debug-Markierung&quot;nach der Verarbeitung fehlschlagen, wird die Analytics-Debugging-Funktion in Ihrer aktuellen Adobe Analytics- oder Assurance-SDK-Version möglicherweise nicht unterstützt.
Bitte aktualisieren Sie die Adobe Analytics- und Assurance SDK-Erweiterungen auf die neuesten Versionen, um dieses Problem zu beheben.

| Mindestanforderung an die Version | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### Kompatibilität von React Native MobileCore und AEPAsurance

| AEP Assurance-Version | Mobile Core-Version | Installationsanleitung |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Wenn Sie `react-native-acpcore` Mit Assurance kann die native Anwendung React mit einer der folgenden Fehlermeldungen nicht erstellt werden:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

oder

```
AppDelegate: AEPAssurance.h file not found
```

**Lösung**

Sollte dies eintreten, sollten Sie Ihre `react-native-aepassurance` mit dem folgenden npm-Befehl:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Dieser Fehler tritt auf, weil die `react-native-acpcore` Erweiterung **only** kompatibel mit `react-native-aepassurance` Versionen 2.x.x und höher.
