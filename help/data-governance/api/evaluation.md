---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Richtlinien
topic: developer guide
translation-type: tm+mt
source-git-commit: 2997243622a7483ae23e21487128cea6badecb80
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 2%

---


# Politikbewertung

Nachdem Marketingaktionen erstellt und Richtlinien definiert wurden, können Sie mit der Policy Service API bewerten, ob Richtlinien durch bestimmte Aktionen verletzt werden. Die zurückgegebenen Beschränkungen haben die Form eines Richtliniensatzes, der durch den Versuch der Marketingaktion für die angegebenen Daten, die Datenverwendungsbeschriftungen enthalten, verletzt wird.

Standardmäßig nehmen **nur Richtlinien, deren Status auf &quot;AKTIVIERT&quot;festgelegt ist, an der Evaluierung** teil. Sie können jedoch den Parameter &quot;Abfrage&quot;verwenden, um Richtlinien des Typs &quot;ENTWURF&quot;in die Evaluierung `?includeDraft=true` einzubeziehen.

Die Evaluierungsanträge können auf drei Arten gestellt werden:

1. Verstößt die Aktion in Anbetracht einer Reihe von Beschreibungen zur Datenverwendung und einer Marketingaktion gegen Richtlinien?
1. Verstößt die Aktion in Anbetracht eines oder mehrerer Datensätze und einer Marketingaktion gegen eine Richtlinie?
1. Verstößt die Aktion in Anbetracht eines oder mehrerer Datensätze und einer Untergruppe von einem oder mehreren Feldern innerhalb jedes dieser Datensätze gegen irgendeine Richtlinie?

## Richtlinien mithilfe von Datenverwendungsbeschriftungen und einer Marketingaktion bewerten

Zur Bewertung von Richtlinienverstößen auf der Grundlage von Datenverwendungsbeschriftungen müssen Sie die Beschriftungen angeben, die während der Anforderung auf den Daten vorhanden sein sollen. Dies geschieht mithilfe von Abfrage-Parametern, bei denen Datenverwendungsbeschriftungen als kommagetrennte Liste von Werten bereitgestellt werden, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**Anfrage**

Die folgende Beispielanforderung bewertet eine Marketingaktion mit den Beschriftungen C1 und C3. Beachten Sie bei der Bewertung von Richtlinien mithilfe von Datenverwendungsbeschriftungen Folgendes:
* **Bei den Beschriftungen für die Datenverwendung wird zwischen Groß- und Kleinschreibung unterschieden.** Die oben dargestellte Anforderung gibt eine verletzte Richtlinie zurück, während die gleiche Anforderung mit Kleinbuchstaben (z. `"c1,c3"`, `"C1,c3"`, `"c1,C3"`) nicht.
* **Achten Sie auf die`AND`und`OR`Operatoren in Ihren Policy-Ausdrücken.** Wenn in diesem Beispiel eine Beschriftung (`C1` oder `C3`) in der Anfrage allein erschienen wäre, hätte die Marketingaktion diese Richtlinie nicht verletzt. Es erfordert beide Bezeichnungen (`C1 AND C3`), um die verletzte Richtlinie zurückzugeben. Vergewissern Sie sich, dass Sie die Richtlinien sorgfältig bewerten und politische Ausdruck mit gleicher Sorgfalt definieren.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Das Antwortobjekt enthält ein `duleLabels` Array, das mit den in der Anforderung gesendeten Beschriftungen übereinstimmen sollte. Wenn die Durchführung der angegebenen Marketingaktion gegen die Datenverwendungsbeschriftungen eine Richtlinie verletzt, enthält das `violatedPolicies` Array die Details der betroffenen Richtlinie (oder Richtlinien). Wenn keine Richtlinien verletzt werden, wird das `violatedPolicies` Array leer angezeigt (`[]`).

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

## Richtlinien mithilfe von Datensätzen und einer Marketingaktion bewerten

Sie können auch Richtlinienverletzungen bewerten, indem Sie die ID eines oder mehrerer Datensätze angeben, aus denen Datenverwendungsbeschriftungen erfasst werden können. Dies geschieht, indem eine POST-Anforderung entweder an den Kern- oder benutzerdefinierten `/constraints` Endpunkt für eine Marketingaktion ausgeführt und die DataSet-IDs im Anforderungstext angegeben werden, wie unten dargestellt.

**API-Format**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Anfrage**

Der Anforderungstext enthält ein Array mit einem Objekt für jede DataSet-ID. Da Sie einen Anforderungstext senden, wird der &quot;Content-Type: &quot;application/json&quot;-Anforderungsheader erforderlich ist, wie im folgenden Beispiel gezeigt.

