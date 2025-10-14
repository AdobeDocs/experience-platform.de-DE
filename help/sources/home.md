---
keywords: Experience Platform;Startseite;beliebte Themen;Quell-Connectoren;Quell-Connector;Quellen;Datenquellen;Datenquelle;Datenquellenverbindung
solution: Experience Platform
title: Übersicht über Quell-Connectoren
description: Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Experience Platform-Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: bd5611b23740f16e41048f3bc65f62312593a075
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 54%

---

# Übersicht über Quell-Connectoren

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Experience Platform-Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Experience Platform zu sammeln und zu zentralisieren. Der Service bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie auf einfache Weise Quellverbindungen zu verschiedenen Datenanbietern einrichten können. Diese Quell-Connectoren bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

Mit Experience Platform können Sie Daten aus unterschiedlichen Quellen an zentraler Stelle aufnehmen und auswerten, um auf diesen Erkenntnissen basierend weitere Schritte einzuleiten.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

>[!BEGINSHADEBOX]

## Von Adobe und Partnern erstellte Quellen {#adobe-and-partner-built-sources}

Einige der Connectoren im Experience Platform-Quellkatalog werden von Adobe erstellt und gepflegt, während andere von Partnerunternehmen mithilfe von [Sources SDK&quot; erstellt und &#x200B;](/help/sources/sources-sdk/overview.md) werden. Ein Hinweis oben auf der Dokumentationsseite für jeden von Partnern erstellten Connector gibt an, ob eine Quelle vom Partner erstellt und gepflegt wird. Beispielsweise wird der [Amazon S3-Connector](/help/sources/connectors/cloud-storage/s3.md) von Adobe erstellt, während der [RainFocus-Connector](/help/sources/connectors/analytics/rainfocus.md) vom RainFocus-Team erstellt und gepflegt wird.

Bei von Partnern erstellten und gepflegten Connectoren bedeutet dies, dass Probleme mit dem Connector möglicherweise vom Partner-Team behoben werden müssen (die Kontaktmethode ist jeweils im Hinweis auf der Dokumentationsseite angegeben). Wenden Sie sich bei Problemen mit von Adobe erstellten und gepflegten Connectoren an den Support oder den Kundendienst von Adobe.

>[!ENDSHADEBOX]

## Quellkatalog

In den folgenden Abschnitten finden Sie eine Liste aller im Quellkatalog verfügbaren Quellen.

### Adobe-Anwendungen {#adobe-applications}

Experience Platform ermöglicht die Aufnahme von Daten aus anderen Adobe-Programmen wie Adobe Analytics und Adobe Audience Manager. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Adobe Audience Manager](connectors/adobe-applications/audience-manager.md)
   - [Adobe Audience Manager-Quellverbindung über die Benutzeroberfläche erstellen](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics-Klassifizierungsdaten](connectors/adobe-applications/classifications.md)
   - [Erstellen einer Adobe Analytics Classifications-Datenquellverbindung über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics Report Suite-Daten](connectors/adobe-applications/analytics.md)
   - [Adobe Analytics-Quellverbindung über die Benutzeroberfläche erstellen](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services](connectors/adobe-applications/campaign.md)
   - [Erstellen einer Quellverbindung zu Adobe Campaign Managed Cloud Services in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce](connectors/adobe-applications/commerce.md)
