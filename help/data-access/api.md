---
keywords: Experience Platform; Startseite; beliebte Themen; Datenzugriff; Python-SDK; Spark SDK; Datenzugriffs-API; Export; Export
solution: Experience Platform
title: Data Access API-Anleitung
description: Die Data Access API unterstützt Adobe Experience Platform, indem sie Entwicklern eine RESTful-Schnittstelle bereitstellt, die sich auf die Auffindbarkeit und Zugänglichkeit erfasster Datensätze innerhalb von Experience Platform konzentriert.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 804eeb4ec976cf41fdd450bd8f307499c3ebae03
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 9%

---

# Handbuch zur Data Access API

>[!IMPORTANT]
>
>Die Data Access API ist jetzt **veraltet**. Es wird empfohlen, zum Exportieren von Daten aus Adobe Experience Platform Ziele zu verwenden. Weitere Informationen finden Sie in der Dokumentation zu [Datenexport-Zielen für Datensätze](../destinations/destination-types.md#dataset-export-destinations).

Die Data Access API unterstützt Adobe Experience Platform, indem sie Benutzern eine RESTful-Schnittstelle bereitstellt, die sich auf die Auffindbarkeit und Zugänglichkeit erfasster Datensätze innerhalb von [!DNL Experience Platform] konzentriert.

![Ein Diagramm, wie der Datenzugriff die Auffindbarkeit und Zugänglichkeit erfasster Datensätze innerhalb von Experience Platform erleichtert.](images/Data_Access_Experience_Platform.png)

## API-Spezifikationsreferenz

In der [Dokumentation zu Data Access OpenAPI](https://developer.adobe.com/experience-platform-apis/references/data-access/) finden Sie ein standardisiertes, maschinenlesbares Format für einfachere Integration, Tests und Exploration.

## Terminologie {#terminology}

Die Tabelle enthält eine Beschreibung einiger Begriffe, die in diesem Dokument häufig verwendet werden.

| Begriff | Beschreibung |
| ----- | ------------ |
| Datensatz | Eine Sammlung von Daten, die ein Schema und Felder enthält. |
| Batch | Eine Gruppe von Daten, die über einen bestimmten Zeitraum gesammelt und als Einheit verarbeitet wurden. |

## Liste der Dateien in einem Batch abrufen {#retrieve-list-of-files-in-a-batch}

Um eine Liste von Dateien abzurufen, die zu einem bestimmten Batch gehören, verwenden Sie die Batch-Kennung (batchID) mit der Data Access API.

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

Das Array `"data"` enthält eine Liste aller Dateien innerhalb des angegebenen Batches. Jede zurückgegebene Datei verfügt über eine eigene eindeutige ID (`{FILE_ID}`), die im Feld `"dataSetFileId"` enthalten ist. Sie können diese eindeutige ID verwenden, um auf die Datei zuzugreifen oder sie herunterzuladen.

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.dataSetFileId` | Die Datei-ID für jede Datei im angegebenen Batch. |
| `data._links.self.href` | Die URL für den Zugriff auf die Datei. |

## Zugreifen auf und Herunterladen von Dateien in einem Batch

Um auf bestimmte Details einer Datei zuzugreifen, verwenden Sie eine Dateikennung (`{FILE_ID}`) mit der Data Access API, einschließlich des Namens, der Größe in Byte und eines Links zum Herunterladen.

Die Antwort enthält ein Daten-Array. Je nachdem, ob es sich bei der von der ID referenzierten Datei um eine einzelne Datei oder ein Verzeichnis handelt, kann das zurückgegebene Datenarray einen einzelnen Eintrag oder eine Liste von Dateien enthalten, die zu diesem Verzeichnis gehören. Jedes Dateielement enthält die Details der Datei.

**API-Format**

```http
GET /files/{FILE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Entspricht &quot;`"dataSetFileId"`&quot;, der Kennung der Datei, auf die zugegriffen werden soll. |

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
| `data.name` | Der Name der Datei (z. B. `profiles.csv`). |
| `data.length` | Die Größe der Datei (in Byte). |
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

Wenn ein Verzeichnis zurückgegeben wird, enthält es ein Array aller Dateien im Ordner.

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.name` | Der Name der Datei (z. B. `profiles.csv`). |
| `data._links.self.href` | Die URL zum Herunterladen der Datei. |

## Dateiinhalt aufrufen {#access-file-contents}

Sie können auch die [!DNL Data Access] -API verwenden, um auf den Inhalt einer Datei zuzugreifen. Sie können die Inhalte dann in eine externe Quelle herunterladen.

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
| `{FILE_NAME}` | Der vollständige Name der Datei (z. B. `profiles.csv`). |

**Antwort**

`Contents of the file`

## Zusätzliche Codebeispiele

Weitere Beispiele finden Sie im Tutorial [Datenzugriff](tutorials/dataset-data.md).

## Abonnieren von Datenerfassungsereignissen {#subscribe-to-data-ingestion-events}

Sie können bestimmte Ereignisse mit hohem Wert über die [Adobe Developer Console](https://developer.adobe.com/console/) abonnieren. Sie können beispielsweise Ereignisse zur Datenaufnahme abonnieren, um über potenzielle Verzögerungen und Fehler informiert zu werden. Weitere Informationen finden Sie im Tutorial zum Anmelden von Adobe-Ereignisbenachrichtigungen ](../observability/alerts/subscribe.md).[
