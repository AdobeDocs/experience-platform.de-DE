---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen Sie eine authentifizierte Streaming-Verbindung
topic: tutorial
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 68%

---


# Erstellen einer authentifizierten Streaming-Verbindung

Authenticated Data Collection allows Adobe Experience Platform services, such as [!DNL Real-time Customer Profile] and [!DNL Identity], to differentiate between records coming from trusted sources and un-trusted sources. Kunden, die persönliche identifizierbare Informationen (PII) senden möchten, können dies tun, indem sie Zugriffstoken als Teil der POST-Anfrage senden.

## Erste Schritte

Um mit dem Streamen von Daten an die Adobe Experience Platform zu beginnen, ist eine Registrierung der Streaming-Verbindung erforderlich. Bei der Registrierung einer Streaming-Verbindung müssen Sie einige wichtige Details wie die Quelle der Streaming-Daten angeben.

After registering a streaming connection, you, as the data producer, will have a unique URL which can be used to stream data to [!DNL Platform].

Für dieses Tutorial sind auch Kenntnisse über verschiedene Adobe Experience Platform-Diensten erforderlich. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Der standardisierte Rahmen, mit dem Erlebnisdaten [!DNL Platform] organisiert werden.
- [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, benutzerdefiniertes Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um erfolgreiche Aufrufe an Streaming-Erfassungs-APIs durchführen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

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

## Verbindung erstellen

Eine Verbindung gibt die Quelle an und enthält die Informationen, die erforderlich sind, um den Fluss mit Streaming-Aufnahme-APIs kompatibel zu machen.

**API-Format**

```http
POST /flowservice/connections
```

**Anfrage**

>[!NOTE]
>
>Die Werte für die aufgelistete `providerId` und die `connectionSpec` **müssen** wie im Beispiel gezeigt verwendet werden, da diese der API anzeigen, dass Sie eine Streaming-Verbindung für die Streaming-Aufnahme erstellen.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
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

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 mit Details zur neu erstellten Verbindung zurück.

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

## Abrufen der Datenerfassungs-URL

Mit der erstellten Verbindung können Sie jetzt Ihre Datenerfassungs-URL abrufen.

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

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit detaillierten Informationen zur angeforderten Verbindung zurück. Die Datenerfassungs-URL wird automatisch mit der Verbindung erstellt und kann mit dem `inletUrl`-Wert abgerufen werden.

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

## Nächste Schritte

Now that you have created an authenticated streaming connection, you can stream either time series or record data, allowing you to ingest data within [!DNL Platform]. To learn how to stream time series data to [!DNL Platform], go to the [streaming time series data tutorial](./streaming-time-series-data.md). To learn how to stream record data to [!DNL Platform], go to the [streaming record data tutorial](./streaming-record-data.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zu authentifizierten Streaming-Verbindungen.

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
