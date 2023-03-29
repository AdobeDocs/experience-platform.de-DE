---
keywords: Experience Platform;Startseite;beliebte Themen;Quell-Connectoren;Quell-Connector;Quellen;Datenquellen;Datenquelle;Datenquellenverbindung
solution: Experience Platform
title: Übersicht über Quell-Connectoren
description: Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 9d6a4b5f60f7895e2c1833493926db147064f3f1
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 84%

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
   - [Adobe Audience Manager-Quellverbindung über die Benutzeroberfläche erstellen](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Übersicht über Adobe Analytics Classifications-Datenquellen](connectors/adobe-applications/classifications.md)
   - [Erstellen einer Adobe Analytics Classifications-Datenquellverbindung über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/classifications.md)
- [Übersicht über Adobe Analytics-Report Suite-Datenquellen](connectors/adobe-applications/analytics.md)
   - [Adobe Analytics-Quellverbindung über die Benutzeroberfläche erstellen](./tutorials/ui/create/adobe-applications/analytics.md)
- [Übersicht über Adobe Campaign Managed Cloud Services-Quellen](connectors/adobe-applications/campaign.md)
   - [Erstellen einer Quellverbindung zu Adobe Campaign Managed Cloud Services in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/campaign.md)
- [Übersicht über die Quellen der Adobe-Datenerfassung](connectors/adobe-applications/data-collection.md)
   - [Erstellen einer Quellverbindung für Kundenattribute in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [Übersicht über [!DNL Marketo Engage]-Quellen](connectors/adobe-applications/marketo/marketo.md)
   - [Erstellen einer  [!DNL Marketo Engage] -Quellverbindung über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Erstellen Sie eine [!DNL Marketo Engage] Quellverbindung und Datenfluss für benutzerdefinierte Aktivitätsdaten](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
- [Übersicht zu Adobe Workfront-Quellen](connectors/adobe-applications/workfront.md)
   - [Erstellen einer Workfront-Quellverbindung über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/workfront.md)

### Werbung {#advertising}

Experience Platform ermöglicht die Aufnahme von Daten aus Werbesystemen von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [Google Ads](connectors/advertising/ads.md)

### Analysen {#analytics}

Experience Platform bietet Unterstützung für die Aufnahme von Daten aus einer Analyseplattform eines Drittanbieters. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md)
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md)

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
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### Customer Success {#customer-success}

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbieter-Anwendungen für das Customer Success Management. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md)
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
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md)

### E-Commerce {#ecommerce}

Experience Platform ermöglicht die Aufnahme von Daten aus E-Commerce-Systemen von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### Lokales System {#local-system}

Experience Platform unterstützt die Erfassung von Daten aus Ihrem lokalen System. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [Lokaler Datei-Upload](connectors/local-system/local-file-upload.md)

### Marketing-Automatisierung {#marketing-automation}

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbietersystemen für die Marketing-Automatisierung. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md)
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md)
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

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

Weitere Informationen zu den verfügbaren Berechtigungen, die über Adobe-Berechtigungen gewährt werden, finden Sie unter [Zugriffssteuerung - Übersicht](../access-control/home.md).

### Attributbasierte Zugriffssteuerung

Die attributbasierte Zugriffssteuerung in Adobe Experience Platform ermöglicht Admins, den Zugriff auf bestimmte Objekte und/oder Funktionen anhand von Attributen zu steuern.

Mit der attributbasierten Zugriffssteuerung können Sie Zuordnungskonfigurationen auf Felder anwenden, für die Sie über Berechtigungen verfügen. Im Übrigen können Sie keine Daten in einen Datensatz aufnehmen, wenn Sie nicht auf alle Felder im Datensatz Zugriff haben.

#### Unterstützung für attributbasierte Zugriffskontrolle in Quellen [!BADGE Neue Funktion]

>[!TIP]
>
>Die attributbasierte Zugriffssteuerung funktioniert wie folgt: **Rollen** werden erstellt, um die Arten von Benutzern zu kategorisieren, die mit Ihrer Platform-Instanz interagieren. **Bezeichnungen** angewendet werden auf **Rollen** , um den Zugriff auf diese Rolle zu bestimmen. **Bezeichnungen** werden auch auf Ressourcen wie Schemafelder und Segmente angewendet. Damit ein Benutzer Zugriff auf bestimmte Schemafelder und Segmente haben kann, müssen diese *Rolle mit der gleichen Beschriftung, die der abgefragten Ressource zugewiesen ist*. Weitere Informationen finden Sie im Abschnitt [Handbuch zur attributbasierten Zugriffskontrolle - End-to-End](../access-control/abac/end-to-end-guide.md).

- Wenden Sie Beschriftungen auf Schemafelder an, um den Zugriff auf bestimmte Schemafelder in Ihrer Organisation zu definieren. Sobald der Zugriff auf bestimmte Schemafelder hergestellt wurde, können Benutzer nur Zuordnungen für die Felder erstellen, auf die sie Zugriff haben.
- Benutzer ohne die entsprechenden Rollen können keine Datenflüsse mit Zuordnungen erstellen oder aktualisieren, die nicht zugängliche Schemafelder beinhalten. Darüber hinaus können nicht autorisierte Benutzer vorhandene Datenflüsse mit nicht zugänglichen Schemafeldern nicht aktualisieren, löschen, aktivieren oder deaktivieren.
- Darüber hinaus muss ein Datenfluss über exakt dieselbe Schema-ID und -Version bei der Zuordnung, dem Zieldatensatz und der Zielverbindung verfügen.

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../access-control/abac/overview.md).

## Allgemeine Geschäftsbedingungen {#terms-and-conditions}

Durch Verwendung einer der als Beta („Beta“) gekennzeichneten Quellen erkennen Sie hiermit an, dass die Beta-Version ***ohne Mängelgewähr und ohne Gewährleistung jeglicher Art*** bereitgestellt wird.

Adobe ist nicht verpflichtet, die Beta-Version zu pflegen, zu korrigieren, zu aktualisieren, zu ändern oder anderweitig zu unterstützen. Es wird empfohlen, Vorsicht walten zu lassen und sich nicht auf die korrekte Funktionsweise oder Leistung solcher Beta-Versionen und/oder deren Begleitmaterialien zu verlassen. Die Beta-Version wird als vertrauliche Information von Adobe betrachtet.

Jedes „Feedback“ (Informationen zur Beta-Version, einschließlich, aber nicht beschränkt auf Probleme oder Mängel, auf die Sie bei der Verwendung der Beta-Version stoßen, Vorschläge, Verbesserungen und Empfehlungen), das Sie Adobe übermitteln, wird hiermit an Adobe übertragen, einschließlich aller Rechte, Titel und Interessen an diesem Feedback.

Senden Sie offenes Feedback oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge mitzuteilen, einen Fehler zu melden oder um eine Funktionsverbesserung zu bitten.
