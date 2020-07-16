---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Datentyps
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 95%

---


# Erstellen eines Datentyps

Bestehen allgemeine Datenstrukturen, die Ihr Unternehmen auf verschiedene Weise verwenden möchte, kann die Definition eines Datentyps von Vorteil sein. Datentypen stellen die konsistente Verwendung von Mehrfeld-Strukturen sicher und sind flexibler als Mixins, da sie an jeder beliebigen Stelle in einem Schema enthalten sein können, indem sie als `type` eines Felds hinzugefügt werden.

Anders ausgedrückt muss bei Datentypen eine Objekthierarchie nur einmal definiert werden. Anschließend kann sie, ganz ähnlich wie bei jedem anderen Typ von Skalar, in einem Feld darauf verweisen.

**API-Format**

```http
POST /tenant/datatypes
```

**Anfrage**

Für die Definition von Datentypen sind weder die Felder `meta:extends` und `meta:intendedToExtend` erforderlich, noch müssen Felder zur Vermeidung verschachtelt sein, um Konflikte zu vermeiden.

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

Bei erfolgreicher Antwort wird der HTTP-Statuscode 201 (Erstellung bestätigt) und eine Payload zurückgegeben, die Details zum neu erstellten Datentyp einschließlich `$id`, `meta:altId` und `version` enthält. These three values are read-only and are assigned by the [!DNL Schema Registry].

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

Eine GET-Anfrage zum Auflisten aller Datentypen im Mandanten-Container würde jetzt den Datentyp „Property Construction“ (Datentyp-Erstellung) umfassen. Auch können Sie mittels Anfrage zum Nachschlagen (GET) unter Angabe der URL-codierten `$id`-URI des Schemas den neuen Datentyp direkt anzeigen. Stellen Sie sicher, dass Ihre Anfrage zum Nachschlagen in der Accept-Kopfzeile die `version` enthält.
