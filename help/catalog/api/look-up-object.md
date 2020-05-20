---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Nachschlagen eines Objekts
topic: developer guide
translation-type: tm+mt
source-git-commit: 4dcd174eda98fee1e8cf668819809bd061c6e8bb
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 2%

---


# Nachschlagen eines Objekts

Wenn Sie die eindeutige ID für ein bestimmtes Katalogobjekt kennen, können Sie eine GET-Anforderung ausführen, um die Details dieses Objekts Ansicht.

>[!NOTE] Beim Anzeigen bestimmter Objekte empfiehlt es sich weiterhin, nach Eigenschaften [zu](filter-data.md) filtern und nur die Eigenschaften zurückzugeben, an denen Sie interessiert sind.

**API-Format**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Der Bezeichner des spezifischen Objekts, das Sie abrufen möchten. |

**Anfrage**

Mit der folgenden Anforderung wird ein Datensatz anhand seiner ID abgerufen und die zugehörigen `name`, `description`, `state`, `tags`und `files` Eigenschaften zurückgegeben.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der angegebene Datensatz nur mit dem angeforderten `properties` im Haupttext zurückgegeben.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE] Eigenschaften, deren Werte mit einem Präfix versehen sind, `@` stellen miteinander verknüpfte Objekte dar. Anweisungen zur Ansicht dieser Objekte finden Sie im Anhang zum [Anzeigen von miteinander verknüpften Objekten](appendix.md#view-interrelated-objects) .
