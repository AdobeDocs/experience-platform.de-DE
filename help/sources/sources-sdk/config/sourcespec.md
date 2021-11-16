---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Connectoren; Quell-Connectoren; Quellen-SDK; SDK
title: Authentifizierungsspezifikationen für Quellen-SDK konfigurieren
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Konfigurationen, die Sie für die Verwendung des Sources-SDK vorbereiten müssen.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '876'
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
        "key": "{CATEGORY}"
      },
      "icon": {
        "key": "{ICON}"
      },
      "description": {
        "key": "{DESCRIPTION}"
      },
      "label": {
        "key": "{LABEL}"
      }
    },
    "urlParams": {
      "path": "{RESOURCE_PATH}",
      "method": "{GET_or_POST}",
      "queryParams": "{QUERY_PARAMS}"
    },
    "headerParams": "{HEADER_VALUES}",
    "bodyParams": "{BODY_PARAMS_USED_IF_METHOD_IS_POST}",
    "contentPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "explodeEntityPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "paginationParams": {
      "type": "{OFFSET_OR_POINTER}",
      "limitName": "{NUMBER_OF_RECORDS_ATTRIBUTE_NAME}",
      "limitValue": "{NUMBER_OF_RECORDS_PER_PAGE}",
      "offSetName": "{OFFSET_ATTRIBUTE_NAME_REQUIRED_IN_CASE_OF_OFFSET BASED_PAGINATION}",
      "pointerName": "{POINTER_PATH_REQUIRED_IN__CASE_OF_POINTER BASED_PAGINATION}"
    },
    "scheduleParams": {
      "scheduleStartParamName": "{START_TIME_PARAMETER_NAME}",
      "scheduleEndParamName": "{END_TIME_PARAMETER_NAME}",
      "scheduleStartParamFormat": "{DATE_TIME_FORMAT_FOR_START_TIME}",
      "scheduleEndParamFormat": "{END_TIME_FORMAT_FOR_START_TIME}"
    }
  },
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define user input parameters to fetch resource values.",
    "properties": "{USER_INPUT}"
  }
}
```

| Eigenschaft | Beschreibung | Beispiel |
| --- | --- | --- |
| `sourceSpec.attributes` | Enthält Informationen zur Quelle, die für die Benutzeroberfläche oder API spezifisch ist. |
| `sourceSpec.attributes.uiAttributes` | Zeigt Informationen über die für die Benutzeroberfläche spezifische Quelle an. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Ein boolesches Attribut, das anzeigt, ob die Quelle mehr Feedback von Kunden benötigt, um sie zu ihrer Funktion hinzuzufügen. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Definiert die Kategorie der Quelle. | <ul><li>`advertising`</li><li>`cloud storage`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li><li>`streaming`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Definiert das Symbol, das für das Rendering der Quelle in der Platform-Benutzeroberfläche verwendet wird. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Zeigt eine kurze Beschreibung der Quelle an. |
| `sourceSpec.attributes.uiAttributes.label` | Zeigt den Titel an, der für das Rendering der Quelle in der Platform-Benutzeroberfläche verwendet werden soll. |
| `sourceSpec.attributes.urlParams` | Enthält Informationen zum URL-Ressourcenpfad, zur Methode und zu den unterstützten Abfrageparametern. |
| `sourceSpec.attributes.urlParams.path` | Definiert den Ressourcenpfad, aus dem die Daten abgerufen werden sollen. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.urlParams.method` | Definiert die HTTP-Methode, die verwendet werden soll, um die Anfrage an die Ressource zum Abrufen von Daten zu senden. | `GET`, `POST` |
| `sourceSpec.attributes.urlParams.queryParams` | Definiert die unterstützten Abfrageparameter, mit denen die Quell-URL angehängt werden kann, wenn eine Anforderung zum Abrufen von Daten gesendet wird. Die Abfrageparameter müssen ein Komma (`,`) getrennte Schlüssel-Wert-Paare. **Hinweis**: Jeder vom Benutzer bereitgestellte Parameterwert muss als Platzhalter formatiert sein. Beispiel: `${USER_PARAMETER}`. | `exclude_fields=emails._links,id=${id}` |
| `sourceSpec.attributes.headerParams` | Definiert das Komma (`,`) getrennten Kopfzeilen, die in der HTTP-Anfrage an die Quell-URL beim Abrufen von Daten bereitgestellt werden müssen. | `Content-Type=application/json,foo=bar&userHeader={{USER_HEADER_VALUE}}` |
| `sourceSpec.attributes.bodyParams` | Definiert die erforderlichen Textparameter. Diese Eigenschaft wird nur verwendet, wenn `urlParams.method` auf `POST`. |
| `sourceSpec.attributes.contentPath` | Definiert den Knoten, der die Liste der Elemente enthält, die in Platform aufgenommen werden müssen. Dieses Attribut sollte der gültigen JSON-Pfadsyntax entsprechen und auf ein bestimmtes Array verweisen. | Siehe [Anhang](#content-path) ein Beispiel für die Ressource, die in einem Inhaltspfad enthalten ist. |
| `sourceSpec.attributes.contentPath.path` | Der Pfad, der auf die Sammlungsdatensätze verweist, die in Platform erfasst werden sollen. | `$.emails` |
| `sourceSpec.attributes.contentPath.skipAttributes` | Mit dieser Eigenschaft können Sie bestimmte Elemente aus der im Inhaltspfad identifizierten Ressource identifizieren, die von der Erfassung ausgeschlossen werden sollen. |
| `sourceSpec.attributes.contentPath.overrideWrapperAttribute` | Mit dieser Eigenschaft können Sie den Wert des Attributnamens überschreiben, den Sie in `contentPath`. |
| `sourceSpec.attributes.contentPath.keepAttributes` | Mit dieser Eigenschaft können Sie explizit die einzelnen Attribute angeben, die Sie zuordnen möchten. |
| `sourceSpec.attributes.explodeEntityPath` | Mit dieser Eigenschaft können Sie zwei Arrays reduzieren und Ressourcendaten in die Platform-Ressource umwandeln. |
| `sourceSpec.attributes.explodeEntityPath.path` | Der Pfad, der auf die Sammlungsdatensätze verweist, die Sie reduzieren möchten. | `$.email.activity` |
| `sourceSpec.attributes.explodeEntityPath.skipAttributes` | Mit dieser Eigenschaft können Sie bestimmte Elemente aus der im Entitätspfad identifizierten Ressource identifizieren, die von der Erfassung ausgeschlossen werden sollen. |
| `sourceSpec.attributes.explodeEntityPath.overrideWrapperAttribute` | Mit dieser Eigenschaft können Sie den Wert des Attributnamens überschreiben, den Sie in `explodeEntityPath`. |
| `sourceSpec.attributes.explodeEntityPath.keepAttributes` | Mit dieser Eigenschaft können Sie explizit die einzelnen Attribute angeben, die Sie zuordnen möchten. |
| `sourceSpec.attributes.paginationParams` | Definiert die Parameter oder Felder, die bereitgestellt werden müssen, um von der aktuellen Seitenantwort des Benutzers oder beim Erstellen einer nächsten Seiten-URL einen Link zur nächsten Seite zu erhalten. |
| `sourceSpec.attributes.paginationParams.type` | Zeigt den Typ des unterstützten Paginierungstyps für Ihre Quelle an. | <ul><li>`offset`: Mit diesem Paginierungstyp können Sie die Ergebnisse analysieren, indem Sie einen Index angeben, von dem aus das resultierende Array gestartet werden soll, und eine Begrenzung dafür, wie viele Ergebnisse zurückgegeben werden.</li><li>`pointer`: Mit diesem Seitentyp können Sie eine `pointer` auf ein bestimmtes Element verweisen, das mit einer Anfrage gesendet werden muss. Die Seitennummerierung des Zeigertyps erfordert den Pfad in der Payload, der auf die nächste Seite verweist.</li></ul> |
| `sourceSpec.attributes.paginationParams.limitName` | Der Name des Limits, mit dem die API die Anzahl der Datensätze angeben kann, die auf einer Seite abgerufen werden sollen. | `count` |
| `sourceSpec.attributes.paginationParams.limitValue` | Die Anzahl der Datensätze, die auf einer Seite abgerufen werden sollen. | `100` |
| `sourceSpec.attributes.paginationParams.offSetName` | Der Name des Offset-Attributs. Dies ist erforderlich, wenn der Paginierungstyp auf `offset`. | `offset` |
| `sourceSpec.attributes.paginationParams.pointerName` | Der Zeiger-Attributname. Dies erfordert den JSON-Pfad zum -Attribut, das auf die nächste Seite verweist. Dies ist erforderlich, wenn der Paginierungstyp auf `pointer`. | `pointer` |
| `sourceSpec.attributes.scheduleParams` | Enthält Parameter, die unterstützte Planungsformate für Ihre Quelle definieren. Zeitplanparameter beinhalten `startTime` und `endTime`, mit denen Sie bestimmte Zeitintervalle für Batch-Ausführungen festlegen können. Dadurch wird sichergestellt, dass in einer vorherigen Batch-Ausführung abgerufene Datensätze nicht erneut abgerufen werden. |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamName` | Definiert den Parameternamen für die Startzeit | `since_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamName` | Definiert den Namen des Endzeit-Parameters | `before_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamFormat` | Definiert das unterstützte Format für `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamFormat` | Definiert das unterstützte Format für `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
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