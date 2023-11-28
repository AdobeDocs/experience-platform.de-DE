---
keywords: Experience Platform;Startseite;beliebte Themen;Quell-Connectoren;Quell-Connector;Quellen;Datenquellen;Datenquelle;Datenquellenverbindung
solution: Experience Platform
title: Übersicht über Quell-Connectoren
description: Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: a0616410da5cef51fdac928ecfb02f0b05a4cdb1
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 80%

---

# Übersicht über Quell-Connectoren

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Platform zu sammeln und zu zentralisieren. Der Service bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie auf einfache Weise Quellverbindungen zu verschiedenen Datenanbietern einrichten können. Diese Quell-Connectoren bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

Mit Experience Platform können Sie Daten aus unterschiedlichen Quellen an zentraler Stelle aufnehmen und auswerten, um auf diesen Erkenntnissen basierend weitere Schritte einzuleiten.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Von Adobe erstellte und von Partnern erstellte Quellen {#adobe-and-partner-built-sources}

Einige der Connectoren im Experience Platform-Quellkatalog werden von Adobe erstellt und gepflegt, während andere von Partnerunternehmen mithilfe von [Quellen-SDK](/help/sources/sources-sdk/overview.md). Ein Hinweis oben auf der Dokumentationsseite für jeden von Partnern erstellten Connector ruft ab, ob eine Quelle vom Partner erstellt und gepflegt wird. Beispiel: die [Amazon S3-Connector](/help/sources/connectors/cloud-storage/s3.md) von Adobe erstellt wird, während die Variable [RainFocus-Connector](/help/sources/connectors/analytics/rainfocus.md) wird vom RainFocus-Team erstellt und gepflegt.

Bei von Partnern erstellten und gepflegten Connectoren bedeutet dies, dass Probleme mit dem Connector möglicherweise vom Partner-Team behoben werden müssen (die Kontaktmethode ist jeweils im Hinweis auf der Dokumentationsseite angegeben). Wenden Sie sich bei Problemen mit von Adobe erstellten und gepflegten Connectoren an den Support oder den Kundendienst von Adobe.

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
- [Adobe Commerce-Quellübersicht](connectors/adobe-applications/commerce.md)
- [Übersicht über die Quellen der Adobe-Datenerfassung](connectors/adobe-applications/data-collection.md)
   - [Erstellen einer Quellverbindung für Kundenattribute in der Benutzeroberfläche](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [Übersicht über [!DNL Marketo Engage]-Quellen](connectors/adobe-applications/marketo/marketo.md)
   - [Erstellen einer  [!DNL Marketo Engage] -Quellverbindung über die Benutzeroberfläche](./tutorials/ui/create/adobe-applications/marketo.md)
   - [Erstellen Sie eine [!DNL Marketo Engage] Quellverbindung und Datenfluss für benutzerdefinierte Aktivitätsdaten](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Werbung {#advertising}

Experience Platform ermöglicht die Aufnahme von Daten aus Werbesystemen von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [Google Ads](connectors/advertising/ads.md) [!BADGE Batch]{type=Neutral}

### Analysen {#analytics}

Experience Platform bietet Unterstützung für die Aufnahme von Daten aus einer Analyseplattform eines Drittanbieters. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE Streaming]{type=Caution}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE Streaming]{type=Caution}

### Cloud-Speicherplatz {#cloud-storage}

Cloud-Speicher bieten eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Die einzelnen Prozessschritte werden mit der Benutzeroberfläche in den Quellen-Workflow integriert. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE Streaming]{type=Caution}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE Streaming]{type=Caution}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE Batch]{type=Neutral}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE Streaming]{type=Caution}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE Batch]{type=Neutral}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE Batch]{type=Neutral}

### Einverständnis und Voreinstellungen {#consent}

Experience Platform unterstützt die Aufnahme von Daten aus einer Einverständnis- und Voreinstellungs-Verwaltungsplattform von Dritten. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE Batch]{type=Neutral}

### CRM (Customer Relationship Management) {#customer-relationship-management}

CRM-Systeme liefern Daten, mit deren Hilfe Kundenbeziehungen gepflegt werden können, um die Kundentreue und -bindung zu fördern. Experience Platform unterstützt die Aufnahme von CRM-Daten aus [!DNL Microsoft Dynamics 365] und [!DNL Salesforce]. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE Batch]{type=Neutral}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE Batch]{type=Neutral}

### Customer Success {#customer-success}

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbieter-Anwendungen für das Customer Success Management. Näheres hierzu finden Sie in den folgenden Dokumenten:

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE Batch]{type=Neutral}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE Batch]{type=Neutral}

