---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erzwingen der Datenverwendungskonformität für Audience-Segmente
topic: tutorial
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# Erzwingen Sie die Einhaltung der Datenauslastung für ein Audiencen-Segment mithilfe von APIs

In diesem Lernprogramm werden die Schritte zum Erzwingen der Einhaltung der Datenverwendungskonformität für Kundensegmente in Echtzeit mithilfe von APIs beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Echtzeit-Profil](../../profile/home.md): Echtzeit-Kundendaten-Profil ist ein generischer Lookup-Entitätsspeicher und wird zur Verwaltung von Experience Data Model-(XDM-)Daten innerhalb der Plattform verwendet. Profil führt Daten über verschiedene Unternehmensdaten hinweg zusammen und bietet Zugriff auf diese Daten in einer einheitlichen Darstellung.
   - [Richtlinien](../../profile/api/merge-policies.md)zusammenführen: Regeln, die vom Echtzeit-Kundenkonto verwendet werden, um zu bestimmen, welche Daten unter bestimmten Bedingungen zu einer einheitlichen Ansicht zusammengeführt werden können. Merge-Richtlinien können für Zwecke der Datenverwaltung konfiguriert werden.
- [Segmentierung](../home.md): Wie lange Kundendaten in Echtzeit eine große Gruppe von im Profil Store enthaltenen Personen in kleinere Gruppen unterteilen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.
- [Datenverwaltung](../../data-governance/home.md): Die Datenverwaltung bietet die Infrastruktur für die Kennzeichnung und Durchsetzung der Datenverwendung (DULE) unter Verwendung der folgenden Komponenten:
   - [Datenverwendungsbeschriftungen](../../data-governance/labels/user-guide.md): Bezeichnungen, die zur Beschreibung von Datensätzen und Feldern im Hinblick auf die Empfindlichkeit bei der Verarbeitung ihrer jeweiligen Daten verwendet werden.
   - [Datenverwendungsrichtlinien](../../data-governance/api/getting-started.md): Konfigurationen, die angeben, welche Marketingaktionen für Daten zulässig sind, die durch bestimmte Datenverwendungsbeschriftungen kategorisiert wurden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Plattform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchführen zu können, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

