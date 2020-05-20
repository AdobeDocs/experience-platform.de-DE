---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform vom 11. März 2020
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 8%

---


# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 11. März 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [Data Governance](#governance)
* [Dateneinbindung](#ingestion)
* [Ziele](#destinations)
* [Identitätsdienst](#identity)
* [Quellen](#sources)

## Data Governance {#governance}

Mit der Experience Platform können Firmen Daten aus mehreren Unternehmenssystemen zusammenführen, um Marketingexperten die Möglichkeit zu geben, Kunden zu identifizieren, zu verstehen und zu binden. Die Experience Platform umfasst eine End-to-End-Infrastruktur für die Datenverwaltung, einschließlich Datennutzungskennzeichnung und -durchsetzung (DULE), um die ordnungsgemäße Verwendung der Daten innerhalb der Plattform und bei der Freigabe zwischen Systemen sicherzustellen.

Adobe Experience Platform Data Governance ist eine Reihe von Strategien und Technologien zur Verwaltung von Kundendaten und zur Gewährleistung der Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung. Es spielt eine Schlüsselrolle in der Experience Platform auf verschiedenen Ebenen, wie z.B. Katalogisierung, Datennutzungsbeschriftung, Datenzugriffsrichtlinien und Zugriffskontrolle von Daten für Marketingaktionen.

**Neue Funktionen**

>[!NOTE] Einige der folgenden neuen Funktionen befinden sich derzeit in der Betaphase und stehen nicht allen Benutzern zur Verfügung. Beta-Funktionen können geändert werden.

| Funktion | Beschreibung |
| ------- | ----------- |
| Automatisierte Durchsetzung von Datenverwendungsrichtlinien für die Echtzeit-Kundendatenplattform | Datenverwendungsrichtlinien werden jetzt im Arbeitsablauf zum Aktivieren von Daten in Ziele erzwungen. Die Datenverwaltung wird auch eingebettet und erzwungen, wenn Änderungen vorgenommen werden, die sich auf bestehende Aktivierungen auswirken (z. B. Änderungen an den Datenbezeichnungen, Zusammenführungsrichtlinien, Segmentdefinitionen usw.). |
| Datenleitung zur Durchsetzung | Wenn eine Datenverwendungsrichtlinie in CDP in Echtzeit verletzt wird, zeigt die Benutzeroberfläche eine Benachrichtigung an, die Informationen zur Datenreihenbildung enthält, damit der Benutzer besser verstehen kann, warum die Richtlinien verletzt wurden und was er tun kann, um die Verletzung zu beheben. |


**Bekannte Probleme**

* Keine

Weitere Informationen zur Datenverwaltung finden Sie in der Übersicht über die [Datenverwaltung](../../data-governance/home.md).

## Dateneinbindung {#ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform Data Ingestion bietet mehrere Alternativen zum Erfassen von Daten, einschließlich Batch-APIs, Streaming-APIs, nativen Adobe-Connectors, Data Integration-Partnern oder der Benutzeroberfläche der Adobe Experience Platform.

**Neue Funktionen**

| Funktion | Beschreibung |
|------- | -----------|
| Partielle Batch-Erfassung | Partielle Stapelverarbeitung ist die Fähigkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen. Mit dieser Funktion können Benutzer alle korrekten Daten erfolgreich in Adobe Experience Platform erfassen, während alle ihre falschen Daten separat gestapelt werden. Details zu nicht erfolgreichen Stapeln werden hinzugefügt, um zu erklären, warum sie die Validierung nicht bestanden haben. Weitere Informationen zur teilweisen Stapelverarbeitung finden Sie in der Dokumentation zur [partiellen Stapelverarbeitung](../../ingestion/batch-ingestion/partial.md). |

**Bekannte Probleme**

* Keine

Weitere Informationen zum Einbinden von Daten in die Plattform finden Sie in der [Dateneinbettungsdokumentation](../../ingestion/home.md).


## Ziele {#destinations}

In der [Adobe Echtzeit-Kundendatenplattform](../../rtcdp/overview.md)sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten nahtlos an diese Partner aktivieren.

**Neue Ziele**

Es stehen neue Ziele zur Verfügung, mit denen Sie Ihre Adobe Experience Platform-Daten aktivieren können. Weitere Informationen finden Sie unter:

| Ziel | Beschreibung |
|--- | ---|
| Cloud-Speicher-Ziele | Adobe Echtzeit-CDP kann Ihre Segmente jetzt als Datendateien an Ihre Amazon S3- oder SFTP-Cloud-Datenspeicherung-Standorte bereitstellen. Auf diese Weise können Sie Zielgruppen und deren Profilattribute über CSV- oder tabulatorgetrennte Dateien an Ihre internen Systeme senden. |
| Werbeziele | Die Google-Zielkarte ist jetzt in drei Zielkarten für die drei verschiedenen Google-Plattformen aufgeteilt, die derzeit in Adobe Echtzeit-CDP unterstützt werden: Google Ads, Google Ad Manager, Google Display &amp; Video 360. |

Weitere Informationen finden Sie in der Übersicht über die [Ziele](../../rtcdp/destinations/destinations-overview.md)

## Identitätsdienst {#identity}

Die Bereitstellung relevanter digitaler Erlebnisse erfordert ein vollständiges Verständnis Ihres Kunden. Dies wird schwieriger, wenn Ihre Kundendaten über verschiedene Systeme verteilt sind, sodass jeder einzelne Kunde mehrere &quot;Identitäten&quot;zu haben scheint.

Der Identitätsdienst für Adobe Experience Platform hilft Ihnen, eine bessere Ansicht Ihres Kundenverhaltens und seines Verhaltens zu erzielen, indem Identitäten geräteübergreifend und systemübergreifend überbrückt werden. So können Sie wirkungsvolle persönliche digitale Erlebnisse in Echtzeit bereitstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbessertes privates Diagramm | Die Funktion für private Diagramme wurde verbessert, um die Wartezeit bei der Diagrammerstellung von einem wöchentlichen Batch-Prozess auf ein täglich aktualisiertes Diagramm zu reduzieren, sodass Identitäts-Service-Kunden auf aktuellere Identitätsdiagramme und Verknüpfungen zugreifen können. |

**Bekannte Probleme**

* Keine

Weitere Informationen zum Identitätsdienst finden Sie in der Übersicht über den [Identitätsdienst](../../identity-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe von Plattformdiensten strukturieren, beschriften und verbessern können. Sie können Daten aus einer Vielzahl von Quellen wie Adobe-Anwendungen, Cloud-basierte Datenspeicherung, Drittanbieter-Software und Ihr CRM-System erfassen.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie Quellverbindungen für verschiedene Datenanbieter einfach einrichten können. Diese Quellverbindungen ermöglichen Ihnen die Authentifizierung und Verbindung zu externen Datenspeicherung- und CRM-Diensten, die Festlegung von Zeiten für die Erfassungsausführung und die Verwaltung des Datenaufkommens.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Veraltete Signale für Adobe Audience Manager Connector | Daten auf Signalebene von Audience Manager werden nicht mehr gesendet. Beachten Sie, dass die Segmentmitgliedschaft für Eigenschaften und Segmente weiterhin einbezogen wird. Infolge dieser Änderung werden keine eingehenden Datensätze mehr generiert. |
| Umbenannte Datensätze | Von Audience Manager Connector erstellte Datensätze enthalten aktualisierte Namen und Beschreibungen. |
| Umschalten zwischen Profil und Audience Manager aktivieren | Der Umschalter für Profile kann aktiviert oder deaktiviert werden, um den Datensatz für Echtzeit-Kundendaten-Profil zu bewerben. Umschalten ist standardmäßig aktiviert. |
| Benutzeroberflächenunterstützung für Cloud-Datenspeicherung-Systeme | Neuer Quell-Connector für Azurblauer Data Lake Datenspeicherung Gen2 in der Benutzeroberfläche. |
| Benutzeroberflächenunterstützung für CRM-Systeme | Neuer Quell-Connector für HubSpot, Salesforce Service Cloud und ServiceNow in der Benutzeroberfläche. |
| Benutzeroberflächenunterstützung für Datenbanksysteme | Neuer Quell-Connector für AWS Redshift, Google BigQuery, MariaDB, Microsoft SQL Server und MySQL in der Benutzeroberfläche. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).