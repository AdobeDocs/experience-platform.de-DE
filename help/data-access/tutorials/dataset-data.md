---
keywords: Experience Platform;Startseite;beliebte Themen;Datenzugriff;Datenzugriffs-API;Abfragedatenzugriff
solution: Experience Platform
title: Anzeigen von Datensatzdaten mithilfe der Datenzugriffs-API
type: Tutorial
description: Erfahren Sie, wie Sie in einem Datensatz gespeicherte Daten mithilfe der Datenzugriffs-API in Adobe Experience Platform finden, darauf zugreifen und sie herunterladen können. In diesem Dokument werden einige der einzigartigen Funktionen der Datenzugriffs-API vorgestellt, wie Paging und partielle Downloads.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 13%

---

# Anzeigen von Datensatzdaten mithilfe [!DNL Data Access] API

In diesem Schritt-für-Schritt-Tutorial erfahren Sie, wie Sie mithilfe der [!DNL Data Access]-API in Adobe Experience Platform in einem Datensatz gespeicherte Daten finden, darauf zugreifen und sie herunterladen können. In diesem Dokument werden einige der einzigartigen Funktionen der [!DNL Data Access]-API vorgestellt, wie Paging und partielle Downloads.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis darüber voraus, wie ein Datensatz erstellt und aufgefüllt wird. Weitere Informationen finden [ im Tutorial ](../../catalog/datasets/create.md) Datensatzerstellung .

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Experience Platform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial“ ](../../landing/api-authentication.md). Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Ablaufdiagramm

Dieses Tutorial folgt den im folgenden Sequenzdiagramm beschriebenen Schritten und hebt die Kernfunktionen der [!DNL Data Access]-API hervor.

![Ein Sequenzdiagramm der Kernfunktionen der Datenzugriffs-API.](../images/sequence_diagram.png)

Um Informationen zu Stapeln und Dateien abzurufen, verwenden Sie die [!DNL Catalog]-API. Um auf diese Dateien zuzugreifen und sie über HTTP als vollständige oder teilweise Downloads herunterzuladen, verwenden Sie je nach Größe der Datei die [!DNL Data Access]-API.

## Suchen der Daten

Bevor Sie mit der Verwendung der [!DNL Data Access]-API beginnen können, müssen Sie den Speicherort der Daten identifizieren, auf die Sie zugreifen möchten. In der [!DNL Catalog]-API gibt es zwei Endpunkte, mit denen Sie die Metadaten einer Organisation durchsuchen und die ID eines Batches oder einer Datei abrufen können, auf den bzw. die Sie zugreifen möchten:

- `GET /batches`: Gibt eine Liste der Batches in Ihrer Organisation zurück
- `GET /dataSetFiles`: Gibt eine Liste der Dateien in Ihrer Organisation zurück

