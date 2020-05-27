---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über Adobe Experience Platform-Quellschnittstellen
topic: overview
translation-type: tm+mt
source-git-commit: 22425c33e39cf788eec6fd0a54f65fb89fdaff4f
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---


# Übersicht über die Quellenanschlüsse

Mit Adobe Experience Platform können Daten aus externen Quellen erfasst werden, während Sie gleichzeitig die Möglichkeit haben, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu beschriften und zu verbessern. Sie können Daten aus verschiedenen Quellen wie Adobe-Anwendungen, Cloud-basierte Datenspeicherung, Datenbanken und vielen anderen Quellen erfassen.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie Quellverbindungen zu verschiedenen Datenanbietern einfach einrichten können. Diese Quellverbindungen ermöglichen es Ihnen, Ihre Drittanbietersysteme zu authentifizieren, Zeiten für die Erfassung festzulegen und den Datendurchsatz zu verwalten.

Mit Experience Platform können Sie Daten, die Sie aus unterschiedlichen Quellen erfassen, zentralisieren und die dabei gewonnenen Erkenntnisse nutzen, um mehr zu tun.

## Arten von Quellen

Quellen in Experience Platform sind in die folgenden Kategorien gruppiert:

### Adobe-Programme

Mit Experience Platform können Daten aus anderen Adobe-Anwendungen, einschließlich Adobe Analytics, Adobe Audience Manager und Experience Platform Launch, erfasst werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über Adobe Audience Manager Connector](connectors/adobe-applications/audience-manager.md)
- [Erstellen eines Adobe Audience Manager-Quellconnectors in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Übersicht über Adobe Analytics-Datenschnittstellen](connectors/adobe-applications/analytics.md)
- [Erstellen eines Adobe Analytics-Quell-Connectors in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/analytics.md)
- [Erstellen eines Quell-Connectors für Kundenattribute in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### Werbung

Experience Platform unterstützt die Erfassung von Daten aus einem Drittanbieteranzeigesystem. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [Google AdWords Connector](connectors/advertising/ads.md)

### Cloud-Speicherplatz

Cloud-Datenspeicherung-Quellen können Ihre eigenen Daten in die Plattform übertragen, ohne dass Sie sie herunterladen, formatieren oder hochladen müssen. Ingetierte Daten können als XDM-JSON-, XDM-Parkett oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird über die Benutzeroberfläche in den Sources-Workflow integriert. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Datenspeicherung Gen2-Stecker für den Azurblau-Data-See](connectors/cloud-storage/adls-gen2.md)
- [Azurblauch und Amazon S3-Stecker](connectors/cloud-storage/blob-s3.md)
- [Amazon Kinesis Connector](connectors/cloud-storage/kinesis.md)
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

Experience Platform unterstützt das Erfassen von Daten aus einer Datenbank eines Drittanbieters. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [Amazon Redshift Connector](connectors/databases/redshift.md)
- [Apache Hive auf der Azurblauen HDInsights-Steckverbindung](connectors/databases/hive.md)
- [Apache Spark auf dem Azurblauen HDInsights-Connector](connectors/databases/spark.md)
- [Blue Data Explorer-Anschluss](connectors/databases/data-explorer.md)
- [Blue-Synapse-Analytics-Anschluss](connectors/databases/synapse-analytics.md)
- [Datenspeicherung-Stecker](connectors/databases/ats.md)
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

Experience Platform unterstützt das Erfassen von Daten aus einem Protokollsystem eines Drittanbieters. Weitere Informationen zu bestimmten Quellschnittstellen finden Sie in den folgenden Dokumenten:

- [Generischer OData Connector](connectors/protocols/odata.md)

## Zugriffskontrolle für Quellen bei der Datenerfassung

Berechtigungen für Quellen in der Datenerfassung können in der Adobe Admin-Konsole verwaltet werden. Sie können auf Berechtigungen über die Registerkarte &quot; *Berechtigungen* &quot;in einem bestimmten Profil zugreifen. Über den Menüeintrag &quot; **Berechtigungen** bearbeiten&quot;können Sie über den Eintrag im Menü &quot; *Dateneingabe* &quot;auf die Berechtigungen für Quellen zugreifen. Die Berechtigung &quot; **Ansichten-Quellen** &quot;gewährt schreibgeschützten Zugriff auf verfügbare Quellen auf der Registerkarte &quot; *Katalog* &quot;und auf authentifizierte Quellen auf der Registerkarte &quot; *Durchsuchen* &quot;. Die Berechtigung &quot;Quellen **verwalten** &quot;gewährt uneingeschränkten Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen.

Die folgende Tabelle zeigt, wie sich die Benutzeroberfläche auf der Grundlage verschiedener Kombinationen dieser Berechtigungen verhält:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **Ansicht-Quellen** auf | Gewähren Sie schreibgeschützten Zugriff auf Quellen in jedem Quelltyp auf der Registerkarte &quot; *Katalog* &quot;sowie auf die Registerkarten &quot; *Durchsuchen*&quot;, &quot; *Konten*&quot;und &quot; *DataFlow* &quot;. |
| **Quellen** verwalten unter | Gewährt zusätzlich zu den Funktionen, die in den **Ansichten-Quellen** enthalten sind, Zugriff auf die Option &quot; *Verbindungsquelle* &quot;im *Katalog* und auf die Option &quot;Daten ** auswählen&quot;in *Durchsuchen*. **Mit Quellen** verwalten können Sie auch *DataFlows* aktivieren oder deaktivieren und deren Zeitpläne bearbeiten. |
| **Ansicht-Quellen** deaktivieren und Quellen **verwalten** deaktivieren | Sperren Sie den Zugriff auf alle Quellen. |

Weitere Informationen zu den verfügbaren Berechtigungen, die über die Admin-Konsole erteilt wurden, einschließlich dieser vier Quellen, finden Sie in der Übersicht über die [Zugriffskontrolle](../access-control/home.md).
