---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Aktualisieren eines Objekts
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 89%

---


# Aktualisieren eines Objekts

You can update part of a [!DNL Catalog] object by including its ID in the path of a PATCH request. In diesem Dokument werden die beiden Methoden zum Ausführen von PATCH-Vorgängen für Katalogobjekte behandelt:

* Verwenden von Feldern
* Verwenden der JSON Patch-Notation

>[!NOTE]
>
>PATCH-Vorgänge können die erweiterbaren Felder eines Objekts, die miteinander verknüpfte Objekte darstellen, nicht ändern.  Änderungen an verknüpften Objekten müssen direkt vorgenommen werden.

## Aktualisieren mithilfe von Feldern

Der folgende Beispielaufruf zeigt, wie ein Objekt mithilfe von Feldern und Werten aktualisiert wird.

**API-Format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | The type of [!DNL Catalog] object to be updated. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Die Kennung des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert die `name`- und `description`-Felder eines Datensatzes auf die in der Payload bereitgestellten Werte. Objektfelder, die nicht aktualisiert werden sollen, können von der Payload ausgeschlossen werden.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des aktualisierten Datensatzes enthält. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die Ausführung einer GET-Anfrage für diesen Datensatz zeigt jetzt, dass nur `name` und `description` aktualisiert wurden, während alle anderen Werte unverändert bleiben.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Aktualisieren mithilfe der JSON Patch-Notation

Der folgende Beispielaufruf zeigt, wie ein Objekt, wie in [RFC-6902](https://tools.ietf.org/html/rfc6902) beschrieben, mit JSON Patch aktualisiert wird.

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API-Format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | The type of [!DNL Catalog] object to be updated. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Die Kennung des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert die `name`- und `description`-Felder eines Datensatzes auf die Werte, die in jedem JSON Patch-Objekt angegeben sind. Bei Verwendung von JSON Patch müssen Sie auch die Kopfzeile für den Inhaltstyp auf `application/json-patch+json` setzen.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des aktualisierten Objekts enthält. Diese ID sollte mit der in der PATCH-Anfrage gesendeten ID übereinstimmen. Die Ausführung einer GET-Anfrage für dieses Objekt zeigt jetzt, dass nur `name` und `description` aktualisiert wurden, während alle anderen Werte unverändert bleiben.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
