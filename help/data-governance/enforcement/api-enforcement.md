---
keywords: Experience Platform;Startseite;beliebte Themen;Richtliniendurchsetzung;Automatisierte Durchsetzung;API-basierte Durchsetzung;Datenverwaltung;Tests
solution: Experience Platform
title: Durchsetzen von Datennutzungsrichtlinien mithilfe der Policy Service-API
type: Tutorial
description: Nachdem Sie Datennutzungsbezeichnungen für Ihre Daten sowie Nutzungsrichtlinien für Marketing-Aktionen hinsichtlich dieser Bezeichnungen erstellt haben, können Sie mit der Policy Service-API bewerten, ob eine Marketing-Aktion, die für einen Datensatz oder eine beliebige Gruppe von Bezeichnungen durchgeführt wird, eine Richtlinienverletzung darstellt. Sie können dann eigene interne Protokolle einrichten, um mit Richtlinienverletzungen je nach API-Antwort umzugehen.
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: ht
source-wordcount: '1002'
ht-degree: 100%

---

# Durchsetzen von Datennutzungsrichtlinien mit der [!DNL Policy Service]-API

Nachdem Sie Datennutzungskennzeichnungen für Ihre Daten sowie Nutzungsrichtlinien für Marketing-Aktionen hinsichtlich dieser Kennzeichnungen erstellt haben, können Sie mit der [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) bewerten, ob eine Marketing-Aktion, die für einen Datensatz oder eine beliebige Gruppe von Kennzeichnungen ausgeführt wird, eine Richtlinienverletzung darstellt. Sie können dann eigene interne Protokolle einrichten, um mit Richtlinienverletzungen je nach API-Antwort umzugehen.

>[!NOTE]
>
>Standardmäßig können nur Richtlinien, deren Status auf `ENABLED` gesetzt ist, an der Bewertung teilnehmen. Damit `DRAFT`-Richtlinien an der Bewertung teilnehmen können, müssen Sie den Abfrageparameter `includeDraft=true` in den Anfragepfad einbeziehen.

In diesem Dokument wird beschrieben, wie Sie mit der [!DNL Policy Service]-API in verschiedenen Szenarien nach Richtlinienverletzungen suchen können.

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der folgenden Schlüsselkonzepte voraus, die beim Durchsetzen von Datennutzungsrichtlinien eine Rolle spielen:

* [Data Governance](../home.md): Das Framework, mit dem [!DNL Platform] die Einhaltung der Datennutzungsrichtlinien durchsetzt.
   * [Datennutzungsbezeichnungen](../labels/overview.md): Datennutzungsbezeichnungen werden auf Datensätze (und/oder einzelne Felder in diesen Datensätzen) angewendet und geben Einschränkungen für die Verwendungsmöglichkeiten dieser Daten an.
   * [Datennutzungsrichtlinien](../policies/overview.md): Datennutzungsrichtlinien sind Regeln, die die Arten von Marketing-Aktionen beschreiben, die für bestimmte Sätze von Datennutzungskennzeichnungen zulässig bzw. eingeschränkt sind.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Bevor Sie mit diesem Tutorial beginnen, lesen Sie das [Entwicklerhandbuch](../api/getting-started.md), um wichtige Informationen zu erhalten, die Sie für die erfolgreiche Durchführung von Aufrufen an die [!DNL Policy Service]-API benötigen, einschließlich erforderlicher Kopfzeilen und Anweisungen zum Lesen von Beispiel-API-Aufrufen.

## Auswerten mit Kennzeichnungen und einer Marketing-Aktion

Sie können eine Richtlinie auswerten, indem Sie eine Marketing-Aktion mit einem Satz von Datennutzungskennzeichnungen testen, die hypothetisch in einem Datensatz vorhanden sein würden. Dies geschieht mithilfe des Abfrageparameters `duleLabels`, bei dem Kennzeichnungen als kommagetrennte Liste von Werten bereitgestellt werden, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketing-Aktion, die mit der von Ihnen auszuwertenden Datennutzungsrichtlinie verknüpft ist. |
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden die URL für die Marketing-Aktion, die Datennutzungskennzeichnungen, anhand der sie getestet wurde, und eine Liste aller Richtlinien zurückgegeben, die beim Testen der Aktion hinsichtlich dieser Kennzeichnungen verletzt wurden. In diesem Beispiel wird die Richtlinie „Daten an Dritte exportieren“ im `violatedPolicies`-Array angezeigt; dadurch wird angegeben, dass die Marketing-Aktion die erwartete Richtlinienverletzung ausgelöst hat.

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `violatedPolicies` | Ein Array, das alle Richtlinien auflistet, die durch Testen der Marketing-Aktion (angegeben in `marketingActionRef`) hinsichtlich der angegebenen `duleLabels` verletzt wurden. |

