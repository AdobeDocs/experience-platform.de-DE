---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datentyp erstellen
topic: developer guide
translation-type: tm+mt
source-git-commit: b0d8c8ee4df11d601d8feb122c70a9cd5d7d5b77
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Datentyp erstellen

Wenn es gemeinsame Datenstrukturen gibt, die Ihr Unternehmen auf verschiedene Weise verwenden möchte, sollten Sie eventuell einen Datentyp definieren. Datentypen ermöglichen den konsistenten Einsatz von Strukturen mit mehreren Feldern und bieten mehr Flexibilität als Mixins, da sie an jeder beliebigen Stelle in einem Schema enthalten sein können, indem sie als Feldelement `type` hinzugefügt werden.

Mit anderen Worten, Datentypen ermöglichen es Ihnen, eine Objekthierarchie einmal zu definieren und auf sie in einem Feld zu verweisen, genau wie jeder andere Skalartyp.

**API-Format**

```http
POST /tenant/datatypes
```

**Anfrage**

Für die Definition eines Datentyps sind weder `meta:extends` noch `meta:intendedToExtend` Felder erforderlich, noch müssen Felder verschachtelt sein, um Kollisionen zu vermeiden.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und eine Nutzlast mit den Details des neu erstellten Datentyps zurück, einschließlich der Variablen `$id`, `meta:altId`und `version`. Diese drei Werte sind schreibgeschützt und werden von der Schema Registry zugewiesen.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the property construction",
    "type": "object",
    "properties": {
        "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed.",
            "meta:xdmType": "int"
        },
        "constructionType": {
            "type": "string",
            "title": "Construction Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "freeStanding",
                "mall",
                "shoppingCenter"
            ],
            "meta:enum": {
                "freeStanding": "Free Standing Building",
                "mall": "Mall Space",
                "shoppingCentre": "Shopping Center"
            },
            "meta:xdmType": "string"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552087079285,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Wenn Sie eine GET-Anforderung zur Liste aller Datentypen im Mieter-Container ausführen, wird jetzt der Datentyp &quot;Eigenschaftenaufbau&quot;einbezogen. Sie können auch eine GET-Anfrage (Lookup) mit dem URL-kodierten `$id` URI ausführen, um den neuen Datentyp direkt Ansicht. Stellen Sie sicher, dass Sie die `version` in Ihren Accept-Header für eine Suchanfrage aufnehmen.
