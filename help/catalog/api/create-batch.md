---
keywords: Experience Platform; Startseite; beliebte Themen; Batch erstellen; Katalogdienst; API
solution: Experience Platform
title: Erstellen eines Batches in der API
description: Sie können einen Batch erstellen, indem Sie eine POST-Anfrage an den Endpunkt /batches in der Catalog Service API richten.
exl-id: 1d2cbca9-1cd6-4b89-9b77-3687268bd849
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 70%

---

# Erstellen eines Batches

Damit in einem Datensatz Daten aufgenommen werden können, muss ihm ein Batch zugeordnet werden. Sie können mithilfe des Werts für `id` eines vorhandenen Datensatzes einen Batch erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/batches` in der Service API senden.[!DNL Catalog]

**API-Format**

```HTTP
POST /batches
```

**Anfrage**

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `datasetId` | Die `id` des Datensatzes, dem der Batch zugeordnet wird. |

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 201 (Erstellung bestätigt) mit einem Antwortobjekt zurückgegeben, das den neu erstellten Batch einschließlich seiner `id`, einer schreibgeschützten, vom System generierten Zeichenfolge, beinhaltet.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{ORG_ID}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```
