---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über Adobe Experience Platform Source Connectors
topic: overview
translation-type: tm+mt
source-git-commit: a9ce046d6ee8622e23f31edbbf777b045109c13b
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 1%

---


# Übersicht über die Quellenanschlüsse

Adobe Experience Platform ermöglicht die Erfassung von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platformen zu strukturieren, zu beschriften und zu verbessern. Sie können Daten aus verschiedenen Quellen wie Adobe-Anwendungen, Cloud-basierte Datenspeicherung, Datenbanken und vielen anderen Quellen erfassen.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie Quellverbindungen zu verschiedenen Datenanbietern mühelos einrichten können. Diese Quellverbindungen ermöglichen es Ihnen, Ihre Drittanbietersysteme zu authentifizieren, Zeiten für die Erfassung festzulegen und den Datendurchsatz zu verwalten.

Mit der Experience Platform können Sie Daten, die Sie aus unterschiedlichen Quellen erfassen, zentralisieren und die dabei gewonnenen Erkenntnisse nutzen, um mehr zu tun.

## Arten von Quellen

Quellen in Experience Platform sind in die folgenden Kategorien gruppiert:

### Adobe-Programme

Mit der Experience Platform können Daten aus anderen Adobe-Anwendungen, einschließlich Adobe Analytics, Adobe Audience Manager und Experience Platform Launch, erfasst werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über den Adobe Audience Manager-Connector](connectors/adobe-applications/audience-manager.md)
- [Erstellen eines Adobe Audience Manager-Quellconnectors in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Überblick über den Analytics-Datenschnittstellen](connectors/adobe-applications/analytics.md)
- [Erstellen eines Adobe Analytics-Quellconnectors in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/analytics.md)
- [Erstellen eines Quell-Connectors für Kundenattribute in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Werbung

Experience Platform unterstützt die Erfassung von Daten aus einem Drittanbieteranzeigesystem. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [Google AdWords Connector](connectors/advertising/ads.md)

### Cloud-Speicherplatz

Cloud-Datenspeicherung-Quellen können Ihre eigenen Daten in die Platform bringen, ohne dass Sie sie herunterladen, formatieren oder hochladen müssen. Ingetierte Daten können als XDM-JSON-, XDM-Parkett oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird über die Benutzeroberfläche in den Sources-Workflow integriert. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Datenspeicherung Gen2-Stecker für den Azurblau-Data-See](connectors/cloud-storage/adls-gen2.md)
- [Azurblauch und Amazon S3-Stecker](connectors/cloud-storage/blob-s3.md)
- [Amazon Kinesis Connector](connectors/cloud-storage/kinesis.md)
- [Apache HDFS-Anschluss](connectors/cloud-storage/hdfs.md)
- [Azurblauer Ereignis-Hubs-Anschluss](connectors/cloud-storage/eventhub.md)
- [Adapterkabel für die Datenspeicherung](connectors/cloud-storage/azure-file-storage.md)
- [FTP- und SFTP-Anschluss](connectors/cloud-storage/ftp-sftp.md)
- [Google Cloud-Datenspeicherung-Connector](connectors/cloud-storage/google-cloud-storage.md)

### CRM (Customer Relationship Management)

CRM-Systeme bieten Daten, die dazu beitragen können, Kundenbeziehungen aufzubauen, was wiederum Loyalität schafft und die Kundenbindung fördert. Experience Platform unterstützt die Erfassung von CRM-Daten aus Microsoft Dynamics 365 und Salesforce. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Microsoft Dynamics Connector](connectors/crm/ms-dynamics.md)
- [Salesforce-Anschluss](connectors/crm/salesforce.md)

### Kundenerfolg

Experience Platform unterstützt die Erfassung von Daten aus einer Drittanbieter-Kundenerfolganwendung. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Salesforce Service Cloud Connector](connectors/customer-success/salesforce-service-cloud.md)
- [ServiceNow Connector](connectors/customer-success/servicenow.md)

### Datenbank

Experience Platform unterstützt das Erfassen von Daten aus einer Drittanbieterdatenbank. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [Amazon Redshift Connector](connectors/databases/redshift.md)
- [Apache Hive auf der Azurblauen HDInsights-Steckverbindung](connectors/databases/hive.md)
- [Apache Spark auf dem Azurblauen HDInsights-Connector](connectors/databases/spark.md)
- [Blue Data Explorer-Anschluss](connectors/databases/data-explorer.md)
- [Azurblase-Analytics-Stecker](connectors/databases/synapse-analytics.md)
- [Datenspeicherung-Stecker](connectors/databases/ats.md)
- [Steckverbinder](connectors/databases/couchbase.md)
- [Google BigQuery Connector](connectors/databases/bigquery.md)
- [GreenPlum-Anschluss](connectors/databases/greenplum.md)
- [HP-Vertikalanschluss](connectors/databases/hp-vertica.md)
- [IBM DB2 Connector](connectors/databases/ibm-db2.md)
- [MariaDB-Anschluss](connectors/databases/mariadb.md)
- [Microsoft SQL Server Connector](connectors/databases/sql-server.md)
- [MySQL Connector](connectors/databases/mysql.md)
- [Oracle Connector](connectors/databases/oracle.md)
- [Phoenix-Anschluss](connectors/databases/phoenix.md)
- [PostgreSQL Connector](connectors/databases/postgres.md)

