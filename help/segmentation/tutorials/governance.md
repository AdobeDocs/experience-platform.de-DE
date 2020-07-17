---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Durchsetzen der Datennutzungskonformität für Zielgruppensegmente
topic: tutorial
translation-type: tm+mt
source-git-commit: cb6a2f91eb6c18835bd9542e5b66af4682227491
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 43%

---


# Durchsetzen der Datennutzungskonformität für Zielgruppensegmente mithilfe von APIs

This tutorial covers the steps for enforcing data usage compliance for [!DNL Real-time Customer Profile] audience segments using APIs.

## Erste Schritte

This tutorial requires a working understanding of the following components of [!DNL Adobe Experience Platform]:

- [!DNL Real-time Customer Profile](../../profile/home.md): [!DNL Real-time Customer Profile] ist ein generischer Lookup-Entitätsspeicher und wird zur Verwaltung von [!DNL Experience Data Model] (XDM-)Daten in [!DNL Platform]. Das Profil führt Daten aus verschiedenen Unternehmensdaten-Assets zusammen und ermöglicht den Zugriff auf diese Daten in einer einheitlichen Darstellung.
   - [Richtlinien](../../profile/api/merge-policies.md)zusammenführen: Regeln, [!DNL Real-time Customer Profile] mit denen bestimmt wird, welche Daten unter bestimmten Voraussetzungen in einer einheitlichen Ansicht zusammengeführt werden können. Zusammenführungsrichtlinien können für Data Governance-Zwecke konfiguriert werden.
- [!DNL Segmentation](../home.md): Wie [!DNL Real-time Customer Profile] unterteilt eine große Gruppe von im Profil Store enthaltenen Personen in kleinere Gruppen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.
- [!DNL Data Governance](../../data-governance/home.md): [!DNL Data Governance] stellt die Infrastruktur für die Kennzeichnung und Durchsetzung der Datenverwendung (DULE) unter Verwendung der folgenden Komponenten bereit:
   - [Datennutzungsbezeichnungen](../../data-governance/labels/user-guide.md): Bezeichnungen, die zur Beschreibung von Datensätzen und Feldern in Bezug auf die Sensibilität, mit der die jeweiligen Daten verarbeitet werden sollen, verwendet werden.
   - [Datennutzungsrichtlinien](../../data-governance/policies/overview.md): Konfigurationen, die angeben, welche Marketing-Aktionen für Daten zulässig sind, die nach bestimmten Datennutzungsbezeichnungen kategorisiert sind.
   - [Durchsetzung](../../data-governance/enforcement/overview.md)der Politik: Ermöglicht es Ihnen, Datenverwendungsrichtlinien zu erzwingen und Datenvorgänge zu verhindern, die Richtlinienverletzungen darstellen.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully make calls to the [!DNL Platform] APIs.

### Lesehilfe für Beispiel-API-Aufrufe

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

### Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Alle Anfragen, die eine Payload enthalten (also POST-, PUT- und PATCH-Anfragen), erfordern eine zusätzliche Kopfzeile:

- Content-Type: application/json

## Look up a merge policy for a segment definition {#merge-policy}

Dieser Workflow beginnt mit dem Zugriff auf ein bekanntes Zielgruppensegment. Segments that are enabled for use in [!DNL Real-time Customer Profile] contain a merge policy ID within their segment definition. Diese Zusammenführungsrichtlinie enthält Informationen darüber, welche Datensätze in das Segment aufgenommen werden sollen, die wiederum alle zutreffenden Datennutzungsbezeichnungen enthalten.

Using the [!DNL Segmentation] API, you can look up a segment definition by its ID to find its associated merge policy.

**API-Format**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | Die Kennung der Segmentdefinition, die Sie nachschlagen möchten. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Segmentdefinition zurück.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{IMS_ORG}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
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
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `mergePolicyId` | Die ID der Zusammenführungsrichtlinie, die für die Segmentdefinition verwendet wird. Diese wird im nächsten Schritt verwendet. |

## Suchen nach Quelldatensätzen in der Zusammenführungsrichtlinie {#datasets}

Merge-Richtlinien enthalten Informationen zu ihren Quelldatasets, die wiederum Datenverwendungsbeschriftungen enthalten. You can lookup the details of a merge policy by providing the merge policy ID in a GET request to the [!DNL Profile] API. Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im Endpunkt-Handbuch zu [Zusammenführungsrichtlinien](../../profile/api/merge-policies.md).

