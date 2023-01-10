---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Authentifizierungsspezifikationen für Self-Serve-Quellen konfigurieren (Batch SDK)
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Self-Serve-Quellen (Batch SDK) vorbereiten müssen.
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 5%

---

# Authentifizierungsspezifikationen für Self-Serve-Quellen konfigurieren (Batch SDK)

Authentifizierungsspezifikationen definieren, wie Adobe Experience Platform-Benutzer eine Verbindung zu Ihrer Quelle herstellen können.

Die `authSpec` -Array enthält Informationen zu den Authentifizierungsparametern, die zum Verbinden einer Quelle mit Platform erforderlich sind. Jede Quelle kann mehrere verschiedene Authentifizierungstypen unterstützen.

## Authentifizierungsspezifikationen

Self-Serve-Quellen (Batch SDK) unterstützen OAuth 2-Aktualisierungs-Codes und einfache Authentifizierung. Die folgenden Tabellen enthalten Anleitungen zur Verwendung eines OAuth 2-Aktualisierungscodes und einer einfachen Authentifizierung

### OAuth 2-Aktualisierungscode

Ein OAuth 2-Aktualisierungscode ermöglicht einen sicheren Zugriff auf eine Anwendung durch Generieren eines temporären Zugriffstokens und eines Aktualisierungstokens. Mit dem Zugriffstoken können Sie sicher auf Ihre Ressourcen zugreifen, ohne andere Anmeldeinformationen angeben zu müssen. Mit dem Aktualisierungs-Token können Sie hingegen ein neues Zugriffstoken generieren, sobald das Zugriffstoken abläuft.

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
| `authSpec.spec` | Enthält Informationen zum Schema, Datentyp und Eigenschaften der Authentifizierung. |
| `authSpec.spec.$schema` | Definiert das für die Authentifizierung verwendete Schema. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definiert den Datentyp des Schemas. | `object` |
| `authSpec.spec.properties` | Enthält Informationen zu den Anmeldeinformationen, die für die Authentifizierung verwendet werden. |
| `authSpec.spec.properties.description` | Zeigt eine kurze Beschreibung der Berechtigung an. |
| `authSpec.spec.properties.type` | Definiert den Datentyp der Berechtigung. | `string` |
| `authSpec.spec.properties.clientId` | Die mit Ihrer Anwendung verknüpfte Client-ID. Die Client-ID wird zusammen mit Ihrem Client-Geheimnis verwendet, um Ihr Zugriffstoken abzurufen. |
| `authSpec.spec.properties.clientSecret` | Das mit Ihrer Anwendung verknüpfte Client-Geheimnis. Das Client-Geheimnis wird zusammen mit Ihrer Client-ID verwendet, um Ihr Zugriffstoken abzurufen. |
| `authSpec.spec.properties.accessToken` | Das Zugriffstoken autorisiert Ihren sicheren Zugriff auf Ihre Anwendung. |
| `authSpec.spec.properties.refreshToken` | Das Aktualisierungstoken wird verwendet, um ein neues Zugriffstoken zu generieren, wenn das Zugriffstoken abläuft. |
| `authSpec.spec.properties.expirationDate` | Definiert das Ablaufdatum des Zugriffstokens. |
| `authSpec.spec.properties.refreshTokenUrl` | Die URL, die zum Abrufen des Aktualisierungstokens verwendet wird. |
| `authSpec.spec.properties.accessTokenUrl` | Die URL, die zum Abrufen des Aktualisierungstokens verwendet wird. |
| `authSpec.spec.properties.requestParameterOverride` | Ermöglicht die Angabe von Berechtigungsparametern, die bei der Authentifizierung überschrieben werden sollen. |
| `authSpec.spec.required` | Zeigt die Anmeldeinformationen an, die für die Authentifizierung erforderlich sind. | `accessToken` |

{style=&quot;table-layout:auto&quot;}


### Einfache Authentifizierung

Die Standardauthentifizierung ist ein Authentifizierungstyp, mit dem Sie mithilfe einer Kombination aus Benutzername und Passwort Ihres Kontos auf Ihre Anwendung zugreifen können.

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
| `authSpec.spec` | Enthält Informationen zum Schema, Datentyp und Eigenschaften der Authentifizierung. |
| `authSpec.spec.$schema` | Definiert das für die Authentifizierung verwendete Schema. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | Definiert den Datentyp des Schemas. | `object` |
| `authSpec.spec.description` | Zeigt weitere Informationen zu Ihrem Authentifizierungstyp an. |
| `authSpec.spec.properties` | Enthält Informationen zu den Anmeldeinformationen, die für die Authentifizierung verwendet werden. |
| `authSpec.spec.properties.username` | Der mit Ihrer Anwendung verknüpfte Konto-Benutzername. |
| `authSpec.spec.properties.password` | Das mit Ihrer Anwendung verknüpfte Kontokennwort. |
| `authSpec.spec.required` | Gibt die Felder an, die als Pflichtwerte für die Eingabe in Platform erforderlich sind. | `username` |

{style=&quot;table-layout:auto&quot;}

## Beispielauthentifizierungsspezifikation

Im Folgenden finden Sie ein Beispiel für eine abgeschlossene Authentifizierungsspezifikation mit einer [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) -Quelle.

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

Wenn Ihre Authentifizierungsspezifikationen ausgefüllt sind, können Sie mit der Konfiguration der Quellspezifikationen für die Quelle fortfahren, die Sie in Platform integrieren möchten. Siehe das Dokument unter [Quellspezifikationen konfigurieren](./sourcespec.md) für weitere Informationen.
