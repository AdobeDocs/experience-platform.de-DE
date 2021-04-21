---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API
title: API-Endpunkt "Richtlinien zusammenführen"
topic-legacy: guide
type: Documentation
description: Mit Adobe Experience Platform können Sie Datenfragmente aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige Ansicht Ihrer einzelnen Kunden zu erhalten. Beim Zusammenführen dieser Daten sind Zusammenführungsrichtlinien die Regeln, die Plattform verwendet, um zu bestimmen, wie Daten priorisiert werden und welche Daten kombiniert werden, um eine einheitliche Ansicht zu erstellen.
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2560'
ht-degree: 54%

---

# Endpunkt der Richtlinien zusammenführen

Mit Adobe Experience Platform können Sie Datenfragmente aus mehreren Quellen zusammenführen und kombinieren, um eine vollständige Ansicht Ihrer einzelnen Kunden zu erhalten. Beim Zusammenführen dieser Daten sind Zusammenführungsrichtlinien die Regeln, die [!DNL Platform] verwenden, um zu bestimmen, wie Daten priorisiert werden und welche Daten kombiniert werden, um eine einheitliche Ansicht zu erstellen.

Wenn ein Kunde beispielsweise über mehrere Kanal mit Ihrer Marke interagiert, enthält Ihr Unternehmen mehrere Profil-Fragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen angezeigt werden. Wenn diese Fragmente in eine Plattform integriert werden, werden sie zusammengeführt, um ein einzelnes Profil für diesen Kunden zu erstellen. Wenn die Daten aus mehreren Quellen in Konflikt geraten (z. B. ein Fragment als &quot;Single&quot;, während die anderen Listen als &quot;verheiratet&quot;Liste werden), bestimmt die Richtlinie zum Zusammenführen, welche Informationen in das Profil für die betreffende Person aufgenommen werden sollen.

Über die RESTful APIs oder die Benutzeroberfläche können Sie neue Zusammenführungsrichtlinien erstellen, vorhandene Richtlinien verwalten und eine standardmäßige Zusammenführungsrichtlinie für Ihr Unternehmen einrichten. In diesem Handbuch werden die Schritte zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der API beschrieben.

