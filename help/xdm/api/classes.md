---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;class registry;Schema Registry;class;Class;classes;Classes;create
solution: Experience Platform
title: Klasse erstellen
description: Mit dem Endpunkt "/classes"in der Schema Registry API können Sie XDM-Klassen in Ihrer Experience-Anwendung programmgesteuert verwalten.
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 24%

---


# Endpunkt der Klassen

Alle XDM-Schema (Experience Data Model) müssen auf einer Klasse basieren. Eine Klasse legt die Basisstruktur von allgemeinen Eigenschaften fest, die alle Schema, die auf dieser Klasse basieren, enthalten müssen, sowie welche Mixins für die Verwendung in diesen Schemas zugelassen sind. Darüber hinaus bestimmt die Klasse eines Schemas die verhaltensbezogenen Aspekte der Daten, die ein Schema enthalten soll, von denen es zwei Typen gibt:

* **[!UICONTROL Datensatz]**: Stellt Informationen zu den Attributen eines Betreffs bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.
* **[!UICONTROL Zeitreihen]**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt dar, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

>[!NOTE]
>
>Weitere Informationen zu Datenverhaltensklassen hinsichtlich ihrer Auswirkungen auf die Schema-Komposition finden Sie in den [Grundlagen der Schema-Komposition](../schema/composition.md).

Mit dem `/classes` Endpunkt in der [!DNL Schema Registry] API können Sie Klassen in Ihrer Experience-Anwendung programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Bevor Sie fortfahren, lesen Sie bitte die [Anleitung](./getting-started.md) zu den ersten Schritten für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtige Informationen zu den erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer Experience Platformen-API erforderlich sind.

## Retrieve a list of classes {#list}

Sie können alle Kurse unter dem `global` Container oder dem  Liste werden, indem Sie eine GET an `tenant` bzw. `/global/classes` `/tenant/classes`anfordern.

