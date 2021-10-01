---
description: Auf dieser Seite werden alle API-Vorgänge beschrieben, die Sie mit dem API-Endpunkt "/authoring/credentials"ausführen können.
title: API-Vorgänge für Anmeldeendpunkte
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 6ff5fd0e80f7ca1015969e91cc23c88251509b61
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 6%

---

# API-Vorgänge für Anmeldeendpunkte {#credentials}

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt `/authoring/credentials` ausführen können.

## Verwendung des API-Endpunkts `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen müssen Sie *nicht* den API-Endpunkt `/credentials` verwenden. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über die Parameter `customerAuthenticationConfigurations` des Endpunkts `/destinations` konfigurieren. Weitere Informationen finden Sie unter [Konfiguration der Anmeldedaten](./credentials-configuration.md) .

Verwenden Sie diesen API-Endpunkt und wählen Sie `PLATFORM_AUTHENTICATION` in der [Zielkonfiguration](./destination-configuration.md#destination-delivery) aus, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel vorhanden ist. Der [!DNL Platform]-Kunde muss keine Authentifizierungsberechtigungen angeben, um eine Verbindung mit Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe des API-Endpunkts `/credentials` ein Anmeldedatenobjekt erstellen.

<!--

Commenting out the example configurations

## Example configurations

**Example configuration for a Basic authentication credential configuration with username and password**

```json
{
  "type": "BASIC",
  "name": "YOUR_DESTINATION_NAME",
  "basicAuthentication": {
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "password": "YOUR_DESTINATION_SERVER_PASSWORD"
  }
}

```

**Example configuration for an OAuth2 credential configuration**

```json

{
  "oauth2AccessTokenAuthentication": {
    "accessToken": "YOUR_DESTINATION_SERVER_ACCESS_TOKEN",
    "expiration": "YOUR_TOKEN_TIME_TO_LIVE",
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "userId": "YOUR_DESTINATION_USER_ID",
    "url": "AUTHORIZATION_PROVIDER_URL",
    "header": "YOUR_AUTHORIZATION_HEADER"
  }
}

```

The sections below list out the necessary parameters for each authentication type. Let us know which authentication type your server uses and provide us with the relevant information for your server type.

## Basic authentication

|Parameter | Type | Description|
|---------|----------|------|
|`username` | String | credentials configuration login username |
|`password` | String | credentials configuration login password |



// commenting out this part as these types of authentication methods are not supported in phase one

### S3 authentication

|Parameter | Type | Description|
|---------|----------|------|
|accessId | String | credentials configuration S3 credential Access key ID |
|secretKey | String | credentials configuration S3 credential Secret key |

### SSH 

|Parameter | Type | Description|
|---------|----------|------|
|username | String | credentials configuration SSH username |
|SSHKey | String | credentials configuration SSH key |



## OAuth1

|Parameter | Type | Description|
|---------|----------|------|
|`apiKey` | String | A value used by the Destinations Service to identify itself to the Service Provider. |
|`apiSecret` | String | Secret used by the Destinations Service to establish ownership of the API key to the Service Provider. |
|`acccessToken` | String | A value used by the Destinations Service to gain access to the Protected Resources on behalf of the User |
|`tokenSecret` | String | A secret used by the Destinations Service to establish ownership of an access token. |

## OAuth2 user credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username` | String | The user's username to log on to your platform. |
|`password` | String | The user's password to log on to your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 client credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username`| String | URL of authorization provider |
|`password` | String | Any header required for authorization |

## OAuth2 access token

|Parameter | Type | Description|
|---------|----------|------|
|`accessToken` | String | Access token provided by the authorization provider |
|`expiration` | String | The time-to-live for the access token |
|`username` | String | The user's username to log on to your platform. |
|`userId` | String | The user's ID with your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 refresh token

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`refreshToken` | String | Refresh token provided by the authorization provider |
|`url` | String | URL of authorization provider |
|`expiration` | String | The time-to-live for the refresh token |
|`header` | String | Any header required for authorization |

-->

## Erste Schritte mit API-Vorgängen zur Konfiguration von Anmeldedaten {#get-started}

Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um wichtige Informationen zu erhalten, die Sie benötigen, um die API erfolgreich aufrufen zu können. Dazu gehören das Abrufen der erforderlichen Zielerstellungsberechtigung und der erforderlichen Kopfzeilen.

## Erstellen einer Konfiguration für Anmeldedaten {#create}

Sie können eine neue Anmeldedaten-Konfiguration erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/credentials` senden.

**API-Format**


```http
POST /authoring/credentials
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Anmeldedaten-Konfiguration, die von den in der Payload bereitgestellten Parametern konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom Endpunkt `/authoring/credentials` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "oauth2UserAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "username":"string",
      "password":"string",
      "header":"string"
   },
   "oauth2ClientAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "header":"string",
      "developerToken":"string"
   },
   "oauth2AccessTokenAuthentication":{
      "accessToken":"string",
      "expiration":"string",
      "username":"string",
      "userId":"string",
      "url":"string",
      "header":"string"
   },
   "oauth2RefreshTokenAuthentication":{
      "refreshToken":"string",
      "expiration":"string",
      "clientId":"string",
      "clientSecret":"string",
      "url":"string",
      "header":"string"
   }
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `username` | Zeichenfolge | Anmeldedaten - Benutzername |
| `password` | Zeichenfolge | Anmeldedaten konfigurieren |
| `url` | Zeichenfolge | URL des Autorisierungsanbieters |
| `clientId` | Zeichenfolge | Client-ID der Client-/Anwendungsberechtigungen |
| `clientSecret` | Zeichenfolge | Client-Geheimnis der Client-/Anwendungsberechtigungen |
| `accessToken` | Zeichenfolge | Vom Autorisierungsanbieter bereitgestelltes Zugriffstoken |
| `expiration` | Zeichenfolge | Die Live-Zeit für das Zugriffstoken |
| `refreshToken` | Zeichenfolge | Vom Autorisierungsanbieter bereitgestelltes Aktualisierungstoken |
| `header` | Zeichenfolge | Alle Header, die für die Autorisierung erforderlich sind |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Anmeldekonfiguration zurück.

