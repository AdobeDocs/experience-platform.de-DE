---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Mixins
topic: developer guide
translation-type: tm+mt
source-git-commit: b2ceac3de73ac622dc885eb388e46e93551f43a8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Erstellen eines Mixins

Mixins sind eine Reihe von Feldern, mit denen ein bestimmtes Konzept beschrieben wird, z. B. &quot;Adresse&quot;oder &quot;Profil-Voreinstellungen&quot;. Es stehen zahlreiche Standard-Mixins zur Verfügung. Sie können auch eigene Mixins definieren, wenn Sie Informationen erfassen möchten, die für Ihr Unternehmen individuell sind. Jedes Mixin enthält ein `meta:intendedToExtend` Feld, mit dem die Klassen, mit denen das Mixin kompatibel ist, Liste werden.

Es kann hilfreich sein, alle verfügbaren Mixins zu überprüfen, um sich mit den Feldern, die in den jeweiligen Mixins enthalten sind, vertraut zu machen. Sie können alle mit einer bestimmten Liste kompatiblen Mixins (GET) durch eine Anforderung an jeden der Container &quot;global&quot;und &quot;mieter&quot;zurückgeben, wobei nur die Mixins zurückgegeben werden, bei denen das Feld &quot;meta:intentedToExtend&quot;mit der verwendeten Klasse übereinstimmt. Die folgenden Beispiele geben alle Mixins zurück, die mit der XDM Individual Profil-Klasse verwendet werden können:

```http
GET /global/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
GET /tenant/mixins?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
```

Die unten stehende Beispiel-API-Anforderung erstellt eine neue Mischung im Pächter-Container.

**API-Format**

```http
POST /tenant/mixins
```

**Anfrage**

Beim Definieren eines neuen Mixins muss ein `meta:intendedToExtend` Attribut enthalten sein, in dem die Klassen aufgelistet werden, mit denen das Mixin kompatibel ist, `$id` und zwar In diesem Beispiel ist das mixin mit der zuvor definierten Property-Klasse kompatibel. Benutzerdefinierte Felder müssen unter `_{TENANT_ID}` (wie im Beispiel gezeigt) verschachtelt sein, um Kollisionen mit anderen Mixins oder Feldern aus den Klassen-Schemas zu vermeiden. Beachten Sie, dass das `propertyConstruction` Feld einen Verweis auf den im vorherigen Aufruf erstellten Datentyp darstellt.

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

Bei einer erfolgreichen Antwort werden HTTP-Status 201 (Erstellt) und eine Nutzlast mit den Details des neu erstellten Mixins zurückgegeben, einschließlich der Werte `$id`, `meta:altId`und `version`. Diese Werte sind schreibgeschützt und werden von der Schema Registry zugewiesen.

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

Wenn Sie eine GET-Anforderung zur Liste aller Mixins im Mieter-Container ausführen, wird jetzt das Mixin &quot;Fahrzeugdetails&quot;enthalten. Alternativ können Sie eine GET-Anfrage (Lookup) mit dem URL-kodierten `$id` URI ausführen, um das neue Mixin direkt Ansicht. Denken Sie daran, die `version` in den Accept-Header für alle Nachschlageanforderungen einzuschließen.
