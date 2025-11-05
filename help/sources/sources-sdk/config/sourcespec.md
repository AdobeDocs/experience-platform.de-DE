---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Konfigurieren von Quellspezifikationen für Selbstbedienungsquellen (Batch-SDK)
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Selbstbedienungsquellen (Batch-SDK) vorbereiten müssen.
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 2ff70ee6e4aa7fd723293e66000ccb161d61ab6a
workflow-type: tm+mt
source-wordcount: '2107'
ht-degree: 38%

---

# Konfigurieren der Quellspezifikation für Selbstbedienungsquellen (Batch-SDK)

Quellenspezifikationen enthalten quellenspezifische Informationen, darunter Attribute, die sich auf die Kategorie einer Quelle, den Beta-Status und das Katalogsymbol beziehen. Sie enthalten auch hilfreiche Informationen wie URL-Parameter, Inhalte, Kopfzeile und Zeitplan. Quellenspezifikationen beschreiben außerdem das Schema der Parameter, die zum Erstellen einer Quellverbindung aus einer Basisverbindung erforderlich sind. Das Schema ist erforderlich, um eine Quellverbindung zu erstellen.

Ein Beispiel für eine vollständig angegebene Quellspezifikation finden Sie im [Anhang](#source-spec).


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
              "type": "string",
              "description": "Enter resource url host path.",
              "example": "https://{domain}.api.mailchimp.com"
            },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "host",
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| Eigenschaft | Beschreibung | Beispiel |
| --- | --- | --- |
| `sourceSpec.attributes` | Enthält Informationen zu der Quelle, die für die UI oder API spezifisch ist. |  |
| `sourceSpec.attributes.uiAttributes` | Zeigt Informationen zu der UI-spezifischen Quelle an. |  |
| `sourceSpec.attributes.uiAttributes.isPreview` | Ein boolesches Attribut, das angibt, ob die Quelle als Vorschau angezeigt wird (nicht für Produktion/allgemeine Verfügbarkeit). | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.isBeta` | Ein boolesches Attribut, das anzeigt, ob die Quelle mehr Kunden-Feedback benötigt, das ihre Funktionalität erweitert. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definiert die Kategorie der Quelle. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definiert das Symbol, das zum Rendern der Quelle in der Experience Platform-Benutzeroberfläche verwendet wird. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Zeigt eine kurze Beschreibung der Quelle an. |  |
| `sourceSpec.attributes.uiAttributes.label` | Zeigt den Titel an, der für das Rendering der Quelle in der Experience Platform-Benutzeroberfläche verwendet werden soll. |  |
| `sourceSpec.attributes.spec.properties.urlParams` | Enthält Informationen zum URL-Ressourcenpfad, zur Methode und zu den unterstützten Abfrageparametern. |  |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Definiert den Ressourcenpfad, aus dem die Daten abgerufen werden sollen. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Definiert die HTTP-Methode, die verwendet werden soll, um die Anfrage zum Abrufen von Daten an die Ressource zu senden. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Definiert die unterstützten Abfrageparameter, mit denen die Quell-URL angehängt werden kann, wenn eine Anfrage zum Abrufen von Daten gesendet wird. **Hinweis**: Jeder vom Benutzer bereitgestellte Parameterwert muss als Platzhalter formatiert sein. Beispiel: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` wird wie folgt an die Quell-URL angehängt: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Definiert Kopfzeilen, die beim Abrufen von Daten in der HTTP-Anfrage an die Quell-URL bereitgestellt werden müssen. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Dieses Attribut kann so konfiguriert werden, dass der HTTP-Text über eine POST-Anfrage gesendet wird. |  |
| `sourceSpec.attributes.spec.properties.contentPath` | Definiert den Knoten, der die Liste der Elemente enthält, die in Experience Platform aufgenommen werden müssen. Dieses Attribut sollte der gültigen JSON-Pfadsyntax entsprechen und muss auf ein bestimmtes Array verweisen. | Im Abschnitt [Zusätzliche Ressourcen](#content-path) finden Sie ein Beispiel für die in einem Inhaltspfad enthaltene Ressource. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Der Pfad, der auf die in Experience Platform aufzunehmenden Sammlungsdatensätze verweist. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Diese Eigenschaft ermöglicht es, in der im Inhaltspfad identifizierten Ressource bestimmte Elemente zu identifizieren, die von der Erfassung ausgeschlossen werden sollen. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Diese Eigenschaft ermöglicht es, explizit die einzelnen Attribute anzugeben, die Sie beibehalten möchten. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Diese Eigenschaft ermöglicht es, den Wert des Attributnamens, den Sie in `contentPath` angegeben haben, zu überschreiben. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Mit dieser Eigenschaft können Sie zwei Arrays reduzieren und Ressourcendaten in Experience Platform-Ressourcen umwandeln. |  |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Pfad, der auf die Sammlungseinträge verweist, die Sie reduzieren möchten. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Diese Eigenschaft ermöglicht es, in der im Entitätspfad identifizierten Ressource bestimmte Elemente zu identifizieren, die von der Erfassung ausgeschlossen werden sollen. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Diese Eigenschaft ermöglicht es, explizit die einzelnen Attribute anzugeben, die Sie beibehalten möchten. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Diese Eigenschaft ermöglicht es, den in `explodeEntityPath` angegebenen Wert des Attributnamens zu überschreiben. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Definiert die Parameter oder Felder, die bereitgestellt werden müssen, um aus der Antwort der aktuellen Seite des Benutzers oder beim Erstellen der URL für eine nächste Seite einen Link zur nächsten Seite zu erhalten. |  |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Zeigt den Typ des unterstützten Paginierungstyps für Ihre Quelle an. | <ul><li>`OFFSET`: Dieser Paginierungstyp ermöglicht es, die Ergebnisse zu analysieren, indem Sie einen Index, von dem aus das resultierende Array gestartet werden soll, und eine Begrenzung dafür angeben, wie viele Ergebnisse zurückgegeben werden.</li><li>`POINTER`: Dieser Paginierungstyp ermöglicht es, mit einer `pointer`-Variablen auf ein bestimmtes Element zu verweisen, das mit einer Anfrage gesendet werden muss. Die Paginierung des Zeigertyps erfordert einen Pfad in der Payload, der auf die nächste Seite verweist.</li><li>`CONTINUATION_TOKEN`: Dieser Paginierungstyp ermöglicht es Ihnen, Ihre Abfrage- oder Kopfzeilenparameter mit einem Fortsetzungs-Token anzuhängen, um verbleibende Rückgabedaten aus Ihrer Quelle abzurufen, die aufgrund eines vorab festgelegten Maximums zunächst nicht zurückgegeben wurden.</li><li>`PAGE`: Dieser Paginierungstyp ermöglicht es, Ihren Abfrageparameter mit einem Paging-Parameter anzuhängen, um die Rückgabedaten nach Seiten zu durchlaufen, beginnend bei Seite null.</li><li>`NONE`: Dieser Paginierungstyp kann für Quellen verwendet werden, die keinen der verfügbaren Paginierungstypen unterstützen. Paginierungstyp `NONE` gibt die gesamten Antwortdaten nach einer Anfrage zurück.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Name des Limits, mit dem die API die Anzahl der Einträge angeben kann, die auf einer Seite abgerufen werden sollen. | `limit` oder `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Anzahl der Einträge, die auf einer Seite abgerufen werden sollen. | `limit=10` oder `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Name des Offset-Attributs. Ist erforderlich, wenn der Paginierungstyp auf `offset` festgesetzt ist. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Der Zeiger-Attributname. Dies erfordert den JSON-Pfad zum Feldnamen, der auf die nächste Seite verweist. Dies ist erforderlich, wenn der Paginierungstyp auf `pointer` eingestellt ist. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Enthält Parameter, die unterstützte Planungsformate für Ihre Quelle definieren. Zeitplanparameter beinhalten `startTime` und `endTime`, mit denen Sie bestimmte Zeitintervalle für Batch-Ausführungen festlegen können. Dadurch wird sichergestellt, dass in einer vorherigen Batch-Ausführung abgerufene Einträge nicht erneut abgerufen werden. |  |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definiert den Namen des Startzeit-Parameters | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definiert den Namen des Endzeit-Parameters | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definiert das unterstützte Format für `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definiert das unterstützte Format für `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Definiert die vom Benutzer bereitgestellten Parameter zum Abrufen von Ressourcenwerten. | Unter [Zusätzliche Ressourcen](#user-input) finden Sie ein Beispiel für vom Benutzer eingegebene Parameter für `spec.properties`. |

{style="table-layout:auto"}

## Weitere Ressourcen {#appendix}

In den folgenden Abschnitten finden Sie Informationen zu zusätzlichen Konfigurationen, die Sie an Ihren `sourceSpec` vornehmen können, einschließlich erweiterter Zeitpläne und benutzerdefinierter Schemata.

### Beispiel für Inhaltspfad {#content-path}

Das Folgende ist ein Beispiel für den Inhalt der `contentPath`-Eigenschaft in einer [!DNL MailChimp Members]-Verbindungsspezifikation.

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties`-Beispiel für Benutzereingabe {#user-input}

Das Folgende ist ein Beispiel für ein vom Benutzer bereitgestelltes `spec.properties` unter Verwendung einer [!DNL MailChimp Members]-Verbindungsspezifikation.

In diesem Beispiel wird `listId` als Teil von `urlParams.path` bereitgestellt. Wenn Sie `listId` von einem Kunden abrufen müssen, müssen Sie es auch als Teil von `spec.properties` definieren.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### Beispiel für Quellspezifikation {#source-spec}

Im Folgenden finden Sie eine abgeschlossene Quellspezifikation mit [!DNL MailChimp Members]:

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "host": "https://{domain}.api.mailchimp.com",
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

### Konfigurieren verschiedener Paginierungstypen für Ihre Quelle {#pagination}

Im Folgenden finden Sie Beispiele für andere Paginierungstypen, die von Selbstbedienungsquellen (Batch-SDK) unterstützt werden:

>[!BEGINTABS]

>[!TAB Versatz]

Dieser Paginierungstyp ermöglicht es, die Ergebnisse zu analysieren, indem Sie einen Index, von dem aus das resultierende Array gestartet werden soll, und eine Begrenzung dafür angeben, wie viele Ergebnisse zurückgegeben werden. Beispiel:

```json
"paginationParams": {
        "type": "OFFSET",
        "limitName": "limit",
        "limitValue": "4",
        "offSetName": "offset",
        "endConditionName": "$.hasMore",
        "endConditionValue": "Const:false"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `type` | Die Art der Paginierung, die zur Rückgabe von Daten verwendet wird. |
| `limitName` | Name des Limits, mit dem die API die Anzahl der Einträge angeben kann, die auf einer Seite abgerufen werden sollen. |
| `limitValue` | Anzahl der Einträge, die auf einer Seite abgerufen werden sollen. |
| `offSetName` | Name des Offset-Attributs. Ist erforderlich, wenn der Paginierungstyp auf `offset` festgesetzt ist. |
| `endConditionName` | Ein benutzerdefinierter Wert, der die Bedingung angibt, die die Paginierungsschleife in der nächsten HTTP-Anfrage beendet. Sie müssen den Attributnamen angeben, auf den Sie die Endbedingung setzen möchten. |
| `endConditionValue` | Der Attributwert, auf den die Bedingung gesetzt werden soll. |

>[!TAB Zeiger]

Mit diesem Paginierungstyp können Sie eine `pointer`-Variable verwenden, um auf ein bestimmtes Element zu verweisen, das mit einer Anfrage gesendet werden muss. Die Paginierung des Zeigertyps erfordert einen Pfad in der Payload, der auf die nächste Seite verweist. Beispiel:

```json
{
 "type": "POINTER",
 "limitName": "limit",
 "limitValue": 1,
 "pointerPath": "paging.next"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `type` | Die Art der Paginierung, die zur Rückgabe von Daten verwendet wird. |
| `limitName` | Name des Limits, mit dem die API die Anzahl der Einträge angeben kann, die auf einer Seite abgerufen werden sollen. |
| `limitValue` | Anzahl der Einträge, die auf einer Seite abgerufen werden sollen. |
| `pointerPath` | Der Zeiger-Attributname. Dies erfordert den JSON-Pfad zum Attribut , das auf die nächste Seite verweist. |

>[!TAB Fortsetzungs-Token]

Ein Fortsetzungs-Token-Typ der Paginierung gibt ein Zeichenfolgen-Token zurück, das angibt, dass es mehr Elemente gibt, die aufgrund einer vordefinierten maximalen Anzahl von Elementen, die in einer einzelnen Antwort zurückgegeben werden können, nicht zurückgegeben werden konnten.

Eine Quelle, die die Paginierung vom Typ Fortsetzungs-Token unterstützt, kann einen Paginierungsparameter ähnlich dem folgenden aufweisen:

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `type` | Die Art der Paginierung, die zur Rückgabe von Daten verwendet wird. |
| `continuationTokenPath` | Der Wert, der an die Abfrageparameter angehängt werden muss, um zur nächsten Seite der zurückgegebenen Ergebnisse zu wechseln. |
| `parameterType` | Die `parameterType`-Eigenschaft definiert, wo die `parameterName` hinzugefügt werden muss. Mit dem `QUERYPARAM` können Sie Ihre Abfrage an die `parameterName` anhängen. Mit dem `HEADERPARAM` können Sie Ihre `parameterName` zu Ihrer Header-Anfrage hinzufügen. |
| `parameterName` | Der Name des Parameters, der zum Einbinden des Fortsetzungstokens verwendet wird. Das Format lautet wie folgt: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | Mit der Eigenschaft `delayRequestMillis` in Paginierung können Sie die Rate der an Ihre Quelle gesendeten Anfragen steuern. Bei einigen Quellen kann die Anzahl der Anfragen, die pro Minute gestellt werden können, begrenzt sein. Beispielsweise ist [!DNL Zendesk] auf 100 Anfragen pro Minute beschränkt. Wenn Sie `delayRequestMillis` auf `850` definieren, können Sie die Quelle so konfigurieren, dass Aufrufe mit nur etwa 80 Anfragen pro Minute durchgeführt werden, was deutlich unter dem Schwellenwert von 100 Anfragen pro Minute liegt. |

Im Folgenden finden Sie ein Beispiel für eine Antwort, die mithilfe des Fortsetzungs-Token-Typs der Paginierung zurückgegeben wird:

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

>[!TAB Seite]

Mit dem `PAGE` Paginierungstyp können Sie die Rückgabedaten nach der Anzahl der Seiten durchlaufen, die bei null beginnen. Bei Verwendung `PAGE` Paginierung vom Typ müssen Sie die Anzahl der auf einer einzelnen Seite angegebenen Datensätze angeben.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "pageSize",
  "limitValue": 100,
  "initialPageIndex": 1,
  "endPageIndex": "headers.x-pagecount",
  "pageParamName": "pageNumber",
  "maximumRequest": 10000
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `type` | Die Art der Paginierung, die zur Rückgabe von Daten verwendet wird. |
| `limitName` | Name des Limits, mit dem die API die Anzahl der Einträge angeben kann, die auf einer Seite abgerufen werden sollen. |
| `limitValue` | Anzahl der Einträge, die auf einer Seite abgerufen werden sollen. |
| `initialPageIndex` | (Optional) Der anfängliche Seitenindex definiert die Seitenzahl, mit der die Paginierung beginnt. Dieses Feld kann für Quellen verwendet werden, bei denen die Paginierung nicht bei 0 beginnt. Wenn kein Wert angegeben wird, wird für den anfänglichen Seitenindex standardmäßig „0“ festgelegt. Dieses Feld erwartet eine Ganzzahl. |
| `endPageIndex` | (Optional) Mit dem Endseitenindex können Sie eine Endbedingung festlegen und die Paginierung stoppen. Dieses Feld kann verwendet werden, wenn keine standardmäßigen Endbedingungen zum Anhalten der Paginierung verfügbar sind. Dieses Feld kann auch verwendet werden, wenn die Anzahl der aufzunehmenden Seiten oder die letzte Seitenzahl über den Antwort-Header angegeben wird, was bei der Verwendung der Paginierung vom Typ `PAGE` üblich ist. Der Wert für den Index der Endseite kann entweder die letzte Seitenzahl oder ein Ausdruckswert vom Typ Zeichenfolge aus der Antwortkopfzeile sein. Beispielsweise können Sie `headers.x-pagecount` verwenden, um den Endseitenindex dem `x-pagecount` Wert in den Antwortkopfzeilen zuzuweisen. **Hinweis**: `x-pagecount` ist für einige Quellen ein obligatorischer Antwort-Header und enthält den Wert und die Anzahl der aufzunehmenden Seiten. |
| `pageParamName` | Der Name des Parameters, den Sie an Abfrageparameter anhängen müssen, um verschiedene Seiten der zurückgegebenen Daten zu durchlaufen. Beispielsweise würde `https://abc.com?pageIndex=1` die zweite Seite der zurückgegebenen Payload einer API zurückgeben. |
| `maximumRequest` | Die maximale Anzahl von Anfragen, die eine Quelle für eine bestimmte inkrementelle Ausführung ausführen kann. Die aktuelle Standardbegrenzung ist 10000. |

{style="table-layout:auto"}


>[!TAB Kein]

Der `NONE` Paginierungstyp kann für Quellen verwendet werden, die keinen der verfügbaren Paginierungstypen unterstützen. Quellen, die den Paginierungstyp von `NONE` verwenden, geben einfach alle abrufbaren Datensätze zurück, wenn eine GET-Anfrage erfolgt.

```json
"paginationParams": {
  "type": "NONE"
}
```

>[!ENDTABS]

### Erweiterte Planung für Selbstbedienungsquellen (Batch-SDK)

Konfigurieren Sie den inkrementellen und Aufstockungs-Zeitplan Ihrer Quelle mithilfe der erweiterten Planung. Mit der Eigenschaft `incremental` können Sie einen Zeitplan konfigurieren, in dem Ihre Quelle nur neue oder geänderte Datensätze aufnimmt, während Sie mit der Eigenschaft `backfill` einen Zeitplan erstellen können, um historische Daten aufzunehmen.

Mit der erweiterten Planung können Sie für Ihre Quelle spezifische Ausdrücke und Funktionen verwenden, um inkrementelle und Aufstockungspläne zu konfigurieren. Im folgenden Beispiel erfordert die [!DNL Zendesk], dass der inkrementelle Zeitplan als `type:user updated > {START_TIME} updated < {END_TIME}` formatiert ist und `type:user updated < {END_TIME}` aufgestockt wird.

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `scheduleParams.type` | Die Art der Planung, die Ihre Quelle verwenden wird. Legen Sie diesen Wert auf `ADVANCE` fest, um den erweiterten Planungstyp zu verwenden. |
| `scheduleParams.paramFormat` | Das definierte Format Ihres Zeitplanparameters. Dieser Wert kann mit den `scheduleStartParamFormat`- und `scheduleEndParamFormat` Ihrer Quelle identisch sein. |
| `scheduleParams.incremental` | Die inkrementelle Abfrage Ihrer Quelle. Inkrementell bezieht sich auf eine Aufnahmemethode, bei der nur neue oder geänderte Daten aufgenommen werden. |
| `scheduleParams.backfill` | Die Aufstockungsabfrage Ihrer Quelle. Aufstockung bezieht sich auf eine Aufnahmemethode, bei der historische Daten aufgenommen werden. |

Nachdem Sie Ihre erweiterte Planung konfiguriert haben, müssen Sie sich dann im Abschnitt URL-, Text- oder Kopfzeilenparameter auf Ihre `scheduleParams` beziehen, je nachdem, was Ihre bestimmte Quelle unterstützt. Im folgenden Beispiel ist `{SCHEDULE_QUERY}` ein Platzhalter, mit dem angegeben wird, wo die inkrementellen und Aufstockungs-Planungsausdrücke verwendet werden sollen. Im Fall einer [!DNL Zendesk] wird `query` in der `queryParams` verwendet, um eine erweiterte Planung anzugeben.

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### Hinzufügen eines benutzerdefinierten Schemas zur Definition der dynamischen Attribute Ihrer Quelle

Sie können Ihrer `sourceSpec` ein benutzerdefiniertes Schema hinzufügen, um alle für Ihre Quelle erforderlichen Attribute zu definieren, einschließlich aller benötigten dynamischen Attribute. Sie können die entsprechende Verbindungsspezifikation Ihrer Quelle aktualisieren, indem Sie eine PUT-Anfrage an den `/connectionSpecs`-Endpunkt der [!DNL Flow Service]-API stellen und dabei Ihr benutzerdefiniertes Schema im `sourceSpec` Abschnitt Ihrer Verbindungsspezifikation angeben.

Im Folgenden finden Sie ein Beispiel für ein benutzerdefiniertes Schema, das Sie der Verbindungsspezifikation Ihrer Quelle hinzufügen können:

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## Nächste Schritte

Wenn Ihre Quellspezifikationen ausgefüllt sind, können Sie mit der Konfiguration der Erkundungsspezifikationen für die Quelle fortfahren, die Sie in Experience Platform integrieren möchten. Weitere Informationen finden Sie im Dokument [Konfigurieren von Erkundungsspezifikationen](./explorespec.md) .
