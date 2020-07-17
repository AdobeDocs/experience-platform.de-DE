---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Richtlinien zusammenführen - Echtzeit-Client-Profil-API
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '2035'
ht-degree: 85%

---


# Endpunkt der Richtlinien zusammenführen

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich einen kompletten Überblick über einzelne Kunden verschaffen können. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view. Über RESTful-APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihre Organisation einrichten. In diesem Handbuch werden die Schritte zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API beschrieben. Informationen zum Arbeiten mit Zusammenführungsrichtlinien unter Verwendung der Benutzeroberfläche finden Sie im [Benutzerhandbuch für Zusammenführungsrichtlinien](../ui/merge-policies.md).

## Erste Schritte

The API endpoint used in this guide is part of the [!DNL Real-time Customer Profile API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Bevor Sie fortfahren, lesen Sie bitte die [Anleitung](getting-started.md) zu den ersten Schritten für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu den erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer beliebigen [!DNL Experience Platform] API erforderlich sind.

## Komponenten von Zusammenführungsrichtlinien {#components-of-merge-policies}

Zusammenführungsrichtlinien gelten jeweils privat für Ihre IMS-Organisation, sodass Sie verschiedene Richtlinien erstellen können, um Schemas auf die gewünschte Weise zusammenzuführen. Any API accessing [!DNL Profile] data requires a merge policy, though a default will be used if one is not explicitly provided. [!DNL Platform] bietet eine standardmäßige Zusammenführungsrichtlinie; alternativ können Sie eine Zusammenführungsrichtlinie für ein bestimmtes Schema erstellen und diese dann als Standard für Ihre Organisation markieren. Jede Organisation kann potenziell über mehrere Zusammenführungsrichtlinien pro Schema verfügen, allerdings kann jedes Schema nur eine Standardzusammenführungsrichtlinie haben. Alle als Standard festgelegten Zusammenführungsrichtlinien werden verwendet, wenn der Schemaname angegeben und eine Zusammenführungsrichtlinie erforderlich, jedoch nicht angegeben ist. Wenn Sie eine Zusammenführungsrichtlinie als Standard festlegen, werden alle vorhandenen Zusammenführungsrichtlinien, die zuvor als Standard festgelegt wurden, automatisch aktualisiert, sodass sie nicht mehr als Standard dienen.

### Komplettes Zusammenführungsrichtlinienobjekt

Ein komplettes Zusammenführungsrichtlinienobjekt stellt einen Satz von Voreinstellungen dar, die bestimmte Aspekte beim Zusammenführen von Profilfragmenten steuern.

**Zusammenführungsrichtlinienobjekt**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Eigenschaft | Beschreibung |
|---|---|
| `id` | Die vom System erzeugte eindeutige Kennung, die zur Erstellungszeit zugewiesen wurde |
| `name` | Anzeigename, anhand dessen die Zusammenführungsrichtlinie in Listenansichten identifiziert werden kann. |
| `imsOrgId` | Organisationskennung, zu der diese Zusammenführungsrichtlinie gehört |
| `identityGraph` | [Identitätsdiagramm](#identity-graph)-Objekt, das das Identitätsdiagramm angibt, aus dem verwandte Identitäten abgerufen werden. Profilfragmente, die für alle verwandten Identitäten gefunden wurden, werden zusammengeführt. |
| `attributeMerge` | [Attributzusammenführungs](#attribute-merge)-Objekt, das angibt, wie die Zusammenführungsrichtlinie Profilattributwerte bei Datenkonflikten priorisiert. |
| `schema` | Das [Schema](#schema)-Objekt, für das die Zusammenführungsrichtlinie verwendet werden kann. |
| `default` | Boolescher Wert, der angibt, ob diese Zusammenführungsrichtlinie für das angegebene Schema standardmäßig verwendet wird. |
| `version` | [!DNL Platform]Von gepflegte Version der Zusammenführungsrichtlinie. Dieser schreibgeschützte Wert wird beim Aktualisieren einer Zusammenführungsrichtlinie inkrementiert. |
| `updateEpoch` | Datum der letzten Aktualisierung der Zusammenführungsrichtlinie. |

**Beispielhafte Zusammenführungsrichtlinie**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Identitätsdiagramm {#identity-graph}

[Der Identitätsdienst](../../identity-service/home.md) für Adobe Experience Platformen verwaltet die weltweit verwendeten Identitätsdiagramme und für jedes Unternehmen auf [!DNL Experience Platform]. Das `identityGraph`-Attribut der Zusammenführungsrichtlinie definiert, wie die verwandten Identitäten für einen Anwender bestimmt werden.

**identityGraph-Objekt**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Wobei `{IDENTITY_GRAPH_TYPE}` einer der folgenden Werte ist:

* **„none“:** Keine Identitätszusammenfügung durchführen.
* **„pdg“:** Identitätszusammenfügung basierend auf Ihrem privaten Identitätsdiagramm durchführen.

**Beispiel`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Attributzusammenführung {#attribute-merge}

Ein Profilfragment besteht aus den Profildaten nur einer Identität aus der Liste an Identitäten, die für einen bestimmten Anwender vorhanden sind. Wenn der verwendete Identitätsdiagrammtyp mehr als eine Identität ergibt, kann es sein, dass Werte für Profileigenschaften miteinander in Konflikt stehen und die Priorität angegeben werden muss. Mithilfe von `attributeMerge` können Sie festlegen, welche Datensatzprofilwerte bei einem Zusammenführungskonflikt priorisiert werden sollen.

**attributeMerge-Objekt**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Wobei `{ATTRIBUTE_MERGE_TYPE}` einer der folgenden Werte ist:

* **„timestampOrdered“**: (Standard) Räumt dem zuletzt aktualisierten Profil im Konfliktfall Priorität ein. Bei diesem Zusammenführungstyp ist das `data`-Attribut nicht erforderlich.
* **„dataSetPrecedence“**: Räumt Profilfragmenten je nach dem Datensatz, aus dem sie stammen, Priorität ein. Dies kann hilfreich sein, wenn in einem Datensatz vorhandene Daten bevorzugt oder im Vergleich zu Daten in einem anderen Datensatz als vertrauenswürdiger eingestuft werden. Bei Verwendung dieses Zusammenführungstyps ist das `order`-Attribut erforderlich, da es die Datensätze in der Reihenfolge der Priorität auflistet.
   * **„order“**: Wenn „dataSetPrecedence“ verwendet wird, muss ein `order`-Array mit einer Liste von Datensätzen angegeben werden. Datensätze, die nicht in der Liste enthalten sind, werden nicht zusammengeführt. Anders ausgedrückt: Datensätze müssen explizit aufgeführt werden, um in einem Profil zusammengeführt zu werden. Das `order`-Array listet die Kennungen der Datensätze in der Reihenfolge ihrer Priorität auf.

**Beispiel für ein attributeMerge-Objekt mit dataSetPrecedence-Typ**

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

**Beispiel für ein attributeMerge-Objekt mit timestampOrdered-Typ**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

Das Schemaobjekt gibt das XDM-Schema an, für das diese Zusammenführungsrichtlinie erstellt wird.

**`schema`-Objekt **

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Wobei der Wert `name` der Name der XDM-Klasse ist, auf der das der Zusammenführungsrichtlinie zugeordnete Schema basiert.

**Beispiel`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

## Zusammenführungsrichtlinien aufrufen {#access-merge-policies}

Using the [!DNL Real-time Customer Profile] API, the `/config/mergePolicies` endpoint allows you perform a lookup request to view a specific merge policy by its ID, or access all of the merge policies in your IMS Organization, filtered by specific criteria. Sie können den `/config/mergePolicies/bulk-get` Endpunkt auch verwenden, um mehrere Zusammenführungsrichtlinien nach ihren IDs abzurufen. Die Schritte für die Durchführung dieser Aufrufe sind in den folgenden Abschnitten beschrieben.

### Auf eine einzelne Zusammenführungsrichtlinie anhand der Kennung zugreifen

Sie können auf eine einzelne Zusammenführungsrichtlinie anhand ihrer Kennung zugreifen, indem Sie eine GET-Anfrage an den `/config/mergePolicies`-Endpunkt senden und die `mergePolicyId` im Anfragepfad einschließen.

**API-Format**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschreibung |
|---|---|
| `{mergePolicyId}` | Die Kennung der Zusammenzuführungsrichtlinie, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Zusammenführungsrichtlinie zurück.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

Einzelheiten zu den einzelnen Elementen, aus denen eine Zusammenführungsrichtlinie besteht, finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies) am Anfang dieses Dokuments.

### Abrufen mehrerer Zusammenführungsrichtlinien nach ihren IDs

Sie können mehrere Zusammenführungsrichtlinien abrufen, indem Sie eine POST-Anforderung an den `/config/mergePolicies/bulk-get` Endpunkt senden und die IDs der Zusammenführungsrichtlinien einschließen, die Sie im Anforderungstext abrufen möchten.

**API-Format**

```http
POST /config/mergePolicies/bulk-get
```

**Anfrage**

Der Anforderungstext enthält ein &quot;ids&quot;-Array mit einzelnen Objekten, die die &quot;id&quot; für jede Zusammenführungsrichtlinie enthalten, für die Sie Details abrufen möchten.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**Antwort**

Bei einer erfolgreichen Antwort werden HTTP-Status 207 (Multi-Status) und die Details der Zusammenführungsrichtlinien zurückgegeben, deren IDs in der POST-Anforderung bereitgestellt wurden.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Einzelheiten zu den einzelnen Elementen, aus denen eine Zusammenführungsrichtlinie besteht, finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies) am Anfang dieses Dokuments.

### Mehrere Zusammenführungsrichtlinien anhand von Kriterien auflisten

Sie können verschiedene Zusammenführungsrichtlinien innerhalb Ihrer IMS-Organisation auflisten, indem Sie eine GET-Anfrage an den `/config/mergePolicies`-Endpunkt richten und optionale Abfrageparameter zum Filtern, Sortieren und Paginieren der Antwort verwenden. Es können mehrere Parameter eingeschlossen werden, getrennt durch das kaufmännische Und-Zeichen (&amp;). Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Zusammenführungsrichtlinien abgerufen.

**API-Format**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
|---|---|
| `default` | Ein boolescher Wert, der Ergebnisse anhand der Frage filtert, ob die Zusammenführungsrichtlinien Standard für eine Schemaklasse sind oder nicht. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu begrenzen, die in einer Seite enthalten sind. Standardwert: 20 |
| `orderBy` | Gibt das Feld an, anhand dessen Ergebnisse sortiert werden sollen (mit `orderBy=name` oder `orderBy=+name`, um anhand der Namen in aufsteigender Reihenfolge zu sortieren, oder mit `orderBy=-name`, um in absteigender Reihenfolge zu sortieren). Wird dieser Wert nicht angegeben, erfolgt die Standardsortierung von `name` in aufsteigender Reihenfolge. |
| `schema.name` | Name des Schemas, für das verfügbare Zusammenführungsrichtlinien abgerufen werden sollen. |
| `identityGraph.type` | Filtert Ergebnisse anhand des Identitätsdiagrammtyps. Mögliche Werte sind „none“ (keine) und „pdg“ (privates Diagramm). |
| `attributeMerge.type` | Filtert Ergebnisse anhand des verwendeten Attributzusammenführungstyps. Mögliche Werte sind „timestampOrdered“ und „dataSetPrecedence“. |
| `start` | Seitenversatz: Gibt die Startkennung für abzurufende Daten an. Standardwert: 0 |
| `version` | Legen Sie den Wert fest, wenn Sie eine bestimmte Version der Zusammenführungsrichtlinie verwenden möchten. Standardmäßig kommt die neueste Version zum Einsatz. |

Weiterführende Informationen zu `schema.name`, `identityGraph.type` und `attributeMerge.type` finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies) weiter oben in diesem Handbuch.


**Anfrage**

Die folgende Anfrage listet alle Zusammenführungsrichtlinien für ein bestimmtes Schema auf:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Antwort**

Eine erfolgreiche Antwort gibt eine paginierte Liste mit Zusammenführungsrichtlinien zurück, die den Kriterien, die mit den in der Anfrage gesendeten Abfrageparametern festgelegt wurden, entsprechen.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `_links.next.href` | Eine URI-Adresse für die nächste Ergebnisseite. Verwenden Sie diesen URI als Anfrageparameter für einen anderen API-Aufruf an denselben Endpunkt, um die Seite anzuzeigen. Wenn keine nächste Seite vorhanden ist, ist dieser Wert eine leere Zeichenfolge. |

## Zusammenführungsrichtlinie erstellen

Sie können eine neue Zusammenführungsrichtlinie für Ihre Organisation erstellen, indem Sie eine POST-Anfrage an den `/config/mergePolicies`-Endpunkt senden.

**API-Format**

```http
POST /config/mergePolicies
```

**Anfrage** Die folgende Anfrage erstellt eine neue Zusammenführungsrichtlinie, die durch die in der Payload angegebenen Attributwerte konfiguriert wird:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| Eigenschaft | Beschreibung |
|---|---|
| `name` | Ein verständlicher Name, mit dem die Zusammenführungsrichtlinie in Listenansichten identifiziert werden kann. |
| `identityGraph.type` | Der Identitätsdiagrammtyp, aus dem zusammenzuführende verwandte Identitäten abgerufen werden sollen. Mögliche Werte: „none“ (keine) und „pdg“ (privates Diagramm). |
| `attributeMerge` | Die Art und Weise, wie Profilattributwerte bei Datenkonflikten priorisiert werden. |
| `schema` | Die XDM-Schemaklasse, die der Zusammenführungsrichtlinie zugeordnet ist. |
| `default` | Gibt an, ob diese Zusammenführungsrichtlinie der Standard für das Schema ist. |

Weiterführende Informationen finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies).

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Zusammenführungsrichtlinie zurück.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

Einzelheiten zu den einzelnen Elementen, aus denen eine Zusammenführungsrichtlinie besteht, finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies) am Anfang dieses Dokuments.

