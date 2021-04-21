---
keywords: Experience Platform;Startseite;beliebte Themen;Katalog;Suche nach mehreren Objekten;API
solution: Experience Platform
title: Mehrere Katalogobjekte suchen
topic-legacy: developer guide
description: Wenn Sie mehrere bestimmte Objekte anzeigen möchten, anstatt eine Anfrage pro Objekt zu stellen, bietet der Katalog eine einfache Verknüpfung zum Anfordern mehrerer Objekte desselben Typs. Sie können eine GET-Anfrage verwenden, um mehrere bestimmte Objekte zurückzugeben, indem Sie eine durch Komma getrennte Liste von IDs einschließen.
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 54%

---

# Mehrere Katalogobjekte suchen

Wenn Sie anstelle einer Anforderung pro Objekt mehrere bestimmte Objekte Ansicht haben möchten, stellt [!DNL Catalog] eine einfache Verknüpfung zum Anfordern mehrerer Objekte desselben Typs bereit. Sie können eine GET-Anfrage verwenden, um mehrere bestimmte Objekte zurückzugeben, indem Sie eine durch Komma getrennte Liste von IDs einschließen.

>[!NOTE]
>
>Auch wenn Sie bestimmte [!DNL Catalog]-Objekte anfordern, ist es immer noch empfehlenswert, den Parameter `properties` &quot;Abfrage&quot;so zu verwenden, dass nur die benötigten Eigenschaften zurückgegeben werden.

**API-Format**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden [!DNL Catalog]-Objekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | Eine Kennung für eines der spezifischen Objekte, die Sie abrufen möchten. |

**Anfrage**

Die folgende Anfrage enthält eine durch Kommas getrennte Liste von Datensatz-IDs sowie eine durch Kommas getrennte Liste von Eigenschaften, die für jeden Datensatz zurückgegeben werden sollen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste der angegebenen Datensätze zurück, die nur die angeforderten Eigenschaften (`name`, `description` und `files`) enthält.

>[!NOTE]
>
>Wenn ein zurückgegebenes Objekt nicht mehr als eine der angeforderten Eigenschaften enthält, die durch die `properties`-Abfrage angegeben werden, gibt die Antwort nur die angeforderten Eigenschaften zurück, die darin enthalten sind, wie unten unter ***`Sample Dataset 3`*** und ***`Sample Dataset 4`*** dargestellt.

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
