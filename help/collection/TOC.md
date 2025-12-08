---
audience: user
solution: Data Collection
user-guide-title: Datenerfassung
breadcrumb-title: Datenerfassung
user-guide-description: Erfahren Sie, wie Sie Daten an Adobe Experience Platform senden.
feature: Data Collection
role: Developer
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 38%

---


# Datenerfassung {#collection}

+ [Überblick](home.md)
+ [Berechtigungen](permissions.md)
+ BrightScript {#brightscript}
   + [BrightScript-Übersicht](brightscript/brs-overview.md)
+ JavaScript {#js}
   + [Übersicht über Web SDK JavaScript](js/js-overview.md)
   + [Versionshinweise](js/release-notes.md)
   + Installation {#install}
      + [Installationsübersicht](js/install/overview.md)
      + [Bibliothek](js/install/library.md)
      + [NPM](js/install/npm.md)
      + [Benutzerdefinierter Build](js/install/create-custom-build.md)
   + Commands {#commands}
      + [appendIdentityToUrl](js/commands/appendidentitytourl.md)
      + [applyPropositions](js/commands/applypropositions.md)
      + [applyResponse](js/commands/applyresponse.md)
      + configure {#configure}
         + [Überblick](js/commands/configure/overview.md)
         + [autoCollectPropositionInteractions](js/commands/configure/autocollectpropositioninteractions.md)
         + [clickCollection](js/commands/configure/clickcollection.md)
         + [clickCollectionEnabled](js/commands/configure/clickcollectionenabled.md)
         + [Kontext](js/commands/configure/context.md)
         + [datastreamId](js/commands/configure/datastreamid.md)
         + [debugEnabled](js/commands/configure/debugenabled.md)
         + [defaultConsent](js/commands/configure/defaultconsent.md)
         + [downloadLinkQualifier](js/commands/configure/downloadlinkqualifier.md)
         + [edgeBasePath](js/commands/configure/edgebasepath.md)
         + [edgeConfigOverrides](js/commands/configure/edgeconfigoverrides.md)
         + [edgeDomain](js/commands/configure/edgedomain.md)
         + [idMigrationEnabled](js/commands/configure/idmigrationenabled.md)
         + [onBeforeEventSend](js/commands/configure/onbeforeeventsend.md)
         + [onBeforeLinkClickSend](js/commands/configure/onbeforelinkclicksend.md)
         + [orgId](js/commands/configure/orgid.md)
         + [PrehidingStyle](js/commands/configure/prehidingstyle.md)
         + [Push-Benachrichtigungen](js/commands/configure/pushnotifications.md)
         + [StreamingMedia](js/commands/configure/streamingmedia.md)
         + [targetMigrationEnabled](js/commands/configure/targetmigrationenabled.md)
         + [thirdPartyCookiesEnabled](js/commands/configure/thirdpartycookiesenabled.md)
      + [createMediaSession](js/commands/createmediasession.md)
      + [getIdentity](js/commands/getidentity.md)
      + [getLibraryInfo](js/commands/getlibraryinfo.md)
      + [getMediaAnalyticsTracker](js/commands/getmediaanalyticstracker.md)
      + sendEvent {#sendevent}
         + [Überblick](js/commands/sendevent/overview.md)
         + [data](js/commands/sendevent/data.md)
         + [DokumentEntladen](js/commands/sendevent/documentunloading.md)
         + [edgeConfigOverrides](js/commands/sendevent/edgeconfigoverrides.md)
         + [eventType](js/commands/sendevent/eventtype.md)
         + [Personalisierung](js/commands/sendevent/personalization.md)
         + [renderDecisions](js/commands/sendevent/renderdecisions.md)
         + [XDM](js/commands/sendevent/xdm.md)
      + [sendMediaEvent](js/commands/sendmediaevent.md)
      + [sendPushSubscription](js/commands/sendpushsubscription.md)
      + [setConsent](js/commands/setconsent.md)
      + [setDebug](js/commands/setdebug.md)
      + [subscribeRulesetItems](js/commands/subscriberulesetitems.md)
      + [Befehlsantworten](js/commands/command-responses.md)
   + [Überwachungshaken](js/monitoring-hooks.md)
   + [Häufig gestellte Fragen](js/faq.md)
+ Client-seitige JavaScript für Tags {#tags}
   + [Überblick](tags/overview.md)
   + [buildInfo](tags/buildinfo.md)
   + [Gesellschaft](tags/company.md)
   + [_container](tags/container.md)
   + [Cookie](tags/cookie.md)
   + [Umgebung](tags/environment.md)
   + [getVar](tags/getvar.md)
   + [getVisitorId](tags/getvisitorid.md)
   + [logger](tags/logger.md)
   + [_monitore](tags/monitors.md)
   + [setDebug](tags/setdebug.md)
   + [setVar](tags/setvar.md)
   + [track](tags/track.md)
+ Anwendungsfälle {#use-cases}
   + [Überblick](use-cases/overview.md)
   + [Client hints](use-cases/client-hints.md)
   + [Client-Status](use-cases/client-state.md)
   + [Erfassen von Commerce-Daten](use-cases/collect-commerce-data.md)
   + [Konfigurieren eines CSP](use-cases/configuring-a-csp.md)
   + [Debugging](use-cases/debugging.md)
   + [Ereignis-Deduplizierung](use-cases/event-duplication.md)
   + Identität {#identity}
      + [Überblick](use-cases/identity/id-overview.md)
      + [IDs von Erstanbieter-Geräten](use-cases/identity/first-party-device-ids.md)
      + [ID-Freigabe](use-cases/identity/id-sharing.md)
   + [Mehrere SDK-Instanzen](use-cases/multiple-instances.md)
   + Personalisierung {#personalization}
      + [Überblick](use-cases/personalization/pers-overview.md)
      + [Ereignisse anzeigen](use-cases/personalization/display-events.md)
      + [Verwalten von Flackern](use-cases/personalization/manage-flicker.md)
      + [Rendern von personalisiertem Inhalt](use-cases/personalization/rendering-personalization-content.md)
      + [Ereignisse der oberen und unteren Seite](use-cases/personalization/top-bottom-page-events.md)
