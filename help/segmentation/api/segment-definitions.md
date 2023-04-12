---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; Segmentdefinition; Segmentdefinitionen; API; API;
solution: Experience Platform
title: API-Endpunkt für Segmentdefinitionen
description: Der Endpunkt "Segmentdefinitionen"in der Adobe Experience Platform Segmentation Service-API ermöglicht Ihnen die programmgesteuerte Verwaltung von Segmentdefinitionen für Ihr Unternehmen.
exl-id: e7811b96-32bf-4b28-9abb-74c17a71ffab
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1258'
ht-degree: 25%

---

# Endpunkt der Segmentdefinitionen

Mit Adobe Experience Platform können Sie Segmente erstellen, die eine Gruppe spezifischer Attribute oder Verhaltensweisen aus einer Gruppe von Profilen definieren. Eine Segmentdefinition ist ein Objekt, das eine Abfrage enthält, die in [!DNL Profile Query Language] (PQL). Dieses Objekt wird auch als PQL-Prädikat bezeichnet. PQL-Prädikate definieren die Regeln für das Segment basierend auf Bedingungen, die sich auf Datensatz- oder Zeitreihendaten beziehen, die Sie für [!DNL Real-Time Customer Profile]. Siehe [PQL-Handbuch](../pql/overview.md) für weitere Informationen zum Schreiben von PQL-Abfragen.

Dieses Handbuch enthält Informationen zum besseren Verständnis von Segmentdefinitionen und enthält Beispiel-API-Aufrufe zum Ausführen grundlegender Aktionen mit der API.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [!DNL Adobe Experience Platform Segmentation Service]-. Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Informationen zum Lesen von Beispiel-API-Aufrufen.

## Abrufen einer Liste von Segmentdefinitionen {#list}

Sie können eine Liste aller Segmentdefinitionen für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an die `/segment/definitions` -Endpunkt.

**API-Format**

