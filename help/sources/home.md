---
keywords: Experience Platform; Startseite; beliebte Themen; Quell-Connectoren; Quell-Connector; Quellen; Datenquellen; Datenquelle; Datenquellenverbindung
solution: Experience Platform
title: Übersicht über Quell-Connectoren
topic-legacy: overview
description: Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 0154891cf2c68a38c08b9fe44251ec13325a7366
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 56%

---

# Übersicht über Connectoren für Datenquellen

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Platform zu sammeln und zu zentralisieren. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie auf einfache Weise Quellverbindungen zu verschiedenen Datenanbietern einrichten können. Diese sogenannten „Quell-Connectoren“ bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

Mit Experience Platform können Sie Daten aus unterschiedlichen Quellen an zentraler Stelle aufnehmen und auswerten, um auf diesen Erkenntnissen basierend weitere Schritte einzuleiten.

## Arten von Datenquellen

Die für die Aufnahme in Experience Platform verwendeten Datenquellen sind in folgende Kategorien unterteilt:

### Adobe-Anwendungen

Experience Platform ermöglicht die Aufnahme von Daten aus anderen Adobe Apps, einschließlich Adobe Analytics und Adobe Audience Manager. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [Übersicht über den Adobe Audience Manager-Connector](connectors/adobe-applications/audience-manager.md)
- [Erstellen einer Adobe Audience Manager-Quellverbindung in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics Classifications Übersicht über die Datenquellenverbindung](connectors/adobe-applications/classifications.md)
- [Erstellen einer Datenquellenverbindung aus Adobe Analytics Classifications in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/classifications.md)
- [Übersicht über die Datenquellenverbindung der Adobe Analytics Report Suite](connectors/adobe-applications/analytics.md)
- [Erstellen einer Adobe Analytics-Quellverbindung in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/analytics.md)
- [Erstellen einer Quellverbindung für Kundenattribute in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] Connector - Übersicht](connectors/adobe-applications/marketo/marketo.md)
- [Erstellen Sie eine [!DNL Marketo Engage] Quellverbindung in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/marketo.md)

### Adobe Advertising

Experience Platform unterstützt die Aufnahme von Daten aus einem Drittanbieter-Werbe-System. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) Connector

### Cloud-Speicherplatz

Cloud-Speicher bieten eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON-, XDM Parquet- oder als Trennzeichen formatiert werden. Die einzelnen Prozessschritte werden anhand der Benutzeroberfläche in den Datenquellen-Workflow integriert. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Azure Data Lake Storage Gen2] Connector](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] Connector](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] Connector](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] Connector](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] Connector](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] Connector](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] Connector](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP] Connector](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] Connector](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] Connector](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] Connector](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] Connector](connectors/cloud-storage/sftp.md)

### CRM (Customer Relationship Management)

CRM-Systeme liefern Daten, mit deren Hilfe Kundenbeziehungen gepflegt werden können, um die Kundentreue und -bindung zu fördern. Experience Platform unterstützt die Aufnahme von CRM-Daten aus [!DNL Microsoft Dynamics 365] und [!DNL Salesforce]. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Microsoft Dynamics] Connector](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] Connector](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Kundenerfolg

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbieter-Anwendungen für das Customer Success Management. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Salesforce Service Cloud] Connector](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] Connector](connectors/customer-success/servicenow.md)

### Datenbank

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Amazon Redshift] Connector](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] Connector](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] Connector](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] Connector](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] Connector](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] Connector](connectors/databases/ats.md)
- [[!DNL Couchbase] Connector](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] Connector](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] Connector](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] Connector](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] Connector](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB] Connector](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server] Connector](connectors/databases/sql-server.md)
- [[!DNL MySQL] Connector](connectors/databases/mysql.md)
- [[!DNL Oracle] Connector](connectors/databases/oracle.md)
- [[!DNL Phoenix] Connector](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] Connector](connectors/databases/postgres.md)
- [[!DNL Snowflake] Connector](connectors/databases/snowflake.md)

### E-Commerce

Experience Platform unterstützt die Aufnahme von Daten aus einem Drittanbieter-E-Commerce-System. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Lokales System

Experience Platform unterstützt die Erfassung von Daten aus Ihrem lokalen System. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [Lokaler Datei-Upload](connectors/local-system/local-file-upload.md)

