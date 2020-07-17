---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentdefinitionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 41a5d816f9dc6e7c26141ff5e9173b1b5631d75e
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 28%

---


# Endpunktleitfaden für Segmentdefinitionen

Mit Adobe Experience Platform können Sie Segmente erstellen, die eine Gruppe spezifischer Attribute oder Verhaltensweisen aus einer Gruppe von Profilen definieren. Eine Segmentdefinition ist ein Objekt, das eine in [!DNL Profile Query Language] (PQL) geschriebene Abfrage kapselt. Dieses Objekt wird auch als PQL-Vorhersage bezeichnet. PQL-Prädikate definieren die Regeln für das Segment basierend auf Bedingungen, die sich auf die Daten aus Datensatz oder Zeitreihen beziehen, die Sie bereitstellen [!DNL Real-time Customer Profile]. Weitere Informationen zum Schreiben von PQL-Abfragen finden Sie im [PQL-Handbuch](../pql/overview.md) .

Dieses Handbuch enthält Informationen zum besseren Verständnis der Segmentdefinitionen sowie Beispiele für API-Aufrufe zur Durchführung grundlegender Aktionen mit der API.

## Erste Schritte

The endpoints used in this guide are part of the [!DNL Adobe Experience Platform Segmentation Service] API. Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example API calls.

## Abrufen einer Liste von Segmentdefinitionen {#list}

Sie können eine Liste aller Segmentdefinitionen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den `/segment/definitions`-Endpunkt senden.

**API-Format**

Der `/segment/definitions` Endpunkt unterstützt mehrere Abfragen-Parameter, um die Ergebnisse zu filtern. Diese Parameter sind optional, ihre Verwendung wird jedoch dringend empfohlen, um den kostspieligen Aufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihr Unternehmen verfügbaren Segmentdefinitionen abgerufen. Es können mehrere Parameter eingeschlossen werden, getrennt durch das kaufmännische Und-Zeichen (`&`).

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Abfrage**

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `start` | Gibt den Startversatz für die zurückgegebenen Segmentdefinitionen an. | `start=4` |
| `limit` | Gibt die Anzahl der pro Seite zurückgegebenen Segmentdefinitionen an. | `limit=20` |
| `page` | Gibt an, auf welcher Seite die Ergebnisse der Segmentdefinitionen beginnen. | `page=5` |
| `sort` | Gibt an, nach welchem Feld die Ergebnisse sortiert werden sollen. Is written in the following format: `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Gibt an, ob die Segmentdefinition Streaming-fähig ist. | `evaluationInfo.continuous.enabled=true` |

**Anfrage**

Die folgende Anforderung ruft die letzten beiden Segmentdefinitionen ab, die in Ihrer IMS-Organisation veröffentlicht wurden.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste von Segmentdefinitionen für die angegebene IMS-Organisation als JSON zurück.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1573253640000,
            "baselineTime": 1574327114,
            "updateEpoch": 1575588309,
            "updateTime": 1575588309000
        },
        {
            "id": "ca763983-5572-4ea4-809c-b7dff7e0d79b",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG}",
            "name": "test segment",
            "description": "",
            "expression": {
                "type": "PQL",
                "format": "pql/json",
                "value": "{PQL_EXPRESSION}"
            },
            "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 1561073779000,
            "baselineTime": 1574327114,
            "updateEpoch": 1574327114,
            "updateTime": 1574327114000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Erstellen einer neuen Segmentdefinition {#create}

Sie können eine neue Segmentdefinition erstellen, indem Sie eine POST-Anfrage an den `/segment/definitions`-Endpunkt senden.

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "workAddress.country = \"US\""
        },
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | **Erforderlich.** Ein eindeutiger Name, unter dem auf das Segment verwiesen wird. |
| `schema` | **Erforderlich.** Das Schema, das den Entitäten im Segment zugeordnet ist. Besteht aus einem `id` oder einem `name` Feld. |
| `expression` | **Erforderlich.** Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruck-Typ an. Derzeit wird nur &quot;PQL&quot;unterstützt. |
| `expression.format` | Gibt die Wertstruktur des Ausdrucks an. Derzeit wird folgendes Format unterstützt: <ul><li>`pql/text`: Eine Textdarstellung einer Segmentdefinition gemäß der veröffentlichten PQL-Grammatik.  Beispiel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ein Ausdruck, der dem unter `expression.format`Angabe angegebenen Typ entspricht. |
| `description` | Eine für Menschen lesbare Beschreibung der Definition. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Segmentdefinition zurück.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Eine systemgenerierte ID der neu erstellten Segmentdefinition. |
| `evaluationInfo` | Ein systemgeneriertes Objekt, das angibt, welcher Typ von Bewertung die Segmentdefinition durchlaufen soll. Es kann sich um Batch-, Continuous- (auch als Streaming bezeichnet) oder synchrone Segmentierung handeln. |

## Abrufen einer bestimmten Segmentdefinition {#get}

You can retrieve detailed information about a specific segment definition by making a GET request to the `/segment/definitions` endpoint and providing the ID of the segment definition you wish to retrieve in the request path.

**API-Format**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SEGMENT_ID}` | Der `id`-Wert der Segmentdefinition, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Segmentdefinition zurück.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Eine vom System generierte schreibgeschützte ID der Segmentdefinition. |
| `name` | Ein eindeutiger Name, unter dem auf das Segment verwiesen wird. |
| `schema` | Das Schema, das den Entitäten im Segment zugeordnet ist. Besteht aus einem `id` oder einem `name` Feld. |
| `expression` | Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruck-Typ an. Derzeit wird nur &quot;PQL&quot;unterstützt. |
| `expression.format` | Gibt die Wertstruktur des Ausdrucks an. Derzeit wird folgendes Format unterstützt: <ul><li>`pql/text`: Eine Textdarstellung einer Segmentdefinition gemäß der veröffentlichten PQL-Grammatik.  Beispiel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ein Ausdruck, der dem unter `expression.format`Angabe angegebenen Typ entspricht. |
| `description` | Eine für Menschen lesbare Beschreibung der Definition. |
| `evaluationInfo` | Ein systemgeneriertes Objekt, das angibt, welcher Typ von Evaluierung, Stapel, kontinuierlicher (auch als Streaming bezeichnet) oder synchroner Segmentdefinition unterzogen wird. |

