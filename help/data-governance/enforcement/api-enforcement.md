---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erzwingen von Datenverwendungsrichtlinien mithilfe der Policy Service API
topic: enforcement
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 3%

---


# Erzwingen von Datenverwendungsrichtlinien mithilfe der Policy Service API

Nachdem Sie Datenverwendungsbeschriftungen für Ihre Daten erstellt und Nutzungsrichtlinien für Marketingaktionen für diese Beschriftungen erstellt haben, können Sie mit der API [für den](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DUL-Policy-Dienst bewerten, ob eine Marketingaktion, die für einen Datensatz oder eine beliebige Gruppe von Beschriftungen durchgeführt wird, eine Richtlinienverletzung darstellt. Sie können dann Ihre eigenen internen Protokolle einrichten, um Richtlinienverletzungen basierend auf der API-Antwort zu behandeln.

>[!NOTE] Standardmäßig `ENABLED` können nur Richtlinien, deren Status auf &quot;Testen&quot;festgelegt ist, an der Evaluierung teilnehmen. Damit `DRAFT` Richtlinien an der Auswertung teilnehmen können, müssen Sie den Parameter &quot;Abfrage&quot; `includeDraft=true` in den Anforderungspfad einbeziehen.

In diesem Dokument wird beschrieben, wie Sie die [!DNL Policy Service] API verwenden, um in verschiedenen Szenarien nach Richtlinienverletzungen zu suchen.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Schlüsselkonzepte, die bei der Durchsetzung von DULE-Richtlinien zum Tragen kommen:

* [Datenverwaltung](../home.md): Das Framework, mit dem die Einhaltung der Datenverwendung [!DNL Platform] erzwungen wird.
   * [Datenverwendungsbeschriftungen](../labels/overview.md): Datenverwendungsbeschriftungen werden auf Datasets (und/oder einzelne Felder innerhalb dieser Datensätze) angewendet und geben Einschränkungen für die Verwendung dieser Daten an.
   * [Datenverwendungsrichtlinien](../policies/overview.md): Datenverwendungs-Richtlinien sind Regeln, die die Arten von Marketingaktionen beschreiben, die für bestimmte Sätze von DULE-Beschriftungen zulässig oder eingeschränkt sind.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte das [Entwicklerhandbuch](../api/getting-started.md) , um wichtige Informationen zu erhalten, die Sie für die erfolgreiche Durchführung von Aufrufen an die DULE [!DNL Policy Service] -API benötigen, einschließlich erforderlicher Kopfzeilen und Anleitungen zum Lesen von Beispiel-API-Aufrufen.

## Bewerten Sie die Bewertung mit DULE-Etiketten und einer Marketingaktion.

Sie können eine Richtlinie bewerten, indem Sie eine Marketingaktion mit einem Satz von DULE-Beschriftungen testen, die hypothetisch in einem Datensatz vorhanden sein würden. Dies geschieht mithilfe des Parameters `duleLabels` Abfrage, bei dem Doppel-Beschriftungen als kommagetrennte Liste von Werten bereitgestellt werden, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion, die mit der von Ihnen bewerteten DULE-Richtlinie verknüpft ist. |
| `{LABEL_1}` | Eine Datenverwendungsbeschriftung zum Testen der Marketingaktion. Es muss mindestens ein Etikett angegeben werden. Bei der Bereitstellung mehrerer Beschriftungen müssen diese durch Kommas getrennt werden. |

**Anfrage**

Die folgende Anforderung testet die `exportToThirdParty` Marketingmaßnahme gegen Etiketten `C1` und `C3`. Da die zuvor in diesem Lernprogramm erstellte Datenverwendungsrichtlinie die `C1` Bezeichnung als eine der `deny` Bedingungen in ihrem Policy-Ausdruck definiert, sollte die Marketingaktion eine Richtlinienverletzung auslösen.

>[!NOTE] Bei den Beschriftungen für die Datenverwendung wird zwischen Groß- und Kleinschreibung unterschieden. Richtlinienverletzungen treten nur dann auf, wenn die in ihren Richtlinien-Ausdrücken definierten Bezeichnungen exakt übereinstimmen. In diesem Beispiel würde eine `C1` Beschriftung eine Verletzung auslösen, eine `c1` Bezeichnung hingegen nicht.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die URL für die Marketingaktion, die DULE-Beschriftungen, gegen die sie getestet wurde, und eine Liste aller DULE-Richtlinien zurückgegeben, die beim Testen der Aktion gegen diese Beschriftungen verletzt wurden. In diesem Beispiel wird die Richtlinie &quot;Daten an Dritte exportieren&quot;im `violatedPolicies` Array angezeigt, was angibt, dass die Marketingaktion die erwartete Richtlinienverletzung ausgelöst hat.

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
| `violatedPolicies` | Ein Array, das alle DULE-Richtlinien auflistet, die durch Testen der Marketingaktion (angegeben in `marketingActionRef`) gegen die bereitgestellte `duleLabels`Richtlinie verletzt wurden. |

## Mit Datensätzen auswerten

Sie können eine DULE-Richtlinie bewerten, indem Sie eine Marketingaktion mit einem oder mehreren Datensätzen testen, aus denen Doppel-Etiketten erfasst werden können. Dies geschieht durch eine POST-Anforderung an `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` und die Bereitstellung von DataSet-IDs im Anforderungstext, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion, die mit der von Ihnen bewerteten DULE-Richtlinie verknüpft ist. |

**Anfrage**

Die folgende Anforderung testet die `exportToThirdParty` Marketingaktion mit drei verschiedenen Datensätzen. Die Datensätze werden nach Typ und ID in einem Array referenziert, das in der Payload bereitgestellt wird.

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
| `entityType` | Jedes Element im Payload-Array muss den Typ der zu definierenden Entität angeben. In diesem Anwendungsfall ist der Wert immer &quot;dataSet&quot;. |
| `entityId` | Jedes Element im Payload-Array muss die eindeutige ID für einen Datensatz bereitstellen. |

**Antwort**

Bei einer erfolgreichen Antwort werden die URL für die Marketingaktion, die DULE-Beschriftungen, die aus den bereitgestellten Datensätzen gesammelt wurden, und eine Liste aller DULE-Richtlinien zurückgegeben, die beim Testen der Aktion gegen diese Beschriftungen verletzt wurden. In diesem Beispiel wird die Richtlinie &quot;Daten an Dritte exportieren&quot;im `violatedPolicies` Array angezeigt, was angibt, dass die Marketingaktion die erwartete Richtlinienverletzung ausgelöst hat.

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
| `duleLabels` | Eine Liste von DULE-Beschriftungen, die aus den in der Anforderungs-Nutzlast bereitgestellten Datensätzen extrahiert wurden. |
| `discoveredLabels` | Eine Liste der Datensätze, die in der Anforderungsnutzlast bereitgestellt wurden, mit den in den einzelnen Datensätzen gefundenen DULE-Beschriftungen auf Datensatzebene und Feldebene. |
| `violatedPolicies` | Ein Array, das alle DULE-Richtlinien auflistet, die durch Testen der Marketingaktion (angegeben in `marketingActionRef`) gegen die bereitgestellte `duleLabels`Richtlinie verletzt wurden. |

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie bei der Durchführung einer Marketingaktion für einen Datensatz oder eine Reihe von DULE-Beschriftungen erfolgreich auf Richtlinienverletzungen überprüft. Mithilfe der in den API-Antworten zurückgegebenen Daten können Sie Protokolle in Ihrer Erlebnisanwendung einrichten, um Richtlinienverletzungen bei deren Auftreten angemessen zu erzwingen.

Anweisungen zum Erzwingen von Datenverwendungsrichtlinien für Audiencen-Segmente in [!DNL Real-time Customer Profile]finden Sie im folgenden [Lernprogramm](../../segmentation/tutorials/governance.md).