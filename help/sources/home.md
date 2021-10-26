---
keywords: Experience Platform;Home;beliebte Themen;Quellschnittstellen;Quellschnittstellen;Quellen;Datenquellen;Datenquelle;Datenquelle;Datenquellenverbindung
solution: Experience Platform
title: Übersicht über Quellschnittstellen
topic-legacy: overview
description: Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: f8cecdaaab3d98c7f6542b51dc764a019b04b0b1
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 56%

---

# Übersicht über Connectoren für Datenquellen

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen unterschiedlichen Quellen innerhalb der Plattform zu sammeln und zu zentralisieren. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie ganz einfach Quellverbindungen zu verschiedenen Datenanbietern einrichten können. Diese sogenannten „Quell-Connectoren“ bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

Mit Experience Platform können Sie Daten aus unterschiedlichen Quellen an zentraler Stelle aufnehmen und auswerten, um auf diesen Erkenntnissen basierend weitere Schritte einzuleiten.

## Arten von Datenquellen

Die für die Aufnahme in Experience Platform verwendeten Datenquellen sind in folgende Kategorien unterteilt:

### Adobe-Anwendungen

Experience Platform ermöglicht die Erfassung von Daten aus anderen Anwendungen der Adobe, einschließlich Adobe Analytics und Adobe Audience Manager. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [Übersicht über den Adobe Audience Manager-Connector](connectors/adobe-applications/audience-manager.md)
- [Adobe Audience Manager-Quellverbindung in der Benutzeroberfläche erstellen](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Übersicht über die Adobe Analytics Classifications-Datenquellenverbindung](connectors/adobe-applications/classifications.md)
- [Adobe Analytics Classifications-Datenquellenverbindung in der Benutzeroberfläche erstellen](./tutorials/ui/create/adobe-applications/classifications.md)
- [Übersicht über die Adobe Analytics Report Suite Datenquellenverbindung](connectors/adobe-applications/analytics.md)
- [Adobe Analytics-Quellverbindung in der Benutzeroberfläche erstellen](./tutorials/ui/create/adobe-applications/analytics.md)
- [Quellverbindung für Kundenattribute in der Benutzeroberfläche erstellen](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] Verbindungsübersicht](connectors/adobe-applications/marketo/marketo.md)
- [Erstellen Sie eine [!DNL Marketo Engage] Quellverbindung in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/marketo.md)

### Adobe Advertising Cloud

Experience Platform unterstützt die Erfassung von Daten aus einem Drittanbieter-Werbesystem. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) Anschluss

### Cloud-Speicherplatz

Cloud-Speicher bieten eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Ingetierte Daten können als XDM-JSON, XDM-Parquet oder als Begrenzt formatiert werden. Die einzelnen Prozessschritte werden anhand der Benutzeroberfläche in den Datenquellen-Workflow integriert. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Azure Data Lake Storage Gen2] Anschluss](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] Anschluss](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] Anschluss](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] Anschluss](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] Anschluss](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] Anschluss](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] Anschluss](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP] Anschluss](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] Anschluss](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] Anschluss](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] Anschluss](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] Anschluss](connectors/cloud-storage/sftp.md)

### CRM (Customer Relationship Management)

CRM-Systeme liefern Daten, mit deren Hilfe Kundenbeziehungen gepflegt werden können, um die Kundentreue und -bindung zu fördern. Experience Platform unterstützt das Erfassen von CRM-Daten aus [!DNL Microsoft Dynamics 365] und [!DNL Salesforce]. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Microsoft Dynamics] Anschluss](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] Anschluss](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Kundenerfolg

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbieter-Anwendungen für das Customer Success Management. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Salesforce Service Cloud] Anschluss](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] Anschluss](connectors/customer-success/servicenow.md)

### Datenbank

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Amazon Redshift] Anschluss](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] Anschluss](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] Anschluss](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] Anschluss](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] Anschluss](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] Anschluss](connectors/databases/ats.md)
- [[!DNL Couchbase] Anschluss](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] Anschluss](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] Anschluss](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] Anschluss](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] Anschluss](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB] Anschluss](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server] Anschluss](connectors/databases/sql-server.md)
- [[!DNL MySQL] Anschluss](connectors/databases/mysql.md)
- [[!DNL Oracle] Anschluss](connectors/databases/oracle.md)
- [[!DNL Phoenix] Anschluss](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] Anschluss](connectors/databases/postgres.md)
- [[!DNL Snowflake] Anschluss](connectors/databases/snowflake.md)

### E-Commerce

Experience Platform unterstützt das Erfassen von Daten von einem Drittanbieter-eCommerce-System. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Lokales System

Experience Platform unterstützt das Erfassen von Daten aus Ihrem lokalen System. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [Upload einer lokalen Datei](connectors/local-system/local-file-upload.md)

