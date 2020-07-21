---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über den Datenzugriff
topic: tutorial
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 14%

---


# Abfrage von Datensatzdaten mit [!DNL Data Access] API

Dieses Dokument bietet eine schrittweise Anleitung zum Auffinden, Zugreifen und Herunterladen von Daten, die in einem Datensatz mit der [!DNL Data Access] API in der Adobe Experience Platform gespeichert sind. Außerdem werden Sie mit einigen der einzigartigen Funktionen der [!DNL Data Access] API, wie z. B. dem Paging und Teildownloads, vorgestellt.

## Erste Schritte

In diesem Lernprogramm erfahren Sie, wie Sie einen Datensatz erstellen und ausfüllen. Weitere Informationen finden Sie im Tutorial [zur Erstellung von](../../catalog/datasets/create.md) Datensätzen.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platform-APIs erfolgreich aufrufen zu können.

### Lesehilfe für Beispiel-API-Aufrufe

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

### Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Alle Anfragen, die eine Payload enthalten (also POST-, PUT- und PATCH-Anfragen), erfordern eine zusätzliche Kopfzeile:

- Content-Type: application/json

## Sequenzdiagramm

Dieses Tutorial folgt den Schritten, die im folgenden Sequenzdiagramm beschrieben werden, und hebt die Kernfunktionalität der [!DNL Data Access] API hervor.</br>
![](../images/sequence_diagram.png)

Mit der [!DNL Catalog] API können Sie Informationen zu Stapeln und Dateien abrufen. Mit der [!DNL Data Access] API können Sie je nach Dateigröße entweder als vollständige oder teilweise Downloads über HTTP auf diese Dateien zugreifen und sie herunterladen.

## Daten suchen

Bevor Sie mit der Verwendung der [!DNL Data Access] API beginnen können, müssen Sie den Speicherort der Daten identifizieren, auf die Sie zugreifen möchten. In der [!DNL Catalog] API gibt es zwei Endpunkte, mit denen Sie die Metadaten eines Unternehmens durchsuchen und die ID eines Stapels oder einer Datei abrufen können, auf den Sie zugreifen möchten:

- `GET /batches`: Gibt eine Liste von Stapeln unter Ihrer Organisation zurück
- `GET /dataSetFiles`: Gibt eine Liste von Dateien in Ihrem Unternehmen zurück

Eine umfassende Liste der Endpunkte in der [!DNL Catalog] API finden Sie in der [API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

## Abrufen einer Liste von Stapeln unter Ihrer IMS-Organisation

Mithilfe der [!DNL Catalog] API können Sie eine Liste von Stapeln aus Ihrem Unternehmen zurückgeben:

**API-Format**

```http
GET /batches
```

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort enthält ein Objekt, das Listen aller Stapel im Zusammenhang mit der IMS-Organisation enthält, wobei jeder Wert der obersten Ebene einen Stapel darstellt. Die einzelnen Stapelobjekte enthalten die Details zu diesem Stapel. Die unten stehende Antwort wurde aus Platzgründen minimiert.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### Filtern der Liste von Stapeln

Filter müssen oft einen bestimmten Stapel finden, um relevante Daten für einen bestimmten Verwendungsfall abrufen zu können. Parameter können einer `GET /batches` Anforderung hinzugefügt werden, um die zurückgegebene Antwort zu filtern. Die unten stehende Anforderung gibt alle nach einer bestimmten Zeit erstellten Stapel innerhalb eines bestimmten Datensatzes zurück, sortiert nach dem Zeitpunkt ihrer Erstellung.

**API-Format**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{START_TIMESTAMP}` | Der Zeitstempel des Beginns in Millisekunden (z. B. 1514836799000). |
| `{DATASET_ID}` | Die ID des Datensatzes. |
| `{SORT_BY}` | Sortiert die Antwort nach dem bereitgestellten Wert. Die Objekte werden beispielsweise `desc:created` nach Erstellungsdatum in absteigender Reihenfolge sortiert. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{IMS_ORG}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{IMS_ORG}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

Eine vollständige Liste von Parametern und Filtern finden Sie in der [Katalog-API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

## Abrufen einer Liste aller Dateien eines bestimmten Stapels

Nachdem Sie nun die ID des Stapels haben, auf den Sie zugreifen möchten, können Sie die [!DNL Data Access] API verwenden, um eine Liste von Dateien zu diesem Stapel zu erhalten.

**API-Format**

```http
GET /batches/{BATCH_ID}/files
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Stapelkennung des Stapels, auf den Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data._links.self.href` | Die URL für den Zugriff auf diese Datei. |

Die Antwort enthält ein Datenarray, das alle Dateien im angegebenen Stapel Liste. Dateien werden durch ihre Datei-ID referenziert, die sich unter dem `dataSetFileId` Feld befindet.

## Zugriff auf eine Datei mit einer Datei-ID

Sobald Sie über eine eindeutige Datei-ID verfügen, können Sie mit der [!DNL Data Access] API auf die spezifischen Details zur Datei zugreifen, einschließlich Name, Größe in Byte und Link zum Herunterladen.

**API-Format**

```http
GET /files/{FILE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Die ID der Datei, auf die Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Je nachdem, ob die Datei-ID auf eine einzelne Datei oder einen Ordner verweist, kann das zurückgegebene Datenarray einen einzelnen Eintrag oder eine Liste von Dateien enthalten, die zu diesem Ordner gehören. Jedes Dateielement enthält Details wie den Namen der Datei, die Größe in Byte und einen Link zum Herunterladen der Datei.

**Fall 1: Datei-ID verweist auf eine einzelne Datei**

**Antwort**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | Der Name der Datei. |
| `_links.self.href` | Die URL zum Herunterladen der Datei. |

**Fall 2: Datei-ID verweist auf ein Verzeichnis**

**Antwort**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `data._links.self.href` | Die URL zum Herunterladen der zugehörigen Datei. |

Diese Antwort gibt einen Ordner mit zwei separaten Dateien mit IDs `{FILE_ID_2}` und `{FILE_ID_3}`zurück. In diesem Szenario müssen Sie die URL der einzelnen Dateien befolgen, um auf die Datei zugreifen zu können.

## Abrufen der Metadaten einer Datei

Sie können die Metadaten einer Datei abrufen, indem Sie eine HEAD-Anforderung senden. Dadurch werden die Metadaten-Header der Datei zurückgegeben, einschließlich der Größe in Byte und des Dateiformats.

**API-Format**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Die Kennung der Datei. |
| `{FILE_NAME`} | Der Dateiname (z. B. Profils.parquet) |

**Anfrage**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwortheader enthalten die Metadaten der abgefragten Datei, darunter:
- `Content-Length`: Gibt die Größe der Nutzlast in Byte an
- `Content-Type`: Gibt den Dateityp an.

## Zugriff auf den Inhalt einer Datei

Sie können auch über die [!DNL Data Access] API auf den Inhalt einer Datei zugreifen.

**API-Format**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Die Kennung der Datei. |
| `{FILE_NAME`} | Der Dateiname (z. B. Profils.parquet). |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den Inhalt der Datei zurück.

