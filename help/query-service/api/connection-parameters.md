---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;API-Leitfaden;Verbindungsparameter;Abfrage-Dienst
solution: Experience Platform
title: API-Endpunkt für Verbindungsparameter
topic-legacy: connection parameters
description: Sie können Ihre Verbindungsparameter für die Verwendung des interaktiven Dienstes abrufen, indem Sie eine GET an den Endpunkt "/connection_parameters"senden.
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 38%

---

# Endpunkt der Verbindungsparameter

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
