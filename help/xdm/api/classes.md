---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Klassenregistrierung; Schema Registry; Klasse; Klassen; erstellen
solution: Experience Platform
title: Klassen-API-Endpunkt
description: Mit dem Endpunkt /classes in der Schema Registry-API können Sie XDM-Klassen in Ihrer Erlebnisanwendung programmgesteuert verwalten.
topic-legacy: developer guide
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 23%

---

# Klassenendpunkt

Alle Experience-Datenmodell (XDM)-Schemas müssen auf einer Klasse basieren. Eine Klasse bestimmt die Basisstruktur von allgemeinen Eigenschaften, die alle Schemas, die auf dieser Klasse basieren, enthalten müssen, sowie welche Schemafeldgruppen für die Verwendung in diesen Schemas geeignet sind. Darüber hinaus bestimmt die Klasse eines Schemas die verhaltensbezogenen Aspekte der Daten, die ein Schema enthalten soll, von denen es zwei Typen gibt:

* **[!UICONTROL Datensatz]**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt kann ein Unternehmen oder eine Person sein.
* **[!UICONTROL Zeitreihe]**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

>[!NOTE]
>
>Weitere Informationen zu Datenverhaltensklassen hinsichtlich ihrer Auswirkungen auf die Schemakomposition finden Sie im Abschnitt [Grundlagen der Schemakomposition](../schema/composition.md).

