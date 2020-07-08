---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform vom 11. März 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 8%

---


# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 11. März 2020**

Aktualisierungen vorhandener Funktionen in der Adobe Experience Platform:

* [Data Governance](#governance)
* [Dateneinbindung](#ingestion)
* [Ziele](#destinations)
* [Identitätsdienst](#identity)
* [Quellen](#sources)

## Data Governance {#governance}

Experience Platform ermöglicht es Firmen, Daten aus mehreren Unternehmenssystemen zusammenzuführen, um Marketingexperten die Identifizierung, das Verständnis und die Interaktion mit Kunden zu erleichtern. Die Experience Platform umfasst eine durchgängige Infrastruktur zur Datenverwaltung, einschließlich Datenbenennung und -durchsetzung (DULE), um die ordnungsgemäße Verwendung der Daten innerhalb der Platform und bei der Freigabe zwischen den Systemen sicherzustellen.

Adobe Experience Platform Data Governance ist eine Reihe von Strategien und Technologien zur Verwaltung von Kundendaten und zur Gewährleistung der Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung. Es spielt eine Schlüsselrolle in der Experience Platform auf verschiedenen Ebenen, wie z.B. Katalogisierung, Datennutzungskennzeichnung, Datenzugriffsrichtlinien und Zugriffskontrolle von Daten für Marketingaktionen.

**Neue Funktionen**

>[!NOTE]
>
>Einige der folgenden neuen Funktionen befinden sich derzeit in der Betaphase und stehen nicht allen Benutzern zur Verfügung. Beta-Funktionen können geändert werden.

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatisierte Durchsetzung von Datenverwendungsrichtlinien für die Echtzeit-Platform von Kundendaten | Datenverwendungsrichtlinien werden jetzt im Arbeitsablauf zum Aktivieren von Daten in Ziele erzwungen. Die Datenverwaltung wird auch eingebettet und erzwungen, wenn Änderungen vorgenommen werden, die sich auf bestehende Aktivierungen auswirken (z. B. Änderungen an den Datenbezeichnungen, Zusammenführungsrichtlinien, Segmentdefinitionen usw.). |
| Datenleitung zur Durchsetzung | Wenn eine Datenverwendungsrichtlinie in CDP in Echtzeit verletzt wird, zeigt die Benutzeroberfläche eine Benachrichtigung an, die Informationen zur Datenreihenbildung enthält, damit der Benutzer besser verstehen kann, warum die Richtlinien verletzt wurden und was er tun kann, um die Verletzung zu beheben. |


**Bekannte Probleme**

* None

Weitere Informationen zur Datenverwaltung finden Sie in der Übersicht über die [Datenverwaltung](../../data-governance/home.md).

## Dateneinbindung {#ingestion}

Adobe Experience Platform bietet eine umfangreiche Palette an Funktionen, mit denen Sie alle Datentypen und Latenzzeiten erfassen können. Adobe Experience Platform Data Ingestion bietet mehrere Alternativen zum Erfassen von Daten, einschließlich Batch-APIs, Streaming-APIs, nativen Adobe-Connectors, Data Integration-Partnern oder der Benutzeroberfläche der Adobe Experience Platform.

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Partielle Batch-Erfassung | Partielle Stapelverarbeitung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform aufnehmen, während alle falschen Daten separat in Batches aufgenommen werden. Details zu nicht erfolgreichen Stapeln werden hinzugefügt, um zu erklären, warum sie die Validierung nicht bestanden haben. Weitere Informationen zur teilweisen Stapelverarbeitung finden Sie in der Dokumentation zur [partiellen Stapelverarbeitung](../../ingestion/batch-ingestion/partial.md). |

**Bekannte Probleme**

* None

Weitere Informationen zur Dateneinfügung in die Platform finden Sie in der [Dateneinbettungsdokumentation](../../ingestion/home.md).


## Ziele {#destinations}

In der [Adobe Echtzeit-Platform](../../rtcdp/overview.md)von Kundendaten sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten nahtlos für diese  aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, an denen Sie Ihre Adobe Experience Platformen aktivieren können. Weitere Informationen finden Sie unter:

| Ziel | Beschreibung |
|--- | ---|
| Cloud-Speicher-Ziele | Adobe Echtzeit-CDP kann Ihre Segmente jetzt als Datendateien an Ihre Amazon S3- oder SFTP-Cloud-Datenspeicherung-Standorte bereitstellen. Auf diese Weise können Sie Zielgruppen und deren Profilattribute über CSV- oder tabulatorgetrennte Dateien an Ihre internen Systeme senden. |
| Werbeziele | Die Google-Zielkarte ist jetzt in drei Zielkarten für die drei verschiedenen Google-Plattformen aufgeteilt, die derzeit in Adobe Echtzeit-CDP unterstützt werden: Google Ads, Google Ad Manager, Google Display &amp; Video 360. |

Weitere Informationen finden Sie in der Übersicht über die [Ziele](../../rtcdp/destinations/destinations-overview.md)

## Identity-Dienst {#identity}

Die Bereitstellung relevanter digitaler Erlebnisse erfordert ein vollständiges Verständnis Ihres Kunden. Dies wird schwieriger, wenn Ihre Kundendaten über verschiedene Systeme verteilt sind, sodass jeder einzelne Kunde mehrere &quot;Identitäten&quot;zu haben scheint.

Der Identitätsdienst für Adobe Experience Platformen hilft Ihnen, eine bessere Ansicht Ihres Kundenverhaltens zu erzielen, indem Identitäten zwischen Geräten und Systemen überbrückt werden, sodass Sie in Echtzeit wirkungsvolle persönliche digitale Erlebnisse bereitstellen können.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbessertes privates Diagramm | Die Funktion für private Diagramme wurde verbessert, um die Wartezeit bei der Diagrammerstellung von einem wöchentlichen Batch-Prozess auf ein täglich aktualisiertes Diagramm zu reduzieren, sodass Identitäts-Service-Kunden auf aktuellere Identitätsdiagramme und Verknüpfungen zugreifen können. |

**Bekannte Probleme**

* None

Weitere Informationen zum Identitätsdienst finden Sie in der Übersicht über den [Identitätsdienst](../../identity-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe von Platform-Diensten strukturieren, beschriften und erweitern können. Sie können Daten aus einer Vielzahl von Quellen wie Adobe-Anwendungen, Cloud-basierte Datenspeicherung, Drittanbieter-Software und Ihr CRM-System erfassen.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie ganz einfach Quellverbindungen für verschiedene Datenanbieter einrichten können. Diese Quellverbindungen ermöglichen Ihnen die Authentifizierung und Verbindung zu externen Datenspeicherung- und CRM-Diensten, die Festlegung von Zeiten für die Erfassungsausführung und die Verwaltung des Datenaufkommens.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Veraltete Signale für den Adobe Audience Manager-Anschluss | Daten auf Signalebene von Audience Manager werden nicht mehr gesendet. Beachten Sie, dass die Segmentmitgliedschaft für Eigenschaften und Segmente weiterhin einbezogen wird. Infolge dieser Änderung werden keine eingehenden Datensätze mehr generiert. |
| Umbenannte Datensätze | Von Audience Manager Connector erstellte Datensätze enthalten aktualisierte Namen und Beschreibungen. |
| Umschalten zwischen Profil und Audience Manager aktivieren | Der Umschalter für Profile kann aktiviert oder deaktiviert werden, um den Datensatz für Echtzeit-Kundendaten-Profil zu bewerben. Umschalten ist standardmäßig aktiviert. |
| Benutzeroberflächenunterstützung für Cloud-Datenspeicherung-Systeme | Neuer Quell-Connector für Azurblauer Data Lake Datenspeicherung Gen2 in der Benutzeroberfläche. |
| Benutzeroberflächenunterstützung für CRM-Systeme | Neuer Quell-Connector für HubSpot, Salesforce Service Cloud und ServiceNow in der Benutzeroberfläche. |
| Benutzeroberflächenunterstützung für Datenbanksysteme | Neuer Quell-Connector für AWS Redshift, Google BigQuery, MariaDB, Microsoft SQL Server und MySQL in der Benutzeroberfläche. |

**Bekannte Probleme**

* None

Weitere Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).