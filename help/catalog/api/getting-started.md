---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch zum Catalog Service
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 52%

---


# [!DNL Catalog Service] Entwicklerhandbuch

[!DNL Catalog Service] ist ein Aufzeichnungssystem für Speicherort und Herkunft von Daten in Experience Platform. [!DNL Catalog] dient als Metadatenspeicher oder „Katalog“, in dem Sie Informationen über Ihre Daten in finden können, ohne auf die Daten selbst zugreifen zu müssen. [!DNL Experience Platform] Weiterführende Informationen dazu finden Sie unter [Catalog – Übersicht](../home.md).

This developer guide provides steps to help you start using the [!DNL Catalog] API. Dann bietet das Handbuch Beispiel-API-Aufrufe für die Ausführung wichtiger Vorgänge mithilfe von [!DNL Catalog].

## Voraussetzungen

[!DNL Catalog] verfolgt Metadaten für verschiedene Arten von Ressourcen und Vorgängen innerhalb von [!DNL Experience Platform]. This developer guide requires a working understanding of the various [!DNL Experience Platform] services involved with creating and managing these resources:

* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.
* [Batch-Erfassung](../../ingestion/batch-ingestion/overview.md)[!DNL Experience Platform]: So erfasst und speichert Daten aus Datendateien wie CSV und Parquet.
* [Streaming-Erfassung](../../ingestion/streaming-ingestion/overview.md)[!DNL Experience Platform]: So erfasst und speichert Daten von Client- und Server-seitigen Geräten in Echtzeit.

The following sections provide additional information that you will need to know or have on-hand in order to successfully make calls to the [!DNL Catalog Service] API.

## Lesehilfe für Beispiel-API-Aufrufe

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

## Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Alle Anfragen, die eine Payload enthalten (also POST-, PUT- und PATCH-Anfragen), erfordern eine zusätzliche Kopfzeile:

* Content-Type: application/json

## Best practices for [!DNL Catalog] API calls

When performing GET requests to the [!DNL Catalog] API, best practice is to include query parameters in your requests in order to return only the objects and properties that you need. Ungefilterte Anfragen können dazu führen, dass Antwort-Payloads größer als 3 GB sind, was die Gesamtleistung verringern kann.

Außerdem können Sie bestimmte Objekte durch Einfügen ihrer Kennung in den Anfragepfad anzeigen oder Abfrageparameter wie `properties` und `limit` zum Filtern von Antworten verwenden. Filter können als Kopfzeilen und Abfrageparameter übergeben werden, wobei Abfrageparameter bei der Übergabe Vorrang erhalten. Weiterführende Informationen finden Sie im Dokument zum [Filtern von Catalog-Daten](filter-data.md).

Since some queries can put a heavy load on the API, global limits have been implemented on [!DNL Catalog] queries to further support best practices.

## Nächste Schritte

This document covered the prerequisite knowledge required to make calls to the [!DNL Catalog] API. Sie können nun mit den Beispielaufrufen im Entwicklerhandbuch fortfahren und den entsprechenden Anweisungen folgen.

Most of the examples in this guide use the `/dataSets` endpoint, but the principles can be applied to other endpoints within [!DNL Catalog] (such as `/batches` and `/accounts`). Eine vollständige Liste aller bei einzelnen Endpunkten verfügbaren Aufrufe und Vorgänge finden Sie in der [Referenz zur Catalog Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

For a step-by-step workflow that demonstrates how the [!DNL Catalog] API is involved with data ingestion, see the tutorial on [creating a dataset](../datasets/create.md).
