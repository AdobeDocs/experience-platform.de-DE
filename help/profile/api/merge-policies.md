---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Entwicklerhandbuch für Customer Profil-API in Echtzeit
topic: guide
translation-type: tm+mt
source-git-commit: 824e9eda41488efc362a6105c552f522185c046d
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 3%

---


# Zusammenführungsrichtlinien

Mit der Adobe Experience Platform können Sie Daten aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige Ansicht der einzelnen Kunden zu erhalten. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine Übersicht zu schaffen. Mit RESTful-APIs oder der Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen festlegen. In diesem Handbuch werden die Schritte zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API beschrieben. Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der Benutzeroberfläche finden Sie im [Benutzerhandbuch](../ui/merge-policies.md)zu Zusammenführungsrichtlinien.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Real-time Customer Profil API. Bevor Sie fortfahren, lesen Sie bitte das Entwicklerhandbuch [zur](getting-started.md)Echtzeit-Customer Profil API. Insbesondere enthält der [Abschnitt](getting-started.md#getting-started) &quot;Erste Schritte&quot;des Profil-Entwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

## Komponenten von Zusammenführungsrichtlinien {#components-of-merge-policies}

Merge-Richtlinien sind privat für Ihre IMS-Organisation, sodass Sie verschiedene Richtlinien erstellen können, um Schema auf die gewünschte Weise zusammenzuführen. Für alle API-Zugriffe auf Profil-Daten ist eine Zusammenführungsrichtlinie erforderlich. Eine Standardeinstellung wird verwendet, wenn keine explizite Angabe erfolgt. Plattform bietet eine standardmäßige Zusammenführungsrichtlinie oder Sie können eine Zusammenführungsrichtlinie für ein bestimmtes Schema erstellen und diese als Standard für Ihr Unternehmen markieren. Jedes Unternehmen kann potenziell über mehrere Zusammenführungsrichtlinien pro Schema verfügen, jedoch kann jedes Schema nur eine Standardzusammenführungsrichtlinie haben. Alle als Standard festgelegten Zusammenführungsrichtlinien werden verwendet, wenn der Schema-Name angegeben wird und eine Zusammenführungsrichtlinie erforderlich, jedoch nicht angegeben ist. Wenn Sie eine Mergerichtlinie als Standard festlegen, werden alle vorhandenen Mergerichtlinien, die zuvor als Standard festgelegt wurden, automatisch aktualisiert, sodass sie nicht mehr als Standard verwendet werden.

### Richtlinienobjekt für Zusammenführung abschließen

Das Objekt für die gesamte Richtlinie zum Zusammenführen stellt einen Satz von Voreinstellungen dar, die bestimmte Aspekte des Zusammenführens von Profil-Fragmenten steuern.

**Richtlinienobjekt zusammenführen**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": {BOOLEAN},
        "updateEpoch": {UPDATE_TIME}
    }
