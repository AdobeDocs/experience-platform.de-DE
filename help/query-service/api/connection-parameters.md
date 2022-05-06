---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; API-Handbuch; Verbindungsparameter; Query Service
solution: Experience Platform
title: Verbindungsparameter-API-Endpunkt
topic-legacy: connection parameters
description: Sie können Ihre Verbindungsparameter für die Verwendung des interaktiven Dienstes abrufen, indem Sie eine GET-Anfrage an den Endpunkt /connection_parameters senden.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 28%

---

# Endpunkt der Verbindungsparameter

## Beispiel-API-Aufruf

Im folgenden Abschnitt werden Sie durch den API-Aufruf geführt, den Sie mithilfe der [!DNL Query Service] API. Der Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Verbindungsparameter anfordern

Sie können Ihre Verbindungsparameter abrufen, indem Sie eine GET-Anfrage an die `/connection_parameters` -Endpunkt. Weitere Informationen zu Clients, die Verbindungsparameter verwenden, um eine Verbindung über den interaktiven Service herzustellen, finden Sie in der Dokumentation zu [Query Service-Clients](../clients/overview.md).

**API-Format**

```http
GET /connection_parameters
```

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Ihren Verbindungsparametern zurück.

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
