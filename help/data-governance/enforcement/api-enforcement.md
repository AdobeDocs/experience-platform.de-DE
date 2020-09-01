---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Datennutzungsrichtlinien mithilfe der Policy Service-API durchsetzen
topic: enforcement
description: Nachdem Sie Datennutzungsbezeichnungen für Ihre Daten sowie Nutzungsrichtlinien für Marketing-Aktionen hinsichtlich dieser Bezeichnungen erstellt haben, können Sie mit der Policy Service-API bewerten, ob eine Marketing-Aktion, die für einen Datensatz oder eine beliebige Gruppe von Bezeichnungen durchgeführt wird, eine Richtlinienverletzung darstellt. Sie können dann eigene interne Protokolle einrichten, um mit Richtlinienverletzungen je nach API-Antwort umzugehen.
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 48%

---


# Enforce data usage policies using the [!DNL Policy Service] API

Once you have created data usage labels for your data, and have created usage policies for marketing actions against those labels, you can use the [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) to evaluate whether a marketing action performed on a dataset or an arbitrary group of labels constitutes a policy violation. Sie können dann eigene interne Protokolle einrichten, um mit Richtlinienverletzungen je nach API-Antwort umzugehen.

>[!NOTE]
>
> Standardmäßig können nur Richtlinien, deren Status auf `ENABLED` gesetzt ist, an der Bewertung teilnehmen. Damit `DRAFT`-Richtlinien an der Bewertung teilnehmen können, müssen Sie den Abfrageparameter `includeDraft=true` in den Anfragepfad einbeziehen.

This document provides steps on how to use the [!DNL Policy Service] API to check for policy violations in different scenarios.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Schlüsselkonzepte, die beim Erzwingen von Datenverwendungsrichtlinien verwendet werden:

* [Data Governance](../home.md)[!DNL Platform]: Das Framework, mit dem die Einhaltung der Datennutzungsrichtlinien durchsetzt.
   * [Datennutzungsbezeichnungen](../labels/overview.md): Datennutzungsbezeichnungen werden auf Datensätze (und/oder einzelne Felder in diesen Datensätzen) angewendet und geben Einschränkungen für die Verwendungsmöglichkeiten dieser Daten an.
   * [Datenverwendungsrichtlinien](../policies/overview.md): Datenverwendungsrichtlinien sind Regeln, die die Arten von Marketingaktionen beschreiben, die für bestimmte Gruppen von Datenverwendungsbeschriftungen zulässig oder eingeschränkt sind.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Before starting this tutorial, please review the [developer guide](../api/getting-started.md) for important information that you need to know in order to successfully make calls to the [!DNL Policy Service] API, including required headers and how to read example API calls.

## Bewerten Sie die Bewertung mit Beschriftungen und einer Marketingaktion.

Sie können eine Richtlinie bewerten, indem Sie eine Marketingaktion mit einer Reihe von Datenverwendungs-Beschriftungen testen, die hypothetisch in einem Datensatz vorhanden sein würden. This is done through the use of the `duleLabels` query parameter, where labels are provided as a comma-separated list of values, as shown in the example below.

**API-Format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion im Zusammenhang mit der Datenverwendungsrichtlinie, die Sie bewerten. |
| `{LABEL_1}` | Eine Datennutzungsbezeichnung zum Testen der Marketing-Aktion. Es muss mindestens eine Bezeichnung angegeben werden. Bei der Bereitstellung mehrerer Bezeichnungen müssen diese durch Kommas getrennt werden. |

**Anfrage**

Die folgende Anfrage testet die Marketing-Aktion `exportToThirdParty` hinsichtlich der Bezeichnungen `C1` und `C3`. Da die zuvor in dieser Anleitung erstellte Datennutzungsrichtlinie die `C1`-Bezeichnung als eine der `deny`-Bedingungen in ihrem Richtlinienausdruck definiert, sollte die Marketing-Aktion eine Richtlinienverletzung auslösen.

>[!NOTE]
>
> Bei Datennutzungsbezeichnungen wird zwischen Groß- und Kleinschreibung unterschieden. Richtlinienverletzungen treten nur dann auf, wenn die in ihren Richtlinienausdrücken definierten Bezeichnungen exakt übereinstimmen. In diesem Beispiel würde eine `C1`-Bezeichnung eine Verletzung auslösen, eine `c1`-Bezeichnung hingegen nicht.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die URL für die Marketingaktion, die Gebrauchsbeschriftungen, gegen die sie getestet wurde, und eine Liste aller Richtlinien zurück, die beim Testen der Aktion gegen diese Beschriftungen verletzt wurden. In diesem Beispiel wird die Richtlinie „Daten an Dritte exportieren“ im `violatedPolicies`-Array angezeigt; dadurch wird angegeben, dass die Marketing-Aktion die erwartete Richtlinienverletzung ausgelöst hat.

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
| `violatedPolicies` | An array listing any policies that were violated by testing the marketing action (specified in `marketingActionRef`) against the provided `duleLabels`. |

## Mit Datensätzen bewerten

Sie können eine Datenverwendungsrichtlinie bewerten, indem Sie eine Marketingaktion mit einem oder mehreren Datensätzen testen, aus denen Beschriftungen erfasst werden können. Dies geschieht durch eine POST-Anfrage an `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` und Angabe von Datensatz-IDs im Anfragetext, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion im Zusammenhang mit der auszuwertenden Richtlinie. |

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

Eine erfolgreiche Antwort gibt die URL für die Marketingaktion, die von den bereitgestellten Datensätzen erfassten Nutzungsbezeichnungen und eine Liste aller Richtlinien zurück, die beim Testen der Aktion gegen diese Bezeichnungen verletzt wurden. In diesem Beispiel wird die Richtlinie „Daten an Dritte exportieren“ im `violatedPolicies`-Array angezeigt; dadurch wird angegeben, dass die Marketing-Aktion die erwartete Richtlinienverletzung ausgelöst hat.

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
| `duleLabels` | Eine Liste von Datenverwendungsbeschriftungen, die aus den in der Anforderungs-Payload bereitgestellten Datensätzen extrahiert wurden. |
| `discoveredLabels` | Eine Liste der Datensätze, die in der Anforderungsnutzlast bereitgestellt wurden, mit den Beschriftungen auf Datensatzebene und auf Feldebene, die in den einzelnen Datensätzen gefunden wurden. |
| `violatedPolicies` | An array listing any policies that were violated by testing the marketing action (specified in `marketingActionRef`) against the provided `duleLabels`. |

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie bei der Durchführung einer Marketingaktion für einen Datensatz oder eine Reihe von Beschriftungen zur Datenverwendung erfolgreich auf Richtlinienverletzungen überprüft. Mithilfe der in den API-Antworten zurückgegebenen Daten können Sie Protokolle in Ihrer Erlebnisanwendung einrichten, um Richtlinienverletzungen bei ihrem Auftreten angemessen durchzusetzen.

For steps on how to enforce data usage policies for audience segments in [!DNL Real-time Customer Profile], please refer to the following [tutorial](../../segmentation/tutorials/governance.md).