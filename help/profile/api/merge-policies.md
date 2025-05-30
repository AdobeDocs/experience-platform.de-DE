---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;
title: API-Endpunkt für Zusammenführungsrichtlinien
type: Documentation
description: Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich eine vollständige Ansicht über jeden einzelnen Ihrer Kunden verschaffen können. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen Experience Platform bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine einheitliche Ansicht zu schaffen.
role: Developer
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 63%

---

# Endpunkt für Zusammenführungsrichtlinien

Mit Adobe Experience Platform können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich eine vollständige Ansicht über jeden einzelnen Ihrer Kunden verschaffen können. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen [!DNL Experience Platform] bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden sollen, um eine einheitliche Ansicht zu schaffen.

Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihre Organisation über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Experience Platform aufgenommen werden, werden sie zusammengeführt, sodass ein einziges Profil für diesen Kunden entsteht. Wenn die Daten aus mehreren Quellen in Konflikt stehen (z. B. listet ein Fragment den Kunden als „ledig“ auf, während ein anderes den Kunden als „verheiratet“ auflistet), bestimmt die Zusammenführungsrichtlinie, welche Informationen priorisiert und in das Profil für die Einzelperson aufgenommen werden sollen.

Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. Dieses Handbuch enthält Schritte zum Arbeiten mit Zusammenführungsrichtlinien unter Verwendung der -API.