## Zusammenführungsrichtlinie aktualisieren {#update}

Sie können eine vorhandene Zusammenführungsrichtlinie ändern, indem Sie einzelne Attribute bearbeiten (PATCH) oder die gesamte Zusammenführungsrichtlinie mit neuen Attributen überschreiben (PUT). Nachfolgend sind entsprechende Beispiele aufgeführt.

### Einzelne Felder einer Zusammenführungsrichtlinie bearbeiten

Sie können einzelne Felder einer Zusammenführungsrichtlinie bearbeiten, indem Sie eine PATCH-Anfrage an den `/config/mergePolicies/{mergePolicyId}`-Endpunkt senden:

**API-Format**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschreibung |
|---|---|
| `{mergePolicyId}` | Die Kennung der Zusammenzuführungsrichtlinie, die Sie löschen möchten. |

**Anfrage**

Mit der folgenden Anfrage wird eine angegebene Zusammenführungsrichtlinie aktualisiert, indem der Wert ihrer `default`-Eigenschaft in `true` geändert wird:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `op` | Gibt den zu verwendenden Vorgang an. Beispiele für andere PATCH-Vorgänge finden Sie in der [JSON-Patch-Dokumentation](http://jsonpatch.com). |
| `path` | Der Pfad des zu aktualisierenden Felds. Zulässige Werte sind: „/name“, „/identityGraph.type“, „/attributeMerge.type“, „/schema.name“, „/version“ und „/default“. |
| `value` | Der Wert, auf den das angegebene Feld gesetzt werden soll. |

Weiterführende Informationen finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies).


