---
keywords: Experience Platform;home;popular topics;catalog;api;Objekt aktualisieren
solution: Experience Platform
title: Aktualisieren eines Katalogobjekts
description: Sie können einen Teil eines Katalogobjekts aktualisieren, indem Sie dessen ID in den Pfad einer PATCH-Anfrage einschließen. Dieses Dokument behandelt die Verwendung von Feldern und die Verwendung der JSON Patch-Notation zum Ausführen von PATCH-Vorgängen für Catalog-Objekte.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 2226b1878ef3398554b6cf96ff400cc1767a9e4c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 81%

---

# Aktualisieren eines Katalogobjekts

Sie können einen Teil eines [!DNL Catalog] -Objekt, indem die zugehörige ID in den Pfad einer PATCH-Anfrage aufgenommen wird. In diesem Dokument werden die beiden Methoden zum Ausführen von PATCH-Vorgängen für Katalogobjekte behandelt:

* Verwenden von Feldern
* Verwenden der JSON Patch-Notation

>[!NOTE]
>
> PATCH-Vorgänge können die erweiterbaren Felder eines Objekts, die miteinander verknüpfte Objekte darstellen, nicht ändern. Änderungen an verknüpften Objekten müssen direkt vorgenommen werden.

## Aktualisieren mithilfe von Feldern

Der folgende Beispielaufruf zeigt, wie ein Objekt mithilfe von Feldern und Werten aktualisiert wird.

**API-Format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt zu aktualisieren. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Die Kennung des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert die `name`- und `description`-Felder eines Datensatzes auf die in der Payload bereitgestellten Werte. Objektfelder, die nicht aktualisiert werden sollen, können von der Payload ausgeschlossen werden.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt zu aktualisieren. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Die Kennung des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert die `name`- und `description`-Felder eines Datensatzes auf die Werte, die in jedem JSON Patch-Objekt angegeben sind. Bei Verwendung von JSON Patch müssen Sie auch die Kopfzeile für den Inhaltstyp auf `application/json-patch+json` setzen.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
