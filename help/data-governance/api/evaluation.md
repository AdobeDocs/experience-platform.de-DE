---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Richtlinien
topic: developer guide
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 95%

---


# Bewertung von Richtlinien

Once marketing actions have been created and policies have been defined, you can use the [!DNL Policy Service] API to evaluate if any policies are violated by certain actions. Die zurückgegebenen Beschränkungen bestehen aus einer Reihe von Richtlinien, gegen die verstoßen werden würde, wenn die Marketing-Aktion für die angegebenen Daten mit Datennutzungsbezeichnungen ausgeführt wird.

Standardmäßig nehmen **nur Richtlinien an der Bewertung teil, deren Status auf „AKTIVIERT“ gesetzt ist**. Sie können jedoch den Abfrageparameter `?includeDraft=true` verwenden, um „ENTWURF“-Richtlinien in die Bewertung einzubeziehen.

Bewertungsanfragen können auf drei Arten gestellt werden:

1. Verstößt die Aktion bei einer Reihe von Datennutzungsbezeichnungen und einer Marketing-Aktion gegen irgendwelche Richtlinien?
1. Verstößt die Aktion bei einem oder mehreren Datensätzen und einer Marketing-Aktion gegen irgendwelche Richtlinien?
1. Verstößt die Aktion bei einem oder mehreren Datensätzen und einer Teilmenge eines oder mehrerer Felder in jedem dieser Datensätze gegen Richtlinien?

## Bewerten von Richtlinien mithilfe von Datennutzungsbezeichnungen und einer Marketing-Aktion

Zur Bewertung von Richtlinienverstößen auf der Grundlage von vorhandenen Datennutzungsbezeichnungen müssen Sie die Bezeichnungen angeben, die während der Anfrage vorhanden sein sollen. Dies geschieht mithilfe von Abfrageparametern, bei denen Datennutzungsbezeichnungen als kommagetrennte Liste von Werten bereitgestellt werden, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**Anfrage**

Die folgende Beispielanfrage bewertet eine Marketing-Aktion mit den Bezeichnungen C1 und C3. Beachten Sie bei der Bewertung von Richtlinien mithilfe von Datennutzungsbezeichnungen Folgendes:
* **Bei den Datennutzungsbezeichnungen wird zwischen Groß- und Kleinschreibung unterschieden.** Die oben dargestellte Anfrage gibt eine verletzte Richtlinie zurück, während die gleiche Anfrage mit Kleinbuchstaben (z. B. `"c1,c3"`, `"C1,c3"`, `"c1,C3"`) dies nicht tut.
* **Achten Sie auf`AND`- und`OR`-Operatoren in Ihren Richtlinienausdrücken.** In diesem Beispiel hätte die Marketing-Aktion nicht gegen diese Richtlinie verstoßen, wenn eine der Bezeichnungen (`C1` oder `C3`) in der Anfrage allein erschienen wäre. Es sind beide Bezeichnungen (`C1 AND C3`) erforderlich, um die verletzte Richtlinie zurückzugeben. Vergewissern Sie sich, dass Sie die Richtlinien sorgfältig bewerten und die Richtlinienausdrücke mit gleicher Sorgfalt definieren.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Das Antwortobjekt enthält ein `duleLabels`-Array, das mit den in der Anfrage gesendeten Bezeichnungen übereinstimmen sollte. Wenn die Durchführung der angegebenen Marketing-Aktion für die Datennutzungsbezeichnungen eine Richtlinie verletzt, enthält das `violatedPolicies`-Array die Details der betroffenen Richtlinie (oder Richtlinien). Wenn keine Richtlinien verletzt werden, wird das `violatedPolicies`-Array leer angezeigt (`[]`).

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

## Bewerten von Richtlinien mithilfe von Datensätzen und einer Marketing-Aktion

Sie können auch Richtlinienverstöße bewerten, indem Sie die ID eines oder mehrerer Datensätze angeben, aus denen Datennutzungsbezeichnungen erfasst werden können. Dies erfolgt durch Ausführen einer POST-Anfrage an den Kern- oder den benutzerdefinierten `/constraints`-Endpunkt für eine Marketing-Aktion und Angeben der Datensatz-IDs innerhalb des Anfrageinhalts, wie unten dargestellt.

**API-Format**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Anfrage**

Der Anfrageinhalt enthält ein Array mit einem Objekt für jede Datensatz-ID. Da Sie einen Anfrageinhalt senden, ist die Anfragekopfzeile „Content-Type: application/json“ erforderlich, wie im folgenden Beispiel gezeigt.

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