Informationen zum Arbeiten mit Zusammenführungsrichtlinien mithilfe der Benutzeroberfläche finden Sie im Handbuch [Richtlinien zusammenführen](../ui/merge-policies.md).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil von [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Komponenten von Zusammenführungsrichtlinien {#components-of-merge-policies}

Merge-Richtlinien sind privat für Ihre IMS-Organisation, sodass Sie verschiedene Richtlinien erstellen können, um Schema auf die von Ihnen gewünschte Weise zusammenzuführen. Für alle API-Zugriffe auf [!DNL Profile]-Daten ist eine Zusammenführungsrichtlinie erforderlich. Eine Standardeinstellung wird verwendet, wenn keine explizite Angabe erfolgt. [!DNL Platform] stellt Unternehmen eine standardmäßige Zusammenführungsrichtlinie zur Verfügung oder Sie können eine Zusammenführungsrichtlinie für eine bestimmte Experience Data Model (XDM)-Schema-Klasse erstellen und diese als Standard für Ihr Unternehmen markieren.

Während jedes Unternehmen potenziell über mehrere Zusammenführungsrichtlinien pro Schema-Klasse verfügen kann, kann jede Klasse nur eine Standardzusammenführungsrichtlinie haben. Alle als Standard festgelegten Zusammenführungsrichtlinien werden verwendet, wenn der Name der Schema-Klasse angegeben ist und eine Zusammenführungsrichtlinie erforderlich ist, jedoch nicht angegeben.

>[!NOTE]
>
>Wenn Sie eine neue Mergerichtlinie als Standard festlegen, werden alle vorhandenen Mergerichtlinien, die zuvor als Standard festgelegt wurden, automatisch aktualisiert und nicht mehr als Standard verwendet.

### Komplettes Zusammenführungsrichtlinienobjekt

Ein komplettes Zusammenführungsrichtlinienobjekt stellt einen Satz von Voreinstellungen dar, die bestimmte Aspekte beim Zusammenführen von Profilfragmenten steuern.

**Zusammenführungsrichtlinienobjekt**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
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
| `attributeMerge` | [Attribute ](#attribute-merge) mergeobject, das angibt, wie die Richtlinie zum Zusammenführen bei Datenkonflikten Profil-Attribute priorisiert. |
| `schema.name` | Als Teil des Objekts [`schema`](#schema) enthält das Feld `name` die XDM-Schema-Klasse, auf die sich die Richtlinie zum Zusammenführen bezieht. Weitere Informationen zu Schemas und Klassen finden Sie in der [XDM-Dokumentation](../../xdm/home.md). |
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

[Adobe Experience Platform Identity ](../../identity-service/home.md) Servicemanagement verwaltet die weltweit verwendeten Identitätsdiagramme und deren Verwendung für jedes Unternehmen  [!DNL Experience Platform]. Das `identityGraph`-Attribut der Zusammenführungsrichtlinie definiert, wie die verwandten Identitäten für einen Anwender bestimmt werden.

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

Ein Profilfragment besteht aus den Profildaten nur einer Identität aus der Liste an Identitäten, die für einen bestimmten Anwender vorhanden sind. Wenn der verwendete Identitätsdiagrammtyp zu mehr als einer Identität führt, besteht die Möglichkeit kollidierender Profil-Attribute, und die Priorität muss angegeben werden. Mit `attributeMerge` können Sie angeben, welche Profil-Attribute im Ereignis eines Zusammenführungskonflikts zwischen Schlüsselwertdatasets (Datensatzdaten) priorisiert werden sollen.

**attributeMerge-Objekt**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Wobei `{ATTRIBUTE_MERGE_TYPE}` einer der folgenden Werte ist:

* **`timestampOrdered`**: (Standard) Geben Sie dem zuletzt aktualisierten Profil Priorität. Bei diesem Zusammenführungstyp ist das `data`-Attribut nicht erforderlich. `timestampOrdered` unterstützt auch benutzerdefinierte Zeitstempel, die beim Zusammenführen von Profil-Fragmenten innerhalb von oder über Datensätze Vorrang haben. Weitere Informationen finden Sie im Abschnitt Anhang zu [mit benutzerdefinierten Zeitstempeln](#custom-timestamps).
* **`dataSetPrecedence`** : Weisen Sie Fragmenten des Profils Priorität auf der Grundlage des Datensatzes zu, aus dem sie stammen. Dies kann hilfreich sein, wenn in einem Datensatz vorhandene Daten bevorzugt oder im Vergleich zu Daten in einem anderen Datensatz als vertrauenswürdiger eingestuft werden. Bei Verwendung dieses Zusammenführungstyps ist das `order`-Attribut erforderlich, da es die Datensätze in der Reihenfolge der Priorität auflistet.
   * **`order`**: Wenn &quot;dataSetPrecedence&quot;verwendet wird, muss ein  `order` Array mit einer Liste von Datensätzen bereitgestellt werden. Datensätze, die nicht in der Liste enthalten sind, werden nicht zusammengeführt. Anders ausgedrückt: Datensätze müssen explizit aufgeführt werden, um in einem Profil zusammengeführt zu werden. Das `order`-Array listet die Kennungen der Datensätze in der Reihenfolge ihrer Priorität auf.

#### Beispiel für ein `attributeMerge`-Objekt mit `dataSetPrecedence`-Typ

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

#### Beispiel für ein `attributeMerge`-Objekt mit `timestampOrdered`-Typ

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

Das Schema-Objekt gibt die Experience Data Model (XDM)-Schema-Klasse an, für die diese Zusammenführungsrichtlinie erstellt wird.

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

Um mehr über XDM zu erfahren und mit Schemas in der Experience Platform zu arbeiten, lesen Sie zunächst den [XDM Systemüberblick](../../xdm/home.md).

## Zusammenführungsrichtlinien aufrufen {#access-merge-policies}

Mit der API [!DNL Real-time Customer Profile] können Sie mit dem Endpunkt `/config/mergePolicies` eine Suchanfrage ausführen, um eine bestimmte Richtlinie für die Zusammenführung nach ihrer ID Ansicht oder auf alle Zusammenführungsrichtlinien in Ihrer IMS-Organisation zuzugreifen, gefiltert nach bestimmten Kriterien. Sie können auch den Endpunkt `/config/mergePolicies/bulk-get` verwenden, um mehrere Zusammenführungsrichtlinien nach ihren IDs abzurufen. Die Schritte für die Durchführung dieser Aufrufe sind in den folgenden Abschnitten beschrieben.

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

Sie können mehrere Zusammenführungsrichtlinien abrufen, indem Sie eine POST an den `/config/mergePolicies/bulk-get`-Endpunkt anfordern und die IDs der Zusammenführungsrichtlinien einschließen, die Sie im Anforderungstext abrufen möchten.

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

Eine erfolgreiche Antwort gibt HTTP-Status 207 (Multi-Status) und die Details der Zusammenführungsrichtlinien zurück, deren IDs in der POST-Anforderung bereitgestellt wurden.

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

Sie können verschiedene Zusammenführungsrichtlinien innerhalb Ihrer IMS-Organisation auflisten, indem Sie eine GET-Anfrage an den `/config/mergePolicies`-Endpunkt richten und optionale Abfrageparameter zum Filtern, Sortieren und Paginieren der Antwort verwenden. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (&amp;) voneinander getrennt werden. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren Zusammenführungsrichtlinien abgerufen.

**API-Format**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
|---|---|
| `default` | Ein boolescher Wert, der Ergebnisse anhand der Frage filtert, ob die Zusammenführungsrichtlinien Standard für eine Schemaklasse sind oder nicht. |
| `limit` | Gibt die maximale Seitengröße an, um die Anzahl der Ergebnisse zu steuern, die auf einer Seite enthalten sind. Standardwert: 20 |
| `orderBy` | Gibt das Feld an, nach dem Ergebnisse sortiert werden sollen (mit `orderBy=name` oder `orderBy=+name`, um anhand der Namen in aufsteigender Reihenfolge zu sortieren, oder mit `orderBy=-name`, um in absteigender Reihenfolge zu sortieren). Wird dieser Wert nicht angegeben, erfolgt die Standardsortierung von `name` in aufsteigender Reihenfolge. |
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
| `name` | Ein verständlicher Name, mit dem die Zusammenführungsrichtlinie in Listenansichten identifiziert werden kann. |
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

Bei erfolgreicher Löschanfrage werden der HTTP-Status 200 (OK) und ein leerer Antworttext zurückgegeben. Um zu überprüfen, ob der Löschvorgang erfolgreich war, können Sie eine GET-Anfrage ausführen, um die Zusammenführungsrichtlinie anhand ihrer Kennung anzuzeigen. Wenn die Zusammenführungsrichtlinie gelöscht wurde, erhalten Sie einen Fehler vom Typ HTTP-Status 404 (Nicht gefunden).

## Nächste Schritte

Da Sie nun wissen, wie Sie Zusammenführungsrichtlinien für Ihr Unternehmen erstellen und konfigurieren, können Sie diese verwenden, um die Ansicht von Profilen innerhalb der Plattform anzupassen und Audiencen aus Ihren [!DNL Real-time Customer Profile]-Daten zu erstellen. Informationen zum Definieren und Verwenden von Segmenten finden Sie in der Dokumentation zu [Adobe Experience Platform Segmentation Service](../../segmentation/home.md).

## Anhang

Dieser Abschnitt enthält zusätzliche Informationen zum Arbeiten mit Zusammenführungsrichtlinien.

### Verwenden benutzerdefinierter Zeitstempel {#custom-timestamps}

Da Datensätze in die Experience Platform aufgenommen werden, wird zum Zeitpunkt der Erfassung ein Systemzeitstempel abgerufen und dem Datensatz hinzugefügt. Wenn `timestampOrdered` als `attributeMerge`-Typ für eine Zusammenführungsrichtlinie ausgewählt ist, werden Profil basierend auf dem Systemzeitstempel zusammengeführt. Das heißt, das Zusammenführen erfolgt auf der Grundlage des Zeitstempels für den Zeitpunkt, zu dem der Datensatz in die Plattform aufgenommen wurde.

Gelegentlich kann es zu Anwendungsfällen kommen, z. B. zum Aufstocken von Daten oder zum Sicherstellen der richtigen Reihenfolge von Ereignissen, wenn Datensätze nicht in der richtigen Reihenfolge aufgenommen werden, wenn ein benutzerdefinierter Zeitstempel angegeben werden muss und die Richtlinie zum Zusammenführen den benutzerdefinierten Zeitstempel und nicht den Systemzeitstempel berücksichtigen muss.

Um einen benutzerdefinierten Zeitstempel zu verwenden, muss das [[!DNL External Source System Audit Details Mixin]](#mixin-details) Ihrem Profil-Schema hinzugefügt werden. Nach dem Hinzufügen kann der benutzerdefinierte Zeitstempel mithilfe des Felds `xdm:lastUpdatedDate` ausgefüllt werden. Wenn ein Datensatz mit dem ausgefüllten Feld `xdm:lastUpdatedDate` erfasst wird, verwendet die Experience Platform dieses Feld, um Datensätze oder Profil-Fragmente innerhalb und zwischen Datensätzen zusammenzuführen. Wenn `xdm:lastUpdatedDate` nicht vorhanden oder nicht gefüllt ist, verwendet die Plattform weiterhin den Systemzeitstempel.

>[!NOTE]
>
>Sie müssen sicherstellen, dass der Zeitstempel `xdm:lastUpdatedDate` aufgefüllt wird, wenn eine PATCH in demselben Datensatz gesendet wird.

Eine schrittweise Anleitung zum Arbeiten mit Schemas mithilfe der Schema Registry API, einschließlich des Hinzufügens von Mixins zu Schemas, finden Sie im Lehrgang [zum Erstellen eines Schemas mit der API](../../xdm/tutorials/create-schema-api.md).

Informationen zum Arbeiten mit benutzerdefinierten Zeitstempeln mithilfe der Benutzeroberfläche finden Sie im Abschnitt [Verwenden von benutzerdefinierten Zeitstempeln](../ui/merge-policies.md#custom-timestamps) im Benutzerhandbuch [Zusammenführungsrichtlinien](../ui/merge-policies.md).

#### [!DNL External Source System Audit Details Mixin] details  {#mixin-details}

Das folgende Beispiel zeigt korrekt ausgefüllte Felder im [!DNL External Source System Audit Details Mixin]. Die vollständige Mix-JSON kann auch im [public Experience Data Model (XDM) repo](https://github.com/adobe/xdm/blob/master/components/mixins/shared/external-source-system-audit-details.schema.json) auf GitHub angezeigt werden.

```json
{
  "xdm:createdBy": "{CREATED_BY}",
  "xdm:createdDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastUpdatedBy": "{LAST_UPDATED_BY}",
  "xdm:lastUpdatedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastActivityDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastReferencedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastViewedDate": "2018-01-02T15:52:25+00:00"
 }
```
