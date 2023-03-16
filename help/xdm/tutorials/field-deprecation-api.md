---
title: Verwerfen eines XDM-Felds in der API
description: Erfahren Sie, wie Sie Experience-Datenmodell-Felder (XDM) in der Schema Registry-API verwerfen.
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: f9f783b75bff66d1bf3e9c6d1ed1c543bd248302
workflow-type: ht
source-wordcount: '588'
ht-degree: 100%

---

# Ein XDM-Feld in der API verwerfen

Im Experience-Datenmodell (XDM) können Sie ein Feld in einem Schema oder einer benutzerdefinierten Ressource verwerfen, indem Sie die [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) verwenden. Wenn ein Feld verworfen wird, wird es in nachgelagerten Benutzeroberflächen wie dem Arbeitsbereich [!UICONTROL Profile] und Customer Journey Analytics ausgeblendet; dies ist jedoch keine grundlegende Veränderung und wirkt sich nicht negativ auf bestehende Datenflüsse aus.

In diesem Dokument wird beschrieben, wie Felder für verschiedene XDM-Ressourcen verworfen werden können. Anweisungen zum Verwerfen eines XDM-Felds mithilfe des Schema-Editors in der Experience Platform-Benutzeroberfläche finden Sie im Tutorial zum [Verwerfen eines XDM-Felds in der Benutzeroberfläche](./field-deprecation-ui.md).

## Erste Schritte

Dieses Tutorial erfordert Aufrufe an die Schema Registry-API. Lesen Sie das [Entwicklerhandbuch](../api/getting-started.md) für wichtige Informationen, die Sie für diese API-Aufrufe benötigen. Dazu gehören Ihre `{TENANT_ID}`, das Konzept der „Container“ und die erforderlichen Header für Anfragen (mit besonderem Augenmerk auf den `Accept`-Header und seine möglichen Werte).

## Verwerfen eines benutzerdefinierten Felds {#custom}

Um ein Feld in einer benutzerdefinierten Klasse, Feldergruppe oder einem Datentyp zu verwerfen, aktualisieren Sie die benutzerdefinierte Ressource über eine PUT- oder PATCH-Anfrage und fügen Sie dem entsprechenden Feld das Attribut `meta:status: deprecated` hinzu.

>[!NOTE]
>
>Allgemeine Informationen zum Aktualisieren von benutzerdefinierten Ressourcen in XDM finden Sie in der folgenden Dokumentation:
>
>* [Aktualisieren einer Klasse](../api/classes.md#patch)
>* [Aktualisieren einer Feldergruppe](../api/field-groups.md#patch)
>* [Aktualisieren eines Datentyps](../api/data-types.md#patch)


Im folgenden Beispiel für einen API-Aufruf wird ein Feld in einem benutzerdefinierten Datentyp verworfen.

**API-Format**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Anfrage**

Die folgende Anfrage verwirft das Feld `expansionArea` für einen Datentyp, der ein Immobilienobjekt beschreibt.

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

Eine erfolgreiche Antwort gibt die Aktualisierungsdetails der benutzerdefinierten Ressource zurück, wobei das verworfene Feld den Wert `meta:status` von `deprecated` enthält. Die folgende Beispielantwort wurde aus Platzgründen gekürzt.

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

## Verwerfen eines Standardfelds in einem Schema {#standard}

Felder von Standardklassen, Feldergruppen und Datentypen können nicht direkt verworfen werden. Stattdessen kann mithilfe eines Deskriptors ihre Verwendung in den einzelnen Schemata verworfen werden, die diese Standardressourcen verwenden.

### Erstellen eines Deskriptors zum Verwerfen eines Felds {#create-descriptor}

Um einen Deskriptor für die Schemafelder zu erstellen, die verworfen werden sollen, stellen Sie eine POST-Anfrage an den Endpunkt `/tenant/descriptors`.

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
| `@type` | Der Typ des Deskriptors. Für einen Deskriptor zum Verwerfen von Feldern muss dieser Wert auf `xdm:descriptorDeprecated` gesetzt werden. |
| `xdm:sourceSchema` | Der URI `$id` des Schemas, auf das Sie den Deskriptor anwenden. |
| `xdm:sourceVersion` | Die Version des Schemas, auf das Sie den Deskriptor anwenden. Sollte auf `1` gesetzt werden. |
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

### Überprüfen des verworfenen Felds {#verify-deprecation}

Nachdem der Deskriptor angewendet wurde, können Sie überprüfen, ob das Feld verworfen wurde, indem Sie das betreffende Schema nachschlagen und dabei den entsprechenden `Accept`-Header verwenden.

>[!NOTE]
>
>Das Anzeigen verworfener Felder bei der Auflistung von Schemata wird derzeit nicht unterstützt.

**API-Format**

```http
GET /tenant/schemas
```

**Anfrage**

Um Informationen zu verworfenen Feldern in die API-Antwort aufzunehmen, müssen Sie den `Accept`-Header auf `application/vnd.adobe.xed-deprecatefield+json; version=1` setzen.

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

Eine erfolgreiche Antwort gibt die Details des Schemas zurück, wobei das verworfene Feld den Wert `meta:status` von `deprecated` enthält. Die folgende Beispielantwort wurde aus Platzgründen gekürzt.

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

In diesem Dokument wird beschrieben, wie Sie XDM-Felder mithilfe der Schema Registry-API verwerfen können. Weitere Informationen zum Konfigurieren von Feldern für benutzerdefinierte Ressourcen finden Sie im Handbuch unter [Definieren von XDM-Feldern in der API](./custom-fields-api.md). Weitere Informationen zum Verwalten von Deskriptoren finden Sie unter [Handbuch für Deskriptoren-Endpunkte](../api/descriptors.md).
