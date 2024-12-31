---
solution: Experience Platform
title: Erzwingen der Einhaltung von Datennutzungsregeln für ein Zielgruppensegment mithilfe von APIs
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Durchsetzen von Segmentdefinitionen zur Datennutzungskonformität mithilfe von APIs beschrieben.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: 914174de797d7d5f6c47769d75380c0ce5685ee2
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 42%

---

# Erzwingen der Einhaltung von Datennutzungsregeln für eine Segmentdefinition mithilfe von APIs

In diesem Tutorial werden die Schritte zum Durchsetzen der Datennutzungskonformität für Segmentdefinitionen mithilfe von APIs beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von [!DNL Adobe Experience Platform] voraus.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): [!DNL Real-Time Customer Profile] ist ein generischer Lookup-Entitätsspeicher und wird zur Verwaltung [!DNL Experience Data Model (XDM)] Daten in [!DNL Platform] verwendet. Das Profil führt Daten aus verschiedenen Unternehmensdaten-Assets zusammen und ermöglicht den Zugriff auf diese Daten in einer einheitlichen Darstellung.
   - [Zusammenführungsrichtlinien](../../profile/api/merge-policies.md): Regeln, mit denen [!DNL Real-Time Customer Profile] bestimmen, welche Daten unter bestimmten Bedingungen zu einer vereinigten Ansicht zusammengeführt werden können. Zusammenführungsrichtlinien können für Data Governance-Zwecke konfiguriert werden.