- [Adobe-Datenerfassung](connectors/adobe-applications/data-collection.md)
   - [Erstellen einer Quellverbindung für Kundenattribute in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]](connectors/adobe-applications/marketo/marketo.md)
   - [Erstellen einer  [!DNL Marketo Engage] -Quellverbindung über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Erstellen einer  [!DNL Marketo Engage] -Quellverbindung und eines Datenflusses für benutzerdefinierte Aktivitätsdaten](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Erweiterte Unternehmensquellen {#advanced-enterprise-sources}

Die folgenden Quellen stehen nur [Kunden von Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) zur Verfügung.

| Quelle | Kategorie | Aufnahmetyp | Cloud |
| --- | --- | --- | --- |
| [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) | Cloud-Speicherplatz | Streaming | Azure, AWS |
| [[!DNL Amazon Redshift]](connectors/databases/redshift.md) | Datenbank | Batch | Azure, AWS |
| [[!DNL Azure Databricks]](connectors/databases/databricks.md) | Datenbank | Batch | Azure |
| [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) | Cloud-Speicherplatz | Streaming | Azure, AWS |
| [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) | Datenbank | Batch | Azure |
| [[!DNL Google BigQuery]](connectors/databases/bigquery.md) | Datenbank | Batch | Azure, AWS |
| [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) | Cloud-Speicherplatz | Streaming | Azure |
| [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) | Datenbank | Streaming | Azure, AWS |
| [[!DNL Snowflake]](connectors/databases/snowflake.md) | Datenbank | Batch | Azure, AWS |

{style="table-layout:auto"}

### Werbung {#advertising}

Sie können die folgenden Quellen verwenden, um Werbedaten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [Google Ads](connectors/advertising/ads.md) | Batch | Azure |

{style="table-layout:auto"}

### Analytics {#analytics}

Sie können die folgenden Quellen verwenden, um Analysedaten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) | Batch | Azure |
| [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) | Streaming | Azure |
| [[!DNL RainFocus]](connectors/analytics/rainfocus.md) | Streaming | Azure |

{style="table-layout:auto"}

### Cloud-Speicherplatz {#cloud-storage}

Cloud-Speicherquellen können Ihre eigenen Daten in Experience Platform übertragen, ohne sie herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Die einzelnen Prozessschritte werden mit der Benutzeroberfläche in den Quellen-Workflow integriert. Näheres hierzu finden Sie in den folgenden Dokumenten:

Sie können die folgenden Quellen verwenden, um Cloud-Speicherdaten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) | Batch | Azure |
| [[!DNL Azure Blob Storage]](connectors/cloud-storage/blob.md) | Batch | Azure |
| [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) | Batch | Azure, AWS |
| [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) | Batch | Azure |
| [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) | Batch | Azure |
| [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) | Batch | Azure, AWS |
| [[!DNL FTP]](connectors/cloud-storage/ftp.md) | Batch | Azure |
| [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) | Batch | Azure |
| [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) | Batch | Azure |
| [[!DNL SFTP]](connectors/cloud-storage/sftp.md) | Batch | Azure |

{style="table-layout:auto"}

### Einverständnis und Voreinstellungen {#consent}

Sie können die folgenden Quellen verwenden, um Einverständnis- und Voreinstellungsdaten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL Didomi]](../sources/connectors/consent-and-preferences/didomi.md) | Streaming | Azure |
| [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) | Batch | Azure |

{style="table-layout:auto"}

### CRM (Customer Relationship Management) {#customer-relationship-management}

CRM-Systeme liefern Daten, mit deren Hilfe Kundenbeziehungen gepflegt werden können, um die Kundentreue und -bindung zu fördern. Experience Platform unterstützt die Aufnahme von CRM-Daten aus [!DNL Microsoft Dynamics 365] und [!DNL Salesforce]. Näheres hierzu finden Sie in den folgenden Dokumenten:

Sie können die folgenden Quellen verwenden, um CRM-Daten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) | Batch | Azure |
| [[!DNL Salesforce]](connectors/crm/salesforce.md) | Batch | Azure, AWS |
| [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) | Batch | Azure |
| [[!DNL Veeva CRM]](connectors/crm/veeva.md) | Batch | Azure |

{style="table-layout:auto"}

### Customer Success {#customer-success}

Sie können die folgenden Quellen verwenden, um Kundenerfolgsdaten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) | Batch | Azure |
| [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) | Batch | Azure |
| [[!DNL Zendesk]](connectors/customer-success/zendesk.md) | Batch | Azure |

{style="table-layout:auto"}

### Datenbank {#database}

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

Sie können die folgenden Quellen verwenden, um Daten aus Ihrer Datenbank in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) | Batch | Azure |
| [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) | Batch | Azure |
| [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) | Batch | Azure |
| [[!DNL Azure Table Storage]](connectors/databases/ats.md) | Batch | Azure |
| [[!DNL GreenPlum]](connectors/databases/greenplum.md) | Batch | Azure |
| [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) | Batch | Azure |
| [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) | Batch | Azure |
| [[!DNL MariaDB]](connectors/databases/mariadb.md) | Batch | Azure |
| [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) | Batch | Azure |
| [[!DNL MySQL]](connectors/databases/mysql.md) | Batch | Azure, AWS |
| [[!DNL Oracle]](connectors/databases/oracle.md) | Batch | Azure, AWS |
| [[!DNL PostgreSQL]](connectors/databases/postgres.md) | Batch | Azure, AWS |
| [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) | Batch | Azure |

{style="table-layout:auto"}

### Daten- und Identitätspartner {#data-partner}

Sie können die folgenden Quellen verwenden, um Daten und Identitätspartnerdaten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) | Batch | Azure |
| [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) | Batch | Azure |
| [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md) | Batch | Azure |
| [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) | Batch | Azure |
| [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) | Batch | Azure |
| [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) | Batch | Azure |

{style="table-layout:auto"}

