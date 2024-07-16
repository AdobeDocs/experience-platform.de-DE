---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Handbuch zur API für Self-Serve-Quellen (Batch SDK)
description: Dieses Dokument bietet einen Überblick über den Prozess der Erstellung einer neuen Quelle, einschließlich der Schritte zum Abrufen, Schreiben und Senden einer neuen Verbindungsspezifikation mithilfe der Flow Service-API.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 10%

---

# Handbuch zur API für Self-Serve-Quellen (Batch SDK)

Dieses Dokument bietet einen Überblick über den Prozess der Erstellung einer neuen Quelle, einschließlich der Schritte zum Schreiben und Senden einer neuen Verbindungsspezifikation mit der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Platform zu sammeln und zu zentralisieren. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie auf einfache Weise Quellverbindungen zu verschiedenen Datenanbietern einrichten können. Diese Quell-Connectoren bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

Die API [!DNL Flow Service] bietet mehrere Endpunkte, mit denen Sie die Verbindungs- und Flussspezifikationen für eine neue Quelle programmgesteuert verwalten können, die Sie über Self-Serve-Quellen (Batch SDK) integrieren.

## Neue Verbindungsspezifikation erstellen

Der erste Schritt beim Konfigurieren einer neuen Quelle besteht darin, eine neue Verbindungsspezifikation zu erstellen.

Verbindungsspezifikationen geben die Connector-Eigenschaften einer Quelle zurück. Dazu gehören Authentifizierungsspezifikationen im Zusammenhang mit der Erstellung der Basis- und Quellverbindungen sowie eine feste Verbindungs-Spezifikations-ID, die einer bestimmten Quelle zugewiesen ist. Verbindungsspezifikationen sind Mandanten und Unternehmen agnostisch. Eine typische Verbindungsspezifikation enthält grundlegende Informationen zu einer bestimmten Quelle sowie drei verschiedene Abschnitte: `authSpec`, `sourceSpec` und `exploreSpec`.

Detaillierte Anweisungen finden Sie im Handbuch zum [Erstellen einer neuen Verbindungsspezifikation](./create.md). Informationen zu den Eigenschaften und Werten, die für eine Verbindungsspezifikation verwendet werden, einschließlich Details zum Konfigurieren von Authentifizierung, Quelle und Analysespezifikationen, finden Sie im Dokument [Konfigurationsoptionen](../config/config.md).

## Flussspezifikationen aktualisieren

Nachdem Sie eine Verbindungsspezifikation erfolgreich erstellt haben, müssen Sie die Flussspezifikation `RestStorageToAEP` anhängen, damit Ihre Quelle einen Datenfluss erstellen kann.

Flussspezifikationen enthalten Informationen, die einen Fluss definieren, einschließlich der von ihm unterstützten Quell- und Zielverbindungs-IDs, Transformationsspezifikationen, die auf die Daten angewendet werden müssen, und Planungsparameter, die zum Generieren eines Datenflusses erforderlich sind.

Detaillierte Anweisungen finden Sie im Handbuch zu [Aktualisierung der Flussspezifikationen](./update-flow-specs.md).

## Verbindungsspezifikation aktualisieren

Sie können Ihre Verbindungsspezifikation aktualisieren, indem Sie eine PUT-Anfrage an die [!DNL Flow Service] -API richten. Weitere Informationen finden Sie im Handbuch zum [Aktualisieren Ihrer Verbindungsspezifikationen](./update-connection-specs.md) .

## Übermitteln Ihrer Quelle

Um Ihre Quelle zur Integration an Experience Platform zu übermitteln, müssen Sie zunächst den gesamten [!DNL Flow Service] API-Workflow für Quellen ausführen, um sicherzustellen, dass Ihre Quelle erfolgreich funktioniert. Wenn Ihre Quelle erfolgreich ausgeführt wird, können Sie fortfahren und sich zur Verifizierung und Promotion an Ihren Adobe-Support-Mitarbeiter wenden. Weitere Informationen finden Sie im Handbuch zum [Testen und Senden der Quelle](./submit.md) .

## Nächste Schritte

Um mit der Verwendung der [!DNL Flow Service] -API zu beginnen und über Self-Serve-Quellen (Batch-SDK) eine neue Quelle zu erstellen, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) und wählen Sie dann eine der Endpunkthandbücher aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
