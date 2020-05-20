---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Objekt ersetzen
topic: developer guide
translation-type: tm+mt
source-git-commit: a753c6460bfe89e2b78fb3e087e9ba7397206dec
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 2%

---


# Objekt ersetzen

Sie können den Inhalt eines Katalogobjekts mit einer PUT-Anforderung überschreiben, bei der die gesamte Ressource durch die Anforderungs-Nutzlast ersetzt wird.

>[!NOTE] Wenn Sie nur einige bestimmte Felder innerhalb eines Katalogobjekts aktualisieren müssen, kann die Verwendung einer PATCH-Anforderung effizienter sein.

**API-Format**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des zu ersetzenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Der Bezeichner des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anforderung überschreibt einen Datensatz mit den Werten, die in der Payload bereitgestellt werden.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des überschriebenen Objekts enthält. Diese ID sollte mit der in der PUT-Anforderung gesendeten ID übereinstimmen. Die Ausführung einer GET-Anforderung für dieses Objekt zeigt jetzt, dass seine Details durch die in der Payload der vorherigen PUT-Anforderung angegebenen ersetzt wurden.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