### Datenbank {#database}

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE Batch]{type=Neutral}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE Batch]{type=Neutral}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE Batch]{type=Neutral}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE Batch]{type=Neutral}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE Batch]{type=Neutral}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE Batch]{type=Neutral}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE Streaming]{type=Caution}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE Batch]{type=Neutral}

### E-Commerce {#ecommerce}

Experience Platform ermöglicht die Aufnahme von Daten aus E-Commerce-Systemen von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE Streaming]{type=Caution}

### Lokales System {#local-system}

Experience Platform unterstützt die Erfassung von Daten aus Ihrem lokalen System. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [Lokaler Datei-Upload](connectors/local-system/local-file-upload.md)

### Marketing-Automatisierung {#marketing-automation}

Experience Platform ermöglicht die Aufnahme von Daten aus Drittanbietersystemen für die Marketing-Automatisierung. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE Streaming]{type=Caution}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE Streaming]{type=Caution}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE Batch]{type=Neutral}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### Zahlungen {#payments}

Experience Platform ermöglicht die Aufnahme von Daten aus Zahlungssystemen von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE Batch]{type=Neutral}

### Streaming {#streaming}

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Quellen. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE Streaming]{type=Caution}

### Protokolle {#protocols}

Experience Platform ermöglicht die Aufnahme von Daten aus Protokollsystemen von Drittanbietern. Näheres zu den einzelnen Quell-Connectoren finden Sie in den folgenden Dokumenten:

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE Batch]{type=Neutral}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE Batch]{type=Neutral}

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

#### Unterstützung für attributbasierte Zugriffskontrolle in Quellen

>[!TIP]
>
>Die attributbasierte Zugriffssteuerung funktioniert wie folgt: **Rollen** werden erstellt, um die Arten von Benutzern zu kategorisieren, die mit Ihrer Platform-Instanz interagieren. **Bezeichnungen** angewendet werden auf **Rollen** , um den Zugriff auf diese bestimmte Rolle zu bestimmen. **Bezeichnungen** werden auch auf Ressourcen wie Schemafelder und Segmente angewendet. Damit ein Benutzer Zugriff auf bestimmte Schemafelder und Segmente haben kann, müssen diese *Rolle mit der gleichen Beschriftung, die der abgefragten Ressource zugewiesen ist*. Weitere Informationen finden Sie im Abschnitt [Handbuch zur attributbasierten Zugriffskontrolle - End-to-End](../access-control/abac/end-to-end-guide.md).

- Wenden Sie Beschriftungen auf Schemafelder an, um den Zugriff auf bestimmte Schemafelder in Ihrer Organisation zu definieren. Sobald der Zugriff auf bestimmte Schemafelder hergestellt wurde, können Benutzer nur Zuordnungen für die Felder erstellen, auf die sie Zugriff haben.
- Benutzer ohne die entsprechenden Rollen können keine Datenflüsse mit Zuordnungen erstellen oder aktualisieren, die nicht zugängliche Schemafelder beinhalten. Darüber hinaus können nicht autorisierte Benutzer vorhandene Datenflüsse mit nicht zugänglichen Schemafeldern nicht aktualisieren, löschen, aktivieren oder deaktivieren.
- Darüber hinaus muss ein Datenfluss über exakt dieselbe Schema-ID und -Version bei der Zuordnung, dem Zieldatensatz und der Zielverbindung verfügen.

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../access-control/abac/overview.md).

## Allgemeine Geschäftsbedingungen {#terms-and-conditions}

Durch Verwendung einer der als Beta („Beta“) gekennzeichneten Quellen erkennen Sie hiermit an, dass die Beta-Version ***ohne Mängelgewähr und ohne Gewährleistung jeglicher Art*** bereitgestellt wird.

Adobe ist nicht verpflichtet, die Beta-Version zu pflegen, zu korrigieren, zu aktualisieren, zu ändern oder anderweitig zu unterstützen. Es wird empfohlen, Vorsicht walten zu lassen und sich nicht auf die korrekte Funktionsweise oder Leistung solcher Beta-Versionen und/oder deren Begleitmaterialien zu verlassen. Die Beta-Version wird als vertrauliche Information von Adobe betrachtet.

Jedes „Feedback“ (Informationen zur Beta-Version, einschließlich, aber nicht beschränkt auf Probleme oder Mängel, auf die Sie bei der Verwendung der Beta-Version stoßen, Vorschläge, Verbesserungen und Empfehlungen), das Sie Adobe übermitteln, wird hiermit an Adobe übertragen, einschließlich aller Rechte, Titel und Interessen an diesem Feedback.

Senden Sie offenes Feedback oder erstellen Sie ein Support-Ticket, um Ihre Vorschläge mitzuteilen, einen Fehler zu melden oder um eine Funktionsverbesserung zu bitten.