### E-Commerce {#ecommerce}

Sie können die folgenden Quellen verwenden, um E-Commerce-Daten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) | Batch | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify.md) | Batch | Azure |
| [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) | Streaming | Azure |

{style="table-layout:auto"}

### Lokales System {#local-system}

Sie können die folgenden Quellen verwenden, um Daten aus Ihrem lokalen System in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [Lokaler Datei-Upload](connectors/local-system/local-file-upload.md) | Batch | Azure |

{style="table-layout:auto"}

### Treue {#loyalty}

Sie können die folgenden Quellen verwenden, um Treueprogramm-Daten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL Capillary Streaming Events]](connectors/loyalty/capillary.md) | Streaming | Azure |

{style="table-layout:auto"}

### Marketing-Automatisierung {#marketing-automation}

Sie können die folgenden Quellen verwenden, um Daten zur Marketing-Automatisierung in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL Braze]](connectors/marketing-automation/braze.md) | Streaming | Azure |
| [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) | Streaming | Azure |
| [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) | Streaming | Azure |
| [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) | Batch | Azure |
| [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) | Batch | Azure |
| [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) | Batch | Azure |
| [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) | Batch | Azure |
| [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) | Batch | Azure |
| [[!DNL Relay Connector]](tutorials/ui/create/marketing-automation/relay-connector.md) | Streaming | Azure |
| [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) | Batch | Azure, AWS |

{style="table-layout:auto"}

### Zahlungen {#payments}

Sie können die folgenden Quellen verwenden, um Zahlungsdaten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud |
| --- | --- | --- |
| [[!DNL Square]](connectors/payments/square.md) | Batch | Azure |
| [[!DNL Stripe]](connectors/payments/stripe.md) | Batch | Azure |

{style="table-layout:auto"}

### Streaming {#streaming}

Sie können die folgenden Quellen verwenden, um Daten an Experience Platform zu streamen.

| Quelle | Aufnahmetyp | Cloud-Support |
| --- | --- | --- |
| [[!DNL HTTP API]](connectors/streaming/http.md) | Streaming | Azure, AWS |

{style="table-layout:auto"}

### Protokolle {#protocols}

Sie können die folgenden Quellen verwenden, um Protokolldaten in Experience Platform aufzunehmen.

| Quelle | Aufnahmetyp | Cloud-Support |
| --- | --- | --- |
| [[!DNL Generic OData]](connectors/protocols/odata.md) | Batch | Azure |
| [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) | Batch | Azure |

{style="table-layout:auto"}

## Zugriffskontrolle für Quellen zur Datenaufnahme

Zugriffsberechtigungen für die zur Datenaufnahme verwendeten Quellen können über Adobe Admin Console verwaltet werden. Der Zugriff auf die Berechtigungen für ein bestimmtes Produktprofil erfolgt über die ihm zugehörige Registerkarte **[!UICONTROL Berechtigungen]**. Im Bereich **[!UICONTROL Berechtigungen bearbeiten]** können Sie über den Menüeintrag **[!UICONTROL Datenaufnahme]** auf die einer Quelle zugehörigen Berechtigungen zugreifen. Die Berechtigung **[!UICONTROL Quellen anzeigen]** gewährt Lesezugriff auf unter der Registerkarte **[!UICONTROL Katalog]** verfügbare Quellen sowie auf authentifizierte Quellen unter der Registerkarte **[!UICONTROL Durchsuchen]**. Mit der Berechtigung **[!UICONTROL Quellen verwalten]** dagegen wird uneingeschränkter Zugriff zum Anzeigen, Erstellen, Bearbeiten und Deaktivieren von Quellen gewährt.

Die folgende Tabelle zeigt, wie sich die Benutzeroberfläche bei verschiedenen Kombinationen dieser Berechtigungen verhält:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **[!UICONTROL Quellen anzeigen]** aktiviert | Gewährt Lesezugriff auf die auf der Registerkarte „Katalog“ aufgeführten Quelltypen sowie auf die Registerkarten „Durchsuchen“, „Konten“ und „Datenfluss“. |
| **[!UICONTROL Quellen verwalten]** aktiviert | Gewährt zusätzlich zu in den **[!UICONTROL Quellen verwalten]** enthaltenen Berechtigungen Zugriff auf die Option **[!UICONTROL Quelle verbinden]** unter **[!UICONTROL Katalog]** sowie auf die Option **[!UICONTROL Daten auswählen]** unter **[!UICONTROL Durchsuchen]**. **[!UICONTROL Quellen verwalten]** beinhaltet außerdem die Berechtigung zum Aktivieren und Deaktivieren von **[!UICONTROL DataFlows]** sowie zur Bearbeitung der zugehörigen Zeitpläne. |
| **[!UICONTROL Quellen anzeigen]** deaktiviert und **[!UICONTROL Quellen verwalten]** deaktiviert | Sperrt den Zugriff auf alle Quellen. |