**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu aktualisierten Zusammenführungsrichtlinie zurück.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

### Zusammenführungsrichtlinie überschreiben

Eine andere Möglichkeit zum Ändern einer Zusammenführungsrichtlinie besteht darin, eine PUT-Anfrage zu verwenden, um die gesamte Zusammenführungsrichtlinie zu überschreiben.

**API-Format**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschreibung |
|---|---|
| `{mergePolicyId}` | Die Kennung der Zusammenzuführungsrichtlinie, die Sie überschreiben möchten. |

**Anfrage**

Die folgende Anfrage überschreibt die angegebene Zusammenführungsrichtlinie und ersetzt ihre Attributwerte durch die in der Payload angegebenen Werte. Da diese Anfrage eine vorhandene Zusammenführungsrichtlinie vollständig ersetzt, müssen Sie alle Felder festlegen, die beim ursprünglichen Definieren der Zusammenführungsrichtlinie erforderlich waren. Hier geben Sie jedoch für die Felder, die Sie ändern möchten, aktualisierte Werte an.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `name` | Ein anwenderfreundlicher Name, anhand dessen die Zusammenführungsrichtlinie in Listenansichten identifiziert werden kann. |
| `identityGraph` | Das Identitätsdiagramm, aus dem zusammenzuführende verwandte Identitäten abgerufen werden sollen. |
| `attributeMerge` | Die Art und Weise, wie Profilattributwerte bei Datenkonflikten priorisiert werden. |
| `schema` | Die XDM-Schemaklasse, die der Zusammenführungsrichtlinie zugeordnet ist. |
| `default` | Gibt an, ob diese Zusammenführungsrichtlinie der Standard für das Schema ist. |

