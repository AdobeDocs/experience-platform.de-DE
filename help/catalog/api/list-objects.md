---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Liste, Objekte
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 1%

---


# Liste, Objekte

Sie können eine Liste aller verfügbaren Objekte eines bestimmten Typs über einen einzigen API-Aufruf abrufen. Es empfiehlt sich, Filter einzubeziehen, die die Größe der Antwort beschränken.

**API-Format**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des aufzuführenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Ein Parameter für die Abfrage, mit dem die in der Antwort zurückgegebenen Ergebnisse gefiltert werden. Mehrere Parameter werden durch das kaufmännische Und (`&`) getrennt. Weitere Informationen finden Sie im Handbuch zum [Filtern von Katalogdaten](filter-data.md) . |

**Anfrage**

Die unten stehende Musteranforderung ruft eine Liste von Datensätzen ab, wobei ein `limit` Filter die Antwort auf fünf Ergebnisse reduziert und ein `properties` Filter, der die für jeden Datensatz angezeigten Eigenschaften einschränkt.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Katalogobjekten in Form von Schlüssel-Wert-Paaren zurück, gefiltert nach den in der Anforderung bereitgestellten Abfragen. Für jedes Schlüssel-Wert-Paar stellt der Schlüssel einen eindeutigen Bezeichner für das betreffende Katalogobjekt dar, der dann in einem anderen Aufruf zur [Ansicht dieses bestimmten Objekts](look-up-object.md) verwendet werden kann.

>[!NOTE]
>
>Wenn ein zurückgegebenes Objekt keine oder mehrere der angeforderten Eigenschaften enthält, die von der `properties` Abfrage angegeben werden, gibt die Antwort nur die angeforderten Eigenschaften zurück, die es enthält, wie unten unter &quot;Beispiel-Datensatz 3&quot;und &quot;Beispiel-Datensatz 4&quot;dargestellt.

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
