---
keywords: Experience Platform; Startseite; beliebte Themen; Löschen eines Objekts; Katalogdienst; API
solution: Experience Platform
title: Löschen eines Objekts in der API
topic-legacy: developer guide
description: Sie können ein Katalogobjekt löschen, indem Sie dessen ID im Pfad einer DELETE-Anfrage angeben.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 47%

---

# Löschen eines Objekts in der API

Sie können eine [!DNL Catalog] -Objekt, indem Sie die Kennung im Pfad einer DELETE-Anfrage angeben.

>[!WARNING]
>
>Seien Sie besonders vorsichtig beim Löschen von Objekten, da dies nicht rückgängig gemacht werden kann und andernorts in [!DNL Experience Platform].

**API-Format**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>Die `DELETE /batches/{ID}` -Endpunkt wird nicht mehr unterstützt. Um einen Batch zu löschen, sollten Sie die [Batch-Aufnahme-API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt, das gelöscht werden soll. Gültige Objekte sind: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Die Kennung des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Mit der folgenden Anfrage wird ein Datensatz gelöscht, dessen ID im Anfragepfad angegeben ist.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>Wenn nicht [!DNL Catalog] -Objekte mit der in Ihrer Anfrage angegebenen ID übereinstimmen, erhalten Sie möglicherweise weiterhin einen HTTP-Status-Code 200, das Antwort-Array ist jedoch leer.
