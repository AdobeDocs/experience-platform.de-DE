---
description: Verwenden Sie Vorlagen für Zielgruppen-Metadaten, um Zielgruppen in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Adobe bietet eine erweiterungsfähige Vorlage für Zielgruppen-Metadaten, die Sie anhand der Spezifikationen Ihrer Marketing-API konfigurieren können. Nachdem Sie die Vorlage definiert, getestet und gesendet haben, wird sie von Adobe zur Strukturierung der API-Aufrufe an Ihr Ziel verwendet.
title: Verwaltung von Zielgruppen-Metadaten
source-git-commit: e69bd819fb8ef6c2384a2b843542d1ddcea0661f
workflow-type: ht
source-wordcount: '1038'
ht-degree: 100%

---


# Verwaltung von Zielgruppen-Metadaten

Verwenden Sie Vorlagen für Zielgruppen-Metadaten, um Zielgruppen in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Adobe bietet eine erweiterungsfähige Vorlage für Zielgruppen-Metadaten, die Sie anhand der Spezifikationen Ihrer Marketing-API konfigurieren können. Nachdem Sie die Konfiguration definiert, getestet und gesendet haben, wird sie von Adobe zur Strukturierung der API-Aufrufe an Ihr Ziel verwendet.

Sie können die in diesem Dokument beschriebenen Funktionen mithilfe des API-Endpunkts `/authoring/audience-templates` konfigurieren. Eine vollständige Liste der Vorgänge, die Sie mit dem Endpunkt durchführen können, finden Sie unter [Erstellen einer Metadatenvorlage](../metadata-api/create-audience-template.md).

## Wann Sie den Endpunkt für die Verwaltung von Zielgruppen-Metadaten verwenden sollten {#when-to-use}

Abhängig von Ihrer API-Konfiguration müssen Sie möglicherweise den Endpunkt für die Verwaltung von Zielgruppen-Metadaten verwenden, während Sie Ihr Ziel in Experience Platform konfigurieren. Der unten stehende Entscheidungsbaum verdeutlicht, wann der Endpunkt für Zielgruppen-Metadaten verwendet werden muss und wie Sie eine Vorlage für Zielgruppen-Metadaten für Ihr Ziel konfiguren.

![Entscheidungsbaum](../assets/functionality/audience-metadata-decision-tree.png)

## Anwendungsfälle, die durch die Verwaltung von Zielgruppen-Metadaten unterstützt werden {#use-cases}

Dank der Unterstützung von Zielgruppen-Metadaten in Destination SDK können Sie bei der Konfiguration Ihres Experience Platform-Ziels den Benutzerinnen und Benutzern von Platform eine von mehreren Optionen bieten, wenn sie Segmente Ihrem Ziel zuordnen und aktivieren. Sie können die Optionen, die den Benutzerinnen und Benutzern zur Verfügung stehen, über die Parameter im Abschnitt [Zielgruppen-Metadatenkonfiguration](../functionality/destination-configuration/audience-metadata-configuration.md) der Zielkonfiguration steuern.

### Anwendungsfall 1: Sie verfügen über eine Drittanbieter-API, und Benutzerinnen und Benutzer müssen keine Zuordnungs-IDs angeben

Wenn Sie über einen API-Endpunkt zum Erstellen, Aktualisieren und Löschen von Segmenten oder Zielgruppen verfügen, können Sie Destination SDK mithilfe von Vorlagen für Zielgruppen-Metadaten so konfigurieren, dass es den Spezifikationen Ihres Segmentendpunkts zum Erstellen/Aktualisieren/Löschen entspricht. Experience Platform kann Segmente programmgesteuert erstellen, aktualisieren und löschen sowie Metadaten erneut synchronisieren.

Beim Aktivieren von Segmenten für Ihr Ziel in der Benutzeroberfläche von Experience Platform müssen Benutzerinnen und Benutzer im Aktivierungs-Workflow das Feld für die Segmentzuordnungs-ID nicht manuell ausfüllen.

