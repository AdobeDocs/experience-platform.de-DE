---
title: Adobe Experience Platform – Versionshinweise März 2020
description: Versionshinweise März 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: Versionshinweise;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 61%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Donnerstag, 11. März 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [Data Governance](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## Data Governance {#governance}

[!DNL Experience Platform] können Unternehmen Daten aus verschiedenen Unternehmenssystemen zusammenführen, damit Marketing-Experten Kunden besser identifizieren, verstehen und ansprechen können. [!DNL Experience Platform] umfasst eine End-to-End-Data-Governance-Infrastruktur, die eine ordnungsgemäße Verwendung von Daten innerhalb von [!DNL Experience Platform] und bei der gemeinsamen Nutzung durch Systeme sicherstellt.

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffssteuerung für Daten bei Marketing-Aktionen.

**Neue Funktionen**

>[!NOTE]
>
>Einige der folgenden neuen Funktionen befinden sich derzeit in der Beta-Phase und stehen nicht allen Benutzern zur Verfügung. Beta-Funktionen können sich ändern.

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatisierte Durchsetzung von Datennutzungsrichtlinien für [!DNL Real-Time Customer Data Platform] | Datennutzungsrichtlinien werden jetzt im Workflow zum Aktivieren von Daten für Ziele durchgesetzt. Data Governance wird auch eingebettet und durchgesetzt, wenn Änderungen vorgenommen werden, die sich auf bestehende Aktivierungen auswirken (z. B. Änderungen an den Datenbezeichnungen, Zusammenführungsrichtlinien, Segmentdefinitionen usw.). |
| Datenherkunft zur Durchsetzung | Wenn eine Datennutzungsrichtlinie in Real-Time CDP verletzt wird, zeigt die Benutzeroberfläche eine Benachrichtigung an, die Informationen zur Datenherkunft enthält, damit Benutzende besser verstehen können, warum die Richtlinien verletzt wurden und was sie tun können, um den Verstoß zu beheben. |


**Bekannte Probleme**

* Keine

Weitere Informationen zur Data Governance finden Sie in [Data Governance – Übersicht](../../data-governance/home.md).

## Datenerfassung {#ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform [!DNL Data Ingestion] bietet mehrere Alternativen für die Aufnahme von Daten, einschließlich Batch-APIs, Streaming-APIs, nativer Adobe-Connectoren, Datenintegrationspartnern oder der Adobe Experience Platform-Benutzeroberfläche.

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Partielle Batch-Erfassung | Partielle Batch-Erfassung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform erfassen, während alle fehlerhaften Daten separat gestapelt werden. Zu nicht erfolgreichen Batches werden Details hinzugefügt, um zu erklären, warum sie die Validierung nicht bestanden haben. Weitere Informationen zur partiellen Batch-Erfassung finden Sie in der [Dokumentation zur partiellen Batch-Erfassung](../../ingestion/batch-ingestion/partial.md). |

**Bekannte Probleme**

* Keine

Weitere Informationen zur Aufnahme von Daten in Experience Platform finden Sie in der [Datenerfassungsdokumentation](../../ingestion/home.md).


## Ziele {#destinations}

In [Real-Time Customer Data Platform](../../rtcdp/overview.md) sind Ziele vorgefertigte Integrationen mit Zielplattformen, die Daten nahtlos für diese Partner aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, für die Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie hier:

| Ziel | Beschreibung |
|--- | ---|
| Cloud-Speicher-Ziele | Real-Time CDP kann Ihre Segmente nun als Datendateien an Ihre [!DNL Amazon S3]- oder SFTP-Cloud-Speicherorte senden. Auf diese Weise können Sie Zielgruppen und deren Profilattribute über CSV- oder tabulatorgetrennte Dateien an Ihre internen Systeme senden. |
| Werbeziele | Die [!DNL Google] Zielkarte ist jetzt in drei Zielkarten für die drei verschiedenen [!DNL Google] aufgeteilt, die derzeit in Real-Time CDP unterstützt werden: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Display &amp; Video 360. |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihrer Kundinnen und Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint.

Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, sich einen besseren Überblick über Ihre Kunden und ihr Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für effektive und persönliche digitale Erlebnisse sorgen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbessertes privates Diagramm | Die Funktion für private Diagramme wurde verbessert, um die Graph-Generierungslatenz von einem wöchentlichen Batch-Prozess auf ein täglich aktualisiertes Diagramm zu reduzieren, sodass [!DNL Identity Service] Kunden auf aktuellere Identitätsdiagramme und Verknüpfungen zugreifen können. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu [!DNL Identity Service] finden Sie unter [Identity Service - Übersicht](../../identity-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Veraltete Signale für Adobe Audience Manager-Connector | Daten auf Signalebene von Audience Manager werden nicht mehr gesendet. Beachten Sie, dass die Segmentzugehörigkeit für Merkmale und Segmente weiterhin enthalten ist. Infolge dieser Änderung werden keine eingehenden Datensätze mehr generiert. |
| Umbenannte Datensätze | Vom Audience Manager-Connector erstellte Datensätze erhalten aktualisierte Namen und Beschreibungen. |
| Aktivieren [!DNL Profile] Umschalters in Audience Manager | [!DNL Profile] Umschalter kann aktiviert oder deaktiviert werden, um einen Datensatz zu [!DNL Real-Time Customer Profile] hochzustufen. Die Umschaltung ist standardmäßig aktiviert. |
| Unterstützung für Cloud-Speicher via Benutzeroberfläche | Neuer Quell-Connector für [!DNL Azure Data Lake Storage Gen2] in der Benutzeroberfläche. |
| Benutzeroberflächenunterstützung für CRM-Systeme | Neuer Quell-Connector für [!DNL HubSpot], [!DNL Salesforce Service Cloud] und [!DNL ServiceNow] in der Benutzeroberfläche. |
| Benutzeroberflächenunterstützung für Datenbanksysteme | Neuer Quell-Connector für [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] und [!DNL MySQL] in der Benutzeroberfläche. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
