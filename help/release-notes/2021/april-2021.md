---
title: Adobe Experience Platform – Versionshinweise April 2021
description: Die Versionshinweise für Adobe Experience Platform vom April 2021.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 96%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 21. April 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für die Bearbeitung von Zuordnungen in vorhandenen Datenflüssen | Sie können nun die Zuordnungssätze für einen vorhandenen Datenfluss aktualisieren. Sie können keine Zuordnungssätze für Datenflüsse aktualisieren, die für eine einmalige Erfassung geplant wurden. Diese Funktion wird bei der HTTP-API, Adobe Analytics, Adobe Audience Manager und [!DNL Marketo Engage] nicht unterstützt. Weitere Informationen finden Sie im Tutorial zum [Aktualisieren von Quelldatenflüssen in der Benutzeroberfläche](../../sources/tutorials/ui/update-dataflows.md). |
| Unterstützung für die Streaming-Erfassung | Sie können beim Erstellen einer Streaming-Quellverbindung nun Funktionen zur Datenvorbereitung verwenden. Weitere Informationen finden Sie im Tutorial zum [Erstellen einer Streaming-Quellverbindung in der Benutzeroberfläche](../../sources/tutorials/ui/create/streaming/http.md). |

Weitere Informationen finden Sie unter [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Das Experience-Datenmodell (XDM) ist eine Open-Source-Spezifikation, die dazu dient, die Leistung digitaler Erlebnisse zu verbessern. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

| Funktion | Beschreibung |
| --- | --- |
| Branchenspezifische Schemaempfehlungen | Bei der Auswahl von Klassen und Schemafeldgruppen in der Benutzeroberfläche des Schema-Editors können Sie einen neuen Filter verwenden, um je nach Branche empfohlene Standardkomponenten anzuzeigen. Weitere Informationen dazu, wie sich diese Komponenten in verschiedenen branchenspezifischen Anwendungsfällen beeinflussen, finden Sie in der Dokumentation zu [branchenspezifischen Datenmodellen](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/industries/overview.html?lang=de). |

## [!DNL Intelligent Services] {#intelligent-services}

Mit Intelligent Services können Marketing-Analysten und -Experten die Vorteile von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen der Firma erstellen, ohne dass hierfür Kenntnisse aus der Datenwissenschaft erforderlich wären.

### Customer AI

In Real-time Customer Data Platform verfügbare Customer AI wird verwendet, um benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion für einzelne Profile skaliert zu generieren. Dies wird erreicht, ohne dass die Geschäftsanforderungen in ein Problem des maschinellen Lernens umgewandelt werden müssen bzw. ein Algorithmus ausgewählt, trainiert oder bereitgestellt werden muss.

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für Adobe Analytics-Daten | Die Funktion zur Unterstützung von Adobe Analytics-Datensätzen über den Analytics-Quell-Connector wurde aktualisiert, sodass Ihre Daten keinem ETL-Vorgang unterzogen werden müssen, um dem Schema Consumer Experience Event (CEE) zu entsprechen. |
| Unterstützung für Adobe Audience Manager-Daten | Die Funktion zur Unterstützung von Adobe Audience Manager-Datensätzen über den Audience Manager-Quell-Connector wurde aktualisiert, sodass Ihre Daten keinem ETL-Vorgang unterzogen werden müssen, um dem Schema Consumer Experience Event (CEE) zu entsprechen. |
| Übersicht über die Modellleistung | Customer AI bietet nun auf der Insights-Seite der Dienstinstanz einen Tab mit einer [Übersicht über die Modellleistung](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics). Auf dem Tab für die Modellleistung werden alle tatsächlichen Konversions- und Abwanderungsraten angezeigt. Auf diese Weise können Sie entschlüsseln und verstehen, was in Ihren einzelnen Kaufneigungs-Buckets geschieht. |

Weitere Informationen zu unterstützten Datensätzen finden Sie in der [[!DNL Intelligent Services] Dokumentation zur Datenvorbereitung](../../intelligent-services/data-preparation.md).

### Attribution AI

Attributions-KI wird verwendet, um Touchpoints Ereignissen zuzuordnen, die zu Konversionen führen. Dies kann von Marketing-Experten genutzt werden, um die Auswirkungen jedes einzelnen Marketing-Touchpoints auf einer Customer Journey zu quantifizieren.

| Funktion | Beschreibung |
| ------- | ----------- |
| Unterstützung für Adobe Analytics-Daten | Die Funktion zur Unterstützung von Adobe Analytics-Datensätzen über den Analytics-Quell-Connector wurde aktualisiert, sodass Ihre Daten keinem ETL-Vorgang unterzogen werden müssen, um dem Schema Consumer Experience Event (CEE) zu entsprechen. |

Weitere Informationen zu unterstützten Datensätzen finden Sie in der [[!DNL Intelligent Services] Dokumentation zur Datenvorbereitung](../../intelligent-services/data-preparation.md).

## Segmentierungs-Service {#segmentation}

Adobe Experience Platform Segmentation Service bietet eine Benutzeroberfläche und RESTful-API, mit der Sie Segmente erstellen und aus Ihren [!DNL Real-Time Customer Profile]-Daten Zielgruppen generieren können. Diese Segmente werden zentral in Platform konfiguriert und gepflegt, sodass sie für jede Adobe-Anwendung leicht zugänglich sind.

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Zusätzliche Aggregationsfunktionen | Segment Builder wurde um Zählfunktionen ergänzt. Mit Zählfunktionen können Sie zählen, wie oft das angegebene Ereignis ausgeführt wurde. Weitere Informationen zu Zählfunktionen finden Sie im Abschnitt zu den Zählfunktionen des [Segment Builder-Handbuchs](../../segmentation/ui/segment-builder.md#count-functions). |

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierung – Übersicht](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| ------- | ----------- |
| [!DNL Marketo Engage] (Betaversion) | Sie können über die Benutzeroberfläche nun eine [!DNL Marketo Engage]-Quellverbindung erstellen, um B2B-Daten an Platform zu übertragen und mit Anwendungen, die mit Platform verbunden sind, auf dem neuesten Stand zu halten. Weitere Informationen finden Sie in der [[!DNL Marketo Engage] Quell-Connector-Dokumentation](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
