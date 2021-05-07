---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Schema-Registrierung;Feldgruppe;Feldgruppen;Erstellen
solution: Experience Platform
title: API-Endpunkt für Feldgruppen
description: Mit dem Endpunkt /fieldgroups in der Schema Registry API können Sie XDM-Schema-Feldgruppen in Ihrer Experience-Anwendung programmgesteuert verwalten.
topic: Entwicklerhandbuch
translation-type: tm+mt
source-git-commit: b25c545e86c8ffd6b5832893152aef597feaf71f
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 9%

---


# Endpunkt der Feldgruppen im Schema

Schema-Feldgruppen sind wiederverwendbare Komponenten, die einen oder mehrere Felder definieren, die ein bestimmtes Konzept repräsentieren, z. B. eine Einzelperson, eine Postanschrift oder eine Webbrowser-Umgebung. Feldgruppen sind als Teil eines Schemas vorgesehen, das eine kompatible Klasse implementiert, je nach dem Verhalten der von ihnen dargestellten Daten (Datensatz oder Zeitreihen). Mit dem `/fieldgroups`-Endpunkt in der [!DNL Schema Registry]-API können Sie Feldgruppen in Ihrer Experience-Anwendung programmatisch verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer Experience Platformen-API benötigt werden.

## Abrufen einer Liste von Feldgruppen {#list}

Sie können alle Feldgruppen unter dem Container `global` oder `tenant` durch eine GET an `/global/fieldgroups` bzw. `/tenant/fieldgroups` Liste haben.