### Marketing-Automatisierung

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbietersystemen für die Marketing-Automatisierung. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL HubSpot] Anschluss](connectors/marketing-automation/hubspot.md)
- [[!DNL MailChimp Campaign]](./tutorials/api/create/marketing-automation/mailchimp-campaign.md)
- [[!DNL MailChimp Members]](./tutorials/api/create/marketing-automation/mailchimp-members.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### Zahlungen

Experience Platform unterstützt die Erfassung von Daten aus einem Zahlungssystem eines Dritten. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL PayPal] Anschluss](connectors/payments/paypal.md)

### Streaming

Experience Platform unterstützt das Erfassen von Daten aus Streaming-Quellen. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL HTTP API]](connectors/streaming/http.md)

### Protokolle

Experience Platform unterstützt das Erfassen von Daten aus einem Protokollsystem eines Drittanbieters. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Generic OData] Anschluss](connectors/protocols/odata.md)

## Zugriffskontrolle für Quellen zur Datenaufnahme

Zugriffsberechtigungen für die zur Datenaufnahme verwendeten Quellen können über Adobe Admin Console verwaltet werden. Der Zugriff auf die Berechtigungen für ein bestimmtes Produktprofil erfolgt über die ihm zugehörige Registerkarte **[!UICONTROL Berechtigungen]**. Im Bereich **[!UICONTROL Berechtigungen bearbeiten]** können Sie über den Menüeintrag **[!UICONTROL Datenaufnahme]** auf die einer Quelle zugehörigen Berechtigungen zugreifen. Die Berechtigung **[!UICONTROL Quellen anzeigen]** gewährt Lesezugriff auf unter der Registerkarte **[!UICONTROL Katalog]** verfügbare Quellen sowie auf authentifizierte Quellen unter der Registerkarte **[!UICONTROL Durchsuchen]**. Mit der Berechtigung **[!UICONTROL Quellen verwalten]** dagegen wird uneingeschränkter Zugriff zum Anzeigen, Erstellen, Bearbeiten und Deaktivieren von Quellen gewährt.

Die folgende Tabelle zeigt, wie sich die Benutzeroberfläche bei verschiedenen Kombinationen dieser Berechtigungen verhält:

| Berechtigungsebene | Beschreibung |
| ---- | ----|
| **[!UICONTROL Quellen anzeigen]** aktiviert | Ermöglichen Sie schreibgeschützten Zugriff auf die Quellen in jedem Quelltyp auf der Registerkarte &quot;Katalog&quot;sowie auf die Registerkarten &quot;Durchsuchen&quot;, &quot;Konten&quot;und &quot;Datenfeldern&quot;. |
| **[!UICONTROL Quellen verwalten]** aktiviert | Gewährt zusätzlich zu in den **[!UICONTROL Quellen verwalten]** enthaltenen Berechtigungen Zugriff auf die Option **[!UICONTROL Quelle verbinden]** unter **[!UICONTROL Katalog]** sowie auf die Option **[!UICONTROL Daten auswählen]** unter **[!UICONTROL Durchsuchen]**. **[!UICONTROL Quellen verwalten]** beinhaltet außerdem die Berechtigung zum Aktivieren und Deaktivieren von **[!UICONTROL DataFlows]** sowie zur Bearbeitung der zugehörigen Zeitpläne. |
| **[!UICONTROL Quellen anzeigen]** deaktiviert und **[!UICONTROL Quellen verwalten]** deaktiviert | Sperrt den Zugriff auf alle Quellen. |

Weitere Informationen zu den über Admin Console erteilten Berechtigungen einschließlich der vier hier erläuterten Quellen finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).

## Allgemeine Geschäftsbedingungen {#terms-and-conditions}

Durch die Verwendung einer der als Beta-Beta-Beta-Quellen (&quot;Beta&quot;) gekennzeichneten Quellen bestätigen Sie hiermit, dass die Beta-Beta-Beta-Version zur Verfügung gestellt wird ***&quot;wie besehen&quot; ohne Gewährleistung jeglicher Art***.

Die Adobe ist nicht verpflichtet, die Beta zu pflegen, zu korrigieren, zu aktualisieren, zu ändern, zu ändern oder anderweitig zu unterstützen. Wir empfehlen Ihnen, Vorsicht walten zu lassen und sich nicht auf die korrekte Funktion oder Leistung solcher Beta- und/oder Begleitmaterialien zu verlassen. Die Beta gilt als vertrauliche Informationen über die Adobe.

Jegliches &quot;Feedback&quot; (Informationen über die Beta einschließlich, aber nicht beschränkt auf Probleme oder Defekte, auf die Sie bei der Nutzung der Beta, Vorschläge, Verbesserungen und Empfehlungen stoßen), das Ihnen von Ihnen der Adobe zur Verfügung gestellt wird, wird hiermit der Adobe einschließlich aller Rechte, des Eigentums und des Interesses an und auf dieses Feedback zugewiesen.

Senden Sie offenes Feedback oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge zu teilen oder einen Fehler zu melden. Suchen Sie nach einer Funktionsverbesserung.
