---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerleitfaden für Datenzugriff
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 10%

---


# Entwicklerleitfaden für Datenzugriff

Die Datenzugriff-API unterstützt die Adobe Experience Platform, indem sie eine RESTful-Benutzeroberfläche bereitstellt, die auf die Erkennung und Zugänglichkeit von erfassten Datensätzen innerhalb von [!DNL Experience Platform]Data Warehouse ausgerichtet ist.

![Datenzugriff auf Experience Platform](images/Data_Access_Experience_Platform.png)

## API-Spezifikation

Die Referenzdokumentation zur Swagger-API finden Sie [hier](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).

## Terminologie

Eine Beschreibung einiger häufig verwendeter Begriffe in diesem Dokument.

| Begriff | Beschreibung |
| ----- | ------------ |
| Datensatz | Eine Datenerfassung, die Schema und Felder enthält. |
| Batch | Eine Gruppe von Daten, die über einen bestimmten Zeitraum gesammelt und als eine Einheit verarbeitet werden. |

## Abrufen der Liste von Dateien in einem Stapel

Mithilfe einer Batch-ID (batchID) kann die Data Access-API eine Liste von Dateien abrufen, die zu diesem Stapel gehören.

**API-Format**

```http
GET /batches/{BATCH_ID}/files
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des angegebenen Stapels. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
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
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

Das `"data"` Array enthält eine Liste aller Dateien im angegebenen Stapel. Jede zurückgegebene Datei verfügt über eine eigene eindeutige ID (`{FILE_ID}`), die im `"dataSetFileId"` Feld enthalten ist. Diese eindeutige ID kann dann verwendet werden, um auf die Datei zuzugreifen oder sie herunterzuladen.

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.dataSetFileId` | Die Datei-ID für jede Datei im angegebenen Stapel. |
| `data._links.self.href` | Die URL für den Zugriff auf die Datei. |

## Zugriff und Herunterladen von Dateien in einem Stapel

Mithilfe einer Datei-ID (`{FILE_ID}`) kann die Datenzugriff-API verwendet werden, um auf bestimmte Details einer Datei zuzugreifen, einschließlich Name, Größe in Byte und Link zum Herunterladen.

Die Antwort enthält ein Datenarray. Je nachdem, ob es sich bei der von der ID referenzierten Datei um eine einzelne Datei oder ein Verzeichnis handelt, kann das zurückgegebene Datenarray einen einzelnen Eintrag oder eine Liste von Dateien enthalten, die zu diesem Verzeichnis gehören. Jedes Dateielement enthält die Details der Datei.

**API-Format**

```http
GET /files/{FILE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Entspricht der `"dataSetFileId"`ID der Datei, auf die zugegriffen werden soll. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Einzeldatei-Antwort**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
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
| `data.name` | Dateiname (z. B. Profils.csv). |
| `data.length` | Größe der Datei (in Byte). |
| `data._links.self.href` | Die URL zum Herunterladen der Datei. |

**Ordnerantwort**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
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

Wenn ein Ordner zurückgegeben wird, enthält er ein Array aller Dateien im Ordner.

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.name` | Dateiname (z. B. Profils.csv). |
| `data._links.self.href` | Die URL zum Herunterladen der Datei. |

## Zugriff auf den Inhalt einer Datei

The [!DNL Data Access] API can also be used to access the contents of a file. Auf diese Weise können Sie den Inhalt in eine externe Quelle herunterladen.

**API-Format**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_NAME}` | Der Name der Datei, auf die Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Die ID der Datei in einem Datensatz. |
| `{FILE_NAME}` | Der vollständige Dateiname (z. B. Profils.csv). |

**Antwort**

```
Contents of the file
```

## Zusätzliche Codebeispiele

Weitere Beispiele finden Sie im [Lernprogramm](tutorials/dataset-data.md)zum Datenzugriff.

## Abonnieren von Datenaufnahme-Ereignissen

[!DNL Platform] stellt bestimmte hochwertige Ereignis über die [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)zum Abonnement bereit. Sie können beispielsweise Ereignisse zur Datenerfassung abonnieren, um über potenzielle Verzögerungen und Fehler informiert zu werden. Weitere Informationen finden Sie im Tutorial zum [Abonnieren von Datenerfassungsbenachrichtigungen](../ingestion/quality/subscribe-events.md) .