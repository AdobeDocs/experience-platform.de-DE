---
title: Versionshinweise zu Adobe Experience Platform
description: Versionshinweise zur Experience Platform vom 21. April 2021.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 35%

---


# Versionshinweise zu Adobe Experience Platform

**Releasedatum: 21. April 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für die Bearbeitung der Zuordnung für vorhandene Datenflüsse | Sie können jetzt die Zuordnungssätze eines vorhandenen Datenflusses aktualisieren. Sie können keine Zuordnungssätze für Datenflüsse aktualisieren, die für eine einmalige Erfassung geplant waren. Diese Funktion wird für HTTP API, Adobe Analytics, Adobe Audience Manager und [!DNL Marketo Engage] nicht unterstützt. Weitere Informationen finden Sie im Tutorial zu [Aktualisieren der Quelldataflows in der Benutzeroberfläche](../../sources/tutorials/ui/update-dataflows.md). |
| Unterstützung für Streaming-Erfassung | Sie können jetzt beim Erstellen einer Streaming-Quellverbindung die Funktion &quot;Datenvorgabe&quot;verwenden. Weitere Informationen finden Sie im Tutorial zum Erstellen einer Streaming-Quellverbindung in der Benutzeroberfläche](../../sources/tutorials/ui/create/streaming/http.md).[ |

Weitere Informationen finden Sie unter [[!DNL Data Prep] overview](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM) ist eine Open-Source-Spezifikation, die die Leistung digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, um Einblicke schneller und besser integriert zu liefern. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

| Funktion | Beschreibung |
| --- | --- |
| Empfehlungen des Schemas durch die Branche | Wenn Sie Klassen und Schema-Feldgruppen in der Benutzeroberfläche des Schema-Editors auswählen, können Sie einen neuen Filter verwenden, um empfohlene Standardkomponenten basierend auf Ihrer Branche Ansicht. Weitere Informationen dazu, wie sich diese Komponenten für verschiedene Anwendungsfälle in der Industrie zueinander verhalten, finden Sie in der Dokumentation zu [Industrie-Datenmodellen](https://www.adobe.com/go/xdm-industry-erds-en). |

## [!DNL Intelligent Services] {#intelligent-services}

Mit Intelligent Services können Marketing-Analysten und -Experten die Vorteile von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen nutzen. Auf diese Weise können Marketinganalysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen einer Firma erstellen, ohne dass hierfür Fachwissen in der Datenwissenschaft erforderlich ist.

### Customer AI

Die in der Kundendatenplattform in Echtzeit verfügbare Kundentelefonie wird verwendet, um benutzerspezifische Tendenzwerte wie Kehren und Konversion für einzelne Profil im Maßstab zu generieren. Dies wird erreicht, ohne dass die Geschäftsanforderungen in ein Problem des maschinellen Lernens umgewandelt, ein Algorithmus ausgewählt, trainiert oder bereitgestellt werden muss.

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für Adobe Analytics-Daten | Die Funktion zur Unterstützung von Adobe Analytics-Datensätzen über den Analytics-Quell-Connector wurde aktualisiert, ohne dass die ETL-Daten an das Consumer Experience Ereignis (CEE)-Schema angepasst werden müssen. |
| Unterstützung für Adobe Audience Manager-Daten | Die Funktion zur Unterstützung von Adobe Audience Manager-Datensätzen über den Audience Manager-Quell-Connector wurde aktualisiert, ohne dass die ETL-Daten an das Consumer Experience Ereignis (CEE)-Schema angepasst werden müssen. |
| Leistungszusammenfassung des Modells | Die Kunden-API verfügt nun über die Registerkarte [Leistungszusammenfassung des Modells](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) auf der Insight-Seite der Dienstinstanz. Auf der Registerkarte &quot;Modellleistung&quot;werden alle tatsächlichen Konversions- und Absturzraten angezeigt. Auf diese Weise können Sie entziffern und verstehen, was in jedem Ihrer Tendenzbehälter geschieht. |

Weitere Informationen zu unterstützten Datensätzen finden Sie in der [[!DNL Intelligent Services] Dokumentation zur Datenvorbereitung](../../intelligent-services/data-preparation.md).

### Attribution AI

Attribution AI wird verwendet, um Touchpoints Ereignissen zuzuordnen, die zu Konversionen führen. Dies kann von Marketing-Experten genutzt werden, um die Auswirkungen jedes einzelnen Marketing-Touchpoints auf einer Customer Journey zu quantifizieren.

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für Adobe Analytics-Daten | Die Funktion zur Unterstützung von Adobe Analytics-Datensätzen über den Analytics-Quell-Connector wurde aktualisiert, ohne dass die ETL-Daten an das Consumer Experience Ereignis (CEE)-Schema angepasst werden müssen. |

Weitere Informationen zu unterstützten Datensätzen finden Sie in der [[!DNL Intelligent Services] Dokumentation zur Datenvorbereitung](../../intelligent-services/data-preparation.md).

## Segmentierungs-Service {#segmentation}

Der Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und Audiencen aus Ihren [!DNL Real-time Customer Profile]-Daten generieren können. Diese Segmente werden zentral in Platform konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Zusätzliche Aggregationsfunktionen | Funktionen zur Zählung wurden im Segmentaufbau hinzugefügt. Mit den Zählfunktionen können Sie zählen, wie oft das angegebene Ereignis ausgeführt wurde. Weitere Informationen zu den Zählfunktionen finden Sie im Abschnitt zu Zählfunktionen im Handbuch [Segmentaufbau](../../segmentation/ui/segment-builder.md#count-functions) |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierungsübersicht](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Sie können jetzt eine [!DNL Marketo Engage]-Quellverbindung über die Benutzeroberfläche erstellen, um B2B-Daten auf die Plattform zu übertragen und diese Daten mithilfe von Anwendungen mit Plattformverbindung auf dem neuesten Stand zu halten. Weitere Informationen finden Sie in der [[!DNL Marketo Engage] Dokumentation zum Quellanschluss](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Beta-Quellen wechseln zu GA | Die folgenden Quellen wurden von der Beta-Version zur GA-Version beworben: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
