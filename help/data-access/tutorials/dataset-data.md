---
keywords: Experience Platform; Startseite; beliebte Themen; Datenzugriff; Data Access API; Query Data Access
solution: Experience Platform
title: Datensatzdaten mit der Data Access API anzeigen
type: Tutorial
description: Erfahren Sie, wie Sie in einem Datensatz gespeicherte Daten mithilfe der Data Access API in Adobe Experience Platform suchen, aufrufen und herunterladen können. Außerdem werden Sie mit einigen der einzigartigen Funktionen der Data Access API, wie z. B. dem Paging und partiellen Downloads, vertraut gemacht.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 18%

---

# Anzeigen von Datensatzdaten mit [!DNL Data Access] API

Dieses Dokument enthält eine schrittweise Anleitung zum Suchen, Aufrufen und Herunterladen von in einem Datensatz gespeicherten Daten mithilfe des [!DNL Data Access] API in Adobe Experience Platform. Sie werden auch mit einigen der einzigartigen Funktionen der [!DNL Data Access] API, z. B. Paging und teilweise Downloads.

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis dafür voraus, wie man einen Datensatz erstellt und füllt. Siehe [Tutorial zur Erstellung von Datensätzen](../../catalog/datasets/create.md) für weitere Informationen.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Sequenzdiagramm

Dieses Tutorial folgt den Schritten, die im unten stehenden Sequenzdiagramm beschrieben sind und die die Kernfunktionalität der [!DNL Data Access] API.</br>
![](../images/sequence_diagram.png)

Die [!DNL Catalog] Mit der API können Sie Informationen zu Batches und Dateien abrufen. Die [!DNL Data Access] Mit der API können Sie je nach Dateigröße entweder als vollständige oder teilweise Downloads über HTTP auf diese Dateien zugreifen und diese herunterladen.

## Suchen Sie die Daten

Bevor Sie mit der Verwendung des [!DNL Data Access] API müssen Sie den Speicherort der Daten identifizieren, auf die Sie zugreifen möchten. Im [!DNL Catalog] API gibt es zwei Endpunkte, mit denen Sie die Metadaten eines Unternehmens durchsuchen und die Kennung eines Batches oder einer Datei abrufen können, auf den/die Sie zugreifen möchten:

- `GET /batches`: Gibt eine Liste der Batches unter Ihrer Organisation aus
- `GET /dataSetFiles`: Gibt eine Liste von Dateien unter Ihrer Organisation aus

