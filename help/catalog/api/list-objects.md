---
keywords: Experience Platform;Startseite;beliebte Themen;filter;filter;filter;daten filtern;daten filtern
solution: Experience Platform
title: Katalogobjekte auflisten
description: Sie können über einen einzigen API-Aufruf eine Liste aller verfügbaren Objekte eines bestimmten Typs abrufen. Es empfiehlt sich, Filter einzubeziehen, um die Größe der Antwort beschränken.
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 409d052c119814a1cf6b79ff4448d1100b18e199
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
| `{OBJECT_TYPE}` | Der Typ [!DNL Catalog] aufzulistenden Objekts. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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

Eine erfolgreiche Antwort gibt eine Liste von [!DNL Catalog]-Objekten in Form von Schlüssel-Wert-Paaren zurück, die nach den in der Anfrage angegebenen Abfrageparametern gefiltert werden. Für jedes Schlüssel-Wert-Paar stellt der Schlüssel eine eindeutige Kennung für das betreffende [!DNL Catalog]-Objekt dar, die dann in einem anderen Aufruf verwendet werden kann, um [dieses spezifische Objekt anzuzeigen](look-up-object.md) um weitere Details zu erhalten.

>[!NOTE]
>
>Wenn ein zurückgegebenes Objekt keine oder mehrere der angeforderten Eigenschaften enthält, die in der `properties` Abfrage angegeben werden, gibt die Antwort nur die angeforderten Eigenschaften zurück, die es enthält, wie in ***`Sample Dataset 3`*** und ***`Sample Dataset 4`*** unten dargestellt.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSetFiles?dataSetId=5bda3a4228babc0000126377"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bde21511dd27b0000d24e95"
    }
}
```
