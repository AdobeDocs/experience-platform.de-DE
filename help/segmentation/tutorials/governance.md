---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erzwingen der Datenverwendungskonformität für Audiencen-Segmente
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 2%

---


# Erzwingen Sie die Einhaltung der Datenauslastung für ein Audiencen-Segment mithilfe von APIs

In diesem Lernprogramm werden die Schritte zum Erzwingen der Einhaltung der Datenverwendungskonformität für Kundensegmente in Echtzeit mithilfe von APIs beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Echtzeit-Profil](../../profile/home.md): Echtzeit-Kundendaten-Profil ist ein generischer Lookup-Entitätsspeicher und wird zur Verwaltung von Erlebnisdatenmodelldaten (XDM) innerhalb der Platform verwendet. Profil führt Daten über verschiedene Unternehmensdaten hinweg zusammen und bietet Zugriff auf diese Daten in einer einheitlichen Darstellung.
   - [Richtlinien](../../profile/api/merge-policies.md)zusammenführen: Regeln, die vom Echtzeit-Kundenkonto verwendet werden, um zu bestimmen, welche Daten unter bestimmten Bedingungen zu einer einheitlichen Ansicht zusammengeführt werden können. Merge-Richtlinien können für Zwecke der Datenverwaltung konfiguriert werden.
- [Segmentierung](../home.md): Wie lange Kundendaten in Echtzeit eine große Gruppe von im Profil Store enthaltenen Personen in kleinere Gruppen unterteilen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.
- [Datenverwaltung](../../data-governance/home.md): Die Datenverwaltung bietet die Infrastruktur für die Kennzeichnung und Durchsetzung der Datenverwendung (DULE) unter Verwendung der folgenden Komponenten:
   - [Datenverwendungsbeschriftungen](../../data-governance/labels/user-guide.md): Bezeichnungen, die zur Beschreibung von Datensätzen und Feldern im Hinblick auf die Empfindlichkeit bei der Verarbeitung ihrer jeweiligen Daten verwendet werden.
   - [Datenverwendungsrichtlinien](../../data-governance/policies/overview.md): Konfigurationen, die angeben, welche Marketingaktionen für Daten zulässig sind, die durch bestimmte Datenverwendungsbeschriftungen kategorisiert wurden.
   - [Durchsetzung](../../data-governance/enforcement/overview.md)der Politik: Ermöglicht es Ihnen, Datenverwendungsrichtlinien zu erzwingen und Datenvorgänge zu verhindern, die Richtlinienverletzungen darstellen.
