---
audience: user
user-guide-title: Zielhandbuch
user-guide-description: Aktivieren Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle.
description: Dieses Dokument listet das Inhaltsverzeichnis für Adobe Experience Platform-Ziele auf
feature: Destinations
role: Admin,User
source-git-commit: bef5176048bad269c9e32e56d1e331a93eb80e13
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Ziele {#destinations}

* [Ziele – Übersicht](./home.md)
* [Zieltypen und Kategorien](./destination-types.md)
* [Leitplanken für Ziele (Aktivierung)](./guardrails.md)
* Funktionsweise von Zielen {#how-destinations-work}
   * [Konfigurierbare und allgemeine Exporteinstellungen in Zielen](./how-destinations-work/destinations-configurations.md)
   * [Profilexportverhalten für verschiedene Zieltypen](./how-destinations-work/profile-export-behavior.md)
   * [Umgang mit Identitäten im Aktivierungs-Workflow für Ziele](./how-destinations-work/identity-handling.md)
* API-Tutorials {#api}
   * [Aktivieren von Daten für dateibasierte Ziele mithilfe der Flow Service-API](/help/destinations/api/activate-segments-file-based-destinations.md)
   * [Verbinden Sie sich mit Streaming-Zielen und aktivieren Sie Daten über die Flow Service-API](./api/streaming-destinations.md)
   * [Verbinden mit dateibasierten E-Mail-Marketing-Zielen und Aktivieren von Daten mithilfe der Flow Service-API](./api/connect-activate-batch-destinations.md)
   * [Aktivieren von Zielgruppen für Batch-Ziele über die Ad-hoc-Aktivierungs-API](./api/ad-hoc-activation-api.md)
   * [Bearbeiten des Ziels](./api/edit-destination.md)
   * [Aktualisieren von Ziel-Datenflüssen](./api/update-destination-dataflows.md)
   * [Löschen von Zielkonten](./api/delete-destination-account.md)
   * [Zieldatenflüsse löschen](./api/delete-destination-dataflow.md)
   * [Datensätze exportieren](/help/destinations/api/export-datasets.md)
   * [Sortieren und Filtern von API-Antworten für Ziele](https://experienceleague.adobe.com/docs/experience-platform/dataflows/api/sort-and-filter.html?lang=de#use-cases)
* Handbücher zur Benutzeroberfläche {#ui}
   * [Arbeitsbereich „Ziele“](./ui/destinations-workspace.md)
   * [Erstellen einer neuen Zielverbindung](./ui/connect-destination.md)
   * Aktivieren von Daten für Ziele{#activate}
      * [Aktivierungsübersicht](./ui/activation-overview.md)
      * [Aktivieren von Zielgruppen für Streaming-Zielgruppenexport-Ziele](./ui/activate-segment-streaming-destinations.md)
      * [Aktivieren von Zielgruppen für Exportziele von Streaming-Profilen](./ui/activate-streaming-profile-destinations.md)
      * [Aktivieren von Zielgruppen für Batch-Profil-Exportziele](./ui/activate-batch-profile-destinations.md)
      * [Aktivieren von Zielgruppen für Edge-Personalisierungsziele](./ui/activate-edge-personalization-destinations.md)
      * [Profilattribute am Edge in Echtzeit nachschlagen](./ui/activate-edge-profile-lookup.md)
      * [Aktivieren von Zielgruppen für kuratierte Ziele basierend auf LiveRamp-Kennungen](./ui/activate-curated-destinations.md)
      * [Aktivieren von potenziellen Zielgruppen für Ziele](./ui/activate-prospect-audiences.md)
      * [Kontozielgruppen für Ziele aktivieren](./ui/activate-account-audiences.md)
      * [Exportieren von Dateien nach Bedarf an Batch-Ziele mithilfe der Experience Platform-Benutzeroberfläche](./ui/export-file-now.md)
      * [Exportieren von Datensätzen mithilfe der Experience Platform-Benutzeroberfläche](./ui/export-datasets.md)
      * [(Beta) Verwenden Sie das XDM-Attribut der letzten Qualifikationszeit in den neuen Beta-Cloud-Speicherzielen](./ui/activate-last-qualification-time.md)
      * [Exportieren von Arrays, Zuordnungen und Objekten](/help/destinations/ui/export-arrays-maps-objects.md)
      * [Durchführen von Umwandlungen an Daten, die in Cloud-Speicher-Ziele exportiert wurden](/help/destinations/ui/data-transformations-calculated-fields.md)
   * [Anzeigen von Zieldetails](./ui/destination-details-page.md)
   * [(Beta) Bearbeiten von Zielen](./ui/edit-destination.md)
   * [Aktualisieren von Zielkonten](./ui/update-accounts.md)
   * [Löschen von Zielkonten](./ui/delete-destination-account.md)
   * [Bearbeiten von Aktivierungsdatenflüssen](./ui/edit-activation.md)
   * [Löschen von Zielen](./ui/delete-destinations.md)
   * [Überwachen von Datenflüssen](./ui/monitor-dataflows.md)
   * [Konfigurieren von Dateiformatierungsoptionen für dateibasierte Ziele](./ui/batch-destinations-file-formatting-options.md)
   * [Abonnieren von kontextbezogenen Zielwarnhinweisen](ui/alerts.md)
* Zielkatalog {#catalog}
   * [Zielkatalog – Übersicht](./catalog/overview.md)
   * Adobe-Ziele{#adobe}
      * [Adobe-Ziele – Übersicht](./catalog/adobe/overview.md)
      * [Experience Cloud-Zielgruppen](/help/destinations/catalog/adobe/experience-cloud-audiences.md)
      * [Marketo Engage-Verbindung](./catalog/adobe/marketo-engage.md)
      * [(Beta) Marketo Engage Person Sync-Verbindung](./catalog/adobe/marketo-engage-person-sync.md)
      * [Marketo Measure Ultimate-Verbindung](./catalog/adobe/marketo-measure-ultimate.md)
      * [Zielgruppenfreigabe in Experience Platform](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de)
      * [Verbindung mit Federated Audience Composition](https://www.adobe.com/go/destinations-federated-audience-composition)
   * Werbeziele{#advertising}
      * [(Beta) Acxiom-Zielgruppenverteilung](./catalog/advertising/acxiom-audience-distribution.md)
      * [Werbeziele – Übersicht](./catalog/advertising/overview.md)
      * [Adobe Advertising Cloud-Verbindung](./catalog/advertising/adobe-advertising-cloud-connection.md)
      * [Adobe Advertising Cloud-Erweiterung](./catalog/advertising/adobe-advertising-cloud.md)
      * [Amazon Ads-Verbindung](./catalog/advertising/amazon-ads.md)
      * [Awin Advertising Conversion Tag-Erweiterung](./catalog/advertising/awin-conversiontag.md)
      * [Awin Advertiser Mastertag-Erweiterung](./catalog/advertising/awin-mastertag.md)
      * [Erweiterung für Bing Ads Universal Event Tracking (UET)](./catalog/advertising/bing-ads.md)
      * [Bombora-Verbindung](./catalog/advertising/bombora.md)
      * [Branch-Erweiterung](./catalog/advertising/branch.md)
      * [Criteo-Verbindung](./catalog/advertising/criteo.md)
      * [Demandbase-Verbindung](./catalog/advertising/demandbase.md)
      * [Demandbase People-Verbindung](./catalog/advertising/demandbase-people.md)
      * [DoubleClick Floodlight (Beta)-Erweiterung](./catalog/advertising/doubleclick-floodlight.md)
      * [Facebook-Pixel-Erweiterung](./catalog/advertising/facebook-pixel.md)
      * [Flashspeak OneTag-Erweiterung](./catalog/advertising/flashtalking.md)
      * [Google Ads-Verbindung](./catalog/advertising/google-ads-destination.md)
      * [Google Ads-Erweiterung](./catalog/advertising/google-ads-extension.md)
      * [Google Ad Manager-Verbindung](./catalog/advertising/google-ad-manager.md)
      * [(Beta) Google Ad Manager 360-Verbindung](./catalog/advertising/google-ad-manager-360-connection.md)
      * [Google Customer Match-Verbindung](./catalog/advertising/google-customer-match.md)
      * [(Eingeschränkte Verfügbarkeit) Google Customer Match + DV360-Verbindung](./catalog/advertising/google-customer-match-dv360.md)
      * [Google Display &amp; Video 360-Verbindung](./catalog/advertising/google-dv360.md)
      * [Google gtag-Erweiterung](./catalog/advertising/gtag-advertising.md)
      * [LinkedIn Insight Tag-Erweiterung](./catalog/advertising/linkedin.md)
      * [LiveRamp – Onboarding-Verbindung](./catalog/advertising/liveramp-onboarding.md)
      * [LiveRamp - Verteilungsverbindung](./catalog/advertising/liveramp-distribution.md)
      * [Magnitrat](/help/destinations/catalog/advertising/magnite-batch.md)
      * [Magnite Streaming Echtzeit-Verbindung](/help/destinations/catalog/advertising/magnite-streaming.md)
      * [Microsoft Bing-Verbindung](./catalog/advertising/bing.md)
      * [Pinterest Conversion Tracking-Erweiterung](./catalog/advertising/pinterest-extension.md)
      * [Pinterest Customer List-Verbindung](./catalog/advertising/pinterest.md)
      * [Pinterest-Verbindungs-Upgrade](./catalog/advertising/pinterest-upgrade.md)
      * [PubMatic Connect-Verbindung](./catalog/advertising/pubmatic.md)
      * [Snapchat Ads-Verbindung](./catalog/advertising/snap-inc.md)
      * [Verbindung mit The Trade Desk](./catalog/advertising/tradedesk.md)
      * [The Trade Desk CRM-Verbindung](./catalog/advertising/tradedesk-emails.md)
      * [Twitter Universal Website Tag-Erweiterung](./catalog/advertising/twitter-uwt.md)
      * [Yahoo/Verizon DataX-Verbindung](./catalog/advertising/datax.md)
   * Analytics-Ziele {#analytics}
      * [Analyseziele – Übersicht](./catalog/analytics/overview.md)
      * [Adform Website Tracking-Erweiterung](./catalog/analytics/adform.md)
      * [Adobe Analytics-Erweiterung](./catalog/analytics/adobe-analytics.md)
      * [Adobe Media Analytics für Audio und Video-Erweiterung](./catalog/analytics/adobe-video-analytics.md)
      * [Clicktale-Erweiterung](./catalog/analytics/clicktale.md)
      * [Contentsquare-Erweiterung](./catalog/analytics/contentsquare.md)
      * [Decibel-Erweiterung](./catalog/analytics/decibel.md)
      * [Demandbase-Erweiterung](./catalog/analytics/demandbase.md)
      * [DialogTech-Erweiterung](./catalog/analytics/dialogtech.md)
      * [Gainsight PX-Verbindung](./catalog/analytics/gainsight-px.md)
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
      * [Übersicht über die Cloud-Speicher-Ziele](./catalog/cloud-storage/overview.md)
      * [Amazon Kinesis-Verbindung](./catalog/cloud-storage/amazon-kinesis.md)
      * [Amazon S3-Verbindung](./catalog/cloud-storage/amazon-s3.md)
      * [Azure Blob-Verbindung](./catalog/cloud-storage/azure-blob.md)
      * [Azure Data Lake Storage Gen2](./catalog/cloud-storage/adls-gen2.md)
      * [Azure Event Hubs-Verbindung](./catalog/cloud-storage/azure-event-hubs.md)
      * [Data Landing Zone](./catalog/cloud-storage/data-landing-zone.md)
      * [Google Cloud Storage](./catalog/cloud-storage/google-cloud-storage.md)
      * [SFTP-Verbindung](./catalog/cloud-storage/sftp.md)
      * [Snowflake-Verbindung](./catalog/cloud-storage/snowflake.md)
      * [AUF DIE ZULASSUNGSLISTE SETZEN IP-Adresse für dateibasierte Cloud-Speicher-Ziele](./catalog/cloud-storage/ip-address-allow-list.md)
   * CRM-Ziele (Customer Relationship Management) {#crm}
      * [Hubspot-Verbindung](./catalog/crm/hubspot.md)
      * [Salesforce-CRM-Verbindung](./catalog/crm/salesforce.md)
      * [Verbindung mit Microsoft Dynamics 365](./catalog/crm/microsoft-dynamics-365.md)
      * [Outreach-Verbindung](catalog/crm/outreach.md)
      * [Zendesk-Verbindung](catalog/crm/zendesk.md)
   * Data Management Platform-Ziele {#data-management}
      * [Data Management Platform (DMP)-Ziele – Übersicht](./catalog/data-management/overview.md)
      * [Audience Manager DIL-Erweiterung](./catalog/data-management/aam-dil-extension.md)
      * [Zeta-Marketing-Plattform](/help/destinations/catalog/data-management/zeta-marketing-platform.md)
   * Daten- und Identitätspartner {#data-partner}
      * [Unterdrückung potenzieller Acxiom-Kunden](./catalog/data-partner/acxiom-prospect-suppression.md)
      * [Acxiom Data Enhancement](./catalog/data-partner/acxiom-data-enhancement.md)
      * [Merkury Enterprise Connections](/help/destinations/catalog/data-partners/merkury-enterprise-connections.md)
      * [Merkury Enterprise Identity](/help/destinations/catalog/data-partners/merkury-enterprise-identity.md)
   * E-Commerce-Ziele {#ecommerce}
      * [SAP Commerce](./catalog/ecommerce/sap-commerce.md)
   * E-Mail-Ziele {#email}
      * [Bizible-Erweiterung](./catalog/email/bizible.md)
      * [Marketo-Erweiterung](./catalog/email/marketo.md)
      * [Marketo Munchkin-Erweiterung](./catalog/email/marketo-munchkin.md)
      * [PebblePost-Erweiterung](./catalog/email/pebblepost.md)
   * E-Mail-Marketing-Ziele  {#email-marketing}
      * [E-Mail-Marketing-Ziele – Übersicht](./catalog/email-marketing/overview.md)
      * [Adobe Campaign-Verbindung](./catalog/email-marketing/adobe-campaign.md)
      * [Adobe Campaign Managed Cloud Services-Verbindung](./catalog/email-marketing/adobe-campaign-managed-services.md)
      * [Mailchimp-Interessenkategorien](./catalog/email-marketing/mailchimp-interest-categories.md)
      * [Mailchimp-Tags](./catalog/email-marketing/mailchimp-tags.md)
      * [(API) Oracle Eloqua-Verbindung](./catalog/email-marketing/oracle-eloqua-api.md)
      * [(Dateien) Oracle Eloqua-Verbindung](./catalog/email-marketing/oracle-eloqua.md)
      * [Oracle Responsys-Verbindung](./catalog/email-marketing/oracle-responsys.md)
      * [(API) Salesforce Marketing Cloud-Verbindung](./catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)
      * [(Dateien) Salesforce Marketing Cloud-Verbindung](./catalog/email-marketing/salesforce-marketing-cloud.md)
      * [[!DNL Salesforce Marketing Cloud Account Engagement]](./catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
      * [SendGrid-Verbindung](./catalog/email-marketing/sendgrid.md)
   * Tag-Erweiterungen {#launch-extensions}
      * [Übersicht über Tag-Erweiterungen](./catalog/launch-extensions/overview.md)
   * Marketing-Automatisierung {#marketing-automation}
      * [RainFocus-Teilnehmerprofile](/help/destinations/catalog/marketing-automation/rainfocus.md)
   * Ziele für mobile Interaktion {#mobile-engagement}
      * [Ziele für mobile Interaktion – Übersicht](./catalog/mobile-engagement/overview.md)
      * [Airship Attributes-Verbindung](./catalog/mobile-engagement/airship-attributes.md)
      * [Airship Tags-Verbindung](./catalog/mobile-engagement/airship-tags.md)
      * [Braze-Verbindung](./catalog/mobile-engagement/braze.md)
      * [Line-Verbindung](./catalog/mobile-engagement/line.md)
      * [Moengage-Verbindung](./catalog/mobile-engagement/moengage.md)
   * Personalisierungsziele {#personalization}
      * [Personalisierungsziele – Übersicht](./catalog/personalization/overview.md)
      * [(Eingeschränkte Verfügbarkeit) Zielgruppenanalyse](./catalog/personalization/audience-analysis.md)
      * [Adobe Commerce-Verbindung](./catalog/personalization/adobe-commerce.md)
      * [Adobe Target-Verbindung](./catalog/personalization/adobe-target-connection.md)
      * [Adobe Target-Erweiterung](./catalog/personalization/adobe-target.md)
      * [Adobe Target v2-Erweiterung](./catalog/personalization/adobe-target-v2.md)
      * [Algolia-Verbindung](./catalog/personalization/algolia.md)
      * [Beemray-Erweiterung](./catalog/personalization/beemray.md)
      * [Benutzerdefinierte Personalisierungsverbindung](./catalog/personalization/custom-personalization.md)
      * [D&amp;B Visitor Intelligence-Erweiterung](./catalog/personalization/dnb.md)
      * [Experience Cloud-ID-Service-Erweiterung](./catalog/personalization/adobe-ecid.md)
      * [Gainsight-Erweiterung](./catalog/personalization/gainsight.md)
      * [KickFire-Erweiterung](./catalog/personalization/kickfire.md)
      * [Marketo Web-Personalisierungserweiterung](./catalog/personalization/marketo-web-personalization.md)
      * [Pega CDH RealTime Audience-Verbindung](./catalog/personalization/pega.md)
      * [(V2) Pega CDH RealTime Audience-Verbindung](./catalog/personalization/pega-v2.md)
      * [Pega-Profilverbindung](./catalog/personalization/pega-profile.md)
   * Social-Media-Ziele{#social}
      * [Social-Media-Ziele – Übersicht](./catalog/social/overview.md)
      * [Facebook-Verbindung](./catalog/social/facebook.md)
      * [(Firmen) Verbindung mit LinkedIn Matched Audiences](./catalog/social/linkedin-b2b.md)
      * [Verbindung für zugeordnete LinkedIn-Zielgruppen](./catalog/social/linkedin.md)
      * [TikTok-Verbindung](./catalog/social/tiktok.md)
      * [[!DNL Twitter Custom Audiences]-Verbindung](./catalog/social/twitter.md)
   * Streaming-Ziele {#streaming}
      * [HTTP-API-Verbindung](./catalog/streaming/http-destination.md)
      * [IP-Adressen-Zulassungsliste für Streaming-Ziele](./catalog/streaming/ip-address-allow-list.md)
   * Umfrageziele {#survey}
      * [Umfrageziele – Übersicht](./catalog/survey/overview.md)
      * [Ziel von Qualtrics Automations](./catalog/survey/qualtrics-automations.md)
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
   * [Erste Schritte mit dem Destination SDK](./destination-sdk/getting-started.md)
   * [Glossar](/help/destinations/destination-sdk/glossary.md)
   * Funktionalität {#functionality}
      * [Konfigurationsoptionen](./destination-sdk/functionality/configuration-options.md)
      * Ziel-Server-Komponenten {#destination-server}
         * [Server-Spezifikationen](./destination-sdk/functionality/destination-server/server-specs.md)
         * [Vorlagenspezifikationen](./destination-sdk/functionality/destination-server/templating-specs.md)
         * [Nachrichtenformat](./destination-sdk/functionality/destination-server/message-format.md)
         * [Unterstützte Transformationsfunktionen](./destination-sdk/functionality/destination-server/supported-functions.md)
         * [Konfiguration der Dateiformatierung](./destination-sdk/functionality/destination-server/file-formatting.md)
      * Zielkonfigurationskomponenten {#destination-configuration}
         * [Zielgruppen-Datentyp konfigurieren](./destination-sdk/functionality/destination-configuration/audience-data-type.md)
         * [Konfiguration der Kundenauthentifizierung](./destination-sdk/functionality/destination-configuration/customer-authentication.md)
         * [OAuth2-Autorisierung](./destination-sdk/functionality/destination-configuration/oauth2-authorization.md)
         * [Benutzerdefinierte Datenfelder](./destination-sdk/functionality/destination-configuration/customer-data-fields.md)
         * [Benutzeroberflächenattribute](./destination-sdk/functionality/destination-configuration/ui-attributes.md)
         * [Konfiguration des Partnerschemas](./destination-sdk/functionality/destination-configuration/schema-configuration.md)
         * [Konfiguration von Identity-Namespaces](./destination-sdk/functionality/destination-configuration/identity-namespace-configuration.md)
         * [Unterstützte Zuordnungskonfigurationen](./destination-sdk/functionality/destination-configuration/supported-mapping-configurations.md)
         * [Zielbereitstellung](./destination-sdk/functionality/destination-configuration/destination-delivery.md)
         * [Konfiguration von Zielgruppen-Metadaten](./destination-sdk/functionality/destination-configuration/audience-metadata-configuration.md)
         * [Aggregationsrichtlinie](./destination-sdk/functionality/destination-configuration/aggregation-policy.md)
         * [Batch-Konfiguration](./destination-sdk/functionality/destination-configuration/batch-configuration.md)
         * [Historische Profilqualifikationen](./destination-sdk/functionality/destination-configuration/historical-profile-qualifications.md)
      * [Ratenbegrenzungs- und Wiederholungsrichtlinie für Streaming-Ziele](./destination-sdk/functionality/rate-limiting-retry-policy.md)
      * [Verwaltung von Zielgruppen-Metadaten](./destination-sdk/functionality/audience-metadata-management.md)
   * Handbücher {#guides}
      * [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](./destination-sdk/guides/configure-destination-instructions.md)
      * [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](./destination-sdk/guides/configure-file-based-destination-instructions.md)
      * [Übermitteln eines im Destination SDK erstellten Ziels zur Überprüfung](./destination-sdk/guides/submit-destination.md)
      * Konfigurieren von dateibasierten Zielen {#configure-file-based-destinations}
         * [Konfigurieren von Dateiformatierungsoptionen](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)
         * [Konfigurieren eines Amazon S3-Ziels mit vordefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration](../destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md)
         * [Konfigurieren eines Amazon S3-Ziels mit benutzerdefinierten Dateinamen- und Formatierungsoptionen](../destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-custom-file-formatting.md)
         * [Konfigurieren eines Azure Blob Storage-Ziels mit benutzerdefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration](../destinations/destination-sdk/guides/batch/configure-blob-destination-with-custom-file-formatting.md)
         * [Konfigurieren eines Azure Data Lake Storage-Ziels mit benutzerdefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration](../destinations/destination-sdk/guides/batch/configure-adls-destination-with-custom-file-formatting.md)
         * [Konfigurieren eines Data Landing Zone-Ziels (DLZ) mit benutzerdefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration](../destinations/destination-sdk/guides/batch/configure-dlz-destination-with-custom-file-formatting.md)
         * [Konfigurieren eines SFTP-Ziels mit vordefinierten Dateiformatierungsoptionen und benutzerdefinierter Dateinamenkonfiguration](../destinations/destination-sdk/guides/batch/configure-sftp-destination-with-predefined-file-formatting.md)
         * [Konfigurieren eines dateibasierten Ziels zum Exportieren von potenziellen Zielgruppen](/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md)
   * API-Referenz zur Zielerstellung {#authoring-api}
      * [API-Referenz zum Destination SDK (Destination Authoring)](https://www.adobe.io/experience-platform-apis/references/destination-authoring/)
      * Vorgänge des Ziel-Servers {#server-operations}
         * [Erstellen einer Ziel-Server-Konfiguration](./destination-sdk/authoring-api/destination-server/create-destination-server.md)
         * [Abrufen einer Ziel-Server-Konfiguration](./destination-sdk/authoring-api/destination-server/retrieve-destination-server.md)
         * [Aktualisieren einer Ziel-Server-Konfiguration](./destination-sdk/authoring-api/destination-server/update-destination-server.md)
         * [Löschen einer Ziel-Server-Konfiguration](./destination-sdk/authoring-api/destination-server/delete-destination-server.md)
      * Vorgänge der Zielkonfiguration {#destination-operations}
         * [Erstellen einer Zielkonfiguration](./destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md)
         * [Abrufen einer Zielkonfiguration](./destination-sdk/authoring-api/destination-configuration/retrieve-destination-configuration.md)
         * [Aktualisieren einer Zielkonfiguration](./destination-sdk/authoring-api/destination-configuration/update-destination-configuration.md)
         * [Löschen einer Zielkonfiguration](./destination-sdk/authoring-api/destination-configuration/delete-destination-configuration.md)
   * API-Referenz für Zielgruppen-Metadaten {#audience-template-api}
      * [Erstellen einer Zielgruppenvorlage](./destination-sdk/metadata-api/create-audience-template.md)
      * [Abrufen einer Zielgruppenvorlage](./destination-sdk/metadata-api/retrieve-audience-template.md)
      * [Aktualisieren einer Zielgruppenvorlage](./destination-sdk/metadata-api/update-audience-template.md)
      * [Löschen einer Zielgruppenvorlage](./destination-sdk/metadata-api/delete-audience-template.md)
   * API-Referenz für Berechtigungskonfigurationen {#credentials-api}
      * [Erstellen einer Anmeldedaten-Konfiguration](./destination-sdk/credentials-api/create-credential-configuration.md)
      * [Abrufen einer Anmeldedaten-Konfiguration](./destination-sdk/credentials-api/retrieve-credential-configuration.md)
      * [Aktualisieren einer Anmeldedaten-Konfiguration](./destination-sdk/credentials-api/update-credential-configuration.md)
      * [Löschen einer Anmeldedaten-Konfiguration](./destination-sdk/credentials-api/delete-credential-configuration.md)
   * API-Referenz für Zieltests {#testing-api}
      * Streaming-Zieltest-API {#streaming-destinations}
         * [Streaming-Zieltest-API – Überblick](./destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md)
         * [Generieren von Beispielprofilen basierend auf einem Quellschema](./destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md)
         * [Erstellen einer Beispiel-Nachrichtenumwandlungsvorlage](./destination-sdk/testing-api/streaming-destinations/sample-template-api.md)
         * [Validieren der exportierten Profilstruktur](./destination-sdk/testing-api/streaming-destinations/render-template-api.md)
         * [Testen Ihres Streaming-Ziels mit Beispielprofilen](./destination-sdk/testing-api/streaming-destinations/destination-testing-api.md)
         * [Erstellen und Testen einer Nachrichtenumwandlungsvorlage](./destination-sdk/testing-api/streaming-destinations/create-template.md)
      * Dateibasierte Zieltest-API {#batch-destinations}
         * [Übersicht über die dateibasierte Zieltest-API](./destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)
         * [Generieren von Beispielprofilen basierend auf einem Quellschema](./destination-sdk/testing-api/batch-destinations/file-based-sample-profile-generation-api.md)
         * [Testen Ihres dateibasierten Ziels mit Beispielprofilen](./destination-sdk/testing-api/batch-destinations/file-based-destination-testing-api.md)
         * [Anzeigen detaillierter Aktivierungsergebnisse](./destination-sdk/testing-api/batch-destinations/file-based-destination-results-api.md)
         * [Überprüfen von vorlagenbasierten Kundenfeldern](./destination-sdk/testing-api/batch-destinations/file-based-render-template-api.md)
   * API-Referenz zur Zielveröffentlichung {#publishing-api}
      * [Erstellen einer Zielveröffentlichungsanfrage](./destination-sdk/publishing-api/create-publishing-request.md)
      * [Abrufen einer Zielveröffentlichungsanfrage](./destination-sdk/publishing-api/retrieve-publishing-request.md)
   * Dokumentieren des Ziels {#document-destination}
      * [Dokumentieren des Ziels in Adobe Experience Platform](./destination-sdk/docs-framework/documentation-instructions.md)
      * [Verwenden der GitHub-Web-Oberfläche, um eine Zieldokumentationsseite zu erstellen](./destination-sdk/docs-framework/use-github-interface-to-create-documentation.md)
      * [Verwenden eines Texteditors in der lokalen Umgebung, um eine Zieldokumentationsseite zu erstellen](./destination-sdk/docs-framework/work-in-local-environment.md)
      * [Dokumentationsvorlage für Self-Service](./destination-sdk/docs-framework/self-service-template.md)
      * [Best Practices für die Inhaltserstellung](./destination-sdk/docs-framework/authoring-best-practices.md)
* [Häufig gestellte Fragen](./destinations-faq.md)
* [Versionshinweise zu Experience Platform](https://experienceleague.adobe.com/de/docs/experience-platform/release-notes/latest)
