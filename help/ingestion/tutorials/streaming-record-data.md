---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming von Datensatzdaten
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 2%

---


# Streamen von Datensatzdaten in die Adobe Experience Platform

In diesem Lernprogramm erfahren Sie, wie Sie mit der Verwendung von Streaming-Ingestion-APIs, die Teil der Data Ingestion Service-APIs der Adobe Experience Platform sind, beginnen können.

## Erste Schritte

Dieses Tutorial erfordert ein Arbeitswissen zu verschiedenen Adobe Experience Platformen-Services. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Der standardisierte Rahmen, nach dem Platform Erlebnisdaten organisiert.
- [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, benutzerdefiniertes Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Entwicklerhandbuch](../../xdm/api/getting-started.md)zur Schema-Registrierung: Ein umfassender Leitfaden, der alle verfügbaren Endpunkte der Schema Registry API und Anweisungen zum Aufrufen an diese Endpunkte enthält. Dies umfasst das Wissen über Ihre `{TENANT_ID}`Daten, die in den Aufrufen während dieses Lernprogramms angezeigt werden, sowie das Erstellen von Schemas, die zum Erstellen eines Datensatzes für die Erfassung verwendet werden.

Darüber hinaus erfordert dieses Lernprogramm, dass Sie bereits eine Streaming-Verbindung erstellt haben. Weitere Informationen zum Erstellen einer Streaming-Verbindung finden Sie im Tutorial zum [Erstellen einer Streaming-Verbindung](./create-streaming-connection.md).

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um erfolgreich Aufrufe von Streaming-Erfassungsschnittstelle-APIs durchführen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

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

## Erstellen Sie ein Schema, das auf der XDM Individual Profil-Klasse basiert

Um einen Datensatz zu erstellen, müssen Sie zunächst ein neues Schema erstellen, das die XDM Individual Profil-Klasse implementiert. Weitere Informationen zum Erstellen von Schemas finden Sie im Entwicklerhandbuch für die [Schema Registry API](../../xdm/api/getting-started.md).

**API-Format**

```http
POST /schemaregistry/tenant/schemas
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:immutableTags": [
        "union"
    ]
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `title` | Der Name, den Sie für Ihr Schema verwenden möchten. Dieser Name muss eindeutig sein. |
| `description` | Eine aussagekräftige Beschreibung des Schemas, das Sie erstellen. |
| `meta:immutableTags` | In diesem Beispiel wird das `union` Tag verwendet, um Ihre Daten in [Echtzeit-Kundendaten](../../profile/home.md)zu speichern. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 mit Details zu Ihrem neu erstellten Schema zurück.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "type": "object",
    "title": "Sample schema",
    "description": "Sample description",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        }
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/cpmtext/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:immutableTags": [
        "union"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createDate": 1551376506996,
        "repo:lastModifiedDate": 1551376506996,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{TENANT_ID}` | Diese ID wird verwendet, um sicherzustellen, dass die von Ihnen erstellten Ressourcen korrekt benannt und in Ihrer IMS-Organisation enthalten sind. Weitere Informationen zur Mandanten-ID finden Sie im [Schema-Registrierungsleitfaden](../../xdm/api/getting-started.md#know-your-tenant-id). |

Bitte beachten Sie die Attribute `$id` sowie die `version` Attribute, da beide bei der Erstellung Ihres Datensatzes verwendet werden.

## Festlegen eines primären Identitätsdeskriptors für das Schema

Fügen Sie anschließend dem oben erstellten Schema einen [Identitätsdeskriptor](../../xdm/api/descriptors.md) hinzu, wobei das Attribut für die E-Mail-Adresse der Arbeit als primäre ID verwendet wird. Dies führt zu zwei Änderungen:

1. Die Arbeits-E-Mail-Adresse wird ein Pflichtfeld. Das bedeutet, dass Nachrichten, die ohne dieses Feld gesendet werden, bei der Überprüfung fehlschlagen und nicht erfasst werden.

2. Echtzeit-Profil verwendet die Arbeits-E-Mail-Adresse als Identifikator, um weitere Informationen zu dieser Person zusammenzuführen.

### Anfrage

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "@type":"xdm:descriptorIdentity",
    "xdm:sourceProperty":"/workEmail/address",
    "xdm:property":"xdm:code",
    "xdm:isPrimary":true,
    "xdm:namespace":"Email",
    "xdm:sourceSchema":"{SCHEMA_REF_ID}",
    "xdm:sourceVersion":1
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEMA_REF_ID}` | Die `$id` Informationen, die Sie zuvor bei der Erstellung des Schemas erhalten haben. Es sollte ungefähr so aussehen: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Identitäts-Namensraum**
>
> Bitte stellen Sie sicher, dass die Codes gültig sind - im obigen Beispiel wird &quot;email&quot; verwendet, ein standardmäßiger Identitäts-Namensraum. Weitere häufig verwendete Standard-Identitäts-Namensraum finden Sie in den häufig gestellten Fragen zum [Identitätsdienst](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Wenn Sie einen benutzerspezifischen Namensraum erstellen möchten, führen Sie die in der Übersicht über den [Identitäts-Namensraum](../../identity-service/home.md)beschriebenen Schritte aus.

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 mit Informationen zum neu erstellten primären Identitätsdeskriptor für das Schema zurück.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/workEmail/address",
    "@id": "17aaebfa382ce8fc0a40d3e43870b6470aab894e1c368d16",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{IMS_ORG}"
}
```