Weiterführende Informationen finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies).


**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Zusammenführungsrichtlinie zurück.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

## Zusammenführungsrichtlinie löschen

Sie können eine Zusammenführungsrichtlinie löschen, indem Sie eine DELETE-Anfrage an den `/config/mergePolicies`-Endpunkt senden und die Kennung der Zusammenführungsrichtlinie, die Sie löschen möchten, im Anfragepfad einschließen.

**API-Format**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschreibung |
|---|---|
| `{mergePolicyId}` | Die Kennung der Zusammenzuführungsrichtlinie, die Sie löschen möchten. |

**Anfrage**

Mit der folgenden Anfrage wird eine Zusammenführungsrichtlinie gelöscht.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Löschanfrage gibt den HTTP-Status 200 (OK) und einen leeren Antworttext zurück. Um zu überprüfen, ob der Löschvorgang erfolgreich war, können Sie eine GET-Anfrage ausführen, um die Zusammenführungsrichtlinie anhand ihrer Kennung anzuzeigen. Wenn die Zusammenführungsrichtlinie gelöscht wurde, erhalten Sie einen Fehler vom Typ HTTP-Status 404 (Nicht gefunden).

## Nächste Schritte

Now that you know how to create and configure merge policies for your IMS Organization, you can use them to create audience segments from your [!DNL Real-time Customer Profile] data. Informationen zum Definieren und Verwenden von Segmenten finden Sie in der Dokumentation zu [Adobe Experience Platform Segmentation Service](../../segmentation/home.md).



