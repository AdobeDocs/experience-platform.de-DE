---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datennutzungsrichtlinien mithilfe der Policy Service-API durchsetzen
topic: enforcement
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 83%

---


# Enforce data usage policies using the [!DNL Policy Service] API

Once you have created data usage labels for your data, and have created usage policies for marketing actions against those labels, you can use the [!DNL DULE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) to evaluate whether a marketing action performed on a dataset or an arbitrary group of labels constitutes a policy violation. Sie können dann eigene interne Protokolle einrichten, um mit Richtlinienverletzungen je nach API-Antwort umzugehen.

>[!NOTE]
>
>Standardmäßig können nur Richtlinien, deren Status auf `ENABLED` gesetzt ist, an der Bewertung teilnehmen. Damit `DRAFT`-Richtlinien an der Bewertung teilnehmen können, müssen Sie den Abfrageparameter `includeDraft=true` in den Anfragepfad einbeziehen.

This document provides steps on how to use the [!DNL Policy Service] API to check for policy violations in different scenarios.

## Erste Schritte

Diese Anleitung setzt ein Verständnis der folgenden Schlüsselkonzepte voraus, die beim Durchsetzen von DULE-Richtlinien gelten:

* [Data Governance](../home.md)[!DNL Platform]: Das Framework, mit dem die Einhaltung der Datennutzungsrichtlinien durchsetzt.
   * [Datennutzungsbezeichnungen](../labels/overview.md): Datennutzungsbezeichnungen werden auf Datensätze (und/oder einzelne Felder in diesen Datensätzen) angewendet und geben Einschränkungen für die Verwendungsmöglichkeiten dieser Daten an.
   * [Datennutzungsrichtlinien](../policies/overview.md): Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die für bestimmte Sätze von DULE-Bezeichnungen zulässig bzw. eingeschränkt sind.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Before starting this tutorial, please review the [developer guide](../api/getting-started.md) for important information that you need to know in order to successfully make calls to the DULE [!DNL Policy Service] API, including required headers and how to read example API calls.

## Mit DULE-Bezeichnungen und einer Marketing-Aktion bewerten

Sie können eine Richtlinie bewerten, indem Sie eine Marketing-Aktion mit einem Satz von DULE-Bezeichnungen testen, die hypothetisch in einem Datensatz vorhanden sein würden. Dies geschieht mithilfe des Abfrageparameters `duleLabels`, bei dem DULE-Bezeichnungen als kommagetrennte Liste von Werten bereitgestellt werden (siehe folgendes Beispiel).

**API-Format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketing-Aktion, die mit der von Ihnen bewerteten DULE-Richtlinie verknüpft ist. |
| `{LABEL_1}` | Eine Datennutzungsbezeichnung zum Testen der Marketing-Aktion. Es muss mindestens eine Bezeichnung angegeben werden. Bei der Bereitstellung mehrerer Bezeichnungen müssen diese durch Kommas getrennt werden. |

**Anfrage**

Die folgende Anfrage testet die Marketing-Aktion `exportToThirdParty` hinsichtlich der Bezeichnungen `C1` und `C3`. Da die zuvor in dieser Anleitung erstellte Datennutzungsrichtlinie die `C1`-Bezeichnung als eine der `deny`-Bedingungen in ihrem Richtlinienausdruck definiert, sollte die Marketing-Aktion eine Richtlinienverletzung auslösen.

>[!NOTE]
>
>Bei Datennutzungsbezeichnungen wird zwischen Groß- und Kleinschreibung unterschieden. Richtlinienverletzungen treten nur dann auf, wenn die in ihren Richtlinienausdrücken definierten Bezeichnungen exakt übereinstimmen. In diesem Beispiel würde eine `C1`-Bezeichnung eine Verletzung auslösen, eine `c1`-Bezeichnung hingegen nicht.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die URL für die Marketing-Aktion, die DULE-Bezeichnungen, anhand der sie getestet wurde, und eine Liste aller DULE-Richtlinien zurückgegeben, die beim Testen der Aktion hinsichtlich dieser Bezeichnungen verletzt wurden. In diesem Beispiel wird die Richtlinie „Daten an Dritte exportieren“ im `violatedPolicies`-Array angezeigt; dadurch wird angegeben, dass die Marketing-Aktion die erwartete Richtlinienverletzung ausgelöst hat.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `violatedPolicies` | Ein Array, das alle DULE-Richtlinien auflistet, die durch Testen der Marketing-Aktion (angegeben in `marketingActionRef`) hinsichtlich der angegebenen `duleLabels` verletzt wurden. |

## Mit Datensätzen bewerten

Sie können eine DULE-Richtlinie bewerten, indem Sie eine Marketing-Aktion mit einem oder mehreren Datensätzen testen, aus denen DULE-Bezeichnungen gesammelt werden können. Dies geschieht durch eine POST-Anfrage an `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` und Angabe von Datensatz-IDs im Anfragetext, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketing-Aktion, die mit der von Ihnen bewerteten DULE-Richtlinie verknüpft ist. |

**Anfrage**

Die folgende Anfrage testet die Marketing-Aktion `exportToThirdParty` mit drei verschiedenen Datensätzen. Die Datensätze werden nach Typ und Kennung in einem Array referenziert, das in der Payload bereitgestellt wird.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
| `entityType` | Jedes Element im Payload-Array muss den Typ der zu definierenden Entität angeben. In diesem Anwendungsfall ist der Wert immer „dataSet“. |
| `entityId` | Jedes Element im Payload-Array muss die eindeutige Kennung für einen Datensatz angeben. |

**Antwort**

Bei einer erfolgreichen Antwort werden die URL für die Marketing-Aktion, die DULE-Bezeichnungen, die aus den bereitgestellten Datensätzen gesammelt wurden, und eine Liste aller DULE-Richtlinien zurückgegeben, die beim Testen der Aktion hinsichtlich dieser Bezeichnungen verletzt wurden. In diesem Beispiel wird die Richtlinie „Daten an Dritte exportieren“ im `violatedPolicies`-Array angezeigt; dadurch wird angegeben, dass die Marketing-Aktion die erwartete Richtlinienverletzung ausgelöst hat.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
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
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `duleLabels` | Eine Liste von DULE-Bezeichnungen, die aus den in der Anfrage-Payload angegebenen Datensätzen extrahiert wurden. |
| `discoveredLabels` | Eine Liste der Datensätze, die in der Anfrage-Payload angegeben wurden; angezeigt werden die in den einzelnen Datensätzen gefundenen DULE-Bezeichnungen auf Datensatzebene und Feldebene. |
| `violatedPolicies` | Ein Array, das alle DULE-Richtlinien auflistet, die durch Testen der Marketing-Aktion (angegeben in `marketingActionRef`) hinsichtlich der angegebenen `duleLabels`-Richtlinie verletzt wurden. |

## Nächste Schritte

Durch Befolgen dieses Dokuments haben Sie bei der Ausführung einer Marketing-Aktion für einen Datensatz oder eine Reihe von DULE-Bezeichnungen erfolgreich auf Richtlinienverletzungen geprüft. Mithilfe der in den API-Antworten zurückgegebenen Daten können Sie Protokolle in Ihrer Erlebnisanwendung einrichten, um Richtlinienverletzungen bei ihrem Auftreten angemessen durchzusetzen.

For steps on how to enforce data usage policies for audience segments in [!DNL Real-time Customer Profile], please refer to the following [tutorial](../../segmentation/tutorials/governance.md).