Weitere Informationen zu den verfügbaren Berechtigungen, die über Adobe-Berechtigungen gewährt werden, finden Sie unter [Zugriffssteuerung - Übersicht](../access-control/home.md).

### Attributbasierte Zugriffssteuerung

Die attributbasierte Zugriffssteuerung in Adobe Experience Platform ermöglicht Admins, den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen zu steuern.

Mit der attributbasierten Zugriffssteuerung können Sie Zuordnungskonfigurationen auf Felder anwenden, für die Sie über Berechtigungen verfügen. Im Übrigen können Sie keine Daten in einen Datensatz aufnehmen, wenn Sie nicht auf alle Felder im Datensatz Zugriff haben.

#### Unterstützung der attributbasierten Zugriffssteuerung in Quellen

>[!TIP]
>
>Die attributbasierte Zugriffssteuerung funktioniert wie folgt: **Rollen** werden erstellt, um die Benutzertypen zu kategorisieren, die mit Ihrer Experience Platform-Instanz interagieren. **Kennzeichnungen** werden auf &quot;**&quot; angewendet** um den Zugriff auf diese bestimmte Rolle festzulegen. **Kennzeichnungen** werden auch auf Ressourcen wie Schemafelder und Segmente angewendet. Damit ein Benutzer Zugriff auf bestimmte Schemafelder und Segmente hat, muss er einer Rolle *mit derselben Beschriftung, die der abgefragten Ressource zugewiesen ist* hinzugefügt werden. Weitere Informationen finden Sie im [End-to-End-Handbuch zur attributbasierten Zugriffssteuerung](../access-control/abac/end-to-end-guide.md).

- Wenden Sie Kennzeichnungen auf Schemafelder an, um den Zugriff auf bestimmte Schemafelder in Ihrer Organisation zu definieren. Sobald der Zugriff auf bestimmte Schemafelder eingerichtet ist, können Benutzerinnen und Benutzer nur noch Zuordnungen für die Felder erstellen, auf die sie Zugriff haben.
- Benutzende ohne die entsprechenden Rollen können keine Datenflüsse mit Zuordnungen erstellen oder aktualisieren, die unzugängliche Schemafelder beinhalten. Darüber hinaus können nicht autorisierte Benutzer vorhandene Datenflüsse mit nicht zugänglichen Schemafeldern nicht aktualisieren, löschen, aktivieren oder deaktivieren.
- Darüber hinaus muss ein Datenfluss in seiner Zuordnung, seinem Zieldatensatz und seiner Zielverbindung exakt dieselbe Schema-ID und Version haben. Dies gilt sowohl für standardmäßige XDM-Schemata als auch für modellbasierte Schemata.

>[!NOTE]
>
>Modellbasierte Schemata haben zusätzliche Anforderungen, einschließlich der Felder Primärschlüssel und Versionskennung. Weitere Informationen finden Sie unter [Übersicht über modellbasierte Schemata](../xdm/schema/model-based.md).

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../access-control/abac/overview.md).

## Allgemeine Geschäftsbedingungen {#terms-and-conditions}

Durch Verwendung einer der als Beta („Beta“) gekennzeichneten Quellen erkennen Sie hiermit an, dass die Beta-Version ***ohne Mängelgewähr und ohne Gewährleistung jeglicher Art*** bereitgestellt wird.

Adobe ist nicht verpflichtet, die Beta-Version zu pflegen, zu korrigieren, zu aktualisieren, zu ändern oder anderweitig zu unterstützen. Es wird empfohlen, informative Inhalte zu verwenden und sich nicht auf die ordnungsgemäße Funktionsweise oder Leistung solcher Beta und/oder Begleitmaterialien zu verlassen. Die Beta-Version wird als vertrauliche Information von Adobe betrachtet.

Jedes „Feedback“ (Informationen zur Beta-Version, einschließlich, aber nicht beschränkt auf Probleme oder Mängel, auf die Sie bei der Verwendung der Beta-Version stoßen, Vorschläge, Verbesserungen und Empfehlungen), das Sie Adobe übermitteln, wird hiermit an Adobe übertragen, einschließlich aller Rechte, Titel und Interessen an diesem Feedback.

Senden Sie offenes Feedback oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge mitzuteilen, einen Fehler zu melden oder um eine Funktionsverbesserung zu bitten.
