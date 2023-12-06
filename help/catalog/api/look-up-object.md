---
keywords: Experience Platform;home;popular topics;catalog;object lookup;api
solution: Experience Platform
title: Nachschlagen eines Katalogobjekts
description: Wenn Sie die eindeutige Kennung eines bestimmten Catalog-Objekts kennen, können Sie eine GET-Anfrage ausführen, um Details zu diesem Objekt anzuzeigen.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 0331b6bbd22255cab92c93070dda1ffaed5bbbcb
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 44%

---

# Nachschlagen eines Katalogobjekts

Wenn Sie die eindeutige Kennung für eine bestimmte [!DNL Catalog] -Objekt, können Sie eine GET-Anfrage ausführen, um die Details dieses Objekts anzuzeigen.

>[!NOTE]
>
>Beim Anzeigen bestimmter Objekte empfiehlt es sich weiterhin, [nach Eigenschaften filtern](filter-data.md) und geben nur die Eigenschaften zurück, die Sie interessieren.

**API-Format**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt abgerufen werden. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }
}
```

>[!NOTE]
>
>Eigenschaften, deren Werte mit dem Präfix `@` stellen miteinander verknüpfte Objekte dar. Anweisungen zum Anzeigen dieser Objekte finden Sie im Anhangsbereich zum [Anzeigen von miteinander verknüpften Objekten](appendix.md#view-interrelated-objects).
