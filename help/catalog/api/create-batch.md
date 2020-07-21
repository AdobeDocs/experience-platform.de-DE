---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Datensatzes
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 100%

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `datasetId` | Die `id` des Datensatzes, dem der Batch zugeordnet wird. |

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Statuscode 201 (Erstellung bestätigt) mit einem Antwortobjekt zurückgegeben, das den neu erstellten Batch einschließlich seiner `id`, einer schreibgeschützten, vom System generierten Zeichenfolge, beinhaltet.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
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
