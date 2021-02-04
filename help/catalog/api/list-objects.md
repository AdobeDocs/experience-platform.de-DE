---
keywords: Experience Platform;Startseite;beliebte Themen;Filter;Filter;Daten filtern;Daten filtern;Daten filtern
solution: Experience Platform
title: Objekte auflisten
topic: developer guide
description: Sie können über einen einzigen API-Aufruf eine Liste aller verfügbaren Objekte eines bestimmten Typs abrufen. Es empfiehlt sich, Filter einzubeziehen, um die Größe der Antwort beschränken.
translation-type: tm+mt
source-git-commit: c081a7521be9715ca32d35504922a70767924fd7
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 55%

---


# Objekte auflisten

Sie können über einen einzigen API-Aufruf eine Liste aller verfügbaren Objekte eines bestimmten Typs abrufen. Es empfiehlt sich, Filter einzubeziehen, um die Größe der Antwort beschränken.

**API-Format**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des anzuzeigenden [!DNL Catalog]-Objekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | Ein Abfrageparameter, mit dem die in der Antwort zurückgegebenen Ergebnisse gefiltert werden. Mehrere Parameter werden durch das kaufmännische Und-Zeichen (`&`) getrennt. Weiterführende Informationen finden Sie im Handbuch zum [Filtern von Katalogdaten](filter-data.md). |

**Anfrage**

Die unten stehende Musteranfrage ruft eine Liste von Datensätzen ab, mit einem `limit`-Filter, der die Antwort auf fünf Ergebnisse reduziert, und einem `properties`-Filter, der die für die einzelnen Datensätze angezeigten Eigenschaften begrenzt.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von [!DNL Catalog]-Objekten in Form von Schlüssel-Wert-Paaren zurück, gefiltert nach den in der Anforderung bereitgestellten Abfragen. Für jedes Schlüssel-Wert-Paar stellt der Schlüssel einen eindeutigen Bezeichner für das fragliche [!DNL Catalog]-Objekt dar, der dann in einem anderen Aufruf von [Ansicht dieses bestimmten Objekts](look-up-object.md) verwendet werden kann, um weitere Informationen zu erhalten.

>[!NOTE]
>
>Wenn ein zurückgegebenes Objekt keine oder mehrere der angeforderten Eigenschaften enthält, die durch die `properties`-Abfrage angegeben werden, gibt die Antwort nur die angeforderten Eigenschaften zurück, die sie enthält, wie unten unter ***`Sample Dataset 3`*** und ***`Sample Dataset 4`*** dargestellt.

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