### Anwendungsfall 2: Benutzerinnen und Benutzer müssen zuerst ein Segment in Ihrem Ziel erstellen und die Zuordnungs-ID manuell eingeben

Wenn Segmente und andere Metadaten von Partnern oder Benutzerinnen bzw. Benutzern manuell in Ihrem Ziel erstellt werden müssen, müssen die Benutzerinnen und Benutzer das Feld für die Segmentzuordnungs-ID im Aktivierungs-Workflow manuell ausfüllen, um die Segmentmetadaten zwischen Ihrem Ziel und Experience Platform zu synchronisieren.

![Eingabe Zuordnungs-ID](../assets/functionality/input-mapping-id.png)

### Anwendungsfall 3: Ihr Ziel akzeptiert die Segment-ID von Experience Platform, und Benutzerinnen und Benutzer müssen die Zuordnungs-ID nicht manuell eingeben

Wenn Ihr Zielsystem die Segment-ID von Experience Platform akzeptiert, können Sie diese in der Vorlage Ihrer Zielgruppen-Metadaten konfigurieren. Benutzerinnen und Benutzer müssen beim Aktivieren eines Segments keine Segmentzuordnungs-ID ausfüllen.

## Generische und erweiterbare Zielgruppenvorlage {#generic-and-extensible}

Für die oben aufgeführten Anwendungsfälle bietet Ihnen Adobe eine generische Vorlage, die Sie an Ihre API-Spezifikationen anpassen können.

Sie können die generische Vorlage zur [Erstellung einer neuen Zielgruppenvorlage](../metadata-api/create-audience-template.md) verwenden, wenn Ihre API Folgendes unterstützt:

* Die HTTP-Methoden: POST, GET, PUT, DELETE, PATCH
* Die Authentifizierungstypen: OAuth 1, OAuth 2 mit Aktualisierungs-Token, OAuth 2 mit Bearer-Token
* Die Funktionen: Erstellen einer Zielgruppe, Aktualisieren einer Zielgruppe, Abrufen einer Zielgruppe, Löschen einer Zielgruppe, Validieren der Anmeldeinformationen

Das Engineering-Team von Adobe ist Ihnen gern dabei behilflich, die generische Vorlage mit benutzerdefinierten Feldern zu erweitern, wenn dies für Ihre Anwendungsfälle erforderlich ist.

## Konfigurationsbeispiele {#configuration-examples}

Dieser Abschnitt enthält drei Beispiele für allgemeine Konfigurationen von Zielgruppen-Metadaten sowie Beschreibungen der wichtigsten Abschnitte der Konfiguration. Beachten Sie, wie sich URL, Kopfzeilen sowie der Aufbau von Anfrage und Antwort zwischen den drei Beispielkonfigurationen unterscheiden. Dies liegt an den unterschiedlichen Spezifikationen der Marketing-API der drei Beispielplattformen.

Beachten Sie, dass in einigen Beispielen Makro-Felder wie `{{authData.accessToken}}` oder `{{segment.name}}` in der URL und in anderen Beispielen in den Kopfzeilen oder im Anfragetext verwendet werden. Das hängt von den Spezifikationen Ihrer Marketing-API ab.

| Vorlagenbereich | Beschreibung |
|--- |--- |
| `create` | Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Kopfzeilen, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen, Segmente und Zielgruppen in Ihrer Plattform programmgesteuert zu erstellen und die erhaltenen Informationen mit Adobe Experience Platform zu synchronisieren. |
| `update` | Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Kopfzeilen, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen, Segmente und Zielgruppen in Ihrer Plattform programmgesteuert zu aktualisieren und die erhaltenen Informationen mit Adobe Experience Platform zu synchronisieren. |
| `delete` | Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Kopfzeilen, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen sowie Segmente und Zielgruppen in Ihrer Plattform programmgesteuert zu löschen. |
| `validate` | Führt Überprüfungen für alle Felder in der Vorlagenkonfiguration durch, bevor Sie die Partner-API aufrufen. Sie können beispielsweise überprüfen, ob die Account-ID des Benutzers korrekt eingegeben wurde. |
| `notify` | Gilt nur für dateibasierte Ziele. Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Header, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen und Sie über erfolgreiche Dateiexporte zu informieren. |

