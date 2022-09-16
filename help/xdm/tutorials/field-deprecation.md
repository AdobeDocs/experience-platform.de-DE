---
title: Veraltetes XDM-Feld
description: Erfahren Sie, wie Sie Experience-Datenmodell (XDM)-Felder in der Schema Registry-API verwerfen.
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: 32d4a364ba740194d4fd7a0f4df7bd69f25f62b8
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 6%

---

# Veraltetes XDM-Feld

Im Experience-Datenmodell (XDM) können Sie ein Feld in einem Schema oder einer benutzerdefinierten Ressource verwerfen, indem Sie die [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Wenn ein Feld veraltet wird, wird es in den nachgelagerten Benutzeroberflächen wie der [!UICONTROL Profile] Arbeitsbereich und Customer Journey Analytics, es handelt sich jedoch andernfalls um eine nicht brechende Änderung, die sich nicht negativ auf bestehende Datenflüsse auswirkt.

In diesem Dokument wird beschrieben, wie Felder für verschiedene XDM-Ressourcen nicht mehr unterstützt werden.

## Erste Schritte

Dieses Tutorial erfordert Aufrufe an die Schema Registry-API. Lesen Sie die [Entwicklerhandbuch](../api/getting-started.md) für wichtige Informationen, die Sie für diese API-Aufrufe benötigen. Dies umfasst Ihre `{TENANT_ID}`, das Konzept der &quot;Container&quot;und die erforderlichen Kopfzeilen für Anfragen (mit besonderem Augenmerk auf die `Accept` -Kopfzeile und die möglichen Werte).

## Benutzerdefiniertes Feld verwerfen {#custom}

Um ein Feld in einer benutzerdefinierten Klasse, Feldergruppe oder einem Datentyp als veraltet zu kennzeichnen, aktualisieren Sie die benutzerdefinierte Ressource über eine PUT- oder PATCH-Anfrage und fügen Sie das Attribut hinzu `meta:status: deprecated` auf das entsprechende Feld.

>[!NOTE]
>
>Allgemeine Informationen zum Aktualisieren von benutzerdefinierten Ressourcen in XDM finden Sie in der folgenden Dokumentation:
>
>* [Klasse aktualisieren](../api/classes.md#patch)
>* [Aktualisieren von Feldergruppen](../api/field-groups.md#patch)
>* [Datentyp aktualisieren](../api/data-types.md#patch)


Der folgende Beispiel-API-Aufruf stellt ein Feld in einem benutzerdefinierten Datentyp ein.

**API-Format**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Anfrage**

Die folgende Anfrage stellt die `expansionArea` für einen Datentyp, der eine Immobilien-Property beschreibt.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/properties/expansionArea/meta:status",
          "value": "deprecated"
        }
      ]'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Aktualisierungsdetails der benutzerdefinierten Ressource zurück, wobei das veraltete Feld eine `meta:status` Wert von `deprecated`. Die folgende Beispielantwort wurde aus Platzgründen gekürzt.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a real-estate property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "expansionArea": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
              "meta:status": "deprecated",
            },
            "propertyName": {
              "title": "Property Name",
              "description": "Name of the property",
              "type": "string"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
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
            },
            "squareFeet": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
            }
          }
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
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Standardfelder in Schemata nicht mehr verwenden {#standard}

Felder von Standardklassen, Feldergruppen und Datentypen können nicht direkt entfernt werden. Stattdessen können Sie deren Verwendung in den einzelnen Schemas, die diese Standardressourcen verwenden, mithilfe eines Deskriptors verzögern.

### Erstellen eines Deskriptors für die Einstellung von Feldern {#create-descriptor}

Um einen Deskriptor für die Schemafelder zu erstellen, die veraltet werden sollen, stellen Sie eine POST-Anfrage an die `/tenant/descriptors` -Endpunkt.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:descriptorDeprecated",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/faxPhone"
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des Deskriptors. Für einen Deskriptor zur Einstellung von Feldern muss dieser Wert auf `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | Der URI `$id` des Schemas, auf das Sie den Deskriptor anwenden. |
| `xdm:sourceVersion` | Die Version des Schemas, auf das Sie den Deskriptor anwenden. Sollte auf `1`. |
| `xdm:sourceProperty` | Der Pfad zur Eigenschaft innerhalb des Schemas, auf das Sie den Deskriptor anwenden. Wenn Sie den Deskriptor auf mehrere Eigenschaften anwenden möchten, können Sie eine Liste von Pfaden in Form eines Arrays bereitstellen (z. B. `["/firstName", "/lastName"]`). |

**Antwort**

```json
{
    "@id": "d882b1202bac0ac71f1e31fbcd9afbcc37f364270186b4b3",
    "@type": "xdm:descriptorDeprecated",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/faxPhone",
    "imsOrg": "{IMS_ORG}",
    "version": "1",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

### Veraltetes Feld überprüfen {#verify-deprecation}

Nachdem der Deskriptor angewendet wurde, können Sie überprüfen, ob das Feld veraltet ist, indem Sie das betreffende Schema nachschlagen und dabei die entsprechende `Accept` -Kopfzeile.

>[!NOTE]
>
>Das Anzeigen veralteter Felder bei der Auflistung von Schemas wird derzeit nicht unterstützt.

**API-Format**

```http
GET /tenant/schemas
```

**Anfrage**

Um Informationen zu veralteten Feldern in die API-Antwort aufzunehmen, müssen Sie die Variable `Accept` -Kopfzeile zu `application/vnd.adobe.xed-deprecatefield+json; version=1`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-deprecatefield+json; version=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Schemas zurück, wobei das veraltete Feld eine `meta:status` Wert von `deprecated`. Die folgende Beispielantwort wurde aus Platzgründen gekürzt.

```json
"faxPhone": {
    "title": "Fax phone",
    "description": "Fax phone number.",
    "type": "object",
    "meta:xdmType": "object",
    "properties": {},
    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
    "meta:xdmField": "xdm:faxPhone",
    "meta:status": "deprecated"
}
```

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie XDM-Felder mithilfe der Schema Registry-API nicht mehr unterstützt werden. Weitere Informationen zum Konfigurieren von Feldern für benutzerdefinierte Ressourcen finden Sie im Handbuch unter [Definieren von XDM-Feldern in der API](./custom-fields-api.md). Weitere Informationen zum Verwalten von Deskriptoren finden Sie unter [Endpunktleitfaden für Deskriptoren](../api/descriptors.md).