### Marketing-Automatisierung

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbietersystemen für die Marketing-Automatisierung. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL MailChimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### Zahlungen

Experience Platform unterstützt die Erfassung von Daten aus einem Zahlungssystem von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL PayPal] Connector](connectors/payments/paypal.md)

### Streaming

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Quellen. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protokolle

Experience Platform unterstützt die Aufnahme von Daten aus einem Drittanbieterprotokollsystem. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## Zugriffskontrolle für Quellen zur Datenaufnahme

Zugriffsberechtigungen für die zur Datenaufnahme verwendeten Quellen können über Adobe Admin Console verwaltet werden. Der Zugriff auf die Berechtigungen für ein bestimmtes Produktprofil erfolgt über die ihm zugehörige Registerkarte **[!UICONTROL Berechtigungen]**. Im Bereich **[!UICONTROL Berechtigungen bearbeiten]** können Sie über den Menüeintrag **[!UICONTROL Datenaufnahme]** auf die einer Quelle zugehörigen Berechtigungen zugreifen. Die Berechtigung **[!UICONTROL Quellen anzeigen]** gewährt Lesezugriff auf unter der Registerkarte **[!UICONTROL Katalog]** verfügbare Quellen sowie auf authentifizierte Quellen unter der Registerkarte **[!UICONTROL Durchsuchen]**. Mit der Berechtigung **[!UICONTROL Quellen verwalten]** dagegen wird uneingeschränkter Zugriff zum Anzeigen, Erstellen, Bearbeiten und Deaktivieren von Quellen gewährt.

Die folgende Tabelle zeigt, wie sich die Benutzeroberfläche bei verschiedenen Kombinationen dieser Berechtigungen verhält:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **[!UICONTROL Quellen anzeigen]** aktiviert | Gewähren Sie schreibgeschützten Zugriff auf die Quellen in den einzelnen Quelltypen auf der Registerkarte Katalog sowie auf die Registerkarten Durchsuchen, Konten und Datenfluss . |
| **[!UICONTROL Quellen verwalten]** aktiviert | Gewährt zusätzlich zu in den **[!UICONTROL Quellen verwalten]** enthaltenen Berechtigungen Zugriff auf die Option **[!UICONTROL Quelle verbinden]** unter **[!UICONTROL Katalog]** sowie auf die Option **[!UICONTROL Daten auswählen]** unter **[!UICONTROL Durchsuchen]**. **[!UICONTROL Quellen verwalten]** beinhaltet außerdem die Berechtigung zum Aktivieren und Deaktivieren von **[!UICONTROL DataFlows]** sowie zur Bearbeitung der zugehörigen Zeitpläne. |
| **[!UICONTROL Quellen anzeigen]** deaktiviert und **[!UICONTROL Quellen verwalten]** deaktiviert | Sperrt den Zugriff auf alle Quellen. |

Weitere Informationen zu den über Admin Console erteilten Berechtigungen einschließlich der vier hier erläuterten Quellen finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).

## Allgemeine Geschäftsbedingungen {#terms-and-conditions}

Durch Verwendung einer der als Beta (&quot;Beta&quot;) gekennzeichneten Quellen erkennen Sie hiermit an, dass die Beta-Version bereitgestellt wird. ***&quot;unverändert&quot;ohne Gewährleistung jeglicher Art***.

Die Adobe ist nicht verpflichtet, die Beta zu pflegen, zu korrigieren, zu aktualisieren, zu ändern, zu ändern oder anderweitig zu unterstützen. Es wird empfohlen, Vorsicht walten zu lassen und sich nicht auf die korrekte Funktionsweise oder Leistung solcher Beta- und/oder Begleitmaterialien zu verlassen. Die Beta wird als vertrauliche Informationen über die Adobe betrachtet.

Jedes &quot;Feedback&quot;(Informationen zur Beta, einschließlich, aber nicht beschränkt auf Probleme oder Mängel, auf die Sie bei der Verwendung der Beta, Vorschläge, Verbesserungen und Empfehlungen stoßen), das von Ihnen an Adobe bereitgestellt wird, wird hiermit der Adobe zugewiesen, einschließlich aller Rechte, Titel und Interessen an und an diesem Feedback.

Senden Sie Feedback öffnen oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge zu teilen oder einen Fehler zu melden, oder suchen Sie nach einer Funktionsverbesserung.
