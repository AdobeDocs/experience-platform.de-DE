---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Konfigurieren von Authentifizierungsspezifikationen für Selbstbedienungsquellen (Batch-SDK)
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Selbstbedienungsquellen (Batch-SDK) vorbereiten müssen.
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 8517532f991413a239e0da890bf53b1bf5b621f0
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 4%

---

# Konfigurieren von Authentifizierungsspezifikationen für Selbstbedienungsquellen (Batch-SDK)

Authentifizierungsspezifikationen definieren, wie Adobe Experience Platform-Benutzer eine Verbindung zu Ihrer Quelle herstellen können.

Das `authSpec`-Array enthält Informationen zu den Authentifizierungsparametern, die zum Verbinden einer Quelle mit Platform erforderlich sind. Jede beliebige Quelle kann mehrere verschiedene Authentifizierungstypen unterstützen.

## Authentifizierungsspezifikationen

Selbstbedienungsquellen (Batch-SDK) unterstützen OAuth 2-Aktualisierungs-Codes und die Standardauthentifizierung. In den folgenden Tabellen finden Sie Anleitungen zur Verwendung eines OAuth 2-Aktualisierungs-Codes und einer einfachen Authentifizierung

### OAuth 2-Aktualisierungs-Code

Ein OAuth 2-Aktualisierungs-Code ermöglicht den sicheren Zugriff auf eine Anwendung, indem er ein temporäres Zugriffstoken und ein Aktualisierungstoken generiert. Mit dem Zugriffs-Token können Sie sicher auf Ihre Ressourcen zugreifen, ohne andere Anmeldeinformationen angeben zu müssen, während Sie mit dem Aktualisierungs-Token ein neues Zugriffs-Token generieren können, sobald das Zugriffs-Token abläuft.