- [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platformen-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

### Werte für erforderliche Kopfzeilen sammeln

Um Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in der Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Eine Richtlinie zum Zusammenführen für eine Segmentdefinition suchen {#merge-policy}

Dieser Arbeitsablauf beginnt mit dem Zugriff auf ein bekanntes Audiencen-Segment. Segmente, die für die Verwendung im Echtzeit-Kundensegment aktiviert sind, enthalten eine Richtlinie-ID zum Zusammenführen innerhalb ihrer Segmentdefinition. Diese Richtlinie zum Zusammenführen enthält Informationen darüber, welche Datensätze in das Segment eingeschlossen werden sollen, die wiederum alle entsprechenden Beschriftungen zur Datenverwendung enthalten.

Mithilfe der [Segmentierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)können Sie eine Segmentdefinition anhand ihrer ID nachschlagen, um die zugehörige Mergerichtlinie zu finden.

**API-Format**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | Die ID der Segmentdefinition, die Sie nachschlagen möchten. |

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
| `mergePolicyId` | Die ID der für die Segmentdefinition verwendeten Mergerichtlinie. Dies wird im nächsten Schritt verwendet. |

## Suchen Sie die Quelldatasets aus der Richtlinie zum Zusammenführen {#datasets}

Merge-Richtlinien enthalten Informationen zu ihren Quelldatasets, die wiederum Datenverwendungsbeschriftungen enthalten. Sie können die Details einer Zusammenführungsrichtlinie nachschlagen, indem Sie die ID der Zusammenführungsrichtlinie in einer GET-Anforderung an die Profil-API angeben.

**API-Format**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | Die ID der im [vorherigen Schritt](#merge-policy)abgerufenen Zusammenführungsrichtlinie. |

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

Eine erfolgreiche Antwort gibt die Details der Mergerichtlinie zurück.

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
| `schema.name` | Der Name des Schemas, das mit der Zusammenführungsrichtlinie verknüpft ist. |
| `attributeMerge.type` | Der Konfigurationstyp für die Datenpriorität für die Zusammenführungsrichtlinie. Wenn der Wert `dataSetPrecedence`angegeben ist, werden die mit dieser Zusammenführungsrichtlinie verknüpften Datensätze unter `attributeMerge > data > order`. Ist der Wert `timestampOrdered`der Wert, werden alle Datensätze, die mit dem Schema verknüpft sind, auf das in der Zusammenführungsrichtlinie verwiesen `schema.name` wird, von der Richtlinie verwendet. |
| `attributeMerge.data.order` | Ist dies der `attributeMerge.type` Fall `dataSetPrecedence`, ist dieses Attribut ein Array, das die IDs der von dieser Zusammenführungsrichtlinie verwendeten Datensätze enthält. Diese IDs werden im nächsten Schritt verwendet. |

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
| `entityType` | Jedes Element im Payload-Array muss den Typ der zu definierenden Entität angeben. In diesem Anwendungsfall ist der Wert immer &quot;dataSet&quot;. |
| `entityID` | Jedes Element im Payload-Array muss die eindeutige ID für einen Datensatz bereitstellen. |

**Antwort**

Eine erfolgreiche Antwort gibt den URI für die Marketingaktion, die von den bereitgestellten Datasets erfassten Datenverwendungsbeschriftungen und eine Liste aller Datenverwendungsrichtlinien zurück, die durch das Testen der Aktion gegen diese Beschriftungen verletzt wurden. In diesem Beispiel wird die Richtlinie &quot;Daten an Dritte exportieren&quot;im `violatedPolicies` Array angezeigt, was angibt, dass die Marketingaktion eine Richtlinienverletzung ausgelöst hat.

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
| `violatedPolicies` | Ein Array, das alle Datenverwendungsrichtlinien auflistet, die durch Testen der (in `marketingActionRef`) Marketingaktion gegen die bereitgestellte `duleLabels`Variable verletzt wurden. |

Mithilfe der in der API-Antwort zurückgegebenen Daten können Sie Protokolle in Ihrer Erlebnisanwendung einrichten, um Richtlinienverstöße bei deren Auftreten angemessen zu erzwingen.

## Datenfelder filtern

Wenn Ihr Segmentsegment die Auswertung nicht bestanden hat, können Sie die im Audience enthaltenen Daten mit einer der beiden folgenden Methoden anpassen.

### Aktualisieren der Richtlinie zum Zusammenführen der Segmentdefinition

Beim Aktualisieren der Richtlinie zum Zusammenführen einer Segmentdefinition werden die Datensätze und Felder angepasst, die beim Ausführen des Segmentauftrags einbezogen werden. Weitere Informationen finden Sie im Abschnitt zum [Aktualisieren einer vorhandenen Richtlinie](../../profile/api/merge-policies.md#update) für die Zusammenführung der API im Tutorial zur API-Zusammenführung.

### Beim Exportieren des Segments bestimmte Datenfelder beschränken

Beim Exportieren eines Segments in ein Dataset mit der Echtzeit-Kunden-Profil-API können Sie die im Export enthaltenen Daten mithilfe des `fields` Parameters filtern. Alle diesem Parameter hinzugefügten Datenfelder werden in den Export einbezogen, während alle anderen Datenfelder ausgeschlossen werden.

Betrachten Sie ein Segment mit Datenfeldern mit den Namen &quot;A&quot;, &quot;B&quot;und &quot;C&quot;. Wenn Sie nur das Feld &quot;C&quot;exportieren möchten, enthält der `fields` Parameter nur das Feld &quot;C&quot;. Dadurch werden die Felder &quot;A&quot;und &quot;B&quot;beim Exportieren des Segments ausgeschlossen.

Weitere Informationen finden Sie im Abschnitt zum [Exportieren eines Segments](./evaluate-a-segment.md#export) im Segmentierungstraining.

## Nächste Schritte

Indem Sie diesem Tutorial folgen, haben Sie die mit einem Audiencen-Segment verknüpften Datenverwendungsbeschriftungen nachgeschlagen und sie auf Richtlinienverletzungen gegen bestimmte Marketingaktionen getestet. Weitere Informationen zur Datenverwaltung in der Experience Platform finden Sie in der Übersicht über die [Datenverwaltung](../../data-governance/home.md).
