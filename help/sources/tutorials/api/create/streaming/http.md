---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming-Verbindung; Streaming-Verbindung erstellen; API-Handbuch; Tutorial; Erstellen einer Streaming-Verbindung; Streaming-Erfassung; Erfassung;
solution: Experience Platform
title: Erstellen einer Streaming-Verbindung mithilfe der API
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie mit der Verwendung von Streaming-Erfassungs-APIs beginnen können, die Bestandteil der Data Ingestion Service-APIs von Adobe Experience Platform sind.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 42b8710cf6c04fabf7df1f005fae6b3828eeee49
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 37%

---


# Streaming-Verbindung mithilfe der API erstellen

Mit Flow Service werden Kundendaten aus verschiedenen Quellen in Adobe Experience Platform erfasst und zentralisiert. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, über die alle unterstützten Quellen verbunden werden können.

In diesem Tutorial wird die [!DNL Flow Service]-API verwendet, um Sie durch die Schritte zum Erstellen einer Streaming-Verbindung mithilfe der Flow Service-API zu führen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Erlebnisdaten  [!DNL Platform] organisiert werden.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Verbraucherprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.

Zum Erstellen einer Streaming-Verbindung müssen Sie außerdem über ein Ziel-XDM-Schema und einen Datensatz verfügen. Um zu erfahren, wie Sie diese erstellen, lesen Sie das Tutorial zu [Streaming-Datensatzdaten](../../../../../ingestion/tutorials/streaming-record-data.md) oder das Tutorial zu [Streaming-Zeitreihendaten](../../../../../ingestion/tutorials/streaming-time-series-data.md).

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die APIs für die Streaming-Erfassung erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../../../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Basisverbindung erstellen

Eine Basisverbindung gibt die Quelle an und enthält die Informationen, die erforderlich sind, um den Fluss mit Streaming-Aufnahme-APIs kompatibel zu machen. Beim Erstellen einer Basisverbindung haben Sie die Möglichkeit, eine nicht authentifizierte und eine authentifizierte Verbindung zu erstellen.

### Nicht authentifizierte Verbindung

Nicht authentifizierte Verbindungen sind die Standard-Streaming-Verbindung, die Sie erstellen können, wenn Sie Daten an Platform streamen möchten.

**API-Format**

```http
POST /flowservice/connections
```

**Anfrage**

Um eine Streaming-Verbindung zu erstellen, müssen die Anbieter-ID und die Verbindungsspezifikations-ID im Rahmen der POST-Anfrage angegeben werden. Die Anbieter-ID ist `521eee4d-8cbe-4906-bb48-fb6bd4450033` und die Verbindungs-Spezifikations-ID ist `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.sourceId` | Die ID der Streaming-Verbindung, die Sie erstellen möchten. |
| `auth.params.dataType` | Der Datentyp für die Streaming-Verbindung. Dieser Wert muss `xdm` sein. |
| `auth.params.name` | Der Name der Streaming-Verbindung, die Sie erstellen möchten. |
| `connectionSpec.id` | Die Verbindungsspezifikation `id` für Streaming-Verbindungen. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die `id` Ihrer neu erstellten Verbindung. Dies wird hier als `{CONNECTION_ID}` bezeichnet. |
| `etag` | Ein der Verbindung zugewiesener Identifikator, die die Revision der Verbindung angibt. |

### Authentifizierte Verbindung

Authentifizierte Verbindungen sollten verwendet werden, wenn Sie zwischen Datensätzen aus vertrauenswürdigen und nicht vertrauenswürdigen Quellen unterscheiden müssen. Benutzer, die Informationen mit personenbezogenen Daten (PII) senden möchten, sollten beim Streaming von Informationen an Platform eine authentifizierte Verbindung erstellen.

**API-Format**

```http
POST /flowservice/connections
```

**Anfrage**

