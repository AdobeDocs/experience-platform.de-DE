---
keywords: Experience Platform;Startseite;beliebte Themen;Datenverwendungskonformität;Erzwingen;Erzwingen der Datenverwendungskonformität;Segmentierungsdienst;Segmentierung;Segmentierung;
solution: Experience Platform
title: Erzwingen der Datenverwendungskompatibilität für ein Audiencen-Segment mithilfe von APIs
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial werden die Schritte zur Durchsetzung der Datennutzungskonformität für Zielgruppensegmente von Echtzeit-Kundenprofilen mithilfe von APIs beschrieben.
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 45%

---

# Durchsetzen der Datennutzungskonformität für Zielgruppensegmente mithilfe von APIs

In diesem Lernprogramm werden die Schritte zum Erzwingen der Datenverwendungskonformität für [!DNL Real-time Customer Profile]-Audiencen mithilfe von APIs beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten von [!DNL Adobe Experience Platform]:

- [[!DNL Real-time Customer Profile]](../../profile/home.md):  [!DNL Real-time Customer Profile] ist ein generischer Lookup-Entitätsspeicher und wird zur Verwaltung von  [!DNL Experience Data Model (XDM)] Daten innerhalb von verwendet  [!DNL Platform]. Das Profil führt Daten aus verschiedenen Unternehmensdaten-Assets zusammen und ermöglicht den Zugriff auf diese Daten in einer einheitlichen Darstellung.
   - [Richtlinien](../../profile/api/merge-policies.md) zusammenführen: Regeln,  [!DNL Real-time Customer Profile] mit denen bestimmt wird, welche Daten unter bestimmten Voraussetzungen in einer einheitlichen Ansicht zusammengeführt werden können. Merge-Richtlinien können für [!DNL Data Governance]-Zwecke konfiguriert werden.
- [[!DNL Segmentation]](../home.md): Wie  [!DNL Real-time Customer Profile] unterteilt eine große Gruppe von im Profil Store enthaltenen Personen in kleinere Gruppen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.
- [[!DNL Data Governance]](../../data-governance/home.md):  [!DNL Data Governance] stellt die Infrastruktur für die Kennzeichnung und Durchsetzung von Daten bereit, wobei folgende Komponenten verwendet werden:
   - [Datennutzungsbezeichnungen](../../data-governance/labels/user-guide.md): Bezeichnungen, die zur Beschreibung von Datensätzen und Feldern in Bezug auf die Sensibilität, mit der die jeweiligen Daten verarbeitet werden sollen, verwendet werden.
   - [Datennutzungsrichtlinien](../../data-governance/policies/overview.md): Konfigurationen, die angeben, welche Marketing-Aktionen für Daten zulässig sind, die nach bestimmten Datennutzungsbezeichnungen kategorisiert sind.
   - [Durchsetzung](../../data-governance/enforcement/overview.md) der Politik: Ermöglicht es Ihnen, Datenverwendungsrichtlinien zu erzwingen und Datenvorgänge zu verhindern, die Richtlinienverletzungen darstellen.
