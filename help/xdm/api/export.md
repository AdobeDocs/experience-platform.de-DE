---
title: API-Endpunkt exportieren
description: Mit dem Endpunkt /export in der Schema Registry-API können Sie XDM-Ressourcen zwischen Sandboxes freigeben.
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 12%

---

# Export-Endpunkt

Alle Ressourcen innerhalb des [!DNL Schema Library] sind in einer bestimmten Sandbox in Adobe Experience Platform enthalten. In einigen Fällen möchten Sie möglicherweise Experience-Datenmodell (XDM)-Ressourcen zwischen Sandboxes und Organisationen freigeben. Mit dem Endpunkt `/rpc/export` in der API [!DNL Schema Registry] können Sie eine Export-Payload für beliebige Schemas, Schemafeldgruppen oder Datentypen in der [!DNL Schema Library] generieren und diese Payload dann verwenden, um diese Ressource (und alle abhängigen Ressourcen) über den [`/rpc/import` -Endpunkt](./import.md) in eine Ziel-Sandbox und Organisation zu importieren.

## Erste Schritte

Der Endpunkt `/rpc/export` ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

Der Endpunkt `/rpc/export` ist Teil der Remote-Prozeduraufrufe (RPCs), die von [!DNL Schema Registry] unterstützt werden. Im Gegensatz zu anderen Endpunkten in der [!DNL Schema Registry]-API erfordern RPC-Endpunkte keine zusätzlichen Kopfzeilen wie `Accept` oder `Content-Type` und verwenden keine `CONTAINER_ID`. Stattdessen müssen sie den Namespace `/rpc` verwenden, wie in den API-Aufrufen unten dargestellt.

## Export-Payload für eine Ressource generieren {#export}

Für vorhandene Schemas, Feldergruppen oder Datentypen im [!DNL Schema Library] können Sie eine Export-Payload generieren, indem Sie eine GET-Anfrage an den `/export` -Endpunkt senden und dabei die Kennung der Ressource im Pfad angeben.

**API-Format**

```http
GET /rpc/export/{RESOURCE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{RESOURCE_ID}` | Die `meta:altId` oder URL-kodierte `$id` der XDM-Ressource, die Sie exportieren möchten. |

{style="table-layout:auto"}

**Anfrage**

Mit der folgenden Anfrage wird eine Export-Payload für eine `Restaurant` -Feldergruppe abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array von Objekten zurück, die die Ziel-XDM-Ressource und alle abhängigen Ressourcen darstellen. In diesem Beispiel ist das erste Objekt im Array ein vom Mandanten erstellter `Property` -Datentyp, den die Feldergruppe `Restaurant` verwendet, während das zweite Objekt die Feldergruppe `Restaurant` selbst ist. Diese Payload kann dann verwendet werden, um [die Ressource](#import) in eine andere Sandbox oder Organisation zu importieren.

Beachten Sie, dass alle Instanzen der Mandanten-ID der Ressource durch `<XDM_TENANTID_PLACEHOLDER>` ersetzt werden. Dadurch kann die Schema Registry die richtige Mandantenkennung automatisch auf die Ressourcen anwenden, je nachdem, wo sie im nachfolgenden Importaufruf gesendet werden.

```json
[
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    },
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_<XDM_TENANTID_PLACEHOLDER>": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
                            }
                        },
                        "meta:xdmType": "object"
                    }
                },
                "meta:xdmType": "object"
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    }
]
```

## Ressource importieren {#import}

Nachdem Sie die Export-Payload aus der CSV-Datei generiert haben, können Sie diese Payload an den `/rpc/import` -Endpunkt senden, um das Schema zu generieren.

Weitere Informationen zum Generieren von Schemas aus Export-Payloads finden Sie im [Import-Endpunkthandbuch](./import.md) .
