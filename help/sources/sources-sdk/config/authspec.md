---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Konfigurieren von Authentifizierungsspezifikationen für Selbstbedienungsquellen (Batch-SDK)
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Selbstbedienungsquellen (Batch-SDK) vorbereiten müssen.
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 4%

---

# Konfigurieren von Authentifizierungsspezifikationen für Selbstbedienungsquellen (Batch-SDK)

Authentifizierungsspezifikationen definieren, wie Adobe Experience Platform-Benutzer eine Verbindung zu Ihrer Quelle herstellen können.

Das `authSpec`-Array enthält Informationen zu den Authentifizierungsparametern, die zum Verbinden einer Quelle mit Platform erforderlich sind. Jede beliebige Quelle kann mehrere verschiedene Authentifizierungstypen unterstützen.

## Authentifizierungsspezifikationen

Selbstbedienungsquellen (Batch-SDK) unterstützen OAuth 2-Aktualisierungs-Codes und die Standardauthentifizierung. In den folgenden Tabellen finden Sie Anleitungen zur Verwendung eines OAuth 2-Aktualisierungs-Codes und einer einfachen Authentifizierung

### OAuth 2-Aktualisierungs-Code

Ein OAuth 2-Aktualisierungs-Code ermöglicht den sicheren Zugriff auf eine Anwendung, indem er ein temporäres Zugriffstoken und ein Aktualisierungstoken generiert. Mit dem Zugriffs-Token können Sie sicher auf Ihre Ressourcen zugreifen, ohne andere Anmeldeinformationen angeben zu müssen, während Sie mit dem Aktualisierungs-Token ein neues Zugriffs-Token generieren können, sobald das Zugriffs-Token abläuft.

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


### Einfache Authentifizierung

Die Standardauthentifizierung ist ein Authentifizierungstyp, mit dem Sie über eine Kombination aus Ihrem Kontonamen und Ihrem Kontokennwort auf Ihre Anwendung zugreifen können.

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
| `authSpec.spec.required` | Gibt die Felder an, die als obligatorische Werte für die Eingabe in Platform erforderlich sind. | `username` |

{style="table-layout:auto"}

## Beispiel einer Authentifizierungsspezifikation

Im Folgenden finden Sie ein Beispiel für eine abgeschlossene Authentifizierungsspezifikation unter Verwendung einer [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md).

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

## Nächste Schritte

Wenn Ihre Authentifizierungsspezifikationen ausgefüllt sind, können Sie mit der Konfiguration der Quellspezifikationen für die Quelle fortfahren, die Sie in Platform integrieren möchten. Weitere Informationen finden Sie im Dokument [Konfigurieren von Quellspezifikationen](./sourcespec.md) .
