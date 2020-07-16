---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ersetzen einer Ressource
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 89%

---


# Ersetzen einer Ressource

The [!DNL Schema Registry] allows you to replace an entire resource through a PUT operation. Bei diesem Vorgang wird die Ressource im Wesentlichen neu geschrieben. Daher muss der Anfrageinhalt alle Felder enthalten, die beim Erstellen einer neuen Ressource mit einer POST-Anfrage erforderlich sind.

Diese Methode ist besonders hilfreich, wenn Sie eine Menge Informationen in der Ressource gleichzeitig aktualisieren möchten.

>[!NOTE]
>
>Wenn Sie nur einen Teil einer Ressource aktualisieren möchten, anstatt sie vollständig zu ersetzen, lesen Sie das Dokument zum [Aktualisieren einer Ressource mit einem PATCH-Vorgang](update-resource.md).

**API-Format**

Eine PUT-Anfrage kann nur für Ressourcen ausgeführt werden, die Sie im Mandanten-Container definieren.

```http
PUT /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{RESOURCE_TYPE}` | The type of resource to be updated from the [!DNL Schema Library]. Gültige Typen sind `datatypes`, `mixins`, `schemas` und `classes`. |
| `{RESOURCE_ID}` | Der URL-codierte `$id`-URI oder `meta:altId` der Ressource. |

**Anfrage**

Diese Beispielanfrage ersetzt den Datentyp „Property Construction“, der in einem früheren Beispiel erstellt wurde. Der Anfrageinhalt ähnelt der POST-Anfrage, mit der der Datentyp erstellt wurde, allerdings enthält er jetzt einen aktualisierten Satz von Feldern, wobei die zuvor definierten Werte durch neue ersetzt werden.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the construction of the property.",
        "type":"object",
        "properties": {
          "dateOpened": {
            "type":"string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "standAlone",
              "highRise",
              "stripMall"
            ],
            "meta:enum": {
              "standAlone": "Stand-Alone Building",
              "highRise": "High Rise Building",
              "stripMall": "Strip Mall"
            }
          },
          "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property."
          },
          "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property."
          }
        } 
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Datentyps zurück und zeigt die aktualisierten Felder und Werte wie in der Anfrage angegeben an.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the construction of the property.",
    "type": "object",
    "properties": {
        "dateOpened": {
            "type": "string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened.",
            "meta:xdmType": "date"
        },
        "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "standAlone",
                "highRise",
                "stripMall"
            ],
            "meta:enum": {
                "standAlone": "Stand-Alone Building",
                "highRise": "High Rise Building",
                "stripMall": "Strip Mall"
            },
            "meta:xdmType": "string"
        },
        "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property.",
            "meta:xdmType": "string"
        },
        "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property.",
            "meta:xdmType": "int"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.2",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552090569013,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
