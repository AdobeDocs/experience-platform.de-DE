---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Datentypregistrierung;Schemaregistrierung;Datentyp;Datentypen;erstellen
solution: Experience Platform
title: Datentypen-API-Endpunkt
description: Mit dem Endpunkt /datatypes in der Schema Registry-API können Sie XDM-Datentypen in Ihrer Erlebnisanwendung programmgesteuert verwalten.
exl-id: 2a58d641-c681-40cf-acc8-7ad842cd6243
source-git-commit: 6e58f070c0a25d7434f1f165543f92ec5a081e66
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 13%

---

# Datentyp-Endpunkt

Datentypen werden in Klassen oder Schemafeldergruppen auf dieselbe Weise als Felder vom Typ „Verweis“ verwendet wie grundlegende Literalfelder, wobei der wesentliche Unterschied darin besteht, dass Datentypen mehrere Unterfelder definieren können. Datentypen ähneln zwar den Feldergruppen insofern, als sie die konsistente Verwendung einer Struktur mit mehreren Feldern ermöglichen, sind jedoch flexibler, da sie an einer beliebigen Stelle in die Schemastruktur aufgenommen werden können, während Feldergruppen nur auf der Stammebene hinzugefügt werden können. Mit dem `/datatypes`-Endpunkt in der [!DNL Schema Registry]-API können Sie Datentypen in Ihrem Erlebnisprogramm programmgesteuert verwalten.

