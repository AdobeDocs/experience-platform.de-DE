---
keywords: Experience Platform;home;popular topics;source connectors;source connector;sources;data sources;data source;data source connection
solution: Experience Platform
title: Überblick über Adobe Experience Platform Connectoren für Datenquellen
topic: overview
description: Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.
translation-type: tm+mt
source-git-commit: 5e5ac80e0c79b3cc0354b469edc036523e29b45d
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 57%

---


# Übersicht über Connectoren für Datenquellen

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Diese sogenannten „Quell-Connectoren“ bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

With [!DNL Experience Platform], you can centralize data you collect from disparate sources and use the insights gained from it to do more.

## Arten von Datenquellen

Sources in [!DNL Experience Platform] are grouped into the following categories:

### Adobe-Anwendungen

[!DNL Experience Platform] ermöglicht die Erfassung von Daten aus anderen Anwendungen der Adobe, einschließlich Adobe Analytics, Adobe Audience Manager und [!DNL Experience Platform Launch]. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [Übersicht über den Adobe Audience Manager-Connector](connectors/adobe-applications/audience-manager.md)
- [Erstellen eines Quell-Connectors für Adobe Audience Manager über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Übersicht über den Adobe Analytics Classifications Data Connector](connectors/adobe-applications/classifications.md)
- [Adobe Analytics Classifications-Datenquellenanschluss in der Benutzeroberfläche erstellen](./tutorials/ui/create/adobe-applications/classifications.md)
- [Übersicht über den Adobe Analytics-Connector](connectors/adobe-applications/analytics.md)
- [Erstellen eines Quell-Connectors für Adobe Analytics über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/analytics.md)
- [Erstellen eines Quell-Connectors für Kundenattribute in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Werbung

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Drittanbieteranzeigesystem. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) connector

### Cloud-Speicherplatz

Cloud storage sources can bring your own data into [!DNL Platform] without the need to download, format, or upload. Ingetierte Daten können als XDM-JSON-, XDM-Parkett oder als Trennzeichen formatiert werden. Die einzelnen Prozessschritte werden anhand der Benutzeroberfläche in den Datenquellen-Workflow integriert. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Azure Data Lake Storage Gen2] connector](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] connector](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] connector](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] connector](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] connector](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] connector](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] connector](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP] connector](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] connector](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL SFTP] connector](connectors/cloud-storage/sftp.md)

### CRM (Customer Relationship Management)

CRM-Systeme liefern Daten, mit deren Hilfe Kundenbeziehungen gepflegt werden können, um die Kundentreue und -bindung zu fördern. [!DNL Experience Platform] bietet Unterstützung für die Erfassung von CRM-Daten aus [!DNL Microsoft Dynamics 365] und [!DNL Salesforce]. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Microsoft Dynamics] connector](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] connector](connectors/crm/salesforce.md)

### Kundenerfolg

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Drittanbieter-Anwendungen für das Customer Success Management. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Salesforce Service Cloud] connector](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] connector](connectors/customer-success/servicenow.md)

### Datenbank

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Amazon Redshift] connector](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] connector](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] connector](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] connector](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] connector](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] connector](connectors/databases/ats.md)
- [[!DNL Couchbase] connector](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] connector](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] connector](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] connector](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] connector](connectors/databases/ibm-db2.md)
- [[!DNL Microsoft SQL Server] connector](connectors/databases/sql-server.md)
- [[!DNL MySQL] connector](connectors/databases/mysql.md)
- [[!DNL Oracle] connector](connectors/databases/oracle.md)
- [[!DNL Phoenix] connector](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] connector](connectors/databases/postgres.md)

### eCommerce

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Drittanbieter-E-Commerce-System. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Marketing-Automatisierung

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Drittanbietersystemen für die Marketing-Automatisierung. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL HubSpot] connector](connectors/marketing-automation/hubspot.md)

### Zahlungen

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Zahlungssystem eines Drittanbieters. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL PayPal] connector](connectors/payments/paypal.md)

