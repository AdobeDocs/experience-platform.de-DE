---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: Entwicklerhandbuch für Query Service
topic: connection parameters
description: Sie können Ihre Verbindungsparameter für die Verwendung des interaktiven Dienstes abrufen, indem Sie eine GET an den Endpunkt "/connection_parameters"senden.
translation-type: tm+mt
source-git-commit: 648544bc60c0cee8ca8b167118391980b6c33d91
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 47%

---


# Verbindungsparameter

## Beispiel-API-Aufrufe

Nachdem Sie wissen, welche Header verwendet werden sollen, können Sie mit dem Aufrufen der [!DNL Query Service]-API beginnen. In den folgenden Abschnitten werden die verschiedenen API-Aufrufe erläutert, die Sie mit der API [!DNL Query Service] durchführen können. Jeder Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Parameter für die Anforderungsverbindung

Sie können Ihre Verbindungsparameter abrufen, indem Sie eine GET an den `/connection_parameters`-Endpunkt anfordern. Weitere Informationen zu Clients, die Verbindungsparameter verwenden, um eine Verbindung über den interaktiven Dienst herzustellen, finden Sie in der Dokumentation zu [Query Service-Clients](../clients/overview.md).

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