Die `/classes` -Endpunkt im [!DNL Schema Registry] Mit der API können Sie Klassen in Ihrer Erlebnisanwendung programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Liste von Klassen abrufen {#list}

Sie können alle Klassen unter der `global` oder `tenant` Container durch eine GET-Anfrage an `/global/classes` oder `/tenant/classes`zurück.

>[!NOTE]
>
>Bei der Auflistung von Ressourcen beschränkt die Schema Registry Ergebnissätze auf 300 Elemente. Um Ressourcen zurückzugeben, die über diese Grenze hinausgehen, müssen Sie Paging-Parameter verwenden. Es wird außerdem empfohlen, zusätzliche Abfrageparameter zu verwenden, um Ergebnisse zu filtern und die Anzahl der zurückgegebenen Ressourcen zu reduzieren. Siehe Abschnitt zu [Abfrageparameter](./appendix.md#query) im Anhang für weitere Informationen.

**API-Format**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, aus dem Sie Klassen abrufen möchten: `global` für von Adoben erstellte Klassen oder `tenant` für Kurse, die Ihrer Organisation gehören. |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse. Siehe [Anhang](./appendix.md#query) für eine Liste der verfügbaren Parameter. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage ruft eine Liste von Klassen aus der `tenant` Container, mithilfe eines `orderby` Abfrageparameter, um die Klassen nach ihren `title` -Attribut.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept` -Kopfzeile, die in der Anfrage gesendet wird. Folgendes `Accept` -Header sind für die Auflistung von Klassen verfügbar:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung jeder Ressource zurück. Dies ist die empfohlene Kopfzeile für die Auflistung von Ressourcen. (Limit: 300) |
| `application/vnd.adobe.xed+json` | Gibt für jede Ressource die vollständige JSON-Klasse mit der ursprünglichen `$ref` und `allOf` enthalten. (Limit: 300) |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Die obige Anfrage verwendete die `application/vnd.adobe.xed-id+json` `Accept` -Kopfzeile; daher enthält die Antwort nur die `title`, `$id`, `meta:altId`und `version` -Attribute für jede Klasse. Andere verwenden `Accept` header (`application/vnd.adobe.xed+json`) gibt alle Attribute jeder Klasse zurück. Wählen Sie die entsprechende `Accept` -Kopfzeile entsprechend den Informationen, die Sie in Ihrer Antwort benötigen.

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

Sie können nach einer bestimmten Klasse suchen, indem Sie die ID der Klasse in den Pfad einer GET-Anfrage einschließen.

**API-Format**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, der die Klasse enthält, die Sie abrufen möchten: `global` für eine von der Adobe erstellte Klasse oder `tenant` für eine Klasse, die Ihrem Unternehmen gehört. |
| `{CLASS_ID}` | Die `meta:altId` oder URL-kodiert `$id` der Klasse, die Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage ruft eine Klasse anhand ihrer `meta:altId` -Wert, der im Pfad angegeben wird.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept` -Kopfzeile, die in der Anfrage gesendet wird. Alle Suchanfragen erfordern eine `version` enthalten sein. `Accept` -Kopfzeile. Folgendes `Accept` Header sind verfügbar:

| `Accept`-Kopfzeile | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Roh mit `$ref` und `allOf`, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` und `allOf` aufgelöst, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Roh mit `$ref` und `allOf`, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` und `allOf` aufgelöst, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` und `allOf` aufgelöst, einschließlich Deskriptoren. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Klasse zurück. Die zurückgegebenen Felder hängen von der `Accept` -Kopfzeile, die in der Anfrage gesendet wird. Experimentieren mit verschiedenen `Accept` Kopfzeilen zum Vergleich der Antworten und zur Bestimmung der Kopfzeile, die für Ihren Anwendungsfall am besten geeignet ist.

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
  "imsOrg":"{ORG_ID}",
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

## Klasse erstellen {#create}

Sie können eine benutzerdefinierte Klasse unter der `tenant` -Container, indem Sie eine POST-Anfrage ausführen.

>[!IMPORTANT]
>
>Beim Erstellen eines Schemas, das auf einer von Ihnen definierten benutzerdefinierten Klasse basiert, können Sie keine Standardfeldgruppen verwenden. Jede Feldergruppe definiert die Klassen, mit denen sie kompatibel sind, in ihren `meta:intendedToExtend` -Attribut. Sobald Sie mit der Definition von Feldergruppen beginnen, die mit Ihrer neuen Klasse kompatibel sind (mithilfe der `$id` Ihrer neuen Klasse im `meta:intendedToExtend` -Feld der Feldergruppe), können Sie diese Feldergruppen jedes Mal wiederverwenden, wenn Sie ein Schema definieren, das die von Ihnen definierte Klasse implementiert. Siehe die Abschnitte unter [Erstellen von Feldergruppen](./field-groups.md#create) und [Erstellen von Schemata](./schemas.md#create) in den entsprechenden Endpunkthandbüchern für weitere Informationen.
>
>Wenn Sie im Echtzeit-Kundenprofil planen, Schemas zu verwenden, die auf benutzerdefinierten Klassen basieren, sollten Sie auch beachten, dass Vereinigungsschemas nur auf Schemas erstellt werden, die dieselbe Klasse aufweisen. Wenn Sie ein benutzerdefiniertes Klassenschema in die Vereinigung für eine andere Klasse einfügen möchten, z. B. [!UICONTROL XDM Individual Profile] oder [!UICONTROL XDM ExperienceEvent]müssen Sie eine Beziehung zu einem anderen Schema herstellen, das diese Klasse verwendet. Siehe Tutorial zu [zur Herstellung einer Beziehung zwischen zwei Schemas in der API](../tutorials/relationship-api.md) für weitere Informationen.

**API-Format**

```http
POST /tenant/classes
```

**Anfrage**

Die Anfrage zum Erstellen einer Klasse (POST) muss ein `allOf`-Attribut enthalten, das eine `$ref` zu einem von zwei Werten enthält: `https://ns.adobe.com/xdm/data/record` oder `https://ns.adobe.com/xdm/data/time-series`. Diese Werte stellen das Verhalten dar, auf dem die Klasse basiert (Datensatz oder Zeitreihe). Weiterführende Informationen zu Unterschieden zwischen Datensatzdaten und Zeitreihendaten finden Sie im Abschnitt zu Verhaltenstypen in den [Grundlagen der Schemakomposition](../schema/composition.md).

Beim Definieren einer Klasse können Sie auch Feldergruppen oder benutzerdefinierte Felder in die Klassendefinition einbeziehen. Dies würde dazu führen, dass die hinzugefügten Feldergruppen und Felder in allen Schemas enthalten sind, die die Klasse implementieren. Folgende Beispielanfrage definiert eine Klasse namens „Eigenschaft“, die Daten zu verschiedenen Eigenschaften erfasst, die von einer Firma besessen und genutzt werden. Sie enthält ein `propertyId`-Feld, das bei jeder Verwendung der Klasse eingeschlossen wird.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `_{TENANT_ID}` | Der `TENANT_ID`-Namespace für Ihre Organisation. Alle von Ihrem Unternehmen erstellten Ressourcen müssen diese Eigenschaft enthalten, um Kollisionen mit anderen Ressourcen in der [!DNL Schema Registry]. |
| `allOf` | Eine Liste mit Ressourcen, deren Eigenschaften von der neuen Klasse geerbt werden sollen. Eines der `$ref`-Objekte im Array definiert das Verhalten der Klasse. In diesem Beispiel übernimmt die Klasse das Verhalten „record“. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und eine Payload mit den Details der neu erstellten Klasse zurück, einschließlich `$id`, `meta:altId` und `version`. Diese drei Werte sind schreibgeschützt und werden von der [!DNL Schema Registry].

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
  "imsOrg": "{ORG_ID}",
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

Durchführen einer GET-Anfrage an [alle Klassen auflisten](#list) im `tenant` -Container würde nun die Property-Klasse enthalten. Sie können auch [Anfrage zum Nachschlagen (GET) ausführen](#lookup) mit der URL-kodierten `$id` , um die neue Klasse direkt anzuzeigen.

## Klasse aktualisieren {#put}

Sie können eine ganze Klasse durch einen PUT-Vorgang ersetzen und die Ressource im Wesentlichen neu schreiben. Beim Aktualisieren einer Klasse über eine PUT-Anfrage muss der Text alle Felder enthalten, die erforderlich sind, wenn [Erstellen einer neuen Klasse](#create) in einer POST-Anfrage.

>[!NOTE]
>
>Wenn Sie nur einen Teil einer Klasse aktualisieren möchten, anstatt sie vollständig zu ersetzen, lesen Sie den Abschnitt unter [Aktualisieren eines Teils einer Klasse](#patch).

**API-Format**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Die `meta:altId` oder URL-kodiert `$id` der Klasse, die Sie neu schreiben möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage schreibt eine vorhandene Klasse neu und ändert deren `description` und `title` eines seiner Felder.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  "imsOrg": "{ORG_ID}",
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

## Aktualisieren eines Teils einer Klasse {#patch}

Sie können einen Teil einer Klasse mithilfe einer PATCH-Anfrage aktualisieren. Die [!DNL Schema Registry] unterstützt alle standardmäßigen JSON Patch-Vorgänge, einschließlich `add`, `remove`und `replace`. Weitere Informationen zum JSON Patch finden Sie im Abschnitt [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Wenn Sie eine gesamte Ressource durch neue Werte ersetzen möchten, anstatt einzelne Felder zu aktualisieren, lesen Sie den Abschnitt unter [Ersetzen einer Klasse mithilfe eines PUT-Vorgangs](#put).

**API-Format**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Die URL-kodierte `$id` URI oder `meta:altId` der Klasse, die Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Beispielanfrage aktualisiert die `description` einer vorhandenen Klasse und `title` eines seiner Felder.

Der Anfragetext hat die Form eines Arrays, wobei jedes aufgelistete Objekt eine bestimmte Änderung an einem einzelnen Feld darstellt. Jedes Objekt enthält den auszuführenden Vorgang (`op`), auf welchem Feld der Vorgang ausgeführt werden soll (`path`) und welche Informationen in diesem Vorgang enthalten sein sollten (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**Antwort**

Die Antwort zeigt, dass beide Vorgänge erfolgreich durchgeführt wurden. Die `description` wurde zusammen mit der `title` des `propertyId` -Feld.

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
  "imsOrg": "{ORG_ID}",
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

Gelegentlich kann es erforderlich sein, eine Klasse aus der Schema Registry zu entfernen. Dies geschieht durch Ausführen einer DELETE-Anfrage mit der im Pfad angegebenen Klassen-ID.

**API-Format**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Die URL-kodierte `$id` URI oder `meta:altId` der Klasse, die Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie einen [Anfrage zum Nachschlagen (GET)](#lookup) für die Klasse. Sie müssen eine `Accept` -Kopfzeile in der Anfrage, sollte jedoch einen HTTP-Status 404 (Nicht gefunden) erhalten, da die Klasse aus der Schema Registry entfernt wurde.