Um eine Streaming-Verbindung zu erstellen, müssen die Anbieter-ID und die Verbindungsspezifikations-ID im Rahmen der POST-Anfrage angegeben werden. Die Anbieter-ID ist `521eee4d-8cbe-4906-bb48-fb6bd4450033` und die Verbindungs-Spezifikations-ID ist `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.sourceId` | Die ID der Streaming-Verbindung, die Sie erstellen möchten. |
| `auth.params.dataType` | Der Datentyp für die Streaming-Verbindung. Dieser Wert muss `xdm` sein. |
| `auth.params.name` | Der Name der Streaming-Verbindung, die Sie erstellen möchten. |
| `auth.params.authenticationRequired` | Der Parameter, der angibt, dass die erstellte Streaming-Verbindung hergestellt wurde |
| `connectionSpec.id` | Die Verbindungsspezifikation `id` für Streaming-Verbindungen. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`).

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die `id` Ihrer neu erstellten Verbindung. Dies wird hier als `{CONNECTION_ID}` bezeichnet. |
| `etag` | Ein der Verbindung zugewiesener Identifikator, die die Revision der Verbindung angibt. |

## Abrufen der Streaming-Endpunkt-URL

Mit der erstellten Basisverbindung können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen.

**API-Format**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der `id`-Wert der zuvor von Ihnen erstellten Verbindung. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zur angeforderten Verbindung zurück. Die Streaming-Endpunkt-URL wird automatisch mit der Verbindung erstellt und kann mit dem Wert `inletUrl` abgerufen werden.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## Quellverbindung erstellen

Nachdem Sie die Basisverbindung erstellt haben, müssen Sie eine Quellverbindung erstellen. Beim Erstellen einer Quellverbindung benötigen Sie den Wert `id` aus Ihrer erstellten Basisverbindung.

**API-Format**

```http
POST /flowservice/sourceConnections
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample source connection",
    "description": "Sample source connection description",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    }
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit detaillierten Informationen zur neu erstellten Quellverbindung zurück, einschließlich der eindeutigen Kennung (`id`).

```json
{
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
}
```

## Erstellen einer Zielverbindung

Nachdem Sie die Quellverbindung erstellt haben, können Sie eine Zielverbindung erstellen. Beim Erstellen Ihrer Zielverbindung benötigen Sie den `id`-Wert Ihres zuvor erstellten Datensatzes.

**API-Format**

```http
POST /flowservice/targetConnections
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample target connection",
    "description": "Sample target connection description",
    "connectionSpec": {
        "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
        "version": "1.0"
    },
    "data": {
        "format": "parquet_xdm"
    },
    "params": {
        "dataSetId": "{DATASET_ID}"
    }
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zur neu erstellten Zielverbindung zurück, einschließlich der eindeutigen Kennung (`id`).

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
}
```

## Datenfluss erstellen

Nachdem Sie Ihre Quell- und Zielverbindungen erstellt haben, können Sie jetzt einen Datenfluss erstellen. Der Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle zuständig. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/flows` senden.

**API-Format**

```http
POST /flows
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample flow",
    "description": "Sample flow description",
    "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "{SOURCE_CONNECTION_ID}"
    ],
    "targetConnectionIds": [
        "{TARGET_CONNECTION_ID}"
    ]
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zum neu erstellten Datenfluss zurück, einschließlich der eindeutigen Kennung (`id`).

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine Streaming-HTTP-Verbindung erstellt, über die Sie den Streaming-Endpunkt verwenden können, um Daten in Platform aufzunehmen. Anweisungen zum Erstellen einer Streaming-Verbindung in der Benutzeroberfläche finden Sie im Tutorial [Erstellen einer Streaming-Verbindung](../../../ui/create/streaming/http.md).

Informationen zum Streamen von Daten an Platform finden Sie im Tutorial zu [Streaming-Zeitreihendaten](../../../../../ingestion/tutorials/streaming-time-series-data.md) oder im Tutorial zu [Streaming-Datensatzdaten](../../../../../ingestion/tutorials/streaming-record-data.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zum Erstellen von Streaming-Verbindungen mithilfe der API.

### Senden von Nachrichten an eine authentifizierte Streaming-Verbindung

Wenn für eine Streaming-Verbindung die Authentifizierung aktiviert ist, muss der Client die `Authorization`-Kopfzeile zu seiner Anfrage hinzufügen.

Wenn die `Authorization`-Kopfzeile nicht vorhanden ist oder ein ungültiges/abgelaufenes Zugriffstoken gesendet wird, wird eine HTTP 401 Unerlaubt-Antwort zurückgegeben, mit einer ähnlichen Antwort wie folgt:

**Antwort**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```

### Posten von Rohdaten, die in Platform erfasst werden sollen {#ingest-data}

Nachdem Sie Ihren Fluss erstellt haben, können Sie Ihre JSON-Nachricht an den zuvor erstellten Streaming-Endpunkt senden.

**API-Format**

```http
POST /collection/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der `id`-Wert der neu erstellten Streaming-Verbindung. |

**Anfrage**

Die Beispielanfrage erfasst Rohdaten an den zuvor erstellten Streaming-Endpunkt.

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu den neu erfassten Informationen zurück.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{CONNECTION_ID}` | Die Kennung der zuvor erstellten Streaming-Verbindung. |
| `xactionId` | Eine eindeutige Kennung, die für den soeben gesendeten Datensatz Server-seitig generiert wurde. Diese Kennung hilft Adobe bei der Verfolgung des Lebenszyklus dieses Datensatzes in verschiedenen Systemen sowie beim Debugging. |
| `receivedTimeMs` | Ein Zeitstempel (Epoche in Millisekunden), der angibt, wann die Anfrage empfangen wurde. |
