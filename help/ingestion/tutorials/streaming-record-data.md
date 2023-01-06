---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming-Erfassung; Erfassung; Datensatzdaten; Stream-Datensatzdaten;
solution: Experience Platform
title: Streamen von Datensatzdaten mit Streaming-Aufnahme-APIs
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie mit der Verwendung von Streaming-Erfassungs-APIs beginnen können, die Bestandteil der Data Ingestion Service-APIs von Adobe Experience Platform sind.
exl-id: 097dfd5a-4e74-430d-8a12-cac11b1603aa
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 58%

---


# Streamen von Datensatzdaten mit Streaming-Aufnahme-APIs

In diesem Tutorial erfahren Sie, wie Sie mit der Verwendung von Streaming-Aufnahme-APIs beginnen, die Teil von Adobe Experience Platform sind [!DNL Data Ingestion Service] APIs.

## Erste Schritte

Für dieses Tutorial benötigen Sie Grundkenntnisse zu verschiedenen Adobe Experience Platform-Diensten. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Der standardisierte Rahmen, durch den [!DNL Platform] organisiert Erlebnisdaten.
   - [Entwicklerhandbuch zur Schema Registry](../../xdm/api/getting-started.md): Ein umfassendes Handbuch, das alle verfügbaren Endpunkte der [!DNL Schema Registry] API und wie Sie Aufrufe an sie durchführen. Zum Beispiel müssen Sie Ihre `{TENANT_ID}` kennen, die in Aufrufen in diesem Tutorial immer wieder verwendet wird, und wissen, wie man Schemas erstellt, die zum Einrichten eines zu erfassenden Datensatzes dienen.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Verbraucherprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../landing/api-guide.md).

## Erstellen eines Schemas basierend auf der [!DNL XDM Individual Profile] class

