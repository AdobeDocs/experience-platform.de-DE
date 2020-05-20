---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Mehrere Objekte suchen
topic: developer guide
translation-type: tm+mt
source-git-commit: f3e9da9ab3d02006c07c59b17751c971a95d49bc
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---


# Mehrere Objekte suchen

Wenn Sie anstelle einer Anforderung pro Objekt mehrere bestimmte Objekte Ansicht haben möchten, stellt Catalog eine einfache Verknüpfung zum Anfordern mehrerer Objekte desselben Typs bereit. Sie können eine einzelne GET-Anforderung verwenden, um mehrere bestimmte Objekte zurückzugeben, indem Sie eine kommagetrennte Liste von IDs einschließen.

>[!NOTE] Auch wenn Sie bestimmte Katalogobjekte anfordern, empfiehlt es sich dennoch, den Parameter &quot; `properties` Abfrage&quot;so zu verwenden, dass nur die benötigten Eigenschaften zurückgegeben werden.

**API-Format**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| `{OBJECT_TYPE}` | Der Typ des abzurufenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | Ein Bezeichner für eines der spezifischen Objekte, die Sie abrufen möchten. |

**Anfrage**

Die folgende Anforderung umfasst eine kommagetrennte Liste von DataSet-IDs sowie eine kommagetrennte Liste von Eigenschaften, die für jeden Datensatz zurückgegeben werden.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste der angegebenen Datensätze zurück, die nur die angeforderten Eigenschaften (`name`, `description`und `files`) enthält.

>[!NOTE] Wenn ein zurückgegebenes Objekt nicht mehr eine der angeforderten Eigenschaften enthält, die von der `properties` Abfrage angegeben werden, gibt die Antwort nur die angeforderten Eigenschaften zurück, die es enthält, wie unten unter &quot;Beispiel-Datensatz 3&quot;und &quot;Beispiel-Datensatz 4&quot;dargestellt.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```