>[!NOTE]
>
>Wenn ein Feld als spezifischer Datentyp definiert ist, können Sie dasselbe Feld mit einem anderen Datentyp in einem anderen Schema nicht erstellen. Diese Einschränkung gilt für den Mandanten Ihrer Organisation.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste von Datentypen {#list}

Sie können alle Datentypen unter dem `global`- oder `tenant`-Container auflisten, indem Sie eine GET-Anfrage an `/global/datatypes` bzw. `/tenant/datatypes` stellen.

>[!NOTE]
>
>Beim Auflisten von Ressourcen beschränkt die Schemaregistrierung Ergebnismengen auf 300 Elemente. Um Ressourcen über dieses Limit hinaus zurückzugeben, müssen Sie Paging-Parameter verwenden. Es wird außerdem empfohlen, zusätzliche Abfrageparameter zu verwenden, um Ergebnisse zu filtern und die Anzahl der zurückgegebenen Ressourcen zu reduzieren. Weitere Informationen finden Sie [ Abschnitt ](./appendix.md#query)Abfrageparameter“ im Anhang.

**API-Format**

```http
GET /{CONTAINER_ID}/datatypes?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, aus dem Sie Datentypen abrufen möchten: `global` für vom Adobe erstellte Datentypen oder `tenant` für Datentypen Ihres Unternehmens. |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse nach . Eine Liste der verfügbaren Parameter finden [ im ](./appendix.md#query)-Dokument . |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft eine Liste von Datentypen aus dem `tenant`-Container ab und verwendet einen `orderby` Abfrageparameter, um die Datentypen nach ihrem `title` Attribut zu sortieren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Format der Antwort hängt von der in der Anfrage gesendeten `Accept`-Kopfzeile ab. Die folgenden `Accept`-Kopfzeilen sind für die Auflistung von Datentypen verfügbar:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung jeder Ressource zurück. Dies ist die empfohlene Kopfzeile zum Auflisten von Ressourcen. (Limit: 300) |
| `application/vnd.adobe.xed+json` | Gibt den vollständigen JSON-Datentyp für jede Ressource mit `$ref` und `allOf` zurück. (Limit: 300) |

{style="table-layout:auto"}

**Antwort**

Die obige Anfrage verwendete den `application/vnd.adobe.xed-id+json` `Accept`-Header. Daher enthält die Antwort für jeden Datentyp nur die Attribute `title`, `$id`, `meta:altId` und `version`. Bei Verwendung der anderen `Accept`-Kopfzeile (`application/vnd.adobe.xed+json`) werden alle Attribute jedes Datentyps zurückgegeben. Wählen Sie den entsprechenden `Accept`-Header entsprechend den Informationen aus, die Sie in Ihrer Antwort benötigen.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
      "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
      "version": "1.0",
      "title": "Loyalty"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/4b0329b5573cbb7cb757db667d7fdf66",
      "meta:altId": "_{TENANT_ID}.datatypes.4b0329b5573cbb7cb757db667d7fdf66",
      "version": "1.0",
      "title": "Property Details"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 2
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/datatypes?orderby=title"
    }
  }
}
```

## Nachschlagen eines Datentyps {#lookup}

Sie können einen bestimmten Datentyp suchen, indem Sie die ID des Datentyps in den Pfad einer GET-Anfrage aufnehmen.

**API-Format**

```http
GET /{CONTAINER_ID}/datatypes/{DATA_TYPE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, der den Datentyp enthält, den Sie abrufen möchten: `global` für einen von Adobe erstellten Datentyp oder `tenant` für einen Datentyp, der Ihrem Unternehmen gehört. |
| `{DATA_TYPE_ID}` | Die `meta:altId` oder URL-kodierte `$id` des Datentyps, den Sie suchen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft einen Datentyp anhand des im Pfad angegebenen `meta:altId`-Werts ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Format der Antwort hängt von der in der Anfrage gesendeten `Accept`-Kopfzeile ab. Bei allen Suchanfragen muss eine `version` in die `Accept`-Kopfzeile aufgenommen werden. Die folgenden `Accept` sind verfügbar:

| `Accept`-Kopfzeile | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Roh mit `$ref` und `allOf`, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` und `allOf` aufgelöst, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Roh mit `$ref` und `allOf`, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` und `allOf` aufgelöst, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` und `allOf` aufgelöst, einschließlich Deskriptoren. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Datentyps zurück. Die zurückgegebenen Felder hängen von der `Accept` ab, die in der Anfrage gesendet wird. Experimentieren Sie mit verschiedenen `Accept`-Kopfzeilen, um die Antworten zu vergleichen und festzustellen, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/78570e371092c032260714dd8bfd6d44",
  "meta:altId": "_{TENANT_ID}.datatypes.78570e371092c032260714dd8bfd6d44",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty",
  "type": "object",
  "description": "Loyalty object containing loyalty-specific fields.",
  "definitions": {
    "customFields": {
      "properties": {
        "loyaltyId": {
          "title": "Loyalty ID",
          "description": "Unique loyalty program member ID. Should be in the format of an email address.",
          "type": "string",
          "meta:xdmType": "string"
        },
        "memberSince": {
          "title": "Member Since",
          "description": "Date person joined loyalty program.",
          "type": "string",
          "format": "date",
          "meta:xdmType": "date"
        },
        "points": {
          "title": "Points",
          "description": "Accumulated loyalty points",
          "type": "integer",
          "meta:xdmType": "int"
        },
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "The current loyalty program level to which the individual member belongs.",
          "type": "string",
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ],
          "meta:enum": {
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          },
          "meta:xdmType": "string"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1557529442681,
    "repo:lastModifiedDate": 1557529442681,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "50b8008b588e911314f9685240dd4c23a247f37179a6d9ff6ba3877dc11ca504",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Erstellen eines Datentyps {#create}

Sie können einen benutzerdefinierten Datentyp unter dem `tenant`-Container definieren, indem Sie eine POST-Anfrage stellen.

**API-Format**

```http
POST /tenant/datatypes
```

**Anfrage**

Im Gegensatz zu Feldergruppen sind für die Definition eines Datentyps keine `meta:extends` oder `meta:intendedToExtend` Felder erforderlich. Ebenso wenig müssen Felder verschachtelt werden, um Kollisionen zu vermeiden.

Bei der Definition der Feldstruktur des Datentyps selbst können Sie primitive Typen verwenden (z. B. `string` oder `object`) oder Sie können durch `$ref` Attribute auf andere vorhandene Datentypen verweisen. Ausführliche Anleitungen zum erwarteten [ für verschiedene XDM-Feldtypen finden Sie ](../tutorials/custom-fields-api.md) Handbuch unter „Definieren benutzerdefinierter XDM-Felder in der API“.

Die folgende Anfrage erstellt einen Objekttyp „Eigenschaftskonstruktion“ mit den Untereigenschaften `yearBuilt`, `propertyType` und `location`:

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
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
              "shoppingCenter": "Shopping Center"
            }
          },
          "location": {
            "title": "Location",
            "description": "The physical location of the property.",
            "$ref": "https://ns.adobe.com/xdm/common/address"
          }
        }
      }'
```

**Antwort**

Bei erfolgreicher Antwort wird der HTTP-Status-Code 201 (Erstellung bestätigt) und eine Payload zurückgegeben, die Details zum neu erstellten Datentyp einschließlich `$id`, `meta:altId` und `version` enthält. Diese drei Werte sind schreibgeschützt und werden vom [!DNL Schema Registry] zugewiesen.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:altId": "_{TENANT_ID}.datatypes.669ffcc61cf5e94e8640dbe6a15f0f24eb3cd1ddbbfb6b36",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
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
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "location": {
      "title": "Location",
      "description": "The physical location of the property.",
      "$ref": "https://ns.adobe.com/xdm/common/address",
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "refs": [
    "https://ns.adobe.com/xdm/common/address"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1670885230789,
    "repo:lastModifiedDate": 1670885230789,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "d3cc803a1f8daa06b7c150d882bd337d88f4d5d5f08d36cfc4c2849dc0255f7e",
    "meta:globalLibVersion": "1.38.3.1"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Wenn Sie eine GET-Anfrage ausführen[ um alle Datentypen ](#list) Mandanten-Container aufzulisten, würde dies jetzt den Datentyp Eigenschaftsdetails enthalten, oder Sie können [eine Suchanfrage (GET) ](#lookup), indem Sie den URL-kodierten `$id`-URI verwenden, um den neuen Datentyp direkt anzuzeigen.

## Aktualisieren eines Datentyps {#put}

Sie können einen gesamten Datentyp durch einen PUT-Vorgang ersetzen, wobei die Ressource im Wesentlichen neu geschrieben wird. Beim Aktualisieren eines Datentyps über eine PUT-Anfrage muss der Hauptteil alle Felder enthalten, die beim [Erstellen eines neuen Datentyps](#create) in einer POST-Anfrage erforderlich sind.

>[!NOTE]
>
>Wenn Sie nur einen Teil eines Datentyps aktualisieren möchten, anstatt ihn vollständig zu ersetzen, finden Sie weitere Informationen im Abschnitt [Aktualisieren eines Teils eines Datentyps](#patch).

**API-Format**

```http
PUT /tenant/datatypes/{DATA_TYPE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATA_TYPE_ID}` | Die `meta:altId` oder URL-kodierte `$id` des Datentyps, den Sie umschreiben möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage schreibt einen vorhandenen Datentyp neu und fügt ein neues `floorSize` hinzu.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Construction",
        "description": "Information related to the property construction",
        "type": "object",
        "properties": {
          "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type": "string",
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
              "shoppingCenter": "Shopping Center"
            }
          },
          "floorSize" {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        } 
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Datentyps zurück.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:altId": "_{TENANT_ID}.datatypes.7602bc6e97e5786a31c95d9e6531a1596687433451d97bc1",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Property Construction",
  "type": "object",
  "description": "Information related to the property construction",
  "properties": {
    "yearBuilt": {
      "type": "integer",
      "title": "Year Built",
      "description": "The year the property was constructed.",
      "meta:xdmType": "int"
    },
    "propertyType": {
      "type": "string",
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
        "shoppingCenter": "Shopping Center"
      },
      "meta:xdmType": "string"
    },
    "floorSize" {
      "type":  "integer",
      "title":  "Floor Size",
      "description":  "The floor size of the property, in square feet.",
      "meta:xdmType": "int"
    }
  },
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1604524729435,
    "repo:lastModifiedDate": 1604524729435,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1c838764342756868ca1297869f582a38d15f03ed0acfc97fda7532d22e942c7",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Aktualisieren eines Teils eines Datentyps {#patch}

Sie können einen Teil eines Datentyps mithilfe einer PATCH-Anfrage aktualisieren. Der [!DNL Schema Registry] unterstützt alle standardmäßigen JSON-Patch-Vorgänge, einschließlich `add`, `remove` und `replace`. Weitere Informationen zu JSON-Patch-Vorgängen finden Sie im [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Wenn Sie eine gesamte Ressource durch neue Werte ersetzen möchten, anstatt einzelne Felder zu aktualisieren, lesen Sie den Abschnitt über [Ersetzen eines Datentyps mithilfe eines PUT-Vorgangs](#put).

**API-Format**

```http
PATCH /tenant/data type/{DATA_TYPE_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATA_TYPE_ID}` | Die URL-codierte `$id`-URI oder -`meta:altId` des Datentyps, den Sie aktualisieren möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Beispielanfrage aktualisiert die `description` eines vorhandenen Datentyps und fügt ein neues `floorSize` hinzu.

Der Anfragetext hat die Form eines Arrays, wobei jedes aufgelistete Objekt eine bestimmte Änderung an einem einzelnen Feld darstellt. Jedes Objekt enthält den auszuführenden Vorgang (`op`), in welchem Feld der Vorgang ausgeführt werden soll (`path`) und welche Informationen in diesem Vorgang enthalten sein sollen (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Construction-related information for a company-operated property."
        },
        { 
          "op": "add",
          "path": "/properties/floorSize",
          "value": {
            "type": "integer",
            "title": "Floor Size",
            "description": "The floor size of the property, in square feet."
          }
        }
      ]'
```

**Antwort**

Die Antwort zeigt, dass beide Vorgänge erfolgreich durchgeführt wurden. Die `description` wurde aktualisiert und `floorSize` wurde unter `definitions` hinzugefügt.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type": "object",
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
  "imsOrg": "{ORG_ID}",
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

## Löschen eines Datentyps {#delete}

Gelegentlich kann es erforderlich sein, einen Datentyp aus der Schemaregistrierung zu entfernen. Dies geschieht, indem eine DELETE-Anfrage mit der Datentyp-ID durchgeführt wird, die im Pfad angegeben ist.

**API-Format**

```http
DELETE /tenant/datatypes/{DATA_TYPE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATA_TYPE_ID}` | Die URL-codierte `$id`-URI oder `meta:altId` des Datentyps, den Sie löschen möchten. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine [Suchanfrage (GET)) ](#lookup) Datentyp ausführen. Sie müssen einen `Accept`-Header in die Anfrage einbeziehen, sollten jedoch einen HTTP-Status 404 (Nicht gefunden) erhalten, da der Datentyp aus der Schemaregistrierung entfernt wurde.
