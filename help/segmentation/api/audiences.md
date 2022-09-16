---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; Zielgruppen; Zielgruppe; API; API;
title: Zielgruppen-API-Endpunkt
topic-legacy: developer guide
description: Mit dem Zielgruppen-Endpunkt in der Adobe Experience Platform Segmentation Service-API können Sie Zielgruppen für Ihr Unternehmen programmgesteuert verwalten.
exl-id: cb1a46e5-3294-4db2-ad46-c5e45f48df15
source-git-commit: 322b9aa5b817276eb4b56daf6e410944591c1d51
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 8%

---

# Zielgruppen-Endpunkt

Eine Zielgruppe ist eine Sammlung von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese Personensammlungen können entweder mit Adobe Experience Platform oder aus externen Quellen erstellt werden. Sie können die `/audiences` -Endpunkt in der Segmentation-API, mit dem Sie Zielgruppen programmgesteuert abrufen, erstellen, aktualisieren und löschen können.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-. Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Informationen zum Lesen von Beispiel-API-Aufrufen.

## Abrufen einer Zielgruppenliste {#list}

Sie können eine Liste aller Zielgruppen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an die `/audiences` -Endpunkt.

**API-Format**

Der `/audiences`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Diese Parameter sind zwar optional, doch wird ihre Verwendung dringend empfohlen, um bei der Auflistung von Ressourcen den teuren Verwaltungsaufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Zielgruppen abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /audiences
GET /audiences?{QUERY_PARAMETERS}
```

Beim Abrufen einer Zielgruppenliste können die folgenden Abfrageparameter verwendet werden:

| Abfrageparameter | Beschreibung | Beispiel |
| --------------- | ----------- | ------- |
| `start` | Gibt den Startversatz für die zurückgegebenen Zielgruppen an. | `start=5` |
| `limit` | Gibt die maximale Anzahl von Zielgruppen an, die pro Seite zurückgegeben werden. | `limit=10` |
| `sort` | Gibt die Reihenfolge an, nach der die Ergebnisse sortiert werden sollen. Dies wird im Format `attributeName:[desc/asc]`. | `sort=updateTime:desc` |
| `property` | Ein Filter, mit dem Sie Zielgruppen angeben können, die **just** mit dem Wert eines Attributs übereinstimmen. Dies wird im Format `property=` | `property=audienceId==test-audience-id` |
| `name` | Ein Filter, mit dem Sie Zielgruppen angeben können, deren Namen **contain** den bereitgestellten Wert. Bei diesem Wert wird nicht zwischen Groß- und Kleinschreibung unterschieden. | `name=Sample` |
| `description` | Ein Filter, mit dem Sie Zielgruppen angeben können, deren Beschreibungen **contain** den bereitgestellten Wert. Bei diesem Wert wird nicht zwischen Groß- und Kleinschreibung unterschieden. | `description=Test Description` |
| `withMetrics` | Ein Filter, der die Metriken zusätzlich zu den Zielgruppen zurückgibt. | `property=withMetrics==true` |

>[!IMPORTANT]
>
>Für Zielgruppen werden Metriken unter der `metrics` und enthält Informationen zu Profilzählungen, zur Erstellung und Aktualisierung von Zeitstempeln.

**Keine Metriken**

Das folgende Anfrage-/Antwortpaar wird verwendet, wenn die `withMetrics` -Abfrageparameter ist nicht vorhanden.

**Anfrage**

Mit der folgenden Anfrage werden die letzten fünf Zielgruppen abgerufen, die in Ihrer Organisation erstellt wurden.

```shell
curl -X GET https: //platform.adobe.io/data/core/ups/audiences?limit=5 \
 -H 'Authorization:  Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id:  {IMS_ORG}' \
 -H 'x-api-key:  {API_KEY}' \
 -H 'x-sandbox-name:  {SANDBOX_NAME}'
```

**Antwort** {#no-metrics}

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste von Zielgruppen zurück, die in Ihrem Unternehmen als JSON erstellt wurden.

>[!NOTE]
>
>Die folgende Antwort wurde aus Platzgründen abgeschnitten und zeigt nur die erste zurückgegebene Zielgruppe an.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "isSystem": false,
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
    ]
}
```

