---
keywords: Experience Platform;home;popular topics;catalog;multiple object lookup;api
solution: Experience Platform
title: Suchen nach mehreren Katalogobjekten
description: Wenn Sie mehrere bestimmte Objekte anzeigen möchten, anstatt eine Anfrage pro Objekt zu stellen, bietet der Katalog eine einfache Verknüpfung zum Anfordern mehrerer Objekte desselben Typs. Sie können eine GET-Anfrage verwenden, um mehrere bestimmte Objekte zurückzugeben, indem Sie eine durch Komma getrennte Liste von IDs einschließen.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 99837f7aa803f3f992dce2127089bff6279c7008
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 49%

---

# Suchen nach mehreren Katalogobjekten

Wenn Sie mehrere spezifische Objekte anzeigen möchten, anstatt eine Anfrage pro Objekt zu stellen, [!DNL Catalog] bietet eine einfache Verknüpfung zum Anfordern mehrerer Objekte desselben Typs. Sie können eine GET-Anfrage verwenden, um mehrere bestimmte Objekte zurückzugeben, indem Sie eine durch Komma getrennte Liste von IDs einschließen.

>[!NOTE]
>
>Auch wenn bestimmte [!DNL Catalog] -Objekte, empfiehlt es sich weiterhin, `properties` -Abfrageparameter, um nur die benötigten Eigenschaften zurückzugeben.

**API-Format**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt abgerufen werden. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{ID}` | Eine Kennung für eines der spezifischen Objekte, die Sie abrufen möchten. |

**Anfrage**

Die folgende Anfrage enthält eine durch Kommas getrennte Liste von Datensatz-IDs sowie eine durch Kommas getrennte Liste von Eigenschaften, die für jeden Datensatz zurückgegeben werden sollen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste der angegebenen Datensätze zurück, die nur die angeforderten Eigenschaften (`name`, `description` und `files`) enthält.

>[!NOTE]
>
>Wenn ein zurückgegebenes Objekt nicht eine oder mehrere der angeforderten Eigenschaften enthält, die durch die Variable `properties` -Abfrage, gibt die Antwort nur die angeforderten Eigenschaften zurück, die sie enthält, wie in ***`Sample Dataset 3`*** und ***`Sample Dataset 4`*** unten.

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
