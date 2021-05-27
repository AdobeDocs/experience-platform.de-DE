---
keywords: Experience Platform;Startseite;beliebte Themen;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schema Registry;Feldergruppe;Feldergruppe;Feldergruppen erstellen
solution: Experience Platform
title: Feldergruppen-API-Endpunkt
description: Mit dem Endpunkt /fieldgroups in der Schema Registry-API können Sie XDM-Schemafeldgruppen in Ihrer Erlebnisanwendung programmgesteuert verwalten.
topic: Entwicklerhandbuch
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 11%

---


# Endpunkt für Schemafeldgruppen

Schemafeldgruppen sind wiederverwendbare Komponenten, die ein oder mehrere Felder definieren, die ein bestimmtes Konzept repräsentieren, z. B. eine Einzelperson, eine Postanschrift oder eine Webbrowser-Umgebung. Feldergruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert, je nach dem Verhalten der Daten, die sie darstellen (Datensatz oder Zeitreihen). Mit dem Endpunkt `/fieldgroups` in der API [!DNL Schema Registry] können Sie Feldergruppen in Ihrer Erlebnisanwendung programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Schema Registry] ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um Links zur zugehörigen Dokumentation zu erhalten, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

## Liste von Feldergruppen abrufen {#list}

Sie können alle Feldergruppen unter dem Container `global` oder `tenant` auflisten, indem Sie eine GET an `/global/fieldgroups` bzw. `/tenant/fieldgroups` anfordern.