+++Beispiel für einen OAuth 2-Aktualisierungs-Code anzeigen

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "authorizationTestUrl": {
        "description": "Authorization test url to validate accessToken.",
        "type": "string"
      },
      "clientId": {
        "description": "Client id of user account.",
        "type": "string"
      },
      "clientSecret": {
        "description": "Client secret of user account.",
        "type": "string",
        "format": "password"
      },
      "accessToken": {
        "description": "Access Token",
        "type": "string",
        "format": "password"
      },
      "refreshToken": {
        "description": "Refresh Token",
        "type": "string",
        "format": "password"
      },
      "expirationDate": {
        "description": "Date of token expiry.",
        "type": "string",
        "format": "date",
        "uiAttributes": {
          "hidden": true
        }
      },
      "accessTokenUrl": {
        "description": "Access token url to fetch access token.",
        "type": "string"
      },
      "requestParameterOverride": {
        "type": "object",
        "description": "Specify parameter to override.",
        "properties": {
          "accessTokenField": {
            "description": "Access token field name to override.",
            "type": "string"
          },
          "refreshTokenField": {
            "description": "Refresh token field name to override.",
            "type": "string"
          },
          "expireInField": {
            "description": "ExpireIn field name to override.",
            "type": "string"
          },
          "authenticationMethod": {
            "description": "Authentication method override.",
            "type": "string",
            "enum": [
              "GET",
              "POST"
            ]
          },
          "clientId": {
            "description": "ClientId field name override.",
            "type": "string"
          },
          "clientSecret": {
            "description": "ClientSecret field name override.",
            "type": "string"
          }
        }
      }
    },
    "required": [
      "accessToken"
    ]
  }
}
```

| Eigenschaft | Beschreibung | Beispiel |
| --- | --- | --- |
| `authSpec.name` | Zeigt den Namen des unterstützten Authentifizierungstyps an. | `oAuth2-refresh-code` |
| `authSpec.type` | Definiert den Authentifizierungstyp, der von der Quelle unterstützt wird. | `oAuth2-refresh-code` |
| `authSpec.spec` | Enthält Informationen zum Schema, zum Datentyp und zu den Eigenschaften der Authentifizierung. |
| `authSpec.spec.$schema` | Definiert das für die Authentifizierung verwendete Schema. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definiert den Datentyp des Schemas. | `object` |
| `authSpec.spec.properties` | Enthält Informationen zu den für die Authentifizierung verwendeten Anmeldeinformationen. |
| `authSpec.spec.properties.description` | Zeigt eine kurze Beschreibung der Berechtigung an. |
| `authSpec.spec.properties.type` | Definiert den Datentyp der Berechtigung. | `string` |
| `authSpec.spec.properties.clientId` | Die mit Ihrer Anwendung verknüpfte Client-ID. Die Client-ID wird zusammen mit Ihrem Client-Geheimnis verwendet, um Ihr Zugriffs-Token abzurufen. |
| `authSpec.spec.properties.clientSecret` | Das mit Ihrer Anwendung verknüpfte Client-Geheimnis. Das Client-Geheimnis wird zusammen mit Ihrer Client-ID verwendet, um Ihr Zugriffs-Token abzurufen. |
| `authSpec.spec.properties.accessToken` | Das Zugriffstoken autorisiert den sicheren Zugriff auf Ihre Anwendung. |
| `authSpec.spec.properties.refreshToken` | Das Aktualisierungs-Token wird verwendet, um ein neues Zugriffs-Token zu generieren, wenn das Zugriffs-Token abläuft. |
| `authSpec.spec.properties.expirationDate` | Definiert das Ablaufdatum des Zugriffstokens. |
| `authSpec.spec.properties.refreshTokenUrl` | Die URL, die zum Abrufen Ihres Aktualisierungs-Tokens verwendet wird. |
| `authSpec.spec.properties.accessTokenUrl` | Die URL, die zum Abrufen Ihres Aktualisierungs-Tokens verwendet wird. |
| `authSpec.spec.properties.requestParameterOverride` | Ermöglicht die Angabe von Berechtigungsparametern, die bei der Authentifizierung überschrieben werden sollen. |
| `authSpec.spec.required` | Zeigt die für die Authentifizierung erforderlichen Anmeldeinformationen an. | `accessToken` |

{style="table-layout:auto"}

+++

### Einfache Authentifizierung

Die Standardauthentifizierung ist ein Authentifizierungstyp, mit dem Sie über eine Kombination aus Ihrem Kontonamen und Ihrem Kontokennwort auf Ihre Anwendung zugreifen können.

+++ Beispiel für einfache Authentifizierung anzeigen

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "username": {
        "description": "Username to connect rest endpoint.",
        "type": "string"
      },
      "password": {
        "description": "Password to connect rest endpoint.",
        "type": "string",
        "format": "password"
      }
    },
    "required": [
      "username",
      "password"
    ]
  }
}
```

| Eigenschaft | Beschreibung | Beispiel |
| --- | --- | --- |
| `authSpec.name` | Zeigt den Namen des unterstützten Authentifizierungstyps an. | `Basic Authentication` |
| `authSpec.type` | Definiert den Authentifizierungstyp, der von der Quelle unterstützt wird. | `BasicAuthentication` |
| `authSpec.spec` | Enthält Informationen zum Schema, zum Datentyp und zu den Eigenschaften der Authentifizierung. |
| `authSpec.spec.$schema` | Definiert das für die Authentifizierung verwendete Schema. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definiert den Datentyp des Schemas. | `object` |
| `authSpec.spec.description` | Zeigt weitere Informationen für Ihren Authentifizierungstyp an. |
| `authSpec.spec.properties` | Enthält Informationen zu den für die Authentifizierung verwendeten Anmeldeinformationen. |
| `authSpec.spec.properties.username` | Der mit Ihrem Programm verknüpfte Benutzername für das Konto. |
| `authSpec.spec.properties.password` | Das mit Ihrer Anwendung verknüpfte Kontokennwort. |
| `authSpec.spec.required` | Gibt die Felder an, die als obligatorische Werte für die Eingabe in Experience Platform erforderlich sind. | `username` |

{style="table-layout:auto"}

+++

### API-Schlüsselauthentifizierung {#api-key-authentication}

Die API-Schlüsselauthentifizierung ist eine sichere Methode für den Zugriff auf APIs, indem in Anfragen ein API-Schlüssel und andere relevante Authentifizierungsparameter bereitgestellt werden. Abhängig von Ihren spezifischen API-Informationen können Sie den API-Schlüssel als Teil der Anfragekopfzeile, der Abfrageparameter oder des Hauptteils senden.