```

| Eigenschaft | Beschreibung |
|---|---|
| `id` | Der vom System erzeugte eindeutige Bezeichner, der zur Erstellungszeit zugewiesen wurde |
| `name` | Benutzerfreundlicher Name, unter dem die Richtlinie zum Zusammenführen in Ansichten der Liste identifiziert werden kann. |
| `imsOrgId` | Organisations-ID, zu der diese Richtlinie gehört |
| `identityGraph` | [Identitätsdiagramm](#identity-graph) -Objekt, das das Identitätsdiagramm angibt, aus dem die entsprechenden Identitäten abgerufen werden. Profil-Fragmente, die für alle verwandten Identitäten gefunden wurden, werden zusammengeführt. |
| `attributeMerge` | [Attributzusammenführungs](#attribute-merge) -Objekt, das angibt, wie die Zusammenführungsrichtlinie bei Datenkonflikten Profil-Attributwerte priorisiert. |
| `schema` | Das [Schema](#schema) -Objekt, für das die Zusammenführungsrichtlinie verwendet werden kann. |
| `default` | Boolescher Wert, der angibt, ob diese Richtlinie für das angegebene Schema standardmäßig verwendet wird. |
| `version` | Plattformgepflegte Version der Zusammenführungsrichtlinie. Dieser schreibgeschützte Wert wird beim Aktualisieren einer Mergerichtlinie inkrementiert. |
| `updateEpoch` | Datum der letzten Aktualisierung der Zusammenführungsrichtlinie. |

**Beispielrichtlinie für die Zusammenführung**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Identitätsdiagramm {#identity-graph}

[Der Adobe Experience Platform Identity Service](../../identity-service/home.md) verwaltet die Identitätsdiagramme, die global und für jedes Unternehmen auf Experience Platform verwendet werden. Das `identityGraph` Attribut der Richtlinie zum Zusammenführen definiert, wie die entsprechenden Identitäten für einen Benutzer bestimmt werden.

**identityGraph-Objekt**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Dabei `{IDENTITY_GRAPH_TYPE}` ist Folgendes zu beachten:

* **&quot;none&quot;:** Keine Identitätszuordnung durchführen.
* **&quot;pdg&quot;:** Führen Sie Identitätszuordnungen basierend auf Ihrem privaten Identitätsdiagramm durch.

**Beispiel`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Attributzusammenführung {#attribute-merge}

Ein Profil-Fragment ist das Profil für nur eine Identität aus der Liste der Identitäten, die für einen bestimmten Benutzer vorhanden sind. Wenn der verwendete Identitätsdiagrammtyp zu mehr als einer Identität führt, besteht die Möglichkeit, dass Werte für die Eigenschaften des Profils miteinander in Konflikt stehen, und die Priorität muss angegeben werden. Mithilfe `attributeMerge`dieser Option können Sie festlegen, welche DataSet-Profil-Werte im Ereignis eines Zusammenführungskonflikts priorisiert werden sollen.

**attributeMerge-Objekt**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Dabei `{ATTRIBUTE_MERGE_TYPE}` ist Folgendes zu beachten:

* **&quot;timestampOrdered&quot;**: (Standard) Geben Sie dem zuletzt aktualisierten Profil im Konfliktfall Priorität. Bei diesem Zusammenführungstyp ist das `data` Attribut nicht erforderlich.
* **&quot;dataSetPrecedence&quot;** : Weisen Sie Fragmenten des Profils Priorität auf der Grundlage des Datensatzes zu, aus dem sie stammen. Dies kann verwendet werden, wenn in einem Datensatz vorhandene Informationen bevorzugt oder gegenüber Daten in einem anderen Datensatz als vertrauenswürdig eingestuft werden. Bei Verwendung dieses Zusammenführungstyps ist das `order` Attribut erforderlich, da es die Datensätze in der Reihenfolge der Priorität Liste.
   * **&quot;Reihenfolge&quot;**: Wenn &quot;dataSetPrecedence&quot;verwendet wird, muss ein `order` Array mit einer Liste von Datensätzen bereitgestellt werden. Datensätze, die nicht in der Liste enthalten sind, werden nicht zusammengeführt. Mit anderen Worten, Datensätze müssen explizit aufgeführt werden, um in ein Profil zusammengeführt zu werden. Das `order` Array Liste die IDs der Datensätze in der Reihenfolge ihrer Priorität.

**Beispiel für attributeMerge-Objekt mit dataSetPrecedence-Typ**

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

**Beispiel für ein attributeMerge-Objekt mit timestampOrderedType**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

Das Schema-Objekt gibt das XDM-Schema an, für das diese Zusammenführungsrichtlinie erstellt wird.

**`schema`object **

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Dabei `name` ist der Wert von der XDM-Klasse, auf der das Schema basiert, das der Mergerichtlinie zugeordnet ist.

**Beispiel`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

## Zugriff auf Zusammenführungsrichtlinien {#access-merge-policies}

Mithilfe der Echtzeit-Client-Profil-API können Sie mit dem `/config/mergePolicies` Endpunkt eine Suchanfrage ausführen, um eine bestimmte Zusammenführungsrichtlinie mit ihrer ID Ansicht oder auf alle Zusammenführungsrichtlinien in Ihrer IMS-Organisation zuzugreifen, gefiltert nach bestimmten Kriterien. Sie können den `/config/mergePolicies/bulk-get` Endpunkt auch verwenden, um mehrere Zusammenführungsrichtlinien nach ihren IDs abzurufen. Die Schritte für die Durchführung dieser Aufrufe sind in den folgenden Abschnitten beschrieben.

### Zugriff auf eine einzige Zusammenführungsrichtlinie mit ID

Sie können auf eine einzelne Mergerichtlinie mit ihrer ID zugreifen, indem Sie eine GET-Anforderung an den `/config/mergePolicies` Endpunkt senden und die `mergePolicyId` im Anforderungspfad einschließen.

**API-Format**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschreibung |
|---|---|
| `{mergePolicyId}` | Der Bezeichner der zusammenzuführenden Richtlinie, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Mergerichtlinie zurück.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

Einzelheiten zu den einzelnen Elementen, aus denen eine Zusammenführungsrichtlinie besteht, finden Sie im Abschnitt [Komponenten der Zusammenführungsrichtlinien](#components-of-merge-policies) zu Beginn dieses Dokuments.

### Abrufen mehrerer Zusammenführungsrichtlinien nach ihren IDs

Sie können mehrere Zusammenführungsrichtlinien abrufen, indem Sie eine POST-Anforderung an den `/config/mergePolicies/bulk-get` Endpunkt senden und die IDs der Zusammenführungsrichtlinien einschließen, die Sie im Anforderungstext abrufen möchten.

**API-Format**

```http
POST /config/mergePolicies/bulk-get
```

**Anfrage**

Der Anforderungstext enthält ein &quot;ids&quot;-Array mit einzelnen Objekten, die die &quot;id&quot; für jede Zusammenführungsrichtlinie enthalten, für die Sie Details abrufen möchten.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**Antwort**

Bei einer erfolgreichen Antwort werden HTTP-Status 207 (Multi-Status) und die Details der Zusammenführungsrichtlinien zurückgegeben, deren IDs in der POST-Anforderung bereitgestellt wurden.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Einzelheiten zu den einzelnen Elementen, aus denen eine Zusammenführungsrichtlinie besteht, finden Sie im Abschnitt [Komponenten der Zusammenführungsrichtlinien](#components-of-merge-policies) zu Beginn dieses Dokuments.

### Liste mehrerer Zusammenführungsrichtlinien nach Kriterien

Sie können mehrere Zusammenführungsrichtlinien innerhalb Ihrer IMS-Organisation Liste haben, indem Sie eine GET-Anforderung an den `/config/mergePolicies` Endpunkt ausgeben und optionale Abfragen zum Filtern, Bestellen und Paginieren der Antwort verwenden. Es können mehrere Parameter eingeschlossen werden, die durch das kaufmännische Und (&amp;) getrennt werden. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihr Unternehmen verfügbaren Zusammenführungsrichtlinien abgerufen.

**API-Format**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
|---|---|
| `default` | Ein boolescher Wert, der von Filtern bestimmt wird, ob die Zusammenführungsrichtlinien die Standardeinstellung für eine Schema-Klasse sind. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die in einer Seite enthalten sind. Standardwert: 20 |
| `orderBy` | Gibt das Feld an, mit dem die Ergebnisse in aufsteigender Reihenfolge sortiert werden `orderBy=name` oder nach Namen sortiert `orderBy=+name` werden oder in absteigender Reihenfolge sortiert werden `orderBy=-name`sollen. Wird dieser Wert nicht angegeben, wird die Standardsortierung in aufsteigender `name` Reihenfolge ausgeführt. |
| `schema.name` | Name des Schemas, für das die verfügbaren Zusammenführungsrichtlinien abgerufen werden sollen. |
| `identityGraph.type` | Filter werden nach dem Identitätsdiagrammtyp berechnet. Mögliche Werte sind &quot;none&quot;und &quot;pdg&quot;(privates Diagramm). |
| `attributeMerge.type` | Filter erhalten die Ergebnisse nach dem verwendeten Attributzusammenführungstyp. Mögliche Werte sind &quot;timestampOrdered&quot;und &quot;dataSetPrecedence&quot;. |
| `start` | Seitenversatz: Geben Sie die Start-ID für die abzurufenden Daten an. Standardwert: 0 |
| `version` | Geben Sie dies an, wenn Sie eine bestimmte Version der Zusammenführungsrichtlinie verwenden möchten. Standardmäßig wird die neueste Version verwendet. |

Weitere Informationen zu `schema.name`, `identityGraph.type`und `attributeMerge.type`zu den [Komponenten der Zusammenführungsrichtlinien](#components-of-merge-policies) finden Sie weiter oben in diesem Handbuch.


**Anfrage**

Die folgende Anforderung Liste alle Zusammenführungsrichtlinien für ein bestimmtes Schema:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Antwort**

Eine erfolgreiche Antwort gibt eine paginierte Liste von Zusammenführungsrichtlinien zurück, die die von den in der Anforderung gesendeten Abfragen angegebenen Kriterien erfüllen.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `_links.next.href` | Eine URI-Adresse für die nächste Ergebnisseite. Verwenden Sie diesen URI als Anforderungsparameter für einen anderen API-Aufruf an denselben Endpunkt, um die Seite Ansicht. Wenn keine nächste Seite vorhanden ist, ist dieser Wert eine leere Zeichenfolge. |

## Eine Richtlinie zum Zusammenführen erstellen

Sie können eine neue Richtlinie zum Zusammenführen für Ihr Unternehmen erstellen, indem Sie eine POST-Anforderung an den `/config/mergePolicies` Endpunkt senden.

**API-Format**

```http
POST /config/mergePolicies
```

**Anforderung** Die folgende Anforderung erstellt eine neue Richtlinie für die Zusammenführung, die durch die in der Payload bereitgestellten Attributwerte konfiguriert wird:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| Eigenschaft | Beschreibung |
|---|---|
| `name` | Ein benutzerfreundlicher Name, unter dem die Fusionspolitik in Ansichten der Liste identifiziert werden kann. |
| `identityGraph.type` | Der Identitätsdiagramm-Typ, aus dem zusammengeführte zugehörige Identitäten abgerufen werden sollen. Mögliche Werte: &quot;none&quot;oder &quot;pdg&quot;(privates Diagramm). |
| `attributeMerge` | Die Art und Weise, wie Profil-Attributwerte bei Datenkonflikten priorisiert werden. |
| `schema` | Die XDM-Schema-Klasse, die der Mergerichtlinie zugeordnet ist. |
| `default` | Gibt an, ob diese Zusammenführungsrichtlinie die Standardrichtlinie für das Schema ist. |

Weitere Informationen finden Sie im Abschnitt [Komponenten der Zusammenführungsrichtlinien](#components-of-merge-policies) .

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Mergerichtlinie zurück.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

Einzelheiten zu den einzelnen Elementen, aus denen eine Zusammenführungsrichtlinie besteht, finden Sie im Abschnitt [Komponenten der Zusammenführungsrichtlinien](#components-of-merge-policies) zu Beginn dieses Dokuments.

## Eine Richtlinie zum Zusammenführen aktualisieren {#update}

Sie können eine vorhandene Richtlinie zum Zusammenführen ändern, indem Sie einzelne Attribute (PATCH) bearbeiten oder die gesamte Richtlinie zum Zusammenführen mit neuen Attributen (PUT) überschreiben. Nachfolgend sind Beispiele für die einzelnen Beispiele aufgeführt.

### Bearbeiten einzelner Felder mit Richtlinien für die Zusammenführung

Sie können einzelne Felder für eine Richtlinie zum Zusammenführen bearbeiten, indem Sie eine PATCH-Anforderung an den `/config/mergePolicies/{mergePolicyId}` Endpunkt senden:

**API-Format**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschreibung |
|---|---|
| `{mergePolicyId}` | Der Bezeichner der zusammenzuführenden Richtlinie, die Sie löschen möchten. |

**Anfrage**

Mit der folgenden Anforderung wird eine angegebene Merge-Richtlinie aktualisiert, indem der Wert ihrer `default` Eigenschaft in `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `op` | Gibt den zu verwendenden Vorgang an. Beispiele für andere PATCH-Vorgänge finden Sie in der [JSON Patch-Dokumentation.](http://jsonpatch.com) |
| `path` | Der Pfad des zu aktualisierenden Felds. Akzeptierte Werte sind: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | Der Wert, auf den das angegebene Feld festgelegt werden soll. |

Weitere Informationen finden Sie im Abschnitt [Komponenten der Zusammenführungsrichtlinien](#components-of-merge-policies) .


**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu aktualisierten Zusammenführungsrichtlinie zurück.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

### Überschreiben einer Richtlinie zum Zusammenführen

Eine andere Möglichkeit, eine Richtlinie zum Zusammenführen zu ändern, besteht darin, eine PUT-Anforderung zu verwenden, die die gesamte Richtlinie zum Zusammenführen überschreibt.

**API-Format**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschreibung |
|---|---|
| `{mergePolicyId}` | Der Bezeichner der Mergerichtlinie, die Sie überschreiben möchten. |

**Anfrage**

Die folgende Anforderung überschreibt die angegebene Zusammenführungsrichtlinie und ersetzt deren Attributwerte durch die in der Payload bereitgestellten Werte. Da diese Anforderung eine vorhandene Fusionsrichtlinie vollständig ersetzt, müssen Sie alle Felder bereitstellen, die beim Definieren der Richtlinie zum Zusammenführen erforderlich waren. Diesmal stellen Sie jedoch aktualisierte Werte für die Felder bereit, die Sie ändern möchten.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `name` | Ein benutzerfreundlicher Name, unter dem die Fusionspolitik in Ansichten der Liste identifiziert werden kann. |
| `identityGraph` | Das Identitätsdiagramm, aus dem zusammengeführte zugehörige Identitäten abgerufen werden. |
| `attributeMerge` | Die Art und Weise, wie Profil-Attributwerte bei Datenkonflikten priorisiert werden. |
| `schema` | Die XDM-Schema-Klasse, die der Mergerichtlinie zugeordnet ist. |
| `default` | Gibt an, ob diese Zusammenführungsrichtlinie die Standardrichtlinie für das Schema ist. |

Weitere Informationen finden Sie im Abschnitt [Komponenten der Zusammenführungsrichtlinien](#components-of-merge-policies) .


**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Zusammenführungsrichtlinie zurück.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

## Eine Richtlinie zum Zusammenführen löschen

Eine Richtlinie zum Zusammenführen kann gelöscht werden, indem eine DELETE-Anforderung an den `/config/mergePolicies` Endpunkt gesendet wird und die ID der Richtlinie zum Zusammenführen, die Sie im Anforderungspfad löschen möchten.

**API-Format**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschreibung |
|---|---|
| `{mergePolicyId}` | Der Bezeichner der zusammenzuführenden Richtlinie, die Sie löschen möchten. |

**Anfrage**

Mit der folgenden Anforderung wird eine Richtlinie zum Zusammenführen gelöscht.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Bei einer erfolgreichen Löschanforderung werden HTTP-Status 200 (OK) und ein leerer Antworttext zurückgegeben. Um zu bestätigen, dass der Löschvorgang erfolgreich war, können Sie eine GET-Anforderung ausführen, um die Zusammenführungsrichtlinie nach ihrer ID Ansicht. Wenn die Richtlinie zum Zusammenführen gelöscht wurde, erhalten Sie einen HTTP-Status-404-Fehler (nicht gefunden).

## Nächste Schritte

Da Sie nun wissen, wie Sie Zusammenführungsrichtlinien für Ihre IMS-Organisation erstellen und konfigurieren, können Sie diese verwenden, um Audiencen-Segmente aus Ihren Echtzeit-Kundendaten zu erstellen. Informationen zum Definieren und Arbeiten mit Segmenten finden Sie in der Dokumentation [zum Segmentierungsdienst für](../../segmentation/home.md) Adobe Experience Platform.