> [!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Eine Richtlinie zum Zusammenführen für eine Segmentdefinition suchen

Dieser Arbeitsablauf beginnt mit dem Zugriff auf ein bekanntes Audiencen-Segment. Segmente, die für die Verwendung im Echtzeit-Kundensegment aktiviert sind, enthalten eine Richtlinie-ID zum Zusammenführen innerhalb ihrer Segmentdefinition. Diese Richtlinie zum Zusammenführen enthält Informationen darüber, welche Datensätze in das Segment eingeschlossen werden sollen, die wiederum alle entsprechenden Beschriftungen zur Datenverwendung enthalten.

Mithilfe der [Segmentierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)können Sie eine Segmentdefinition anhand ihrer ID suchen, um die zugehörige Zusammenführungsrichtlinie zu finden.

**API-Format**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | Die ID der Segmentdefinition, die Sie suchen möchten. |

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

## Suchen Sie die Quelldatasets aus der Richtlinie zum Zusammenführen

Merge-Richtlinien enthalten Informationen zu ihren Quelldatasets, die wiederum Doppel-Beschriftungen enthalten. Sie können die Details einer Zusammenführungsrichtlinie nachschlagen, indem Sie die ID der Zusammenführungsrichtlinie in einer GET-Anforderung an die Profil-API angeben.

**API-Format**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | Die ID der im [vorherigen Schritt](#lookup-a-merge-policy-for-a-segment-definition)abgerufenen Zusammenführungsrichtlinie. |

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

## Suchdatenverwendungsbeschriftungen für die Quelldatasets

Nachdem Sie die IDs der Quelldatasets der Richtlinie zusammengeführt haben, können Sie mit diesen IDs die für die Datasets selbst konfigurierten Datenverwendungsbeschriftungen und alle darin enthaltenen Datenfelder suchen.

Mit dem folgenden Aufruf der [Katalogdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) werden die mit einem Datensatz verknüpften Datenverwendungsbeschriftungen abgerufen, indem die ID im Anforderungspfad angegeben wird:

**API-Format**

```http
GET /dataSets/{DATASET_ID}/dule
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{DATASET_ID}` | Die ID des Datensatzes, dessen Datenverwendungsbeschriftungen Sie nachschlagen möchten. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b95b155419ec801e6eee780/dule \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Datenverwendungsbeschriftungen zurück, die mit dem Datensatz als Ganzes verknüpft sind, sowie alle mit dem Quelldatenfeld verknüpften Datenfelder.

```json
{
    "connection": {},
    "dataset": {
        "identity": [],
        "contract": [
            "C3"
        ],
        "sensitive": [],
        "contracts": [
            "C3"
        ],
        "identifiability": [],
        "specialTypes": []
    },
    "fields": [],
    "schemaFields": [
        {
            "path": "/properties/personalEmail/properties/address",
            "identity": [
                "I1"
            ],
            "contract": [
                "C2",
                "C9"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C9"
            ],
            "identifiability": [
                "I1"
            ],
            "specialTypes": []
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `dataset` | Ein Objekt, das die Datenverwendungsbeschriftungen enthält, die auf den Datensatz als Ganzes angewendet werden. |
| `schemaFields` | Ein Array von Objekten, die bestimmte Schema-Felder darstellen, auf die Datenverwendungsbeschriftungen angewendet wurden. |
| `schemaFields.path` | Der Pfad des Schema-Felds, dessen Datenverwendungsbeschriftungen im selben Objekt aufgeführt sind. |

## Datenfelder filtern

> [!NOTE] Dieser Schritt ist optional. Wenn Sie die im Segment enthaltenen Daten nicht auf Grundlage Ihrer Ergebnisse im vorherigen Schritt der [Suche nach Datenverwendungsbeschriftungen](#lookup-data-usage-labels-for-the-source-datasets)anpassen möchten, können Sie den letzten Schritt der [Auswertung der Daten auf Richtlinienverletzungen](#evaluate-data-for-policy-violations)überspringen.

Wenn Sie die im Segmentsegment der Audience enthaltenen Daten anpassen möchten, können Sie dies mit einer der beiden folgenden Methoden tun:

### Aktualisieren der Richtlinie zum Zusammenführen der Segmentdefinition

Beim Aktualisieren der Richtlinie zum Zusammenführen einer Segmentdefinition werden die Datensätze und Felder angepasst, die beim Ausführen des Segmentauftrags einbezogen werden. Weitere Informationen finden Sie im Abschnitt zum [Aktualisieren einer vorhandenen Zusammenführungsrichtlinie](../../profile/api/merge-policies.md) im Lernprogramm zur Zusammenführung.

### Beim Exportieren des Segments bestimmte Datenfelder beschränken

Beim Exportieren eines Segments in ein Dataset mit der Echtzeit-Kunden-Profil-API können Sie die im Export enthaltenen Daten mithilfe des `fields` Parameters filtern. Alle diesem Parameter hinzugefügten Datenfelder werden in den Export einbezogen, während alle anderen Datenfelder ausgeschlossen werden.

Betrachten Sie ein Segment mit Datenfeldern mit den Namen &quot;A&quot;, &quot;B&quot;und &quot;C&quot;. Wenn Sie nur das Feld &quot;C&quot;exportieren möchten, enthält der `fields` Parameter nur das Feld &quot;C&quot;. Dadurch werden die Felder &quot;A&quot;und &quot;B&quot;beim Exportieren des Segments ausgeschlossen.

Weitere Informationen finden Sie im Abschnitt zum [Exportieren eines Segments](./evaluate-a-segment.md#export-a-segment) im Segmentierungstraining.

## Daten für Richtlinienverletzungen auswerten

Nachdem Sie nun die mit Ihrem Segmentsegment verknüpften Datenverwendungsbeschriftungen gesammelt haben, können Sie diese Bezeichnungen mit Marketingaktionen testen, um Verstöße gegen die Richtlinien zur Datenverwendung zu bewerten. Ausführliche Anweisungen zum Durchführen von Richtlinienbewertungen mit der [DUL Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)finden Sie im Dokument zur [Richtlinienbewertung](../../data-governance/enforcement/overview.md).

## Nächste Schritte

Indem Sie diesem Tutorial folgen, haben Sie die mit einem Audiencen-Segment verknüpften Datenverwendungsbeschriftungen nachgeschlagen und sie auf Richtlinienverletzungen gegen bestimmte Marketingaktionen getestet. Weitere Informationen zur Datenverwaltung in Experience Platform finden Sie in der Übersicht über die [Datenverwaltung](../../data-governance/home.md).