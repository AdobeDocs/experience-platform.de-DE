---
description: Verwenden Sie Vorlagen für Zielgruppen-Metadaten, um Zielgruppen in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Adobe bietet eine erweiterungsfähige Vorlage für Zielgruppen-Metadaten, die Sie anhand der Spezifikationen Ihrer Marketing-API konfigurieren können. Nachdem Sie die Vorlage definiert, getestet und gesendet haben, wird sie von Adobe zur Strukturierung der API-Aufrufe an Ihr Ziel verwendet.
title: Verwaltung von Zielgruppen-Metadaten
exl-id: 795e8adb-c595-4ac5-8d1a-7940608d01cd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 73%

---

# Verwaltung von Zielgruppen-Metadaten

Verwenden Sie Vorlagen für Zielgruppen-Metadaten, um Zielgruppen in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Adobe bietet eine erweiterungsfähige Vorlage für Zielgruppen-Metadaten, die Sie anhand der Spezifikationen Ihrer Marketing-API konfigurieren können. Nachdem Sie die Konfiguration definiert, getestet und gesendet haben, wird sie von Adobe zur Strukturierung der API-Aufrufe an Ihr Ziel verwendet.

Sie können die in diesem Dokument beschriebenen Funktionen mithilfe des API-Endpunkts `/authoring/audience-templates` konfigurieren. Eine vollständige Liste der Vorgänge, die Sie mit dem Endpunkt durchführen können, finden Sie unter [Erstellen einer Metadatenvorlage](../metadata-api/create-audience-template.md).

## Wann Sie den Endpunkt für die Verwaltung von Zielgruppen-Metadaten verwenden sollten {#when-to-use}

Abhängig von Ihrer API-Konfiguration müssen Sie möglicherweise den Endpunkt für die Verwaltung von Zielgruppen-Metadaten verwenden, während Sie Ihr Ziel in Experience Platform konfigurieren. Der unten stehende Entscheidungsbaum verdeutlicht, wann der Endpunkt für Zielgruppen-Metadaten verwendet werden muss und wie Sie eine Vorlage für Zielgruppen-Metadaten für Ihr Ziel konfiguren.

![Entscheidungsbaum](../assets/functionality/audience-metadata-decision-tree.png)

## Anwendungsfälle, die durch die Verwaltung von Zielgruppen-Metadaten unterstützt werden {#use-cases}

Dank der Unterstützung von Zielgruppen-Metadaten in Destination SDK können Sie bei der Konfiguration Ihres Experience Platform-Ziels Experience Platform-Benutzern eine von mehreren Optionen bieten, wenn sie Zielgruppen Ihrem Ziel zuordnen und aktivieren. Sie können die Optionen, die den Benutzerinnen und Benutzern zur Verfügung stehen, über die Parameter im Abschnitt [Zielgruppen-Metadatenkonfiguration](../functionality/destination-configuration/audience-metadata-configuration.md) der Zielkonfiguration steuern.

### Anwendungsfall 1: Sie verfügen über eine Drittanbieter-API, und Benutzerinnen und Benutzer müssen keine Zuordnungs-IDs angeben

Wenn Sie über einen API-Endpunkt zum Erstellen, Aktualisieren und Löschen von Zielgruppen verfügen, können Sie Destination SDK mithilfe von Vorlagen für Zielgruppen-Metadaten so konfigurieren, dass es den Spezifikationen Ihres Zielgruppenendpunkts zum Erstellen/Aktualisieren/Löschen entspricht. Experience Platform kann Zielgruppen programmgesteuert erstellen, aktualisieren und löschen sowie Metadaten erneut synchronisieren.

Beim Aktivieren von Zielgruppen für Ihr Ziel in der Benutzeroberfläche von Experience Platform brauchen Benutzerinnen und Benutzer im Aktivierungs-Workflow das Feld für die Zielgruppenzuordnungs-ID nicht manuell auszufüllen.

### Anwendungsfall 2: Benutzerinnen und Benutzer müssen zuerst ein Zielgruppe in Ihrem Ziel erstellen und die Zuordnungs-ID manuell eingeben

Wenn Zielgruppen- und andere Metadaten von Partnern oder Benutzerinnen bzw. Benutzern manuell in Ihrem Ziel erstellt werden müssen, müssen die Benutzerinnen und Benutzer das Feld für die Segmentzuordnungs-ID im Aktivierungs-Workflow manuell ausfüllen, um die Zielgruppen-Metadaten zwischen Ihrem Ziel und Experience Platform zu synchronisieren.

![Eingabe-Zuordnungs-ID](../assets/functionality/input-mapping-id.png)