>[!NOTE]
>
>Bei der Auflistung von Ressourcen beschränkt die Schema Registry Ergebnissätze auf 300 Elemente. Um Ressourcen zurückzugeben, die über diese Grenze hinausgehen, müssen Sie Paging-Parameter verwenden. Es wird außerdem empfohlen, zusätzliche Abfrageparameter zu verwenden, um Ergebnisse zu filtern und die Anzahl der zurückgegebenen Ressourcen zu reduzieren. Weitere Informationen finden Sie im Abschnitt zu [Abfrageparametern](./appendix.md#query) im Anhang.

**API-Format**

```http
GET /{CONTAINER_ID}/fieldgroups?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, aus dem Sie Feldergruppen abrufen möchten: `global` für von Adoben erstellte Feldergruppen oder `tenant` für Feldergruppen, die Ihrem Unternehmen gehören. |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse. Eine Liste der verfügbaren Parameter finden Sie im Dokument [Anhang](./appendix.md#query) . |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Mit der folgenden Anfrage wird eine Liste von Feldergruppen aus dem `tenant`-Container abgerufen, wobei mithilfe eines `orderby`-Abfrageparameters die Feldergruppen nach ihrem `title`-Attribut sortiert werden.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept`-Kopfzeile ab, die in der Anfrage gesendet wird. Die folgenden `Accept`-Kopfzeilen stehen zur Auflistung von Feldergruppen zur Verfügung:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung jeder Ressource zurück. Dies ist die empfohlene Kopfzeile für die Auflistung von Ressourcen. (Limit: 300) |
| `application/vnd.adobe.xed+json` | Gibt die vollständige JSON-Feldergruppe für jede Ressource zurück, wobei die ursprünglichen Werte `$ref` und `allOf` enthalten sind. (Limit: 300) |

{style=&quot;table-layout:auto&quot;}

**Antwort**

In der obigen Anfrage wurde die Kopfzeile `application/vnd.adobe.xed-id+json` `Accept` verwendet. Daher enthält die Antwort nur die Attribute `title`, `$id`, `meta:altId` und `version` für jede Feldergruppe. Mit der anderen `Accept`-Kopfzeile (`application/vnd.adobe.xed+json`) werden alle Attribute jeder Feldergruppe zurückgegeben. Wählen Sie je nach den Informationen, die Sie in Ihrer Antwort benötigen, die entsprechende `Accept`-Kopfzeile aus.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/6ece98e9842907c78c651f5b249d9f09",
      "meta:altId": "_{TENANT_ID}.fieldgroups.6ece98e9842907c78c651f5b249d9f09",
      "version": "1.0",
      "title": "CRM Data"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/6386ee478a30914964c6e676ad55603c",
      "meta:altId": "_{TENANT_ID}.fieldgroups.6386ee478a30914964c6e676ad55603c",
      "version": "1.9",
      "title": "Loyalty Member Details"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/67626b2830db3d3ea6c8f9d007aa5797",
      "meta:altId": "_{TENANT_ID}.fieldgroups.67626b2830db3d3ea6c8f9d007aa5797",
      "version": "1.0",
      "title": "Restaurant"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/2583b25b613fec704da6ef70cf527688",
      "meta:altId": "_{TENANT_ID}.fieldgroups.2583b25b613fec704da6ef70cf527688",
      "version": "1.1",
      "title": "Retail Customer Preferences"
    },
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/fieldgroups"
    }
  }
}
```

## Feldergruppe nachschlagen {#lookup}

Sie können nach einer bestimmten Feldergruppe suchen, indem Sie die Kennung der Feldergruppe in den Pfad einer GET-Anfrage einschließen.

**API-Format**

```http
GET /{CONTAINER_ID}/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, der die Feldergruppe enthält, die Sie abrufen möchten: `global` für eine von Adoben erstellte Feldergruppe oder `tenant` für eine Feldergruppe, die sich im Besitz Ihrer Organisation befindet. |
| `{FIELD_GROUP_ID}` | Die `meta:altId` oder URL-kodierte `$id` der Feldergruppe, die Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Mit der folgenden Anfrage wird eine Feldergruppe anhand des im Pfad angegebenen Wertes `meta:altId` abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept`-Kopfzeile ab, die in der Anfrage gesendet wird. Für alle Nachschlageanfragen muss `version` in der `Accept`-Kopfzeile enthalten sein. Die folgenden `Accept`-Header sind verfügbar:

| `Accept`-Kopfzeile | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Roh mit `$ref` und `allOf`, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Roh mit `$ref` und `allOf`, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, einschließlich Deskriptoren. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Feldergruppe zurück. Die zurückgegebenen Felder hängen von der `Accept`-Kopfzeile ab, die in der Anfrage gesendet wird. Experimentieren Sie mit verschiedenen `Accept`-Kopfzeilen, um die Antworten zu vergleichen und zu bestimmen, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
  "version": "1.2",
  "title": "Favorite Hotel",
  "type": "object",
  "description": "",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "favoriteHotel": {
              "title": "Favorite Hotel",
              "description": "Reference field for hotel schema.",
              "type": "string",
              "isRequired": false,
              "meta:xdmType": "string"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "meta:xdmType": "object"
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

## Feldergruppe erstellen {#create}

Sie können eine benutzerdefinierte Feldergruppe unter dem Container `tenant` definieren, indem Sie eine POST anfordern.

**API-Format**

```http
POST /tenant/fieldgroups
```

**Anfrage**

Bei der Definition einer neuen Feldergruppe muss sie ein `meta:intendedToExtend` -Attribut enthalten, in dem die `$id` der Klassen aufgelistet wird, mit denen die Feldergruppe kompatibel ist. In diesem Beispiel ist die Feldergruppe mit einer `Property`-Klasse kompatibel, die zuvor definiert wurde. Benutzerdefinierte Felder müssen unter `_{TENANT_ID}` verschachtelt sein (wie im Beispiel gezeigt), um Kollisionen mit ähnlichen Feldern zu vermeiden, die von Klassen und anderen Feldergruppen bereitgestellt werden.

>[!NOTE]
>
>Weitere Informationen zum Definieren verschiedener Feldtypen, die in Ihre Feldergruppe aufgenommen werden sollen, finden Sie im [Handbuch zu Feldbeschränkungen](../schema/field-constraints.md#define-fields).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
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

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und eine Payload mit den Details der neu erstellten Feldergruppe zurück, einschließlich `$id`, `meta:altId` und `version`. Diese Werte sind schreibgeschützt und werden durch [!DNL Schema Registry] zugewiesen.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
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

Wenn Sie eine GET-Anfrage an [Auflisten aller Feldergruppen](#list) im Mandanten-Container ausführen, wäre jetzt die Feldergruppe Eigenschaftendetails enthalten. Alternativ können Sie [eine Nachschlageanfrage (GET)](#lookup) mit dem URL-kodierten `$id` -URI ausführen, um die neue Feldergruppe direkt anzuzeigen.

## Aktualisieren von Feldergruppen {#put}

Sie können eine ganze Feldergruppe durch einen PUT-Vorgang ersetzen und die Ressource im Wesentlichen neu schreiben. Beim Aktualisieren einer Feldergruppe über eine PUT-Anfrage muss der Hauptteil alle Felder einschließen, die beim Erstellen einer neuen Feldergruppe](#create) in einer POST-Anfrage erforderlich sind.[

>[!NOTE]
>
>Wenn Sie nur einen Teil einer Feldergruppe aktualisieren möchten, anstatt sie vollständig zu ersetzen, lesen Sie den Abschnitt unter [Aktualisieren eines Teils einer Feldergruppe](#patch).

**API-Format**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{FIELD_GROUP_ID}` | Die `meta:altId` oder URL-kodierte `$id` der Feldergruppe, die Sie neu schreiben möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage schreibt eine vorhandene Feldergruppe neu und fügt ein neues `propertyCountry` -Feld hinzu.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property Details",
        "description": "Detailed information related to the properties owned and operated by the company.",
        "type": "object",
        "meta:intendedToExtend": ["https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"],
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
                "$ref": "#/definitions/property"
            }
        ]
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der aktualisierten Feldergruppe zurück.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Detailed information related to the properties owned and operated by the company.",
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

