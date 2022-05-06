---
keywords: Experience Platform; Startseite; beliebte Themen; Katalog; Objektsuche; API
solution: Experience Platform
title: Nachschlagen eines Katalogobjekts
topic-legacy: developer guide
description: Wenn Sie die eindeutige Kennung eines bestimmten Catalog-Objekts kennen, können Sie eine GET-Anfrage ausführen, um Details zu diesem Objekt anzuzeigen.
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 71%

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
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt, das abgerufen werden soll. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Die Kennung des spezifischen Objekts, das Sie abrufen möchten. |

**Anfrage**

Mit der folgenden Anfrage wird ein Datensatz anhand seiner Kennung abgerufen und werden die zugehörigen Eigenschaften `name`, `description`, `state`, `tags` und `files` zurückgegeben.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
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
        "state": "DRAFT",
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