```SHELL
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

**Antwort**

Das Antwortobjekt enthält ein `duleLabels` Array, das eine konsolidierte Liste aller in den angegebenen Datensätzen gefundenen Beschriftungen enthält. Diese Liste enthält Beschriftungen auf Datensatzebene und Feldebene für alle Felder im Datensatz.

Die Antwort enthält außerdem ein `discoveredLabels` Array, das Objekte für jeden Datensatz enthält und in Beschriftungen auf Dataset- und Feldebene `datasetLabels` unterteilt ist. Jede Beschriftung auf Feldebene zeigt den Pfad zum jeweiligen Feld mit dieser Beschriftung.

Wenn die angegebene Marketingaktion gegen eine Richtlinie verstößt, die die `duleLabels` in den Datensätzen enthaltenen Informationen enthält, enthält das `violatedPolicies` Array die Details der betreffenden Richtlinie (oder Richtlinien). Wenn keine Richtlinien verletzt werden, wird das `violatedPolicies` Array leer angezeigt (`[]`).

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

## Richtlinien mithilfe von Datensätzen, Feldern und einer Marketingaktion bewerten

Neben der Bereitstellung einer oder mehrerer DataSet-IDs kann auch eine Untergruppe von Feldern aus jedem Datensatz angegeben werden, die angibt, dass nur die Datenverwendungsbeschriftungen in diesen Feldern ausgewertet werden sollten. Ähnlich wie bei der POST-Anforderung, die nur Datensätze umfasst, fügt diese Anforderung dem Anforderungstext spezifische Felder für jeden Datensatz hinzu.

Berücksichtigen Sie bei der Bewertung von Richtlinien mithilfe von DataSet-Feldern Folgendes:

* **Bei Feldnamen wird zwischen Groß- und Kleinschreibung unterschieden.** Bei der Bereitstellung von Feldern müssen sie genau so geschrieben werden, wie sie im Datensatz angezeigt werden (z. B. `firstName` vs `firstname`).
* **Vererbung der Datenbeschriftung.** Datenverwendungsbeschriftungen können auf mehreren Ebenen angewendet werden und werden nach unten übernommen. Wenn Ihre Richtlinienbewertungen nicht so zurückgegeben werden, wie Sie dachten, sollten Sie die geerbten Beschriftungen von Datensätzen bis zu den Feldern überprüfen, die auf Feldebene angewendet werden.

**API-Format**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Anfrage**

Der Anforderungstext enthält ein Array mit einem Objekt für jede Datensatzkennung und die Untergruppe der Felder in diesem Datensatz, die für die Auswertung verwendet werden sollen. Da Sie einen Anforderungstext senden, wird der &quot;Content-Type: &quot;application/json&quot;-Anforderungsheader erforderlich ist, wie im folgenden Beispiel gezeigt.

```SHELL
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

**Antwort**

Das Antwortobjekt enthält ein `duleLabels` Array, das die konsolidierte Liste der Beschriftungen in den angegebenen Feldern enthält. Denken Sie daran, dass dies auch Datenbezeichnungen enthält, da sie in Felder vererbt werden.

Wenn eine Richtlinie durch die Durchführung der angegebenen Marketingaktion für die Daten in den bereitgestellten Feldern verletzt wird, enthält das `violatedPolicies` Array die Details der betreffenden Richtlinie (oder Richtlinien). Wenn keine Richtlinien verletzt werden, wird das `violatedPolicies` Array leer angezeigt (`[]`).

In der folgenden Antwort sehen Sie, dass die Liste von jetzt kürzer `duleLabels` ist, ebenso wie die für jeden Datensatz, da sie nur die im Anforderungstext angegebenen Felder enthält `discoveredLabels` . Sie werden auch feststellen, dass die zuvor verletzte Richtlinie &quot;Targeting-Anzeigen oder Inhalte&quot;beide `C4 AND C6` Bezeichnungen erfordert hat, sodass sie nicht mehr verletzt werden und das `violatedPolicies` Array leer erscheint.

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

## Richtlinienbewertung für Echtzeit-Profil von Kunden

Die Policy-Service-API kann auch verwendet werden, um Richtlinienverletzungen zu überprüfen, die die Verwendung von Echtzeit-Kundensegmenten beinhalten. Weiterführende Informationen finden Sie im Tutorial zum [Erzwingen der Einhaltung von Datennutzungsrichtlinien für Zielgruppensegmente](../../segmentation/tutorials/governance.md).