## Berechtigungskonfigurationen auflisten {#retrieve-list}

Sie können eine Liste aller Anmeldedaten-Konfigurationen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/authoring/credentials` stellen.

**API-Format**


```http
GET /authoring/credentials
```

**Anfrage**

Mit der folgenden Anfrage wird die Liste der Berechtigungskonfigurationen abgerufen, auf die Sie Zugriff haben, basierend auf der IMS-Organisation und der Sandbox-Konfiguration.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die folgende Antwort gibt den HTTP-Status 200 mit einer Liste von Anmeldekonfigurationen zurück, auf die Sie Zugriff haben, basierend auf der von Ihnen verwendeten IMS-Organisations-ID und dem Sandbox-Namen. Ein `instanceId` entspricht der Vorlage für eine Anmeldedaten-Konfiguration. Die Antwort wird aus Gründen der Kürze abgeschnitten.

```json
{
   "items":[
      {
         "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
         "createdDate":"2021-06-07T06:41:48.641943Z",
         "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
         "type":"OAUTH2_USER_CREDENTIAL",
         "name":"yourdestination",
         "oauth2UserAuthentication":{
            "url":"ABCD",
            "clientId":"ABCDEFGHIJKL",
            "clientSecret":"clientsecret",
            "username":"username",
            "password":"password",
            "header":"header"
         }
      }
   ]
}
    
```

## Vorhandene Anmeldekonfiguration aktualisieren {#update}

Sie können eine vorhandene Berechtigungskonfiguration aktualisieren, indem Sie eine PUT-Anfrage an den `/authoring/credentials`-Endpunkt senden und die Instanz-ID der Berechtigungskonfiguration angeben, die Sie aktualisieren möchten. Geben Sie im Hauptteil des Aufrufs die aktualisierte Konfiguration der Anmeldedaten an.

**API-Format**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Konfiguration der Anmeldeinformationen, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert eine vorhandene Anmeldekonfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```





## Bestimmte Anmeldeinformationen abrufen {#get}

Sie können detaillierte Informationen zu einer bestimmten Berechtigungskonfiguration abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/authoring/credentials` senden und die Instanz-ID der Berechtigungskonfiguration angeben, die Sie aktualisieren möchten.

**API-Format**


```http
GET /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Konfiguration der Anmeldeinformationen, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Anmeldedaten-Konfiguration zurück.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```


## Löschen einer bestimmten Konfiguration von Anmeldeinformationen {#delete}

Sie können die angegebene Konfiguration der Anmeldeinformationen löschen, indem Sie eine DELETE-Anfrage an den Endpunkt `/authoring/credentials` senden und im Anfragepfad die Kennung der Anmeldeinformationen angeben, die Sie löschen möchten.

**API-Format**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `id` der Anmeldeinformationen, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurück.

## Umgang mit API-Fehlern

Die Ziel-SDK-API-Endpunkte folgen den allgemeinen Grundsätzen der Experience Platform API-Fehlermeldung. Weitere Informationen finden Sie unter [API-Status-Codes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) und [Fehler in der Anforderungsheader](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) im Handbuch zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wann der Anmeldeinformationen-Endpunkt verwendet und wie eine Konfiguration für Anmeldeinformationen mithilfe des API-Endpunkts `/authoring/credentials` oder des Endpunkts `/authoring/destinations` eingerichtet wird. Lesen Sie [wie Sie das Ziel-SDK verwenden, um Ihr Ziel zu konfigurieren](./configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
