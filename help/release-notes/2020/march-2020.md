---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zu Experience Platform vom 11. März 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: Versionshinweise;
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 65%

---


# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 11. März 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform]In werden Daten aus verschiedensten Unternehmenssystemen in einer Weise zusammengeführt, die es Marketing-Experten ermöglicht, Kunden zu identifizieren, ein besseres Verständnis von Kunden zu gewinnen und diese gezielter anzusprechen. [!DNL Experience Platform] umfasst eine End-to-End-Infrastruktur zur Datenverwaltung, um die ordnungsgemäße Verwendung von Daten innerhalb  [!DNL Platform] und bei der Freigabe zwischen Systemen sicherzustellen.

Adobe Experience Platform [!DNL Data Governance] ist eine Reihe von Strategien und Technologien zur Verwaltung von Kundendaten und zur Gewährleistung der Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung. Es spielt eine Schlüsselrolle innerhalb von [!DNL Experience Platform] auf verschiedenen Ebenen, einschließlich Katalogisierung, Datenbindung, Datenbeschriftung, Datenzugriffsrichtlinien und Zugriffskontrolle von Daten für Marketingaktionen.

**Neue Funktionen**

>[!NOTE]
>
> Einige der folgenden neuen Funktionen befinden sich derzeit in der Beta-Phase und stehen nicht allen Benutzern zur Verfügung. Beta-Funktionen können sich ändern.

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatisierte Durchsetzung von Datenverwendungsrichtlinien für [!DNL Real-time Customer Data Platform] | Datennutzungsrichtlinien werden jetzt im Workflow zum Aktivieren von Daten für Ziele durchgesetzt. [!DNL Data Governance] wird auch eingebettet und durchgesetzt, wenn Änderungen vorgenommen werden, die sich auf bestehende Aktivierungen auswirken (z. B. Änderungen an den Datenbezeichnungen, Zusammenführungsrichtlinien, Segmentdefinitionen usw.). |
| Datenherkunft zur Durchsetzung | Wenn eine Datennutzungsrichtlinie in der Echtzeit-Kundendatenplattform verletzt wird, zeigt die Benutzeroberfläche eine Benachrichtigung an, die Informationen zur Datenherkunft enthält, damit der Benutzer besser versteht, warum gegen die Richtlinien verstoßen wurde und wie er den Verstoß beheben kann. |


**Bekannte Probleme**

* Keine

Weitere Informationen zu [!DNL Data Governance] finden Sie unter [Übersicht über die Datenverwaltung](../../data-governance/home.md).

## Datenaufnahme {#ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform [!DNL Data Ingestion] bietet mehrere Alternativen zum Erfassen von Daten, einschließlich Batch-APIs, Streaming-APIs, nativen Adoben-Connectors, Data Integration-Partnern oder der Adobe Experience Platform-Benutzeroberfläche.

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Partielle Batch-Erfassung | Partielle Batch-Erfassung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform erfassen, während alle fehlerhaften Daten separat gestapelt werden. Zu nicht erfolgreichen Batches werden Details hinzugefügt, um zu erklären, warum sie die Validierung nicht bestanden haben. Weitere Informationen zur partiellen Batch-Erfassung finden Sie in der [Dokumentation zur partiellen Batch-Erfassung](../../ingestion/batch-ingestion/partial.md). |

**Bekannte Probleme**

* Keine

Weitere Informationen zur Erfassung von Daten in Platform finden Sie in der [Datenerfassungsdokumentation](../../ingestion/home.md).


## Ziele {#destinations}

In der [ Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, für die Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie hier:

| Ziel | Beschreibung |
|--- | ---|
| Cloud-Speicher-Ziele | Echtzeit-CDP kann Ihre Segmente jetzt als Datendateien an Ihre [!DNL Amazon S3]- oder SFTP-Cloud-Datenspeicherung-Speicherorte senden. Auf diese Weise können Sie Zielgruppen und deren Profilattribute über CSV- oder tabulatorgetrennte Dateien an Ihre internen Systeme senden. |
| Werbeziele | Die [!DNL Google]-Zielkarte ist jetzt in drei Zielkarten aufgeteilt, für die drei verschiedenen [!DNL Google]-Plattformen, die derzeit in Echtzeit-CDP unterstützt werden: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] Anzeigen und Video 360. |

Weitere Informationen finden Sie in [Ziele – Übersicht](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint.

Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, eine bessere Ansicht Ihres Kundenverhaltens zu erzielen, indem Identitäten zwischen Geräten und Systemen überbrückt werden, sodass Sie in Echtzeit wirkungsvolle persönliche digitale Erlebnisse bereitstellen können.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbessertes privates Diagramm | Die Funktion &quot;Private Graph&quot;wurde verbessert, um die Wartezeit bei der Diagrammerstellung von einem wöchentlichen Batch-Prozess auf ein täglich aktualisiertes Diagramm zu reduzieren, sodass [!DNL Identity Service]-Kunden auf aktuellere Identitätsdiagramme und Verknüpfungen zugreifen können. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu [!DNL Identity Service] finden Sie unter [Übersicht über den Identitätsdienst](../../identity-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe der [!DNL Platform]-Dienste strukturieren, beschriften und erweitern können. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Veraltete Signale für Adobe Audience Manager-Connector | Daten auf Signalebene von Audience Manager werden nicht mehr gesendet. Beachten Sie, dass die Segmentzugehörigkeit für Eigenschaften und Segmente weiterhin enthalten ist. Infolge dieser Änderung werden keine eingehenden Datensätze mehr generiert. |
| Umbenannte Datensätze | Vom Audience Manager-Connector erstellte Datensätze erhalten aktualisierte Namen und Beschreibungen. |
| Umschalten in Audience Manager aktivieren[!DNL Profile] | [!DNL Profile] kann aktiviert oder deaktiviert werden, um DataSet zu bewerben  [!DNL Real-time Customer Profile]. Die Umschaltung ist standardmäßig aktiviert. |
| Unterstützung für Cloud-Speicher via Benutzeroberfläche | Neuer Quellanschluss für [!DNL Azure Data Lake Storage Gen2] in der Benutzeroberfläche. |
| Benutzeroberflächenunterstützung für CRM-Systeme | Neuer Quellanschluss für [!DNL HubSpot], [!DNL Salesforce Service Cloud] und [!DNL ServiceNow] in der Benutzeroberfläche. |
| Benutzeroberflächenunterstützung für Datenbanksysteme | Neuer Quellanschluss für [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server] und [!DNL MySQL] in der Benutzeroberfläche. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).