- [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um die [!DNL Platform]-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Suchen Sie nach einer Richtlinie zum Zusammenführen für eine Segmentdefinition {#merge-policy}

Dieser Workflow beginnt mit dem Zugriff auf ein bekanntes Zielgruppensegment. Segmente, die für die Verwendung in [!DNL Real-time Customer Profile] aktiviert sind, enthalten eine Richtlinie-ID zum Zusammenführen innerhalb ihrer Segmentdefinition. Diese Zusammenführungsrichtlinie enthält Informationen darüber, welche Datensätze in das Segment eingeschlossen werden sollen, die wiederum alle entsprechenden Beschriftungen zur Datennutzung enthalten.

Mithilfe der API [!DNL Segmentation] können Sie eine Segmentdefinition anhand ihrer ID nachschlagen, um die zugehörige Mergerichtlinie zu finden.

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

Merge-Richtlinien enthalten Informationen zu ihren Quelldatasets, die wiederum Datenverwendungsbeschriftungen enthalten. Sie können die Details einer Zusammenführungsrichtlinie nachschlagen, indem Sie die ID der Zusammenführungsrichtlinie in einer GET an die API [!DNL Profile] übermitteln. Weitere Informationen zu Zusammenführungsrichtlinien finden Sie im [Endpunktleitfaden ](../../profile/api/merge-policies.md) für Zusammenführungsrichtlinien.

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
| `attributeMerge.type` | Der Konfigurationstyp für die Datenpriorität für die Zusammenführungsrichtlinie. Wenn der Wert `dataSetPrecedence` ist, werden die mit dieser Zusammenführungsrichtlinie verknüpften Datensätze unter `attributeMerge > data > order` aufgelistet. Wenn der Wert `timestampOrdered` ist, werden alle Datensätze, die mit dem in `schema.name` referenzierten Schema verknüpft sind, von der Richtlinie verwendet. |
| `attributeMerge.data.order` | Wenn `attributeMerge.type` `dataSetPrecedence` ist, ist dieses Attribut ein Array, das die IDs der von dieser Zusammenführungsrichtlinie verwendeten Datensätze enthält. Diese IDs werden im nächsten Schritt verwendet. |

## Bewerten Sie Datensätze für Richtlinienverletzungen.

>[!NOTE]
>
> Bei diesem Schritt wird davon ausgegangen, dass Sie über mindestens eine aktive Datenverwendungsrichtlinie verfügen, die verhindert, dass bestimmte Marketingaktionen für Daten mit bestimmten Beschriftungen durchgeführt werden. Wenn Sie keine entsprechenden Nutzungsrichtlinien für die zu evaluierenden Datensätze haben, führen Sie das [Lernprogramm zur Richtlinienerstellung](../../data-governance/policies/create.md) durch, um eine zu erstellen, bevor Sie mit diesem Schritt fortfahren.

Nachdem Sie die IDs der Quelldatasets der Richtlinie erhalten haben, können Sie die [Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) verwenden, um diese Datensätze anhand bestimmter Marketingaktionen zu bewerten, um Verstöße gegen die Richtlinien zur Datenverwendung zu prüfen.

Zur Auswertung der Datensätze müssen Sie den Namen der Marketingaktion im Pfad einer Anforderung zur POST angeben und gleichzeitig die Datensatzkennungen im Anforderungstext bereitstellen, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| Parameter | Beschreibung |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | Der Name der Marketingaktion im Zusammenhang mit der Datenverwendungsrichtlinie, nach der Sie die Datensätze bewerten. Je nachdem, ob die Richtlinie von Adobe oder Ihrem Unternehmen definiert wurde, müssen Sie `/marketingActions/core` bzw. `/marketingActions/custom` verwenden. |

**Anfrage**

Die folgende Anforderung testet die Marketingaktion `exportToThirdParty` gegen Datensätze, die im [vorherigen Schritt](#datasets) abgerufen wurden. Die Anforderungs-Nutzlast ist ein Array, das die IDs der einzelnen Datensätze enthält.

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

Eine erfolgreiche Antwort gibt den URI für die Marketingaktion, die von den bereitgestellten Datasets erfassten Datenverwendungsbeschriftungen und eine Liste aller Datenverwendungsrichtlinien zurück, die durch das Testen der Aktion gegen diese Beschriftungen verletzt wurden. In diesem Beispiel wird die Richtlinie &quot;Daten an Dritte exportieren&quot;im Array `violatedPolicies` angezeigt, was angibt, dass die Marketingaktion eine Richtlinienverletzung ausgelöst hat.

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
| `violatedPolicies` | Ein Array, das alle Datenverwendungsrichtlinien auflistet, die durch Testen der Marketingaktion (angegeben in `marketingActionRef`) gegen das bereitgestellte `duleLabels` verletzt wurden. |

Mithilfe der in der API-Antwort zurückgegebenen Daten können Sie Protokolle in Ihrer Erlebnisanwendung einrichten, um Richtlinienverstöße bei deren Auftreten angemessen zu erzwingen.

## Filtern von Datenfeldern

Wenn Ihr Segmentsegment die Auswertung nicht bestanden hat, können Sie die im Audience enthaltenen Daten mit einer der beiden folgenden Methoden anpassen.

### Aktualisieren der Zusammenführungsrichtlinie der Segmentdefinition

Durch Aktualisieren der Zusammenführungsrichtlinie einer Segmentdefinition werden die Datensätze und Felder angepasst, die beim Ausführen des Segmentauftrags einbezogen sind. Weitere Informationen finden Sie im Abschnitt [Aktualisieren einer vorhandenen Mergerichtlinie](../../profile/api/merge-policies.md#update) im Lernprogramm zur API-Zusammenführung.

### Einschränken bestimmter Datenfelder beim Exportieren des Segments

Wenn Sie ein Segment mit der API [!DNL Segmentation] in ein Dataset exportieren, können Sie die im Export enthaltenen Daten mit dem Parameter `fields` filtern. Alle diesem Parameter hinzugefügten Datenfelder werden in den Export einbezogen, während alle anderen Datenfelder ausgeschlossen werden.

Stellen Sie sich ein Segment mit Datenfeldern mit den Namen „A“, „B“ und „C“ vor. Wenn Sie nur das Feld „C“ exportieren möchten, enthält der `fields`-Parameter nur das Feld „C“. Auf diese Weise werden die Felder „A“ und „B“ beim Exportieren des Segments ausgeschlossen.

Weitere Informationen finden Sie im Abschnitt [Exportieren eines Segments](./evaluate-a-segment.md#export) im Tutorial zur Segmentierung.

## Nächste Schritte

In diesem Tutorial haben Sie nach den mit einem Zielgruppensegment verknüpften Datennutzungsbezeichnungen gesucht und diese auf Richtlinienverstöße bei bestimmten Marketing-Aktionen getestet. Weitere Informationen zu [!DNL Data Governance] in [!DNL Experience Platform] finden Sie in der Übersicht für [[!DNL Data Governance]](../../data-governance/home.md).
