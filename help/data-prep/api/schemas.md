---
keywords: Experience Platform;Startseite;beliebte Themen;Datenvorbereitung;API-Handbuch;Schemas;
solution: Experience Platform
title: API-Endpunkt für Schemas
description: Sie können den Endpunkt „/schemas“ in der Adobe Experience Platform-API verwenden, um Schemas zur Verwendung mit Mapper in Platform programmgesteuert abzurufen, zu erstellen und zu aktualisieren.
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 100%

---



# Endpunkt für Schemas

Schemas können mit Mapper verwendet werden, um dafür zu sorgen, dass die von Ihnen in Adobe Experience Platform erfassten Daten mit den gewünschten Daten übereinstimmen. Sie können den `/schemas`-Endpunkt nutzen, um programmgesteuert benutzerdefinierte Schemas zur Verwendung mit Mapper in Platform zu erstellen, aufzulisten und abzurufen.

>[!NOTE]
>
>Mit diesem Endpunkt erstellte Schemas werden ausschließlich mit Mapper und Zuordnungssätzen genutzt. Informationen zum Erstellen von Schemas, auf die andere Platform-Dienste zugreifen können, finden Sie im [Schema Registry-Entwicklerhandbuch](../../xdm/api/schemas.md).

## Abrufen aller Schemas

Sie können eine Liste aller verfügbaren Mapper-Schemas für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den `/schemas`-Endpunkt senden.

**API-Format**

