---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datensatz erstellen
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 70%

---


# Datensatz erstellen

In order to create a dataset using the [!DNL Catalog] API, you must know the `$id` value of the [!DNL Experience Data Model] (XDM) schema on which the dataset will be based. Once you have the schema ID, you can create a dataset by making a POST request to the `/datasets` endpoint in the [!DNL Catalog] API.

>[!NOTE]
>
>This document only covers how to create a dataset object in [!DNL Catalog]. Ausführliche Anweisungen zum Erstellen, Füllen und Überwachen eines Datensatzes finden Sie im folgenden [Tutorial](../datasets/create.md).

**API-Format**

```HTTP
POST /dataSets
```

**Anfrage**

Die folgende Anfrage erstellt einen Datensatz, der auf ein zuvor definiertes Schema verweist.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name des zu erstellenden Datensatzes. |
| `schemaRef.id` | Der URI-`$id`-Wert für das XDM-Schema, auf dem der Datensatz basieren soll. |

>[!NOTE]
>
>In diesem Beispiel wird das [Parquet](https://parquet.apache.org/documentation/latest/)-Dateiformat für die Eigenschaft `containerFormat` verwendet. Ein Beispiel zur Nutzung des JSON-Dateiformats finden Sie im [Entwicklerhandbuch zur Batch-Erfassung](../../ingestion/batch-ingestion/api-overview.md).

**Antwort**

Bei erfolgreicher Anfrage wird der HTTP-Statuscode 201 (Erstellung bestätigt) mit einem Antwortobjekt zurückgegeben, das ein Array mit der ID des neu erstellten Datensatzes im Format `"@/datasets/{DATASET_ID}"` beinhaltet. Die Datensatzkennung ist eine schreibgeschützte, systemgenerierte Zeichenfolge, mit der in API-Aufrufen auf den Datensatz verwiesen wird.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