## Segmentdefinitionen stapelweise abrufen {#bulk-get}

Sie können detaillierte Informationen zu mehreren angegebenen Segmentdefinitionen abrufen, indem Sie eine POST-Anforderung an den `/segment/definitions/bulk-get` Endpunkt senden und die `id` Werte der Segmentdefinitionen im Anforderungstext angeben.

**API-Format**

```http
POST /segment/definitions/bulk-get
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "54669488-03ab-4e0d-a694-37fe49e32be8"
            },
            {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05"
            }
        ]
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 207 mit den angeforderten Segmentdefinitionen zurück.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        },
        "4afe34ae-8c98-4513-8a1d-67ccaa54bc05": {
            "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 60,
            "profileInstanceId": "ups",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
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
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "dataGovernancePolicy": {
                "excludeOptOut": true
            },
            "creationTime": 0,
            "updateEpoch": 1579292094,
            "updateTime": 1579292094000
        }

    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Eine vom System generierte schreibgeschützte ID der Segmentdefinition. |
| `name` | Ein eindeutiger Name, unter dem auf das Segment verwiesen wird. |
| `schema` | Das Schema, das den Entitäten im Segment zugeordnet ist. Besteht aus einem `id` oder einem `name` Feld. |
| `expression` | Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruck-Typ an. Derzeit wird nur &quot;PQL&quot;unterstützt. |
| `expression.format` | Gibt die Wertstruktur des Ausdrucks an. Derzeit wird folgendes Format unterstützt: <ul><li>`pql/text`: Eine Textdarstellung einer Segmentdefinition gemäß der veröffentlichten PQL-Grammatik.  Beispiel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ein Ausdruck, der dem unter `expression.format`Angabe angegebenen Typ entspricht. |
| `description` | Eine für Menschen lesbare Beschreibung der Definition. |
| `evaluationInfo` | Ein systemgeneriertes Objekt, das angibt, welcher Typ von Evaluierung, Stapel, kontinuierlicher (auch als Streaming bezeichnet) oder synchroner Segmentdefinition unterzogen wird. |

## Löschen einer bestimmten Segmentdefinition {#delete}

Sie können eine bestimmte Segmentdefinition löschen, indem Sie eine DELETE-Anforderung an den `/segment/definitions` Endpunkt senden und die ID der Segmentdefinition angeben, die Sie im Anforderungspfad löschen möchten.

**API-Format**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SEGMENT_ID}` | : Der `id`-Wert der Segmentdefinition, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 ohne Meldung zurück.

## Aktualisieren einer bestimmten Segmentdefinition

Sie können eine bestimmte Segmentdefinition aktualisieren, indem Sie eine PATCH-Anforderung an den `/segment/definitions` Endpunkt senden und die ID der Segmentdefinition angeben, die Sie im Anforderungspfad aktualisieren möchten.

**API-Format**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SEGMENT_ID}` | Der `id`-Wert der Segmentdefinition, die Sie aktualisieren möchten. |

**Anfrage**

Mit der folgenden Anfrage wird das Land der Arbeitsadresse von den USA nach Kanada aktualisiert.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "name": "Updated people who ordered in the last 30 days",
    "profileInstanceId": "ups",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "payloadSchema": "string",
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu aktualisierten Segmentdefinition zurück. Beachten Sie, dass das Land der Arbeitsadresse von den USA (USA) bis Kanada (CA) aktualisiert wurde.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "profileInstanceId": "ups",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "Updated people who ordered in the last 30 days",
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "workAddress.country = \"CA\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579295340,
    "updateTime": 1579295340000
}
```

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis dafür, wie Segmentdefinitionen funktionieren. Weitere Informationen zum Erstellen eines Segments finden Sie im Lernprogramm zum [Erstellen eines Segments](../tutorials/create-a-segment.md) .