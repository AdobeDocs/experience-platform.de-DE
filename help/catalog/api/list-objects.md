---
keywords: Experience Platform; Startseite; beliebte Themen; Filter; Filtern; Filtern von Daten; Filtern von Daten
solution: Experience Platform
title: Katalogobjekte auflisten
description: Sie können über einen einzigen API-Aufruf eine Liste aller verfügbaren Objekte eines bestimmten Typs abrufen. Es empfiehlt sich, Filter einzubeziehen, um die Größe der Antwort beschränken.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 53%

---

# Katalogobjekte auflisten

Sie können über einen einzigen API-Aufruf eine Liste aller verfügbaren Objekte eines bestimmten Typs abrufen. Es empfiehlt sich, Filter einzubeziehen, um die Größe der Antwort beschränken.

**API-Format**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt, das aufgeführt werden soll. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Ein Abfrageparameter, mit dem die in der Antwort zurückgegebenen Ergebnisse gefiltert werden. Mehrere Parameter werden durch das kaufmännische Und-Zeichen (`&`) getrennt. Weiterführende Informationen finden Sie im Handbuch zum [Filtern von Katalogdaten](filter-data.md). |

**Anfrage**

Die unten stehende Musteranfrage ruft eine Liste von Datensätzen ab, mit einem `limit`-Filter, der die Antwort auf fünf Ergebnisse reduziert, und einem `properties`-Filter, der die für die einzelnen Datensätze angezeigten Eigenschaften begrenzt.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von [!DNL Catalog] -Objekte in Form von Schlüssel-Wert-Paaren, gefiltert durch die in der Anfrage angegebenen Abfrageparameter. Für jedes Schlüssel-Wert-Paar stellt der Schlüssel eine eindeutige Kennung für die [!DNL Catalog] -Objekt, das dann in einem anderen Aufruf an verwendet werden kann [Anzeigen eines bestimmten Objekts](look-up-object.md) für weitere Details.

>[!NOTE]
>
>Wenn ein zurückgegebenes Objekt keine der angeforderten Eigenschaften enthält, die durch die Variable `properties` -Abfrage, gibt die Antwort nur die angeforderten Eigenschaften zurück, die sie enthält, wie in ***`Sample Dataset 3`*** und ***`Sample Dataset 4`*** unten.

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
