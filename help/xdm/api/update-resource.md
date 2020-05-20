---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ressource aktualisieren
topic: developer guide
translation-type: tm+mt
source-git-commit: 0d3bee939226d9ef4ac1672b71e0d240f32c5dcf
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 2%

---


# Ressource aktualisieren

Sie können Ressourcen im Mandanten-Container mit einer PATCH-Anforderung ändern oder aktualisieren. Die Schema Registry unterstützt alle standardmäßigen JSON-Patch-Vorgänge, einschließlich Hinzufügen, Entfernen und Ersetzen.

Weitere Informationen zum JSON Patch, einschließlich der verfügbaren Operationen, finden Sie in der offiziellen [JSON Patch-Dokumentation](http://jsonpatch.com/).

>[!NOTE] Wenn Sie eine gesamte Ressource durch neue Werte ersetzen möchten, anstatt einzelne Felder zu aktualisieren, lesen Sie das Dokument zum [Ersetzen einer Ressource mit einem PUT-Vorgang](replace-resource.md).

## Hinzufügen von Mixins mit einem Schema

Einer der häufigsten PATCH-Vorgänge besteht darin, einem XDM-Schema zuvor definierte Mixins hinzuzufügen, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{RESOURCE_TYPE}` | Der Typ der Ressource, die in der Schema-Bibliothek aktualisiert werden soll. Gültige Typen sind `datatypes`, `mixins`, `schemas`und `classes`. |
| `{RESOURCE_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` die Ressource. |

**Anfrage**

Mit einem PATCH-Vorgang können Sie ein Schema aktualisieren, um Felder einzuschließen, die in einer zuvor erstellten Mischung definiert sind. Dazu müssen Sie eine PATCH-Anforderung an das Schema mit dessen `meta:altId` oder dem URL-kodierten `$id` URI durchführen.

Der Anforderungstext enthält den Vorgang (`op`), den Sie ausführen möchten, wo (`path`) Sie den Vorgang ausführen möchten und welche Informationen (`value`) Sie in den Vorgang einbeziehen möchten. In diesem Beispiel wird der `$id` Wert des mixins sowohl den Feldern `meta:extends` als auch den `allOf` Feldern für das Schema Zielgruppe hinzugefügt.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "add", "path": "/meta:extends/-", "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"}}
      ]'
```

**Antwort**

Die Antwort zeigt, dass beide Vorgänge erfolgreich durchgeführt wurden. Das mixin `$id` wurde dem `meta:extends` Array hinzugefügt und ein Verweis (`$ref`) auf das mixin wird `$id` jetzt im `allOf` Array angezeigt.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Aktualisieren einzelner Felder für eine Ressource

Sie können auch PATCH-Anforderungen senden, die mehrere Änderungen an einzelnen Feldern innerhalb einer Schema Registry-Ressource vornehmen.

**API-Format**

```SHELL
PATCH /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{RESOURCE_TYPE}` | Der Typ der Ressource, die in der Schema-Bibliothek aktualisiert werden soll. Gültige Typen sind `datatypes`, `mixins`, `schemas`und `classes`. |
| `{RESOURCE_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` die Ressource. |

**Anfrage**

Der Anforderungstext enthält den Vorgang (`op`), den Speicherort (`path`) und die Informationen (`value`), die zum Aktualisieren des Mixins erforderlich sind. Diese Anforderung aktualisiert das Eigenschaftendetails-Mixin, um das Feld &quot;propertyCity&quot;zu entfernen und ein neues Feld &quot;propertyAddress&quot;hinzuzufügen, das auf einen Standarddatentyp mit Adressinformationen verweist. Außerdem wird ein neues Feld &quot;emailAddress&quot;hinzugefügt, das auf einen Standarddatentyp mit E-Mail-Informationen verweist.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.mixins.e49cbb2eec33618f686b8344b4597ecf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
          { "op": "remove", "path": "/definitions/vehicles/properties/_{TENANT_ID}/properties/propertyCity"},
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyAddress", "value":
            {
              "title": "Property Address",
              "description": "Address of the Property",
              "$ref": "https://ns.adobe.com/xdm/common/address"
            } 
          },
          { "op": "add", "path": "/definitions/property/properties/_{TENANT_ID}/properties/emailAddress", "value":
            {
              "title": "Property Email Address",
              "description": "Email address of the Property",
              "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
            } 
          },
      ]'
```

**Antwort**

Eine erfolgreiche Antwort zeigt, dass die Vorgänge erfolgreich abgeschlossen wurden, da die neuen Felder vorhanden sind und das Feld &quot;propertyCity&quot;entfernt wurde.

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
                        },
                        "propertyAddress": {
                            "title": "Property Address",
                            "description": "Address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/common/address"
                        },
                        "emailAddress": {
                            "title": "Property Email Address",
                            "description": "Email address of the Property",
                            "$ref": "https://ns.adobe.com/xdm/context/emailaddress"
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
    "version": "1.1",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1552088205144,
        "repo:lastModifiedDate": 1552089776535,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
