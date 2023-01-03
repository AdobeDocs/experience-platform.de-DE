---
keywords: Experience Platform;Startseite;beliebte Themen;Richtliniendurchsetzung;Automatische Durchsetzung;API-basierte Durchsetzung;Data Governance
solution: Experience Platform
title: API-Endpunkte für die Richtlinienauswertung
topic-legacy: developer guide
description: Nachdem Marketing-Aktionen erstellt und Richtlinien definiert wurden, können Sie mit der Policy Service-API bewerten, ob Richtlinien durch bestimmte Aktionen verletzt werden. Die zurückgegebenen Beschränkungen bestehen aus einer Reihe von Richtlinien, gegen die verstoßen werden würde, wenn die Marketing-Aktion für die angegebenen Daten mit Datennutzungsbezeichnungen ausgeführt wird.
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 98%

---

# Endpunkte für die Richtlinienauswertung

Nachdem Marketing-Aktionen erstellt und Datennutzungsrichtlinien definiert wurden, können Sie die [!DNL Policy Service] API zur Bewertung, ob Richtlinien durch bestimmte Aktionen verletzt werden. Die zurückgegebenen Beschränkungen bestehen aus einer Reihe von Richtlinien, gegen die verstoßen werden würde, wenn die Marketing-Aktion für die angegebenen Daten mit Datennutzungsbezeichnungen ausgeführt wird.

Standardmäßig werden nur Richtlinien, deren Status auf `ENABLED` gesetzt ist, in die Bewertung einbezogen. Sie können jedoch den Abfrageparameter `?includeDraft=true` verwenden, um auch `DRAFT`-Richtlinien in die Auswertung einzubeziehen.

Bewertungsanfragen können auf drei Arten gestellt werden:

1. Verstößt die Aktion angesichts einer vorgegebenen Marketing-Aktion und einer Reihe von Datennutzungskennzeichnungen gegen Richtlinien?
1. Verstößt die Aktion angesichts einer vorgegebenen Marketing-Aktion und eines oder mehrerer Datensätze gegen eine Richtlinie?
1. Verstößt die Aktion angesichts einer vorgegebenen Marketing-Aktion, eines oder mehrerer Datensätze und einer Teilmenge eines oder mehrerer Felder in jedem dieser Datensätze gegen Richtlinien?

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der [[!DNL Policy Service] -API](https://www.adobe.io/experience-platform-apis/references/policy-service/). Bevor Sie fortfahren, werfen Sie im Handbuch [Erste Schritte](./getting-started.md) einen Blick auf die Informationen zu Links zu entsprechenden Dokumentationen, den Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Auswerten auf Richtlinienverletzungen mithilfe von Datennutzungskennzeichnungen {#labels}

Sie können basierend auf dem Vorhandensein eines bestimmten Satzes von Datennutzungskennzeichnungen auf Richtlinienverletzungen auswerten, indem Sie den Abfrageparameter `duleLabels` in einer GET-Anfrage verwenden.

**API-Format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketing-Aktion, die hinsichtlich einer Reihe von Datennutzungskennzeichnungen getestet werden soll. Sie können eine Liste der verfügbaren Marketing-Aktionen abrufen, indem Sie eine [GET-Anfrage an den Endpunkt der Marketing-Aktionen](./marketing-actions.md#list) stellen. |
| `{LABELS_LIST}` | Eine kommagetrennte Liste von Datennutzungskennzeichnungen, hinsichtlich derer die Marketing-Aktion getestet wird. Beispiel: `duleLabels=C1,C2,C3`<br><br>Beachten Sie, dass bei Namen der Kennzeichnungen die Groß-/Kleinschreibung eine Rolle spielt. Stellen Sie sicher, dass Sie die richtige Groß-/Kleinschreibung verwenden, wenn Sie sie im Parameter `duleLabels` auflisten. |

**Anfrage**

Die folgende Beispielanfrage bewertet eine Marketing-Aktion mit den Bezeichnungen C1 und C3.

>[!IMPORTANT]
>
>Achten Sie auf `AND`- und `OR`-Operatoren in Ihren Richtlinienausdrücken. In diesem Beispiel hätte die Marketing-Aktion nicht gegen diese Richtlinie verstoßen, wenn eine der Kennzeichnungen (`C1` bzw. `C3`) allein in der Anfrage erschienen wäre. Beide Kennzeichnungen (`C1` und `C3`) sind erforderlich, damit eine Verletzung der Richtlinie gemeldet wird. Vergewissern Sie sich, dass Sie die Richtlinien sorgfältig bewerten und die Richtlinienausdrücke mit gleicher Sorgfalt definieren.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält ein `violatedPolicies`-Array mit den Details der Richtlinien, die bei der Durchführung der Marketing-Aktion hinsichtlich der angegebenen Kennzeichnungen verletzt wurden. Wenn keine Richtlinien verletzt werden, ist das `violatedPolicies`-Array leer.

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## Auf Richtlinienverletzungen mithilfe von Datensätzen auswerten {#datasets}

Sie können auch auf Richtlinienverstöße auswerten, indem Sie die ID eines oder mehrerer Datensätze angeben, aus denen Datennutzungskennzeichnungen erfasst werden können. Dies geschieht, indem für eine bestimmte Marketing-Aktion eine POST-Anfrage an den `/constraints`-Endpunkt gestellt und eine Liste der Datensatz-IDs im Anfragetext bereitgestellt wird.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketing-Aktion, die mit einem oder mehreren Datensätzen getestet werden soll. Sie können eine Liste der verfügbaren Marketing-Aktionen abrufen, indem Sie eine [GET-Anfrage an den Endpunkt der Marketing-Aktionen](./marketing-actions.md#list) stellen. |

**Anfrage**

Die folgende Anfrage führt die Marketing-Aktion `crossSiteTargeting` für einen Satz von drei Datensätzen aus, um auf etwaige Richtlinienverletzungen auszuwerten.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityId` | Die ID eines Datensatzes, mit dem die Marketing-Aktion getestet wird. Eine Liste der Datensätze und der zugehörigen IDs können Sie erhalten, indem Sie eine GET-Anfrage an den `/dataSets`-Endpunkt in der [!DNL Catalog Service]-API stellen. Weitere Informationen finden Sie im Handbuch zum [Auflisten von [!DNL Catalog] -Objekten](../../catalog/api/list-objects.md). |

**Antwort**

Eine erfolgreiche Antwort enthält ein `violatedPolicies`-Array mit den Details der Richtlinien, die bei der Durchführung der Marketing-Aktion mit den bereitgestellten Datensätzen verletzt wurden. Wenn keine Richtlinien verletzt werden, ist das `violatedPolicies`-Array leer.

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## Auswerten auf Richtlinienverletzungen mithilfe bestimmter Datensatzfelder {#fields}

Sie können Richtlinienverletzungen anhand einer Teilmenge von Feldern aus einem oder mehreren Datensätzen auswerten, sodass nur die auf diese Felder angewendeten Datennutzungskennzeichnungen ausgewertet werden.

Beachten Sie bei der Bewertung von Richtlinien mithilfe von Datensatzfeldern Folgendes:

* **Bei den Feldnamen wird zwischen Groß- und Kleinschreibung unterschieden**: Bei der Bereitstellung von Feldern müssen sie genau so geschrieben werden, wie sie im Datensatz erscheinen (z. B. `firstName` vs. `firstname`).
* **Vererbung von Datensatzkennzeichnungen**: Einzelne Felder in einem Datensatz übernehmen alle Kennzeichnungen, die auf Datensatzebene angewendet wurden. Wenn Ihre Richtlinienauswertungen nicht die erwarteten Ergebnisse zurückgeben, stellen Sie sicher, dass Sie zusätzlich zu den auf Feldebene angewendeten Kennzeichnungen auch alle Kennzeichnungen überprüfen, die möglicherweise von der Datensatzebene in die Felder übernommen wurden.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketing-Aktion, die mit einer Teilmenge von Datensatzfeldern getestet werden soll. Sie können eine Liste der verfügbaren Marketing-Aktionen abrufen, indem Sie eine [GET-Anfrage an den Endpunkt der Marketing-Aktionen](./marketing-actions.md#list) stellen. |

**Anfrage**

Die folgende Anfrage testet die Marketing-Aktion `crossSiteTargeting` für einen bestimmten Satz von Feldern, die zu drei Datensätzen gehören. Die Payload ähnelt einer [Auswertungsanfrage, bei der nur Datensätze einbezogen werden](#datasets), wobei für jeden Datensatz spezifische Felder hinzugefügt werden, aus denen Kennzeichnungen gesammelt werden sollen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityId` | Die ID eines Datensatzes, dessen Felder mit der Marketing-Aktion ausgewertet werden sollen. Eine Liste der Datensätze und der zugehörigen IDs können Sie erhalten, indem Sie eine GET-Anfrage an den `/dataSets`-Endpunkt in der [!DNL Catalog Service]-API stellen. Weitere Informationen finden Sie im Handbuch zum [Auflisten von [!DNL Catalog] -Objekten](../../catalog/api/list-objects.md). |
| `entityMeta.fields` | Ein Array von Pfaden zu bestimmten Feldern im Schema des Datensatzes, bereitgestellt in Form von JSON-Zeigerzeichenfolgen. Einzelheiten zur für diese Zeichenfolgen gültigen Syntax finden Sie im Abschnitt [JSON-Zeiger](../../landing/api-fundamentals.md#json-pointer) im API-Grundlagenhandbuch. |

**Antwort**

Eine erfolgreiche Antwort enthält ein `violatedPolicies`-Array mit den Details der Richtlinien, die bei der Durchführung der Marketing-Aktion hinsichtlich der bereitgestellten Datensatzfelder verletzt wurden. Wenn keine Richtlinien verletzt werden, ist das `violatedPolicies`-Array leer.

Beim Vergleich der untenstehenden Beispielantwort mit der [Antwort, wenn nur Datensätze einbezogen werden](#datasets), beachten Sie, dass die Liste der gesammelten Kennzeichnungen kürzer ist. Die Werte für `discoveredLabels` für jeden Datensatz haben sich ebenfalls verringert, da sie nur die im Anfragetext angegebenen Felder enthalten. Darüber hinaus erfordert die zuvor verletzte Richtlinie `Targeting Ads or Content`, dass beide `C4 AND C6`-Kennzeichnungen vorhanden sind, und wird daher nicht mehr verletzt, wie das leere `violatedPolicies`-Array zeigt.

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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

Mit dem Endpunkt `/bulk-eval` können Sie mehrere Auswertungsaufträge in einem einzelnen API-Aufruf ausführen.

**API-Format**

```http
POST /bulk-eval
```

**Anfrage**

Die Payload einer Massenauswertungsanfrage sollte ein Array von Objekten sein, mit je einem für jeden auszuführenden Auswertungsauftrag. Für Aufträge, die basierend auf Datensätzen und Feldern ausgewertet werden, muss ein `entityList`-Array bereitgestellt werden. Für Aufträge, die anhand von Datennutzungskennzeichnungen ausgewertet werden, muss ein `labels`-Array bereitgestellt werden.

>[!WARNING]
>
>Wenn ein aufgelisteter Auswertungsauftrag sowohl ein `entityList`- als auch ein `labels`-Array enthält, wird ein Fehler ausgegeben. Wenn Sie dieselbe Marketing-Aktion auf Grundlage von sowohl Datensätzen als auch Kennzeichnungen auswerten möchten, müssen Sie für diese Marketing-Aktion separate Auswertungsaufträge einbeziehen.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `evalRef` | Der URI der Marketing-Aktion zum Testen von Kennzeichnungen oder Datensätzen auf Richtlinienverletzungen. |
| `includeDraft` | Standardmäßig werden nur aktivierte Richtlinien in die Auswertung einbezogen. Wenn `includeDraft` auf `true` eingestellt ist, werden auch Richtlinien mit dem Status `DRAFT` einbezogen. |
| `labels` | Ein Array von Datennutzungskennzeichnungen zum Testen der Marketing-Aktion.<br><br>**WICHTIG**: Bei Verwendung dieser Eigenschaft darf KEINE `entityList`-Eigenschaft im selben Objekt enthalten sein. Um dieselbe Marketing-Aktion mit Datensätzen und/oder Feldern auszuwerten, müssen Sie ein separates Objekt in die Payload der Anfrage einbeziehen, das ein `entityList`-Array enthält. |
| `entityList` | Ein Array von Datensätzen und (optional) spezifischen Feldern in diesen Datensätzen, um die Marketing-Aktion zu testen.<br><br>**WICHTIG**: Bei Verwendung dieser Eigenschaft darf KEINE `labels`-Eigenschaft im selben Objekt enthalten sein. Um dieselbe Marketing-Aktion mit bestimmten Datennutzungskennzeichnungen auszuwerten, müssen Sie ein separates Objekt in die Payload der Anfrage einbeziehen, das ein `labels`-Array enthält. |
| `entityType` | Der Typ der Entität, gegen die die Marketing-Aktion getestet werden soll. Derzeit wird nur `dataSet` unterstützt. |
| `entityId` | Die ID eines Datensatzes, mit dem die Marketing-Aktion getestet wird. |
| `entityMeta.fields` | (Optional) Eine Liste bestimmter Felder im Datensatz, um die Marketing-Aktion zu testen. |

**Antwort**

Eine erfolgreiche Antwort gibt eine Reihe von Auswertungsergebnissen zurück. Eines für jeden Richtlinienauswertungsauftrag, der in der Anfrage gesendet wird.

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
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
      "imsOrg": "{ORG_ID}",
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
          "imsOrg": "{ORG_ID}",
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

## Richtlinienauswertung für [!DNL Real-Time Customer Profile]

Die [!DNL Policy Service]-API kann auch verwendet werden, um nach Richtlinienverstößen zu suchen, bei denen [!DNL Real-Time Customer Profile]-Segmente verwendet werden. Weiterführende Informationen finden Sie im Tutorial zum [Durchsetzen der Datennutzungskonformität für Zielgruppensegmente](../../segmentation/tutorials/governance.md).