| Eigenschaft | Zielgruppentyp | Beschreibung |
| -------- | ------------- | ----------- | 
| `id` | Beide | Eine systemgenerierte schreibgeschützte Kennung für die Zielgruppe. |
| `audienceId` | Beide | Wenn es sich bei der Audience um eine Platform-generierte Audience handelt, ist dies derselbe Wert wie der `id`. Wenn die Audience extern generiert wird, wird dieser Wert vom Client bereitgestellt. |
| `schema` | Beide | Das Experience-Datenmodell (XDM)-Schema der Zielgruppe. |
| `imsOrgId` | Beide | Die ID der Organisation, zu der die Zielgruppe gehört. |
| `sandbox` | Beide | Informationen zur Sandbox, zu der die Zielgruppe gehört. Weitere Informationen zu Sandboxes finden Sie im [Sandbox-Übersicht](../../sandboxes/home.md). |
| `name` | Beide | Der Name der Zielgruppe. |
| `description` | Beide | Eine Beschreibung der Zielgruppe. |
| `expression` | Plattformgenerierte | Der PQL-Ausdruck (Profile Query Language) der Audience. Weitere Informationen zu PQL-Ausdrücken finden Sie im [Handbuch zu PQL-Ausdrücken](../pql/overview.md). |
| `mergePolicyId` | Plattformgenerierte | Die Kennung der Zusammenführungsrichtlinie, mit der die Zielgruppe verknüpft ist. Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im [Handbuch zu Zusammenführungsrichtlinien](../../profile/api/merge-policies.md). |
| `evaluationInfo` | Plattformgenerierte | Zeigt an, wie die Zielgruppe bewertet wird. Mögliche Auswertungsmethoden sind Batch, Streaming oder Edge. Weitere Informationen zu den Bewertungsmethoden finden Sie im [Segmentierungsübersicht](../home.md) |
| `dependents` | Beide | Ein Array von Zielgruppen-IDs, die von der aktuellen Zielgruppe abhängen. Dies wird verwendet, wenn Sie eine Zielgruppe erstellen, die ein Segment eines Segments ist. |
| `dependencies` | Beide | Ein Array von Zielgruppen-IDs, von denen die Zielgruppe abhängig ist. Dies wird verwendet, wenn Sie eine Zielgruppe erstellen, die ein Segment eines Segments ist. |
| `type` | Beide | Ein systemgeneriertes Feld, das anzeigt, ob die Zielgruppe Platform-generiert ist oder eine extern generierte Zielgruppe ist. Mögliche Werte sind `SegmentDefinition` und `ExternalAudience`. A `SegmentDefinition` bezieht sich auf eine Zielgruppe, die in Platform generiert wurde, während eine `ExternalAudience` bezieht sich auf eine Zielgruppe, die nicht in Platform generiert wurde. |
| `createdBy` | Beide | Die ID des Benutzers, der die Zielgruppe erstellt hat. |
| `labels` | Beide | Datennutzung auf Objektebene und attributbasierte Zugriffssteuerungsbeschriftungen, die für die Zielgruppe relevant sind. |
| `namespace` | Beide | Der Namespace, zu dem die Zielgruppe gehört. Mögliche Werte sind `AAM`, `AAMSegments`, `AAMTraits`und `AEPSegments`. |
| `audienceMeta` | Extern | Extern erstellte Metadaten aus der extern erstellten Zielgruppe. |

**Mit Metriken**

Das folgende Anfrage-/Antwortpaar wird verwendet, wenn die `withMetrics` -Abfrageparameter vorhanden ist.

**Anfrage**

Mit der folgenden Anfrage werden die letzten fünf Zielgruppen mit Metriken abgerufen, die in Ihrer Organisation erstellt wurden.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences?propoerty=withMetrics==true&limit=5&sort=totalProfiles:desc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste von Zielgruppen mit Metriken für die angegebene Organisation als JSON zurück.

>[!NOTE]
>
>Die folgende Antwort wurde aus Platzgründen abgeschnitten und zeigt nur die erste zurückgegebene Zielgruppe an.

```json
{
    "children": [
        {
            "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "isSystem": false,
            "name": "People who ordered in the last 30 days",
            "description": "Last 30 days",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"US\""
            },
            "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1650374572000,
            "updateEpoch": 1650374573,
            "updateTime": 1650374573000,
            "createEpoch": 1650374572,
            "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
            "dependents": [],
            "definedOn": [
                {
                    "meta: resourceType": "unions",
                    "meta: containerId": "tenant",
                    "$ref": "https: //ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "dependencies": [],
            "metrics": {
                "type": "export",
                "jobId": "test-job-id",
                "id": "32a83b5d-a118-4bd6-b3cb-3aee2f4c30a1",
                "data": {
                    "totalProfiles": 11200769,
                    "totalProfilesByNamespace": {
                        "crmid": 11400769
                    },
                    "totalProfilesByStatus": {
                        "existing": 11400769
                    }
                },
                "createEpoch": 1653583927,
                "updateEpoch": 1653583927
            },
            "type": "SegmentDefinition",
            "overridePerformanceWarnings": false,
            "createdBy": "{CREATED_BY_ID}",
            "lifecycle": "published",
            "labels": [
                "core/C1"
            ],
            "namespace": "AEPSegments"
        }
   ],
   "_page": {
      "totalCount": 111,
      "pageSize": 5,
      "next": "1"
   },
   "_links": {
      "next": {
         "href": "@/audiences?start=1&limit=5&totalCount=111"
      }
   }
}
```

