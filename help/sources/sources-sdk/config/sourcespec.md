---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Connectoren; Quell-Connectoren; Quellen-SDK; SDK
title: Authentifizierungsspezifikationen für Quellen-SDK konfigurieren
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung des Sources-SDK vorbereiten müssen.
hide: true
hidefromtoc: true
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 4c4c89ab7db7d3546163d707ac80210561c2fa02
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---

# Quellspezifikation für das Quellen-SDK konfigurieren

Quellspezifikationen enthalten quellenspezifische Informationen, einschließlich Attributen, die sich auf die Kategorie einer Quelle, den Beta-Status und das Katalogsymbol beziehen. Sie enthalten auch nützliche Informationen wie URL-Parameter, Inhalt, Kopfzeile und Zeitplan. Quellspezifikationen beschreiben auch das Schema der Parameter, die zum Erstellen einer Quellverbindung aus einer Basisverbindung erforderlich sind. Das Schema ist erforderlich, um eine Quellverbindung zu erstellen.

Siehe [Anhang](#source-spec) ein Beispiel für eine vollständig ausgefüllte Quellspezifikation.


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
| `sourceSpec.attributes` | Enthält Informationen zur Quelle, die für die Benutzeroberfläche oder API spezifisch ist. |
| `sourceSpec.attributes.uiAttributes` | Zeigt Informationen über die für die Benutzeroberfläche spezifische Quelle an. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Ein boolesches Attribut, das anzeigt, ob die Quelle mehr Feedback von Kunden benötigt, um sie zu ihrer Funktion hinzuzufügen. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definiert die Kategorie der Quelle. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definiert das Symbol, das für das Rendering der Quelle in der Platform-Benutzeroberfläche verwendet wird. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Zeigt eine kurze Beschreibung der Quelle an. |
| `sourceSpec.attributes.uiAttributes.label` | Zeigt den Titel an, der für das Rendering der Quelle in der Platform-Benutzeroberfläche verwendet werden soll. |
| `sourceSpec.attributes.spec.properties.urlParams` | Enthält Informationen zum URL-Ressourcenpfad, zur Methode und zu den unterstützten Abfrageparametern. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Definiert den Ressourcenpfad, aus dem die Daten abgerufen werden sollen. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Definiert die HTTP-Methode, die verwendet werden soll, um die Anfrage an die Ressource zum Abrufen von Daten zu senden. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Definiert die unterstützten Abfrageparameter, mit denen die Quell-URL angehängt werden kann, wenn eine Anforderung zum Abrufen von Daten gesendet wird. **Hinweis**: Jeder vom Benutzer bereitgestellte Parameterwert muss als Platzhalter formatiert sein. Beispiel: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` wird wie folgt an die Quell-URL angehängt: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Definiert Kopfzeilen, die in der HTTP-Anfrage an die Quell-URL beim Abrufen von Daten bereitgestellt werden müssen. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.contentPath` | Definiert den Knoten, der die Liste der Elemente enthält, die in Platform aufgenommen werden müssen. Dieses Attribut sollte der gültigen JSON-Pfadsyntax entsprechen und auf ein bestimmtes Array verweisen. | Siehe [Anhang](#content-path) ein Beispiel für die Ressource, die in einem Inhaltspfad enthalten ist. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Der Pfad, der auf die Sammlungsdatensätze verweist, die in Platform erfasst werden sollen. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Mit dieser Eigenschaft können Sie bestimmte Elemente aus der im Inhaltspfad identifizierten Ressource identifizieren, die von der Erfassung ausgeschlossen werden sollen. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Mit dieser Eigenschaft können Sie explizit die einzelnen Attribute angeben, die Sie beibehalten möchten. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Mit dieser Eigenschaft können Sie den Wert des Attributnamens überschreiben, den Sie in `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Mit dieser Eigenschaft können Sie zwei Arrays reduzieren und Ressourcendaten in die Platform-Ressource umwandeln. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Der Pfad, der auf die Sammlungsdatensätze verweist, die Sie reduzieren möchten. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Mit dieser Eigenschaft können Sie bestimmte Elemente aus der im Entitätspfad identifizierten Ressource identifizieren, die von der Erfassung ausgeschlossen werden sollen. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Mit dieser Eigenschaft können Sie explizit die einzelnen Attribute angeben, die Sie beibehalten möchten. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Mit dieser Eigenschaft können Sie den Wert des Attributnamens überschreiben, den Sie in `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Definiert die Parameter oder Felder, die bereitgestellt werden müssen, um von der aktuellen Seitenantwort des Benutzers oder beim Erstellen einer nächsten Seiten-URL einen Link zur nächsten Seite zu erhalten. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Zeigt den Typ des unterstützten Paginierungstyps für Ihre Quelle an. | <ul><li>`offset`: Mit diesem Paginierungstyp können Sie die Ergebnisse analysieren, indem Sie einen Index angeben, von dem aus das resultierende Array gestartet werden soll, und eine Begrenzung dafür, wie viele Ergebnisse zurückgegeben werden.</li><li>`pointer`: Mit diesem Seitentyp können Sie eine `pointer` auf ein bestimmtes Element verweisen, das mit einer Anfrage gesendet werden muss. Die Seitennummerierung des Zeigertyps erfordert den Pfad in der Payload, der auf die nächste Seite verweist.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Der Name des Limits, mit dem die API die Anzahl der Datensätze angeben kann, die auf einer Seite abgerufen werden sollen. | `limit` oder `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Die Anzahl der Datensätze, die auf einer Seite abgerufen werden sollen. | `limit=10` oder `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Der Name des Offset-Attributs. Dies ist erforderlich, wenn der Paginierungstyp auf `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Der Zeiger-Attributname. Dies erfordert den JSON-Pfad zum -Attribut, das auf die nächste Seite verweist. Dies ist erforderlich, wenn der Paginierungstyp auf `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Enthält Parameter, die unterstützte Planungsformate für Ihre Quelle definieren. Zeitplanparameter beinhalten `startTime` und `endTime`, mit denen Sie bestimmte Zeitintervalle für Batch-Ausführungen festlegen können. Dadurch wird sichergestellt, dass in einer vorherigen Batch-Ausführung abgerufene Datensätze nicht erneut abgerufen werden. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Definiert den Parameternamen für die Startzeit | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Definiert den Namen des Endzeit-Parameters | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Definiert das unterstützte Format für `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Definiert das unterstützte Format für `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Definiert die vom Benutzer bereitgestellten Parameter zum Abrufen von Ressourcenwerten. | Siehe [Anhang](#user-input) für ein Beispiel für vom Benutzer eingegebene Parameter für `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Anhang {#appendix}

### Beispiel für Inhaltspfad {#content-path}

Im Folgenden finden Sie ein Beispiel für den Inhalt der `contentPath` -Eigenschaft in einer [!DNL MailChimp Campaigns] Verbindungsspezifikation.

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

### `spec.properties` Beispiel für Benutzereingabe {#user-input}

Im Folgenden finden Sie ein Beispiel für einen vom Benutzer bereitgestellten `spec.properties` mit [!DNL MailChimp Members] Verbindungsspezifikation.

In diesem Beispiel `listId` wird als Teil von `urlParams.path`. Wenn Sie `listId` von einem Kunden aus erstellen, müssen Sie ihn auch als Teil von `spec.properties`.


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

## Nächste Schritte

Nachdem Sie die Quellspezifikationen ausgefüllt haben, können Sie mit der Konfiguration der Analysespezifikationen für die Quelle fortfahren, die Sie in Platform integrieren möchten. Siehe das Dokument unter [Konfigurieren von Erkunden-Spezifikationen](./explorespec.md) für weitere Informationen.