Informationen zum Arbeiten mit Zusammenführungsrichtlinien über die Benutzeroberfläche von finden Sie im [Handbuch zur Benutzeroberfläche der Zusammenführungsrichtlinien](../merge-policies/ui-guide.md). Um mehr über Zusammenführungsrichtlinien im Allgemeinen und ihre Rolle in Experience Platform zu erfahren, lesen Sie zunächst die [Übersicht über Zusammenführungsrichtlinien](../merge-policies/overview.md).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil von [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, schauen Sie bitte im Handbuch in [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Komponenten von Zusammenführungsrichtlinien {#components-of-merge-policies}

Zusammenführungsrichtlinien gelten für Ihre Organisation als privat, sodass Sie verschiedene Richtlinien erstellen können, um Schemas auf die gewünschte Weise zusammenzuführen. Jede API, die auf [!DNL Profile] Daten zugreift, erfordert eine Zusammenführungsrichtlinie. Es wird jedoch eine Standardrichtlinie verwendet, wenn keine explizite Angabe erfolgt. [!DNL Experience Platform] stellt Organisationen eine standardmäßige Zusammenführungsrichtlinie bereit. Sie können aber auch eine Zusammenführungsrichtlinie für eine bestimmte Schemaklasse des Experience-Datenmodells (XDM) erstellen und als Standard für Ihre Organisation festlegen.

Während jede Organisation potenziell mehrere Zusammenführungsrichtlinien pro Schemaklasse haben kann, kann jede Klasse nur eine standardmäßige Zusammenführungsrichtlinie haben. Jede als Standard festgelegte Zusammenführungsrichtlinie wird in Fällen verwendet, in denen der Name der Schemaklasse angegeben wird und eine Zusammenführungsrichtlinie erforderlich, aber nicht angegeben ist.

>[!NOTE]
>
>Wenn Sie eine neue Zusammenführungsrichtlinie als Standard festlegen, wird jede vorhandene Zusammenführungsrichtlinie, die zuvor als Standard festgelegt wurde, automatisch aktualisiert und nicht mehr als Standard verwendet.

Um sicherzustellen, dass alle Profilnutzer in den Randbereichen mit derselben Ansicht arbeiten, können Zusammenführungsrichtlinien als am Rand aktiv markiert werden. Damit eine Zielgruppe in Edge aktiviert (als Edge-Zielgruppe markiert) werden kann, muss sie an eine Zusammenführungsrichtlinie gebunden sein, die als in Edge aktiv markiert ist. Wenn eine Zielgruppe **nicht** mit einer Zusammenführungsrichtlinie verknüpft ist, die als im Randbereich aktiv markiert ist, wird die Zielgruppe nicht als im Randbereich aktiv, sondern als Streaming-Zielgruppe markiert.

Darüber hinaus kann jede Organisation nur über **eine** Zusammenführungsrichtlinie verfügen, die im Randbereich aktiv ist. Wenn eine Zusammenführungsrichtlinie im Randbereich aktiv ist, kann sie für andere Randsysteme verwendet werden, z. B. für das Edge-Profil, die Edge-Segmentierung und Ziele in Edge.

### Komplettes Zusammenführungsrichtlinienobjekt

Ein komplettes Zusammenführungsrichtlinienobjekt stellt einen Satz von Voreinstellungen dar, die bestimmte Aspekte beim Zusammenführen von Profilfragmenten steuern.

**Zusammenführungsrichtlinienobjekt**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Eigenschaft | Beschreibung |
|---|---|
| `id` | Die vom System erzeugte eindeutige Kennung, die zur Erstellungszeit zugewiesen wurde |
| `name` | Anzeigename, anhand dessen die Zusammenführungsrichtlinie in Listenansichten identifiziert werden kann. |
| `imsOrgId` | Organisationskennung, zu der diese Zusammenführungsrichtlinie gehört |
| `schema.name` | Als Teil des [`schema`](#schema)-Objekts enthält das `name` die XDM-Schemaklasse, auf die sich die Zusammenführungsrichtlinie bezieht. Weitere Informationen zu Schemata und Klassen finden Sie in der [XDM-Dokumentation](../../xdm/home.md). |
| `version` | [!DNL Experience Platform] gepflegte Version der Zusammenführungsrichtlinie. Dieser schreibgeschützte Wert wird beim Aktualisieren einer Zusammenführungsrichtlinie inkrementiert. |
| `identityGraph` | [Identitätsdiagramm](#identity-graph)-Objekt, das das Identitätsdiagramm angibt, aus dem verwandte Identitäten abgerufen werden. Profilfragmente, die für alle verwandten Identitäten gefunden wurden, werden zusammengeführt. |
| `attributeMerge` | [Attributzusammenführung](#attribute-merge) Objekt, das angibt, wie die Zusammenführungsrichtlinie Profilattribute im Falle von Datenkonflikten priorisiert. |
| `isActiveOnEdge` | Boolescher Wert, der angibt, ob diese Zusammenführungsrichtlinie im Randbereich verwendet werden kann. Standardmäßig ist dieser Wert `false`. |
| `default` | Boolescher Wert, der angibt, ob diese Zusammenführungsrichtlinie für das angegebene Schema standardmäßig verwendet wird. |
| `updateEpoch` | Datum der letzten Aktualisierung der Zusammenführungsrichtlinie. |

**Beispielhafte Zusammenführungsrichtlinie**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Identitätsdiagramm {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md) verwaltet die global und für jede Organisation verwendeten Identitätsdiagramme [!DNL Experience Platform]. Das `identityGraph`-Attribut der Zusammenführungsrichtlinie definiert, wie die verwandten Identitäten für einen Anwender bestimmt werden.

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

### Zusammenführung von Attributen {#attribute-merge}

Ein Profilfragment besteht aus den Profildaten nur einer Identität aus der Liste an Identitäten, die für einen bestimmten Anwender vorhanden sind. Wenn der verwendete Identitätsdiagrammtyp zu mehr als einer Identität führt, besteht die Möglichkeit von widersprüchlichen Profilattributen, und die Priorität muss angegeben werden. Mit `attributeMerge` können Sie angeben, welche Profilattribute im Falle eines Zusammenführungskonflikts zwischen Datensätzen vom Typ „Schlüsselwert (Datensatzdaten)“ priorisiert werden sollen.

**attributeMerge-Objekt**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Wobei `{ATTRIBUTE_MERGE_TYPE}` einer der folgenden Werte ist:

* **`timestampOrdered`**: (Standard) Dem zuletzt aktualisierten Profil Priorität einräumen. Bei diesem Zusammenführungstyp ist das `data`-Attribut nicht erforderlich.
* **`dataSetPrecedence`**: Geben Sie Profilfragmenten Priorität, basierend auf dem Datensatz, aus dem sie stammen. Dies kann hilfreich sein, wenn in einem Datensatz vorhandene Daten bevorzugt oder im Vergleich zu Daten in einem anderen Datensatz als vertrauenswürdiger eingestuft werden. Bei Verwendung dieses Zusammenführungstyps ist das `order`-Attribut erforderlich, da es die Datensätze in der Reihenfolge der Priorität auflistet.
   * **`order`**: Wenn „dataSetPrecedence“ verwendet wird, muss ein `order`-Array mit einer Liste von Datensätzen bereitgestellt werden. Datensätze, die nicht in der Liste enthalten sind, werden nicht zusammengeführt. Anders ausgedrückt: Datensätze müssen explizit aufgeführt werden, um in einem Profil zusammengeführt zu werden. Das `order`-Array listet die Kennungen der Datensätze in der Reihenfolge ihrer Priorität auf.

#### Beispiel `attributeMerge` ein Objekt mit `dataSetPrecedence` Typ

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### Beispiel `attributeMerge` ein Objekt mit `timestampOrdered` Typ

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

Das Schemaobjekt gibt die Schemaklasse des Experience-Datenmodells (XDM) an, für die diese Zusammenführungsrichtlinie erstellt wird.

**`schema`-Objekt**

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

Um mehr über XDM und das Arbeiten mit Schemata in Experience Platform zu erfahren, lesen Sie zunächst die [XDM-Systemübersicht](../../xdm/home.md).

## Zugriff auf Zusammenführungsrichtlinien {#access-merge-policies}

Mithilfe der [!DNL Real-Time Customer Profile]-API können Sie mit dem `/config/mergePolicies`-Endpunkt eine Suchanfrage ausführen, um eine bestimmte Zusammenführungsrichtlinie anhand ihrer ID anzuzeigen oder auf alle Zusammenführungsrichtlinien in Ihrer Organisation zuzugreifen, die nach bestimmten Kriterien gefiltert wurden. Sie können auch den `/config/mergePolicies/bulk-get`-Endpunkt verwenden, um mehrere Zusammenführungsrichtlinien anhand ihrer IDs abzurufen. Die Schritte zum Ausführen dieser Aufrufe werden in den folgenden Abschnitten beschrieben.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Zusammenführungsrichtlinie zurück.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

Einzelheiten zu den einzelnen Elementen, aus denen eine Zusammenführungsrichtlinie besteht, finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies) am Anfang dieses Dokuments.

### Abrufen mehrerer Zusammenführungsrichtlinien anhand ihrer IDs

Sie können mehrere Zusammenführungsrichtlinien abrufen, indem Sie eine POST-Anfrage an den `/config/mergePolicies/bulk-get`-Endpunkt senden und die IDs der Zusammenführungsrichtlinien, die Sie abrufen möchten, in den Anfragetext aufnehmen.

**API-Format**

```http
POST /config/mergePolicies/bulk-get
```

**Anfrage**

Der Anfragetext enthält ein „ids“-Array mit einzelnen Objekten, die die „id“ für jede Zusammenführungsrichtlinie enthalten, für die Details abgerufen werden sollen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Bei einer erfolgreichen Antwort werden der HTTP-Status 207 (Multi-Status) und die Details der Zusammenführungsrichtlinien zurückgegeben, deren IDs in der POST-Anfrage angegeben wurden.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Einzelheiten zu den einzelnen Elementen, aus denen eine Zusammenführungsrichtlinie besteht, finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies) am Anfang dieses Dokuments.

### Mehrere Zusammenführungsrichtlinien anhand von Kriterien auflisten

Sie können mehrere Zusammenführungsrichtlinien in Ihrer Organisation auflisten, indem Sie eine GET-Anfrage an den `/config/mergePolicies`-Endpunkt senden und optionale Abfrageparameter verwenden, um die Antwort zu filtern, zu sortieren und zu paginieren. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (&amp;) voneinander getrennt werden. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Zusammenführungsrichtlinien abgerufen.

**API-Format**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
|---|---|
| `default` | Ein boolescher Wert, der Ergebnisse anhand der Frage filtert, ob die Zusammenführungsrichtlinien Standard für eine Schemaklasse sind oder nicht. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die auf einer Seite enthalten sind. Standardwert: 20 |
| `orderBy` | Gibt das Feld an, nach dem Ergebnisse sortiert werden sollen (mit `orderBy=name` oder `orderBy=+name`, um anhand der Namen in aufsteigender Reihenfolge zu sortieren, oder mit `orderBy=-name`, um in absteigender Reihenfolge zu sortieren). Wird dieser Wert nicht angegeben, erfolgt die Standardsortierung von `name` in aufsteigender Reihenfolge. |
| `isActiveOnEdge` | Ein boolescher Wert, der die Ergebnisse danach filtert, ob die Zusammenführungsrichtlinien im Randbereich aktiv sind oder nicht. |
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "isActiveOnEdge": true,
    "default": true
}'
```

| Eigenschaft | Beschreibung |
|---|---|
| `name` | Ein verständlicher Name, mit dem die Zusammenführungsrichtlinie in Listenansichten identifiziert werden kann. |
| `identityGraph.type` | Der Identitätsdiagrammtyp, aus dem zusammenzuführende verwandte Identitäten abgerufen werden sollen. Mögliche Werte: „none“ (keine) und „pdg“ (privates Diagramm). |
| `attributeMerge` | Die Art und Weise, wie Profilattributwerte bei Datenkonflikten priorisiert werden. |
| `schema` | Die XDM-Schemaklasse, die der Zusammenführungsrichtlinie zugeordnet ist. |
| `isActiveOnEdge` | Gibt an, ob diese Zusammenführungsrichtlinie im Randbereich aktiv ist. |
| `default` | Gibt an, ob diese Zusammenführungsrichtlinie der Standard für das Schema ist. |

Weiterführende Informationen finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies).

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Zusammenführungsrichtlinie zurück.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Gibt den zu verwendenden Vorgang an. Beispiele für andere PATCH-Vorgänge finden Sie in der [JSON-Patch-Dokumentation](https://datatracker.ietf.org/doc/html/rfc6902). |
| `path` | Der Pfad des zu aktualisierenden Felds. Akzeptierte Werte sind: &quot;/name“, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version“, &quot;/default“, &quot;/isActiveOnEdge“ |
| `value` | Der Wert, auf den das angegebene Feld gesetzt werden soll. |

Weiterführende Informationen finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies).


**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu aktualisierten Zusammenführungsrichtlinie zurück.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": true,
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `name` | Ein verständlicher Name, mit dem die Zusammenführungsrichtlinie in Listenansichten identifiziert werden kann. |
| `identityGraph` | Das Identitätsdiagramm, aus dem zusammenzuführende verwandte Identitäten abgerufen werden sollen. |
| `attributeMerge` | Die Art und Weise, wie Profilattributwerte bei Datenkonflikten priorisiert werden. |
| `schema` | Die XDM-Schemaklasse, die der Zusammenführungsrichtlinie zugeordnet ist. |
| `isActiveOnEdge` | Gibt an, ob diese Zusammenführungsrichtlinie im Randbereich aktiv ist. |
| `default` | Gibt an, ob diese Zusammenführungsrichtlinie der Standard für das Schema ist. |

Weiterführende Informationen finden Sie im Abschnitt [Komponenten von Zusammenführungsrichtlinien](#components-of-merge-policies).

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Zusammenführungsrichtlinie zurück.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## Zusammenführungsrichtlinie löschen

Sie können eine Zusammenführungsrichtlinie löschen, indem Sie eine DELETE-Anfrage an den `/config/mergePolicies`-Endpunkt senden und die Kennung der Zusammenführungsrichtlinie, die Sie löschen möchten, im Anfragepfad einschließen.

>[!NOTE]
>
>Wenn die Zusammenführungsrichtlinie auf „true“ festgelegt `isActiveOnEdge`, kann **Zusammenführungsrichtlinie (**) gelöscht werden. Verwenden Sie entweder die Endpunkte [PATCH](#edit-individual-merge-policy-fields) oder [PUT](#overwrite-a-merge-policy), um die Zusammenführungsrichtlinie zu aktualisieren, bevor Sie sie löschen.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Bei erfolgreicher Löschanfrage werden der HTTP-Status 200 (OK) und ein leerer Antworttext zurückgegeben. Um zu überprüfen, ob der Löschvorgang erfolgreich war, können Sie eine GET-Anfrage ausführen, um die Zusammenführungsrichtlinie anhand ihrer Kennung anzuzeigen. Wenn die Zusammenführungsrichtlinie gelöscht wurde, erhalten Sie einen Fehler vom Typ HTTP-Status 404 (Nicht gefunden).

## Nächste Schritte

Nachdem Sie nun wissen, wie Zusammenführungsrichtlinien für Ihr Unternehmen erstellt und konfiguriert werden, können Sie sie verwenden, um die Ansicht von Kundenprofilen in Experience Platform anzupassen und aus Ihren [!DNL Real-Time Customer Profile] Zielgruppen zu erstellen.

Weitere Informationen zum Definieren und Verwenden von Zielgruppen finden [&#128279;](../../segmentation/home.md) in der Dokumentation zum Adobe Experience Platform-Segmentierungs-Service.
