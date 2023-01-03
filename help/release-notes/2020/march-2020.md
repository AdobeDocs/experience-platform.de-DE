---
title: Adobe Experience Platform - Versionshinweise, März 2020
description: Die Versionshinweise für Adobe Experience Platform vom März 2020.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: Versionshinweise;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 68%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 11. März 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [Data Governance](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Data Governance {#governance}

[!DNL Experience Platform]In werden Daten aus verschiedensten Unternehmenssystemen in einer Weise zusammengeführt, die es Marketing-Experten ermöglicht, Kunden zu identifizieren, ein besseres Verständnis von Kunden zu gewinnen und diese gezielter anzusprechen. [!DNL Experience Platform] umfasst eine durchgängige Data Governance-Infrastruktur, um die ordnungsgemäße Verwendung der Daten in [!DNL Platform] und wenn sie zwischen Systemen freigegeben werden.

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffssteuerung für Daten bei Marketing-Aktionen.

**Neue Funktionen**

>[!NOTE]
>
> Einige der folgenden neuen Funktionen befinden sich derzeit in der Beta-Phase und stehen nicht allen Benutzern zur Verfügung. Beta-Funktionen können sich ändern.

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatisierte Durchsetzung von Datennutzungsrichtlinien für [!DNL Real-Time Customer Data Platform] | Datennutzungsrichtlinien werden jetzt im Workflow zum Aktivieren von Daten für Ziele durchgesetzt. Data Governance wird auch eingebettet und durchgesetzt, wenn Änderungen vorgenommen werden, die sich auf bestehende Aktivierungen auswirken (z. B. Änderungen an den Datenbezeichnungen, Zusammenführungsrichtlinien, Segmentdefinitionen usw.). |
| Datenherkunft zur Durchsetzung | Wenn eine Datennutzungsrichtlinie in Real-Time CDP verletzt wird, zeigt die Benutzeroberfläche eine Benachrichtigung mit Informationen zur Datenherkunft an, damit der Benutzer besser verstehen kann, warum gegen die Richtlinien verstoßen wurde und was er tun kann, um den Verstoß zu beheben. |


**Bekannte Probleme**

* Keine

Weitere Informationen zur Data Governance finden Sie in [Data Governance – Übersicht](../../data-governance/home.md).

## Datenerfassung {#ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform [!DNL Data Ingestion] bietet mehrere Alternativen zum Erfassen von Daten, einschließlich Batch-APIs, Streaming-APIs, nativen Adobe-Connectoren, Datenintegrationspartnern oder der Adobe Experience Platform-Benutzeroberfläche.

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Partielle Batch-Erfassung | Partielle Batch-Erfassung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform erfassen, während alle fehlerhaften Daten separat gestapelt werden. Zu nicht erfolgreichen Batches werden Details hinzugefügt, um zu erklären, warum sie die Validierung nicht bestanden haben. Weitere Informationen zur partiellen Batch-Erfassung finden Sie in der [Dokumentation zur partiellen Batch-Erfassung](../../ingestion/batch-ingestion/partial.md). |

**Bekannte Probleme**

* Keine

Weitere Informationen zur Erfassung von Daten in Platform finden Sie in der [Datenerfassungsdokumentation](../../ingestion/home.md).


## Ziele {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner nahtlos aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, für die Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie hier:

| Ziel | Beschreibung |
|--- | ---|
| Cloud-Speicher-Ziele | Real-Time CDP kann Ihre Segmente nun als Datendateien an Ihre [!DNL Amazon S3] oder SFTP-Cloud-Speicher. Auf diese Weise können Sie Zielgruppen und deren Profilattribute über CSV- oder tabulatorgetrennte Dateien an Ihre internen Systeme senden. |
| Werbeziele | Die [!DNL Google] Die Zielkarte ist jetzt in drei Zielkarten für die drei verschiedenen [!DNL Google] Plattformen, die derzeit in Real-Time CDP unterstützt werden: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint.

Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, sich einen besseren Überblick über Ihre Kunden und ihr Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für effektive und persönliche digitale Erlebnisse sorgen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbessertes privates Diagramm | Die Funktion für private Diagramme wurde verbessert, um die Latenz bei der Diagrammgenerierung von einem wöchentlichen Batch-Prozess auf ein täglich aktualisiertes Diagramm zu reduzieren, sodass [!DNL Identity Service] -Kunden, um auf aktuellere Identitätsdiagramme und Links zuzugreifen. |

**Bekannte Probleme**

* Keine

Weitere Informationen finden Sie unter [!DNL Identity Service], siehe [Identity Service - Übersicht](../../identity-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten strukturieren, beschriften und erweitern, indem es [!DNL Platform] Dienste. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Veraltete Signale für Adobe Audience Manager-Connector | Daten auf Signalebene von Audience Manager werden nicht mehr gesendet. Beachten Sie, dass die Segmentzugehörigkeit für Eigenschaften und Segmente weiterhin enthalten ist. Infolge dieser Änderung werden keine eingehenden Datensätze mehr generiert. |
| Umbenannte Datensätze | Vom Audience Manager-Connector erstellte Datensätze erhalten aktualisierte Namen und Beschreibungen. |
| Aktivieren [!DNL Profile] Umschalten in Audience Manager | [!DNL Profile] Umschalten kann aktiviert oder deaktiviert werden, um den Datensatz zu bewerben [!DNL Real-Time Customer Profile]. Die Umschaltung ist standardmäßig aktiviert. |
| Unterstützung für Cloud-Speicher via Benutzeroberfläche | Neuer Quell-Connector für [!DNL Azure Data Lake Storage Gen2] in der Benutzeroberfläche. |
| Benutzeroberflächenunterstützung für CRM-Systeme | Neuer Quell-Connector für [!DNL HubSpot], [!DNL Salesforce Service Cloud]und [!DNL ServiceNow] in der Benutzeroberfläche. |
| Benutzeroberflächenunterstützung für Datenbanksysteme | Neuer Quell-Connector für [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server]und [!DNL MySQL] in der Benutzeroberfläche. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