Eine umfassende Liste der Endpunkte in der [!DNL Catalog]-API finden Sie in der [API-Referenz](https://developer.adobe.com/experience-platform-apis/references/catalog/).

## Abrufen einer Liste von Batches unter Ihrer Organisation

Mit der [!DNL Catalog]-API können Sie eine Liste der Batches in Ihrer Organisation zurückgeben:

**API-Format**

```http
GET /batches
```

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort enthält ein -Objekt, das alle mit der Organisation verbundenen Batches auflistet, wobei jeder Wert der obersten Ebene einen Batch darstellt. Die einzelnen Batch-Objekte enthalten die Details für diesen spezifischen Batch. Die unten stehende Antwort wurde aus Platzgründen minimiert.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
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

### Filtern der Liste der Stapel {#filter-batches-list}

Filter sind oft erforderlich, um einen bestimmten Batch zu finden, um relevante Daten für einen bestimmten Anwendungsfall abzurufen. Parameter können zu einer `GET /batches` hinzugefügt werden, um die zurückgegebene Antwort zu filtern. Die nachstehende Anfrage gibt alle Batches zurück, die nach einer bestimmten Zeit innerhalb eines bestimmten Datensatzes erstellt wurden, sortiert nach dem Zeitpunkt ihrer Erstellung.

**API-Format**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{START_TIMESTAMP}` | Der Startzeitstempel in Millisekunden (z. B. 1514836799000). |
| `{DATASET_ID}` | Die Datensatz-ID. |
| `{SORT_BY}` | Sortiert die Antwort nach dem angegebenen Wert. Beispielsweise sortiert `desc:created` die Objekte nach Erstellungsdatum in absteigender Reihenfolge. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

Eine vollständige Liste der Parameter und Filter finden Sie in der [Katalog-API-Referenz](https://developer.adobe.com/experience-platform-apis/references/catalog/).

## Abrufen einer Liste aller Dateien, die zu einem bestimmten Stapel gehören

Nachdem Sie nun über die ID des Batches verfügen, auf den Sie zugreifen möchten, können Sie mit der [!DNL Data Access]-API eine Liste der zu diesem Batch gehörenden Dateien abrufen.

**API-Format**

```http
GET /batches/{BATCH_ID}/files
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Batch-Kennung des Batches, auf den Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Die Antwort enthält ein Daten-Array, das alle Dateien innerhalb des angegebenen Batches auflistet. Dateien werden durch ihre Datei-ID referenziert, die sich unter dem Feld `dataSetFileId` befindet.

## Zugriff auf eine Datei mit einer Datei-ID {#access-file-with-file-id}

Sobald Sie über eine eindeutige Datei-ID verfügen, können Sie mit der [!DNL Data Access]-API auf spezifische Details zur Datei zugreifen, einschließlich ihres Namens, ihrer Größe in Byte und eines Links zum Herunterladen.

**API-Format**

```http
GET /files/{FILE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Die Kennung der Datei, auf die Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Je nachdem, ob die Datei-ID auf eine einzelne Datei oder ein Verzeichnis verweist, kann das zurückgegebene Daten-Array einen einzelnen Eintrag oder eine Liste von Dateien enthalten, die zu diesem Verzeichnis gehören. Jedes Dateielement enthält Details wie den Namen der Datei, die Größe in Byte und einen Link zum Herunterladen der Datei.

**Fall 1: Die Datei-ID verweist auf eine einzelne Datei**

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

**Fall 2: Die Datei-ID verweist auf ein Verzeichnis**

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

Diese Antwort gibt ein Verzeichnis mit zwei separaten Dateien mit den IDs `{FILE_ID_2}` und `{FILE_ID_3}` zurück. In diesem Szenario müssen Sie der URL jeder Datei folgen, um auf die Datei zuzugreifen.

## Abrufen der Metadaten einer Datei

Sie können die Metadaten einer Datei abrufen, indem Sie eine HEAD-Anfrage stellen. Dadurch werden die Metadaten-Header der Datei zurückgegeben, einschließlich ihrer Größe in Byte und Dateiformat.

**API-Format**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Die Kennung der Datei. |
| `{FILE_NAME}` | Der Dateiname (z. B. profiles.parquet) |

**Anfrage**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort-Header enthalten die Metadaten der abgefragten Datei, einschließlich:

- `Content-Length`: Gibt die Größe der Payload in Byte an
- `Content-Type`: Gibt den Dateityp an.

## Zugriff auf den Inhalt einer Datei

Sie können auch über die [!DNL Data Access]-API auf den Inhalt einer Datei zugreifen.

**API-Format**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Die Kennung der Datei. |
| `{FILE_NAME}` | Der Dateiname (z. B. profiles.parquet). |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den Inhalt der Datei zurück.

## Herunterladen von partiellen Inhalten einer Datei {#download-partial-file-contents}

Um einen bestimmten Bytebereich aus einer Datei herunterzuladen, geben Sie während einer `GET /files/{FILE_ID}`-Anfrage an die [!DNL Data Access]-API eine Bereichskopfzeile an. Wenn der Bereich nicht angegeben ist, lädt die API standardmäßig die gesamte Datei herunter.

Das HEAD-Beispiel im [vorherigen Abschnitt](#retrieve-the-metadata-of-a-file) gibt die Größe einer bestimmten Datei in Byte an.

**API-Format**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID} ` | Die Kennung der Datei. |
| `{FILE_NAME}` | Der Dateiname (z. B. profiles.parquet) |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `Range: bytes=0-99` | Gibt den Bytebereich an, der heruntergeladen werden soll. Wenn dies nicht angegeben ist, lädt die API die gesamte Datei herunter. In diesem Beispiel werden die ersten 100 Byte heruntergeladen. |

**Antwort**

Der Antworttext enthält die ersten 100 Byte der Datei (wie in der Anfrage durch den Header „Range“ angegeben) zusammen mit dem HTTP-Status 206 (Partial Contents). Die Antwort enthält außerdem die folgenden Kopfzeilen:

- Inhaltslänge: 100 (die Anzahl der zurückgegebenen Bytes)
- Inhaltstyp: application/parquet (eine Parquet-Datei wurde angefordert, daher ist der Inhaltstyp der Antwort `parquet`)
- Inhaltsbereich: Bytes 0-99/249058 (der angeforderte Bereich (0-99) der Gesamtzahl der Bytes (249058))

## Konfigurieren der API-Antwortpaginierung {#configure-response-pagination}

Antworten innerhalb der [!DNL Data Access]-API werden paginiert. Standardmäßig ist die maximale Anzahl von Einträgen pro Seite 100. Sie können das Standardverhalten mit Paging-Parametern ändern.

- `limit`: Sie können die Anzahl der Einträge pro Seite Ihren Anforderungen entsprechend mit dem Parameter „limit“ angeben.
- `start`: Der Versatz kann durch den Abfrageparameter „start“ festgelegt werden.
- `&`: Sie können ein kaufmännisches Und-Zeichen verwenden, um mehrere Parameter in einem einzigen Aufruf zu kombinieren.

**API-Format**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Batch-Kennung des Batches, auf den Sie zugreifen möchten. |
| `{OFFSET}` | Der angegebene Index zum Starten des Ergebnis-Arrays (z. B. start=0) |
| `{LIMIT}` | Steuert, wie viele Ergebnisse im Ergebnis-Array zurückgegeben werden (z. B. limit=1) |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**:

Die Antwort enthält ein `"data"`-Array mit einem einzelnen Element, wie in der `limit=1` für Anforderungsparameter angegeben. Dieses Element ist ein Objekt, das die Details der ersten verfügbaren Datei enthält, wie sie im `start=0` der Anfrage angegeben sind (denken Sie daran, dass bei der nullbasierten Nummerierung das erste Element „0“ ist).

Der `_links.next.href` enthält den Link zur nächsten Seite mit Antworten, auf der Sie sehen können, dass der `start`-Parameter auf `start=1` erweitert wurde.

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