### Protokolle

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Drittanbieter-Protokollsystem. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Generic OData] connector](connectors/protocols/odata.md)

## Zugriffskontrolle für Quellen zur Datenaufnahme

Zugriffsberechtigungen für die zur Datenaufnahme verwendeten Quellen können über Adobe Admin Console verwaltet werden. Der Zugriff auf die Berechtigungen für ein bestimmtes Produktprofil erfolgt über die ihm zugehörige Registerkarte **[!UICONTROL Berechtigungen]**. Im Bereich **[!UICONTROL Berechtigungen bearbeiten]** können Sie über den Menüeintrag **[!UICONTROL Datenaufnahme]** auf die einer Quelle zugehörigen Berechtigungen zugreifen. Die Berechtigung **[!UICONTROL Quellen anzeigen]** gewährt Lesezugriff auf unter der Registerkarte **[!UICONTROL Katalog]** verfügbare Quellen sowie auf authentifizierte Quellen unter der Registerkarte **[!UICONTROL Durchsuchen]**. Mit der Berechtigung **[!UICONTROL Quellen verwalten]** dagegen wird uneingeschränkter Zugriff zum Anzeigen, Erstellen, Bearbeiten und Deaktivieren von Quellen gewährt.

Die folgende Tabelle zeigt, wie sich die Benutzeroberfläche bei verschiedenen Kombinationen dieser Berechtigungen verhält:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **[!UICONTROL Quellen anzeigen]** aktiviert | Gewähren Sie auf der Registerkarte &quot;Katalog&quot;schreibgeschützten Zugriff auf die Quellen in den einzelnen Quelltypen sowie auf die Registerkarten &quot;Durchsuchen&quot;, &quot;Konten&quot;und &quot;Datenflug&quot;. |
| **[!UICONTROL Quellen verwalten]** aktiviert | Gewährt zusätzlich zu in den **[!UICONTROL Quellen verwalten]** enthaltenen Berechtigungen Zugriff auf die Option **[!UICONTROL Quelle verbinden]** unter **[!UICONTROL Katalog]** sowie auf die Option **[!UICONTROL Daten auswählen]** unter **[!UICONTROL Durchsuchen]**. **[!UICONTROL Quellen verwalten]** beinhaltet außerdem die Berechtigung zum Aktivieren und Deaktivieren von **[!UICONTROL DataFlows]** sowie zur Bearbeitung der zugehörigen Zeitpläne. |
| **[!UICONTROL Quellen anzeigen]** deaktiviert und **[!UICONTROL Quellen verwalten]** deaktiviert | Sperrt den Zugriff auf alle Quellen. |

Weitere Informationen zu den über Admin Console erteilten Berechtigungen einschließlich der vier hier erläuterten Quellen finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).

## Geschäftsbedingungen {#terms-and-conditions}

Durch die Verwendung einer der als Beta (&quot;Beta&quot;) gekennzeichneten Quellen bestätigen Sie hiermit, dass die Betaversion ***&quot;wie besehen&quot;ohne Gewährleistung jeglicher Art*** bereitgestellt wird.

Die Adobe ist nicht verpflichtet, die Betaversion beizubehalten, zu korrigieren, zu aktualisieren, zu ändern, zu ändern oder anderweitig zu unterstützen. Es wird empfohlen, Vorsicht walten zu lassen und sich nicht auf die richtige Funktionsweise oder Leistung solcher Beta- und/oder Begleitmaterialien zu verlassen. Die Beta wird als vertrauliche Informationen über die Adobe betrachtet.

Jegliches &quot;Feedback&quot; (Informationen über die Beta einschließlich, aber nicht beschränkt auf Probleme oder Fehler, die Sie bei der Nutzung der Beta, Vorschläge, Verbesserungen und Empfehlungen), die Sie der Adobe zur Verfügung stellen, wird hiermit der Adobe einschließlich aller Rechte, Titel und Interesse an und an solchen Feedback zugewiesen.

Senden Sie Open Feedback oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge freizugeben oder einen Fehler zu melden, eine Funktionsverbesserung zu suchen.
