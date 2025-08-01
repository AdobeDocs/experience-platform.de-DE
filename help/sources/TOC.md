---
audience: user
user-guide-title: Hilfe zu Adobe Experience Platform-Quell-Connectoren
breadcrumb-title: Anleitung zu Quell-Connectoren
user-guide-description: Nehmen Sie Daten aus verschiedenen Quellen auf. Erfahren Sie, wie Sie bereits aufgenommene Daten strukturieren, kennzeichnen und erweitern können.
feature: Sources
role: Developer
source-git-commit: 8ba51f144e3120637d8c6027be85b1b4e6e5d613
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 91%

---


# Quellen {#sources}

- [Quellen – Übersicht](home.md)
- Verfügbare Quell-Connectoren {#connectors}
   - Adobe-Anwendungen {#adobe-applications}
      - [Analytics-Klassifizierungsquelle](connectors/adobe-applications/classifications.md)
      - [Analytics-Quelle](connectors/adobe-applications/analytics.md)
      - [Audience Manager-Quelle](connectors/adobe-applications/audience-manager.md)
      - [Adobe Campaign Managed Cloud Services-Quelle](connectors/adobe-applications/campaign.md)
      - [Adobe Commerce-Quelle](connectors/adobe-applications/commerce.md)
      - [Quelle für Kundenattribute](connectors/adobe-applications/customer-attributes.md)
      - [Datenerfassungsquelle](connectors/adobe-applications/data-collection.md)
      - Feldzuordnungen {#mapping}
         - [Analytics-Feldzuordnungen](connectors/adobe-applications/mapping/analytics.md)
         - [Audience Manager-Feldzuordnungen](connectors/adobe-applications/mapping/audience-manager.md)
         - [Marketo Engage-Feldzuordnungen](connectors/adobe-applications/mapping/marketo.md)
         - [Microsoft Dynamics-Feldzuordnungen](connectors/adobe-applications/mapping/dynamics.md)
         - [Salesforce-Feldzuordnungen](connectors/adobe-applications/mapping/salesforce.md)
      - Marketo {#marketo}
         - [Marketo Engage-Connector](connectors/adobe-applications/marketo/marketo.md)
         - [Handbuch zur Marketo Engage-Authentifizierung](connectors/adobe-applications/marketo/marketo-auth.md)
         - [B2B-Namespaces und -Schemata](connectors/adobe-applications/marketo/marketo-namespaces.md)
         - [Migrationshandbuch für die ECID-Zuordnung](connectors/adobe-applications/marketo/migration.md)
   - Werbung {#advertising}
      - [Google Ads-Connector](connectors/advertising/ads.md)
      - [Pinterest Ads](connectors/advertising/pinterest-ads.md)
   - Analytics {#analytics}
      - [Mixpanel-Connector](connectors/analytics/mixpanel.md)
      - [Pendo](connectors/analytics/pendo-webhook.md)
      - [RainFocus](connectors/analytics/rainfocus.md)
   - Cloud-Speicherplatz {#cloud-storage}
      - [Amazon Kinesis-Connector](connectors/cloud-storage/kinesis.md)
      - [Amazon S3-Connector](connectors/cloud-storage/s3.md)
      - [Apache HDFS-Connector](connectors/cloud-storage/hdfs.md)
      - [Azure Data Lake Storage Gen2-Connector](connectors/cloud-storage/adls-gen2.md)
      - [Azure-Blob-Connector](connectors/cloud-storage/blob.md)
      - [Azure Event Hubs-Connector](connectors/cloud-storage/eventhub.md)
      - [Azure File Storage-Connector](connectors/cloud-storage/azure-file-storage.md)
      - [Data Landing Zone](connectors/cloud-storage/data-landing-zone.md)
      - [FTP-Connector](connectors/cloud-storage/ftp.md)
      - [Google Cloud Storage-Connector](connectors/cloud-storage/google-cloud-storage.md)
      - [Google PubSub](connectors/cloud-storage/google-pubsub.md)
      - [Oracle Object Storage](connectors/cloud-storage/oracle-object-storage.md)
      - [SFTP-Connector](connectors/cloud-storage/sftp.md)
      - [Amazon S3- und Azure Blob-Connector](connectors/cloud-storage/blob-s3.md)
   - Consent &amp; Preferences {#consent}
      - [Didomi](connectors/consent-and-preferences/didomi.md)
      - [OneTrust-Integration](connectors/consent-and-preferences/onetrust.md)
   - CRM {#crm}
      - [Microsoft Dynamics-Connector](connectors/crm/ms-dynamics.md)
      - [Salesforce-Connector](connectors/crm/salesforce.md)
      - [SugarCRM-Connector](connectors/crm/sugarcrm.md)
      - [Veva CRM-Connector](connectors/crm/veeva.md)
   - Customer Success {#customer-success}
      - [Salesforce Service Cloud-Connector](connectors/customer-success/salesforce-service-cloud.md)
      - [ServiceNow-Connector](connectors/customer-success/servicenow.md)
      - [Zendesk-Connector](connectors/customer-success/zendesk.md)
   - Datenbanken {#databases}
      - [Amazon Redshift-Connector](connectors/databases/redshift.md)
      - [Apache Hive on Azure HDInsights-Connector](connectors/databases/hive.md)
      - [Apache Spark on Azure HDInsights-Connector](connectors/databases/spark.md)
      - [Azure Databricks-Connector](connectors/databases/databricks.md)
      - [Azure Data Explorer-Connector](connectors/databases/data-explorer.md)
      - [Azure Synapse Analytics-Connector](connectors/databases/synapse-analytics.md)
      - [Azure Table Storage-Connector](connectors/databases/ats.md)
      - [Google BigQuery-Connector](connectors/databases/bigquery.md)
      - [GreenPlum-Connector](connectors/databases/greenplum.md)
      - [HP Vertica-Connector](connectors/databases/hp-vertica.md)
      - [IBM DB2-Connector](connectors/databases/ibm-db2.md)
      - [MariaDB-Connector](connectors/databases/mariadb.md)
      - [Microsoft SQL Server-Connector](connectors/databases/sql-server.md)
      - [MySQL-Connector](connectors/databases/mysql.md)
      - [Oracle-Connector](connectors/databases/oracle.md)
      - [PostgreSQL-Connector](connectors/databases/postgres.md)
      - [Snowflake Streaming-Connector](connectors/databases/snowflake-streaming.md)
      - [Snowflake-Connector](connectors/databases/snowflake.md)
      - [Teradata Vantage-Connector](connectors/databases/teradata-vantage.md)
   - Daten- und Identitätspartner {#data-partner}
      - [Acxiom-Datenaufnahme](connectors/data-partners/acxiom-data-ingestion.md)
      - [Datenimport aus Acxiom Prospecting](connectors/data-partners/acxiom-prospecting-data-import.md)
      - [Algolia-Benutzerprofile](connectors/data-partners/algolia-user-profiles.md)
      - [Bombora Intent](connectors/data-partners/bombora.md)
      - [Demandbase Intent](connectors/data-partners/demandbase.md)
      - [Identitätsauflösung für Unternehmen von Merkury](connectors/data-partners/merkury.md)
   - E-Commerce {#ecommerce}
      - [SAP Commerce](connectors/ecommerce/sap-commerce.md)
      - [Shopify](connectors/ecommerce/shopify.md)
      - [Shopify Streaming](connectors/ecommerce/shopify-streaming.md)
   - Lokales System {#local-system}
      - [Connector für den Upload lokaler Dateien](connectors/local-system/local-file-upload.md)
   - Marketing-Automatisierung {#marketing-automation}
      - [Braze Currents](connectors/marketing-automation/braze.md)
      - [Chatlio](connectors/marketing-automation/chatlio-webhook.md)
      - [Customer.io](connectors/marketing-automation/customerio-webhook.md)
      - [HubSpot-Connector](connectors/marketing-automation/hubspot.md)
      - [Mailchimp-Connector](connectors/marketing-automation/mailchimp.md)
      - [Oracle Eloqua-Connector](connectors/marketing-automation/oracle-eloqua.md)
      - [Oracle NetSuite](connectors/marketing-automation/oracle-netsuite.md)
      - [PathFactory](connectors/marketing-automation/pathfactory.md)
      - [Salesforce Marketing Cloud](connectors/marketing-automation/salesforce-marketing-cloud.md)
   - Zahlungen {#payments}
      - [Square-Connector](connectors/payments/square.md)
      - [Stripe-Connector](connectors/payments/stripe.md)
   - Protokolle {#protocols}
      - [Generic OData-Connector](connectors/protocols/odata.md)
      - [Generic REST-API-Connector](connectors/protocols/generic-rest.md)
   - Streaming {#streaming}
      - [HTTP-API-Connector](connectors/streaming/http.md)
- API-Tutorials {#api-tutorials}
   - Erstellen einer Basisverbindung {#create}
      - Werbung {#advertising}
         - [Google Ads](tutorials/api/create/advertising/ads.md)
         - [Pinterest Ads](tutorials/api/create/advertising/pinterest-ads.md)
      - Analytics {#analytics}
         - [Mixpanel](tutorials/api/create/analytics/mixpanel.md)
         - [Pendo](tutorials/api/create/analytics/pendo-webhook.md)
      - Cloud-Speicherplatz {#cloud-storage}
         - [Amazon Kinesis](tutorials/api/create/cloud-storage/kinesis.md)
         - [Amazon S3](tutorials/api/create/cloud-storage/s3.md)
         - [Apache HDFS](tutorials/api/create/cloud-storage/hdfs.md)
         - [Azure Blob](tutorials/api/create/cloud-storage/blob.md)
         - [Azure Data Lake Storage Gen2](tutorials/api/create/cloud-storage/adls-gen2.md)
         - [Azure Event Hubs](tutorials/api/create/cloud-storage/eventhub.md)
         - [Azure File Storage](tutorials/api/create/cloud-storage/azure-file-storage.md)
         - [Data Landing Zone](tutorials/api/create/cloud-storage/data-landing-zone.md)
         - [FTP](tutorials/api/create/cloud-storage/ftp.md)
         - [Google Cloud Storage](tutorials/api/create/cloud-storage/google.md)
         - [Google PubSub](tutorials/api/create/cloud-storage/google-pubsub.md)
         - [Oracle Object Storage](tutorials/api/create/cloud-storage/oracle-object-storage.md)
         - [SFTP](tutorials/api/create/cloud-storage/sftp.md)
      - Consent &amp; Preferences {#consent}
         - [OneTrust-Integration](tutorials/api/create/consent-and-preferences/onetrust.md)
      - CRM {#crm}
         - [Microsoft Dynamics](tutorials/api/create/crm/ms-dynamics.md)
         - [Salesforce](tutorials/api/create/crm/salesforce.md)
         - [SugarCRM-Konten und -Kontakte](tutorials/api/create/crm/sugarcrm-accounts-contacts.md)
         - [SugarCRM-Ereignisse](tutorials/api/create/crm/sugarcrm-events.md)
         - [Veeva CRM](tutorials/api/create/crm/veeva.md)
      - Customer Success {#customer-success}
         - [Salesforce Service Cloud](tutorials/api/create/customer-success/salesforce-service-cloud.md)
         - [ServiceNow](tutorials/api/create/customer-success/servicenow.md)
         - [Zendesk](tutorials/api/create/customer-success/zendesk.md)
      - Datenbanken {#databases}
         - [Amazon Redshift](tutorials/api/create/databases/redshift.md)
         - [Apache Hive on Azure HDInsights](tutorials/api/create/databases/hive.md)
         - [Apache Spark on Azure HDInsights](tutorials/api/create/databases/spark.md)
         - [Azure Databricks](tutorials/api/create/databases/databricks.md)
         - [Azure Data Explorer](tutorials/api/create/databases/data-explorer.md)
         - [Azure Synapse Analytics](tutorials/api/create/databases/synapse-analytics.md)
         - [Azure Table Storage](tutorials/api/create/databases/ats.md)
         - [Google BigQuery](tutorials/api/create/databases/bigquery.md)
         - [GreenPlum](tutorials/api/create/databases/greenplum.md)
         - [HP Vertica](tutorials/api/create/databases/hp-vertica.md)
         - [IBM DB2](tutorials/api/create/databases/ibm-db2.md)
         - [MariaDB](tutorials/api/create/databases/mariadb.md)
         - [MySQL](tutorials/api/create/databases/mysql.md)
         - [Oracle](tutorials/api/create/databases/oracle.md)
         - [PostgreSQL](tutorials/api/create/databases/postgres.md)
         - [Snowflake-Streaming](tutorials/api/create/databases/snowflake-streaming.md)
         - [Snowflake](tutorials/api/create/databases/snowflake.md)
         - [Teradata Vantage](tutorials/api/create/databases/teradata-vantage.md)
         - [SQL Server](tutorials/api/create/databases/sql-server.md)
      - E-Commerce {#ecommerce}
         - [SAP Commerce](tutorials/api/create/ecommerce/sap-commerce.md)
         - [Shopify](tutorials/api/create/ecommerce/shopify.md)
         - [Shopify Streaming](tutorials/api/create/ecommerce/shopify-streaming.md)
      - Marketing-Automatisierung {#marketing-automation}
         - [Chatlio](tutorials/api/create/marketing-automation/chatlio-webhook.md)
         - [Customer.io](tutorials/api/create/marketing-automation/customerio-webhook.md)
         - [HubSpot](tutorials/api/create/marketing-automation/hubspot.md)
         - [MailChimp-Kampagne](tutorials/api/create/marketing-automation/mailchimp-campaign.md)
         - [MailChimp-Mitglieder](tutorials/api/create/marketing-automation/mailchimp-members.md)
         - [Oracle Eloqua](tutorials/api/create/marketing-automation/oracle-eloqua.md)
         - [Oracle NetSuite-Aktivitäten](tutorials/api/create/marketing-automation/oracle-netsuite-activities.md)
         - [Oracle NetSuite-Entitäten](tutorials/api/create/marketing-automation/oracle-netsuite-entities.md)
         - [PathFactory](tutorials/api/create/marketing-automation/pathfactory.md)
         - [Salesforce Marketing Cloud](tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
      - Zahlungen {#payments}
         - [Square](tutorials/api/create/payments/square.md)
         - [Stripe](tutorials/api/create/payments/stripe.md)
      - Protokolle {#protocols}
         - [Generic OData](tutorials/api/create/protocols/odata.md)
         - [Generic REST-API](tutorials/api/create/protocols/generic-rest.md)
      - Streaming {#streaming}
         - [HTTP-API](tutorials/api/create/streaming/http.md)
   - Daten erkunden {#explore}
      - [Erkunden von Werbedaten](tutorials/api/explore/advertising.md)
      - [Erkunden von Cloud-Speicherdaten](tutorials/api/explore/cloud-storage.md)
      - [Erkunden von CRM-Daten](tutorials/api/explore/crm.md)
      - [Erkunden von Customer-Success-Daten](tutorials/api/explore/customer-success.md)
      - [Erkunden von Datenbankdaten](tutorials/api/explore/database-nosql.md)
      - [Erkunden von E-Commerce-Daten](tutorials/api/explore/ecommerce.md)
      - [Erkunden von Daten zur Marketing-Automatisierung](tutorials/api/explore/marketing-automation.md)
      - [Erkunden von Zahlungsdaten](tutorials/api/explore/payments.md)
      - [Erkunden von Protokolldaten](tutorials/api/explore/protocols.md)
      - [Durchsuchen von Datentabellen](tutorials/api/explore/tabular.md)
   - Erfassen von Daten {#collect}
      - [Erfassen von Werbedaten](tutorials/api/collect/advertising.md)
      - [Erfassen von Cloud-Speicherdaten](tutorials/api/collect/cloud-storage.md)
      - [Erfassen von CRM-Daten](tutorials/api/collect/crm.md)
      - [Erfassen von Customer-Success-Daten](tutorials/api/collect/customer-success.md)
      - [Erfassen von Datenbankdaten](tutorials/api/collect/database-nosql.md)
      - [Erfassen von E-Commerce-Daten](tutorials/api/collect/ecommerce.md)
      - [Erfassen von Daten zur Marketing-Automatisierung](tutorials/api/collect/marketing-automation.md)
      - [Erfassen von Zahlungsdaten](tutorials/api/collect/payments.md)
      - [Erfassen von Protokolldaten](tutorials/api/collect/protocols.md)
      - [Erfassen von Streaming-Daten](tutorials/api/collect/streaming.md)
   - [On-Demand-Aufnahme](tutorials/api/on-demand-ingestion.md)
   - [Filtern von Daten auf Quellebene](tutorials/api/filter.md)
   - [Überwachen von Datenflüssen](tutorials/api/monitor.md)
   - [Aktualisieren von Konten](tutorials/api/update.md)
   - [Aktualisieren von Datenflüssen](tutorials/api/update-dataflows.md)
   - [Wiederholen fehlgeschlagener Datenfluss-Ausführungen](tutorials/api/retry-flows.md)
   - [Löschen von Konten](tutorials/api/delete.md)
   - [Löschen von Datenflüssen](tutorials/api/delete-dataflows.md)
   - [Aufnehmen verschlüsselter Daten](tutorials/api/encrypt-data.md)
   - [Speichern eines Datenflusses als Entwurf](tutorials/api/draft.md)
   - [Anwenden von Zugriffskennzeichnungen auf einen Datenfluss](tutorials/api/labels.md)
   - [Verwenden privater Endpunkte](tutorials/api/private-link.md)
   - [Änderungsdatenerfassung aktivieren](tutorials/api/change-data-capture.md)
- Tutorials zur Benutzeroberfläche {#ui-tutorials}
   - Erstellen einer Quellverbindung {#create}
      - Adobe-Anwendungen {#adobe-applications}
         - [Adobe Analytics (Report Suite-Daten)](tutorials/ui/create/adobe-applications/analytics.md)
         - [Adobe Analytics (Klassifizierungsdaten)](tutorials/ui/create/adobe-applications/classifications.md)
         - [Adobe Audience Manager](tutorials/ui/create/adobe-applications/audience-manager.md)
         - [Adobe Campaign Managed Cloud Services](tutorials/ui/create/adobe-applications/campaign.md)
         - [Kundenattribute](tutorials/ui/create/adobe-applications/customer-attributes.md)
         - [Marketo Engage](tutorials/ui/create/adobe-applications/marketo.md)
         - [Benutzerdefinierte Marketo-Aktivitäten](tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
      - Werbung {#advertising}
         - [Google Ads](tutorials/ui/create/advertising/ads.md)
         - [Pinterest Ads](tutorials/ui/create/advertising/pinterest-ads.md)
      - Analytics {#analytics}
         - [Mixpanel](tutorials/ui/create/analytics/mixpanel.md)
         - [Pendo](tutorials/ui/create/analytics/pendo-webhook.md)
         - [RainFocus](tutorials/ui/create/analytics/rainfocus.md)
      - Cloud-Speicherplatz {#cloud-storage}
         - [Amazon Kinesis](tutorials/ui/create/cloud-storage/kinesis.md)
         - [Amazon S3](tutorials/ui/create/cloud-storage/s3.md)
         - [Apache HDFS](tutorials/ui/create/cloud-storage/hdfs.md)
         - [Azure Data Lake Storage Gen2](tutorials/ui/create/cloud-storage/adls-gen2.md)
         - [Azure Blob](tutorials/ui/create/cloud-storage/blob.md)
         - [Azure Event Hubs](tutorials/ui/create/cloud-storage/eventhub.md)
         - [Azure File Storage](tutorials/ui/create/cloud-storage/azure-file-storage.md)
         - [Data Landing Zone](tutorials/ui/create/cloud-storage/data-landing-zone.md)
         - [FTP](tutorials/ui/create/cloud-storage/ftp.md)
         - [Google Cloud Storage](tutorials/ui/create/cloud-storage/google-cloud-storage.md)
         - [Google PubSub](tutorials/ui/create/cloud-storage/google-pubsub.md)
         - [Oracle Object Storage](tutorials/ui/create/cloud-storage/oracle-object-storage.md)
         - [SFTP](tutorials/ui/create/cloud-storage/sftp.md)
         - [Amazon S3 und Blob](tutorials/ui/create/cloud-storage/blob-s3.md)
      - Consent &amp; Preferences {#consent}
         - [Didomi](tutorials/ui/create/consent-and-preferences/didomi.md)
         - [OneTrust-Integration](tutorials/ui/create/consent-and-preferences/onetrust.md)
      - CRM {#crm}
         - [Microsoft Dynamics](tutorials/ui/create/crm/dynamics.md)
         - [Salesforce](tutorials/ui/create/crm/salesforce.md)
         - [SugarCRM-Konten und -Kontakte](tutorials/ui/create/crm/sugarcrm-accounts-contacts.md)
         - [SugarCRM-Ereignisse](tutorials/ui/create/crm/sugarcrm-events.md)
         - [Veeva CRM](tutorials/ui/create/crm/veeva.md)
      - Customer Success {#customer-success}
         - [Salesforce Service Cloud](tutorials/ui/create/customer-success/salesforce-service-cloud.md)
         - [ServiceNow](tutorials/ui/create/customer-success/servicenow.md)
         - [Zendesk](tutorials/ui/create/customer-success/zendesk.md)
      - Datenbanken {#databases}
         - [Amazon Redshift](tutorials/ui/create/databases/redshift.md)
         - [Apache Hive on Azure HDInsights](tutorials/ui/create/databases/hive.md)
         - [Apache Spark on Azure HDInsights](tutorials/ui/create/databases/spark.md)
         - [Azure Databricks](tutorials/ui/create/databases/databricks.md)
         - [Azure Data Explorer](tutorials/ui/create/databases/data-explorer.md)
         - [Azure Synapse Analytics](tutorials/ui/create/databases/synapse-analytics.md)
         - [Azure Table Storage](tutorials/ui/create/databases/ats.md)
         - [Google BigQuery](tutorials/ui/create/databases/bigquery.md)
         - [GreenPlum](tutorials/ui/create/databases/greenplum.md)
         - [HP Vertica](tutorials/ui/create/databases/hp-vertica.md)
         - [IBM DB2](tutorials/ui/create/databases/ibm-db2.md)
         - [MariaDB](tutorials/ui/create/databases/mariadb.md)
         - [Microsoft SQL Server](tutorials/ui/create/databases/sql-server.md)
         - [MySQL](tutorials/ui/create/databases/mysql.md)
         - [Oracle](tutorials/ui/create/databases/oracle.md)
         - [PostgreSQL](tutorials/ui/create/databases/postgres.md)
         - [Snowflake](tutorials/ui/create/databases/snowflake.md)
         - [Snowflake-Streaming](tutorials/ui/create/databases/snowflake-streaming.md)
         - [Teradata Vantage](tutorials/ui/create/databases/teradata-vantage.md)
      - Daten- und Identitätspartner {#data-partner}
         - [Acxiom-Datenaufnahme](tutorials/ui/create/data-partners/acxiom-data-ingestion.md)
         - [Datenimport aus Acxiom Prospecting](tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md)
         - [Algolia-Benutzerprofile](tutorials/ui/create/data-partners/algolia-user-profiles.md)
         - [Bombora Intent](tutorials/ui/create/data-partners/bombora.md)
         - [Demandbase Intent](tutorials/ui/create/data-partners/demandbase.md)
         - [Identitätsauflösung für Unternehmen von Merkury](tutorials/ui/create/data-partners/merkury.md)
      - E-Commerce {#ecommerce}
         - [SAP Commerce](tutorials/ui/create/ecommerce/sap-commerce.md)
         - [Shopify](tutorials/ui/create/ecommerce/shopify.md)
         - [Shopify Streaming](tutorials/ui/create/ecommerce/shopify-streaming.md)
      - Lokales System {#local-system}
         - [Lokaler Datei-Upload](tutorials/ui/create/local-system/local-file-upload.md)
      - Marketing-Automatisierung {#marketing-automation}
         - [Braze Currents](tutorials/ui/create/marketing-automation/braze.md)
         - [Chatlio](tutorials/ui/create/marketing-automation/chatlio-webhook.md)
         - [Customer.io](tutorials/ui/create/marketing-automation/customerio-webhook.md)
         - [HubSpot](tutorials/ui/create/marketing-automation/hubspot.md)
         - [Mailchimp-Kampagnen](tutorials/ui/create/marketing-automation/mailchimp-campaigns.md)
         - [Mailchimp-Mitglieder](tutorials/ui/create/marketing-automation/mailchimp-members.md)
         - [Oracle Eloqua](tutorials/ui/create/marketing-automation/oracle-eloqua.md)
         - [Oracle NetSuite-Aktivitäten](tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md)
         - [Oracle NetSuite-Entitäten](tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md)
         - [PathFactory](tutorials/ui/create/marketing-automation/pathfactory.md)
         - [Salesforce Marketing Cloud](tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
      - Zahlungen {#payments}
         - [Square](tutorials/ui/create/payments/square.md)
         - [Stripe](tutorials/ui/create/payments/stripe.md)
      - Protokolle {#protocols}
         - [Generic OData](tutorials/ui/create/protocols/odata.md)
      - Streaming {#streaming}
         - [HTTP-API](tutorials/ui/create/streaming/http.md)
   - Datenfluss konfigurieren {#dataflow}
      - [Datenfluss der Werbeverbindung](tutorials/ui/dataflow/advertising.md)
      - [Datenfluss der Analytics-Verbindung](tutorials/ui/dataflow/analytics.md)
      - [Datenfluss der Batch-Cloud-Speicherverbindung](tutorials/ui/dataflow/batch/cloud-storage.md)
      - [Datenfluss der Streaming-Cloud-Speicher-Verbindung](tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
      - [Verbindungsdatenfluss für Einverständnis und Voreinstellungen](tutorials/ui/dataflow/consent-and-preferences.md)
      - [Datenfluss der CRM-Verbindung](tutorials/ui/dataflow/crm.md)
      - [Datenfluss der Customer-Success-Verbindung](tutorials/ui/dataflow/customer-success.md)
      - [Datenfluss der Datenbankverbindung](tutorials/ui/dataflow/databases.md)
      - [Datenfluss der E-Commerce-Verbindung](tutorials/ui/dataflow/ecommerce.md)
      - [Datenfluss für Verbindung zur Marketing-Automatisierung](tutorials/ui/dataflow/marketing-automation.md)
      - [Datenfluss der Zahlungsverbindung](tutorials/ui/dataflow/payments.md)
      - [Datenfluss der Protokollverbindung](tutorials/ui/dataflow/protocols.md)
   - [Erstellen eines Quellen-Datenflusses mithilfe von Vorlagen in der Benutzeroberfläche](tutorials/ui/templates.md)
   - [Filtern von Quellobjekten](tutorials/ui/filter.md)
   - [Aufnehmen verschlüsselter Daten](tutorials/ui/encryped-ingestion.md)
   - [On-Demand-Aufnahme](tutorials/ui/on-demand-ingestion.md)
   - [Überwachen von Batch-Datenflüssen](tutorials/ui/monitor.md)
   - [Überwachen von Streaming-Datenflüssen](tutorials/ui/monitor-streaming.md)
   - [Aktualisieren von Konten](tutorials/ui/update.md)
   - [Aktualisieren von Datenflüssen](tutorials/ui/update-dataflows.md)
   - [Löschen von Konten](tutorials/ui/delete-accounts.md)
   - [Löschen von Datenflüssen](tutorials/ui/delete.md)
   - [Abonnieren von Warnmeldungen für Quellen](tutorials/ui/alerts.md)
   - [Speichern eines Datenflusses als Entwurf](tutorials/ui/draft.md)
   - [Anwenden von Zugriffskennzeichnungen auf einen Datenfluss](tutorials/ui/labels.md)
- Selbstbedienungsquellen (Batch-SDK) {#sdk}
   - [Überblick](sources-sdk/overview.md)
   - Konfigurieren der Verbindungsspezifikation {#config}
      - [Konfigurationsoptionen](sources-sdk/config/config.md)
      - [Konfigurieren der Authentifizierungsspezifikation](sources-sdk/config/authspec.md)
      - [Konfigurieren der Quellspezifikation](sources-sdk/config/sourcespec.md)
      - [Konfigurieren der Analysespezifikation](sources-sdk/config/explorespec.md)
   - Handbuch zur API für Selbstbedienungsquellen (Batch-SDK) {#self-serve-api}
      - [Übersicht über die API für Selbstbedienungsquellen (Batch SDK)](sources-sdk/api/api-overview.md)
      - [Erste Schritte](sources-sdk/api/getting-started.md)
      - [Erstellen einer Verbindungsspezifikation](sources-sdk/api/create.md)
      - [Aktualisieren einer Verbindungsspezifikation](sources-sdk/api/update-connection-specs.md)
      - [Aktualisieren einer Flussspezifikation](sources-sdk/api/update-flow-specs.md)
      - [Übermitteln Ihrer Quelle](sources-sdk/api/submit.md)
   - Dokumentationshandbuch {#documentation}
      - [Dokumentieren Ihrer Quelle in Adobe Experience Platform](sources-sdk/documentation/doc-overview.md)
      - [Verwenden der GitHub-Web-Oberfläche, um eine Seite mit der Quellendokumentation zu erstellen](sources-sdk/documentation/github.md)
      - [Verwenden eines Texteditors in Ihrer lokalen Umgebung, um die Seite mit der Quellendokumentation zu erstellen.](sources-sdk/documentation/text-editor.md)
      - [Dokumentationsvorlage für Selbstbedienungs-API](sources-sdk/documentation/template.md)
      - [Dokumentationsvorlage für Selbstbedienungs-Benutzeroberfläche](sources-sdk/documentation/ui-template.md)
   - Streaming-SDK {#streaming-sdk}
      - [Erste Schritte mit Selbstbedienungsquellen (Streaming-SDK)](sources-sdk/streaming/getting-started.md)
      - [Erstellen einer Verbindungsspezifikation für eine Streaming-Quelle](sources-sdk/streaming/create.md)
      - [Aktualisierung einer Verbindungsspezifikation für eine Streaming-Quelle](sources-sdk/streaming/update-connection-specs.md)
      - [Aktualisieren der Streaming-Flussspezifikation](sources-sdk/streaming/update-flow-specs.md)
      - [Testen und Senden einer Verbindungsspezifikation zur Verifizierung](sources-sdk/streaming/submit.md)
      - [Dokumentieren einer Quelle (Streaming-SDK)](sources-sdk/streaming/document-streaming.md)
      - [Dokumentation einer Streaming-Vorlage für eine Selbstbedienungs-API](sources-sdk/streaming/streaming-template-api.md)
      - [Dokumentation einer Streaming-Vorlage für eine Selbstbedienungs-Benutzeroberfläche](sources-sdk/streaming/streaming-template-ui.md)
- Fehlermeldungen {#errors}
   - [Fehlermeldungen in Quellen](./errors/sources-errors.md)
   - [Fehlermeldungen in Flow Service](./errors/flow-service-errors.md)
- [Flusslaufbenachrichtigungen](notifications.md)
- [IP-Adressen-Zulassungsliste](ip-address-allow-list.md)
- [Häufig gestellte Fragen](./troubleshooting.md)
- [API-Referenz](https://www.adobe.io/experience-platform-apis/references/flow-service/)
- [Versionshinweise zu Experience Platform](https://experienceleague.adobe.com/de/docs/experience-platform/release-notes/latest)
