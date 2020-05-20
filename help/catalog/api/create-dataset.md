---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datensatz erstellen
topic: developer guide
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 1%

---


# Datensatz erstellen

Um mit der Katalog-API einen Datensatz zu erstellen, müssen Sie den `$id` Wert des XDM-Schemas (Experience Data Model) kennen, auf dem der Datensatz basieren soll. Sobald Sie über die Schema-ID verfügen, können Sie einen Datensatz erstellen, indem Sie eine POST-Anforderung an den `/datasets` Endpunkt in der Katalog-API senden.

>[!NOTE] In diesem Dokument wird nur die Erstellung eines Datensatzobjekts im Katalog behandelt. Ausführliche Anweisungen zum Erstellen, Füllen und Überwachen eines Datensatzes finden Sie im folgenden [Lernprogramm](../datasets/create.md).

**API-Format**

```HTTP
POST /dataSets
```

**Anfrage**

Die folgende Anforderung erstellt einen Datensatz, der auf ein zuvor definiertes Schema verweist.

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
| `schemaRef.id` | Der URI- `$id` Wert für das XDM-Schema, auf dem der Datensatz basiert. |

>[!NOTE] In diesem Beispiel wird das [Parquet](https://parquet.apache.org/documentation/latest/) -Dateiformat für seine `containerFormat` Eigenschaft verwendet. Ein Beispiel, das das JSON-Dateiformat verwendet, finden Sie im Entwicklerhandbuch für [Stapelverarbeitung](../../ingestion/batch-ingestion/api-overview.md).

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und ein Antwortobjekt zurück, das aus einem Array mit der ID des neu erstellten Datensatzes im Format `"@/datasets/{DATASET_ID}"`besteht. Die DataSet-ID ist eine schreibgeschützte, systemgenerierte Zeichenfolge, mit der auf den Datensatz in API-Aufrufen verwiesen wird.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