Das Antwortobjekt enthält ein `duleLabels`-Array, das eine konsolidierte Liste aller in den angegebenen Datensätzen gefundenen Bezeichnungen enthält. Diese Liste enthält Bezeichnungen auf Datensatz- und Feldebene für alle Felder im Datensatz.

Die Antwort enthält außerdem ein `discoveredLabels`-Array mit Objekten für jeden Datensatz, in dem die `datasetLabels` in Bezeichnungen auf Datensatz- und Feldebene unterteilt sind. Jede Bezeichnung auf Feldebene zeigt den Pfad zum jeweiligen Feld mit dieser Bezeichnung.

Wenn die angegebene Marketing-Aktion gegen eine Richtlinie verstößt, die die `duleLabels` in den Datensätzen betrifft, enthält das `violatedPolicies`-Array die Details der betroffenen Richtlinie (oder Richtlinien). Wenn keine Richtlinien verletzt werden, wird das `violatedPolicies`-Array leer angezeigt (`[]`).

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

## Bewerten von Richtlinien mithilfe von Datensätzen, Feldern und einer Marketing-Aktion

Zusätzlich zur Angabe einer oder mehrerer Datensatz-IDs kann auch eine Teilmenge von Feldern aus jedem Datensatz angegeben werden, die angibt, dass nur die Datennutzungsbezeichnungen für diese Felder ausgewertet werden sollten. Ähnlich wie bei der POST-Anfrage, die nur Datensätze umfasst, fügt diese Anfrage dem Anfrageinhalt spezifische Felder für jeden Datensatz hinzu.

Beachten Sie bei der Bewertung von Richtlinien mithilfe von Datensatzfeldern Folgendes:

* **Bei Feldnamen wird zwischen Groß- und Kleinschreibung unterschieden.** Bei der Bereitstellung von Feldern müssen sie genau so geschrieben werden, wie sie im Datensatz erscheinen (z. B. `firstName` vs. `firstname`).
* **Vererbung der Datensatzbezeichnungen.** Datennutzungsbezeichnungen können auf mehreren Ebenen angewendet werden und werden nach unten vererbt. Wenn Ihre Richtlinienbewertungen nicht so zurückgegeben werden, wie Sie es sich vorgestellt haben, überprüfen Sie zusätzlich zu den auf Feldebene angewendeten Bezeichnungen die vererbten Bezeichnungen von den Datensätzen bis hin zu den Feldern.

**API-Format**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**Anfrage**

Der Anfrageinhalt enthält ein Array mit einem Objekt für jede Datensatz-ID und die Teilmenge der Felder in diesem Datensatz, die für die Bewertung verwendet werden sollen. Da Sie einen Anfrageinhalt senden, ist die Anfragekopfzeile „Content-Type: application/json“ erforderlich, wie im folgenden Beispiel gezeigt.

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

Das Antwortobjekt enthält ein `duleLabels`-Array, das die konsolidierte Liste der in den angegebenen Feldern gefundenen Bezeichnungen enthält. Denken Sie daran, dass dies auch Datensatzbezeichnungen umfasst, da diese bis zu den Feldern vererbt werden.

Wenn die Durchführung der angegebenen Marketing-Aktion für die Daten in den abgegebenen Feldern eine Richtlinie verletzt, enthält das `violatedPolicies`-Array die Details der betroffenen Richtlinie (oder Richtlinien). Wenn keine Richtlinien verletzt werden, wird das `violatedPolicies`-Array leer angezeigt (`[]`).

In der folgenden Antwort sehen Sie, dass die Liste der `duleLabels` jetzt kürzer ist, ebenso wie die `discoveredLabels` für jeden Datensatz, da sie nur die im Anfrageinhalt angegebenen Felder enthält. Sie werden auch feststellen, dass die zuvor verletzte Richtlinie „Targeting-Anzeigen oder Inhalte“ beide `C4 AND C6`-Bezeichnungen erforderte. Sie wird also nicht mehr verletzt und das `violatedPolicies`-Array ist leer.

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

## Politikbewertung für [!DNL Real-time Customer Profile]

The [!DNL Policy Service] API can also be used to check for policy violations involving the use of [!DNL Real-time Customer Profile] segments. Weiterführende Informationen finden Sie im Tutorial zum [Durchsetzen der Datennutzungskonformität für Zielgruppensegmente](../../segmentation/tutorials/governance.md).