---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch für Entwickler von Katalogdiensten
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Handbuch für Entwickler von Katalogdiensten

Der Katalogdienst ist das Datensatzsystem für die Datenposition und -linie innerhalb der Adobe Experience Platform. Der Katalog dient als Metadatenspeicher oder &quot;Katalog&quot;, in dem Sie Informationen zu Ihren Daten innerhalb der Experience Platform finden können, ohne dass Sie selbst auf die Daten zugreifen müssen. See the [Catalog overview](../home.md) for more information.

In diesem Entwicklerhandbuch finden Sie Anweisungen, wie Sie mit der Katalog-API Beginn ausführen können. Das Handbuch enthält dann Beispiel-API-Aufrufe für die Ausführung wichtiger Vorgänge mithilfe von Catalog.

## Voraussetzungen

Der Katalog verfolgt Metadaten für verschiedene Arten von Ressourcen und Vorgängen in der Experience Platform. Dieses Entwicklerhandbuch erfordert ein Verständnis der verschiedenen Experience Platform-Services, die mit der Erstellung und Verwaltung dieser Ressourcen verbunden sind:

* [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
* [Stapelverarbeitung](../../ingestion/batch-ingestion/overview.md): Wie Experience Platform Daten aus Datendateien wie CSV und Parquet erfasst und speichert.
* [Streaming-Erfassung](../../ingestion/streaming-ingestion/overview.md): So erfasst und speichert Experience Platform Daten von client- und serverseitigen Geräten in Echtzeit.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Katalogdienst-API erfolgreich aufrufen zu können.

## Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

## Werte für erforderliche Kopfzeilen sammeln

Um Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in der Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

* Content-Type: application/json

## Bewährte Verfahren für Aufrufe der Katalog-API

Beim Durchführen von GET-Anforderungen an die Katalog-API sollten Sie die Parameter für die Abfrage in Ihre Anforderungen aufnehmen, um nur die benötigten Objekte und Eigenschaften zurückzugeben. Ungefilterte Anforderungen können dazu führen, dass Antwortnutzlasten größer als 3 GB sind, was die Gesamtleistung verlangsamen kann.

Sie können bestimmte Objekte durch Einfügen ihrer ID in den Anforderungspfad oder mithilfe von Abfragen wie `properties` und zum Filtern `limit` von Antworten Ansichten erstellen. Filter können als Kopfzeilen und als Abfrage übergeben werden, wobei die Parameter als Abfrage Vorrang haben. Weitere Informationen finden Sie im Dokument zum [Filtern von Katalogdaten](filter-data.md) .

Da einige Abfragen die API stark belasten können, wurden globale Beschränkungen für Katalog-Abfragen implementiert, um Best Practices weiter zu unterstützen.

## Nächste Schritte

In diesem Dokument wurden die erforderlichen Kenntnisse zum Aufrufen der Katalog-API behandelt. Sie können nun zu den Beispielaufrufen in diesem Entwicklerhandbuch fortfahren und deren Anweisungen folgen.

Die meisten Beispiele in diesem Handbuch verwenden den `/dataSets` Endpunkt, aber die Prinzipien können auf andere Endpunkte innerhalb des Katalogs angewendet werden (z. B. `/batches` und `/accounts`). Eine vollständige Liste aller für jeden Endpunkt verfügbaren Aufrufe und Vorgänge finden Sie in der Referenz [zur](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Katalogdienst-API.

Ein schrittweiser Arbeitsablauf, der zeigt, wie die Katalog-API mit der Datenerfassung verbunden ist, finden Sie im Lernprogramm zum [Erstellen eines Datensatzes](../datasets/create.md).
