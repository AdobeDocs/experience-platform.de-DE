---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über Adobe Experience Platform Source Connectors
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 1%

---


# Übersicht über die Quellenanschlüsse

Adobe Experience Platform allows data to be ingested from external sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services. Sie können Daten aus verschiedenen Quellen wie Adobe-Anwendungen, Cloud-basierte Datenspeicherung, Datenbanken und vielen anderen Quellen erfassen.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie Quellverbindungen zu verschiedenen Datenanbietern einfach einrichten können. Diese Quellverbindungen ermöglichen es Ihnen, Ihre Drittanbietersysteme zu authentifizieren, Zeiten für die Erfassung festzulegen und den Datendurchsatz zu verwalten.

Mit [!DNL Experience Platform]dieser Funktion können Sie Daten, die Sie aus unterschiedlichen Quellen erfassen, zentralisieren und die dabei gewonnenen Erkenntnisse nutzen, um mehr zu tun.

## Arten von Quellen

Die Quellen in [!DNL Experience Platform] sind in die folgenden Kategorien gruppiert:

### Adobe-Programme

[!DNL Experience Platform] ermöglicht die Erfassung von Daten aus anderen Adobe-Anwendungen, einschließlich Adobe Analytics, Adobe Audience Manager und [!DNL Experience Platform Launch]. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über den Adobe Audience Manager-Connector](connectors/adobe-applications/audience-manager.md)
- [Erstellen eines Adobe Audience Manager-Quellconnectors in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Überblick über den Analytics-Datenschnittstellen](connectors/adobe-applications/analytics.md)
- [Erstellen eines Adobe Analytics-Quellconnectors in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/analytics.md)
- [Erstellen eines Quell-Connectors für Kundenattribute in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Werbung

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Drittanbieteranzeigesystem. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [!DNL Google AdWords](connectors/advertising/ads.md) connector

### Cloud-Speicherplatz

Cloud-Datenspeicherung-Quellen können Ihre eigenen Daten in [!DNL Platform] ohne Download, Format oder Upload übertragen. Ingetierte Daten können als XDM-JSON-, XDM-Parkett oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird über die Benutzeroberfläche in den Sources-Workflow integriert. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [!DNL Azure Data Lake Storage Gen2](connectors/cloud-storage/adls-gen2.md) connector
- [!DNL Azure Blob and Amazon S3](connectors/cloud-storage/blob-s3.md) connector
- [!DNL Amazon Kinesis](connectors/cloud-storage/kinesis.md) connector
- [!DNL Apache HDFS](connectors/cloud-storage/hdfs.md) connector
- [!DNL Azure Event Hubs](connectors/cloud-storage/eventhub.md) connector
- [!DNL Azure File Storage](connectors/cloud-storage/azure-file-storage.md) connector
- [!DNL FTP and SFTP](connectors/cloud-storage/ftp-sftp.md) connector
- [!DNL Google Cloud Storage](connectors/cloud-storage/google-cloud-storage.md) connector

### CRM (Customer Relationship Management)

CRM-Systeme bieten Daten, die dazu beitragen können, Kundenbeziehungen aufzubauen, was wiederum Loyalität schafft und die Kundenbindung fördert. [!DNL Experience Platform] bietet Unterstützung für die Erfassung von CRM-Daten aus [!DNL Microsoft Dynamics 365] und [!DNL Salesforce]. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [!DNL Microsoft Dynamics](connectors/crm/ms-dynamics.md) connector
- [!DNL Salesforce](connectors/crm/salesforce.md) connector

### Kundenerfolg

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einer Drittanbieter-Kundenerfolganwendung. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [!DNL Salesforce Service Cloud](connectors/customer-success/salesforce-service-cloud.md) connector
- [!DNL ServiceNow](connectors/customer-success/servicenow.md) connector

### Datenbank

[!DNL Experience Platform] unterstützt das Erfassen von Daten aus einer Datenbank eines Drittanbieters. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

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

### Marketingautomatisierung

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Marketingautomatisierungssystem eines Drittanbieters. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [!DNL HubSpot](connectors/marketing-automation/hubspot.md) connector

### Zahlungen

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Zahlungssystem eines Drittanbieters. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [!DNL PayPal](connectors/payments/paypal.md) connector

### Protokolle

[!DNL Experience Platform] unterstützt die Erfassung von Daten aus einem Drittanbieter-Protokollsystem. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [!DNL Generic OData](connectors/protocols/odata.md) connector

## Zugriffskontrolle für Quellen bei der Datenerfassung

Berechtigungen für Quellen in der Datenerfassung können innerhalb der Adobe-Admin Console verwaltet werden. Sie können auf Berechtigungen über die Registerkarte &quot; *[!UICONTROL Berechtigungen]* &quot;in einem bestimmten Profil zugreifen. Über den Menüeintrag &quot; **[!UICONTROL Berechtigungen]** bearbeiten&quot;können Sie über den Eintrag im Menü &quot; *[!UICONTROL Dateneingabe]* &quot;auf die Berechtigungen für Quellen zugreifen. Die Berechtigung &quot; **[!UICONTROL Ansichten-Quellen]** &quot;gewährt schreibgeschützten Zugriff auf verfügbare Quellen auf der Registerkarte &quot; *[!UICONTROL Katalog]* &quot;und auf authentifizierte Quellen auf der Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;. Die Berechtigung &quot;Quellen **[!UICONTROL verwalten]** &quot;gewährt uneingeschränkten Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen.

Die folgende Tabelle zeigt, wie sich die Benutzeroberfläche auf der Grundlage verschiedener Kombinationen dieser Berechtigungen verhält:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **[!UICONTROL Ansicht-Quellen]** auf | Gewähren Sie schreibgeschützten Zugriff auf Quellen in jedem Quelltyp auf der Registerkarte &quot; *Katalog* &quot;sowie auf die Registerkarten &quot; *Durchsuchen*&quot;, &quot; *Konten*&quot;und &quot; *DataFlow* &quot;. |
| **[!UICONTROL Quellen]** verwalten unter | Gewährt zusätzlich zu den Funktionen in den **[!UICONTROL Ansichten-Quellen]** Zugriff auf die Option &quot; *[!UICONTROL Verbindungsquelle]* &quot;im *[!UICONTROL Katalog]* und auf die Option &quot;Daten ** auswählen&quot;in *[!UICONTROL Durchsuchen]*. **[!UICONTROL Mit Quellen]** verwalten können Sie auch *[!UICONTROL DataFlows]* aktivieren oder deaktivieren und deren Zeitpläne bearbeiten. |
| **[!UICONTROL Ansicht-Quellen]** deaktivieren und Quellen **[!UICONTROL verwalten]** deaktivieren | Sperren Sie den Zugriff auf alle Quellen. |

Weitere Informationen zu den verfügbaren Berechtigungen, die über die Admin Console erteilt wurden, einschließlich dieser vier Quellen, finden Sie in der Übersicht über die [Zugriffskontrolle](../access-control/home.md).

## Geschäftsbedingungen {#terms-and-conditions}

Durch die Verwendung einer der als Beta (&quot;Beta&quot;) gekennzeichneten Quellen bestätigen Sie hiermit, dass die Betaversion ***&quot;wie besehen&quot;ohne Gewährleistung jeglicher Art*** bereitgestellt wird.

Adobe ist nicht verpflichtet, die Beta-Version beizubehalten, zu korrigieren, zu aktualisieren, zu ändern, zu ändern oder anderweitig zu unterstützen. Es wird empfohlen, Vorsicht walten zu lassen und sich nicht auf die richtige Funktionsweise oder Leistung solcher Beta- und/oder Begleitmaterialien zu verlassen. Die Beta-Version wird als vertrauliche Informationen von Adobe betrachtet.

Alle &quot;Feedback&quot;(Informationen zur Betaversion, einschließlich, aber nicht beschränkt auf Probleme oder Defekte, auf die Sie bei der Verwendung der Beta-Version stoßen, Vorschläge, Verbesserungen und Empfehlungen), die Sie Adobe zur Verfügung stellen, werden Adobe hiermit zugewiesen, einschließlich aller Rechte, Titel und Interessen an und an solchen Feedback.

Senden Sie Open Feedback oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge freizugeben oder einen Fehler zu melden, eine Funktionsverbesserung zu suchen.
