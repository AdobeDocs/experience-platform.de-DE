---
solution: Data Collection
audience: user
user-guide-title: Hilfe zu Adobe Experience Platform Web SDK
breadcrumb-title: Web SDK-Handbuch
user-guide-description: Interagieren Sie mit Experience Cloud-Services über das Edge-Netzwerk.
feature: Web SDK
source-git-commit: 2b9edb258e647dc04faadbbaeab429cf8ac3e0ec
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 84%

---


# Adobe Experience Platform Web SDK {#edge}

* [Platform Web-SDK – Übersicht](home.md)
* Grundlagen {#fundamentals}
   * [Voraussetzungen](fundamentals/prerequisite.md)
   * [Installieren des SDK](fundamentals/installing-the-sdk.md)
   * [Konfigurieren des SDK](fundamentals/configuring-the-sdk.md)
   * [Ausführen von Befehlen](fundamentals/executing-commands.md)
   * [Verfolgen von Ereignissen](fundamentals/tracking-events.md)
   * [Debugging](fundamentals/debugging.md)
   * [Konfigurieren eines CSP](fundamentals/configuring-a-csp.md)
   * [Interaktion mit mehreren Eigenschaften](fundamentals/interacting-with-multiple-properties.md)
   * [Unterstützte Anwendungsfälle](fundamentals/supported-use-cases.md)
* Datenströme {#datastreams}
   * [Übersicht](./datastreams/overview.md)
   * [Datenvorbereitung für die Datenerfassung](./datastreams/data-prep.md)
* Identität {#identity}
   * [Übersicht](identity/overview.md)
   * [IDs von Erstanbieter-Geräten](identity/first-party-device-ids.md)
   * [Mobile-zu-Web und Domain-übergreifender ID-Austausch](identity/id-sharing.md)
* Datenerfassung {#data-collection}
   * [Automatisch erfasste Informationen](data-collection/automatic-information.md)
   * [Verfolgen von Links](data-collection/track-links.md)
   * [Sammeln von Handels- und Produktdaten](data-collection/collect-commerce-data.md)
   * Adobe Analytics {#adobe-analytics}
      * [Verwenden von Adobe Analytics mit dem Platform Web SDK](data-collection/adobe-analytics/analytics-overview.md)
      * [Zuordnen von Analytics-Variablen](data-collection/adobe-analytics/manually-mapping-variables.md)
      * [Automatisch zugeordnete Variablen](data-collection/adobe-analytics/automatically-mapped-vars.md)
      * [Senden von Daten an Analytics](data-collection/adobe-analytics/sending-data-to-analytics.md)
* Personalisierung {#personalization}
   * [Rendern von personalisierten Inhalten](personalization/rendering-personalization-content.md)
   * [Verwalten von Flackern](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Übersicht](personalization/adobe-target/target-overview.md)
      * [Implementierung von Einzelseitenanwendungen](personalization/adobe-target/spa-implementation.md)
      * [Zugriff auf Antwort-Token](personalization/adobe-target/accessing-response-tokens.md)
      * [Verwenden der Mbox-Drittanbieter-ID](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Vergleich der at.js-Bibliothek mit dem Web SDK](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Protokollierung von Analytics for Target (A4T) {#a4t}
         * [Überblick](personalization/adobe-target/analytics-logging/overview.md)
         * [Client-seitig Protokollierung](personalization/adobe-target/analytics-logging/client-side.md)
         * [Serverseitige Protokollierung](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [Übersicht](personalization/offer-decisioning/offer-decisioning-overview.md)
* Einverständnis {#consent}
   * [Unterstützen von Zustimmung](consent/supporting-consent.md)
   * IAB-Transparenz und -Einverständnis – Framework 2.0 {#iab-tcf}
      * [Übersicht](consent/iab-tcf/overview.md)
      * [Integrieren mit Tags](consent/iab-tcf/with-launch.md)
      * [Integrieren ohne Tags](consent/iab-tcf/without-launch.md)
* Web SDK-Tag-Erweiterung {#extension}
   * [Web SDK-Erweiterung](extension/web-sdk-extension-configuration.md)
   * [Ereignistypen](extension/event-types.md)
   * [Aktionstypen](extension/action-types.md)
   * [Datenelementtypen](extension/data-element-types.md)
   * [Zugreifen auf die ECID](extension/accessing-the-ecid.md)
   * [Versionshinweise zur Web SDK-Erweiterung](extension/web-sdk-ext-release-notes.md)
* [Versionshinweise](release-notes.md)
* [Häufig gestellte Fragen](web-sdk-faq.md)
* [Ressourcen](resources.md)
