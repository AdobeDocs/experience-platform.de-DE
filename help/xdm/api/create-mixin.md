---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Mixins
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 92%

---


# Erstellen eines Mixins

Mixins sind eine Reihe von Feldern, mit denen ein bestimmtes Konzept beschrieben wird, z. B. „Adresse“ oder „Profil-Voreinstellungen“. Es stehen zahlreiche Standard-Mixins zur Verfügung. Sie können auch eigene Mixins definieren, wenn Sie Informationen erfassen möchten, die für Ihr Unternehmen individuell sind. Jedes Mixin enthält ein `meta:intendedToExtend`-Feld, in dem die Klassen, mit denen das Mixin kompatibel ist, aufgelistet werden.

Es kann hilfreich sein, alle verfügbaren Mixins zu überprüfen, um sich mit den Feldern vertraut zu machen, die in den jeweiligen Mixins enthalten sind. Sie können alle mit einer bestimmten Klasse kompatiblen Mixins (GET) auflisten, indem Sie eine Anfrage an jeden der Container „global“ und „tentant“ senden, und nur jene Mixins zurückgeben, bei denen das Feld „meta:intendedToExtend“ mit der von Ihnen verwendeten Klasse übereinstimmt. The examples below will return all mixins that can be used with the [!DNL XDM Individual Profile] class:

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

Die nachstehende Beispiel-API-Anfrage erstellt ein neues Mixin im Mandanten-Container.

**API-Format**

```http
POST /tenant/mixins
```

**Anfrage**

Beim Definieren eines neuen Mixins muss dieses ein `meta:intendedToExtend`-Attribut enthalten, in dem die `$id` der Klassen aufgelistet wird, mit dem das Mixin kompatibel ist. In diesem Beispiel ist das Mixin mit der zuvor von Ihnen definierten Property-Klasse kompatibel. Benutzerdefinierte Felder müssen unter `_{TENANT_ID}` (wie im Beispiel gezeigt) verschachtelt sein, um Kollisionen mit anderen Mixins oder Feldern aus den Klassenschemas zu vermeiden. Beachten Sie, dass das Feld `propertyConstruction` einen Verweis auf den im vorherigen Aufruf erstellten Datentyp darstellt.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Details",
        "description":"Detailed information related to the properties owned and operated by the company.",
        "type":"object",
        "meta:intendedToExtend":["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
              "type":"object",
              "properties": {
                  "propertyName": {
                    "type": "string",
                    "title": "Property Name",
                    "description": "Name of the property"
                  },
                  "propertyCity": {
                    "title": "Property City",
                    "description": "City where the property is located.",
                    "type": "string"
                  },
                  "phoneNumber": {
                    "title": "Phone Number",
                    "description": "Primary phone number for the property.",
                    "type": "string"
                  },
                  "propertyType": {
                    "type": "string",
                    "title": "Property Type",
                    "description": "Type and primary use of property.",
                    "enum": [
                        "retail",
                        "yoga",
                        "fitness"
                    ],
                    "meta:enum": {
                        "retail": "Retail Store",
                        "yoga": "Yoga Studio",
                        "fitness": "Fitness Center"
                    }
                  },
                  "propertyConstruction": {
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                  }
                }
              }
            }
          }
        },
        "allOf": [
            {
                "$ref": "#/definitions/property"
            }
        ]
}'
```

**Antwort**

Bei einer erfolgreichen Antwort werden HTTP-Status 201 (Erstellt) und eine Payload mit den Details des neu erstellten Mixins zurückgegeben, einschließlich der Werte `$id`, `meta:altId`und `version`. These values are read-only and are assigned by the [!DNL Schema Registry].

```JSON
{
    "title": "Property Details",
    "description": "Detailed information related to the properties owned and operated by the company.",
    "type": "object",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
    ],
    "definitions": {
        "property": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "propertyName": {
                            "type": "string",
                            "title": "Property Name",
                            "description": "Name of the property",
                            "meta:xdmType": "string"
                        },
                        "propertyCity": {
                            "title": "Property City",
                            "description": "City where the property is located.",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "phoneNumber": {
                            "title": "Phone Number",
                            "description": "Primary phone number for the property.",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "propertyType": {
                            "type": "string",
                            "title": "Property Type",
                            "description": "Type and primary use of property.",
                            "enum": [
                                "retail",
                                "yoga",
                                "fitness"
                            ],
                            "meta:enum": {
                                "retail": "Retail Store",
                                "yoga": "Yoga Studio",
                                "fitness": "Fitness Center"
                            },
                            "meta:xdmType": "string"
                        },
                        "propertyConstruction": {
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/property"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf",
    "version": "1.0",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552088205144,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Eine GET-Anfrage zur Auflistung aller Mixins im Mandanten-Container würde jetzt das Mixin „Fahrzeugdetails“ enthalten. Alternativ können Sie eine GET-Anfrage (Nachschlagen) mit dem URL-codierten `$id`-URI ausführen, um das neue Mixin direkt anzuzeigen. Denken Sie daran, die `version` in die Accept-Kopfzeile für alle Nachschlageanfrage einzuschließen.
