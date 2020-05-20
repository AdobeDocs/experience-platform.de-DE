---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Abfrage Service
topic: connection parameters
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 1%

---


# Verbindungsparameter

## Beispiel-API-Aufrufe

Nachdem Sie wissen, welche Header verwendet werden sollen, können Sie mit dem Aufrufen der Abfrage Service API beginnen. In den folgenden Abschnitten werden die verschiedenen API-Aufrufe erläutert, die Sie mit der Abfrage Service API durchführen können. Jeder Aufruf enthält das allgemeine API-Format, eine Musteranforderung mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Anfordern von Verbindungsparametern für den interaktiven Dienst

Sie können Ihre Verbindungsparameter für die Verwendung des [interaktiven Dienstes](../creating-queries/writing-queries.md) abrufen, indem Sie eine GET-Anforderung an den `/connection_parameters` Endpunkt senden. Weitere Informationen zu Clients, die Verbindungsparameter für die Verbindung über den interaktiven Dienst verwenden, finden Sie in der Dokumentation zu [Abfrage Service Clients](../clients/overview.md).

**API-Format**

```http
GET /connection_parameters
```

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Ihren Verbindungsparametern zurück.

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
