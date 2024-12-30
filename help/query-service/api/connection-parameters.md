---
keywords: Experience Platform;Startseite;beliebte Themen;Query Service;API-Handbuch;Verbindungsparameter;Query Service;
solution: Experience Platform
title: API-Endpunkt für Verbindungsparameter
description: Sie können Ihre Verbindungsparameter zur Verwendung des interaktiven Services abrufen, indem Sie eine GET-Anfrage an den Endpunkt /connection_parameters stellen.
role: Developer
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 29%

---

# Verbindungsparameter-Endpunkt

## Beispiel für API-Aufruf

Der folgende Abschnitt führt Sie durch den API-Aufruf, den Sie mit der [!DNL Query Service]-API ausführen können. Der Aufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.

### Verbindungsparameter anfordern

Sie können Ihre Verbindungsparameter abrufen, indem Sie eine GET-Anfrage an den `/connection_parameters`-Endpunkt senden. Weitere Informationen zu Clients, die Verbindungsparameter verwenden, um eine Verbindung über den interaktiven Service herzustellen, finden Sie in der Dokumentation zu [Query Service-Clients](../clients/overview.md).

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
