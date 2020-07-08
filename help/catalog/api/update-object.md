---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Objekt aktualisieren
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 3%

---


# Objekt aktualisieren

Sie können einen Teil eines Katalogobjekts aktualisieren, indem Sie dessen ID in den Pfad einer PATCH-Anforderung einschließen. Dieses Dokument behandelt die beiden Methoden zum Ausführen von PATCH-Vorgängen für Katalogobjekte:

* Felder verwenden
* Verwenden der JSON-Patch-Notation

>[!NOTE]
>
>PATCH-Vorgänge an einem Objekt können seine erweiterbaren Felder, die miteinander verknüpfte Objekte darstellen, nicht ändern.  Änderungen an verknüpften Objekten müssen direkt vorgenommen werden.

## Aktualisieren mit Feldern

Der folgende Beispielaufruf zeigt, wie ein Objekt mithilfe von Feldern und Werten aktualisiert wird.

**API-Format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des zu aktualisierenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Der Bezeichner des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anforderung aktualisiert die `name` und die `description` Felder eines Datensatzes auf die in der Nutzlast bereitgestellten Werte. Objektfelder, die nicht aktualisiert werden sollen, können aus der Nutzlast ausgeschlossen werden.

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

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des aktualisierten Datensatzes enthält. Diese ID sollte mit der in der PATCH-Anforderung gesendeten ID übereinstimmen. Die Ausführung einer GET-Anforderung für diesen Datensatz zeigt jetzt, dass nur die Werte `name` und aktualisiert wurden, während alle anderen Werte unverändert bleiben, `description` während die Werte aktualisiert wurden.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Aktualisieren mit JSON-Patch-Notation

Der folgende Beispielaufruf zeigt, wie ein Objekt mit dem JSON-Patch aktualisiert wird, wie in [RFC-6902](https://tools.ietf.org/html/rfc6902)beschrieben.

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API-Format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des zu aktualisierenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | Der Bezeichner des spezifischen Objekts, das Sie aktualisieren möchten. |

**Anfrage**

Mit der folgenden Anforderung werden die Werte `name` und `description` Felder eines Datensatzes auf die Werte der JSON Patch-Objekte aktualisiert. Bei Verwendung von JSON Patch müssen Sie auch die Content-Type-Kopfzeile auf `application/json-patch+json`.

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

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des aktualisierten Objekts enthält. Diese ID sollte mit der in der PATCH-Anforderung gesendeten ID übereinstimmen. Die Ausführung einer GET-Anforderung für dieses Objekt zeigt jetzt, dass nur die Werte `name` und aktualisiert wurden, während alle anderen Werte unverändert bleiben. `description`

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
