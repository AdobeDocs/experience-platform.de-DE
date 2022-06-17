---
keywords: Experience Platform;Startseite;beliebte Themen;Quell-Connectoren;Quell-Connector;Quellen;Datenquellen;Datenquelle;Datenquellenverbindung
solution: Experience Platform
title: Übersicht über Quell-Connectoren
topic-legacy: overview
description: Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 16f61ae259f6da23cfb7aa96e685716cd623d1b2
workflow-type: ht
source-wordcount: '1001'
ht-degree: 100%

---

# Übersicht über Quell-Connectoren

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Platform zu sammeln und zu zentralisieren. Der Service bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie auf einfache Weise Quellverbindungen zu verschiedenen Datenanbietern einrichten können. Diese sogenannten „Quell-Connectoren“ bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

Mit Experience Platform können Sie Daten aus unterschiedlichen Quellen an zentraler Stelle aufnehmen und auswerten, um auf diesen Erkenntnissen basierend weitere Schritte einzuleiten.

## Arten von Datenquellen

Die für die Aufnahme in Experience Platform verwendeten Datenquellen sind in folgende Kategorien unterteilt:

### Adobe-Anwendungen {#adobe-applications}

Experience Platform ermöglicht die Aufnahme von Daten aus anderen Adobe-Programmen wie Adobe Analytics und Adobe Audience Manager. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [Übersicht über Adobe Audience Manager-Quellen](connectors/adobe-applications/audience-manager.md)
- [Erstellen einer Adobe Audience Manager-Quellverbindung über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Übersicht über Adobe Analytics Classifications-Datenquellenverbindungen](connectors/adobe-applications/classifications.md)
- [Erstellen einer Adobe Analytics Classifications-Datenquellenverbindung über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/classifications.md)
- [Übersicht über Adobe Analytics-Report Suite-Datenquellenverbindungen](connectors/adobe-applications/analytics.md)
- [Erstellen einer Adobe Analytics-Quellverbindung über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/analytics.md)
- [Übersicht über die Quellen der Adobe-Datenerfassung](connectors/adobe-applications/data-collection.md)
- [Erstellen einer Quellverbindung für Kundenattribute in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [Übersicht über [!DNL Marketo Engage]-Quellen](connectors/adobe-applications/marketo/marketo.md)
- [Erstellen einer  [!DNL Marketo Engage] -Quellverbindung über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/marketo.md)

### Werbung {#advertising}

Experience Platform ermöglicht die Aufnahme von Daten aus Werbesystemen von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Google AdWords]](connectors/advertising/ads.md)

<!-- ### Analytics {#analytics}

Experience Platform provides support for ingesting data from a third-party analytics platform. See the following related documents for more information:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) -->

### Cloud-Speicherplatz {#cloud-storage}

Cloud-Speicher bieten eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Die einzelnen Prozessschritte werden mit der Benutzeroberfläche in den Quellen-Workflow integriert. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP]](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md)

### Einverständnis und Voreinstellungen {#consent}

Experience Platform unterstützt die Aufnahme von Daten aus einer Einverständnis- und Voreinstellungs-Verwaltungsplattform von Dritten. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)

### CRM (Customer Relationship Management) {#customer-relationship-management}

CRM-Systeme liefern Daten, mit deren Hilfe Kundenbeziehungen gepflegt werden können, um die Kundentreue und -bindung zu fördern. Experience Platform unterstützt die Aufnahme von CRM-Daten aus [!DNL Microsoft Dynamics 365] und [!DNL Salesforce]. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Customer Success {#customer-success}

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbieter-Anwendungen für das Customer Success Management. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md)

### Datenbank {#database}

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage]](connectors/databases/ats.md)
- [[!DNL Couchbase]](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md)
- [[!DNL GreenPlum]](connectors/databases/greenplum.md)
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB]](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [[!DNL MySQL]](connectors/databases/mysql.md)
- [[!DNL Oracle]](connectors/databases/oracle.md)
- [[!DNL Phoenix]](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL]](connectors/databases/postgres.md)
- [[!DNL Snowflake]](connectors/databases/snowflake.md)

### E-Commerce {#ecommerce}

