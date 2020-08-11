---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Überblick über Adobe Experience Platform Connectoren für Datenquellen
topic: overview
translation-type: tm+mt
source-git-commit: 8e39cc206efa3fc314ae689845c88f0923ac1743
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 59%

---


# Übersicht über Connectoren für Datenquellen

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Diese sogenannten „Quell-Connectoren“ bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

With [!DNL Experience Platform], you can centralize data you collect from disparate sources and use the insights gained from it to do more.

## Arten von Datenquellen

Sources in [!DNL Experience Platform] are grouped into the following categories:

### Adobe-Anwendungen

[!DNL Experience Platform] allows data to be ingested from other Adobe applications, including Adobe Analytics, Adobe Audience Manager, and [!DNL Experience Platform Launch]. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [Übersicht über den Adobe Audience Manager-Connector](connectors/adobe-applications/audience-manager.md)
- [Erstellen eines Quell-Connectors für Adobe Audience Manager über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Übersicht über den Adobe Analytics-Connector](connectors/adobe-applications/analytics.md)
- [Erstellen eines Quell-Connectors für Adobe Analytics über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/analytics.md)
- [Erstellen eines Quell-Connectors für Kundenattribute in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Werbung

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Drittanbieteranzeigesystem. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [!DNL Google AdWords](connectors/advertising/ads.md) connector

### Cloud-Speicherplatz

Cloud storage sources can bring your own data into [!DNL Platform] without the need to download, format, or upload. Ingested data can be formatted as XDM JSON, XDM parquet, or delimited. Die einzelnen Prozessschritte werden anhand der Benutzeroberfläche in den Datenquellen-Workflow integriert. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [!DNL Azure Data Lake Storage Gen2](connectors/cloud-storage/adls-gen2.md) connector
- [!DNL Azure Blob](connectors/cloud-storage/blob.md) connector
- [!DNL Amazon Kinesis](connectors/cloud-storage/kinesis.md) connector
- [!DNL Amazon S3](connectors/cloud-storage/s3.md) connector
- [!DNL Apache HDFS](connectors/cloud-storage/hdfs.md) connector
- [!DNL Azure Event Hubs](connectors/cloud-storage/eventhub.md) connector
- [!DNL Azure File Storage](connectors/cloud-storage/azure-file-storage.md) connector
- [!DNL FTP and SFTP](connectors/cloud-storage/ftp-sftp.md) connector
- [!DNL Google Cloud Storage](connectors/cloud-storage/google-cloud-storage.md) connector

### CRM (Customer Relationship Management)

CRM-Systeme liefern Daten, mit deren Hilfe Kundenbeziehungen gepflegt werden können, um die Kundentreue und -bindung zu fördern. [!DNL Experience Platform] provides support for ingesting CRM data from [!DNL Microsoft Dynamics 365] and [!DNL Salesforce]. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [!DNL Microsoft Dynamics](connectors/crm/ms-dynamics.md) connector
- [!DNL Salesforce](connectors/crm/salesforce.md) connector

### Customer Success

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Drittanbieter-Anwendungen für das Customer Success Management. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [!DNL Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md) connector
- [!DNL ServiceNow](connectors/customer-success/servicenow.md) connector

### Datenbank

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [!DNL Amazon Redshift](connectors/databases/redshift.md) connector
- [!DNL Apache Hive on Azure HDInsights](connectors/databases/hive.md) connector
- [!DNL Apache Spark on Azure HDInsights](connectors/databases/spark.md) connector
- [!DNL Azure Data Explorer](connectors/databases/data-explorer.md) connector
- [!DNL Azure Synapse Analytics](connectors/databases/synapse-analytics.md) connector
- [!DNL Azure Table Storage](connectors/databases/ats.md) connector
- [!DNL Couchbase](connectors/databases/couchbase.md) connector
- [!DNL Google BigQuery](connectors/databases/bigquery.md) connector
- [!DNL GreenPlum](connectors/databases/greenplum.md) connector
- [!DNL HP Vertica](connectors/databases/hp-vertica.md) connector
- [!DNL IBM DB2](connectors/databases/ibm-db2.md) connector
- [!DNL MariaDB](connectors/databases/mariadb.md) connector
- [!DNL Microsoft SQL Server](connectors/databases/sql-server.md) connector
- [!DNL MySQL](connectors/databases/mysql.md) connector
- [!DNL Oracle](connectors/databases/oracle.md) connector
- [!DNL Phoenix](connectors/databases/phoenix.md) connector
- [!DNL PostgreSQL](connectors/databases/postgres.md) connector

### Marketing-Automatisierung

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Drittanbietersystemen für die Marketing-Automatisierung. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [!DNL HubSpot](connectors/marketing-automation/hubspot.md) connector

### Payments

[!DNL Experience Platform] provides support for ingesting data from a third-party payments system. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [!DNL PayPal](connectors/payments/paypal.md) connector

### Protocols

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Drittanbieter-Protokollsystem. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [!DNL Generic OData](connectors/protocols/odata.md) connector

## Zugriffskontrolle für Quellen zur Datenaufnahme

Zugriffsberechtigungen für die zur Datenaufnahme verwendeten Quellen können über Adobe Admin Console verwaltet werden. Der Zugriff auf die Berechtigungen für ein bestimmtes Produktprofil erfolgt über die ihm zugehörige Registerkarte *[!UICONTROL Berechtigungen]*. Im Bereich **[!UICONTROL Berechtigungen bearbeiten]** können Sie über den Menüeintrag *[!UICONTROL Datenaufnahme]* auf die einer Quelle zugehörigen Berechtigungen zugreifen. Die Berechtigung **[!UICONTROL Quellen anzeigen]** gewährt Lesezugriff auf unter der Registerkarte *[!UICONTROL Katalog]* verfügbare Quellen sowie auf authentifizierte Quellen unter der Registerkarte *[!UICONTROL Durchsuchen]*. Mit der Berechtigung **[!UICONTROL Quellen verwalten]** dagegen wird uneingeschränkter Zugriff zum Anzeigen, Erstellen, Bearbeiten und Deaktivieren von Quellen gewährt.

Die folgende Tabelle zeigt, wie sich die Benutzeroberfläche bei verschiedenen Kombinationen dieser Berechtigungen verhält:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **[!UICONTROL Quellen anzeigen]** aktiviert | Gewährt Lesezugriff auf die unter der Registerkarte *Katalog* aufgeführten Quelltypen sowie auf die Registerkarten *Durchsuchen*, *Konten* und *DataFlow*. |
| **[!UICONTROL Quellen verwalten]** aktiviert | Gewährt zusätzlich zu in den **[!UICONTROL Quellen verwalten]** enthaltenen Berechtigungen Zugriff auf die Option *[!UICONTROL Quelle verbinden]* unter *[!UICONTROL Katalog]* sowie auf die Option *[!UICONTROL Daten auswählen]* unter *[!UICONTROL Durchsuchen]*. **[!UICONTROL Quellen verwalten]** beinhaltet außerdem die Berechtigung zum Aktivieren und Deaktivieren von *[!UICONTROL DataFlows]* sowie zur Bearbeitung der zugehörigen Zeitpläne. |
| **[!UICONTROL Quellen anzeigen]** deaktiviert und **[!UICONTROL Quellen verwalten]** deaktiviert | Sperrt den Zugriff auf alle Quellen. |

Weitere Informationen zu den über Admin Console erteilten Berechtigungen einschließlich der vier hier erläuterten Quellen finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).

## Geschäftsbedingungen {#terms-and-conditions}

By using any of the Sources labeled as beta (“Beta”), You hereby acknowledge that the Beta is provided ***“as is” without warranty of any kind***.

Adobe shall have no obligation to maintain, correct, update, change, modify, or otherwise support the Beta. Es wird empfohlen, Vorsicht walten zu lassen und sich nicht auf die richtige Funktionsweise oder Leistung solcher Beta- und/oder Begleitmaterialien zu verlassen. Die Beta wird als vertrauliche Informationen über die Adobe betrachtet.

Jegliches &quot;Feedback&quot; (Informationen über die Beta einschließlich, aber nicht beschränkt auf Probleme oder Fehler, die Sie bei der Nutzung der Beta, Vorschläge, Verbesserungen und Empfehlungen), die Sie der Adobe zur Verfügung stellen, wird hiermit der Adobe einschließlich aller Rechte, Titel und Interesse an und an solchen Feedback zugewiesen.

Senden Sie Open Feedback oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge freizugeben oder einen Fehler zu melden, eine Funktionsverbesserung zu suchen.
