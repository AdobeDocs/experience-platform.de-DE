---
solution: Experience Platform
title: API-Endpunkt für Segmentdefinitionen
description: Mit dem Endpunkt Segmentdefinitionen in der Segmentierungs-Service-API von Adobe Experience Platform können Sie Segmentdefinitionen für Ihr Unternehmen programmgesteuert verwalten.
role: Developer
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: b3c7b97e257f76337bd02d1db9390ab314f7d1cd
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 13%

---

# Endpunkt für Segmentdefinitionen

Mit Adobe Experience Platform können Sie Segmentdefinitionen erstellen, die eine Gruppe spezifischer Attribute oder Verhaltensweisen aus einer Gruppe von Profilen definieren. Eine Segmentdefinition ist ein Objekt, das eine in [!DNL Profile Query Language] (PQL) geschriebene Abfrage kapselt. Segmentdefinitionen werden auf Profile angewendet, um Zielgruppen zu erstellen. Dieses Objekt (Segmentdefinition) wird auch als PQL-Prädikat bezeichnet. PQL-Prädikate definieren die Regeln für die Segmentdefinition basierend auf Bedingungen, die sich auf Datensatz- oder Zeitreihendaten beziehen, die Sie [!DNL Real-Time Customer Profile] bereitstellen. Weitere Informationen zum Schreiben von PQL-Abfragen [&#128279;](../pql/overview.md) Sie im Handbuch zu PQL .

Dieses Handbuch enthält Informationen, die Ihnen dabei helfen, Segmentdefinitionen besser zu verstehen, und enthält Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mit der -API.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-API. Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](./getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderlichen Kopfzeilen sowie Beispiele für API-Aufrufe lesen können.

## Abrufen einer Liste von Segmentdefinitionen {#list}

Sie können eine Liste aller Segmentdefinitionen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den `/segment/definitions`-Endpunkt stellen.

**API-Format**

Der `/segment/definitions`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Obwohl diese Parameter optional sind, wird ihre Verwendung dringend empfohlen, um kostspieligen Aufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Segmentdefinitionen abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Abfrageparameter**

+++ Eine Liste der verfügbaren Abfrageparameter.

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `start` | Gibt den Anfangsversatz für die zurückgegebenen Segmentdefinitionen an. | `start=4` |
| `limit` | Gibt die Anzahl der pro Seite zurückgegebenen Segmentdefinitionen an. | `limit=20` |
| `page` | Gibt an, auf welcher Seite die Ergebnisse der Segmentdefinitionen beginnen. | `page=5` |
| `sort` | Gibt an, nach welchem Feld die Ergebnisse sortiert werden sollen. Wird im folgenden Format geschrieben: `[attributeName]:[desc/asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Gibt an, ob die Segmentdefinition Streaming-fähig ist. | `evaluationInfo.continuous.enabled=true` |

+++

**Anfrage**

Die folgende Anfrage ruft die letzten beiden Segmentdefinitionen ab, die in Ihrer Organisation veröffentlicht wurden.

+++ Eine Beispielanfrage zum Abrufen einer Liste von Segmentdefinitionen.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit einer Liste von Segmentdefinitionen für die angegebene Organisation als JSON zurück.

+++ Eine Beispielantwort beim Abrufen einer Liste von Segmentdefinitionen.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

+++

## Erstellen einer neuen Segmentdefinition {#create}

Sie können eine neue Segmentdefinition erstellen, indem Sie eine POST-Anfrage an den `/segment/definitions`-Endpunkt senden.

>[!IMPORTANT]
>
>Segmentdefinitionen, die über die API erstellt wurden **können nicht** mit Segment Builder bearbeitet werden.

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

Beim Erstellen einer neuen Segmentdefinition können Sie diese entweder im `pql/text`- oder im `pql/json`-Format erstellen.

>[!BEGINTABS]

>[!TAB Verwenden von pql/text]

+++ Eine Beispielanfrage zum Erstellen einer Segmentdefinition.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
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
        "schema": {
            "name": "_xdm.context.profile"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Ein eindeutiger Name, mit dem auf die Segmentdefinition verwiesen werden kann. |
| `description` | (Optional) Eine Beschreibung der Segmentdefinition, die Sie erstellen. |
| `expression` | Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruckstyp an. Derzeit wird nur PQL unterstützt. |
| `expression.format` | Gibt die Struktur des Ausdrucks im Wert an. Zu den unterstützten Werten gehören `pql/text` und `pql/json`. |
| `expression.value` | Ein Ausdruck, der dem in `expression.format` angegebenen Typ entspricht. |
| `evaluationInfo` | (Optional) Der Typ der Segmentdefinition, die Sie erstellen. Wenn Sie ein Batch-Segment erstellen möchten, setzen Sie `evaluationInfo.batch.enabled` auf „true“. Wenn Sie ein Streaming-Segment erstellen möchten, setzen Sie `evaluationInfo.continuous.enabled` auf „true“. Wenn Sie ein Edge-Segment erstellen möchten, setzen Sie `evaluationInfo.synchronous.enabled` auf „true“. Wenn dies leer gelassen wird, wird die Segmentdefinition als **Batch-** erstellt. |
| `schema` | Das Schema, das mit den Entitäten im Segment verknüpft ist. Besteht entweder aus einem `id` oder aus `name` Feld. |

+++

>[!TAB Verwenden von pql/json]

+++ Eine Beispielanfrage zum Erstellen einer Segmentdefinition.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People who ordered in the last 30 days",
        "profileInstanceId": "ups",
        "description": "Last 30 days",
        "expression": {
            "type": "PQL",
            "format": "pql/json",
            "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"a\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}},{\"nodeType\":\"fieldLookup\",\"fieldName\":\"b\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}]}"
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
        "schema": {
            "name": "_xdm.context.profile"
        },
        "payloadSchema": "string"
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Ein eindeutiger Name, mit dem auf die Segmentdefinition verwiesen werden kann. |
| `description` | (Optional) Eine Beschreibung der Segmentdefinition, die Sie erstellen. |
| `evaluationInfo` | (Optional) Der Typ der Segmentdefinition, die Sie erstellen. Wenn Sie ein Batch-Segment erstellen möchten, setzen Sie `evaluationInfo.batch.enabled` auf „true“. Wenn Sie ein Streaming-Segment erstellen möchten, setzen Sie `evaluationInfo.continuous.enabled` auf „true“. Wenn Sie ein Edge-Segment erstellen möchten, setzen Sie `evaluationInfo.synchronous.enabled` auf „true“. Wenn dies leer gelassen wird, wird die Segmentdefinition als **Batch-** erstellt. |
| `schema` | Das Schema, das mit den Entitäten im Segment verknüpft ist. Besteht entweder aus einem `id` oder aus `name` Feld. |
| `expression` | Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruckstyp an. Derzeit wird nur PQL unterstützt. |
| `expression.format` | Gibt die Struktur des Ausdrucks im Wert an. |
| `expression.value` | Ein Ausdruck, der dem in `expression.format` angegebenen Typ entspricht. |

+++

>[!ENDTABS]

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Segmentdefinition zurück.

+++ Eine Beispielantwort beim Erstellen einer Segmentdefinition.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `id` | Eine systemgenerierte ID Ihrer neu erstellten Segmentdefinition. |
| `evaluationInfo` | Ein -Objekt, das angibt, welcher Art der Auswertung die Segmentdefinition unterzogen wird. Dabei kann es sich um Batch-, Streaming- (auch als fortlaufende Segmentierung bezeichnet) oder Edge- (auch als synchrone Segmentierung bezeichnet) handeln. |

+++

## Abrufen einer bestimmten Segmentdefinition {#get}

Sie können detaillierte Informationen zu einer bestimmten Segmentdefinition abrufen, indem Sie eine GET-Anfrage an den `/segment/definitions`-Endpunkt senden und im Anfragepfad die ID der Segmentdefinition angeben, die Sie abrufen möchten.

**API-Format**

```http
GET /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SEGMENT_ID}` | Der `id` Wert der Segmentdefinition, die Sie abrufen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Abrufen einer Segmentdefinition.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Segmentdefinition zurück.

+++ Eine Beispielantwort beim Abrufen einer Segmentdefinition.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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
| `id` | Eine systemgenerierte schreibgeschützte ID der Segmentdefinition. |
| `name` | Ein eindeutiger Name, mit dem auf die Segmentdefinition verwiesen werden kann. |
| `schema` | Das Schema, das mit den Entitäten im Segment verknüpft ist. Besteht entweder aus einem `id` oder aus `name` Feld. |
| `expression` | Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruckstyp an. Derzeit wird nur PQL unterstützt. |
| `expression.format` | Gibt die Struktur des Ausdrucks im Wert an. Derzeit wird das folgende Format unterstützt: <ul><li>`pql/text`: Eine textliche Darstellung einer Segmentdefinition gemäß der veröffentlichten PQL-Grammatik.  Beispiel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ein Ausdruck, der dem in `expression.format` angegebenen Typ entspricht. |
| `description` | Eine für Menschen lesbare Beschreibung der Definition. |
| `evaluationInfo` | Ein Objekt, das angibt, welchem Typ von Auswertung, Batch, Streaming (auch als fortlaufend bezeichnet) oder Edge (auch als synchron bezeichnet) die Segmentdefinition unterzogen wird. |

+++

## Massenabruf von Segmentdefinitionen {#bulk-get}

Sie können detaillierte Informationen zu mehreren angegebenen Segmentdefinitionen abrufen, indem Sie eine POST-Anfrage an den `/segment/definitions/bulk-get`-Endpunkt senden und die `id` Werte der Segmentdefinitionen im Anfragetext angeben.

**API-Format**

```http
POST /segment/definitions/bulk-get
```

**Anfrage**

+++ Eine Beispielanfrage bei Verwendung des Massenabruf-Endpunkts.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `ids` | Ein Array, das Objekte mit den IDs der Segmentdefinitionen enthält, die Sie abrufen möchten. |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 207 mit den angeforderten Segmentdefinitionen zurückgegeben.

+++ Eine Beispielantwort bei Verwendung des Massenabruf-Endpunkts.

```json
{
    "results": {
        "54669488-03ab-4e0d-a694-37fe49e32be8": {
            "id": "54669488-03ab-4e0d-a694-37fe49e32be8",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
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
            "profileInstanceId": "ups",
            "imsOrgId": "{ORG_ID}",
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
| `id` | Eine systemgenerierte schreibgeschützte ID der Segmentdefinition. |
| `name` | Ein eindeutiger Name, mit dem auf die Segmentdefinition verwiesen werden kann. |
| `schema` | Das Schema, das mit den Entitäten im Segment verknüpft ist. Besteht entweder aus einem `id` oder aus `name` Feld. |
| `expression` | Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruckstyp an. Derzeit wird nur PQL unterstützt. |
| `expression.format` | Gibt die Struktur des Ausdrucks im Wert an. Derzeit wird das folgende Format unterstützt: <ul><li>`pql/text`: Eine textliche Darstellung einer Segmentdefinition gemäß der veröffentlichten PQL-Grammatik.  Beispiel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ein Ausdruck, der dem in `expression.format` angegebenen Typ entspricht. |
| `description` | Eine für Menschen lesbare Beschreibung der Definition. |
| `evaluationInfo` | Ein Objekt, das angibt, welchem Typ von Auswertung, Batch, Streaming (auch als fortlaufend bezeichnet) oder Edge (auch als synchron bezeichnet) die Segmentdefinition unterzogen wird. |

+++

## Löschen einer bestimmten Segmentdefinition {#delete}

DELETE Sie können das Löschen einer bestimmten Segmentdefinition anfordern, indem Sie eine Segmentanfrage an den `/segment/definitions`-Endpunkt senden und im Anfragepfad die ID der Segmentdefinition angeben, die Sie löschen möchten.

>[!NOTE]
>
> Eine Segmentdefinition, die in einer Zielaktivierung verwendet wird (**)** gelöscht werden.

**API-Format**

```http
DELETE /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SEGMENT_ID}` | Der `id` der Segmentdefinition, die Sie löschen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Löschen einer Segmentdefinition.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 ohne Meldung zurück.

## Aktualisieren einer bestimmten Segmentdefinition

Sie können eine bestimmte Segmentdefinition aktualisieren, indem Sie eine PATCH-Anfrage an den `/segment/definitions`-Endpunkt senden und im Anfragepfad die ID der Segmentdefinition angeben, die Sie aktualisieren möchten.

**API-Format**

```http
PATCH /segment/definitions/{SEGMENT_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{SEGMENT_ID}` | Der `id` der Segmentdefinition, die Sie aktualisieren möchten. |

**Anfrage**

Mit der folgenden Anfrage wird das Land der Arbeitsadresse von den USA nach Kanada aktualisiert.

>[!NOTE]
>
>Da dieser API-**den** der Segmentdefinition ersetzt, stellen Sie sicher **dass** Felder, die Sie beibehalten möchten, als Teil des Anfragetexts enthalten sind.

+++ Eine Beispielanfrage zum Aktualisieren einer Segmentdefinition.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/segment/definitions/4afe34ae-8c98-4513-8a1d-67ccaa54bc05 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu aktualisierten Segmentdefinition zurück.

+++ Eine Beispielantwort beim Aktualisieren einer Segmentdefinition.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
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

+++

## Segmentdefinition konvertieren

Sie können eine Segmentdefinition zwischen `pql/text` und `pql/json` oder `pql/json` in `pql/text` konvertieren, indem Sie eine POST-Anfrage an den `/segment/conversion`-Endpunkt senden.

**API-Format**

```http
POST /segment/conversion
```

**Anfrage**

Die folgende Anfrage ändert das Format der Segmentdefinition von `pql/text` in `pql/json`.

+++ Eine Beispielanfrage zum Konvertieren der Segmentdefinition.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        "payloadSchema": "string"
    }'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zur neu konvertierten Segmentdefinition zurückgegeben.

+++ Eine Beispielantwort beim Konvertieren der Segmentdefinition.

```json
{
    "imsOrgId": "6A29340459CA8D350A49413A@AdobeOrg",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "description": "Last 30 days",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

+++

## Nächste Schritte

Nach dem Lesen dieses Handbuchs wissen Sie jetzt besser, wie Segmentdefinitionen funktionieren. Weitere Informationen zum Erstellen eines Segments finden Sie im Tutorial [Erstellen eines Segments](../tutorials/create-a-segment.md) .
