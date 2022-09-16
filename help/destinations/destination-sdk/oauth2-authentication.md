---
description: Auf dieser Seite werden die verschiedenen von Destination SDK unterstützten OAuth 2-Authentifizierungsflüsse beschrieben und Anweisungen zum Einrichten der OAuth 2-Authentifizierung für Ihr Ziel bereitgestellt.
title: OAuth 2-Authentifizierung
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 87fb3ffa65449b61e05d94d2b56daf727ecebdea
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 6%

---

# OAuth 2-Authentifizierung

## Übersicht {#overview}

Verwenden Sie Destination SDK, damit Adobe Experience Platform mithilfe der [OAuth 2-Authentifizierungs-Framework](https://tools.ietf.org/html/rfc6749).

Auf dieser Seite werden die verschiedenen von Destination SDK unterstützten OAuth 2-Authentifizierungsflüsse beschrieben und Anweisungen zum Einrichten der OAuth 2-Authentifizierung für Ihr Ziel bereitgestellt.

## Hinzufügen von OAuth 2-Authentifizierungsdetails zur Zielkonfiguration {#how-to-setup}

### Voraussetzungen in Ihrem System {#prerequisites}

Als ersten Schritt müssen Sie eine App in Ihrem System für Adobe Experience Platform erstellen oder anderweitig die Experience Platform in Ihrem System registrieren. Das Ziel besteht darin, eine Client-ID und ein Client-Geheimnis zu generieren, die zum Authentifizieren der Experience Platform für Ihr Ziel erforderlich sind. Als Teil dieser Konfiguration in Ihrem System benötigen Sie die Adobe Experience Platform OAuth 2-Umleitungs-/Callback-URLs, die Sie aus der folgenden Liste erhalten können.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>Der Schritt zum Registrieren einer Umleitungs-/Callback-URL für Adobe Experience Platform in Ihrem System ist nur für das [OAuth 2 mit Autorisierungscode](./oauth2-authentication.md#authorization-code) Grant-Typ. Für die beiden anderen unterstützten Grant-Typen (Kennwort und Client-Anmeldeinformationen) können Sie diesen Schritt überspringen.

Am Ende dieses Schritts sollten Sie Folgendes haben:
* eine Client-ID;
* Client-Geheimnis;
* Callback-URL der Adobe (für die Gewährung des Autorisierungscodes).

### Was Sie in Destination SDK tun müssen {#to-do-in-destination-sdk}

Um die OAuth 2-Authentifizierung für Ihr Ziel in Experience Platform einzurichten, müssen Sie Ihre OAuth 2-Details zum [Zielkonfiguration](./destination-configuration.md)unter `customerAuthenticationConfigurations` -Parameter mithilfe der `platform.adobe.io/data/core/activation/authoring/destinations` [API-Endpunkt](./destination-configuration-api.md). Siehe [Beispielkonfiguration](./destination-configuration.md#example-configuration). Spezifische Anweisungen dazu, welche Felder Sie Ihrer Konfigurationsvorlage hinzufügen müssen, abhängig vom OAuth 2-Authentifizierungs-Grant-Typ, finden Sie weiter unten auf dieser Seite.

## Unterstützte OAuth 2-Grant-Typen {#oauth2-grant-types}

Experience Platform unterstützt die drei OAuth 2-Grant-Typen in der folgenden Tabelle. Wenn Sie ein benutzerdefiniertes OAuth 2-Setup haben, kann Adobe es mithilfe von benutzerdefinierten Feldern in Ihrer Integration unterstützen. Weitere Informationen finden Sie in den Abschnitten zu den einzelnen Fördertypen.

>[!IMPORTANT]
>
>* Sie geben die Eingabeparameter wie in den folgenden Abschnitten beschrieben an. Adobe-interne Systeme stellen eine Verbindung zum Authentifizierungssystem Ihrer Plattform her und erfassen Ausgabeparameter, mit denen der Benutzer authentifiziert und die Authentifizierung für Ihr Ziel verwaltet wird.
>* Die in der Tabelle fett hervorgehobenen Eingabeparameter sind erforderliche Parameter im OAuth 2-Authentifizierungsfluss. Die anderen Parameter sind optional. Es gibt weitere benutzerdefinierte Eingabeparameter, die hier nicht angezeigt werden, aber in den Abschnitten ausführlich beschrieben werden [Anpassen der OAuth 2-Konfiguration](./oauth2-authentication.md#customize-configuration) und [Aktualisierung des Zugriffstokens](./oauth2-authentication.md#access-token-refresh).


| OAuth 2 Grant | Eingaben | Ausgaben |
|---------|----------|---------|
| Autorisierungscode | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Passwort | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>accessTokenUrl</b></li><li><b>Benutzername</b></li><li><b>Passwort</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| Client Credential | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

In der obigen Tabelle sind die Felder aufgeführt, die in standardmäßigen OAuth 2-Flüssen verwendet werden. Zusätzlich zu diesen Standardfeldern können verschiedene Partnerintegrationen zusätzliche Eingaben und Ausgaben erfordern. Adobe hat ein flexibles OAuth 2-Authentifizierungs-/Autorisierungs-Framework für die Destination SDK entwickelt, das Varianten des obigen Standardfeldmusters handhaben kann und gleichzeitig einen Mechanismus zur automatischen Neuerstellung ungültiger Ausgaben unterstützt, z. B. abgelaufene Zugriffstoken.

Die Ausgabe enthält in allen Fällen ein Zugriffstoken, das von Experience Platform verwendet wird, um sich zu authentifizieren und die Authentifizierung für Ihr Ziel zu verwalten.

Das System, das von Adobe für die OAuth 2-Authentifizierung entwickelt wurde:
* Unterstützt alle drei OAuth 2-Stipendien und berücksichtigt dabei alle Variationen in ihnen, z. B. zusätzliche Datenfelder, nicht standardmäßige API-Aufrufe und mehr.
* Unterstützt Zugriffstoken mit variierenden Lebenszeitwerten (90 Tage, 30 Minuten oder beliebige andere von Ihnen angegebene Lebenszeitwerte).
* Unterstützt OAuth 2-Autorisierungsflüsse mit oder ohne Aktualisierungstoken.

## OAuth 2 mit Autorisierungscode {#authorization-code}

Wenn Ihr Ziel einen standardmäßigen OAuth 2.0-Autorisierungscode-Fluss unterstützt (lesen Sie den Abschnitt [RFC-Standardspezifikationen](https://tools.ietf.org/html/rfc6749#section-4.1)) oder eine Variante davon, lesen Sie die erforderlichen und optionalen Felder unten:

| OAuth 2 Grant | Eingaben | Ausgaben |
|---------|----------|---------|
| Autorisierungscode | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

Um diese Authentifizierungsmethode für Ihr Ziel einzurichten, fügen Sie die folgenden Zeilen zu Ihrer Konfiguration hinzu: `/destinations` [Endpunkt](./destination-configuration.md):

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
| `authType` | Zeichenfolge | Verwenden Sie &quot;OAUTH2&quot;. |
| `grant` | Zeichenfolge | Verwenden Sie &quot;OAUTH2_AUTHORIZATION_CODE&quot;. |
| `accessTokenUrl` | Zeichenfolge | Die URL auf Ihrer Seite, die Zugriffstoken und optional Token zur Aktualisierung ausgibt. |
| `authorizationUrl` | Zeichenfolge | Die URL Ihres Autorisierungsservers, über die Sie den Benutzer zur Anmeldung bei der Anwendung weiterleiten. |
| `refreshTokenUrl` | Zeichenfolge | *Optional.* Die URL auf Ihrer Seite, die Aktualisierungstoken ausgibt. Häufig wird die `refreshTokenUrl` ist identisch mit dem `accessTokenUrl`. |
| `clientId` | Zeichenfolge | Die Client-ID, die Ihr System Adobe Experience Platform zuweist. |
| `clientSecret` | Zeichenfolge | Das Client-Geheimnis, das Ihr System Adobe Experience Platform zuweist. |
| `scope` | Liste von Zeichenfolgen | *Optional*. Legen Sie den Umfang fest, den das Zugriffstoken der Experience Platform für Ihre Ressourcen ermöglicht. Beispiel: &quot;lesen, schreiben&quot;. |

{style=&quot;table-layout:auto&quot;}

## OAuth 2 mit Passwortgewährung

Für die OAuth 2 Password Grant (lesen Sie die [RFC-Standardspezifikationen](https://tools.ietf.org/html/rfc6749#section-4.3)), erfordert die Experience Platform den Benutzernamen und das Kennwort des Benutzers. Im Authentifizierungsfluss tauscht Experience Platform diese Anmeldeinformationen gegen ein Zugriffstoken und optional ein Aktualisierungstoken aus.
Adobe verwendet die folgenden Standardeingaben, um die Zielkonfiguration zu vereinfachen und Werte zu überschreiben:

| OAuth 2 Grant | Eingaben | Ausgaben |
|---------|----------|---------|
| Passwort | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>accessTokenUrl</b></li><li><b>Benutzername</b></li><li><b>Passwort</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> Sie müssen keine Parameter für `username` und `password` in der unten stehenden Konfiguration. Wenn Sie `"grant": "OAUTH2_PASSWORD"` In der Zielkonfiguration fordert das System den Benutzer auf, in der Experience Platform-Benutzeroberfläche einen Benutzernamen und ein Kennwort anzugeben, wenn er sich bei Ihrem Ziel authentifiziert.

Um diese Authentifizierungsmethode für Ihr Ziel einzurichten, fügen Sie die folgenden Zeilen zu Ihrer Konfiguration hinzu: `/destinations` [Endpunkt](./destination-configuration.md):

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
| `authType` | Zeichenfolge | Verwenden Sie &quot;OAUTH2&quot;. |
| `grant` | Zeichenfolge | Verwenden Sie &quot;OAUTH2_PASSWORD&quot;. |
| `accessTokenUrl` | Zeichenfolge | Die URL auf Ihrer Seite, die Zugriffstoken und optional Token zur Aktualisierung ausgibt. |
| `clientId` | Zeichenfolge | Die Client-ID, die Ihr System Adobe Experience Platform zuweist. |
| `clientSecret` | Zeichenfolge | Das Client-Geheimnis, das Ihr System Adobe Experience Platform zuweist. |
| `scope` | Liste von Zeichenfolgen | *Optional*. Legen Sie den Umfang fest, den das Zugriffstoken der Experience Platform für Ihre Ressourcen ermöglicht. Beispiel: &quot;lesen, schreiben&quot;. |

{style=&quot;table-layout:auto&quot;}

## OAuth 2 mit Client Credentials Grant

Sie können eine OAuth 2 Client-Anmeldedaten konfigurieren (lesen Sie den Abschnitt [RFC-Standardspezifikationen](https://tools.ietf.org/html/rfc6749#section-4.4)) Ziel, das die unten aufgeführten Standardeingaben und -ausgänge unterstützt. Sie können die Werte anpassen. Siehe [Anpassen der OAuth 2-Konfiguration](./oauth2-authentication.md#customize-configuration) für Details.

| OAuth 2 Grant | Eingaben | Ausgaben |
|---------|----------|---------|
| Client-Anmeldedaten | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>Scope (Umfang)</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style=&quot;table-layout:auto&quot;}

Um diese Authentifizierungsmethode für Ihr Ziel einzurichten, fügen Sie die folgenden Zeilen zu Ihrer Konfiguration hinzu: `/destinations` [Endpunkt](./destination-configuration.md):

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
| `authType` | Zeichenfolge | Verwenden Sie &quot;OAUTH2&quot;. |
| `grant` | Zeichenfolge | Verwenden Sie &quot;OAUTH2_CLIENT_CREDENTIALS&quot;. |
| `accessTokenUrl` | Zeichenfolge | Die URL Ihres Autorisierungsservers, die ein Zugriffstoken und ein optionales Aktualisierungstoken ausgibt. |
| `refreshTokenUrl` | Zeichenfolge | *Optional.* Die URL auf Ihrer Seite, die Aktualisierungstoken ausgibt. Häufig wird die `refreshTokenUrl` ist identisch mit dem `accessTokenUrl`. |
| `clientId` | Zeichenfolge | Die Client-ID, die Ihr System Adobe Experience Platform zuweist. |
| `clientSecret` | Zeichenfolge | Das Client-Geheimnis, das Ihr System Adobe Experience Platform zuweist. |
| `scope` | Liste von Zeichenfolgen | *Optional*. Legen Sie den Umfang fest, den das Zugriffstoken der Experience Platform für Ihre Ressourcen ermöglicht. Beispiel: &quot;lesen, schreiben&quot;. |

{style=&quot;table-layout:auto&quot;}

## Anpassen der OAuth 2-Konfiguration {#customize-configuration}

Die in den obigen Abschnitten beschriebenen Konfigurationen beschreiben standardmäßige OAuth 2-Zuschüsse. Das von Adobe entworfene System bietet jedoch Flexibilität, sodass Sie benutzerdefinierte Parameter für alle Variationen der OAuth 2-Förderung verwenden können. Um die standardmäßigen OAuth 2-Einstellungen anzupassen, verwenden Sie die `authenticationDataFields` Parameter, wie in den Beispielen unten dargestellt.

### Beispiel 1: Verwenden `authenticationDataFields` zur Erfassung von Informationen aus der Authentifizierungsantwort {#example-1}

In diesem Beispiel verfügt eine Zielplattform über Aktualisierungstoken, die nach einer bestimmten Zeitdauer ablaufen. In diesem Fall richtet der Partner die `refreshTokenExpiration` benutzerdefiniertes Feld zum Abrufen des Ablaufs des Aktualisierungstokens aus dem `refresh_token_expires_in` in der API-Antwort.

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

### Beispiel 2: Verwenden `authenticationDataFields` , um ein spezielles Aktualisierungstoken bereitzustellen {#example-2}

In diesem Beispiel richtet ein Partner sein Ziel ein, um ein spezielles Aktualisierungstoken bereitzustellen. Außerdem wird das Ablaufdatum für Zugriffstoken nicht in der API-Antwort zurückgegeben, sodass sie einen Standardwert (in diesem Fall 3600 Sekunden) hartcodieren können.

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

### Beispiel 3: Der Benutzer gibt die Client-ID und das Client-Geheimnis ein, wenn er das Ziel konfiguriert {#example-3}

In diesem Beispiel wird nicht wie im Abschnitt gezeigt eine globale Client-ID und ein Client-Geheimnis erstellt [Voraussetzungen in Ihrem System](./oauth2-authentication.md#prerequisites), muss der Kunde die Client-ID, das Client-Geheimnis und die Konto-ID eingeben (die ID, die der Kunde zum Anmelden am Ziel verwendet).

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



Sie können die folgenden Parameter in `authenticationDataFields` Anpassen der OAuth 2-Konfiguration:

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `authenticationDataFields.name` | Zeichenfolge | Der Name des benutzerdefinierten Felds. |
| `authenticationDataFields.title` | Zeichenfolge | Ein Titel, den Sie für das benutzerdefinierte Feld angeben können. |
| `authenticationDataFields.description` | Zeichenfolge | Eine Beschreibung des von Ihnen eingerichteten benutzerdefinierten Datenfelds. |
| `authenticationDataFields.type` | Zeichenfolge | Definiert den Typ des benutzerdefinierten Datenfelds. <br> Akzeptierte Werte: `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | Boolesch | Gibt an, ob das benutzerdefinierte Datenfeld im Authentifizierungsfluss erforderlich ist. |
| `authenticationDataFields.format` | Zeichenfolge | Wenn Sie `"format":"password"`, verschlüsselt Adobe den Wert des Authentifizierungsdatenfelds. Bei Verwendung mit `"fieldType": "CUSTOMER"`wird die Eingabe auch in der Benutzeroberfläche ausgeblendet, wenn der Benutzer in das Feld eingibt. |
| `authenticationDataFields.fieldType` | Zeichenfolge | Gibt an, ob die Eingabe vom Partner (Sie) oder vom Benutzer stammt, wenn dieser Ihr Ziel in Experience Platform eingerichtet hat. |
| `authenticationDataFields.value` | Zeichenfolge. Boolesch. Ganzzahl | Der -Wert des benutzerdefinierten Datenfelds. Der Wert entspricht dem ausgewählten Typ aus `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | Zeichenfolge | Gibt an, auf welches Feld aus dem API-Antwortpfad verwiesen wird. |

{style=&quot;table-layout:auto&quot;}

## Aktualisierung des Zugriffstokens {#access-token-refresh}

Adobe hat ein System entwickelt, das abgelaufene Zugriffstoken aktualisiert, ohne dass der Benutzer sich wieder bei Ihrer Plattform anmelden muss. Das System kann ein neues Token generieren, sodass die Aktivierung an Ihr Ziel nahtlos für den Kunden fortgesetzt wird.

Um die Aktualisierung des Zugriffstokens einzurichten, müssen Sie möglicherweise eine vorlagenbasierte HTTP-Anforderung konfigurieren, die es der Adobe ermöglicht, mithilfe eines Aktualisierungstokens ein neues Zugriffstoken zu erhalten. Wenn das Zugriffstoken abgelaufen ist, verwendet Adobe die von Ihnen bereitgestellte Vorlagenanforderung und fügt die von Ihnen angegebenen Parameter hinzu. Verwenden Sie die `accessTokenRequest` Parameter zum Konfigurieren eines Aktualisierungsmechanismus für Zugriffstoken.


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

Sie können die folgenden Parameter in `accessTokenRequest` , um Ihren Token-Aktualisierungsprozess anzupassen:

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | Zeichenfolge | Verwenden Sie `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | Zeichenfolge | <ul><li>Verwendung `PEBBLE_V1` wenn Sie Vorlagen für den Wert in `accessTokenRequest.urlBasedDestination.url.value`.</li><li> Verwendung `NONE` wenn der Wert im Feld `accessTokenRequest.urlBasedDestination.url.value` ist eine Konstante. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | Zeichenfolge | Die URL, an die Experience Platform das Zugriffstoken anfordert. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | Zeichenfolge | <ul><li>Verwendung `PEBBLE_V1` Wenn Sie Vorlagen für die Werte in `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> Verwendung `NONE` wenn der Wert im Feld `accessTokenRequest.httpTemplate.requestBody.value` ist eine Konstante. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | Zeichenfolge | Verwenden Sie die Vorlagensprache, um Felder in der HTTP-Anfrage an den Zugriffstoken-Endpunkt anzupassen. Informationen zur Verwendung der Vorlage zum Anpassen von Feldern finden Sie im Abschnitt [Vorlagenkonventionen](./oauth2-authentication.md#templating-conventions) Abschnitt. |
| `accessTokenRequest.httpTemplate.httpMethod` | Zeichenfolge | Gibt die HTTP-Methode an, die zum Aufrufen Ihres Zugriffstoken-Endpunkts verwendet wird. In den meisten Fällen ist dieser Wert `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | Zeichenfolge | Gibt den Inhaltstyp des HTTP-Aufrufs für Ihren Zugriffstoken-Endpunkt an. <br> Beispiel: `application/x-www-form-urlencoded` oder `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | Zeichenfolge | Gibt an, ob dem HTTP-Aufruf an Ihren Zugriffstoken-Endpunkt Kopfzeilen hinzugefügt werden sollen. |
| `accessTokenRequest.responseFields.templatingStrategy` | Zeichenfolge | <ul><li>Verwendung `PEBBLE_V1` Wenn Sie Vorlagen für die Werte in `accessTokenRequest.responseFields.value`.</li><li> Verwendung `NONE` wenn der Wert im Feld `accessTokenRequest.responseFields.value` ist eine Konstante. </li></li> |
| `accessTokenRequest.responseFields.value` | Zeichenfolge | Verwenden Sie die Vorlagensprache, um über Ihren Zugriffstoken-Endpunkt auf Felder in der HTTP-Antwort zuzugreifen. Informationen zur Verwendung der Vorlage zum Anpassen von Feldern finden Sie im Abschnitt [Vorlagenkonventionen](./oauth2-authentication.md#templating-conventions) Abschnitt. |
| `accessTokenRequest.validations.name` | Zeichenfolge | Gibt den Namen an, den Sie für diese Validierung angegeben haben. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | Zeichenfolge | <ul><li>Verwendung `PEBBLE_V1` Wenn Sie Vorlagen für die Werte in `accessTokenRequest.validations.actualValue.value`.</li><li> Verwendung `NONE` wenn der Wert im Feld `accessTokenRequest.validations.actualValue.value` ist eine Konstante. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | Zeichenfolge | Verwenden Sie die Vorlagensprache für den Zugriff auf Felder in der HTTP-Antwort. Informationen zur Verwendung der Vorlage zum Anpassen von Feldern finden Sie im Abschnitt [Vorlagenkonventionen](./oauth2-authentication.md#templating-conventions) Abschnitt. |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | Zeichenfolge | <ul><li>Verwendung `PEBBLE_V1` Wenn Sie Vorlagen für die Werte in `accessTokenRequest.validations.expectedValue.value`.</li><li> Verwendung `NONE` wenn der Wert im Feld `accessTokenRequest.validations.expectedValue.value` ist eine Konstante. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | Zeichenfolge | Verwenden Sie die Vorlagensprache für den Zugriff auf Felder in der HTTP-Antwort. Informationen zur Verwendung der Vorlage zum Anpassen von Feldern finden Sie im Abschnitt [Vorlagenkonventionen](./oauth2-authentication.md#templating-conventions) Abschnitt. |

{style=&quot;table-layout:auto&quot;}

## Vorlagenkonventionen {#templating-conventions}

Abhängig von Ihrer Authentifizierungsanpassung müssen Sie möglicherweise auf Datenfelder in der Authentifizierungsantwort zugreifen, wie im vorherigen Abschnitt gezeigt. Machen Sie sich dazu bitte mit der [Pebble-Vorlagensprache](https://pebbletemplates.io/) , die von Adobe verwendet werden, und lesen Sie die unten stehenden Vorlagenkonventionen, um Ihre OAuth 2-Implementierung anzupassen.


| Präfix | Beschreibung | Beispiel |
|---------|----------|---------|
| authData | Zugriff auf den Wert eines beliebigen Partner- oder Kundendatenfelds. | ``{{ authData.accessToken }}`` |
| response.body | HTTP-Antworttext | ``{{ response.body.access_token }}`` |
| response.status | HTTP-Antwortstatus | ``{{ response.status }}`` |
| response.headers | HTTP-Antwortheader | ``{{ response.headers.server[0] }}`` |
| userContext | Auf Informationen zum aktuellen Authentifizierungsversuch zugreifen | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authentication attempt `</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte {#next-steps}

Durch Lesen dieses Artikels erhalten Sie jetzt Informationen zu den von Adobe Experience Platform unterstützten OAuth 2-Authentifizierungsmustern und erfahren, wie Sie Ihr Ziel mit OAuth 2-Authentifizierungsunterstützung konfigurieren. Als Nächstes können Sie Ihr OAuth 2-unterstütztes Ziel mithilfe von Destination SDK einrichten. Lesen [Verwenden Sie Destination SDK, um Ihr Ziel zu konfigurieren](./configure-destination-instructions.md) für die nächsten Schritte.
