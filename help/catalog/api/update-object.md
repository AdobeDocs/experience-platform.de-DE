---
keywords: Experience Platform;Startseite;beliebte Themen;Katalog;API;Objekt aktualisieren
solution: Experience Platform
title: Aktualisieren eines Katalogobjekts
description: Sie können einen Teil eines Katalogobjekts aktualisieren, indem Sie dessen ID in den Pfad einer PATCH-Anfrage einschließen. In diesem Dokument wird die Verwendung von Feldern und die Verwendung der JSON-Patch-Notation für die Durchführung von PATCH-Vorgängen für Katalogobjekte beschrieben.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 5534cd5d5b0122ccbfcb3bae6c664c9f2d6eda8a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 41%

---

# Aktualisieren eines Catalog-Objekts

Sie können einen Teil eines [!DNL Catalog]-Objekts aktualisieren, indem Sie seine ID im Pfad einer PATCH-Anfrage angeben. In diesem Dokument werden die beiden Methoden zum Ausführen von PATCH-Vorgängen für Katalogobjekte behandelt:

* Verwenden von Feldern
* Verwenden der JSON Patch-Notation

>[!NOTE]
>
>PATCH-Vorgänge für ein Objekt können seine erweiterbaren Felder, die miteinander verknüpfte Objekte darstellen, nicht ändern. Änderungen an verknüpften Objekten müssen direkt vorgenommen werden.

## Aktualisieren mithilfe von Feldern

Der folgende Beispielaufruf zeigt, wie ein Objekt mithilfe von Feldern und Werten aktualisiert wird.

**API-Format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ [!DNL Catalog] zu aktualisierenden Objekts. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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

## Aktualisieren mithilfe der JSON Patch-Notation {#patch-notation}

Der folgende Beispielaufruf zeigt, wie ein Objekt, wie in [RFC-6902](https://tools.ietf.org/html/rfc6902) beschrieben, mit JSON Patch aktualisiert wird.

Weitere Informationen zur JSON-Patch-Syntax finden Sie im [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-patch).

**API-Format**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ [!DNL Catalog] zu aktualisierenden Objekts. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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

## Aktualisieren mit der PATCH v2-Notation {#patch-v2-notation}

Der `/v2/dataSets/{DATASET_ID}`-Endpunkt bietet eine flexiblere Möglichkeit, komplexe oder tief verschachtelte Datensatzattribute zu aktualisieren.

Wenn Sie ein tief verschachteltes Feld aktualisieren (z. B. `a.b.c.d`), muss in der Regel jede Ebene im Pfad bereits vorhanden sein. Wenn eine Ebene fehlt, müssen Sie jede manuell erstellen, bevor Sie den endgültigen Wert festlegen. Dies erfordert häufig mehrere Vorgänge, was die Komplexität erhöht und die Wahrscheinlichkeit von Fehlern erhöht.

Der `/v2/dataSets/{DATASET_ID}`-Endpunkt erstellt automatisch alle fehlenden Ebenen im Pfad. Anstatt `b` und `c` vor dem Festlegen von `d` manuell zu überprüfen und hinzuzufügen, erledigt der PATCH-`v2` dies für Sie.

Wenn Sie eine PATCH-Anfrage an den `/v2/dataSets/{DATASET_ID}`-Endpunkt senden, müssen Sie nur die endgültige Struktur senden, und das System füllt die fehlenden Teile aus, bevor Sie die Aktualisierung anwenden.

>[!NOTE]
>
>`If-Match`- und `If-None-Match`-Kopfzeilen sind für den `/v2/dataSets/{id}`-Endpunkt optional. PATCH-Anfragen an diesen Endpunkt führen Aktualisierungen dynamisch zusammen, sodass Änderungen möglich sind, ohne die neueste Datensatzversion abzurufen. Dadurch wird zwar das Risiko von Datenverlusten durch gleichzeitige Updates reduziert, Sie können jedoch `If-Match` mit den neuesten `etag` verwenden, um sicherzustellen, dass Änderungen nur für eine bestimmte Version gelten. Alternativ verhindert `If-None-Match` Aktualisierungen, wenn sich der Datensatz seit der letzten bekannten Version nicht geändert hat.

**API-Format**

```http
PATCH /V2/DATASETS/{DATASET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Die Kennung des zu aktualisierenden Datensatzes. |

**Anfrage**

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/v2/dataSets/67b3077efa10d92ab7a71858 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P9Y"
            }
            }
        }
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein -Array zurück, das die ID des aktualisierten Datensatzes enthält, der mit der in der PATCH-Anfrage gesendeten ID übereinstimmen sollte. Wenn Sie eine GET-Anfrage für dieses Objekt ausführen, wird jetzt angezeigt, dass das `extensions.adobe_lakeHouse.rowExpiration`-Objekt ohne vorherige manuelle Erstellungsschritte erstellt wurde.

```json
[
    "@/dataSets/67b3077efa10d92ab7a71858"
]
```

### Ein Beispieldatensatz vor und nach der Aktualisierung

Das folgende JSON-Beispiel veranschaulicht die Datensatzstruktur **vor** der PATCH-Anfrage, bei der das `extensions.adobe_lakeHouse.rowExpiration`-Objekt nicht im Datensatz vorhanden ist.

+++Beispiel auswählen, um es anzuzeigen

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "createdUser": "{USER_ID}",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "extensions": {
            "adobe_lakeHouse": {},
            "adobe_unifiedProfile": {}
        },
        "created": 1739786110978,
        "updated": 1739786111203,
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed+json; version=1"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "GEN2",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

Die folgende JSON-Datei zeigt die Datensatzstruktur **nach** der PATCH-Anfrage. Das Update erstellt automatisch das fehlende `extensions.adobe_lakeHouse.rowExpiration`-Objekt ohne vorherige manuelle Erstellungsschritte. Dieses Beispiel zeigt, wie die `/v2/` PATCH-Anfrage mehrere Vorgänge überflüssig macht und Aktualisierungen einfacher und effizienter werden.


+++Beispiel auswählen, um es anzuzeigen

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                    "ttlValue": "{TTL_VALUE}"
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "{VERSION}",
        "created": "{CREATED_TIMESTAMP}",
        "updated": "{UPDATED_TIMESTAMP}",
        "createdClient": "{CLIENT_ID}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "{CONTENT_TYPE}"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "{STORAGE_TYPE}",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++