- [[!DNL Segmentation]](../home.md): Wie [!DNL Real-Time Customer Profile] eine große Gruppe von Personen im Profilspeicher in kleinere Gruppen mit ähnlichen Eigenschaften unterteilt, die ähnlich auf Marketing-Strategien reagieren.
- [Data Governance](../../data-governance/home.md): Data Governance bietet die Infrastruktur für Datennutzungskennzeichnungen und -durchsetzung, wobei die folgenden Komponenten verwendet werden:
   - [Datennutzungsbezeichnungen](../../data-governance/labels/user-guide.md): Bezeichnungen, die zur Beschreibung von Datensätzen und Feldern in Bezug auf die Sensibilität, mit der die jeweiligen Daten verarbeitet werden sollen, verwendet werden.
   - [Datennutzungsrichtlinien](../../data-governance/policies/overview.md): Konfigurationen, die angeben, welche Marketing-Aktionen für Daten zulässig sind, die nach bestimmten Datennutzungsbezeichnungen kategorisiert sind.
   - [Richtliniendurchsetzung](../../data-governance/enforcement/overview.md): Ermöglicht die Durchsetzung von Datennutzungsrichtlinien und die Verhinderung von Datenvorgängen, bei denen Richtlinien verletzt werden.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Platform]-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Suchen einer Zusammenführungsrichtlinie für eine Segmentdefinition {#merge-policy}

Dieser Workflow beginnt mit dem Zugriff auf eine bekannte Segmentdefinition. Segmentdefinitionen, die für die Verwendung in aktiviert sind, [!DNL Real-Time Customer Profile] eine Zusammenführungsrichtlinien-ID in ihrer Segmentdefinition enthalten. Diese Zusammenführungsrichtlinie enthält Informationen darüber, welche Datensätze in die Segmentdefinition aufgenommen werden sollen, die wiederum alle anwendbaren Datennutzungskennzeichnungen enthalten.

Mithilfe der [!DNL Segmentation]-API können Sie eine Segmentdefinition anhand ihrer ID nachschlagen, um die zugehörige Zusammenführungsrichtlinie zu finden.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrgId": "{ORG_ID}",
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

Zusammenführungsrichtlinien enthalten Informationen über die Quelldatensätze, die wiederum Datennutzungsbeschriftungen enthalten. Sie können die Details einer Zusammenführungsrichtlinie nachschlagen, indem Sie die Zusammenführungsrichtlinien-ID in einer GET-Anfrage an die [!DNL Profile]-API angeben. Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im [Handbuch zu Zusammenführungsrichtlinien-Endpunkten](../../profile/api/merge-policies.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Zusammenführungsrichtlinie zurück.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
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
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schema.name` | Der Name des Schemas, das der Zusammenführungsrichtlinie zugeordnet ist. |
| `attributeMerge.type` | Der Konfigurationstyp für die Datenpriorität für die Zusammenführungsrichtlinie. Wenn der Wert `dataSetPrecedence` ist, werden die mit dieser Zusammenführungsrichtlinie verknüpften Datensätze unter `attributeMerge > data > order` aufgelistet. Wenn der Wert `timestampOrdered` ist, werden alle Datensätze, die mit dem in `schema.name` referenzierten Schema verknüpft sind, von der Richtlinie verwendet. |
| `attributeMerge.data.order` | Wenn `attributeMerge.type` `dataSetPrecedence` ist, ist dieses Attribut ein Array, das die IDs der von dieser Zusammenführungsrichtlinie verwendeten Datensätze enthält. Diese IDs werden im nächsten Schritt verwendet. |

## Auswerten von Datensätzen auf Richtlinienverletzungen

>[!NOTE]
>
> Bei diesem Schritt wird davon ausgegangen, dass Sie über mindestens eine aktive Datennutzungsrichtlinie verfügen, die verhindert, dass bestimmte Marketing-Aktionen für Daten mit bestimmten Kennzeichnungen ausgeführt werden. Wenn Sie keine anwendbaren Nutzungsrichtlinien für die Datensätze haben, die ausgewertet werden, befolgen Sie bitte das [Tutorial zur Richtlinienerstellung](../../data-governance/policies/create.md) um eine zu erstellen, bevor Sie mit diesem Schritt fortfahren.

Nachdem Sie die IDs der Quelldatensätze der Zusammenführungsrichtlinie abgerufen haben, können Sie die [Policy Service-API](https://www.adobe.io/experience-platform-apis/references/policy-service/) verwenden, um diese Datensätze mit bestimmten Marketing-Aktionen zu bewerten, um Verstöße gegen Datennutzungsrichtlinien festzustellen.

Um die Datensätze auszuwerten, müssen Sie den Namen der Marketing-Aktion im Pfad einer POST-Anfrage angeben und dabei die Datensatz-IDs im Anfrageinhalt angeben, wie im folgenden Beispiel dargestellt.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketing-Aktion, die mit der Datennutzungsrichtlinie verknüpft ist, nach der Sie die Datensätze bewerten. Je nachdem, ob die Richtlinie durch Adobe oder Ihr Unternehmen definiert wurde, müssen Sie `/marketingActions/core` bzw. `/marketingActions/custom` verwenden. |

**Anfrage**

Die folgende Anfrage testet die `exportToThirdParty` Marketing-Aktion mit Datensätzen, die im [ Schritt abgerufen ](#datasets). Die Anfrage-Payload ist ein Array, das die IDs der einzelnen Datensätze enthält.

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

Bei einer erfolgreichen Antwort werden der URI für die Marketing-Aktion, die Datennutzungskennzeichnungen, die aus den bereitgestellten Datensätzen gesammelt wurden, und eine Liste aller Datennutzungsrichtlinien zurückgegeben, die beim Testen der Aktion hinsichtlich dieser Kennzeichnungen verletzt wurden. In diesem Beispiel wird die Richtlinie „Daten an Dritte exportieren“ im `violatedPolicies`-Array angezeigt, was darauf hinweist, dass die Marketing-Aktion einen Richtlinienverstoß ausgelöst hat.

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
| `duleLabels` | Eine Liste von Datennutzungskennzeichnungen, die aus den bereitgestellten Datensätzen extrahiert wurden. |
| `discoveredLabels` | Eine Liste der Datensätze, die in der Payload der Anfrage angegeben wurden; angezeigt werden die in den einzelnen Datensätzen gefundenen Kennzeichnungen auf Datensatzebene und Feldebene. |
| `violatedPolicies` | Ein Array, das alle Datennutzungsrichtlinien auflistet, die durch Testen der Marketing-Aktion (angegeben in `marketingActionRef`) hinsichtlich der angegebenen `duleLabels` verletzt wurden. |

Mithilfe der in der API-Antwort zurückgegebenen Daten können Sie Protokolle in Ihrer Erlebnisanwendung einrichten, um Richtlinienverletzungen bei ihrem Auftreten angemessen durchzusetzen.

## Filtern von Datenfeldern

Wenn die Segmentdefinition die Auswertung nicht besteht, können Sie die in der Segmentdefinition enthaltenen Daten durch eine der beiden unten beschriebenen Methoden anpassen.

### Aktualisieren der Zusammenführungsrichtlinie der Segmentdefinition

Durch Aktualisieren der Zusammenführungsrichtlinie einer Segmentdefinition werden die Datensätze und Felder angepasst, die beim Ausführen des Segmentauftrags einbezogen sind. Weitere Informationen finden Sie im Abschnitt [Aktualisieren einer vorhandenen Zusammenführungsrichtlinie](../../profile/api/merge-policies.md#update) im Tutorial API-Zusammenführungsrichtlinie .

### Beschränken bestimmter Datenfelder beim Exportieren der Segmentdefinition

Beim Exportieren einer Segmentdefinition in einen Datensatz mithilfe der [!DNL Segmentation]-API können Sie die im Export enthaltenen Daten mithilfe des `fields`-Parameters filtern. Alle diesem Parameter hinzugefügten Datenfelder werden in den Export einbezogen, während alle anderen Datenfelder ausgeschlossen werden.

Stellen Sie sich eine Segmentdefinition vor, die Datenfelder mit den Namen „A“, „B“ und „C“ enthält. Wenn Sie nur das Feld „C“ exportieren möchten, enthält der `fields`-Parameter nur das Feld „C“. Dadurch würden die Felder „A“ und „B“ beim Exportieren der Segmentdefinition ausgeschlossen.

Weitere Informationen finden Sie im Abschnitt [Exportieren ](./evaluate-a-segment.md#export) Segmentdefinition“ im Segmentierungs-Tutorial.

## Nächste Schritte

In diesem Tutorial haben Sie die mit einer Segmentdefinition verbundenen Datennutzungskennzeichnungen nachgeschlagen und sie auf Richtlinienverletzungen bei bestimmten Marketing-Aktionen getestet. Weitere Informationen zu Data Governance in [!DNL Experience Platform] finden Sie in der Übersicht zu [Data Governance](../../data-governance/home.md).
