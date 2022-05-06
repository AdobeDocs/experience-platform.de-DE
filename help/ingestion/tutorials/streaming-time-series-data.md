---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming-Erfassung; Erfassung; Zeitreihendaten; Stream-Zeitreihendaten;
solution: Experience Platform
title: Streamen von Zeitreihendaten mit Streaming-Aufnahme-APIs
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie mit der Verwendung von Streaming-Erfassungs-APIs beginnen können, die Bestandteil der Data Ingestion Service-APIs von Adobe Experience Platform sind.
exl-id: 720b15ea-217c-4c13-b68f-41d17b54d500
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 66%

---

# Streamen von Zeitreihendaten mit Streaming-Aufnahme-APIs

In diesem Tutorial erfahren Sie, wie Sie mit der Verwendung von Streaming-Aufnahme-APIs beginnen, die Teil von Adobe Experience Platform sind [!DNL Data Ingestion Service] APIs.

## Erste Schritte

Für dieses Tutorial benötigen Sie Grundkenntnisse zu verschiedenen Adobe Experience Platform-Diensten. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Der standardisierte Rahmen, durch den [!DNL Platform] organisiert Erlebnisdaten.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Verbraucherprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Entwicklerhandbuch zur Schema Registry](../../xdm/api/getting-started.md): Ein umfassendes Handbuch, das alle verfügbaren Endpunkte der [!DNL Schema Registry] API und wie Sie Aufrufe an sie durchführen. Zum Beispiel müssen Sie Ihre `{TENANT_ID}` kennen, die in Aufrufen in diesem Tutorial immer wieder verwendet wird, und wissen, wie man Schemas erstellt, die zum Einrichten eines zu erfassenden Datensatzes dienen.

Darüber hinaus setzt dieses Tutorial voraus, dass Sie bereits eine Streaming-Verbindung hergestellt haben. Weiterführende Informationen zum Erstellen einer Streaming-Verbindung finden Sie im Tutorial zum [Erstellen einer Streaming-Verbindung](./create-streaming-connection.md).

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die APIs für die Streaming-Erfassung erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

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

## Schema erstellen auf Grundlage der XDM ExperienceEvent-Klasse

Um einen Datensatz zu erstellen, müssen Sie zunächst ein neues Schema erstellen, das die [!DNL XDM ExperienceEvent] -Klasse. Weiterführende Informationen zum Erstellen von Schemas finden Sie im [Entwicklerhandbuch zur Schema Registry-API](../../xdm/api/getting-started.md).

**API-Format**

