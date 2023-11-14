---
keywords: Experience Platform;home;popular topics;catalog;object lookup;api
solution: Experience Platform
title: Nachschlagen eines Katalogobjekts
description: Wenn Sie die eindeutige Kennung eines bestimmten Catalog-Objekts kennen, können Sie eine GET-Anfrage ausführen, um Details zu diesem Objekt anzuzeigen.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 2226b1878ef3398554b6cf96ff400cc1767a9e4c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 63%

---

# Nachschlagen eines Katalogobjekts

Wenn Sie die eindeutige Kennung für eine bestimmte [!DNL Catalog] -Objekt, können Sie eine GET-Anfrage ausführen, um die Details dieses Objekts anzuzeigen.

>[!NOTE]
>
>Beim Anzeigen einzelner Objekte empfiehlt es sich weiterhin, [nach Eigenschaften zu filtern](filter-data.md), um nur die Eigenschaften zurückzugeben, die Sie von Interesse sind.

**API-Format**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt abgerufen werden. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Die Kennung des spezifischen Objekts, das Sie abrufen möchten. |

**Anfrage**

Die folgende Anfrage ruft einen Datensatz anhand seiner Kennung ab und gibt dessen `name`, `description`, `tags`, und `files` Eigenschaften.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der angegebene Datensatz nur mit den angeforderten `properties` im Text zurückgegeben.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE]
>
> Eigenschaften, deren Werte mit einem `@`-Präfix versehen sind, stellen miteinander verknüpfte Objekte dar. Anweisungen zum Anzeigen dieser Objekte finden Sie im Anhangsbereich zum [Anzeigen von miteinander verknüpften Objekten](appendix.md#view-interrelated-objects).
