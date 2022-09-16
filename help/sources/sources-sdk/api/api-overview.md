---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Handbuch zur API für Self-Serve-Quellen (Batch SDK)
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Prozess der Erstellung einer neuen Quelle, einschließlich der Schritte zum Abrufen, Schreiben und Senden einer neuen Verbindungsspezifikation mithilfe der Flow Service-API.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 11%

---

# Handbuch zur API für Self-Serve-Quellen (Batch SDK)

Dieses Dokument bietet einen Überblick über den Prozess der Erstellung einer neuen Quelle, einschließlich der Schritte zum Schreiben und Senden einer neuen Verbindungsspezifikation mit dem [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Platform zu sammeln und zu zentralisieren. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie auf einfache Weise Quellverbindungen zu verschiedenen Datenanbietern einrichten können. Diese sogenannten „Quell-Connectoren“ bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

Die [!DNL Flow Service] API bietet mehrere Endpunkte, mit denen Sie die Verbindungs- und Flussspezifikationen für eine neue Quelle programmgesteuert verwalten können, die Sie über Self-Serve-Quellen (Batch SDK) integrieren.

## Neue Verbindungsspezifikation erstellen

Der erste Schritt beim Konfigurieren einer neuen Quelle besteht darin, eine neue Verbindungsspezifikation zu erstellen.

Verbindungsspezifikationen geben die Connector-Eigenschaften einer Quelle zurück. Dazu gehören Authentifizierungsspezifikationen im Zusammenhang mit der Erstellung der Basis- und Quellverbindungen sowie eine feste Verbindungs-Spezifikations-ID, die einer bestimmten Quelle zugewiesen ist. Verbindungsspezifikationen sind Mandant und IMS-Organisation agnostisch. Eine typische Verbindungsspezifikation enthält grundlegende Informationen zu einer bestimmten Quelle sowie drei verschiedene Abschnitte: `authSpec`, `sourceSpec`und `exploreSpec`.

Detaillierte Anweisungen finden Sie im Handbuch unter [Erstellen einer neuen Verbindungsspezifikation](./create.md). Informationen zu den Eigenschaften und Werten, die für eine Verbindungsspezifikation verwendet werden, einschließlich Details zum Konfigurieren der Authentifizierung, Quelle und zu Analysespezifikationen, finden Sie in der [Konfigurationsoptionen-Dokument](../config/config.md).

## Flussspezifikationen aktualisieren

Nachdem Sie eine Verbindungsspezifikation erfolgreich erstellt haben, müssen Sie die `RestStorageToAEP` Flussspezifikation, damit Ihre Quelle einen Datenfluss erstellen kann.

Flussspezifikationen enthalten Informationen, die einen Fluss definieren, einschließlich der von ihm unterstützten Quell- und Zielverbindungs-IDs, Transformationsspezifikationen, die auf die Daten angewendet werden müssen, und Planungsparameter, die zum Generieren eines Datenflusses erforderlich sind.

Detaillierte Anweisungen finden Sie im Handbuch unter [Flussspezifikationen aktualisieren](./update-flow-specs.md).

## Verbindungsspezifikation aktualisieren

Sie können Ihre Verbindungsspezifikation aktualisieren, indem Sie eine PUT-Anfrage an die [!DNL Flow Service] API. Siehe Handbuch unter [Aktualisieren der Verbindungsspezifikationen](./update-connection-specs.md) für weitere Informationen.

## Übermitteln Ihrer Quelle

Um Ihre Quelle zur Integration in Experience Platform zu übermitteln, müssen Sie zunächst die gesamte [!DNL Flow Service] API-Workflow für Quellen, um sicherzustellen, dass Ihre Quelle erfolgreich funktioniert. Wenn Ihre Quelle erfolgreich ausgeführt wird, können Sie fortfahren und sich zur Überprüfung und Promotion an Ihren Kundenbetreuer wenden. Siehe Handbuch unter [Testen und Senden der Quelle](./submit.md) für weitere Informationen

## Nächste Schritte

So verwenden Sie die [!DNL Flow Service] API erstellen und eine neue Quelle über Self-Serve-Quellen (Batch SDK) erstellen, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md) Wählen Sie dann eine der Endpunktleitfäden aus, um zu erfahren, wie Sie bestimmte Endpunkte verwenden.
