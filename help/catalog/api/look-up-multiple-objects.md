---
keywords: Experience Platform; Startseite; beliebte Themen; Katalog; Suche mehrerer Objekte; API
solution: Experience Platform
title: Suchen nach mehreren Katalogobjekten
description: Wenn Sie mehrere bestimmte Objekte anzeigen möchten, anstatt eine Anfrage pro Objekt zu stellen, bietet der Katalog eine einfache Verknüpfung zum Anfordern mehrerer Objekte desselben Typs. Sie können eine GET-Anfrage verwenden, um mehrere bestimmte Objekte zurückzugeben, indem Sie eine durch Komma getrennte Liste von IDs einschließen.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 2226b1878ef3398554b6cf96ff400cc1767a9e4c
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 54%

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
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt, das abgerufen werden soll. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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
