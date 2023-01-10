---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Quellspezifikationen für Self-Serve-Quellen konfigurieren (Batch-SDK)
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung von Self-Serve-Quellen (Batch SDK) vorbereiten müssen.
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 50%

---

# Quellspezifikation für Self-Serve-Quellen konfigurieren (Batch-SDK)

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
| `sourceSpec.attributes` | Enthält Informationen zu der Quelle, die für die UI oder API spezifisch ist. |
| `sourceSpec.attributes.uiAttributes` | Zeigt Informationen zu der UI-spezifischen Quelle an. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Ein boolesches Attribut, das anzeigt, ob die Quelle mehr Kunden-Feedback benötigt, das ihre Funktionalität erweitert. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definiert die Kategorie der Quelle. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definiert das Symbol, das für das Rendering der Quelle in der Platform-Benutzeroberfläche verwendet wird. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Zeigt eine kurze Beschreibung der Quelle an. |
| `sourceSpec.attributes.uiAttributes.label` | Zeigt den Titel an, der für das Rendering der Quelle in der Platform-Benutzeroberfläche verwendet werden soll. |
| `sourceSpec.attributes.spec.properties.urlParams` | Enthält Informationen zum URL-Ressourcenpfad, zur Methode und zu den unterstützten Abfrageparametern. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Definiert den Ressourcenpfad, aus dem die Daten abgerufen werden sollen. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Definiert die HTTP-Methode, die verwendet werden soll, um die Anfrage zum Abrufen von Daten an die Ressource zu senden. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Definiert die unterstützten Abfrageparameter, mit denen die Quell-URL angehängt werden kann, wenn eine Anfrage zum Abrufen von Daten gesendet wird. **Hinweis**: Jeder vom Benutzer bereitgestellte Parameterwert muss als Platzhalter formatiert sein. Beispiel: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` wird wie folgt an die Quell-URL angehängt: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Definiert Kopfzeilen, die beim Abrufen von Daten in der HTTP-Anfrage an die Quell-URL bereitgestellt werden müssen. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Dieses Attribut kann so konfiguriert werden, dass der HTTP-Textkörper über eine POST-Anfrage gesendet wird. |
| `sourceSpec.attributes.spec.properties.contentPath` | Definiert den Knoten, der die Liste der Elemente enthält, die in Platform aufgenommen werden müssen. Dieses Attribut sollte der gültigen JSON-Pfadsyntax entsprechen und muss auf ein bestimmtes Array verweisen. | Anzeigen der [Abschnitt mit zusätzlichen Ressourcen](#content-path) ein Beispiel für die Ressource, die in einem Inhaltspfad enthalten ist. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Pfad, der auf die Sammlungsdatensätze verweist, die in Platform erfasst werden sollen. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Diese Eigenschaft ermöglicht es, in der im Inhaltspfad identifizierten Ressource bestimmte Elemente zu identifizieren, die von der Erfassung ausgeschlossen werden sollen. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Diese Eigenschaft ermöglicht es, explizit die einzelnen Attribute anzugeben, die Sie beibehalten möchten. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Diese Eigenschaft ermöglicht es, den Wert des Attributnamens, den Sie in `contentPath` angegeben haben, zu überschreiben. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Diese Eigenschaft ermöglicht es, zwei Arrays zu vereinfachen und Ressourcendaten in die Platform-Ressource zu überführen. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Pfad, der auf die Sammlungsdatensätze verweist, die Sie reduzieren möchten. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Diese Eigenschaft ermöglicht es, in der im Entitätspfad identifizierten Ressource bestimmte Elemente zu identifizieren, die von der Erfassung ausgeschlossen werden sollen. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Diese Eigenschaft ermöglicht es, explizit die einzelnen Attribute anzugeben, die Sie beibehalten möchten. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Diese Eigenschaft ermöglicht es, den in `explodeEntityPath` angegebenen Wert des Attributnamens zu überschreiben. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Definiert die Parameter oder Felder, die bereitgestellt werden müssen, um aus der Antwort der aktuellen Seite des Benutzers oder beim Erstellen der URL für eine nächste Seite einen Link zur nächsten Seite zu erhalten. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Zeigt den Typ des unterstützten Paginierungstyps für Ihre Quelle an. | <ul><li>`OFFSET`: Dieser Paginierungstyp ermöglicht es, die Ergebnisse zu analysieren, indem Sie einen Index, von dem aus das resultierende Array gestartet werden soll, und eine Begrenzung dafür angeben, wie viele Ergebnisse zurückgegeben werden.</li><li>`POINTER`: Dieser Paginierungstyp ermöglicht es, mit einer `pointer`-Variablen auf ein bestimmtes Element zu verweisen, das mit einer Anfrage gesendet werden muss. Die Paginierung des Zeigertyps erfordert einen Pfad in der Payload, der auf die nächste Seite verweist..</li><li>`CONTINUATION_TOKEN`: Mit diesem Paginierungstyp können Sie Ihre Abfrage- oder Kopfzeilenparameter mit einem Fortsetzung-Token anhängen, um die verbleibenden Rückgabedaten aus Ihrer Quelle abzurufen, die aufgrund eines vorab festgelegten Maximalwerts nicht zurückgegeben wurden.</li><li>`PAGE`: Mit diesem Paginierungstyp können Sie Ihren Abfrageparameter mit einem Paging-Parameter anhängen, um durch die Rückgabedaten nach Seiten zu navigieren, beginnend bei Seite Null.</li><li>`NONE`: Dieser Seitentyp kann für Quellen verwendet werden, die keinen der verfügbaren Paginierungstypen unterstützen. Paginierungstyp `NONE` gibt die gesamten Antwortdaten nach einer Anfrage zurück.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Name des Limits, mit dem die API die Anzahl der Datensätze angeben kann, die auf einer Seite abgerufen werden sollen. | `limit` oder `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Anzahl der Datensätze, die auf einer Seite abgerufen werden sollen. | `limit=10` oder `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Name des Offset-Attributs. Ist erforderlich, wenn der Paginierungstyp auf `offset` festgesetzt ist. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Der Zeiger-Attributname. Dies erfordert den JSON-Pfad zum Feldnamen, der auf die nächste Seite verweist. Dies ist erforderlich, wenn der Paginierungstyp auf `pointer` eingestellt ist. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Enthält Parameter, die unterstützte Planungsformate für Ihre Quelle definieren. Zeitplanparameter beinhalten `startTime` und `endTime`, mit denen Sie bestimmte Zeitintervalle für Batch-Ausführungen festlegen können. Dadurch wird sichergestellt, dass in einer vorherigen Batch-Ausführung abgerufene Datensätze nicht erneut abgerufen werden. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definiert den Namen des Startzeit-Parameters | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definiert den Namen des Endzeit-Parameters | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definiert das unterstützte Format für `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definiert das unterstützte Format für `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Definiert die vom Benutzer bereitgestellten Parameter zum Abrufen von Ressourcenwerten. | Siehe [Zusätzliche Ressourcen](#user-input) für ein Beispiel für vom Benutzer eingegebene Parameter für `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Weitere Ressourcen {#appendix}

Die folgenden Abschnitte enthalten Informationen zu zusätzlichen Konfigurationen, die Sie für Ihre `sourceSpec`, einschließlich erweiterter Planung und benutzerdefinierter Schemata.

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

Im Folgenden finden Sie Beispiele für andere Paginierungstypen, die von Self-Serve-Quellen (Batch SDK) unterstützt werden:

#### `CONTINUATION_TOKEN`

Ein Fortsetzung-Token-Typ der Paginierung gibt ein Zeichenfolgen-Token zurück, das das Vorhandensein weiterer Elemente angibt, die aufgrund einer vorab festgelegten maximalen Anzahl von Elementen, die in einer einzelnen Antwort zurückgegeben werden können, nicht zurückgegeben werden konnten.

Eine Quelle, die den Weiterleitungstoken-Typ der Paginierung unterstützt, kann einen Paginierungsparameter aufweisen, der Folgendem ähnelt:

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
| `type` | Die Art der Paginierung, die zum Zurückgeben von Daten verwendet wird. |
| `continuationTokenPath` | Der Wert, der an die Abfrageparameter angehängt werden muss, um zur nächsten Seite der zurückgegebenen Ergebnisse zu wechseln. |
| `parameterType` | Die `parameterType` -Eigenschaft definiert, wo die `parameterName` hinzugefügt werden. Die `QUERYPARAM` -Typ ermöglicht es Ihnen, Ihre Abfrage mit der `parameterName`. Die `HEADERPARAM` ermöglicht es Ihnen, Ihre `parameterName` zu Ihrer Kopfzeilenanforderung hinzufügen. |
| `parameterName` | Der Name des Parameters, der zum Integrieren des Fortsetzung-Tokens verwendet wird. Das Format lautet wie folgt: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | Die `delayRequestMillis` -Eigenschaft in Paginierung ermöglicht es Ihnen, die Rate der Anforderungen an Ihre Quelle zu steuern. Einige Quellen können die Anzahl der Anfragen begrenzen, die Sie pro Minute stellen können. Beispiel: [!DNL Zendesk] ist auf 100 Anfragen pro Minute beschränkt und definiert  `delayRequestMillis` nach `850` ermöglicht es Ihnen, die Quelle so zu konfigurieren, dass sie Anrufe mit nur etwa 80 Anfragen pro Minute sendet, deutlich unter dem Schwellenwert von 100 Anfragen pro Minute. |

Im Folgenden finden Sie ein Beispiel für eine Antwort, die mit dem Paginierungstyp Fortsetzung-Token zurückgegeben wird:

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

#### `PAGE`

Die `PAGE` Mit dem Seitentyp können Sie durch die Rückkehrdaten nach der Anzahl der Seiten, die bei null beginnen, navigieren. Bei Verwendung von `PAGE` Paginierung eingeben, müssen Sie die Anzahl der Datensätze angeben, die auf einer einzelnen Seite angegeben werden.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `type` | Die Art der Paginierung, die zum Zurückgeben von Daten verwendet wird. |
| `limitName` | Name des Limits, mit dem die API die Anzahl der Datensätze angeben kann, die auf einer Seite abgerufen werden sollen. |
| `limitValue` | Anzahl der Datensätze, die auf einer Seite abgerufen werden sollen. |
| `pageParamName` | Der Name des Parameters, der an Abfrageparameter angehängt werden muss, um durch verschiedene Seiten der Rückgabedaten zu navigieren. Beispiel: `https://abc.com?pageIndex=1` gibt die zweite Seite der Rückgabe-Payload einer API zurück. |
| `maximumRequest` | Die maximale Anzahl von Anforderungen, die eine Quelle für eine bestimmte inkrementelle Ausführung stellen kann. Der aktuelle Standardwert ist 10000. |

#### `NONE`

Die `NONE` Der Paginierungstyp kann für Quellen verwendet werden, die keinen der verfügbaren Paginierungstypen unterstützen. Quellen, die die Paginierung verwenden `NONE` geben Sie einfach alle abrufbaren Datensätze zurück, wenn eine GET angefordert wird.

```json
"paginationParams": {
  "type": "NONE"
}
```

### Erweiterte Planung für Self-Serve-Quellen (Batch-SDK)

Konfigurieren Sie den inkrementellen und Aufstockungsplan Ihrer Quelle mithilfe der erweiterten Planung. Die `incremental` -Eigenschaft können Sie einen Zeitplan konfigurieren, in dem Ihre Quelle nur neue oder geänderte Datensätze erfasst, während die `backfill` -Eigenschaft können Sie einen Zeitplan für die Erfassung historischer Daten erstellen.

Mit der erweiterten Planung können Sie Quellausdrücke und -funktionen verwenden, um inkrementelle Zeitpläne und Aufstockungszeitpläne zu konfigurieren. Im folgenden Beispiel wird die Variable [!DNL Zendesk] -Quelle erfordert, dass der inkrementelle Zeitplan als `type:user updated > {START_TIME} updated < {END_TIME}` und Aufstockung als `type:user updated < {END_TIME}`.

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
| `scheduleParams.type` | Die Art der Planung Ihrer Quelle wird verwendet. Setzen Sie diesen Wert auf `ADVANCE` , um den erweiterten Planungstyp zu verwenden. |
| `scheduleParams.paramFormat` | Das definierte Format Ihres Planungsparameters. Dieser Wert kann mit dem Wert Ihrer Quelle übereinstimmen. `scheduleStartParamFormat` und `scheduleEndParamFormat` -Werte. |
| `scheduleParams.incremental` | Die inkrementelle Abfrage Ihrer Quelle. Inkrementell bezieht sich auf eine Erfassungsmethode, bei der nur neue oder geänderte Daten erfasst werden. |
| `scheduleParams.backfill` | Die Aufstockungsabfrage Ihrer Quelle. Aufstockung bezieht sich auf eine Erfassungsmethode, bei der historische Daten erfasst werden. |

Nachdem Sie die erweiterte Planung konfiguriert haben, müssen Sie die `scheduleParams` im Abschnitt URL-, Text- oder Kopfzeilenparameter , je nachdem, was Ihre jeweilige Quelle unterstützt. Im folgenden Beispiel: `{SCHEDULE_QUERY}` ist ein Platzhalter, mit dem festgelegt wird, wo die inkrementellen Ausdrücke für die Aufstockung und die Aufstockung verwendet werden. Im Falle einer [!DNL Zendesk] Quelle, `query` wird in der Variablen `queryParams` um die erweiterte Planung festzulegen.

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

### Fügen Sie ein benutzerdefiniertes Schema hinzu, um die dynamischen Attribute Ihrer Quelle zu definieren

Sie können ein benutzerdefiniertes Schema zu Ihrem `sourceSpec` , um alle für Ihre Quelle erforderlichen Attribute zu definieren, einschließlich etwaiger dynamischer Attribute, die Sie benötigen. Sie können die entsprechende Verbindungsspezifikation Ihrer Quelle aktualisieren, indem Sie eine PUT-Anfrage an die `/connectionSpecs` Endpunkt der [!DNL Flow Service] API bei der Bereitstellung Ihres benutzerdefinierten Schemas im `sourceSpec` Abschnitt Ihrer Verbindungsspezifikation.

Im Folgenden finden Sie ein Beispiel für ein benutzerdefiniertes Schema, das Sie zur Verbindungsspezifikation Ihrer Quelle hinzufügen können:

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

Wenn Ihre Quellspezifikationen ausgefüllt sind, können Sie mit der Konfiguration der Erkundungsspezifikationen für die Quelle fortfahren, die Sie in Platform integrieren möchten. Weitere Informationen finden Sie im Dokument zum [Konfigurieren von Erkungungsspezifikationen](./explorespec.md).