## Herunterladen von partiellen Inhalten einer Datei

Die [!DNL Data Access] API ermöglicht das Herunterladen von Dateien in Textbausteinen. Eine Bereichsüberschrift kann während einer `GET /files/{FILE_ID}` Anforderung zum Herunterladen eines bestimmten Bytebereichs aus einer Datei angegeben werden. Wenn der Bereich nicht angegeben ist, lädt die API standardmäßig die gesamte Datei herunter.

Das HEAD-Beispiel im [vorherigen Abschnitt](#retrieve-the-metadata-of-a-file) gibt die Größe einer bestimmten Datei in Byte an.

**API-Format**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID} ` | Die Kennung der Datei. |
| `{FILE_NAME}` | Der Dateiname (z. B. Profils.parquet) |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `Range: bytes=0-99` | Gibt den Bereich der herunterzuladenden Bytes an. Wenn dies nicht angegeben ist, lädt die API die gesamte Datei herunter. In diesem Beispiel werden die ersten 100 Byte heruntergeladen. |

**Antwort**

Der Antworttext enthält die ersten 100 Byte der Datei (wie im Header &quot;Range&quot;in der Anforderung angegeben) zusammen mit HTTP-Status 206 (teilweise Inhalte). Die Antwort umfasst außerdem die folgenden Überschriften:

- Inhaltslänge: 100 (die Anzahl der zurückgegebenen Bytes)
- Content-Typ: application/parquet (eine Parkettdatei wurde angefordert, daher ist der Typ des Antwortinhalts parquet)
- Inhaltsbereich: Byte 0-99/249058 (der angeforderte Bereich (0-99) von der Gesamtzahl der Byte (249058))

## API-Antwortpaginierung konfigurieren

Antworten innerhalb der [!DNL Data Access] API werden paginiert. Standardmäßig beträgt die maximale Anzahl von Einträgen pro Seite 100. Mithilfe von Seitenparametern kann das Standardverhalten geändert werden.

- `limit`: Mit dem Parameter &quot;limit&quot;können Sie die Anzahl der Einträge pro Seite entsprechend Ihren Anforderungen festlegen.
- `start`: Der Offset kann durch den Parameter &quot;Beginn&quot; Abfrage festgelegt werden.
- `&`: Sie können ein kaufmännisches Und verwenden, um mehrere Parameter in einem einzigen Aufruf zu kombinieren.

**API-Format**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Stapelkennung des Stapels, auf den Sie zugreifen möchten. |
| `{OFFSET}` | Der angegebene Index, um das Ergebnisarray Beginn (z. B. Beginn=0) |
| `{LIMIT}` | Steuert, wie viele Ergebnisse im Ergebnisarray zurückgegeben werden (z. B. limit=1) |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**:

Die Antwort enthält ein `"data"` Array mit einem einzelnen Element, wie vom Anforderungsparameter angegeben `limit=1`. Dieses Element ist ein Objekt, das die Details der ersten verfügbaren Datei enthält, wie vom `start=0` Parameter in der Anforderung angegeben (denken Sie daran, dass bei der Nummerierung mit Null das erste Element &quot;0&quot;ist).

Der `_links.next.href` Wert enthält den Link zur nächsten Seite der Antworten, auf der Sie sehen können, dass der `start` Parameter erweitert wurde, um `start=1`.

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```