{style="table-layout:auto"}

### Streaming-Beispiel 1 {#example-1}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

### Streaming-Beispiel 2 {#example-2}

```json
{
   "instanceId":"12c78017-5af3-4d4e-8f9c-d330c547c482",
   "createdDate":"2021-07-20T13:27:37.029490Z",
   "lastModifiedDate":"2021-07-20T18:53:03.622306Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}
```

### Streaming-Beispiel 3 {#example-3}

```json
{
   "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
   "createdDate":"2021-07-20T13:30:30.843054Z",
   "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v2/dmpSegments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{authData.accessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "name":"{{segment.name}}",
               "type":"USER",
               "account":"{{customerData.accountId}}",
               "accessPolicy":"PRIVATE",
               "destinations":[
                  {
                     "destination":"MOVIESTAR"
                  }
               ],
               "sourcePlatform":"ADOBE"
            }
         },
         "responseFields":[
            {
               "value":"{{headers.x-moviestar-id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{authData.accessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "patch":{
                  "$set":{
                     "name":"{{segment.name}}"
                  }
               }
            }
         },
         "responseErrorFields":[
            {
               "value":"{{message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{authData.accessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{message}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar audience template - Third example"
   }
}
```


### Dateibasiertes Beispiel {#example-file-based}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "notify":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

Beschreibungen aller Parameter in der Vorlage finden Sie in der API-Referenz zum [Erstellen einer Zielgruppenvorlage](../metadata-api/create-audience-template.md).

## Verwendete Makros in Vorlagen für Zielgruppen-Metadaten

Um Informationen wie Segment-IDs, Zugriffstoken, Fehlermeldungen und mehr zwischen Experience Platform und Ihrer API zu übermitteln, enthalten die Zielgruppenvorlagen Makros. Im Folgenden finden Sie eine Beschreibung der Makros, die in den drei Konfigurationsbeispielen auf dieser Seite verwendet werden:

| Makro | Beschreibung |
|--- |--- |
| `{{segment.alias}}` | Ermöglicht den Zugriff auf den Alias des Segments in Experience Platform. |
| `{{segment.name}}` | Ermöglicht den Zugriff auf den Namen des Segments in Experience Platform. |
| `{{segment.id}}` | Ermöglicht den Zugriff auf die ID des Segments in Experience Platform. |
| `{{customerData.accountId}}` | Ermöglicht den Zugriff auf das Feld „Konto-ID“, das Sie in der Zielkonfiguration eingerichtet haben. |
| `{{oauth2ServiceAccessToken}}` | Ermöglicht Ihnen die dynamische Generierung eines Zugriffs-Tokens basierend auf Ihrer OAuth 2-Konfiguration. |
| `{{authData.accessToken}}` | Ermöglicht die Weitergabe des Zugriffs-Tokens an den API-Endpunkt. Verwenden Sie `{{authData.accessToken}}`, wenn Experience Platform nicht ablaufende Token verwenden soll, um eine Verbindung zu Ihrem Ziel herzustellen. Andernfalls verwenden Sie `{{oauth2ServiceAccessToken}}`, um ein Zugriffs-Token zu generieren. |
| `{{body.segments[0].segment.id}}` | Gibt die eindeutige Kennung der erstellten Zielgruppe als Wert des Schlüssels `externalAudienceId` zurück. |
| `{{error.message}}` | Gibt eine Fehlermeldung zurück, die Benutzerinnen und Benutzern in der Benutzeroberfläche von Experience Platform angezeigt wird. |

{style="table-layout:auto"}