### Anwendungsfall 3: Ihr Ziel akzeptiert die Zielgruppen-ID von Experience Platform, und Benutzerinnen und Benutzer brauchen die Zuordnungs-ID nicht manuell einzugeben

Wenn Ihr Zielsystem die Zielgruppen-ID von Experience Platform akzeptiert, können Sie diese in der Vorlage Ihrer Zielgruppen-Metadaten konfigurieren. Benutzerinnen und Benutzer müssen beim Aktivieren eines Segments keine Zielgruppen-ID ausfüllen.

## Generische und erweiterbare Zielgruppenvorlage {#generic-and-extensible}

Für die oben aufgeführten Anwendungsfälle bietet Ihnen Adobe eine generische Vorlage, die Sie an Ihre API-Spezifikationen anpassen können.

Sie können die generische Vorlage zur [Erstellung einer neuen Zielgruppenvorlage](../metadata-api/create-audience-template.md) verwenden, wenn Ihre API Folgendes unterstützt:

* Die HTTP-Methoden: POST, GET, PUT, DELETE, PATCH
* Die Authentifizierungstypen: OAuth 1, OAuth 2 mit Aktualisierungs-Token, OAuth 2 mit Bearer-Token
* Die Funktionen: Erstellen einer Zielgruppe, Aktualisieren einer Zielgruppe, Abrufen einer Zielgruppe, Löschen einer Zielgruppe, Validieren der Anmeldedaten

Das Engineering-Team von Adobe ist Ihnen gern dabei behilflich, die generische Vorlage mit benutzerdefinierten Feldern zu erweitern, wenn dies für Ihre Anwendungsfälle erforderlich ist.


## Unterstützte Vorlagenereignisse {#supported-events}

In der folgenden Tabelle werden die Ereignisse beschrieben, die von Zielgruppen-Metadatenvorlagen unterstützt werden.

| Vorlagenbereich | Beschreibung |
|--- |--- |
| `create` | Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Kopfzeilen, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen, Segmente und Zielgruppen in Ihrer Plattform programmgesteuert zu erstellen und die erhaltenen Informationen mit Adobe Experience Platform zu synchronisieren. |
| `update` | Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Kopfzeilen, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen, Segmente und Zielgruppen in Ihrer Plattform programmgesteuert zu aktualisieren und die erhaltenen Informationen mit Adobe Experience Platform zu synchronisieren. |
| `delete` | Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Kopfzeilen, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen sowie Segmente und Zielgruppen in Ihrer Plattform programmgesteuert zu löschen. |
| `validate` | Führt Überprüfungen für alle Felder in der Vorlagenkonfiguration durch, bevor Sie die Partner-API aufrufen. Sie können beispielsweise überprüfen, ob die Account-ID des Benutzers korrekt eingegeben wurde. |
| `notify` | Gilt nur für dateibasierte Ziele. Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Header, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen und Sie über erfolgreiche Dateiexporte zu informieren. |
| `createDestination` | Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Kopfzeilen, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen, einen Datenfluss in Ihrer Plattform programmgesteuert zu erstellen und die Informationen wieder mit Adobe Experience Platform zu synchronisieren. |
| `updateDestination` | Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Kopfzeilen, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen, einen Datenfluss in Ihrer Plattform programmgesteuert zu aktualisieren und die Informationen wieder mit Adobe Experience Platform zu synchronisieren. |
| `deleteDestination` | Umfasst alle erforderlichen Komponenten (URL, HTTP-Methode, Kopfzeilen, Anfrage- und Antworttext), um einen HTTP-Aufruf an Ihre API durchzuführen und einen Datenfluss programmgesteuert aus Ihrer Plattform zu löschen. |

{style="table-layout:auto"}

## Konfigurationsbeispiele {#configuration-examples}

Dieser Abschnitt enthält Beispiele für allgemeine Konfigurationen von Zielgruppen-Metadaten.

Beachten Sie, wie sich die URL, die Kopfzeilen und der Anfragetext zwischen den drei Beispielkonfigurationen unterscheiden. Dies liegt an den unterschiedlichen Spezifikationen der Marketing-API der drei Beispielplattformen.

Beachten Sie, dass in einigen Beispielen Makro-Felder wie `{{authData.accessToken}}` oder `{{segment.name}}` in der URL und in anderen Beispielen in den Kopfzeilen oder im Anfragetext verwendet werden. Ihre Verwendung hängt von den Spezifikationen Ihrer Marketing-API ab.

+++Streaming-Beispiel 1

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

+++

+++Streaming-Beispiel 2

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

+++

+++Streaming-Beispiel 3

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

+++

+++Dateibasiertes Beispiel

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

+++

