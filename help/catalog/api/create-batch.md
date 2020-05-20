---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datensatz erstellen
topic: developer guide
translation-type: tm+mt
source-git-commit: a25ca22fb8ec9eb95f74e4fd76a7f18e87343085
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 4%

---


# Stapel erstellen

Damit ein Datensatz Daten erfassen kann, muss ihm ein Stapel zugeordnet sein. Mithilfe des `id` Werts eines vorhandenen Datensatzes können Sie einen Stapel erstellen, indem Sie eine POST-Anforderung an den `/batches` Endpunkt in der Katalog-API senden.

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
| `datasetId` | Der Datensatz, mit `id` dem der Stapel verknüpft wird. |

**Antwort**

Bei einer erfolgreichen Antwort werden HTTP-Status 201 (Erstellt) und ein Antwortobjekt mit Details zum neu erstellten Stapel zurückgegeben, einschließlich einer `id`schreibgeschützten, vom System erstellten Zeichenfolge.

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
