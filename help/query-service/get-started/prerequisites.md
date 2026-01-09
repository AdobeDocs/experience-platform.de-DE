---
keywords: Experience Platform;Abfrage-Service;Abfrage-Service;Abfrage
title: Erste Schritte mit dem Abfrage-Service von Adobe Experience Platform
description: Eine Aufschlüsselung der erforderlichen Schritte zur vollständigen Nutzung des Adobe Experience Platform Query Service
exl-id: 36ab9354-23f9-4cb8-bcd4-00fe076386ab
source-git-commit: fa22a0ca0c79d5d62fd39de3a808f84a11a80c4d
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 2%

---

# Erste Schritte mit Adobe Experience Platform [!DNL Query Service] {#getting-started}

Verwenden Sie den Abfrage-Service von Adobe Experience Platform, um SQL-Abfragen für aufgenommene Datensätze auszuführen, Daten aus mehreren Quellen zu verbinden und abgeleitete Datensätze für Analysen, maschinelle Lern-Workflows oder Echtzeit-Kundenprofile zu generieren. Greifen Sie nach der Aufnahme von Daten auf den Abfrage-Service über die Benutzeroberfläche für interaktive Analyse und Zusammenarbeit oder über die API für die automatisierte und programmgesteuerte Ausführung von Abfragen zu.

## Voraussetzungen {#prerequisites}

Bevor Sie mit der Datenabfrage beginnen können, stellen Sie Folgendes sicher:

- **Erforderliche Berechtigungen**: Ihr Benutzerkonto hat Zugriff auf den Abfrage-Service in Experience Platform. Wenn der Service nicht in der Benutzeroberfläche verfügbar ist, lesen Sie die [Dokumentation zu Berechtigungen](../../access-control/home.md#permissions) und wenden Sie sich an Ihren Systemadministrator.
- **Datenaufnahme**: Sie haben Daten in Experience Platform aufgenommen.

Wenn Sie Daten aufnehmen müssen, finden Sie im [Tutorial zur Datenaufnahme](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=de) einen Überblick über die Erstellung von Datensätzen, die Schemazuordnung, die Aufnahme und die Validierung. Lesen Sie [&#x200B; Dokumentation „Aufnahme - Übersicht](../../ingestion/home.md), um weitere Informationen und Links zu anderen Lernressourcen zu erhalten.

## Schnellstartpfade

Nachdem Sie Ihre Daten in Experience Platform aufgenommen haben, können Sie mit dem Abfrage-Service beginnen, indem Sie entweder die [!DNL Query Editor] in Experience Platform oder die Abfrage-Service-API verwenden.

### [!DNL Query Editor]

Verwenden Sie die [!DNL Query Editor] für Analysen, Datenexploration und die Entwicklung kollaborativer Abfragen. Einen Überblick über die Benutzeroberflächenfunktionen finden Sie unter [Dokumentation zur Query Service-Benutzeroberfläche](../ui/overview.md). Informationen zum Schreiben und Ausführen von Abfragen in der Benutzeroberfläche finden Sie in der [[!DNL Query Editor user guide]](../ui/user-guide.md).

### Abfrage-Service-API

Verwenden Sie die Abfrage-Service-API für automatisierte Workflows, die Verwaltung von Abfragevorlagen und programmgesteuerte Integrationen. Ausführliche Anweisungen zur Verwendung [&#x200B; Abfrage-Service-API finden &#x200B;](../api/getting-started.md) im Query Service-Entwicklerhandbuch .

## Nächste Schritte

In diesem Dokument wurden die Voraussetzungen für die Verwendung [!DNL Query Service] Funktionen in Experience Platform behandelt. Um schnell mit den Funktionen von Query Service zu beginnen, sollten Sie die folgenden Dokumente lesen:

- [Allgemeine Leitlinien für die Ausführung von Abfragen](../best-practices/writing-queries.md)
- [SQL-Syntax in Query Service](../sql/syntax.md)
- [Erstellen abgeleiteter Datensätze mit SQL](../data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

Weitere Informationen dazu, wie der Abfrage-Service die Datenverarbeitung in Experience Platform unterstützt, finden Sie in der [Präsentation zum abgebrochenen Durchsuchen-Anwendungsfall](../use-cases/abandoned-browse.md#video-example).

Die folgenden Ressourcen sind nützlich, um Ihr Verständnis von [!DNL Query Service] zu verbessern:

- [[!DNL Query Service] Benutzeroberfläche – Übersicht](../ui/overview.md)
- [[!DNL Query Service]](../ui/credentials.md)
- [Die Übersicht über Client-Verbindungen](../clients/overview.md)
