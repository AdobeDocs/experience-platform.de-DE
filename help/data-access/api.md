---
keywords: Experience Platform;Home;beliebte Themen;Datenzugriff;Python-SDK;Spark-SDK;Datenzugriffs-API;export;export
solution: Experience Platform
title: Data Access API-Anleitung
topic-legacy: developer guide
description: Die Data Access API unterstützt Adobe Experience Platform, indem sie Entwicklern eine RESTful-Schnittstelle bereitstellt, die sich auf die Auffindbarkeit und Zugänglichkeit erfasster Datensätze in Experience Platform konzentriert.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 20%

---

# Handbuch zur Data Access API

Die Data Access API unterstützt Adobe Experience Platform, indem sie Benutzern eine RESTful-Schnittstelle bereitstellt, die sich auf die Auffindbarkeit und Zugänglichkeit erfasster Datensätze in [!DNL Experience Platform].

![Data Access auf Experience Platform](images/Data_Access_Experience_Platform.png)

## API-Spezifikationsreferenz

Die Referenzdokumentation zur Swagger-API finden Sie [here](https://www.adobe.io/experience-platform-apis/references/data-access/).

## Terminologie

Eine Beschreibung einiger häufig verwendeter Begriffe in diesem Dokument.

| Begriff | Beschreibung |
| ----- | ------------ |
| Datensatz | Eine Sammlung von Daten, die Schema und Felder enthält. |
| Batch | Eine Gruppe von Daten, die über einen bestimmten Zeitraum gesammelt und als Einheit verarbeitet wurden. |

## Liste der Dateien in einem Batch abrufen

Mithilfe einer Batch-Kennung (batchID) kann die Data Access API eine Liste der Dateien abrufen, die zu diesem Batch gehören.

**API-Format**

```http
GET /batches/{BATCH_ID}/files
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die Kennung des angegebenen Batches. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
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

Die `"data"` -Array enthält eine Liste aller Dateien im angegebenen Batch. Jede zurückgegebene Datei verfügt über eine eigene eindeutige ID (`{FILE_ID}`) in der `"dataSetFileId"` -Feld. Diese eindeutige ID kann dann verwendet werden, um auf die Datei zuzugreifen oder sie herunterzuladen.

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.dataSetFileId` | Die Datei-ID für jede Datei im angegebenen Batch. |
| `data._links.self.href` | Die URL für den Zugriff auf die Datei. |

## Zugreifen auf und Herunterladen von Dateien in einem Batch

Durch Verwendung der Datei-ID (`{FILE_ID}`), kann die Data Access API verwendet werden, um auf bestimmte Details einer Datei zuzugreifen, einschließlich Name, Größe in Byte und Link zum Herunterladen.

Die Antwort enthält ein Daten-Array. Je nachdem, ob es sich bei der von der ID referenzierten Datei um eine einzelne Datei oder ein Verzeichnis handelt, kann das zurückgegebene Datenarray einen einzelnen Eintrag oder eine Liste von Dateien enthalten, die zu diesem Verzeichnis gehören. Jedes Dateielement enthält die Details der Datei.

**API-Format**

```http
GET /files/{FILE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Gleich `"dataSetFileId"`, die Kennung der Datei, auf die zugegriffen werden soll. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Einzelne Dateiantwort**

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
| `data.name` | Name der Datei (z. B. profiles.csv). |
| `data.length` | Größe der Datei (in Byte). |
| `data._links.self.href` | Die URL zum Herunterladen der Datei. |

**Verzeichnisantwort**

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

Wenn ein Verzeichnis zurückgegeben wird, enthält es ein Array aller Dateien im Ordner.

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.name` | Name der Datei (z. B. profiles.csv). |
| `data._links.self.href` | Die URL zum Herunterladen der Datei. |

## Dateiinhalt aufrufen

Die [!DNL Data Access] API kann auch verwendet werden, um auf den Inhalt einer Datei zuzugreifen. Damit können Sie den Inhalt dann in eine externe Quelle herunterladen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Die ID der Datei in einem Datensatz. |
| `{FILE_NAME}` | Der vollständige Name der Datei (z. B. profiles.csv). |

**Antwort**

`Contents of the file`

## Zusätzliche Codebeispiele

Weitere Proben finden Sie im Abschnitt [Tutorial zum Datenzugriff](tutorials/dataset-data.md).

## Abonnieren von Datenerfassungsereignissen

[!DNL Platform] stellt bestimmte hochwertige Ereignisse über [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) zum Abonnieren bereit. Sie können beispielsweise Ereignisse zur Datenaufnahme abonnieren, um über potenzielle Verzögerungen und Fehler informiert zu werden. Weitere Informationen finden Sie im Tutorial zum [Abonnieren von Datenaufnahmebenachrichtigungen](../ingestion/quality/subscribe-events.md).