## Mit Datensätzen bewerten

Sie können eine Datennutzungsrichtlinie bewerten, indem Sie eine Marketing-Aktion mit einem oder mehreren Datensätzen testen, aus denen Kennzeichnungen gesammelt werden können. Dies geschieht durch eine POST-Anfrage an `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` und Angabe von Datensatz-IDs im Anfragetext, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketing-Aktion, die mit der von Ihnen bewerteten Richtlinie verknüpft ist. |

**Anfrage**

Die folgende Anfrage testet die Marketing-Aktion `exportToThirdParty` mit drei verschiedenen Datensätzen. Die Datensätze werden nach Typ und Kennung in einem Array referenziert, das in der Payload bereitgestellt wird.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `entityType` | Jedes Element im Payload-Array muss den Typ der zu definierenden Entität angeben. In diesem Anwendungsfall ist der Wert immer „dataSet“. |
| `entityId` | Jedes Element im Payload-Array muss die eindeutige Kennung für einen Datensatz angeben. |
| `entityMeta.fields` | (Optional) Ein Array von [JSON-Zeiger](../../landing/api-fundamentals.md#json-pointer)-Zeichenfolgen, das auf bestimmte Felder im Schema des Datensatzes verweist. Wenn dieses Array enthalten ist, werden nur die im Array enthaltenen Felder in die Auswertung einbezogen. Alle Schema-Felder, die nicht im Array enthalten sind, werden nicht in die Auswertung einbezogen.<br><br>Wenn dieses Feld nicht enthalten ist, werden alle Felder, die sich im Datensatzschema befinden, ausgewertet. |

**Antwort**

Bei einer erfolgreichen Antwort werden die URL für die Marketing-Aktion, die Datennutzungskennzeichnungen, die aus den bereitgestellten Datensätzen gesammelt wurden, und eine Liste all der Richtlinien zurückgegeben, die beim Testen der Aktion hinsichtlich dieser Kennzeichnungen verletzt wurden. In diesem Beispiel wird die Richtlinie „Daten an Dritte exportieren“ im `violatedPolicies`-Array angezeigt; dadurch wird angegeben, dass die Marketing-Aktion die erwartete Richtlinienverletzung ausgelöst hat.

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
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
            "imsOrg": "{ORG_ID}",
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
| `duleLabels` | Eine Liste von Datennutzungskennzeichnungen, die aus den in der Payload der Anfrage angegebenen Datensätzen extrahiert wurden. |
| `discoveredLabels` | Eine Liste der Datensätze, die in der Payload der Anfrage angegeben wurden; angezeigt werden die in den einzelnen Datensätzen gefundenen Kennzeichnungen auf Datensatzebene und Feldebene. |
| `violatedPolicies` | Ein Array, das alle Richtlinien auflistet, die durch Testen der Marketing-Aktion (angegeben in `marketingActionRef`) hinsichtlich der angegebenen `duleLabels` verletzt wurden. |

## Nächste Schritte

Indem Sie dieses Dokuments lesen, haben Sie bei der Ausführung einer Marketing-Aktion für einen Datensatz oder eine Reihe von Datennutzungskennzeichnungen erfolgreich geprüft, ob Richtlinien verletzt wurden. Mithilfe der in den API-Antworten zurückgegebenen Daten können Sie Protokolle in Ihrer Erlebnisanwendung einrichten, um Richtlinienverletzungen bei ihrem Auftreten angemessen durchzusetzen.

Informationen dazu, wie Platform automatisch die Richtliniendurchsetzung für aktivierte Segmente bereitstellt, finden Sie im Handbuch [Automatische Durchsetzung](./auto-enforcement.md).
