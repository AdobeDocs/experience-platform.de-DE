---
description: Auf dieser Seite werden alle API-Vorgänge beschrieben, die Sie mit dem API-Endpunkt „/authoring/credentials“ ausführen können.
title: API-Vorgänge für Zugriffsdaten-Endpunkte
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 91%

---

# API-Vorgänge für Zugriffsdaten-Endpunkte {#credentials}

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt `/authoring/credentials` ausführen können.

Eine Beschreibung der von diesem Endpunkt unterstützten Funktionen finden Sie unter:

* [Konfiguration des Streaming-Ziels](destination-configuration.md) für die Funktion, die Sie für Streaming-Ziele konfigurieren können.
* [Konfiguration des dateibasierten Ziels](file-based-destination-configuration.md) für die Funktion, die Sie für dateibasierte Ziele konfigurieren können.

## Verwendung des API-Endpunkts `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen müssen Sie den API-Endpunkt `/credentials` *nicht* verwenden. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über die `customerAuthenticationConfigurations`-Parameter des Endpunkts `/destinations` konfigurieren. Lesen Sie [Authentifizierungskonfiguration](./authentication-configuration.md#when-to-use) für weitere Informationen.

Verwenden Sie diesen API-Endpunkt und wählen Sie `PLATFORM_AUTHENTICATION` in der [Zielkonfiguration](./destination-configuration.md#destination-delivery), wenn es ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel gibt und der [!DNL Platform]-Kunde keine Authentifizierungsdaten bereitstellen muss, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe des API-Endpunkts `/credentials` ein Zugangsdatenobjekt erstellen.

## Erste Schritte mit API-Vorgängen zur Konfiguration von Zugriffsdaten {#get-started}

Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderliche Authoring-Berechtigung für Ziele und die Kopfzeilen abrufen können.

## Erstellen einer Zugangsdaten-Konfiguration {#create}

Sie können eine neue Zugangsdaten-Konfiguration erstellen, indem Sie eine POST-Anfrage an den `/authoring/credentials`-Endpunkt senden.

**API-Format**

```http
POST /authoring/credentials
```

**Anfrage**

Mit der folgenden Anfrage wird eine neue Zugangsdaten-Konfiguration erstellt, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom `/authoring/credentials`-Endpunkt akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
   },
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   },
   "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   },
   "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   },
   "azureConnectionStringAuthentication":{
      "connectionString":"string"
   },
   "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `username` | Zeichenfolge | Benutzername für die Anmeldung zur Zugriffsdaten-Konfiguration |
| `password` | Zeichenfolge | Passwort für die Anmeldung zur Zugangsdaten-Konfiguration |
| `url` | Zeichenfolge | URL des Autorisierungsanbieters |
| `clientId` | Zeichenfolge | Client-ID der Client-/Programm-Zugangsdaten |
| `clientSecret` | Zeichenfolge | Client-Geheimnis der Client-/Programm-Zugangsdaten |
| `accessToken` | Zeichenfolge | Vom Autorisierungsanbieter bereitgestelltes Zugriffs-Token |
| `expiration` | Zeichenfolge | Die Time-to-Live für das Zugriffs-Token |
| `refreshToken` | Zeichenfolge | Vom Autorisierungsanbieter bereitgestelltes Aktualisierungs-Token |
| `header` | Zeichenfolge | Etwaige Kopfzeilen, die für die Autorisierung erforderlich sind |
| `accessId` | Zeichenfolge | Amazon S3-Zugriffs-ID |
| `secretKey` | Zeichenfolge | Amazon S3-Geheimschlüssel |
| `sshKey` | Zeichenfolge | SSH-Schlüssel für SFTP mit SSH-Authentifizierung |
| `tenant` | Zeichenfolge | Azure Data Lake Storage-Mandant |
| `servicePrincipalId` | Zeichenfolge | Azure Service Principal ID für Azure Data Lake Storage |
| `servicePrincipalKey` | Zeichenfolge | Azure Service Principal Key für Azure Data Lake Storage |
| `connectionString` | Zeichenfolge | Azure Blob Storage-Verbindungszeichenfolge |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurück.

## Anzeigen der Zugangsdaten-Konfigurationen {#retrieve-list}

Sie können eine Liste aller Anmeldekonfigurationen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an die `/authoring/credentials` -Endpunkt.

**API-Format**


```http
GET /authoring/credentials
```

**Anfrage**

Mit der folgenden Anfrage wird die Liste der Anmeldekonfigurationen abgerufen, auf die Sie je nach Organisations- und Sandbox-Konfiguration Zugriff haben.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die folgende Antwort gibt den HTTP-Status 200 mit einer Liste von Anmeldekonfigurationen zurück, auf die Sie Zugriff haben, basierend auf der Organisations-ID und dem Sandbox-Namen, die Sie verwendet haben. Eine `instanceId` entspricht der Vorlage für eine einzige Anmeldedaten-Konfiguration. Die Antwort wird verkürzt angegeben.

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

## Aktualisieren einer vorhandenen Anmeldedaten-Konfiguration {#update}

Sie können eine vorhandene Anmeldedaten-Konfiguration aktualisieren, indem Sie eine PUT-Anfrage an den `/authoring/credentials`-Endpunkt senden und die Instanz-ID der Anmeldedaten-Konfiguration angeben, die Sie aktualisieren möchten. Geben Sie im Hauptteil des Aufrufs die aktualisierte Anmeldedaten-Konfiguration an.

**API-Format**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die Kennung der Anmeldedaten-Konfiguration, die Sie aktualisieren möchten. |

**Anfrage**

Mit der folgenden Anfrage wird eine vorhandene Anmeldedaten-Konfiguration aktualisiert, die durch die in der Payload bereitgestellten Parameter konfiguriert ist.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Abrufen einer bestimmten Anmeldedaten-Konfiguration {#get}

Sie können detaillierte Informationen zu einer bestimmten Anmeldedaten-Konfiguration abrufen, indem Sie eine GET-Anfrage an den `/authoring/credentials`-Endpunkt senden und die Instanz-ID der Anmeldedaten-Konfiguration angeben, die Sie aktualisieren möchten.

**API-Format**

```http
GET /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Anmeldedaten-Konfiguration, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Löschen einer bestimmten Anmeldedaten-Konfiguration {#delete}

Sie können eine bestimmte Anmeldedaten-Konfiguration löschen, indem Sie eine DELETE-Anfrage an den `/authoring/credentials`-Endpunkt senden und die Kennung der Anmeldedaten-Konfiguration angeben, die Sie im Anfragepfad löschen möchten.

**API-Format**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `id` der Anmeldedaten-Konfiguration, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurück.

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wann der Zugangsdaten-Endpunkt verwendet wird und wie Sie eine Zugangsdaten-Konfiguration mithilfe des `/authoring/credentials`-API-Endpunkts oder des `/authoring/destinations`-Endpunkts einrichten. Lesen Sie [Verwendung des Destination SDK zum Konfigurieren Ihres Ziels](./configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
