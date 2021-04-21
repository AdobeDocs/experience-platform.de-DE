---
keywords: Experience Platform;Home;beliebte Themen;Richtliniendurchsetzung;Automatische Durchsetzung;API-basierte Durchsetzung;Datenverwaltung
solution: Experience Platform
title: API-Endpunkte für Richtlinienbewertung
topic-legacy: developer guide
description: Nachdem Marketing-Aktionen erstellt und Richtlinien definiert wurden, können Sie mit der Policy Service-API bewerten, ob Richtlinien durch bestimmte Aktionen verletzt werden. Die zurückgegebenen Beschränkungen bestehen aus einer Reihe von Richtlinien, gegen die verstoßen werden würde, wenn die Marketing-Aktion für die angegebenen Daten mit Datennutzungsbezeichnungen ausgeführt wird.
exl-id: f9903939-268b-492c-aca7-63200bfe4179
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 16%

---

# Endpunkte für die Politikbewertung

Nachdem Marketingaktionen erstellt und Richtlinien definiert wurden, können Sie mit der API [!DNL Policy Service] bewerten, ob Richtlinien durch bestimmte Aktionen verletzt werden. Die zurückgegebenen Beschränkungen bestehen aus einer Reihe von Richtlinien, gegen die verstoßen werden würde, wenn die Marketing-Aktion für die angegebenen Daten mit Datennutzungsbezeichnungen ausgeführt wird.

Standardmäßig nehmen nur Richtlinien, deren Status auf `ENABLED` festgelegt ist, an der Evaluierung teil. Sie können jedoch den Parameter &quot;Abfrage&quot;`?includeDraft=true` verwenden, um `DRAFT`-Richtlinien in die Evaluierung einzubeziehen.

Bewertungsanfragen können auf drei Arten gestellt werden:

1. Verstößt die Aktion angesichts einer Marketingaktion und einer Reihe von Beschreibungen zur Datenverwendung gegen Richtlinien?
1. Verstößt die Aktion angesichts einer Marketingaktion und eines oder mehrerer Datensätze gegen eine Richtlinie?
1. Verstößt die Aktion angesichts einer Marketingaktion, eines oder mehrerer Datensätze und einer Untergruppe von einem oder mehreren Feldern innerhalb jedes dieser Datensätze gegen eine Richtlinie?

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Auf Richtlinienverletzungen mithilfe von Datenverwendungsbezeichnungen {#labels} bewerten

Sie können anhand des Parameters `duleLabels` &quot;Abfrage&quot;in einer GET-Anforderung auswerten, ob eine Richtlinie verletzt wurde.

**API-Format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion, die mit einer Reihe von Beschriftungen für die Datenverwendung getestet werden soll. Sie können eine Liste der verfügbaren Marketingaktionen abrufen, indem Sie eine [GET an den Endpunkt der Marketingaktionen](./marketing-actions.md#list) anfordern. |
| `{LABELS_LIST}` | Eine kommagetrennte Liste von Datenverwendungsbezeichnungen, mit denen die Marketingaktion getestet wird. Beispiel: `duleLabels=C1,C2,C3`<br><br>Beachten Sie, dass bei Beschriftungsnamen die Groß-/Kleinschreibung beachtet wird. Stellen Sie sicher, dass Sie die richtige Groß-/Kleinschreibung verwenden, wenn Sie sie im Parameter `duleLabels` auflisten. |

**Anfrage**

Die folgende Beispielanfrage bewertet eine Marketing-Aktion mit den Bezeichnungen C1 und C3.

>[!IMPORTANT]
>
>Achten Sie auf `AND`- und `OR`-Operatoren in Ihren Richtlinienausdrücken. Wenn im Beispiel unten eine Beschriftung (`C1` oder `C3`) in der Anforderung allein erschienen wäre, hätte die Marketingaktion diese Richtlinie nicht verletzt. Es erfordert beide Bezeichnungen (`C1` und `C3`), um die verletzte Richtlinie zurückzugeben. Vergewissern Sie sich, dass Sie die Richtlinien sorgfältig bewerten und die Richtlinienausdrücke mit gleicher Sorgfalt definieren.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält ein Array mit den Details der Richtlinien, die bei der Durchführung der Marketingaktion gegen die angegebenen Beschriftungen verletzt wurden. `violatedPolicies` Wenn keine Richtlinien verletzt werden, ist das `violatedPolicies`-Array leer.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

## Auf Richtlinienverletzungen mithilfe von Datasets {#datasets} bewerten

Sie können anhand eines oder mehrerer Datensätze, aus denen Datenverwendungsbeschriftungen erfasst werden können, eine Bewertung auf Richtlinienverletzungen vornehmen. Dies geschieht, indem eine POST an den `/constraints`-Endpunkt für eine bestimmte Marketingaktion angefordert und eine Liste der DataSet-IDs im Anforderungstext bereitgestellt wird.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion, die mit einem oder mehreren Datensätzen getestet werden soll. Sie können eine Liste der verfügbaren Marketingaktionen abrufen, indem Sie eine [GET an den Endpunkt der Marketingaktionen](./marketing-actions.md#list) anfordern. |

**Anfrage**

Die folgende Anforderung führt die Marketingaktion `crossSiteTargeting` für einen Satz von drei Datensätzen aus, um etwaige Richtlinienverletzungen zu bewerten.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f"
        }
      ]'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `entityType` | Der Typ der Entität, deren ID in der nebengeordneten `entityId`-Eigenschaft angegeben ist. Derzeit ist der einzige akzeptierte Wert `dataSet`. |
| `entityId` | Die ID eines Datensatzes, mit dem die Marketingaktion getestet wird. Eine Liste der Datensätze und der zugehörigen IDs können Sie erhalten, indem Sie eine GET an den `/dataSets`-Endpunkt in der [!DNL Catalog Service]-API anfordern. Weitere Informationen finden Sie im Handbuch [listing [!DNL Catalog] object](../../catalog/api/list-objects.md). |

**Antwort**

Eine erfolgreiche Antwort enthält ein Array mit den Details der Richtlinien, die bei der Durchführung der Marketingaktion gegen die bereitgestellten Datensätze verletzt wurden. `violatedPolicies` Wenn keine Richtlinien verletzt werden, ist das `violatedPolicies`-Array leer.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C1",
        "C2",
        "C4",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C1"
                        ],
                        "path": "/properties/identityMap"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `duleLabels` | Das Antwortobjekt enthält ein `duleLabels`-Array, das eine konsolidierte Liste aller in den angegebenen Datensätzen gefundenen Bezeichnungen enthält. Diese Liste enthält Bezeichnungen auf Datensatz- und Feldebene für alle Felder im Datensatz. |