**API-Format**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | Die ID der im [vorherigen Schritt](#merge-policy) abgerufenen Zusammenführungsrichtlinie. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Zusammenführungsrichtlinie zurück.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schema.name` | Der Name des Schemas, das der Zusammenführungsrichtlinie zugeordnet ist. |
| `attributeMerge.type` | Der Konfigurationstyp für die Datenpriorität für die Zusammenführungsrichtlinie. Wenn der Wert `dataSetPrecedence` ist, werden die mit dieser Zusammenführungsrichtlinie verknüpften Datensätze unter `attributeMerge > data > order` aufgelistet. Wenn der Wert `timestampOrdered`ist, werden alle Datensätze, die mit dem in `schema.name` referenzierten Schema verknüpft sind, von der Richtlinie verwendet. |
| `attributeMerge.data.order` | Wenn `attributeMerge.type` `dataSetPrecedence` ist, ist dieses Attribut ein Array, das die IDs der von dieser Zusammenführungsrichtlinie verwendeten Datensätze enthält. Diese IDs werden im nächsten Schritt verwendet. |

## Bewerten Sie Datensätze für Richtlinienverletzungen.

>[!NOTE]
>
> Bei diesem Schritt wird davon ausgegangen, dass Sie über mindestens eine aktive Datenverwendungsrichtlinie verfügen, die verhindert, dass bestimmte Marketingaktionen für Daten mit bestimmten Beschriftungen durchgeführt werden. Wenn Sie keine anwendbaren Nutzungsrichtlinien für die zu evaluierenden Datensätze haben, führen Sie das [Richtlinienerstellungslehrgang](../../data-governance/policies/create.md) durch, um eine zu erstellen, bevor Sie mit diesem Schritt fortfahren.

Nachdem Sie die IDs der Quelldatasets der Richtlinie zur Zusammenführung erhalten haben, können Sie diese Datensätze mit der [DUL Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) gegen bestimmte Marketingaktionen auswerten, um Verstöße gegen die Datenverwendungsrichtlinie zu prüfen.

Zur Auswertung der Datensätze müssen Sie den Namen der Marketingaktion im Pfad einer POST-Anforderung angeben und gleichzeitig die DataSet-IDs im Anforderungstext bereitstellen, wie im Beispiel unten dargestellt.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion im Zusammenhang mit der Datenverwendungsrichtlinie, nach der Sie die Datensätze bewerten. Je nachdem, ob die Richtlinie von Adobe oder Ihrem Unternehmen definiert wurde, müssen Sie sie verwenden `/marketingActions/core` bzw. `/marketingActions/custom`verwenden. |

**Anfrage**

Die folgende Anforderung testet die `exportToThirdParty` Marketingaktion mit den im [vorherigen Schritt](#datasets)erhaltenen Datensätzen. Die Anforderungs-Nutzlast ist ein Array, das die IDs der einzelnen Datensätze enthält.

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
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `entityType` | Jedes Element im Payload-Array muss den Typ der zu definierenden Entität angeben. In diesem Anwendungsfall ist der Wert immer „dataSet“. |
| `entityID` | Jedes Element im Payload-Array muss die eindeutige Kennung für einen Datensatz angeben. |

**Antwort**

Eine erfolgreiche Antwort gibt den URI für die Marketingaktion, die von den bereitgestellten Datasets erfassten Datenverwendungsbeschriftungen und eine Liste aller Datenverwendungsrichtlinien zurück, die durch das Testen der Aktion gegen diese Beschriftungen verletzt wurden. In this example, the &quot;Export Data to Third Party&quot; policy is shown in the `violatedPolicies` array, indicating that the marketing action triggered a policy violation.

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
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
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
      "entityId": "5b7c86968f7b6501e21ba9df",
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
| `duleLabels` | Eine Liste von Datenverwendungsbeschriftungen, die aus den bereitgestellten Datensätzen extrahiert wurden. |
| `discoveredLabels` | Eine Liste der Datensätze, die in der Anforderungsnutzlast bereitgestellt wurden, mit den Beschriftungen auf Datensatzebene und auf Feldebene, die in den einzelnen Datensätzen gefunden wurden. |
| `violatedPolicies` | An array listing any data usage policies that were violated by testing the marketing action (specified in `marketingActionRef`) against the provided `duleLabels`. |

Mithilfe der in der API-Antwort zurückgegebenen Daten können Sie Protokolle in Ihrer Erlebnisanwendung einrichten, um Richtlinienverstöße bei deren Auftreten angemessen zu erzwingen.

## Filtern von Datenfeldern

Wenn Ihr Segmentsegment die Auswertung nicht bestanden hat, können Sie die im Audience enthaltenen Daten mit einer der beiden folgenden Methoden anpassen.

### Aktualisieren der Zusammenführungsrichtlinie der Segmentdefinition

Durch Aktualisieren der Zusammenführungsrichtlinie einer Segmentdefinition werden die Datensätze und Felder angepasst, die beim Ausführen des Segmentauftrags einbezogen sind. See the section on [updating an existing merge policy](../../profile/api/merge-policies.md#update) in the API merge policy tutorial for more information.

### Einschränken bestimmter Datenfelder beim Exportieren des Segments

When exporting a segment to a dataset using the [!DNL Segmentation] API, you can filter the data that is included in the export by using the `fields` parameter. Alle diesem Parameter hinzugefügten Datenfelder werden in den Export einbezogen, während alle anderen Datenfelder ausgeschlossen werden.

Stellen Sie sich ein Segment mit Datenfeldern mit den Namen „A“, „B“ und „C“ vor. Wenn Sie nur das Feld „C“ exportieren möchten, enthält der `fields`-Parameter nur das Feld „C“. Auf diese Weise werden die Felder „A“ und „B“ beim Exportieren des Segments ausgeschlossen.

Weitere Informationen finden Sie im Abschnitt [Exportieren eines Segments](./evaluate-a-segment.md#export) im Tutorial zur Segmentierung.

## Nächste Schritte

In diesem Tutorial haben Sie nach den mit einem Zielgruppensegment verknüpften Datennutzungsbezeichnungen gesucht und diese auf Richtlinienverstöße bei bestimmten Marketing-Aktionen getestet. Für weitere Informationen zu [!DNL Data Governance] in [!DNL Experience Platform]lesen Sie bitte die Übersicht für [!DNL Data Governance](../../data-governance/home.md).
