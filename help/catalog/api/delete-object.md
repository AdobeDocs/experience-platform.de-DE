---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Löschen eines Objekts
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 50%

---


# Löschen eines Objekts

You can delete a [!DNL Catalog] object by providing its ID in the path of a DELETE request.

>[!WARNING]
>
>Take extra care when deleting objects, as this cannot be undone and may produce breaking changes elsewhere in [!DNL Experience Platform].

**API-Format**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>Der `DELETE /batches/{ID}` Endpunkt wurde nicht mehr unterstützt. Um einen Stapel zu löschen, sollten Sie die [Stapelverarbeitungs-API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)verwenden.

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | The type of [!DNL Catalog] object to be deleted. Gültige Objekte sind: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Die Kennung des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Mit der folgenden Anfrage wird ein Datensatz gelöscht, dessen ID im Anfragepfad angegeben ist.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) und ein Array mit der ID des gelöschten Datensatzes zurück. Diese ID sollte mit der in der DELETE-Anfrage gesendeten ID übereinstimmen. Wenn Sie eine GET-Anfrage für das gelöschte Objekt ausführen, wird der HTTP-Status 404 (Nicht gefunden) zurückgegeben. Damit wird bestätigt, dass der Datensatz erfolgreich gelöscht wurde.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>If no [!DNL Catalog] objects match the ID provided in your request, you may still receive an HTTP Status Code 200, but the response array will be empty.