Der `/schemas`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Zwar sind die meisten dieser Parameter optional, doch wird ihre Verwendung dringend empfohlen, um kostspieligen Aufwand zu reduzieren. Sie müssen jedoch sowohl den Parameter `start` als auch den Parameter `limit` in Ihre Anfrage einbeziehen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{LIMIT}` | **Erforderlich**. Gibt die Anzahl der Schemas an, die zurückgegeben werden. |
| `{START}` | **Erforderlich**. Gibt den Versatz der Ergebnisseiten an. Um die erste Ergebnisseite zu erhalten, setzen Sie den Wert auf `start=0`. |
| `{NAME}` | Filtert das Schema anhand des Namens. |
| `{ORDER_BY}` | Sortiert die Reihenfolge der Ergebnisse. Die unterstützten Felder sind `modifiedDate` und `createdDate`. Sie können der Eigenschaft `+` oder `-` voranstellen, um in auf- bzw. absteigender Reihenfolge zu sortieren. |

**Anfrage**

Mit der folgenden Anfrage werden die letzten beiden erstellten Schemas für Ihre IMS-Organisation abgerufen.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die folgende Antwort gibt den HTTP-Status-Code 200 mit einer Liste der angeforderten Schemas zurück.

>[!NOTE]
>
>Die folgende Antwort wurde aus Platzgründen gekürzt.

```json
{
    "data": [
        {
            "id": "823ac494f35e4e84bcb2f061378fcca6",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
                "contentType": "1.0"
            }
        },
        {
            "id": "0f868d3a1b804fb0abf738306290ae79",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema 2",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0f868d3a1b804fb0abf738306290ae79",
                "contentType": "1.0"
            }
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

## Erstellen von Schemas

Sie können für die Validierung ein Schema erstellen, indem Sie eine POST-Anfrage an den `/schemas`-Endpunkt senden. Es gibt drei Möglichkeiten zum Erstellen eines Schemas: Senden eines [JSON-Schemas](https://json-schema.org/), Verwenden von Beispieldaten oder Verweisen auf ein vorhandenes XDM-Schema.

```http
POST /schemas
```

### Verwenden eines JSON-Schemas

**Anfrage**

Mit der folgenden Anfrage können Sie ein Schema erstellen, indem Sie ein [JSON-Schema](https://json-schema.org/) senden.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zu Ihrem neu erstellten Schema zurück.

```json
{
    "id": "6daffabf14b1425292add3719afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

### Verwenden von Beispieldaten

**Anfrage**

Mit der folgenden Anfrage können Sie ein Schema anhand von Beispieldaten erstellen, die Sie zuvor hochgeladen haben.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `sampleId` | Die Kennung der Beispieldaten, auf denen das Schema basiert. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zu Ihrem neu erstellten Schema zurück.

```json
{
    "id": "b2ee78bd55ac45f781a93fb8b90d99b2",
    "version": 0,
    "jsonSchema": {
        "title": "SampleSchema:45439a93d48d47d098d26e0f0840cc02",
        "type": "object",
        "properties": {
            "gender": {
                "title": "gender",
                "type": "string"
            },
            "last_name": {
                "title": "last_name",
                "type": "string"
            },
            "id": {
                "title": "id",
                "type": "string"
            },
            "ip_address": {
                "title": "ip_address",
                "type": "string"
            },
            "first_name": {
                "title": "first_name",
                "type": "string"
            },
            "email": {
                "title": "email",
                "type": "string"
            }
        }
    },
    "sampleId": "45439a93d48d47d098d26e0f0840cc02"
}
```

### Verweisen auf ein XDM-Schema

**Anfrage**

Mit der folgenden Anfrage können Sie ein Schema erstellen, indem Sie auf ein vorhandenes XDM-Schema verweisen.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "name": "outputSchema1",
     "schemaRef": {
         "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0d555890502224d187b619f23c35c8d1",
         "contentType": "application/vnd.adobe.xed-full+json;version=1"
     }  
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name des Schemas, das Sie erstellen möchten. |
| `schemaRef.id` | Die Kennung des Schemas, auf das Sie verweisen. |
| `schemaRef.contentType` | Bestimmt das Antwortformat des referenzierten Schemas. Weitere Informationen zu diesem Feld finden Sie im [Schema Registry-Entwicklerhandbuch](../../xdm/api/schemas.md#lookup) |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zu Ihrem neu erstellten Schema zurück.

>[!NOTE]
>
>Die folgende Antwort wurde aus Platzgründen gekürzt.

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{ORG_ID}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## Erstellen von Schemas per Datei-Upload

Sie können ein Schema erstellen, indem Sie dafür eine JSON-Datei hochladen, aus der konvertiert werden soll.

**API-Format**

```http
POST /schemas/upload
```

**Anfrage**

Mit der folgenden Anfrage können Sie ein Schema aus einer hochgeladenen JSON-Datei erstellen.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zu Ihrem neu erstellten Schema zurück.

```json
{
    "id": "292add3716daffabf14b14259afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

## Abrufen einzelner Schemas

Sie können Informationen zu einem bestimmten Schema abrufen, indem Sie eine GET-Anfrage an den `/schemas`-Endpunkt senden und im Anfragepfad die Kennung des Schemas angeben, das Sie abrufen möchten.

**API-Format**

```http
GET /schemas/{SCHEMA_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SCHEMA_ID}` | Die Kennung des Schemas, das Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anfrage ruft Details zum angegebenen Schema ab.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Details zum angegebenen Schema zurück.

```json
{
    "id": "0f868d3a1b804fb0abf738306290ae79",
    "version": 0,
    "jsonSchema": {
        "title": "Sample schema",
        "description": "Sample description",
        "type": "object",
        "properties": {
            "_id": {
                "title": "Identifier",
                "description": "A unique identifier for the record.",
                "type": "string",
                "format": "uri-reference",
                "meta:xdmField": "@id",
                "meta:xdmType": "string"
            },
            "personalEmail": {
                "title": "Personal Email",
                "description": "A personal email address.",
                "type": "object",
                "properties": {
                    "primary": {
                        "title": "Primary",
                        "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                        "type": "boolean",
                        "meta:xdmField": "xdm:primary",
                        "meta:xdmType": "boolean"
                    },
                    "address": {
                        "title": "Address",
                        "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                        "type": "string",
                        "format": "email",
                        "meta:xdmField": "xdm:address",
                        "meta:xdmType": "string"
                    }
                },
                "meta:xdmField": "xdm:personalEmail",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
                "meta:xdmType": "object"
            }
        },
        "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc"
    },
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
        "contentType": "1.0"
    }
}
```
