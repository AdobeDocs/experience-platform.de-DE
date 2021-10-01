---
keywords: Experience Platform; Startseite; beliebte Themen; Katalog; API; Objekt ersetzen
solution: Experience Platform
title: Katalogobjekt ersetzen
topic-legacy: developer guide
description: Sie können den Inhalt eines Catalog-Objekts mithilfe einer PUT-Anfrage überschreiben, wobei die gesamte Ressource durch die Anfrage-Payload ersetzt wird.
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 10%

---

# Catalog-Objekt ersetzen

Sie können den Inhalt eines [!DNL Catalog]-Objekts mithilfe einer PUT-Anfrage überschreiben, wobei die gesamte Ressource durch die Anfrage-Payload ersetzt wird.

>[!NOTE]
>
>Wenn Sie nur einige bestimmte Felder in einem [!DNL Catalog] -Objekt aktualisieren müssen, kann die Verwendung einer PATCH-Anfrage effizienter sein.

**API-Format**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des zu ersetzenden [!DNL Catalog]-Objekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Die Kennung des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage überschreibt einen Datensatz mit den in der Payload angegebenen Werten.

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

Eine erfolgreiche Antwort gibt ein Array zurück, das die Kennung des überschriebenen Objekts enthält. Diese ID sollte mit der in der PUT-Anfrage gesendeten ID übereinstimmen. Die Ausführung einer GET-Anfrage für dieses Objekt zeigt jetzt, dass seine Details durch die in der Payload der vorherigen PUT-Anfrage angegebenen ersetzt wurden.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