Die folgenden Parameter sind normalerweise bei der Verwendung der API-Schlüsselauthentifizierung erforderlich:

| Parameter | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `host` | string | Nein | Die Ressourcen-URL. |
| `authKey1` | Zeichenfolge | Ja | Der erste für den API-Zugriff erforderliche Authentifizierungsschlüssel. Sie wird normalerweise im Anfrage-Header oder in Abfrageparametern gesendet. |
| `authKey2` | Zeichenfolge | Optional | Ein zweiter Authentifizierungsschlüssel. Bei Bedarf wird dieser Schlüssel häufig zur weiteren Validierung von Anfragen verwendet. |
| `authKeyN` | Zeichenfolge | Optional | Eine zusätzliche Authentifizierungsvariable, die bei Bedarf verwendet werden kann, aber die API. |

{style="table-layout:auto"}

+++API-Schlüsselauthentifizierung anzeigen

```json
{
  "name": "API Key Authentication",
  "type": "KeyBased",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define authentication parameters required for API access",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource URL host path"
      },
      "authKey1": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 1",
        "description": "Primary authentication key for accessing the API",
        "restAttributes": {
          "headerParamName": "X-Auth-Key1"
        }
      },
      "authKey2": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 2",
        "description": "Secondary authentication key, if required",
        "restAttributes": {
          "headerParamName": "X-Auth-Key2"
        }
      },
      ..
      ..
      "authKeyN": {
        "type": "string",
        "format": "password",
        "title": "Additional Authentication Key",
        "description": "Additional authentication keys as needed by the API",
        "restAttributes": {
          "headerParamName": "X-Auth-KeyN"
        }
      }
    },
    "required": [
      "authKey1"
    ]
  }
}
```

+++

### Authentifizierungsverhalten

Sie können den `restAttributes`-Parameter verwenden, um zu definieren, wie der API-Schlüssel in die Anfrage aufgenommen werden soll. Im folgenden Beispiel zeigt das Attribut `headerParamName` an, dass die `X-Auth-Key1` als Kopfzeile gesendet werden soll.

```json
  "restAttributes": {
      "headerParamName": "X-Auth-Key1"
  }
```

Jeder Authentifizierungsschlüssel (z. B. `authKey1`, `authKey2` usw.) kann mit `restAttributes` verknüpft werden, um anzugeben, wie sie als Anfragen gesendet werden.

Wenn `authKey1` `"headerParamName": "X-Auth-Key1"` hat. Das bedeutet, dass der Anfrage-Header `X-Auth-Key:{YOUR_AUTH_KEY1}` enthalten sollte. Außerdem müssen der Schlüsselname und die `headerParamName` nicht unbedingt identisch sein. z. B.:

* Der `authKey1` kann `headerParamName: X-Custom-Auth-Key` haben. Das bedeutet, dass der Anfrage-Header `X-Custom-Auth-Key` anstelle von `authKey1` verwendet.
* Umgekehrt können `authKey1` `headerParamName: authKey1` haben. Das bedeutet, dass der Name des Anfrage-Headers unverändert bleibt.

**Beispiel-API-Format**

```http
GET /data?X-Auth-Key1={YOUR_AUTH_KEY1}&X-Auth-Key2={YOUR_AUTH_KEY2}
```

## Beispiel-Authentifizierungsspezifikation

Im Folgenden finden Sie ein Beispiel für eine abgeschlossene Authentifizierungsspezifikation unter Verwendung einer [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md).

+++Beispiel-Authentifizierungsspezifikation anzeigen

```json
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "accessToken": {
            "description": "Access Token of mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "username": {
            "description": "Username to connect mailChimp endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "username",
          "password"
        ]
      }
    }
  ],
```

+++

## Nächste Schritte

Wenn Ihre Authentifizierungsspezifikationen ausgefüllt sind, können Sie mit der Konfiguration der Quellspezifikationen für die Quelle fortfahren, die Sie in Platform integrieren möchten. Weitere Informationen finden Sie im Dokument [Konfigurieren von Quellspezifikationen](./sourcespec.md) .