Für eine umfassende Liste von Endpunkten im [!DNL Catalog] API, siehe [API-Referenz](https://www.adobe.io/experience-platform-apis/references/catalog/).

## Abrufen einer Liste von Batches unter Ihrer IMS-Organisation

Verwenden der [!DNL Catalog] API können Sie eine Liste von Batches unter Ihrem Unternehmen zurückgeben:

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

Die Antwort enthält ein Objekt, das alle Batches auflistet, die mit der IMS-Organisation verbunden sind, wobei jeder Wert der obersten Ebene einen Batch darstellt. Die einzelnen Batch-Objekte enthalten die Details für diesen Batch. Die folgende Antwort wurde aus Platzgründen minimiert.

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

### Filtern der Batch-Liste

Filter sind häufig erforderlich, um einen bestimmten Batch zu finden, um relevante Daten für einen bestimmten Anwendungsfall abzurufen. Parameter können zu einer `GET /batches` anfordern, um die zurückgegebene Antwort zu filtern. Die nachstehende Anfrage gibt alle Batches zurück, die nach einem bestimmten Zeitpunkt innerhalb eines bestimmten Datensatzes erstellt wurden und nach dem Zeitpunkt der Erstellung sortiert wurden.

**API-Format**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{START_TIMESTAMP}` | Der Start-Zeitstempel in Millisekunden (z. B. 1514836799000). |
| `{DATASET_ID}` | Die Kennung des Datensatzes. |
| `{SORT_BY}` | Sortiert die Antwort nach dem angegebenen Wert. Beispiel: `desc:created` sortiert die Objekte nach Erstellungsdatum in absteigender Reihenfolge. |

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

Eine vollständige Liste der Parameter und Filter finden Sie im [Referenz zur Catalog API](https://www.adobe.io/experience-platform-apis/references/catalog/).

## Liste aller Dateien abrufen, die zu einem bestimmten Batch gehören

Nachdem Sie nun über die Kennung des Batches verfügen, auf den Sie zugreifen möchten, können Sie die [!DNL Data Access] API zum Abrufen einer Liste von Dateien, die zu diesem Batch gehören.

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

Die Antwort enthält ein Daten-Array, das alle Dateien innerhalb des angegebenen Batches auflistet. Die Dateien werden durch ihre Datei-ID referenziert, die sich unter der `dataSetFileId` -Feld.

## Zugriff auf eine Datei mit einer Datei-ID

Sobald Sie über eine eindeutige Datei-ID verfügen, können Sie die [!DNL Data Access] API für den Zugriff auf spezifische Details zur Datei, einschließlich Name, Größe in Byte und Link zum Herunterladen.

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

Je nachdem, ob die Datei-ID auf eine einzelne Datei oder ein Verzeichnis verweist, kann das zurückgegebene Datenarray einen einzelnen Eintrag oder eine Liste von Dateien enthalten, die zu diesem Verzeichnis gehören. Jedes Dateielement enthält Details wie den Namen der Datei, die Größe in Byte und einen Link zum Herunterladen der Datei.

**1. Fall: Datei-ID verweist auf eine einzelne Datei**

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

**2. Fall: Datei-ID verweist auf ein Verzeichnis**

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

Diese Antwort gibt einen Ordner mit zwei separaten Dateien mit IDs zurück `{FILE_ID_2}` und `{FILE_ID_3}`. In diesem Szenario müssen Sie der URL jeder Datei folgen, um auf die Datei zugreifen zu können.

## Abrufen der Metadaten einer Datei

Sie können die Metadaten einer Datei abrufen, indem Sie eine HEAD-Anfrage stellen. Dadurch werden die Metadaten-Header der Datei zurückgegeben, einschließlich der Größe in Byte und des Dateiformats.

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

Die Antwortheader enthalten die Metadaten der abgefragten Datei, darunter:
- `Content-Length`: Gibt die Größe der Payload in Byte an
- `Content-Type`: Gibt den Dateityp an.

## Dateiinhalt aufrufen

Sie können auch auf den Inhalt einer Datei zugreifen, indem Sie die [!DNL Data Access] API.

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

## Herunterladen von partiellen Inhalten einer Datei

Die [!DNL Data Access] API ermöglicht das Herunterladen von Dateien in Blöcken. Eine Bereichskopfzeile kann während einer `GET /files/{FILE_ID}` Anfrage zum Herunterladen eines bestimmten Byte-Bereichs aus einer Datei. Wenn der Bereich nicht angegeben ist, lädt die API standardmäßig die gesamte Datei herunter.

Das HEAD-Beispiel im [vorheriger Abschnitt](#retrieve-the-metadata-of-a-file) gibt die Größe einer bestimmten Datei in Byte an.

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
| `Range: bytes=0-99` | Gibt den Bereich der herunterzuladenden Bytes an. Wenn dies nicht angegeben ist, lädt die API die gesamte Datei herunter. In diesem Beispiel werden die ersten 100 Byte heruntergeladen. |

**Antwort**

Der Antworttext enthält die ersten 100 Byte der Datei (wie durch die &quot;Bereich&quot;-Kopfzeile in der Anfrage angegeben) zusammen mit dem HTTP-Status 206 (Teilinhalt). Die Antwort enthält auch die folgenden Kopfzeilen:

- Content-Length: 100 (die Anzahl der zurückgegebenen Bytes)
- Content-Type: application/parquet (eine Parquet-Datei wurde angefordert; daher ist der Antwortinhaltstyp `parquet`)
- Inhaltsbereich: Byte 0-99/249058 (der angeforderte Bereich (0-99) von der Gesamtzahl der Byte (249058))

## API-Antwort-Paginierung konfigurieren

Antworten innerhalb der [!DNL Data Access] API wird paginiert. Standardmäßig beträgt die maximale Anzahl von Einträgen pro Seite 100. Paging-Parameter können verwendet werden, um das Standardverhalten zu ändern.

- `limit`: Mithilfe des Parameters &quot;limit&quot; können Sie die Anzahl der Einträge pro Seite entsprechend Ihren Anforderungen angeben.
- `start`: Der Versatz kann durch den Abfrageparameter &quot;start&quot;festgelegt werden.
- `&`: Sie können ein kaufmännisches Und-Zeichen verwenden, um mehrere Parameter in einem einzelnen Aufruf zu kombinieren.

**API-Format**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Batch-Kennung des Batches, auf den Sie zugreifen möchten. |
| `{OFFSET}` | Der angegebene Index, um das Ergebnis-Array zu starten (z. B. start=0) |
| `{LIMIT}` | Steuert, wie viele Ergebnisse im Ergebnisarray zurückgegeben werden (z. B. limit=1) |

**Anfrage**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**:

Die Antwort enthält eine `"data"` Array mit einem einzelnen Element, wie durch den Anforderungsparameter angegeben `limit=1`. Dieses Element ist ein Objekt, das die Details der ersten verfügbaren Datei enthält, wie in der `start=0` -Parameter in der Anfrage (denken Sie daran, dass bei einer Nummerierung mit 0 das erste Element &quot;0&quot;ist).

Die `_links.next.href` -Wert den Link zur nächsten Antwortseite enthält, auf der Sie sehen können, dass die Variable `start` -Parameter wurde erweitert auf `start=1`.

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