>[!NOTE]
>
>Bei der Auflistung von Ressourcen wird das Schema Registry-Ergebnis auf 300 Elemente begrenzt. Um Ressourcen über diese Grenze hinaus zurückzugeben, müssen Sie Paging-Parameter verwenden. Es wird außerdem empfohlen, zusätzliche Abfragen zu verwenden, um Ergebnisse zu filtern und die Anzahl der zurückgegebenen Ressourcen zu reduzieren. Weitere Informationen finden Sie im Dokument unter [Abfrage parameters](./appendix.md#query) im Anhang.

**API-Format**

```http
GET /{CONTAINER_ID}/fieldgroups?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, von dem Sie Feldgruppen abrufen möchten: `global` für von der Adobe erstellte Feldgruppen oder `tenant` für Feldgruppen, die sich im Besitz Ihres Unternehmens befinden. |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse. Eine Liste der verfügbaren Parameter finden Sie im Dokument [Anhang](./appendix.md#query). |

**Anfrage**

Mit der folgenden Anforderung wird eine Liste von Feldgruppen aus dem Container `tenant` abgerufen. Dabei werden die Feldgruppen mit dem Parameter `orderby` sortiert, indem die Abfrage nach dem Attribut `title` sortiert wird.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept`-Kopfzeile ab, die in der Anforderung gesendet wird. Die folgenden `Accept`-Kopfzeilen stehen zur Auflistung von Feldgruppen zur Verfügung:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung der einzelnen Ressourcen zurück. Dies ist die empfohlene Kopfzeile für die Auflistung der Ressourcen. (Maximal: 300) |
| `application/vnd.adobe.xed+json` | Gibt für jede Ressource die vollständige JSON-Feldgruppe zurück, wobei die ursprünglichen `$ref` und `allOf` enthalten sind. (Maximal: 300) |

**Antwort**

Bei der oben genannten Anforderung wurde die Überschrift `application/vnd.adobe.xed-id+json` `Accept` verwendet. Daher enthält die Antwort nur die Attribute `title`, `$id`, `meta:altId` und `version` für jede Feldgruppe. Mit der anderen `Accept`-Kopfzeile (`application/vnd.adobe.xed+json`) werden alle Attribute jeder Feldgruppe zurückgegeben. Wählen Sie die entsprechende `Accept`-Kopfzeile, je nach den Informationen, die Sie in Ihrer Antwort benötigen.

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

## Suchen Sie nach einer Feldgruppe {#lookup}

Sie können eine bestimmte Feldgruppe nachschlagen, indem Sie die ID der Feldgruppe in den Pfad einer GET-Anforderung aufnehmen.

**API-Format**

```http
GET /{CONTAINER_ID}/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, in dem die Feldgruppe enthalten ist, die Sie abrufen möchten: `global` für eine von der Adobe erstellte Feldgruppe oder `tenant` für eine Feldgruppe im Besitz Ihres Unternehmens. |
| `{FIELD_GROUP_ID}` | Die `meta:altId`- oder URL-kodierte `$id` der Feldgruppe, nach der Sie suchen möchten. |

**Anfrage**

Mit der folgenden Anforderung wird eine Feldgruppe anhand des im Pfad angegebenen Werts `meta:altId` abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.fieldgroups.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept`-Kopfzeile ab, die in der Anforderung gesendet wird. Für alle Nachschlageanforderungen muss eine `version` in die `Accept`-Kopfzeile eingefügt werden. Die folgenden `Accept`-Kopfzeilen stehen zur Verfügung:

| `Accept`-Kopfzeile | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Roh mit `$ref` und `allOf`, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Roh mit `$ref` und `allOf`, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, einschließlich Deskriptoren. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Feldgruppe zurück. Die zurückgegebenen Felder hängen von der `Accept`-Kopfzeile ab, die in der Anforderung gesendet wird. Experimentieren Sie mit verschiedenen `Accept`-Kopfzeilen, um die Antworten zu vergleichen und festzustellen, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

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

## Feldgruppe {#create} erstellen

Sie können eine benutzerspezifische Feldgruppe unter dem Container `tenant` definieren, indem Sie eine POST anfordern.

**API-Format**

```http
POST /tenant/fieldgroups
```

**Anfrage**

Beim Definieren einer neuen Feldgruppe muss ein `meta:intendedToExtend`-Attribut vorhanden sein, das die `$id` der Klassen auflistet, mit denen die Feldgruppe kompatibel ist. In diesem Beispiel ist die Feldgruppe mit einer `Property`-Klasse kompatibel, die zuvor definiert wurde. Benutzerdefinierte Felder müssen unter `_{TENANT_ID}` verschachtelt sein (wie im Beispiel gezeigt), um Kollisionen mit ähnlichen Feldern zu vermeiden, die von Klassen und anderen Feldgruppen bereitgestellt werden.

>[!NOTE]
>
>Weitere Informationen zum Definieren verschiedener Feldtypen, die in Ihre Feldgruppe aufgenommen werden sollen, finden Sie im Handbuch [Feldbeschränkungen](../schema/field-constraints.md#define-fields).

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

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und eine Nutzlast mit den Details der neu erstellten Feldgruppe zurück, einschließlich der `$id`, `meta:altId` und `version`. Diese Werte sind schreibgeschützt und werden durch das [!DNL Schema Registry] zugewiesen.

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

Wenn Sie eine GET für [Liste aller Feldgruppen](#list) im Pächter-Container durchführen, wird jetzt die Feldgruppe Eigenschaftendetails einbezogen. Alternativ können Sie eine Suchanfrage (GET) [ mit dem URL-kodierten `$id`-URI ausführen, um die neue Feldgruppe direkt Ansicht.](#lookup)

## Feldgruppe {#put} aktualisieren

Sie können eine gesamte Feldgruppe durch einen PUT-Vorgang ersetzen und die Ressource im Grunde neu schreiben. Beim Aktualisieren einer Feldgruppe über eine PUT-Anforderung muss der Textkörper alle erforderlichen Felder enthalten, wenn [eine neue Feldgruppe](#create) in einer POST erstellt wird.

>[!NOTE]
>
>Wenn Sie nur einen Teil einer Feldgruppe aktualisieren möchten, anstatt sie vollständig zu ersetzen, lesen Sie den Abschnitt unter [Aktualisieren eines Teils einer Feldgruppe](#patch).

**API-Format**

```http
PUT /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{FIELD_GROUP_ID}` | Die `meta:altId`- oder URL-kodierte `$id` der Feldgruppe, die Sie neu schreiben möchten. |

**Anfrage**

Mit der folgenden Anforderung wird eine bestehende Feldgruppe neu geschrieben und ein neues `propertyCountry`-Feld hinzugefügt.

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

Eine erfolgreiche Antwort gibt die Details der aktualisierten Feldgruppe zurück.

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

## Einen Teil einer Feldgruppe {#patch} aktualisieren

Sie können einen Teil einer Feldgruppe mit einer PATCH-Anforderung aktualisieren. [!DNL Schema Registry] unterstützt alle standardmäßigen JSON-Patch-Vorgänge, einschließlich `add`, `remove` und `replace`. Weitere Informationen zum JSON-Patch finden Sie im Handbuch [API-Grundlagen](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Wenn Sie eine gesamte Ressource durch neue Werte ersetzen möchten, anstatt einzelne Felder zu aktualisieren, lesen Sie den Abschnitt unter [Ersetzen einer Feldgruppe mit einem PUT-Vorgang](#put).

**API-Format**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{FIELD_GROUP_ID}` | Die URL-kodierte `$id`-URI oder `meta:altId` der Feldgruppe, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Beispielanforderung aktualisiert das `description` einer vorhandenen Feldgruppe und fügt ein neues `propertyCity`-Feld hinzu.

Der Anforderungstext besteht aus einem Array, wobei jedes aufgelistete Objekt eine bestimmte Änderung an einem einzelnen Feld darstellt. Jedes Objekt enthält den auszuführenden Vorgang (`op`), für welches Feld der Vorgang ausgeführt werden soll (`path`) und welche Informationen in diesen Vorgang einbezogen werden sollen (`value`).

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

## Eine Feldgruppe {#delete} löschen

Es kann vorkommen, dass eine Feldgruppe aus der Schema-Registrierung entfernt werden muss. Dies geschieht durch eine DELETE-Anforderung mit der Feldgruppen-ID, die im Pfad angegeben ist.

**API-Format**

```http
DELETE /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{FIELD_GROUP_ID}` | Die URL-kodierte `$id`-URI oder `meta:altId` der Feldgruppe, die Sie löschen möchten. |

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

Sie können den Löschvorgang bestätigen, indem Sie eine [Nachschlageanforderung (GET)](#lookup) für die Feldgruppe versuchen. Sie müssen einen `Accept`-Header in die Anforderung einbeziehen, sollten jedoch einen HTTP-Status 404 (Nicht gefunden) erhalten, da die Feldgruppe aus der Schema-Registrierung entfernt wurde.