In den folgenden Listen werden die Eigenschaften aufgeführt **exklusiv** der `withMetrics` Antwort. Wenn Sie die standardmäßigen Zielgruppeneigenschaften kennen möchten, lesen Sie bitte die [vorheriger Abschnitt](#no-metrics).

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `metrics.imsOrgId` | Die Organisations-ID der Zielgruppe. |
| `metrics.sandbox` | Die mit der Zielgruppe verbundenen Sandbox-Informationen. |
| `metrics.jobId` | Die ID des Segmentauftrags, der die Zielgruppe verarbeitet. |
| `metrics.type` | Der Auftragstyp des Segments. Dies kann entweder `export` oder `batch_segmentation`. |
| `metrics.id` | Die Kennung der Zielgruppe. |
| `metrics.data` | Metriken mit Bezug zur Zielgruppe. Dazu gehören Informationen wie die Gesamtzahl der in der Audience enthaltenen Profile, die Gesamtzahl der Profile pro Namespace und die Gesamtzahl der Profile pro Status. |
| `metrics.createEpoch` | Ein Zeitstempel, der anzeigt, wann die Audience erstellt wurde. |
| `metrics.updateEpoch` | Ein Zeitstempel, der anzeigt, wann die Zielgruppe zuletzt aktualisiert wurde. |

## Erstellen einer neuen Zielgruppe {#create}

Sie können eine neue Zielgruppe erstellen, indem Sie eine POST-Anfrage an die `/audiences` -Endpunkt.

**API-Format**

```http
POST /audiences
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/audiences
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "type": "SegmentDefinition",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "labels": [
          "core/C1"
        ]
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `name` | Der Name der Zielgruppe. |
| `description` | Eine Beschreibung der Zielgruppe. |
| `type` | Ein Feld, das anzeigt, ob die Zielgruppe Platform-generiert oder eine extern generierte Zielgruppe ist. Mögliche Werte sind `SegmentDefinition` und `ExternalAudience`. A `SegmentDefinition` bezieht sich auf eine Zielgruppe, die in Platform generiert wurde, während eine `ExternalAudience` bezieht sich auf eine Zielgruppe, die nicht in Platform generiert wurde. |
| `expression` | Der PQL-Ausdruck (Profile Query Language) der Audience. Weitere Informationen zu PQL-Ausdrücken finden Sie im [Handbuch zu PQL-Ausdrücken](../pql/overview.md). |
| `schema` | Das Experience-Datenmodell (XDM)-Schema der Zielgruppe. |
| `labels` | Datennutzung auf Objektebene und attributbasierte Zugriffssteuerungsbeschriftungen, die für die Zielgruppe relevant sind. |

**Antwort**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
     "schema": {
      "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,     
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Bestimmte Zielgruppe nachschlagen {#get}

Sie können detaillierte Informationen zu einer bestimmten Zielgruppe nachschlagen, indem Sie eine GET-Anfrage an die `/audiences` -Endpunkt und geben Sie die Kennung der Zielgruppe an, die Sie im Anfragepfad abrufen möchten.

**API-Format**

```http
GET /audiences/{AUDIENCE_ID}
GET /audiences/{AUDIENCE_ID}?property=withmetrics==true
```

| Parameter | Beschreibung |
| --------- | ----------- | 
| `{AUDIENCE_ID}` | Die Kennung der Zielgruppe, die Sie abrufen möchten. |
| `property=withmetrics==true` | Ein optionaler Abfrageparameter, den Sie verwenden können, wenn Sie eine bestimmte Zielgruppe mit den Zielgruppenmetriken abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Informationen zur angegebenen Zielgruppe zurück. Die Antwort unterscheidet sich je nachdem, ob die Zielgruppe mit Adobe Experience Platform oder externen Quellen generiert wurde.

**Plattformgenerierte**

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem": false,
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"US\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
        "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

**Extern generiert**

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "externalSegment1",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "isSystem":false,
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "active",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "labels": [
        "core/C1"
    ],
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Aktualisieren eines Felds in einer Audience {#update-field}

Sie können die Felder einer bestimmten Zielgruppe aktualisieren, indem Sie eine PATCH-Anfrage an die `/audiences` -Endpunkt und die Kennung der Zielgruppe angeben, die Sie im Anfragepfad aktualisieren möchten.

**API-Format**

```http
PATCH /audiences/{AUDIENCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{AUDIENCE_ID}` | Die ID der Zielgruppe, die Sie aktualisieren möchten. |

**Anfrage**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
     [
        {
            "op": "add",
            "path": "/expression",
            "value": {
                "type": "PQL",
                "format": "pql/text",
                "value": "workAddress.country = \"CA\""
            }
        }
      ]'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `op` | Für die Aktualisierung von Zielgruppen ist dieser Wert immer `add`. |
| `path` | Der Pfad des Felds, das Sie aktualisieren möchten. |
| `value` | Der Wert, auf den das Feld aktualisiert werden soll. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Informationen zu Ihrer neu aktualisierten Zielgruppe zurück.

```json
{
    "id": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "mergePolicyId": "ef006bbe-750e-4e81-85f0-0c6902192dcc",
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
    },
    "dataGovernancePolicy": {
      "excludeOptOut": true
    },
    "creationTime": 1650374572000,
    "updateEpoch": 1650374573,
    "updateTime": 1650374573000,
    "createEpoch": 1650374572,
    "_etag": "\"33120d7c-0000-0200-0000-625eb7ad0000\"",
    "dependents": [],
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [],
    "type": "SegmentDefinition",
    "overridePerformanceWarnings": false,
    "createdBy": "{CREATED_BY_ID}",
    "lifecycle": "active",
    "labels": [
      "core/C1"
    ],
    "namespace": "AEPSegments"
}
```

## Audience aktualisieren {#put}

Sie können eine bestimmte Zielgruppe aktualisieren (überschreiben), indem Sie eine PUT-Anfrage an die `/audiences` -Endpunkt und die Kennung der Zielgruppe angeben, die Sie im Anfragepfad aktualisieren möchten.

**API-Format**

```http
PUT /audiences/{AUDIENCE_ID}
```

**Anfrage**

```shell
curl -X PUT https://platform.adobe.io/data/core/ups/audiences/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "audienceId":"test-external-audience-id",
    "name":"new externalSegment",
    "namespace":"aam",
    "description":"Last 30 days",
    "type":"ExternalSegment",
    "lifecycle":"published",
    "datasetId":"6254cf3c97f8e31b639fb14d",
    "labels":[
        "core/C1"
    ]
}' 
```

| Eigenschaft | Beschreibung |
| -------- | ----------- | 
| `audienceId` | Die Kennung der Audience. Dies wird von externen Zielgruppen verwendet |
| `name` | Der Name der Zielgruppe. |
| `namespace` |  |
| `description` | Eine Beschreibung der Zielgruppe. |
| `type` | Ein systemgeneriertes Feld, das anzeigt, ob die Zielgruppe Platform-generiert ist oder eine extern generierte Zielgruppe ist. Mögliche Werte sind `SegmentDefinition` und `ExternalAudience`. A `SegmentDefinition` bezieht sich auf eine Zielgruppe, die in Platform generiert wurde, während eine `ExternalAudience` bezieht sich auf eine Zielgruppe, die nicht in Platform generiert wurde. |
| `lifecycle` | Der Status der Zielgruppe. Mögliche Werte sind `draft`, `published`, `inactive`und `archived`. `draft` steht für den Zeitpunkt der Erstellung der Audience; `published` wann die Audience veröffentlicht wird, `inactive` wenn die Zielgruppe nicht mehr aktiv ist, und `archived` wenn die Zielgruppe gelöscht wird. |
| `datasetId` | Die ID des Datensatzes, in dem die Zielgruppendaten gefunden werden können. |
| `labels` | Datennutzung auf Objektebene und attributbasierte Zugriffssteuerungsbeschriftungen, die für die Zielgruppe relevant sind. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu aktualisierten Zielgruppe zurück. Beachten Sie, dass die Details Ihrer Zielgruppe je nachdem, ob es sich um eine Platform-generierte Zielgruppe oder eine extern generierte Zielgruppe handelt, unterschiedlich sind.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "audienceId": "test-external-audience-id",
    "name": "new externalSegment",
    "namespace": "aam",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "6ed34f6f-fe21-4a30-934f-6ffe21fa3075",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "type": "ExternalSegment",
    "lifecycle": "published",
    "createdBy": "{CREATED_BY_ID}",
    "datasetId": "6254cf3c97f8e31b639fb14d",
    "_etag": "\"f4102699-0000-0200-0000-625cd61a0000\"",
    "creationTime": 1650251290000,
    "updateEpoch": 1650251290,
    "updateTime": 1650251290000,
    "createEpoch": 1650251290
}
```

## Löschen einer Zielgruppe {#delete}

Sie können eine bestimmte Zielgruppe löschen, indem Sie eine DELETE-Anfrage an die `/audiences` -Endpunkt und die Kennung der Zielgruppe angeben, die Sie im Anfragepfad löschen möchten.

**API-Format**

```http
DELETE /audiences/{AUDIENCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{AUDIENCE_ID}` | Die ID der Zielgruppe, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/audiences/60ccea95-1435-4180-97a5-58af4aa285ab5 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 ohne Meldung zurück.