Der `/segment/definitions`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Diese Parameter sind zwar optional, doch wird ihre Verwendung dringend empfohlen, um den teuren Verwaltungsaufwand zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihr Unternehmen verfügbaren Segmentdefinitionen abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /segment/definitions
GET /segment/definitions?{QUERY_PARAMETERS}
```

**Abfrageparameter**

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `start` | Gibt den Startversatz für die zurückgegebenen Segmentdefinitionen an. | `start=4` |
| `limit` | Gibt die Anzahl der pro Seite zurückgegebenen Segmentdefinitionen an. | `limit=20` |
| `page` | Gibt an, auf welcher Seite die Ergebnisse der Segmentdefinitionen beginnen. | `page=5` |
| `sort` | Gibt an, nach welchem Feld die Ergebnisse sortiert werden sollen. ist im folgenden Format geschrieben: `[attributeName]:[desc|asc]`. | `sort=updateTime:desc` |
| `evaluationInfo.continuous.enabled` | Gibt an, ob die Segmentdefinition Streaming-fähig ist. | `evaluationInfo.continuous.enabled=true` |

**Anfrage**

Mit der folgenden Anfrage werden die letzten beiden Segmentdefinitionen abgerufen, die innerhalb Ihres Unternehmens veröffentlicht wurden.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/definitions?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste von Segmentdefinitionen für die angegebene Organisation als JSON zurück.

```json
{
    "segments": [
        {
            "id": "3da8bad9-29fb-40e0-b39e-f80322e964de",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
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
            "ttlInDays": 30,
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
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | **Erforderlich.** Ein eindeutiger Name, mit dem auf das Segment verwiesen wird. |
| `description` | Eine Beschreibung der Segmentdefinition, die Sie erstellen. |
| `evaluationInfo` | Der Typ des Segments, das Sie erstellen. Wenn Sie ein Batch-Segment erstellen möchten, legen Sie `evaluationInfo.batch.enabled` auf wahr zu sein. Wenn Sie ein Streaming-Segment erstellen möchten, legen Sie `evaluationInfo.continuous.enabled` auf wahr zu sein. Wenn Sie ein Kantensegment erstellen möchten, legen Sie `evaluationInfo.synchronous.enabled` auf wahr zu sein. Wenn das Segment leer gelassen wird, wird es als **Batch** Segment. |
| `schema` | **Erforderlich.** Das mit den Entitäten im Segment verknüpfte Schema. Besteht aus einer der beiden `id` oder `name` -Feld. |
| `expression` | **Erforderlich.** Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruckstyp an. Derzeit wird nur &quot;PQL&quot;unterstützt. |
| `expression.format` | Gibt die Struktur des Ausdrucks in Wert an. Derzeit wird das folgende Format unterstützt: <ul><li>`pql/text`: Eine Textdarstellung einer Segmentdefinition gemäß der veröffentlichten PQL-Grammatik.  Beispiel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ein Ausdruck, der dem in `expression.format`. |
| `description` | Eine für Menschen lesbare Beschreibung der Definition. |

>[!NOTE]
>
>Ein Segmentdefinitionsausdruck kann auch auf ein berechnetes Attribut verweisen. Weitere Informationen finden Sie im Abschnitt [Handbuch zum API-Endpunkt für berechnete Attribute](../../profile/computed-attributes/ca-api.md)
>
>Die Funktion für berechnete Attribute ist alphanumerisch und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

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
| `evaluationInfo` | Ein Objekt, das angibt, welcher Evaluierungstyp für die Segmentdefinition durchgeführt wird. Dabei kann es sich um Batch-, Streaming- (auch als fortlaufend bezeichnet) oder Edge-Segmentierung (auch als synchrone Segmentierung bezeichnet) handeln. |

## Abrufen einer bestimmten Segmentdefinition {#get}

Sie können detaillierte Informationen zu einer bestimmten Segmentdefinition abrufen, indem Sie eine GET-Anfrage an die `/segment/definitions` -Endpunkt und geben Sie die Kennung der Segmentdefinition an, die Sie im Anfragepfad abrufen möchten.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `id` | Eine vom System generierte schreibgeschützte ID der Segmentdefinition. |
| `name` | Ein eindeutiger Name, mit dem auf das Segment verwiesen wird. |
| `schema` | Das mit den Entitäten im Segment verknüpfte Schema. Besteht aus einer der beiden `id` oder `name` -Feld. |
| `expression` | Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruckstyp an. Derzeit wird nur &quot;PQL&quot;unterstützt. |
| `expression.format` | Gibt die Struktur des Ausdrucks in Wert an. Derzeit wird das folgende Format unterstützt: <ul><li>`pql/text`: Eine Textdarstellung einer Segmentdefinition gemäß der veröffentlichten PQL-Grammatik.  Beispiel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ein Ausdruck, der dem in `expression.format`. |
| `description` | Eine für Menschen lesbare Beschreibung der Definition. |
| `evaluationInfo` | Ein Objekt, das angibt, welcher Typ von Auswertung, Batch, Streaming (auch als kontinuierlich bezeichnet) oder Edge (auch als synchron bezeichnet) die Segmentdefinition durchlaufen wird. |

## Massenabruf von Segmentdefinitionen {#bulk-get}

Sie können detaillierte Informationen über mehrere angegebene Segmentdefinitionen abrufen, indem Sie eine POST-Anfrage an die `/segment/definitions/bulk-get` Endpunkt und Bereitstellung der `id` -Werte der Segmentdefinitionen im Anfragetext.

**API-Format**

```http
POST /segment/definitions/bulk-get
```

**Anfrage**

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

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 207 mit den angeforderten Segmentdefinitionen zurück.

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
            "ttlInDays": 60,
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
| `id` | Eine vom System generierte schreibgeschützte ID der Segmentdefinition. |
| `name` | Ein eindeutiger Name, mit dem auf das Segment verwiesen wird. |
| `schema` | Das mit den Entitäten im Segment verknüpfte Schema. Besteht aus einer der beiden `id` oder `name` -Feld. |
| `expression` | Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruckstyp an. Derzeit wird nur &quot;PQL&quot;unterstützt. |
| `expression.format` | Gibt die Struktur des Ausdrucks in Wert an. Derzeit wird das folgende Format unterstützt: <ul><li>`pql/text`: Eine Textdarstellung einer Segmentdefinition gemäß der veröffentlichten PQL-Grammatik.  Beispiel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ein Ausdruck, der dem in `expression.format`. |
| `description` | Eine für Menschen lesbare Beschreibung der Definition. |
| `evaluationInfo` | Ein Objekt, das angibt, welcher Typ von Auswertung, Batch, Streaming (auch als kontinuierlich bezeichnet) oder Edge (auch als synchron bezeichnet) die Segmentdefinition durchlaufen wird. |

## Löschen einer bestimmten Segmentdefinition {#delete}

Sie können das Löschen einer bestimmten Segmentdefinition anfordern, indem Sie eine DELETE-Anfrage an die `/segment/definitions` -Endpunkt und geben Sie die Kennung der Segmentdefinition an, die Sie im Anfragepfad löschen möchten.

>[!NOTE]
>
> Sie können ein Segment, das in einer Zielaktivierung verwendet wird, **nicht** löschen.

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
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 ohne Meldung zurück.

## Aktualisieren einer bestimmten Segmentdefinition

Sie können eine bestimmte Segmentdefinition aktualisieren, indem Sie eine PATCH-Anfrage an die `/segment/definitions` -Endpunkt und die Kennung der Segmentdefinition angeben, die Sie im Anfragepfad aktualisieren möchten.

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
    "ttlInDays": 60,
    "creationTime": 0,
    "updateTime": 0,
    "updateEpoch": 0
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu aktualisierten Segmentdefinition zurück. Beachten Sie, dass das Land der Arbeitsadresse von den USA (USA) nach Kanada (CA) aktualisiert wurde.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
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

## Segmentdefinition konvertieren

Sie können eine Segmentdefinition konvertieren zwischen `pql/text` und `pql/json` oder `pql/json` nach `pql/text` , indem Sie eine POST an die `/segment/conversion` -Endpunkt.

**API-Format**

```http
POST /segment/conversion
```

**Anfrage**

Die folgende Anfrage ändert das Format der Segmentdefinition von `pql/text` nach `pql/json`.

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
        "payloadSchema": "string",
        "ttlInDays": 60
    }'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu konvertierten Segmentdefinition zurück.

```json
{
    "ttlInDays": 60,
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

## Nächste Schritte

Nach dem Lesen dieses Handbuchs haben Sie jetzt ein besseres Verständnis davon, wie Segmentdefinitionen funktionieren. Weitere Informationen zum Erstellen eines Segments finden Sie im Abschnitt [Erstellen eines Segments](../tutorials/create-a-segment.md) Tutorial.