### Marketingautomatisierung

Experience Platform unterstützt die Erfassung von Daten aus einem Marketingautomatisierungssystem eines Drittanbieters. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [HubSpot-Anschluss](connectors/marketing-automation/hubspot.md)

### Zahlungen

Experience Platform unterstützt die Erfassung von Daten aus einem Zahlungssystem eines Drittanbieters. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [PayPal-Anschluss](connectors/payments/paypal.md)

### Protokolle

Experience Platform unterstützt die Erfassung von Daten aus einem Drittanbieter-Protokollsystem. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [Generischer OData Connector](connectors/protocols/odata.md)

## Zugriffskontrolle für Quellen bei der Datenerfassung

Berechtigungen für Quellen in der Datenerfassung können innerhalb der Adobe-Admin Console verwaltet werden. Sie können auf Berechtigungen über die Registerkarte &quot; *Berechtigungen* &quot;in einem bestimmten Profil zugreifen. Über den Menüeintrag &quot; **Berechtigungen** bearbeiten&quot;können Sie über den Eintrag im Menü &quot; *Dateneingabe* &quot;auf die Berechtigungen für Quellen zugreifen. Die Berechtigung &quot; **Ansichten-Quellen** &quot;gewährt schreibgeschützten Zugriff auf verfügbare Quellen auf der Registerkarte &quot; *Katalog* &quot;und auf authentifizierte Quellen auf der Registerkarte &quot; *Durchsuchen* &quot;. Die Berechtigung &quot;Quellen **verwalten** &quot;gewährt uneingeschränkten Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen.

Die folgende Tabelle zeigt, wie sich die Benutzeroberfläche auf der Grundlage verschiedener Kombinationen dieser Berechtigungen verhält:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **Ansicht-Quellen** auf | Gewähren Sie schreibgeschützten Zugriff auf Quellen in jedem Quelltyp auf der Registerkarte &quot; *Katalog* &quot;sowie auf die Registerkarten &quot; *Durchsuchen*&quot;, &quot; *Konten*&quot;und &quot; *DataFlow* &quot;. |
| **Quellen** verwalten unter | Gewährt zusätzlich zu den Funktionen, die in den **Ansichten-Quellen** enthalten sind, Zugriff auf die Option &quot; *Verbindungsquelle* &quot;im *Katalog* und auf die Option &quot;Daten ** auswählen&quot;in *Durchsuchen*. **Mit Quellen** verwalten können Sie auch *DataFlows* aktivieren oder deaktivieren und deren Zeitpläne bearbeiten. |
| **Ansicht-Quellen** deaktivieren und Quellen **verwalten** deaktivieren | Sperren Sie den Zugriff auf alle Quellen. |

Weitere Informationen zu den verfügbaren Berechtigungen, die über die Admin Console erteilt wurden, einschließlich dieser vier Quellen, finden Sie in der Übersicht über die [Zugriffskontrolle](../access-control/home.md).

## Geschäftsbedingungen {#terms-and-conditions}

Durch die Verwendung einer der als Beta (&quot;Beta&quot;) gekennzeichneten Quellen bestätigen Sie hiermit, dass die Betaversion ***&quot;wie besehen&quot;ohne Gewährleistung jeglicher Art*** bereitgestellt wird.

Adobe ist nicht verpflichtet, die Beta-Version beizubehalten, zu korrigieren, zu aktualisieren, zu ändern, zu ändern oder anderweitig zu unterstützen. Es wird empfohlen, Vorsicht walten zu lassen und sich nicht auf die richtige Funktionsweise oder Leistung solcher Beta- und/oder Begleitmaterialien zu verlassen. Die Beta-Version wird als vertrauliche Informationen von Adobe betrachtet.

Alle &quot;Feedback&quot;(Informationen zur Betaversion, einschließlich, aber nicht beschränkt auf Probleme oder Defekte, auf die Sie bei der Verwendung der Beta-Version stoßen, Vorschläge, Verbesserungen und Empfehlungen), die Sie Adobe zur Verfügung stellen, werden Adobe hiermit zugewiesen, einschließlich aller Rechte, Titel und Interessen an und an solchen Feedback.

Senden Sie Open Feedback oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge freizugeben oder einen Fehler zu melden, eine Funktionsverbesserung zu suchen.