```http
POST /schemaregistry/tenant/schemas
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce"
        },
        {  
         "$ref":"https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
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
| `meta:immutableTags` | In diesem Beispiel wird die `union` -Tag verwendet wird, um Ihre Daten in [[!DNL Real-time Customer Profile]](../../profile/home.md). |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zu Ihrem neu erstellten Schema zurück.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.{SCHEMA_ID}",
    "meta:resourceType": "schemas",
    "version": "1",
    "type": "object",
    "title": "{SCHEMA_NAME}",
    "description": "{SCHEMA_DESCRIPTION}",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent-commerce",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "required": [
        "@id",
        "xdm:timestamp"
    ],
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/experienceevent",
        "https://ns.adobe.com/xdm/data/time-series",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/experienceevent-environment-details",
        "https://ns.adobe.com/xdm/context/experienceevent-commerce",
        "https://ns.adobe.com/experience/campaign/experienceevent-profile-work-details"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
    "meta:registryMetadata": {
        "repo:createDate": 1551229957987,
        "repo:lastModifiedDate": 1551229957987,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:tenantNamespace": "{NAMESPACE}"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{TENANT_ID}` | Diese Kennung stellt sicher, dass die von Ihnen erstellten Ressourcen den richtigen Namespace aufweisen und in Ihrer IMS-Organisation enthalten sind. Weiterführende Informationen zur Mandantenkennung finden Sie im [Handbuch zur Schemaregistrierung](../../xdm/api/getting-started.md#know-your-tenant-id). |

Beachten Sie die Attribute `$id` sowie `version`, da Sie bei der Erstellung Ihres Datensatzes beide von ihnen verwenden werden.

## Primären Identitätsdeskriptor für das Schema festlegen

Fügen Sie anschließend dem oben erstellten Schema einen [Identitätsdeskriptor](../../xdm/api/descriptors.md) hinzu, wobei Sie das Attribut „Geschäftliche E-Mail-Adresse“ als primäre Kennung verwenden. Dies führt zu zwei Änderungen:

1. Die geschäftliche E-Mail-Adresse wird zu einem Pflichtfeld. Das bedeutet, dass Nachrichten, die ohne dieses Feld gesendet werden, bei der Validierung fehlschlagen und nicht erfasst werden.

2. [!DNL Real-time Customer Profile] verwendet die geschäftliche E-Mail-Adresse als Kennung, um weitere Informationen zu dieser Person zusammenzufügen.

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
    "xdm:sourceProperty":"/_experience/campaign/message/profileSnapshot/workEmail/address",
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
>&#x200B;**Identitäts-Namespace-Codes**
>
> Stellen Sie sicher, dass die Codes gültig sind – im obigen Beispiel kommt „email“ zum Einsatz, was ein standardmäßiger Identitäts-Namespace ist. Weitere häufig verwendete standardmäßige Identitäts-Namespaces finden Sie in den [FAQ zum Identity Service](../../identity-service/troubleshooting-guide.md#what-are-the-standard-identity-namespaces-provided-by-experience-platform).
>
> Wenn Sie einen benutzerspezifischen Namespace erstellen möchten, führen Sie die in der [Übersicht zum Identitäts-Namespace](../../identity-service/home.md) beschriebenen Schritte aus.

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Informationen zum neu erstellten primären Identitäts-Namespace für das Schema zurück.

```json
{
    "xdm:property": "xdm:code",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
    "xdm:namespace": "Email",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceVersion": 1,
    "xdm:isPrimary": true,
    "xdm:sourceProperty": "/_experience/campaign/message/profileSnapshot/workEmail/address",
    "@id": "ec31c09e0906561861be5a71fcd964e29ebe7923b8eb0d1e",
    "meta:containerId": "tenant",
    "version": "1",
    "imsOrg": "{ORG_ID}"
}
```

## Datensatz für Zeitreihendaten erstellen

Nachdem Sie Ihr Schema erstellt haben, müssen Sie nun einen Datensatz für die Erfassung von Datensatzdaten anlegen.

>[!NOTE]
>
>Dieser Datensatz wird für **[!DNL Real-time Customer Profile]** und **[!DNL Identity]** durch Festlegen der entsprechenden Tags.

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
  -d '{
    "name": "{DATASET_NAME}",
    "description": "{DATASET_DESCRIPTION}",
    "schemaRef": {
        "id": "{SCHEMA_REF_ID}",
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
    "@/dataSets/5e72608b10f6e318ad2dee0f"
]
```


## Aufbauen einer Streaming-Verbindung

Nachdem Sie Ihr Schema und Ihren Datensatz erstellt haben, müssen Sie eine Streaming-Verbindung erstellen, um Ihre Daten aufzunehmen.

Weiterführende Informationen zum Erstellen einer Streaming-Verbindung finden Sie im Tutorial zum [Erstellen einer Streaming-Verbindung](./create-streaming-connection.md).

## Zeitreihendaten an die Streaming-Verbindung erfassen

Mit dem erstellten Datensatz, der Streaming-Verbindung und dem erstellten Datenfluss können Sie XDM-formatierte JSON-Datensätze erfassen, um Zeitreihendaten in [!DNL Platform].

**API-Format**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der `id`-Wert der neu erstellten Streaming-Verbindung. |
| `syncValidation` | Ein optionaler Abfrageparameter, der für Entwicklungszwecke vorgesehen ist. Wenn er auf `true` gesetzt ist, kann er für unmittelbares Feedback verwendet werden, um zu ermitteln, ob die Anfrage erfolgreich gesendet wurde. Standardmäßig ist dieser Wert auf `false` gesetzt. Beachten Sie Folgendes: Wenn Sie diesen Abfrageparameter auf `true` dass die Anfrage auf 60-mal pro Minute beschränkt wird `CONNECTION_ID`. |

**Anfrage**

Die Erfassung von Zeitreihendaten in eine Streaming-Verbindung kann entweder mit oder ohne Quellname erfolgen.

Die folgende Beispielanfrage erfasst Zeitreihendaten mit einem fehlenden Quellnamen in Platform. Wenn den Daten der Quellname fehlt, wird die Quell-ID aus der Definition der Streaming-Verbindung hinzugefügt.

Beide `xdmEntity._id` und `xdmEntity.timestamp` sind erforderliche Felder für Zeitreihendaten. Die `xdmEntity._id` -Attribut eine eindeutige Kennung für den Datensatz selbst darstellt, **not** eine eindeutige ID der Person oder des Geräts, deren Datensatz sie enthält.

Sie müssen Ihre eigene `xdmEntity._id` und `xdmEntity.timestamp` für den Datensatz so zu verwenden, dass er konsistent bleibt, wenn der Datensatz jemals wieder aufgenommen werden muss. Idealerweise enthält Ihr Quellsystem diese Werte. Wenn keine ID verfügbar ist, sollten Sie die Werte anderer Felder im Datensatz verketten, um einen eindeutigen Wert zu erstellen, der bei der erneuten Aufnahme durchgängig aus dem Datensatz neu generiert werden kann.

>[!NOTE]
>
>Der folgende API-Aufruf **not** Authentifizierungs-Header benötigen.

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{
    "header": {
        "schemaRef": {
            "id": "{SCHEMA_REF_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "flowId": "{FLOW_ID}",
        "datasetId": "{DATASET_ID}"
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity":{
            "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": "2019-02-23T22:07:01Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            },
            "productListItems": [
                {
                    "SKU": "CC",
                    "name": "Fernie Snow",
                    "quantity": 30,
                    "priceTotal": 7.8
                }
            ],
            "commerce": {
                "productViews": {
                    "value": 1
                }
            },
            "_experience": {
                "campaign": {
                    "message": {
                        "profileSnapshot": {
                            "workEmail":{
                                "address": "janedoe@example.com"
                            }
                        }
                    }
                }
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
| `{CONNECTION_ID}` | Die `inletId` der zuvor erstellten Streaming-Verbindung. |
| `xactionId` | Eine eindeutige Kennung, die für den soeben gesendeten Datensatz Server-seitig generiert wurde. Diese Kennung hilft Adobe bei der Verfolgung des Lebenszyklus dieses Datensatzes in verschiedenen Systemen sowie beim Debugging. |
| `receivedTimeMs`: Ein Zeitstempel (Epoche in Millisekunden), der angibt, wann die Anfrage empfangen wurde. |
| `syncValidation.status` | Da der Abfrageparameter `syncValidation=true` hinzugefügt wurde, wird dieser Wert angezeigt. Wenn die Validierung erfolgreich war, lautet der Status `pass`. |

## Die neu erfassten Zeitreihendaten abrufen

Zur Validierung der zuvor erfassten Datensätze können Sie die [[!DNL Profile Access API]](../../profile/api/entities.md) , um die Zeitreihendaten abzurufen. Dazu können Sie eine GET-Anfrage an den `/access/entities`-Endpunkt richten und optionale Abfrageparameter nutzen. Es können mehrere Parameter verwendet werden, getrennt durch das kaufmännische Und-Zeichen (&amp;).

>[!NOTE]
>
>Wenn die Kennung der Zusammenführungsrichtlinie nicht definiert ist und die `schema.name` oder `relatedSchema.name` is `_xdm.context.profile`, [!DNL Profile Access] wird abgerufen **all** verwandte Identitäten.

**API-Format**

```http
GET /access/entities
GET /access/entities?{QUERY_PARAMETERS}
GET /access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `schema.name` | **Erforderlich.** Der Name des Schemas, auf das Sie zugreifen. |
| `relatedSchema.name` | **Erforderlich.** Da Sie auf ein `_xdm.context.experienceevent` zugreifen, gibt dieser Wert das Schema für die Profilentität an, mit der die Zeitreihenereignisse verwandt sind. |
| `relatedEntityId` | Die Kennung der verwandten Entität. Falls angegeben, müssen Sie auch den Entitäts-Namespace angeben. |
| `relatedEntityIdNS` | Der Namespace der Kennung, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=janedoe@example.com&relatedEntityIdNS=email \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu den angeforderten Entitäten zurück. Wie Sie sehen können, sind dies die gleichen Zeitreihendaten, die zuvor erfasst wurden.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "9af5adcc-db9c-4692-b826-65d3abe68c22",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
            "entityId": "9af5adcc-db9c-4692-b826-65d3abe68c22",
            "timestamp": 1582495621000,
            "entity": {
                "environment": {
                    "browserDetails": {
                        "javaScriptVersion": "1.6",
                        "cookiesEnabled": true,
                        "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
                        "acceptLanguage": "en-US",
                        "javaEnabled": true
                    },
                    "colorDepth": 32,
                    "viewportHeight": 799,
                    "viewportWidth": 414
                },
                "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Fernie Snow",
                        "quantity": 30,
                        "SKU": "CC",
                        "priceTotal": 7.8
                    }
                ],
                "_experience": {
                    "campaign": {
                        "message": {
                            "profileSnapshot": {
                                "workEmail": {
                                    "address": "janedoe@example.com"
                                }
                            }
                        }
                    }
                },
                "timestamp": "2020-02-23T22:07:01Z"
            },
            "lastModifiedAt": "2020-03-18T18:51:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Nächste Schritte

Durch Lesen dieses Dokuments wissen Sie jetzt, wie Sie Datensatzdaten in [!DNL Platform] Streaming-Verbindungen verwenden. Sie können versuchen, zusätzliche Aufrufe mit unterschiedlichen Werten durchzuführen und die aktualisierten Werte abzurufen. Darüber hinaus können Sie mit der Überwachung der erfassten Daten beginnen durch [!DNL Platform] Benutzeroberfläche. Weiterführende Informationen finden Sie im Handbuch zur [Überwachung der Datenerfassung](../quality/monitor-data-ingestion.md).

Weitere allgemeine Informationen zur Streaming-Erfassung finden Sie in der [Streaming-Erfassung – Übersicht](../streaming-ingestion/overview.md).