Experience Platform ermöglicht die Aufnahme von Daten aus E-Commerce-Systemen von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Lokales System {#local-system}

Experience Platform unterstützt die Erfassung von Daten aus Ihrem lokalen System. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [Lokaler Datei-Upload](connectors/local-system/local-file-upload.md)

### Marketing-Automatisierung {#marketing-automation}

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbietersystemen für die Marketing-Automatisierung. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### Zahlungen {#payments}

Experience Platform ermöglicht die Aufnahme von Daten aus Zahlungssystemen von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### Streaming {#streaming}

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Quellen. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protokolle {#protocols}

Experience Platform ermöglicht die Aufnahme von Daten aus Protokollsystemen von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## Zugriffskontrolle für Quellen zur Datenaufnahme

Zugriffsberechtigungen für die zur Datenaufnahme verwendeten Quellen können über Adobe Admin Console verwaltet werden. Der Zugriff auf die Berechtigungen für ein bestimmtes Produktprofil erfolgt über die ihm zugehörige Registerkarte **[!UICONTROL Berechtigungen]**. Im Bereich **[!UICONTROL Berechtigungen bearbeiten]** können Sie über den Menüeintrag **[!UICONTROL Datenaufnahme]** auf die einer Quelle zugehörigen Berechtigungen zugreifen. Die Berechtigung **[!UICONTROL Quellen anzeigen]** gewährt Lesezugriff auf unter der Registerkarte **[!UICONTROL Katalog]** verfügbare Quellen sowie auf authentifizierte Quellen unter der Registerkarte **[!UICONTROL Durchsuchen]**. Mit der Berechtigung **[!UICONTROL Quellen verwalten]** dagegen wird uneingeschränkter Zugriff zum Anzeigen, Erstellen, Bearbeiten und Deaktivieren von Quellen gewährt.

Die folgende Tabelle zeigt, wie sich die Benutzeroberfläche bei verschiedenen Kombinationen dieser Berechtigungen verhält:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **[!UICONTROL Quellen anzeigen]** aktiviert | Gewährt Lesezugriff auf die auf der Registerkarte „Katalog“ aufgeführten Quelltypen sowie auf die Registerkarten „Durchsuchen“, „Konten“ und „Datenfluss“. |
| **[!UICONTROL Quellen verwalten]** aktiviert | Gewährt zusätzlich zu in den **[!UICONTROL Quellen verwalten]** enthaltenen Berechtigungen Zugriff auf die Option **[!UICONTROL Quelle verbinden]** unter **[!UICONTROL Katalog]** sowie auf die Option **[!UICONTROL Daten auswählen]** unter **[!UICONTROL Durchsuchen]**. **[!UICONTROL Quellen verwalten]** beinhaltet außerdem die Berechtigung zum Aktivieren und Deaktivieren von **[!UICONTROL DataFlows]** sowie zur Bearbeitung der zugehörigen Zeitpläne. |
| **[!UICONTROL Quellen anzeigen]** deaktiviert und **[!UICONTROL Quellen verwalten]** deaktiviert | Sperrt den Zugriff auf alle Quellen. |

Weitere Informationen zu den über Admin Console erteilten Berechtigungen einschließlich der vier hier erläuterten Quellen finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).

## Allgemeine Geschäftsbedingungen {#terms-and-conditions}

Durch Verwendung einer der als Beta („Beta“) gekennzeichneten Quellen erkennen Sie hiermit an, dass die Beta-Version ***ohne Mängelgewähr und ohne Gewährleistung jeglicher Art*** bereitgestellt wird.

Adobe ist nicht verpflichtet, die Beta-Version zu pflegen, zu korrigieren, zu aktualisieren, zu ändern oder anderweitig zu unterstützen. Es wird empfohlen, Vorsicht walten zu lassen und sich nicht auf die korrekte Funktionsweise oder Leistung solcher Beta-Versionen und/oder deren Begleitmaterialien zu verlassen. Die Beta-Version wird als vertrauliche Information von Adobe betrachtet.

Jedes „Feedback“ (Informationen zur Beta-Version, insbesondere Probleme oder Mängel, auf die Sie bei der Verwendung der Beta-Version stoßen, Vorschläge, Verbesserungen und Empfehlungen), das sie Adobe geben, wird hiermit Adobe zugewiesen, einschließlich aller Rechte, Titel und Interessen an diesem Feedback.

Senden Sie offenes Feedback oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge mitzuteilen oder einen Fehler zu melden oder nach einer Funktionsverbesserung zu suchen.
