---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zu Experience Platform vom 11. März 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 67%

---


# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 11. März 2020**

Aktualisierungen vorhandener Funktionen in der Adobe Experience Platform:

* [!DNL Data Governance](#governance)
* [!DNL Data Ingestion](#ingestion)
* [!DNL Destinations](#destinations)
* [!DNL Identity Service](#identity)
* [!DNL Sources](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform]Mit können Firmen Daten aus mehreren Unternehmenssystemen zusammenführen, damit Marketing-Experten Kunden besser identifizieren, verstehen und binden können. [!DNL Experience Platform] umfasst eine durchgängige Data Governance-Infrastruktur, einschließlich DULE (Data Usage Labeling and Enforcement), um die ordnungsgemäße Nutzung von Daten in und bei der gemeinsamen Nutzung durch verschiedene Systeme sicherzustellen.[!DNL Platform]

Adobe Experience Platform [!DNL Data Governance] is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**Neue Funktionen**

>[!NOTE]
>
>Einige der folgenden neuen Funktionen befinden sich derzeit in der Beta-Phase und stehen nicht allen Benutzern zur Verfügung. Beta-Funktionen können sich ändern.

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatisierte Durchsetzung von Datenverwendungsrichtlinien für [!DNL Real-time Customer Data Platform] | Datennutzungsrichtlinien werden jetzt im Workflow zum Aktivieren von Daten für Ziele durchgesetzt. [!DNL Data Governance] wird auch eingebettet und durchgesetzt, wenn Änderungen vorgenommen werden, die sich auf bestehende Aktivierungen auswirken (z. B. Änderungen an den Datenbezeichnungen, Zusammenführungsrichtlinien, Segmentdefinitionen usw.). |
| Datenherkunft zur Durchsetzung | Wenn eine Datennutzungsrichtlinie in der Echtzeit-Kundendatenplattform verletzt wird, zeigt die Benutzeroberfläche eine Benachrichtigung an, die Informationen zur Datenherkunft enthält, damit der Benutzer besser versteht, warum gegen die Richtlinien verstoßen wurde und wie er den Verstoß beheben kann. |


**Bekannte Probleme**

* Keine

For more information about [!DNL Data Governance], see the [Data Governance overview](../../data-governance/home.md).

## Datenerfassung {#ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform [!DNL Data Ingestion] provides multiple alternatives for ingesting data including Batch APIs, Streaming APIs, native Adobe connectors, data integration partners, or the Adobe Experience Platform UI.

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Partielle Batch-Erfassung | Partielle Batch-Erfassung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform erfassen, während alle fehlerhaften Daten separat gestapelt werden. Zu nicht erfolgreichen Batches werden Details hinzugefügt, um zu erklären, warum sie die Validierung nicht bestanden haben. Weitere Informationen zur partiellen Batch-Erfassung finden Sie in der [Dokumentation zur partiellen Batch-Erfassung](../../ingestion/batch-ingestion/partial.md). |

**Bekannte Probleme**

* Keine

Weitere Informationen zur Erfassung von Daten in Platform finden Sie in der [Datenerfassungsdokumentation](../../ingestion/home.md).


## Ziele {#destinations}

In der [Adobe Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, für die Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie hier:

| Ziel | Beschreibung |
|--- | ---|
| Cloud-Speicher-Ziele | Adobe Real-time CDP can now deliver your segments as data files to your [!DNL Amazon S3] or SFTP cloud storage locations. Auf diese Weise können Sie Zielgruppen und deren Profilattribute über CSV- oder tabulatorgetrennte Dateien an Ihre internen Systeme senden. |
| Werbeziele | The [!DNL Google] destination card is now split into three destination cards, for the three different [!DNL Google] platforms currently supported in Adobe Real-time CDP: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Identity Service] {#identity}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint.

Adobe Experience Platform [!DNL Identity Service] helps you to gain a better view of your customer and their behavior by bridging identities across devices and systems, allowing you to deliver impactful, personal digital experiences in real-time.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbessertes privates Diagramm | Private Graph functionality has been enhanced to reduce graph generation latency from a weekly batch process to a daily refreshed graph, allowing [!DNL Identity Service] customers to access more up-to-date identity graphs and linkages. |

**Bekannte Probleme**

* Keine

For more information about [!DNL Identity Service], see the [Identity Service overview](../../identity-service/home.md).

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, damit Sie für verschiedene Datenanbieter bequem Quellverbindungen einrichten können. Diese Quellverbindungen ermöglichen Ihnen das Authentifizieren und Verbinden mit externen Speichersystemen und CRM-Diensten, das Festlegen von Zeiten für Erfassungsläufe und das Verwalten des Datendurchsatzes bei der Erfassung.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Veraltete Signale für Adobe Audience Manager-Connector | Daten auf Signalebene von Audience Manager werden nicht mehr gesendet. Beachten Sie, dass die Segmentzugehörigkeit für Eigenschaften und Segmente weiterhin enthalten ist. Infolge dieser Änderung werden keine eingehenden Datensätze mehr generiert. |
| Umbenannte Datensätze | Vom Audience Manager-Connector erstellte Datensätze erhalten aktualisierte Namen und Beschreibungen. |
| Enable [!DNL Profile] toggle in Audience Manger | [!DNL Profile] kann aktiviert oder deaktiviert werden, um DataSet zu bewerben [!DNL Real-time Customer Profile]. Die Umschaltung ist standardmäßig aktiviert. |
| Benutzeroberflächenunterstützung für Cloud-Speichersysteme | New source connector for [!DNL Azure Data Lake Storage Gen2] in the UI. |
| Benutzeroberflächenunterstützung für CRM-Systeme | New source connector for [!DNL HubSpot], [!DNL Salesforce Service Cloud], and [!DNL ServiceNow] in the UI. |
| Benutzeroberflächenunterstützung für Datenbanksysteme | New source connector for [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server], and [!DNL MySQL] in the UI. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).