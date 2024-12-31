---
keywords: Experience Platform;Startseite;beliebte Themen;Katalog;API;Objekt ersetzen
solution: Experience Platform
title: Ersetzen eines Katalogobjekts
description: Sie können den Inhalt eines Catalog-Objekts mithilfe einer PUT-Anfrage überschreiben, wobei die gesamte Ressource durch die Anfrage-Payload ersetzt wird.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 2d6167ee7aaa0b79514be6e532e61602ae5cc640
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 10%

---

# Ersetzen eines Catalog-Objekts

Sie können den Inhalt eines [!DNL Catalog]-Objekts mithilfe einer PUT-Anfrage überschreiben, wobei die gesamte Ressource durch die Anfrage-Payload ersetzt wird.

>[!NOTE]
>
>Wenn Sie nur einige bestimmte Felder innerhalb eines [!DNL Catalog] aktualisieren müssen, ist die Verwendung einer PATCH-Anfrage möglicherweise effizienter.

**API-Format**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ [!DNL Catalog] zu ersetzenden Objekts. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | Die Kennung des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage überschreibt einen Datensatz mit den in der Payload angegebenen Werten.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein -Array zurück, das die ID des überschriebenen Objekts enthält. Diese ID sollte mit der in der PUT-Anfrage gesendeten ID übereinstimmen. Wenn Sie eine GET-Anfrage für dieses Objekt ausführen, wird jetzt angezeigt, dass seine Details durch die in der Payload der vorherigen PUT-Anfrage angegebenen ersetzt werden müssen.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