## Aktualisieren eines Teils einer Feldergruppe {#patch}

Sie können einen Teil einer Feldergruppe mithilfe einer PATCH-Anfrage aktualisieren. [!DNL Schema Registry] unterstützt alle standardmäßigen JSON Patch-Vorgänge, einschließlich `add`, `remove` und `replace`. Weitere Informationen zu JSON Patch finden Sie im [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Wenn Sie eine gesamte Ressource durch neue Werte ersetzen möchten, anstatt einzelne Felder zu aktualisieren, lesen Sie den Abschnitt unter [Ersetzen einer Feldergruppe durch einen PUT-Vorgang](#put).

**API-Format**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{FIELD_GROUP_ID}` | Die URL-kodierte `$id` -URI oder `meta:altId` der Feldergruppe, die Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Beispielanfrage aktualisiert die `description` einer vorhandenen Feldergruppe und fügt ein neues `propertyCity` -Feld hinzu.

Der Anfragetext hat die Form eines Arrays, wobei jedes aufgelistete Objekt eine bestimmte Änderung an einem einzelnen Feld darstellt. Jedes Objekt enthält den auszuführenden Vorgang (`op`), das Feld, für das der Vorgang ausgeführt werden soll (`path`), und welche Informationen in diesem Vorgang enthalten sein sollen (`value`).

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/description",
          "value": "Details relating to a property operated by the company."
        },
        { 
          "op": "add",
          "path": "/definitions/property/properties/_{TENANT_ID}/properties/propertyCity",
          "value": {
            "title": "Property City",
            "description": "City where the property is located.",
            "type": "string"
          }
        }
      ]'
```

**Antwort**

Die Antwort zeigt, dass beide Vorgänge erfolgreich durchgeführt wurden. Das `description` wurde aktualisiert und `propertyCountry` wurde unter `definitions` hinzugefügt.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "fieldgroups",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a property operated by the company.",
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

## Eine Feldergruppe löschen {#delete}

Gelegentlich kann es erforderlich sein, eine Feldergruppe aus der Schema Registry zu entfernen. Dies geschieht durch Ausführen einer DELETE-Anfrage mit der im Pfad angegebenen Feldergruppen-ID.

**API-Format**

```http
DELETE /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{FIELD_GROUP_ID}` | Der URL-kodierte `$id` -URI oder `meta:altId` der Feldergruppe, die Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine [Nachschlageanfrage (GET)](#lookup) für die Feldergruppe ausführen. Sie müssen einen `Accept`-Header in die Anfrage einbeziehen, sollten jedoch einen HTTP-Status 404 (Nicht gefunden) erhalten, da die Feldergruppe aus der Schema Registry entfernt wurde.