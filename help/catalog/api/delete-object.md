---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Löschen eines Objekts
topic: developer guide
translation-type: tm+mt
source-git-commit: 6c17351b04fedefd4b57b9530f1d957da8183a68
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 2%

---


# Löschen eines Objekts

Sie können ein Katalogobjekt löschen, indem Sie dessen ID im Pfad einer DELETE-Anforderung angeben.

>[!WARNING] Gehen Sie beim Löschen von Objekten besonders vorsichtig vor, da dies nicht rückgängig gemacht werden kann und andernorts in der Experience Platform zu unerwarteten Änderungen führen kann.

**API-Format**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT] Der `DELETE /batches/{ID}` Endpunkt wurde nicht mehr unterstützt. Um einen Stapel zu löschen, sollten Sie die [Stapelverarbeitungs-API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)verwenden.

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des zu löschenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Der Bezeichner des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Mit der folgenden Anforderung wird ein Datensatz gelöscht, dessen ID im Anforderungspfad angegeben ist.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) und ein Array mit der ID des gelöschten Datensatzes zurück. Diese ID sollte mit der ID übereinstimmen, die in der DELETE-Anforderung gesendet wurde. Wenn Sie eine GET-Anforderung für das gelöschte Objekt ausführen, wird der HTTP-Status 404 (Nicht gefunden) zurückgegeben und bestätigt, dass der Datensatz erfolgreich gelöscht wurde.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE] Wenn keine Katalogobjekte mit der in Ihrer Anforderung angegebenen ID übereinstimmen, erhalten Sie möglicherweise trotzdem einen HTTP-Statuscode 200, aber das Antwortarray ist leer.
