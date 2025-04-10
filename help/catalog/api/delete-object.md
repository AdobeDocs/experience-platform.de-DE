---
keywords: Experience Platform;Startseite;beliebte Themen;Objekt löschen;Katalog-Service;API
solution: Experience Platform
title: Löschen eines Objekts in der API
description: Sie können ein Katalogobjekt löschen, indem Sie dessen ID im Pfad einer DELETE-Anfrage angeben.
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: d88336d314e767a068ef6524161baeb642a58433
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 48%

---

# Löschen eines Objekts in der API

Sie können ein [!DNL Catalog]-Objekt löschen, indem Sie seine ID im Pfad einer DELETE-Anfrage angeben.

>[!WARNING]
>
>Seien Sie beim Löschen von Objekten besonders vorsichtig, da dies nicht rückgängig gemacht werden kann und an anderer Stelle in [!DNL Experience Platform] zu grundlegenden Änderungen führen kann.

**API-Format**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>Der `DELETE /batches/{ID}`-Endpunkt wird nicht mehr unterstützt. Um einen Batch zu löschen, sollten Sie die [Batch-Aufnahme-API“ ](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ [!DNL Catalog] zu löschenden Objekts. Gültige Objekte sind: <ul><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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
>Wenn keine [!DNL Catalog] Objekte mit der in Ihrer Anfrage angegebenen ID übereinstimmen, erhalten Sie möglicherweise trotzdem den HTTP-Status-Code 200, aber das Antwort-Array ist leer.
