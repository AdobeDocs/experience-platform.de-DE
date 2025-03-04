---
solution: Data Collection
audience: user
user-guide-title: Hilfe zu Adobe Experience Platform Web SDK
breadcrumb-title: Web SDK-Handbuch
user-guide-description: Interagieren Sie mit Experience Cloud-Services über das Edge-Netzwerk.
feature: Web SDK
role: Developer
source-git-commit: bed63cb9be1ffe39a538d1c3f8be9065ffb2ca28
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 50%

---


# Adobe Experience Platform Web SDK {#web-sdk}

* [Web SDK – Übersicht](home.md)
* [Versionshinweise](release-notes.md)
* Web SDK-{#install}
   * [Überblick](install/overview.md)
   * [Installieren von Web SDK mithilfe der Tag-Erweiterung](install/extension.md)
   * [Installieren von Web SDK mithilfe der JavaScript-Bibliothek](install/library.md)
   * [Installieren von Web SDK mithilfe des NPM-Pakets](install/npm.md)
   * [Erstellen eines benutzerdefinierten Web-SDK-Builds mit dem NPM-Paket](install/create-custom-build.md)
* Befehle {#commands}
   * Konfigurieren von {#configure}
      * [Überblick](commands/configure/overview.md)
      * [autoCollectPropositionInteractions](commands/configure/autocollectpropositioninteractions.md)
      * [clickCollectionEnabled](commands/configure/clickcollectionenabled.md)
      * [clickCollection](commands/configure/clickcollection.md)
      * [Kontext](commands/configure/context.md)
      * [datastreamId](commands/configure/datastreamid.md)
      * [debugEnabled](commands/configure/debugenabled.md)
      * [defaultConsent](commands/configure/defaultconsent.md)
      * [downloadLinkQualifier](commands/configure/downloadlinkqualifier.md)
      * [edgeBasePath](commands/configure/edgebasepath.md)
      * [edgeDomain](commands/configure/edgedomain.md)
      * [idMigrationEnabled](commands/configure/idmigrationenabled.md)
      * [StreamingMedia](commands/configure/streamingmedia.md)
      * [onBeforeEventSend](commands/configure/onbeforeeventsend.md)
      * [onBeforeLinkClickSend](commands/configure/onbeforelinkclicksend.md)
      * [orgId](commands/configure/orgid.md)
      * [PrehidingStyle](commands/configure/prehidingstyle.md)
      * [targetMigrationEnabled](commands/configure/targetmigrationenabled.md)
      * [thirdPartyCookiesEnabled](commands/configure/thirdpartycookiesenabled.md)
   * sendEvent-{#sendevent}
      * [Überblick](commands/sendevent/overview.md)
      * [data](commands/sendevent/data.md)
      * [DokumentEntladen](commands/sendevent/documentunloading.md)
      * [Personalisierung](commands/sendevent/personalization.md)
      * [renderDecisions](commands/sendevent/renderdecisions.md)
      * [type](commands/sendevent/type.md)
      * [XDM](commands/sendevent/xdm.md)
   * [appendIdentityToUrl](commands/appendidentitytourl.md)
   * [applyPropositions](commands/applypropositions.md)
   * [applyResponse](commands/applyresponse.md)
   * [createMediaSession](commands/createmediasession.md)
   * [getIdentity](commands/getidentity.md)
   * [getLibraryInfo](commands/getlibraryinfo.md)
   * [getMediaAnalyticsTracker](commands/getmediaanalyticstracker.md)
   * [setConsent](commands/setconsent.md)
   * [setDebug](commands/setdebug.md)
   * [sendMediaEvent](commands/sendmediaevent.md)
   * [subscribeRulesetItems](commands/subscriberulesetitems.md)
   * [Konfigurieren von Datenstromüberschreibungen](commands/datastream-overrides.md)
   * [Befehlsantworten](commands/command-responses.md)

* Identität {#identity}
   * [Übersicht](identity/overview.md)
   * [IDs von Erstanbieter-Geräten](identity/first-party-device-ids.md)
   * [Mobile-zu-Web und Domain-übergreifender ID-Austausch](identity/id-sharing.md)

* Personalisierung {#personalization}
   * [Anzeigeereignisse verwalten](personalization/display-events.md)
   * [Rendern von personalisierten Inhalten](personalization/rendering-personalization-content.md)
   * [Personalisierung über Hybridimplementierung](personalization/hybrid-personalization.md)
   * [Verwalten von Flackern](personalization/manage-flicker.md)
   * Adobe Target {#adobe-target}
      * [Übersicht](personalization/adobe-target/target-overview.md)
      * [Implementierung von Einzelseitenanwendungen](personalization/adobe-target/spa-implementation.md)
      * [Zugriff auf Antwort-Token](personalization/adobe-target/accessing-response-tokens.md)
      * [Verwenden der mBox-Drittanbieter-ID](personalization/adobe-target/using-mbox-3rdpartyid.md)
      * [Vergleich der at.js-Bibliothek mit dem Web SDK](personalization/adobe-target/web-sdk-atjs-comparison.md)
      * Analytics for Target (A4T)-Protokollierung {#a4t}
         * [Übersicht](personalization/adobe-target/analytics-logging/overview.md)
         * [Client-seitige Protokollierung](personalization/adobe-target/analytics-logging/client-side.md)
         * [Server-seitige Protokollierung](personalization/adobe-target/analytics-logging/server-side.md)
   * Offer Decisioning {#offer-decisioning}
      * [Übersicht](personalization/offer-decisioning/offer-decisioning-overview.md)
   * Adobe Journey Optimizer {#ajo}
      * [Übersicht](personalization/ajo/overview.md)
      * [Implementierung von Einzelseitenanwendungen](personalization/ajo/web-spa-implementation.md)
      * [Konfigurieren der Web-In-App-Messaging-Unterstützung in Web SDK](personalization/web-in-app-messaging.md)

* Einverständnis {#consent}
   * IAB-Transparenz und -Einverständnis – Framework 2.0 {#iab-tcf}
      * [Übersicht](consent/iab-tcf/overview.md)
      * [Integrieren mit Tags](consent/iab-tcf/with-tags.md)
      * [Integrieren ohne Tags](consent/iab-tcf/without-tags.md)

* Anwendungsfälle {#use-cases}
   * [Überblick](use-cases/overview.md)
   * [Senden von Daten an Adobe Analytics mithilfe der Web-SDK](use-cases/adobe-analytics.md)
   * [User Agent Client-Hinweise](use-cases/client-hints.md)
   * [Erfassen von Commerce-Daten](use-cases/collect-commerce-data.md)
   * [Konfigurieren eines CSP](use-cases/configuring-a-csp.md)
   * [Debugging-Methoden](use-cases/debugging.md)
   * [Verwenden mehrerer SDK-Web-Instanzen](use-cases/multiple-instances.md)
   * [Konfigurieren von Ereignissen der oberen und unteren Seite](use-cases/top-bottom-page-events.md)
* [Überwachungshaken](monitoring-hooks.md)
* [Häufig gestellte Fragen](faq.md)
* [Ressourcen](resources.md)
