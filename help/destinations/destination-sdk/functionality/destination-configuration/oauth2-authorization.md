---
description: Auf dieser Seite werden die verschiedenen OAuth 2-Autorisierungsflüsse beschrieben, die von Destination SDK unterstützt werden, und Sie erhalten Anweisungen zum Einrichten der OAuth 2-Autorisierung für Ihr Ziel.
title: OAuth 2-Autorisierung
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 7ba9971b44410e609c64f4dcf956a1976207353e
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 78%

---


# OAuth 2-Autorisierung

Destination SDK unterstützt mehrere Autorisierungsmethoden für Ihr Ziel. Dazu gehört die Möglichkeit, sich mithilfe der [OAuth 2-Autorisierungs-Framework](https://tools.ietf.org/html/rfc6749).

Auf dieser Seite werden die verschiedenen OAuth 2-Autorisierungsflüsse beschrieben, die von Destination SDK unterstützt werden, und Sie erhalten Anweisungen zum Einrichten der OAuth 2-Autorisierung für Ihr Ziel.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Nein |

## Hinzufügen von OAuth 2-Autorisierungsdetails zur Zielkonfiguration {#how-to-setup}

### Voraussetzungen in Ihrem System {#prerequisites}

Als ersten Schritt müssen Sie in Ihrem System eine Anwendung für Adobe Experience Platform erstellen oder anderweitig Experience Platform in Ihrem System registrieren. Das Ziel besteht darin, eine Client-ID und ein Client-Geheimnis zu generieren, die für die Authentifizierung von Experience Platform an Ihrem Ziel erforderlich sind.

Als Teil dieser Konfiguration in Ihrem System benötigen Sie die Adobe Experience Platform OAuth 2-Umleitungs-/Callback-URLs, die Sie in der folgenden Liste finden.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-can2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-gbr9.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>Der Schritt zum Registrieren einer Umleitungs-/Callback-URL für Adobe Experience Platform in Ihrem System ist nur für den Gewährungstyp [OAuth 2 mit Autorisierungs-Code](#authorization-code) erforderlich. Für die beiden anderen unterstützten Gewährungstypen (Kennwort und Client-Anmeldeinformationen) können Sie diesen Schritt überspringen.

Am Ende dieses Schritts sollten Sie über Folgendes verfügen:
* eine Client-ID;
* ein Client-Geheimnis;
* die Callback-URL von Adobe (für die Gewährung des Autorisierungs-Codes).

### Was Sie in Destination SDK tun müssen {#to-do-in-destination-sdk}

Um die OAuth 2-Autorisierung für Ihr Ziel in Experience Platform einzurichten, müssen Sie Ihre OAuth 2-Details zum [Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)unter der `customerAuthenticationConfigurations` -Parameter. Siehe [Kundenauthentifizierung](../../functionality/destination-configuration/customer-authentication.md) für ausführliche Beispiele. Spezifische Anweisungen dazu, welche Felder Sie je nach OAuth 2-Autorisierungstyp zu Ihrer Konfigurationsvorlage hinzufügen müssen, finden Sie weiter unten auf dieser Seite.

## Unterstützte OAuth 2-Gewährungstypen {#oauth2-grant-types}

Experience Platform unterstützt die drei OAuth 2-Gewährungstypen in der folgenden Tabelle. Wenn Sie ein benutzerdefiniertes OAuth 2-Setup haben, kann Adobe es mithilfe von benutzerdefinierten Feldern in Ihrer Integration unterstützen. Weitere Informationen finden Sie in den Abschnitten zu den einzelnen Fördertypen.

>[!IMPORTANT]
>
>* Sie geben die Eingabeparameter wie in den folgenden Abschnitten beschrieben an. Adobe-interne Systeme stellen eine Verbindung zum Autorisierungssystem Ihrer Plattform her und erfassen Ausgabeparameter, mit denen der Benutzer authentifiziert und die Autorisierung für Ihr Ziel verwaltet wird.
>* Die in der Tabelle fett hervorgehobenen Eingabeparameter sind erforderliche Parameter im OAuth 2-Autorisierungsfluss. Die anderen Parameter sind optional. Es gibt weitere benutzerdefinierte Eingabeparameter, die hier nicht gezeigt werden, aber in den Abschnitten [Anpassen der OAuth 2-Konfiguration](#customize-configuration) und [Aktualisierung des Zugriffstokens](#access-token-refresh) ausführlich beschrieben werden.

| OAuth 2-Gewährung | Eingaben | Ausgaben |
|---------|----------|---------|
| Autorisierungs-Code | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Kennwort | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Client-Anmeldeinformationen | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

In der obigen Tabelle sind die Felder aufgeführt, die in standardmäßigen OAuth 2-Flüssen verwendet werden. Zusätzlich zu diesen Standardfeldern können verschiedene Partnerintegrationen zusätzliche Eingaben und Ausgaben erfordern. Adobe hat ein flexibles OAuth 2-Autorisierungs-Framework für die Destination SDK entwickelt, das Varianten des obigen Standardfeldmusters handhaben kann und gleichzeitig einen Mechanismus zur automatischen Neuerstellung ungültiger Ausgaben unterstützt, wie z. B. abgelaufene Zugriffstoken.

Die Ausgabe enthält in allen Fällen ein Zugriffstoken, das von Experience Platform verwendet wird, um sich zu authentifizieren und die Autorisierung für Ihr Ziel beizubehalten.

Das System, das Adobe für die OAuth 2-Autorisierung entwickelt hat:
* Unterstützt alle drei OAuth 2-Gewährungstypen und berücksichtigt dabei alle Variationen in ihnen, z. B. zusätzliche Datenfelder, nicht standardmäßige API-Aufrufe und mehr.
* Unterstützt Zugriffstoken mit variierenden Lebenszeitwerten (90 Tage, 30 Minuten oder ein beliebiger anderer von Ihnen angegebener Lebenszeitwert).
* Unterstützt OAuth 2-Autorisierungsflüsse mit oder ohne Aktualisierungs-Token.

## OAuth 2 mit Autorisierungs-Code {#authorization-code}

Wenn Ihr Ziel einen standardmäßigen OAuth 2.0-Autorisierungs-Code-Fluss (lesen Sie dazu den Abschnitt [RFC-Standardspezifikationen](https://tools.ietf.org/html/rfc6749#section-4.1)) oder eine Variante davon unterstützt, finden Sie unten die erforderlichen und die optionalen Felder:

| OAuth 2-Gewährung | Eingaben | Ausgaben |
|---------|----------|---------|
| Autorisierungs-Code | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Um diese Autorisierungsmethode für Ihr Ziel einzurichten, fügen Sie Ihrer Konfiguration die folgenden Zeilen hinzu, wenn Sie [Zielkonfiguration erstellen](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_AUTHORIZATION_CODE",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "authorizationUrl": "https://www.moviestar.com/dialog/OAuth",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `authType` | Zeichenfolge | Verwenden Sie „OAUTH2“. |
| `grant` | Zeichenfolge | Verwenden Sie „OAUTH2_AUTHORIZATION_CODE“. |
| `accessTokenUrl` | Zeichenfolge | Die URL auf Ihrer Seite, die Zugriffstoken ausgibt und optional Token aktualisiert. |
| `authorizationUrl` | Zeichenfolge | Die URL Ihres Autorisierungs-Servers, über die Sie die Benutzerin bzw. den Benutzer zur Anmeldung bei Ihrer Anwendung weiterleiten. |
| `refreshTokenUrl` | Zeichenfolge | *Optional.* Die URL auf Ihrer Seite, die Aktualisierungs-Token ausgibt. Häufig ist die `refreshTokenUrl` identisch mit der `accessTokenUrl`. |
| `clientId` | Zeichenfolge | Die Client-ID, die Ihr System Adobe Experience Platform zuweist. |
| `clientSecret` | Zeichenfolge | Das Client-Geheimnis, das Ihr System Adobe Experience Platform zuweist. |
| `scope` | Liste von Zeichenfolgen | *Optional*. Legen Sie den Umfang der Aktionen fest, die das Zugriffstoken Experience Platform für Ihre Ressourcen ermöglicht. Beispiel: „lesen, schreiben“. |

{style="table-layout:auto"}

## OAUth 2 mit Passwortgewährung

Für die OAuth 2-Passwortgewährung (lesen Sie die [RFC-Standardspezifikationen](https://tools.ietf.org/html/rfc6749#section-4.3)) erfordert Experience Platform den Benutzernamen und das Passwort der Benutzerin bzw. des Benutzers. Im Autorisierungsfluss tauscht Experience Platform diese Anmeldeinformationen gegen ein Zugriffstoken und optional ein Aktualisierungstoken aus.
Adobe verwendet die folgenden Standardeingaben, um die Zielkonfiguration zu vereinfachen und Werte zu überschreiben:

| OAuth 2-Gewährung | Eingaben | Ausgaben |
|---------|----------|---------|
| Kennwort | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>accessTokenUrl</b></li><li><b>username</b></li><li><b>password</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> Sie müssen in der unten stehenden Konfiguration keine Parameter für `username` und `password` hinzufügen. Wenn Sie `"grant": "OAUTH2_PASSWORD"` in der Zielkonfiguration hinzufügen, fordert das System die Benutzenden auf, in der Experience Platform-Benutzeroberfläche einen Benutzernamen und ein Passwort anzugeben, wenn sie sich bei Ihrem Ziel authentifizieren.

Um diese Autorisierungsmethode für Ihr Ziel einzurichten, fügen Sie Ihrer Konfiguration die folgenden Zeilen hinzu, wenn Sie [Zielkonfiguration erstellen](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_PASSWORD",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `authType` | Zeichenfolge | Verwenden Sie „OAUTH2“. |
| `grant` | Zeichenfolge | Verwenden Sie „OAUTH2_PASSWORD“. |
| `accessTokenUrl` | Zeichenfolge | Die URL auf Ihrer Seite, die Zugriffstoken ausgibt und optional Token aktualisiert. |
| `clientId` | Zeichenfolge | Die Client-ID, die Ihr System Adobe Experience Platform zuweist. |
| `clientSecret` | Zeichenfolge | Das Client-Geheimnis, das Ihr System Adobe Experience Platform zuweist. |
| `scope` | Liste von Zeichenfolgen | *Optional*. Legen Sie den Umfang der Aktionen fest, die das Zugriffstoken Experience Platform für Ihre Ressourcen ermöglicht. Beispiel: „lesen, schreiben“. |

{style="table-layout:auto"}

## OAuth 2 mit Gewährung von Client-Anmeldeinformationen

Sie können ein Ziel für OAuth 2 Client-Anmeldeinformationen konfigurieren (lesen Sie den Abschnitt [RFC-Standardspezifikationen](https://tools.ietf.org/html/rfc6749#section-4.4)) konfigurieren, das die unten aufgeführten Standardeingaben und -ausgaben unterstützt. Sie können die Werte anpassen. Siehe [Anpassen der OAuth 2-Konfiguration](#customize-configuration) für Details.

| OAuth 2-Gewährung | Eingaben | Ausgaben |
|---------|----------|---------|
| Client-Anmeldeinformationen | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

Um diese Autorisierungsmethode für Ihr Ziel einzurichten, fügen Sie Ihrer Konfiguration die folgenden Zeilen hinzu, wenn Sie [Zielkonfiguration erstellen](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_CLIENT_CREDENTIALS",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `authType` | Zeichenfolge | Verwenden Sie „OAUTH2“. |
| `grant` | Zeichenfolge | Verwenden Sie „OAUTH2_CLIENT_CREDENTIALS“. |
| `accessTokenUrl` | Zeichenfolge | Die URL Ihres Autorisierungs-Servers, die ein Zugriffstoken und ein optionales Aktualisierungstoken ausgibt. |
| `refreshTokenUrl` | Zeichenfolge | *Optional.* Die URL auf Ihrer Seite, die Aktualisierungs-Token ausgibt. Häufig ist die `refreshTokenUrl` identisch mit der `accessTokenUrl`. |
| `clientId` | Zeichenfolge | Die Client-ID, die Ihr System Adobe Experience Platform zuweist. |
| `clientSecret` | Zeichenfolge | Das Client-Geheimnis, das Ihr System Adobe Experience Platform zuweist. |
| `scope` | Liste von Zeichenfolgen | *Optional*. Legen Sie den Umfang der Aktionen fest, die das Zugriffstoken Experience Platform für Ihre Ressourcen ermöglicht. Beispiel: „lesen, schreiben“. |

{style="table-layout:auto"}

## Anpassen der OAuth 2-Konfiguration {#customize-configuration}

Die in den obigen Abschnitten beschriebenen Konfigurationen beschreiben standardmäßige OAuth 2-Gewährungen. Das von Adobe entworfene System bietet jedoch eine Flexibilität, sodass Sie für alle Variationen der OAuth 2-Gewährungen auch benutzerdefinierte Parameter verwenden können. Um die standardmäßigen OAuth 2-Einstellungen anzupassen, verwenden Sie die Parameter `authenticationDataFields`, wie in den Beispielen unten dargestellt.

### Beispiel 1: Verwendung von `authenticationDataFields` zur Erfassung von Informationen aus der Zulassungsantwort {#example-1}

In diesem Beispiel verfügt eine Zielplattform über Aktualisierungstoken, die nach einer bestimmten Zeitdauer ablaufen. In diesem Fall richtet der Partner das benutzerdefinierte Feld `refreshTokenExpiration` ein, um das Ablaufdatum des Aktualisierungstokens aus dem Feld `refresh_token_expires_in` in der API-Antwort abzurufen.

```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "options":{
            
         },
         "grant":"OAUTH2_AUTHORIZATION_CODE",
         "accessTokenUrl":"https://api.moviestar.com/OAuth/access_token",
         "authorizationUrl":"https://api.moviestar.com/OAuth/authorization",
         "scope":[
            "read",
            "write",
            "delete"
         ],
         "refreshTokenUrl":"https://api.moviestar.com/OAuth/accessToken",
         "clientSecret":"client-secret-here",
         "authenticationDataFields":[
            {
               "name":"refreshTokenExpiration",
               "title":"Refresh Token Expires In",
               "description":"Time in seconds when the refresh token will expire",
               "type":"string",
               "isRequired":false,
               "source":"CUSTOMER",
               "authenticationResponsePath":"refresh_token_expires_in"
            }
         ]
      }
   ]
}  
```

### Beispiel 2: Verwenden von `authenticationDataFields`, um ein spezielles Aktualisierungstoken bereitzustellen {#example-2}

In diesem Beispiel richtet ein Partner sein Ziel ein, um ein spezielles Aktualisierungstoken bereitzustellen. Außerdem wird das Ablaufdatum für Zugriffstoken nicht in der API-Antwort zurückgegeben, sodass er einen Standardwert (in diesem Fall 3600 Sekunden) hartcodieren kann.

```json
      "authenticationDataFields": [
        {
            "name": "refreshToken",
            "value": "special_refresh_token"
        },
        {
            "name": "expiresIn",
            "value": 3600
        } 
      ]
```

### Beispiel 3: Die Benutzenden geben die Client-ID und das Client-Geheimnis ein, wenn sie das Ziel konfigurieren {#example-3}

In diesem Beispiel muss die Kundin oder der Kunde nicht (wie im Abschnitt [Voraussetzungen in Ihrem System](#prerequisites) gezeigt) eine globale Kunden-ID und ein Kundengeheimnis erstellen, sondern die Kunden-ID, das Kundengeheimnis und die Konto-ID (die ID, die die Kundin bzw. der Kunde für die Anmeldung beim Ziel verwendet) eingeben

```json
{
    //...
    "customerAuthenticationConfigurations": [
        {
            "authType": "OAUTH2",
            "grant": "OAUTH2_CLIENT_CREDENTIALS",
            "authenticationDataFields": [
                {
                    "name": "clientId",
                    "title": "Client ID",
                    "description": "Client ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "source": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                }
            ],
            "accessTokenRequest": {
                "destinationServerType": "URL_BASED",
                "urlBasedDestination": {
                    "url": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "https://{{ authData.moviestarId }}.yourdestination.com/identity/oauth/token"
                    }
                },
                "httpTemplate": {
                    "requestBody": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
                    },
                    "httpMethod": "POST",
                    "contentType": "application/x-www-form-urlencoded"
                },
                "responseFields": [
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.access_token }}",
                        "name": "accessToken"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.scope }}",
                        "name": "scope"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.token_type }}",
                        "name": "tokenType"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.expires_in }}",
                        "name": "expiresIn"
                    }
                ]
            }
        }
    ]
//...
}
```



Sie können die folgenden Parameter in `authenticationDataFields` zum Anpassen Ihrer OAuth 2-Konfiguration verwenden:

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `authenticationDataFields.name` | Zeichenfolge | Der Name des benutzerdefinierten Felds. |
| `authenticationDataFields.title` | Zeichenfolge | Ein Titel, den Sie für das benutzerdefinierte Feld angeben können. |
| `authenticationDataFields.description` | Zeichenfolge | Eine Beschreibung des von Ihnen eingerichteten benutzerdefinierten Datenfelds. |
| `authenticationDataFields.type` | Zeichenfolge | Definiert den Typ des benutzerdefinierten Datenfelds. <br> Akzeptierte Werte: `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Boolesch | Gibt an, ob das benutzerdefinierte Datenfeld im Autorisierungsfluss erforderlich ist. |
| `authenticationDataFields.format` | Zeichenfolge | Wenn Sie `"format":"password"`, verschlüsselt Adobe den Wert des Autorisierungsdatenfelds. Bei Verwendung mit `"fieldType": "CUSTOMER"` ist außerdem die Eingabe in der Benutzeroberfläche unsichtbar, wenn Benutzende etwas in das Feld eingeben. |
| `authenticationDataFields.fieldType` | Zeichenfolge | Gibt an, ob die Eingabe vom Partner (d. h. Ihnen) oder von den Benutzenden stammt, wenn sie Ihr Ziel in Experience Platform einrichten. |
| `authenticationDataFields.value` | Zeichenfolge. Boolesch. Ganzzahl | Der Wert des benutzerdefinierten Datenfelds. Der Wert entspricht dem ausgewählten Typ aus `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | Zeichenfolge | Gibt an, auf welches Feld aus dem API-Antwortpfad verwiesen wird. |

{style="table-layout:auto"}

## Aktualisierung des Zugriffstokens {#access-token-refresh}

Adobe hat ein System entwickelt, das abgelaufene Zugriffstoken aktualisiert, ohne dass die Benutzenden sich wieder bei Ihrer Plattform anmelden müssen. Das System kann ein neues Token generieren, sodass die Aktivierung an Ihr Ziel nahtlos für die Kundinnen und Kunden fortgesetzt wird.

Um die Aktualisierung des Zugriffstokens einzurichten, müssen Sie möglicherweise eine vorlagenbasierte HTTP-Anfrage konfigurieren, die es Adobe ermöglicht, mithilfe eines Aktualisierungstokens ein neues Zugriffstoken zu erhalten. Wenn das Zugriffstoken abgelaufen ist, verwendet Adobe die von Ihnen bereitgestellte vorlagenbasierte Anfrage und fügt die von Ihnen angegebenen Parameter hinzu. Verwenden Sie den Parameter `accessTokenRequest` zum Konfigurieren eines Aktualisierungsmechanismus für Zugriffstoken.


```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "grant":"OAUTH2_CLIENT_CREDENTIALS",
         "accessTokenRequest":{
            "destinationServerType":"URL_BASED",
            "urlBasedDestination":{
               "url":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"https://{{authData.customerId}}.yourdestination.com/identity/oauth/token"
               }
            },
            "httpTemplate":{
               "requestBody":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
               },
               "httpMethod":"POST",
               "contentType":"application/x-www-form-urlencoded",
               "headers":[
                  
               ]
            },
            "responseFields":[
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.expires_in }}",
                  "name":"expiresIn"
               },
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.access_token }}",
                  "name":"accessToken"
               }
            ],
            "validations":[
               {
                  "name":"access_token validation",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{response.body.access_token is empty }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"false"
                  }
               },
               {
                  "name":"response status",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{ response.status }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"200"
                  }
               }
            ]
         }
      }
   ]
}
```

Sie können die folgenden Parameter in `accessTokenRequest` verwenden, um Ihren Token-Aktualisierungsprozess anzupassen:

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | Zeichenfolge | Verwenden Sie `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | Zeichenfolge | <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Sie Vorlagen für den Wert in `accessTokenRequest.urlBasedDestination.url.value` verwenden.</li><li> Verwenden Sie `NONE`, wenn der Wert im Feld `accessTokenRequest.urlBasedDestination.url.value` eine Konstante ist. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | Zeichenfolge | Die URL, an die Experience Platform das Zugriffstoken anfordert. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | Zeichenfolge | <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Sie Vorlagen für die Werte in `accessTokenRequest.httpTemplate.requestBody.value` verwenden.</li><li> Verwenden Sie `NONE`, wenn der Wert im Feld `accessTokenRequest.httpTemplate.requestBody.value` eine Konstante ist. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | Zeichenfolge | Verwenden Sie die Vorlagensprache, um Felder in der HTTP-Anfrage an den Zugriffstoken-Endpunkt anzupassen. Informationen darüber, wie Sie Felder mithilfe von Vorlagen anpassen können, finden Sie im Abschnitt [Vorlagenkonventionen](#templating-conventions). |
| `accessTokenRequest.httpTemplate.httpMethod` | Zeichenfolge | Gibt die HTTP-Methode an, die zum Aufrufen Ihres Zugriffstoken-Endpunkts verwendet wird. In den meisten Fällen ist dieser Wert `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | Zeichenfolge | Gibt den Inhaltstyp des HTTP-Aufrufs für Ihren Zugriffstoken-Endpunkt an. <br> Beispielsweise `application/x-www-form-urlencoded` oder `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | Zeichenfolge | Gibt an, ob dem HTTP-Aufruf an Ihren Zugriffstoken-Endpunkt Kopfzeilen hinzugefügt werden sollen. |
| `accessTokenRequest.responseFields.templatingStrategy` | Zeichenfolge | <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Sie Vorlagen für die Werte in `accessTokenRequest.responseFields.value` verwenden.</li><li> Verwenden Sie `NONE`, wenn der Wert im Feld `accessTokenRequest.responseFields.value` eine Konstante ist. </li></li> |
| `accessTokenRequest.responseFields.value` | Zeichenfolge | Verwenden Sie die Vorlagensprache, um über Ihren Zugriffstoken-Endpunkt auf Felder in der HTTP-Antwort zuzugreifen. Informationen darüber, wie Sie Felder mithilfe von Vorlagen anpassen können, finden Sie im Abschnitt [Vorlagenkonventionen](#templating-conventions). |
| `accessTokenRequest.validations.name` | Zeichenfolge | Gibt den Namen an, den Sie für diese Validierung angegeben haben. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | Zeichenfolge | <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Sie Vorlagen für die Werte in `accessTokenRequest.validations.actualValue.value` verwenden.</li><li> Verwenden Sie `NONE`, wenn der Wert im Feld `accessTokenRequest.validations.actualValue.value` eine Konstante ist. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | Zeichenfolge | Verwenden Sie die Vorlagensprache für den Zugriff auf Felder in der HTTP-Antwort. Informationen darüber, wie Sie Felder mithilfe von Vorlagen anpassen können, finden Sie im Abschnitt [Vorlagenkonventionen](#templating-conventions). |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | Zeichenfolge | <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Sie Vorlagen für die Werte in `accessTokenRequest.validations.expectedValue.value` verwenden.</li><li> Verwenden Sie `NONE`, wenn der Wert im Feld `accessTokenRequest.validations.expectedValue.value` eine Konstante ist. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | Zeichenfolge | Verwenden Sie die Vorlagensprache für den Zugriff auf Felder in der HTTP-Antwort. Informationen darüber, wie Sie Felder mithilfe von Vorlagen anpassen können, finden Sie im Abschnitt [Vorlagenkonventionen](#templating-conventions). |

{style="table-layout:auto"}

## Vorlagenkonventionen {#templating-conventions}

Abhängig von Ihrer Autorisierungsanpassung müssen Sie möglicherweise auf Datenfelder in der Autorisierungsantwort zugreifen, wie im vorherigen Abschnitt gezeigt. Machen Sie sich dazu bitte mit der [Pebble-Vorlagensprache](https://pebbletemplates.io/) vertraut, die von Adobe verwendet wird, und lesen Sie die unten stehenden Vorlagenkonventionen, um Ihre OAuth 2-Implementierung anzupassen.


| Präfix | Beschreibung | Beispiel |
|---------|----------|---------|
| authData | Zugriff auf den Wert eines beliebigen Partner- oder Kundendatenfelds. | ``{{ authData.accessToken }}`` |
| response.body | HTTP-Antworttext | ``{{ response.body.access_token }}`` |
| response.status | HTTP-Antwortstatus | ``{{ response.status }}`` |
| response.headers | HTTP-Antwort-Header | ``{{ response.headers.server[0] }}`` |
| userContext | Auf Informationen zum aktuellen Autorisierungsversuch zugreifen | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authorization attempt `</li></ul> |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Durch Lesen dieses Artikels erhalten Sie jetzt Informationen zu den von Adobe Experience Platform unterstützten OAuth 2-Autorisierungsmustern und erfahren, wie Sie Ihr Ziel mit OAuth 2-Autorisierungsunterstützung konfigurieren. Als Nächstes können Sie Ihr OAuth 2-unterstütztes Ziel mithilfe von Destination SDK einrichten. Lesen Sie [Verwenden von Destination SDK, um Ihr Ziel zu konfigurieren](../../guides/configure-destination-instructions.md) für die nächsten Schritte.