>[!NOTE]
>
>Bei der Auflistung von Ressourcen wird das Schema Registry-Ergebnis auf 300 Elemente begrenzt. Um Ressourcen über diese Grenze hinaus zurückzugeben, müssen Sie Paging-Parameter verwenden. Es wird außerdem empfohlen, zusätzliche Abfragen zu verwenden, um Ergebnisse zu filtern und die Anzahl der zurückgegebenen Ressourcen zu reduzieren. Weitere Informationen finden Sie im Dokument zu den Parametern für die [Abfrage](./appendix.md#query) im Anhang.

**API-Format**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, von dem Sie Klassen abrufen möchten: `global` für von der Adobe erstellte Kurse oder `tenant` für Kurse, die im Besitz Ihrer Organisation sind. |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse. Eine Liste der verfügbaren Parameter finden Sie im Dokument [im](./appendix.md#query) Anhang. |

**Anfrage**

Die folgende Anforderung ruft eine Liste von Klassen aus dem `tenant` Container ab, wobei ein `orderby` Abfrage-Parameter verwendet wird, um die Klassen nach ihrem `title` Attribut zu sortieren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

The response format depends on the `Accept` header sent in the request. The following `Accept` headers are available for listing classes:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung der einzelnen Ressourcen zurück. Dies ist die empfohlene Kopfzeile für die Auflistung der Ressourcen. (Maximal: 300) |
| `application/vnd.adobe.xed+json` | Returns full JSON class for each resource, with original `$ref` and `allOf` included. (Maximal: 300) |

**Antwort**

The request above used the `application/vnd.adobe.xed-id+json` `Accept` header, therefore the response includes only the `title`, `$id`, `meta:altId`, and `version` attributes for each class. Mit der anderen `Accept` Kopfzeile (`application/vnd.adobe.xed+json`) werden alle Attribute jeder Klasse zurückgegeben. Select the appropriate `Accept` header depending on the information you require in your response.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## Klasse nachschlagen {#lookup}

Sie können eine bestimmte Klasse nachschlagen, indem Sie die ID der Klasse in den Pfad einer GET-Anforderung einschließen.

**API-Format**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, in dem die Klasse enthalten ist, die Sie abrufen möchten: `global` für eine von der Adobe erstellte Klasse oder `tenant` für eine Klasse im Besitz Ihres Unternehmens. |
| `{CLASS_ID}` | Die `meta:altId` oder URL-kodierte `$id` Klasse, nach der Sie suchen möchten. |

**Anfrage**

Die folgende Anforderung ruft eine Klasse anhand ihres im Pfad angegebenen `meta:altId` Werts ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

The response format depends on the `Accept` header sent in the request. All lookup requests require a `version` be included in the `Accept` header. The following `Accept` headers are available:

| `Accept`-Kopfzeile | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Roh mit `$ref` und `allOf`, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Roh mit `$ref` und `allOf`, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, einschließlich Deskriptoren. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Klasse zurück. The fields that are returned depend on the `Accept` header sent in the request. Experiment with different `Accept` headers to compare the responses and determine which header is best for your use case.

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{IMS_ORG}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## Erstellen einer Klasse {#create}

Sie können eine benutzerdefinierte Klasse unter dem `tenant` Container definieren, indem Sie eine POST anfordern.

>[!IMPORTANT]
>
>Beim Erstellen eines Schemas, das auf einer von Ihnen definierten benutzerspezifischen Klasse basiert, können Sie keine standardmäßigen Mixins verwenden. Jedes Mixin definiert die Klassen, mit denen es kompatibel ist, in seinem `meta:intendedToExtend`-Attribut. Sobald Sie Mixins definiert haben, die mit Ihrer neuen Klasse kompatibel sind (durch Verwendung der `$id` Ihrer neuen Klasse im `meta:intendedToExtend`-Feld des Mixins), können Sie die Mixins jedes Mal wiederverwenden, wenn Sie ein Schema definieren, das die von Ihnen definierte Klasse implementiert. Weitere Informationen finden Sie in den Abschnitten zum [Erstellen von Mixins](./mixins.md#create) und [Erstellen von Schemas](./schemas.md#create) in den jeweiligen Endpunkthandbüchern.
>
>Wenn Sie planen, Schema auf Basis von benutzerdefinierten Klassen im Echtzeit-Kundencenter zu verwenden, sollten Sie auch bedenken, dass Schema der Vereinigung nur auf Schemas mit derselben Klasse basieren. Wenn Sie ein benutzerdefiniertes Schema in die Vereinigung für eine andere Klasse wie [!UICONTROL XDM Individual Profil] oder [!UICONTROL XDM ExperienceEvent]einbeziehen möchten, müssen Sie eine Beziehung zu einem anderen Schema herstellen, das diese Klasse verwendet. See the tutorial on [establishing a relationship between two schemas in the API](../tutorials/relationship-api.md) for more information.

**API-Format**

```http
POST /tenant/classes
```

**Anfrage**

Die Anfrage zum Erstellen einer Klasse (POST) muss ein `allOf`-Attribut enthalten, das eine `$ref` zu einem von zwei Werten enthält: `https://ns.adobe.com/xdm/data/record` oder `https://ns.adobe.com/xdm/data/time-series`. Diese Werte stellen das Verhalten dar, auf dem die Klasse basiert (Datensatz oder Zeitreihe). Weiterführende Informationen zu Unterschieden zwischen Datensatzdaten und Zeitreihendaten finden Sie im Abschnitt zu Verhaltenstypen in den [Grundlagen der Schemakomposition](../schema/composition.md).

Beim Definieren einer Klasse können Sie auch Mixins oder benutzerdefinierte Felder in die Klassendefinition einschließen. Das würde dazu führen, dass die hinzugefügten Mixins und Felder in allen Schemas enthalten sind, die die Klasse implementieren. Folgende Beispielanfrage definiert eine Klasse namens „Eigenschaft“, die Daten zu verschiedenen Eigenschaften erfasst, die von einer Firma besessen und genutzt werden. Sie enthält ein `propertyId`-Feld, das bei jeder Verwendung der Klasse eingeschlossen wird.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `_{TENANT_ID}` | Der `TENANT_ID`-Namespace für Ihre Organisation. All resources created by your organization must include this property to avoid collisions with other resources in the [!DNL Schema Registry]. |
| `allOf` | Eine Liste mit Ressourcen, deren Eigenschaften von der neuen Klasse geerbt werden sollen. Eines der `$ref`-Objekte im Array definiert das Verhalten der Klasse. In diesem Beispiel übernimmt die Klasse das Verhalten „record“. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und eine Payload mit den Details der neu erstellten Klasse zurück, einschließlich `$id`, `meta:altId` und `version`. These three values are read-only and are assigned by the [!DNL Schema Registry].

```JSON
{
  "title": "Property",
  "description": "Properties owned and operated by the company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property Identification Number",
                  "type": "string",
                  "description": "Unique Property identification number",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
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
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

Performing a GET request to [list all classes](#list) in the `tenant` container would now include the Property class. You can also [perform a lookup (GET) request](#lookup) using the URL-encoded `$id` to view the new class directly.

## Klasse aktualisieren {#put}

Sie können eine ganze Klasse durch einen PUT-Vorgang ersetzen und die Ressource im Grunde neu schreiben. Beim Aktualisieren einer Klasse über eine PUT-Anforderung muss der Textkörper alle Felder enthalten, die beim [Erstellen einer neuen Klasse](#create) in einer POST-Anforderung erforderlich sind.

>[!NOTE]
>
>If you only want to update part of a class instead of replacing it entirely, see the section on [updating a portion of a class](#patch).

**API-Format**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Die `meta:altId` oder URL-kodierte `$id` Klasse, die Sie erneut schreiben möchten. |

**Anfrage**

Mit der folgenden Anforderung wird eine vorhandene Klasse neu geschrieben, wobei deren `description` und die `title` eines ihrer Felder geändert werden.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
        "type": "object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Klasse zurück.

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
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
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Update a portion of a class {#patch}

Sie können einen Teil einer Klasse mit einer PATCH-Anforderung aktualisieren. Der [!DNL Schema Registry] unterstützt alle standardmäßigen JSON Patch-Vorgänge einschließlich `add`, `remove`und `replace`. Weitere Informationen zum JSON-Patch finden Sie im Handbuch [API-Grundlagen](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>If you want to replace an entire resource with new values instead of updating individual fields, see the section on [replacing a class using a PUT operation](#put).

**API-Format**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` die Klasse, die aktualisiert werden soll. |

**Anfrage**

Die folgende Beispielanforderung aktualisiert die `description` einer vorhandenen Klasse und die `title` eines ihrer Felder.

Der Anforderungstext besteht aus einem Array, wobei jedes aufgelistete Objekt eine bestimmte Änderung an einem einzelnen Feld darstellt. Jedes Objekt enthält die auszuführende Operation (`op`), welches Feld für die Operation ausgeführt werden soll (`path`) und welche Informationen in diesen Vorgang einzuschließen sind (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Antwort**

Die Antwort zeigt, dass beide Vorgänge erfolgreich durchgeführt wurden. Die Datei `description` wurde zusammen mit dem `title` Feld aktualisiert `propertyId` .

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
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
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{IMS_ORG}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## Klasse löschen {#delete}

Es kann gelegentlich erforderlich sein, eine Klasse aus der Schema-Registrierung zu entfernen. Dies geschieht durch eine DELETE-Anforderung mit der im Pfad angegebenen Klassen-ID.

**API-Format**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` die Klasse, die gelöscht werden soll. |

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

You can confirm the deletion by attempting a [lookup (GET) request](#lookup) for the class. You will need to include an `Accept` header in the request, but should receive an HTTP status 404 (Not Found) because the class has been removed from the Schema Registry.