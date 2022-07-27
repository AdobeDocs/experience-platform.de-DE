---
audience: user
user-guide-title: Zielhandbuch
user-guide-description: Aktivieren Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, gezielte Werbung und viele andere Anwendungsfälle.
description: Dieses Dokument listet das Inhaltsverzeichnis für Adobe Experience Platform-Ziele auf
feature: Destinations
source-git-commit: 97f68a0d11b1b1fb51f230eee5f1f1e6b6ca2307
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 84%

---


# Ziele {#destinations}

* [Ziele – Übersicht](./home.md)
* [Zieltypen und Kategorien](./destination-types.md)
* API-Tutorials {#api}
   * [Verbinden Sie sich mit Streaming-Zielen und aktivieren Sie Daten über die Flow Service-API](./api/streaming-destinations.md)
   * [Verbinden Sie sich mit Batch-Cloud-Speicher und E-Mail-Marketing-Zielen und aktivieren Sie Daten mit der Flow Service-API](./api/connect-activate-batch-destinations.md)
   * [(Beta) Aktivieren von Zielgruppensegmenten für Batch-Ziele über die Ad-hoc-Aktivierungs-API](./api/ad-hoc-activation-api.md)
   * [Aktualisieren von Ziel-Datenflüssen](./api/update-destination-dataflows.md)
   * [Löschen von Zielkonten](./api/delete-destination-account.md)
   * [Zieldatenflüsse löschen](./api/delete-destination-dataflow.md)
* UI-Handbücher {#ui}
   * [Arbeitsbereich „Ziele“](./ui/destinations-workspace.md)
   * [Erstellen einer neuen Zielverbindung](./ui/connect-destination.md)
   * Aktivieren von Zielgruppendaten für Ziele {#activate}
      * [Aktivierungsübersicht](./ui/activation-overview.md)
      * [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](./ui/activate-segment-streaming-destinations.md)
      * [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](./ui/activate-streaming-profile-destinations.md)
      * [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](./ui/activate-batch-profile-destinations.md)
      * [Aktivieren von Zielgruppendaten für Profilanforderungsziele](./ui/activate-profile-request-destinations.md)
      * [Konfigurieren von Personalisierungszielen für die Personalisierung auf derselben Seite und auf der nächsten Seite](./ui/configure-personalization-destinations.md)
      * [(Beta) Exportieren Sie Dateien On-Demand mithilfe der Experience Platform-Benutzeroberfläche in Batch-Ziele](./ui/export-file-now.md)
   * [Anzeigen von Zieldetails](./ui/destination-details-page.md)
   * [Aktualisieren von Zielkonten](./ui/update-accounts.md)
   * [Löschen von Zielkonten](./ui/delete-destination-account.md)
   * [Bearbeiten von Aktivierungsdatenflüssen](./ui/edit-activation.md)
   * [Löschen von Zielen](./ui/delete-destinations.md)
   * [Überwachen von Datenflüssen](./ui/monitor-dataflows.md)
   * [In-Context-Zielwarnungen abonnieren](ui/alerts.md)
* Zielkatalog {#catalog}
   * [Zielkatalog – Übersicht](./catalog/overview.md)
   * Adobe-Ziele {#adobe}
      * [Adobe-Ziele – Übersicht](./catalog/adobe/overview.md)
      * [Marketo Engage-Verbindung](./catalog/adobe/marketo-engage.md)
      * [Segmentfreigabe in Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de)
   * Werbeziele {#advertising}
      * [Werbeziele – Übersicht](./catalog/advertising/overview.md)
      * [Adobe Advertising Cloud-Verbindung](./catalog/advertising/adobe-advertising-cloud-connection.md)
      * [Adobe Advertising Cloud-Erweiterung](./catalog/advertising/adobe-advertising-cloud.md)
      * [Awin Advertising Conversion Tag-Erweiterung](./catalog/advertising/awin-conversiontag.md)
      * [Awin Advertiser Mastertag-Erweiterung](./catalog/advertising/awin-mastertag.md)
      * [Erweiterung für Bing Ads Universal Event Tracking (UET)](./catalog/advertising/bing-ads.md)
      * [Branch-Erweiterung](./catalog/advertising/branch.md)
      * [(Beta) Criteo-Verbindung](./catalog/advertising/criteo.md)
      * [DoubleClick Floodlight (Beta)-Erweiterung](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook-Pixel-Erweiterung](./catalog/advertising/facebook-pixel.md)
      * [Flashspeak OneTag-Erweiterung](./catalog/advertising/flashtalking.md)
      * [Google Ads-Verbindung](./catalog/advertising/google-ads-destination.md)
      * [Google Ads-Erweiterung](./catalog/advertising/google-ads-extension.md)
      * [Google Ad Manager-Verbindung](./catalog/advertising/google-ad-manager.md)
      * [(Beta) Google Ad Manager 360-Verbindung](./catalog/advertising/google-ad-manager-360-connection.md)
      * [Google Customer Match-Verbindung](./catalog/advertising/google-customer-match.md)
      * [Google Display &amp; Video 360-Verbindung](./catalog/advertising/google-dv360.md)
      * [Google gtag-Erweiterung](./catalog/advertising/gtag-advertising.md)
      * [LinkedIn Insight Tag-Erweiterung](./catalog/advertising/linkedin.md)
      * [Microsoft Bing-Verbindung](./catalog/advertising/bing.md)
      * [Pinterest Conversion Tracking-Erweiterung](./catalog/advertising/pinterest-extension.md)
      * [Pinterest Customer List-Verbindung](./catalog/advertising/pinterest.md)
      * [(Beta) Snapchat Ads-Verbindung](./catalog/advertising/snap-inc.md)
      * [The Trade Desk-Verbindung](./catalog/advertising/tradedesk.md)
      * [Die CRM-Verbindung des Trade Desk](./catalog/advertising/tradedesk-emails.md)
      * [Twitter Universal Website Tag-Erweiterung](./catalog/advertising/twitter-uwt.md)
      * [Yahoo/Verizon DataX-Verbindung](./catalog/advertising/datax.md)
   * Analyseziele {#analytics}
      * [Analyseziele – Übersicht](./catalog/analytics/overview.md)
      * [Adform Website Tracking-Erweiterung](./catalog/analytics/adform.md)
      * [Adobe Analytics-Erweiterung](./catalog/analytics/adobe-analytics.md)
      * [Adobe Media Analytics für Audio und Video-Erweiterung](./catalog/analytics/adobe-video-analytics.md)
      * [Clicktale-Erweiterung](./catalog/analytics/clicktale.md)
      * [Contentsquare-Erweiterung](./catalog/analytics/contentsquare.md)
      * [Decibel-Erweiterung](./catalog/analytics/decibel.md)
      * [Demandbase-Erweiterung](./catalog/analytics/demandbase.md)
      * [DialogTech-Erweiterung](./catalog/analytics/dialogtech.md)
      * [Google Global Site Tag-Erweiterung](./catalog/analytics/gtag-analytics.md)
      * [Google Universal Analytics-Erweiterung](./catalog/analytics/google-universal-analytics.md)
      * [JW Player Analytics (Beta)-Erweiterung](./catalog/analytics/jw-player-analytics.md)
      * [Nielsen BSDK-Erweiterung](./catalog/analytics/nielsen-bsdk.md)
      * [Nielsen IMA Handler-Erweiterung](./catalog/analytics/nielsen-ima.md)
      * [Nielsen VideoJS Player Handler-Erweiterung](./catalog/analytics/nielsen-videojs.md)
      * [Parse.ly Analytics-Erweiterung](./catalog/analytics/parsely.md)
      * [Quantum Metric-Erweiterung](./catalog/analytics/quantum-metric.md)
      * [SessionCam-Erweiterung](./catalog/analytics/sessioncam.md)
      * [TMMData-Erweiterung](./catalog/analytics/tmmdata.md)
      * [Yext Conversion Tracking-Erweiterung](./catalog/analytics/yext.md)
   * Cloud-Speicher-Ziele {#cloud-storage}
      * [Cloud-Speicher-Ziele – Übersicht](./catalog/cloud-storage/overview.md)
      * [Amazon Kinesis-Verbindung](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3-Verbindung](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob-Verbindung](./catalog/cloud-storage/azure-blob.md)
      * [Azure Event Hubs-Verbindung](./catalog/cloud-storage/azure-event-hubs.md)
      * [SFTP-Verbindung](./catalog/cloud-storage/sftp.md)
      * [IP-Adresse - Zulassungsliste für Cloud-Speicher-Ziele](./catalog/cloud-storage/ip-address-allow-list.md)
   * Data Management Platform-Ziele {#data-management}
      * [Data Management Platform (DMP)-Ziele – Übersicht](./catalog/data-management/overview.md)
      * [Audience Manager DIL-Erweiterung](./catalog/data-management/aam-dil-extension.md)
   * E-Mail-Ziele {#email}
      * [Bizible-Erweiterung](./catalog/email/bizible.md)
      * [Marketo-Erweiterung](./catalog/email/marketo.md)
      * [Marketo Munchkin-Erweiterung](./catalog/email/marketo-munchkin.md)
      * [PebblePost-Erweiterung](./catalog/email/pebblepost.md)
   * E-Mail-Marketing-Ziele {#email-marketing}
      * [E-Mail-Marketing-Ziele – Übersicht](./catalog/email-marketing/overview.md)
      * [Adobe Campaign-Verbindung](./catalog/email-marketing/adobe-campaign.md)
      * [Oracle Eloqua-Verbindung](./catalog/email-marketing/oracle-eloqua.md)
      * [Oracle Responsys-Verbindung](./catalog/email-marketing/oracle-responsys.md)
      * [(API) Salesforce-Marketing Cloud-Verbindung](./catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)
      * [(Dateien) Salesforce-Marketing Cloud-Verbindung](./catalog/email-marketing/salesforce-marketing-cloud.md)
      * [SendGrid-Verbindung](./catalog/email-marketing/sendgrid.md)
   * Tag-Erweiterungen {#launch-extensions}
      * [Übersicht über Tag-Erweiterungen](./catalog/launch-extensions/overview.md)
   * Ziele für mobile Interaktion {#mobile-engagement}
      * [Ziele für mobile Interaktion – Übersicht](./catalog/mobile-engagement/overview.md)
      * [Airship Attributes-Verbindung](./catalog/mobile-engagement/airship-attributes.md)
      * [Airship Tags-Verbindung](./catalog/mobile-engagement/airship-tags.md)
      * [Braze-Verbindung](./catalog/mobile-engagement/braze.md)
   * Personalisierungsziele {#personalization}
      * [Personalisierungsziele – Übersicht](./catalog/personalization/overview.md)
      * [Adobe Target-Verbindung](./catalog/personalization/adobe-target-connection.md)
      * [Adobe Target-Erweiterung](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2-Erweiterung](./catalog/personalization/adobe-target-v2.md)
      * [Beemray-Erweiterung](./catalog/personalization/beemray.md)
      * [Benutzerdefinierte Personalisierungsverbindung](./catalog/personalization/custom-personalization.md)
      * [D&amp;B Visitor Intelligence-Erweiterung](./catalog/personalization/dnb.md)
      * [Experience Cloud-ID-Service-Erweiterung](./catalog/personalization/adobe-ecid.md)
      * [Gainsight-Erweiterung](./catalog/personalization/gainsight.md)
      * [KickFire-Erweiterung](./catalog/personalization/kickfire.md)
      * [Marketo Web-Personalisierungserweiterung](./catalog/personalization/marketo-web-personalization.md)
      * [Pega Customer Decision Hub-Verbindung](./catalog/personalization/pega.md)
   * Social-Media-Ziele {#social}
      * [Social-Media-Ziele – Übersicht](./catalog/social/overview.md)
      * [Adobe Livefyre-Erweiterung](./catalog/social/adobe-livefyre.md)
      * [Facebook-Verbindung](./catalog/social/facebook.md)
      * [LinkedIn Matched Audiences-Verbindung](./catalog/social/linkedin.md)
      * [[!DNL Twitter Custom Audiences]-Verbindung](./catalog/social/twitter.md)
   * Streaming-Ziele {#streaming}
      * [HTTP-API-Verbindung](./catalog/streaming/http-destination.md)
      * [IP-Adressen-Zulassungsliste für Streaming-Ziele](./catalog/streaming/ip-address-allow-list.md)
   * Umfrageziele {#survey}
      * [Umfrageziele – Übersicht](./catalog/survey/overview.md)
      * [Foresee-Erweiterungsziel](./catalog/survey/foresee.md)
      * [InMoment-Erweiterung](./catalog/survey/inmoment.md)
      * [Qualtrics Website Feedback-Erweiterung](./catalog/survey/qualtrics.md)
      * [QuestionPro Intercept Surveys-Erweiterung](./catalog/survey/web-intercept-surveys.md)
   * Sprache der Kundenziele {#voice}
      * [Sprache der Kundenziele – Übersicht](./catalog/voice/overview.md)
      * [Confirmit Digital Feedback-Erweiterung](./catalog/voice/confirmit-digital-feedback.md)
      * [Invoca Tags-Erweiterung](./catalog/voice/invoca.md)
      * [Medallia-Verbindung](./catalog/voice/medallia-connector.md)
      * [Medallia-Erweiterung](./catalog/voice/medallia.md)
      * [Talk URL Inbox-Erweiterung](./catalog/voice/talkurl.md)
* Destination SDK {#destination-sdk}
   * [Übersicht](./destination-sdk/overview.md)
   * [Voraussetzungen für die Integration](./destination-sdk/integration-prerequisites.md)
   * [Erste Schritte](./destination-sdk/getting-started.md)
   * Funktionen des Destination SDK {#functionality}
      * [Konfigurationsoptionen](./destination-sdk/configuration-options.md)
      * [Konfiguration des Streaming-Ziels](./destination-sdk/destination-configuration.md)
      * [(Beta) Konfiguration dateibasierter Ziele](./destination-sdk/file-based-destination-configuration.md)
      * [Server- und Vorlagenspezifikationen für Streaming-Ziele](./destination-sdk/server-and-template-configuration.md)
      * [(Beta) Dateibasierte Ziel-Server- und Dateispezifikationen](./destination-sdk/server-and-file-configuration.md)
      * [Nachrichtenformat](./destination-sdk/message-format.md)
      * [Verwaltung von Zielgruppen-Metadaten](./destination-sdk/audience-metadata-management.md)
      * Authentifizierung {#authentication}
         * [Authentifizierungskonfiguration](./destination-sdk/authentication-configuration.md)
         * [OAuth 2-Authentifizierung](./destination-sdk/oauth2-authentication.md)
      * Entwickler-Tools {#developer-tools}
         * [Erstellen und Testen einer Nachrichten-Umwandlungsvorlage](./destination-sdk/create-template.md)
         * [Testen einer Zielkonfiguration](./destination-sdk/test-destination.md)
   * API-Vorgänge {#api}
      * [API-Referenz zum Destination SDK (Destination Authoring)](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * [API-Vorgänge für Ziel-Endpunkte](./destination-sdk/destination-configuration-api.md)
      * [API-Vorgänge für Ziel-Server-Endpunkte](./destination-sdk/destination-server-api.md)
      * [API-Vorgänge für Zielgruppen-Metadaten-Endpunkte](./destination-sdk/audience-metadata-api.md)
      * [API-Vorgänge für Zugriffsdaten-Endpunkte](./destination-sdk/credentials-configuration-api.md)
      * [Veröffentlichen von Endpunkt-API-Vorgänge](./destination-sdk/destination-publish-api.md)
      * Referenz zu Entwickler-Tools {#developer-tools-reference}
         * Streaming-Ziel-Test-API {#streaming-destination-testing-api}
            * [Abrufen von Beispielvorlagen-API-Vorgängen](./destination-sdk/sample-template-api.md)
            * [API-Vorgänge für Rendervorlagen](./destination-sdk/render-template-api.md)
            * [API-Vorgänge für Zieltests](./destination-sdk/destination-testing-api.md)
            * [Beispiele für API-Vorgänge zur Profilerstellung](./destination-sdk/sample-profile-generation-api.md)
         * Dateibasierte Ziel-Test-API {#file-based-destination-testing-api}
            * [Übersicht über die dateibasierte Ziel-Test-API](./destination-sdk/file-based-destination-testing-overview.md)
            * [Erstellen von Beispielprofilen basierend auf einem Quellschema](./destination-sdk/file-based-sample-profile-generation-api.md)
            * [Testen Ihres dateibasierten Ziels mit Beispielprofilen](./destination-sdk/file-based-destination-testing-api.md)
            * [Detaillierte Aktivierungsergebnisse anzeigen](./destination-sdk/file-based-destination-results-api.md)
            * [Validieren von vorlagenbasierten Kundenfeldern](./destination-sdk/file-based-render-template-api.md)
   * Handbücher {#guides}
      * [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](./destination-sdk/configure-destination-instructions.md)
      * [(Beta) Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](./destination-sdk/configure-file-based-destination-instructions.md)
      * [Übermitteln eines im Destination SDK erstellten Ziels zur Überprüfung](./destination-sdk/submit-destination.md)
   * Referenz {#reference}
      * [Ratenbegrenzungs- und Wiederholungsrichtlinie für Streaming-Ziele](./destination-sdk/rate-limiting-retry-policy.md)
      * [Unterstützte Umwandlungsfunktionen](./destination-sdk/supported-functions.md)
   * Dokumentieren des Ziels {#document-destination}
      * [Dokumentieren des Ziels in Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Verwenden der GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Verwenden eines Texteditors in der lokalen Umgebung, um eine Zieldokumentationsseite zu erstellen](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Dokumentationsvorlage für Self-Service](./destination-sdk/docs-framework/self-service-template.md)
      * [Best Practices für die Inhaltserstellung](./destination-sdk/docs-framework/authoring-best-practices.md)
* [Häufig gestellte Fragen](./destinations-faq.md)
* [Platform – Versionshinweise](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=de)