## Datensatzdaten erstellen

Nachdem Sie Ihr Schema erstellt haben, müssen Sie einen Datensatz erstellen, um Datensatzdaten zu erfassen.

>[!NOTE]
>
>Dieser Datensatz wird für **Echtzeit-Kundendienst** und **Identitätsdienst** aktiviert.

**API-Format**

```http
POST /catalog/dataSets
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1.0"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 und ein Array zurück, das die ID des neu erstellten Datensatzes im Format enthält `@/dataSets/{DATASET_ID}`.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Erfassen von Datensatzdaten zur Streaming-Verbindung

Mit der vorhandenen Dataset- und Streaming-Verbindung können Sie XDM-formatierte JSON-Datensätze erfassen, um Datensatzdaten in die Platform zu erfassen.

**API-Format**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der `id` Wert der zuvor erstellten Streaming-Verbindung. |
| `synchronousValidation` | Ein optionaler Parameter für die Abfrage, der für Entwicklungszwecke vorgesehen ist. Wenn diese Einstellung auf `true`festgelegt ist, kann sie für sofortiges Feedback verwendet werden, um festzustellen, ob die Anforderung erfolgreich gesendet wurde. Standardmäßig ist dieser Wert auf `false`. |

**Anfrage**

>[!NOTE]
>
>Für den folgenden API-Aufruf sind **keine** Authentifizierungsheader erforderlich.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
            "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
            }
        },
        "xdmEntity": {
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                },
                "birthDate": "1969-03-14",
                "gender": "female"
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "type": "work",
                "status": "active"
            }
        }
    }
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zum neu gestreamen Profil zurück.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "synchronousValidation": {
        "status": "pass"
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{CONNECTION_ID}` | Die ID der zuvor erstellten Streaming-Verbindung. |
| `xactionId` | Eine eindeutige ID, die serverseitig für den soeben gesendeten Datensatz generiert wurde. Diese ID unterstützt Adobe bei der Verfolgung des Lebenszyklus dieses Datensatzes über verschiedene Systeme und beim Debugging. |
| `receivedTimeMs` | Ein Zeitstempel (Epoche in Millisekunden), der angibt, wann die Anforderung eingegangen ist. |
| `synchronousValidation.status` | Da der Parameter Abfrage hinzugefügt `synchronousValidation=true` wurde, wird dieser Wert angezeigt. Wenn die Überprüfung erfolgreich war, wird der Status `pass`angezeigt. |

## Abrufen der neu erfassten Datensatzdaten

Zur Validierung der zuvor erfassten Datensätze können Sie die Datensatzdaten mit der [Profil Access API](../../profile/api/entities.md) abrufen.

>[!NOTE]
>
>Wenn die Richtlinie zum Zusammenführen nicht definiert ist und das Schema.</span>name oder relatedSchema</span>.name ist `_xdm.context.profile`, ruft Profil Access **alle** zugehörigen Identitäten ab.

**API-Format**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `schema.name` | **Erforderlich.** Der Name des Schemas, auf das Sie zugreifen. |
| `entityId` | Die ID der Entität. Falls angegeben, müssen Sie auch den Entitäts-Namensraum angeben. |
| `entityIdNS` | Der Namensraum der ID, die Sie abrufen möchten. |

**Anfrage**

Sie können die zuvor erfassten Datensatzdaten mit der folgenden GET-Anforderung überprüfen.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit Details zu den angeforderten Entitäten zurück. Wie Sie sehen können, ist dies der gleiche Datensatz, der zuvor erfolgreich aufgenommen wurde.

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "mergePolicy": {
            "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56"
        },
        "sources": [
            "5e30d7986c0cc218a85cee65"
        ],
        "tags": [
            "1580346827274:2478:215"
        ],
        "identityGraph": [
            "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA"
        ],
        "entity": {
            "person": {
                "name": {
                    "lastName": "Doe",
                    "middleName": "F",
                    "firstName": "Jane"
                },
                "gender": "female",
                "birthDate": "1969-03-14"
            },
            "workEmail": {
                "type": "work",
                "address": "janedoe@example.com",
                "status": "active",
                "primary": true
            },
            "identityMap": {
                "email": [
                    {
                        "id": "janedoe@example.com"
                    }
                ]
            }
        },
        "lastModifiedAt": "2020-01-30T01:13:59Z"
    }
}
```

## Nächste Schritte

Durch Lesen dieses Dokuments wissen Sie jetzt, wie Sie Datensatzdaten mithilfe von Streaming-Verbindungen in die Platform aufnehmen können. Sie können versuchen, mehr Aufrufe mit unterschiedlichen Werten durchzuführen und die aktualisierten Werte abzurufen. Darüber hinaus können Sie Beginn zur Überwachung der erfassten Daten über die Benutzeroberfläche der Platform verwenden. Weitere Informationen finden Sie im Handbuch zur Erfassung der [Überwachungsdaten](../quality/monitor-data-flows.md) .

Weitere Informationen zur Streaming-Erfassung im Allgemeinen finden Sie in der [Streaming-Übersicht](../streaming-ingestion/overview.md).