| `discoveredLabels` | Die Antwort enthält außerdem ein `discoveredLabels`-Array mit Objekten für jeden Datensatz, in dem die `datasetLabels` in Bezeichnungen auf Datensatz- und Feldebene unterteilt sind. Jede Bezeichnung auf Feldebene zeigt den Pfad zum jeweiligen Feld mit dieser Bezeichnung. |

## Auf Richtlinienverletzungen mithilfe bestimmter Datensatzfelder {#fields} bewerten

Sie können Richtlinienverletzungen anhand einer Untergruppe von Feldern aus einem oder mehreren Datensätzen auswerten, sodass nur die auf diese Felder angewendeten Datenverwendungsbeschriftungen ausgewertet werden.

Beachten Sie bei der Bewertung von Richtlinien mithilfe von Datensatzfeldern Folgendes:

* **Bei Feldnamen wird zwischen Groß- und Kleinschreibung unterschieden**: Bei der Bereitstellung von Feldern müssen sie genau so geschrieben werden, wie sie im Datensatz angezeigt werden (z. B.  `firstName` vs  `firstname`).
* **Vererbung** der Datenbeschriftung: Einzelne Felder in einem Datensatz übernehmen alle Bezeichnungen, die auf Datensatzebene angewendet wurden. Wenn Ihre Richtlinienbewertungen nicht erwartungsgemäß zurückgegeben werden, überprüfen Sie, ob Sie zusätzlich zu den auf Feldebene angewendeten Beschriftungen auch Beschriftungen finden, die möglicherweise von der Datensatzebene bis zu den Feldern geerbt wurden.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion, die mit einer Untergruppe von Datenfeldern getestet werden soll. Sie können eine Liste der verfügbaren Marketingaktionen abrufen, indem Sie eine [GET an den Endpunkt der Marketingaktionen](./marketing-actions.md#list) anfordern. |

**Anfrage**

Die folgende Anforderung testet die Marketingaktion `crossSiteTargeting` auf einem bestimmten Satz von Feldern, die zu drei Datensätzen gehören. Die Nutzlast ähnelt einer [Bewertungsanfrage, bei der nur Datensätze](#datasets) einbezogen werden, wobei für jeden Datensatz spezifische Felder hinzugefügt werden, aus denen Beschriftungen gesammelt werden sollen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `entityType` | Der Typ der Entität, deren ID in der nebengeordneten `entityId`-Eigenschaft angegeben ist. Derzeit ist der einzige akzeptierte Wert `dataSet`. |
| `entityId` | Die ID eines Datensatzes, dessen Felder mit der Marketingaktion ausgewertet werden sollen. Eine Liste der Datensätze und der zugehörigen IDs können Sie erhalten, indem Sie eine GET an den `/dataSets`-Endpunkt in der [!DNL Catalog Service]-API anfordern. Weitere Informationen finden Sie im Handbuch [listing [!DNL Catalog] object](../../catalog/api/list-objects.md). |
| `entityMeta.fields` | Ein Array von Pfaden zu bestimmten Feldern im Schema des Datensatzes, bereitgestellt in Form von JSON-Zeigerzeichenfolgen. Einzelheiten zur für diese Zeichenfolgen verwendeten Syntax finden Sie im Abschnitt zu [JSON-Zeiger](../../landing/api-fundamentals.md#json-pointer) im API-Grundlagenhandbuch. |

**Antwort**

Eine erfolgreiche Antwort enthält ein Array mit den Details der Richtlinien, die bei der Durchführung der Marketingaktion gegen die bereitgestellten Datensatzfelder verletzt wurden. `violatedPolicies` Wenn keine Richtlinien verletzt werden, ist das `violatedPolicies`-Array leer.

Beim Vergleich der unten stehenden Beispielantwort mit der Antwort [nur mit Datensätzen](#datasets) beachten Sie, dass die Liste der erfassten Beschriftungen kürzer ist. Die Werte für `discoveredLabels` für jeden Datensatz wurden ebenfalls verringert, da sie nur die im Anforderungstext angegebenen Felder enthalten. Darüber hinaus erfordert die zuvor verletzte Richtlinie `Targeting Ads or Content`, dass beide Beschriftungen `C4 AND C6` vorhanden sind, und wird daher nicht mehr verletzt, wie durch das leere `violatedPolicies`-Array angegeben.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## Richtlinien stapelweise auswerten {#bulk}

Mit dem Endpunkt `/bulk-eval` können Sie mehrere Evaluierungsaufträge in einem einzelnen API-Aufruf ausführen.

**API-Format**

```http
POST /bulk-eval
```

**Anfrage**

Die Nutzlast einer Massenauswertungsanforderung sollte ein Array von Objekten sein; einen für jeden auszuführenden Bewertungsauftrag. Für Aufträge, die basierend auf Datensätzen und Feldern ausgewertet werden, muss ein `entityList`-Array bereitgestellt werden. Für Aufträge, die anhand von Datenverwendungsbeschriftungen ausgewertet werden, muss ein `labels`-Array bereitgestellt werden.

>[!WARNING]
>
>Wenn ein aufgelisteter Bewertungsauftrag sowohl ein `entityList`- als auch ein `labels`-Array enthält, wird ein Fehler ausgegeben. Wenn Sie dieselbe Marketingaktion auf Grundlage von Datensätzen und Etiketten bewerten möchten, müssen Sie für diese Marketingaktion separate Bewertungsaufträge einbeziehen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `evalRef` | Der URI der Marketingaktion zum Testen von Beschriftungen oder Datensätzen auf Richtlinienverletzungen. |
| `includeDraft` | Standardmäßig werden nur aktivierte Richtlinien an der Auswertung beteiligt. Wenn `includeDraft` auf `true` eingestellt ist, werden auch Richtlinien mit dem Status `DRAFT` teilgenommen. |
| `labels` | Ein Array von Datenverwendungsbeschriftungen zum Testen der Marketingaktion.<br><br>**WICHTIG**: Bei Verwendung dieser Eigenschaft darf eine  `entityList` Eigenschaft NICHT im selben Objekt enthalten sein. Um dieselbe Marketingaktion mit Datensätzen und/oder Feldern auszuwerten, müssen Sie ein separates Objekt in die Anforderungsnutzlast einbeziehen, das ein `entityList`-Array enthält. |
| `entityList` | Ein Array von Datensätzen und (optional) spezifischen Feldern in diesen Datensätzen, um die Marketingaktion zu testen.<br><br>**WICHTIG**: Bei Verwendung dieser Eigenschaft darf eine  `labels` Eigenschaft NICHT im selben Objekt enthalten sein. Um dieselbe Marketingaktion mit bestimmten Datenverwendungsbeschriftungen auszuwerten, müssen Sie ein separates Objekt in die Anforderungsnutzlast einbeziehen, das ein `labels`-Array enthält. |
| `entityType` | Der Typ der Entität, gegen die die Marketingaktion getestet werden soll. Derzeit wird nur `dataSet` unterstützt. |
| `entityId` | Die ID eines Datensatzes, mit dem die Marketingaktion getestet wird. |
| `entityMeta.fields` | (Optional) Eine Liste bestimmter Felder im Datensatz, um die Marketingaktion zu testen. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Reihe von Bewertungsergebnissen zurück. einen für jeden Richtlinienbewertungsauftrag, der in der Anforderung gesendet wird.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{IMS_ORG}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## Richtlinienbewertung für [!DNL Real-time Customer Profile]

Die [!DNL Policy Service]-API kann auch verwendet werden, um Richtlinienverletzungen zu überprüfen, die die Verwendung von [!DNL Real-time Customer Profile]-Segmenten beinhalten. Weiterführende Informationen finden Sie im Tutorial zum [Durchsetzen der Datennutzungskonformität für Zielgruppensegmente](../../segmentation/tutorials/governance.md).