Um einen Datensatz zu erstellen, müssen Sie zunächst ein neues Schema erstellen, das die [!DNL XDM Individual Profile] -Klasse. Weiterführende Informationen zum Erstellen von Schemas finden Sie im [Entwicklerhandbuch zur Schema Registry-API](../../xdm/api/getting-started.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `meta:immutableTags` | In diesem Beispiel wird die `union` -Tag verwendet wird, um Ihre Daten in [[!DNL Real-Time Customer Profile]](../../profile/home.md). |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zu Ihrem neu erstellten Schema zurück.

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
    "imsOrg": "{ORG_ID}",
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
| `{TENANT_ID}` | Diese Kennung stellt sicher, dass die von Ihnen erstellten Ressourcen den richtigen Namespace aufweisen und in Ihrer IMS-Organisation enthalten sind. Weiterführende Informationen zur Mandantenkennung finden Sie im [Handbuch zur Schemaregistrierung](../../xdm/api/getting-started.md#know-your-tenant-id). |

Beachten Sie die Attribute `$id` sowie `version`, da Sie bei der Erstellung Ihres Datensatzes beide von ihnen verwenden werden.

## Primären Identitätsdeskriptor für das Schema festlegen

Fügen Sie anschließend dem oben erstellten Schema einen [Identitätsdeskriptor](../../xdm/api/descriptors.md) hinzu, wobei Sie das Attribut „Geschäftliche E-Mail-Adresse“ als primäre Kennung verwenden. Dies führt zu zwei Änderungen:

1. Die geschäftliche E-Mail-Adresse wird zu einem Pflichtfeld. Das bedeutet, dass Nachrichten, die ohne dieses Feld gesendet werden, bei der Validierung fehlschlagen und nicht erfasst werden.

2. [!DNL Real-Time Customer Profile] verwendet die geschäftliche E-Mail-Adresse als Kennung, um weitere Informationen zu dieser Person zusammenzufügen.

### Anfrage

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `{SCHEMA_REF_ID}` | Die `$id`, die Sie zuvor bei der Erstellung des Schemas erhalten haben. Sie sollte ungefähr so aussehen: `"https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}"` |

>[!NOTE]
>
>&#x200B; &#x200B;**Identitäts-Namespace-Codes**
>
> Stellen Sie sicher, dass die Codes gültig sind – im obigen Beispiel kommt „email“ zum Einsatz, was ein standardmäßiger Identitäts-Namespace ist. Weitere häufig verwendete standardmäßige Identitäts-Namespaces finden Sie in den [FAQ zum Identity Service](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Wenn Sie einen benutzerspezifischen Namespace erstellen möchten, führen Sie die in der [Übersicht zum Identitäts-Namespace](../../identity-service/home.md) beschriebenen Schritte aus.

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Informationen zum neu erstellten primären Identitätsdeskriptor für das Schema zurück.

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
    "imsOrg": "{ORG_ID}"
}
```

## Datensatz für Datensatzdaten erstellen

Nachdem Sie Ihr Schema erstellt haben, müssen Sie nun einen Datensatz für die Erfassung von Datensatzdaten anlegen.

>[!NOTE]
>
>Dieser Datensatz wird für **[!DNL Real-Time Customer Profile]** und **[!DNL Identity Service]**.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d ' {
    "name": "Dataset name",
    "description": "Dataset description",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID},
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
    },
    "tags": {
        "unifiedIdentity": ["enabled:true"],
        "unifiedProfile": ["enabled:true"]
    }
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 und ein Array zurück, das die Kennung des neu erstellten Datensatzes im Format `@/dataSets/{DATASET_ID}` enthält.

```json
[
    "@/dataSets/5e30d7986c0cc218a85cee65
]
```

## Aufbauen einer Streaming-Verbindung

Nachdem Sie Ihr Schema und Ihren Datensatz erstellt haben, können Sie eine Streaming-Verbindung erstellen

Weiterführende Informationen zum Erstellen einer Streaming-Verbindung finden Sie im Tutorial zum [Erstellen einer Streaming-Verbindung](./create-streaming-connection.md).

## Aufnehmen von Datensatzdaten in die Streaming-Verbindung {#ingest-data}

Mit dem vorhandenen Datensatz und der Streaming-Verbindung können Sie XDM-formatierte JSON-Datensätze erfassen, um Datensatzdaten in [!DNL Platform].

**API-Format**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Die `inletId` -Wert der zuvor erstellten Streaming-Verbindung. |
| `syncValidation` | Ein optionaler Abfrageparameter, der für Entwicklungszwecke vorgesehen ist. Wenn er auf `true` gesetzt ist, kann er für unmittelbares Feedback verwendet werden, um zu ermitteln, ob die Anfrage erfolgreich gesendet wurde. Standardmäßig ist dieser Wert auf `false` gesetzt. Beachten Sie Folgendes: Wenn Sie diesen Abfrageparameter auf `true` dass die Anfrage auf 60-mal pro Minute beschränkt wird `CONNECTION_ID`. |

**Anfrage**

Die Aufnahme von Datensatzdaten in eine Streaming-Verbindung kann entweder mit oder ohne den Quellnamen erfolgen.

Die folgende Beispielanfrage erfasst einen Datensatz mit einem fehlenden Quellnamen in Platform. Wenn einem Datensatz der Quellname fehlt, wird die Quell-ID aus der Definition der Streaming-Verbindung hinzugefügt.

>[!NOTE]
>
>Der folgende API-Aufruf **not** Authentifizierungs-Header benötigen.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "flowId": "{FLOW_ID}",
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
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

Wenn Sie einen Quellnamen einbeziehen möchten, zeigt das folgende Beispiel, wie Sie ihn einschließen.

```json
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample source name"
        }
    }
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zum neu gestreamten zurück [!DNL Profile].

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507,
    "syncValidation": {
        "status": "pass"
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{CONNECTION_ID}` | Die Kennung der zuvor erstellten Streaming-Verbindung. |
| `xactionId` | Eine eindeutige Kennung, die für den soeben gesendeten Datensatz Server-seitig generiert wurde. Diese Kennung hilft Adobe bei der Verfolgung des Lebenszyklus dieses Datensatzes in verschiedenen Systemen sowie beim Debugging. |
| `receivedTimeMs` | Ein Zeitstempel (Epoche in Millisekunden), der angibt, wann die Anfrage empfangen wurde. |
| `syncValidation.status` | Da der Abfrageparameter `syncValidation=true` hinzugefügt wurde, wird dieser Wert angezeigt. Wenn die Validierung erfolgreich war, lautet der Status `pass`. |

## Abrufen der neu erfassten Datensatzdaten

Zur Validierung der zuvor erfassten Datensätze können Sie die [[!DNL Profile Access API]](../../profile/api/entities.md) , um die Datensatzdaten abzurufen.

>[!NOTE]
>
>Wenn die Kennung der Zusammenführungsrichtlinie nicht definiert ist und die `schema.name` oder `relatedSchema.name` is `_xdm.context.profile`, [!DNL Profile Access] wird abgerufen **all** verwandte Identitäten.

**API-Format**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `schema.name` | **Erforderlich.** Der Name des Schemas, auf das Sie zugreifen. |
| `entityId` | Die ID der Entität. Falls angegeben, müssen Sie auch den Entitäts-Namespace angeben. |
| `entityIdNS` | Der Namespace der Kennung, die Sie abrufen möchten. |

**Anfrage**

Sie können die zuvor erfassten Datensatzdaten mit der folgenden GET-Anfrage überprüfen.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email'\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu den angeforderten Entitäten zurück. Wie Sie sehen können, ist dies der gleiche Datensatz, der zuvor erfolgreich aufgenommen wurde.

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

Durch Lesen dieses Dokuments wissen Sie jetzt, wie Sie Datensatzdaten in [!DNL Platform] Streaming-Verbindungen verwenden. Sie können versuchen, zusätzliche Aufrufe mit unterschiedlichen Werten durchzuführen und die aktualisierten Werte abzurufen. Darüber hinaus können Sie mit der Überwachung der erfassten Daten beginnen durch [!DNL Platform] Benutzeroberfläche. Weiterführende Informationen finden Sie im Handbuch zur [Überwachung der Datenerfassung](../quality/monitor-data-ingestion.md).

Weitere allgemeine Informationen zur Streaming-Erfassung finden Sie in der [Streaming-Erfassung – Übersicht](../streaming-ingestion/overview.md).