Beschreibungen aller Parameter in der Vorlage finden Sie in der API-Referenz zum [Erstellen einer Zielgruppenvorlage](../metadata-api/create-audience-template.md).

## Verwendete Makros in Vorlagen für Zielgruppen-Metadaten {#macros}

Um Informationen wie Zielgruppen-IDs, Zugriffs-Token, Fehlermeldungen und mehr zwischen Experience Platform und Ihrer API zu übermitteln, enthalten die Vorlagen für Zielgruppen Makros. Im Folgenden finden Sie eine Beschreibung der Makros, die in den drei Konfigurationsbeispielen auf dieser Seite verwendet werden:

| Makro | Beschreibung |
|--- |--- |
| `{{segment.alias}}` | Ermöglicht den Zugriff auf den Alias der Zielgruppe in Experience Platform. |
| `{{segment.name}}` | Ermöglicht den Zugriff auf den Namen der Zielgruppe in Experience Platform. |
| `{{segment.id}}` | Ermöglicht den Zugriff auf die ID der Zielgruppe in Experience Platform. |
| `{{customerData.accountId}}` | Ermöglicht den Zugriff auf das Feld „Konto-ID“, das Sie in der Zielkonfiguration eingerichtet haben. |
| `{{oauth2ServiceAccessToken}}` | Ermöglicht Ihnen die dynamische Generierung eines Zugriffs-Tokens basierend auf Ihrer OAuth 2-Konfiguration. |
| `{{authData.accessToken}}` | Ermöglicht die Weitergabe des Zugriffs-Tokens an den API-Endpunkt. Verwenden Sie `{{authData.accessToken}}`, wenn Experience Platform nicht ablaufende Token verwenden soll, um eine Verbindung zu Ihrem Ziel herzustellen. Andernfalls verwenden Sie `{{oauth2ServiceAccessToken}}`, um ein Zugriffs-Token zu generieren. |
| `{{body.segments[0].segment.id}}` | Gibt die eindeutige Kennung der erstellten Zielgruppe als Wert des Schlüssels `externalAudienceId` zurück. |
| `{{error.message}}` | Gibt eine Fehlermeldung zurück, die Benutzerinnen und Benutzern in der Benutzeroberfläche von Experience Platform angezeigt wird. |
| `{{{segmentEnrichmentAttributes}}}` | Ermöglicht den Zugriff auf alle Anreicherungsattribute für eine bestimmte Zielgruppe.  Dieses Makro wird von den Ereignissen `create`, `update` und `delete` unterstützt. Anreicherungsattribute sind nur für [benutzerdefinierte Upload-Zielgruppen](destination-configuration/schema-configuration.md#external-audiences) verfügbar. Im [Handbuch zur Aktivierung von Batch-Zielgruppen](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) finden Sie Informationen zur Funktionsweise der Anreicherungsattribut-Auswahl. |
| `{{destination.name}}` | Gibt den Namen Ihres Ziels zurück. |
| `{{destination.sandboxName}}` | Gibt den Namen der Experience Platform-Sandbox zurück, in der Ihr Ziel konfiguriert ist. |
| `{{destination.id}}` | Gibt die ID Ihrer Zielkonfiguration zurück. |
| `{{destination.imsOrgId}}` | Gibt die IMS-Organisations-ID zurück, in der Ihr Ziel konfiguriert ist. |
| `{{destination.enrichmentAttributes}}` | Ermöglicht den Zugriff auf alle Anreicherungsattribute für alle Zielgruppen, die einem Ziel zugeordnet sind. Dieses Makro wird von den Ereignissen `createDestination`, `updateDestination` und `deleteDestination` unterstützt. Anreicherungsattribute sind nur für [benutzerdefinierte Upload-Zielgruppen](destination-configuration/schema-configuration.md#external-audiences) verfügbar. Im [Handbuch zur Aktivierung von Batch-Zielgruppen](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) finden Sie Informationen zur Funktionsweise der Anreicherungsattribut-Auswahl. |
| `{{destination.enrichmentAttributes.<namespace>.<segmentId>}}` | Ermöglicht den Zugriff auf Anreicherungsattribute für bestimmte externe, einem Ziel zugeordnete Zielgruppen. Anreicherungsattribute sind nur für [benutzerdefinierte Upload-Zielgruppen](destination-configuration/schema-configuration.md#external-audiences) verfügbar. Im [Handbuch zur Aktivierung von Batch-Zielgruppen](../../ui/activate-batch-profile-destinations.md#select-enrichment-attributes) finden Sie Informationen zur Funktionsweise der Anreicherungsattribut-Auswahl. |

{style="table-layout:auto"}
