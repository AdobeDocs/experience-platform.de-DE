---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Handbuch zur API für Selbstbedienungsquellen (Batch-SDK)
description: Dieses Dokument bietet einen Überblick über den Prozess der Erstellung einer neuen Quelle, einschließlich der Schritte zum Abrufen, Schreiben und Senden einer neuen Verbindungsspezifikation mithilfe der Flow Service-API.
exl-id: 7e827989-207b-41e2-84d6-5ecb754bebb6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 8%

---

# Handbuch zur API für Selbstbedienungsquellen (Batch-SDK)

Dieses Dokument bietet einen Überblick über den Prozess der Erstellung einer neuen Quelle, einschließlich der Schritte zum Schreiben und Senden einer neuen Verbindungsspezifikation mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Experience Platform zu sammeln und zu zentralisieren. Der Service bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie auf einfache Weise Quellverbindungen zu verschiedenen Datenanbietern einrichten können. Diese Quell-Connectoren bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

Die [!DNL Flow Service]-API bietet mehrere Endpunkte, mit denen Sie die Verbindungs- und Flussspezifikationen für eine neue Quelle, die Sie über Selbstbedienungsquellen (Batch-SDK) integrieren, programmgesteuert verwalten können.

## Erstellen einer neuen Verbindungsspezifikation

Der erste Schritt beim Konfigurieren einer neuen Quelle besteht darin, eine neue Verbindungsspezifikation zu erstellen.

Verbindungsspezifikationen geben die Connector-Eigenschaften einer Quelle zurück. Sie enthalten Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen und eine feste Verbindungsspezifikations-ID, die einer bestimmten Quelle zugewiesen wird. Verbindungsspezifikationen sind mandanten- und organisationsunabhängig. Eine typische Verbindungsspezifikation enthält grundlegende Informationen zu einer bestimmten Quelle sowie drei verschiedene Abschnitte: `authSpec`, `sourceSpec` und `exploreSpec`.

Detaillierte Anweisungen finden Sie im Handbuch unter [Erstellen einer neuen Verbindungsspezifikation](./create.md). Informationen zu den Eigenschaften und Werten, die für eine Verbindungsspezifikation verwendet werden, einschließlich Details zum Konfigurieren der Authentifizierungs-, Quell- und Erkundungsspezifikationen, finden Sie [ Dokument „Konfigurationsoptionen](../config/config.md).

## Aktualisieren von Flussspezifikationen

Nachdem Sie eine Verbindungsspezifikation erfolgreich erstellt haben, müssen Sie die `RestStorageToAEP` Flussspezifikation anhängen, damit Ihre Quelle einen Datenfluss erstellen kann.

Flussspezifikationen enthalten Informationen, die einen Fluss definieren, darunter die unterstützten Quell- und Zielverbindungs-IDs, Transformationsspezifikationen, die auf die Daten angewendet werden müssen, und Zeitplanparameter, die zum Generieren eines Flusses erforderlich sind.

Detaillierte Anweisungen finden Sie im Handbuch zum [Aktualisieren von Flussspezifikationen](./update-flow-specs.md).

## Aktualisieren der Verbindungsspezifikation

Sie können Ihre Verbindungsspezifikation aktualisieren, indem Sie eine PUT-Anfrage an die [!DNL Flow Service]-API senden. Weitere Informationen finden Sie in [ Anleitung zum Aktualisieren ](./update-connection-specs.md) Verbindungsspezifikationen .

## Übermitteln Ihrer Quelle

Um Ihre Quelle zur Integration in Experience Platform zu übermitteln, müssen Sie zunächst den gesamten [!DNL Flow Service]-API-Workflow für Quellen abschließen, um sicherzustellen, dass Ihre Quelle erfolgreich funktioniert. Wenn Ihre Quelle erfolgreich ausgeführt wird, können Sie fortfahren und sich an Ihren Adobe-Support-Mitarbeiter wenden, um sie zu überprüfen und zu bewerben. Weitere Informationen finden Sie in [ Anleitung zum Testen und Senden ](./submit.md) Quelle .

## Nächste Schritte

Um mit der Verwendung der [!DNL Flow Service]-API zu beginnen und mithilfe von Selbstbedienungsquellen (Batch-SDK) eine neue Quelle zu erstellen, lesen Sie [Erste Schritte](./getting-started.md) und wählen Sie dann eines der Endpunkthandbücher aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden.
