---
keywords: Experience Platform;Startseite;beliebte Themen;Datenzugriff;Python-SDK;Spark-SDK;Datenzugriffs-API;Export;Export
solution: Experience Platform
title: Handbuch zur Datenzugriffs-API
description: Die Datenzugriffs-API unterstützt Adobe Experience Platform, indem sie Entwicklerinnen und Entwicklern eine RESTful-Schnittstelle bereitstellt, die sich auf die Auffindbarkeit und Zugänglichkeit aufgenommener Datensätze innerhalb von Experience Platform konzentriert.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 78dbb735bad70e2115cbbaabb6cf74bf38983460
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 9%

---

# Handbuch zur Datenzugriffs-API

>[!IMPORTANT]
>
>Die Datenzugriffs-API ist jetzt **veraltet**. Es wird empfohlen, Ziele zum Exportieren von Daten aus Adobe Experience Platform zu verwenden. Weitere Informationen finden Sie in der Dokumentation [ Datensatzexportziele ](../destinations/destination-types.md#dataset-export-destinations).

Die Datenzugriffs-API unterstützt Adobe Experience Platform, indem sie Benutzenden eine RESTful-Schnittstelle bereitstellt, die sich auf die Auffindbarkeit und Zugänglichkeit aufgenommener Datensätze innerhalb von [!DNL Experience Platform] konzentriert.

![Ein Diagramm dazu, wie Data Access die Auffindbarkeit und Zugänglichkeit erfasster Datensätze innerhalb von Experience Platform erleichtert.](images/Data_Access_Experience_Platform.png)

## API-Spezifikationsreferenz

In der [OpenAPI-Referenzdokumentation für den Datenzugriff](https://developer.adobe.com/experience-platform-apis/references/data-access/) finden Sie ein standardisiertes, maschinenlesbares Format für eine einfachere Integration, Tests und Untersuchung.

## Terminologie {#terminology}

Die Tabelle enthält eine Beschreibung einiger in diesem Dokument häufig verwendeter Begriffe.

| Begriff | Beschreibung |
| ----- | ------------ |
| Datensatz | Eine Sammlung von Daten, die ein Schema und Felder enthält. |
| Batch | Ein Satz von Daten, die über einen bestimmten Zeitraum erfasst und als eine Einheit verarbeitet werden. |

## Abrufen einer Liste von Dateien in einem Batch {#retrieve-list-of-files-in-a-batch}

Um eine Liste von Dateien abzurufen, die zu einem bestimmten Batch gehören, verwenden Sie die Batch-Kennung (batchID) mit der Datenzugriffs-API.

**API-Format**

```http
GET /batches/{BATCH_ID}/files
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{BATCH_ID}` | Die ID des angegebenen Batches. |

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

Das `"data"`-Array enthält eine Liste aller Dateien im angegebenen Batch. Jede zurückgegebene Datei verfügt über eine eigene eindeutige ID (`{FILE_ID}`), die im `"dataSetFileId"` enthalten ist. Mit dieser eindeutigen ID können Sie auf die Datei zugreifen oder sie herunterladen.

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.dataSetFileId` | Die Datei-ID für jede Datei im angegebenen Batch. |
| `data._links.self.href` | Die URL für den Zugriff auf die Datei. |

## Zugreifen auf und Herunterladen von Dateien in einem Batch

Um auf bestimmte Details einer Datei zuzugreifen, verwenden Sie eine Dateikennung (`{FILE_ID}`) mit der Datenzugriffs-API, einschließlich ihres Namens, ihrer Größe in Byte und eines Links zum Herunterladen.

Die Antwort enthält ein Daten-Array. Je nachdem, ob es sich bei der Datei, auf die die ID verweist, um eine einzelne Datei oder ein Verzeichnis handelt, kann das zurückgegebene Daten-Array einen einzelnen Eintrag oder eine Liste von Dateien enthalten, die zu diesem Verzeichnis gehören. Jedes Dateielement enthält die Details der Datei.

**API-Format**

```http
GET /files/{FILE_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_ID}` | Entspricht der `"dataSetFileId"`, der ID der Datei, auf die zugegriffen werden soll. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `data.name` | Der Name der Datei (z. B. `profiles.parquet`). |
| `data.length` | Die Größe der Datei (in Byte). |
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

Wenn ein Verzeichnis zurückgegeben wird, enthält es ein Array aller Dateien im Verzeichnis .

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `data.name` | Der Name der Datei (z. B. `profiles.parquet`). |
| `data._links.self.href` | Die URL zum Herunterladen der Datei. |

## Zugriff auf den Inhalt einer Datei {#access-file-contents}

Sie können auch die [!DNL Data Access]-API verwenden, um auf den Inhalt einer Datei zuzugreifen. Anschließend können Sie die Inhalte in eine externe Quelle herunterladen.

**API-Format**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{FILE_NAME}` | Der Name der Datei, auf die Sie versuchen zuzugreifen. |

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
| `{FILE_NAME}` | Der vollständige Dateiname (z. B. `profiles.parquet`). |

**Antwort**

`Contents of the file`

## Zusätzliche Code-Beispiele

Weitere Beispiele finden Sie im [Tutorial zum Datenzugriff](tutorials/dataset-data.md).

## Abonnieren von Datenerfassungsereignissen {#subscribe-to-data-ingestion-events}

Sie können bestimmte hochwertige Ereignisse über die [Adobe Developer Console&rbrace; ](https://developer.adobe.com/console/). Sie können beispielsweise Ereignisse zur Datenaufnahme abonnieren, um über potenzielle Verzögerungen und Fehler informiert zu werden. Weitere Informationen finden Sie im Tutorial [Abonnieren von Adobe](../observability/alerts/subscribe.md)Ereignisbenachrichtigungen“.
