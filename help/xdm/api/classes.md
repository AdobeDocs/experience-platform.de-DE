---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Klassenregistrierung;Schemaregistrierung;Klasse;Klasse;Klassen;Klassen;erstellen
solution: Experience Platform
title: Klassen-API-Endpunkt
description: Mit dem /classes-Endpunkt in der Schema Registry-API können Sie XDM-Klassen in Ihrer Erlebnisanwendung programmgesteuert verwalten.
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 22%

---

# Classes-Endpunkt

Alle Experience-Datenmodell (XDM)-Schemata müssen auf einer -Klasse basieren. Eine Klasse bestimmt die Basisstruktur von allgemeinen Eigenschaften, die alle Schemata enthalten müssen, die auf dieser Klasse basieren, sowie die Schemafeldgruppen, die für die Verwendung in diesen Schemata geeignet sind. Darüber hinaus bestimmt die Klasse eines Schemas die Verhaltensaspekte der Daten, die ein Schema enthalten soll. Es gibt zwei Arten von Daten:

* **[!UICONTROL Datensatz]**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt kann ein Unternehmen oder eine Person sein.
* **[!UICONTROL Zeitreihe]**: Stellt eine Momentaufnahme des Systems zum Zeitpunkt bereit, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

>[!NOTE]
>
>Weitere Informationen zu Klassen in Bezug auf Datenverhalten und deren Auswirkungen auf die Schemakomposition finden Sie unter [Grundlagen der Schemakomposition](../schema/composition.md).

Mit dem `/classes`-Endpunkt in der [!DNL Schema Registry]-API können Sie Klassen in Ihrem Erlebnisprogramm programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste von Klassen {#list}

Sie können alle Klassen unter dem `global`- oder `tenant`-Container durch eine GET-Anfrage an `/global/classes` bzw. `/tenant/classes` auflisten.

>[!NOTE]
>
>Beim Auflisten von Ressourcen beschränkt die Schemaregistrierung Ergebnismengen auf 300 Elemente. Um Ressourcen über dieses Limit hinaus zurückzugeben, müssen Sie Paging-Parameter verwenden. Es wird außerdem empfohlen, zusätzliche Abfrageparameter zu verwenden, um Ergebnisse zu filtern und die Anzahl der zurückgegebenen Ressourcen zu reduzieren. Weitere Informationen finden Sie [&#x200B; Abschnitt &#x200B;](./appendix.md#query)Abfrageparameter“ im Anhang.

**API-Format**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, aus dem Sie Klassen abrufen möchten: `global` für von Adobe erstellte Klassen oder `tenant` für Klassen, die Ihrem Unternehmen gehören. |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse nach . Eine Liste der verfügbaren Parameter finden [&#x200B; im &#x200B;](./appendix.md#query)-Dokument . |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft eine Liste von Klassen aus dem `tenant`-Container ab und verwendet einen `orderby` Abfrageparameter, um die Klassen nach ihrem `title` Attribut zu sortieren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Format der Antwort hängt von der in der Anfrage gesendeten `Accept`-Kopfzeile ab. Die folgenden `Accept`-Kopfzeilen sind für die Auflistung von Klassen verfügbar:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung jeder Ressource zurück. Dies ist die empfohlene Kopfzeile zum Auflisten von Ressourcen. (Limit: 300) |
| `application/vnd.adobe.xed+json` | Gibt für jede Ressource eine vollständige JSON-Klasse mit `$ref` und `allOf` zurück. (Limit: 300) |

{style="table-layout:auto"}

**Antwort**

Die obige Anfrage verwendete den `application/vnd.adobe.xed-id+json` `Accept`-Header. Daher enthält die Antwort für jede Klasse nur die Attribute `title`, `$id`, `meta:altId` und `version`. Bei Verwendung der anderen `Accept`-Kopfzeile (`application/vnd.adobe.xed+json`) werden alle Attribute jeder Klasse zurückgegeben. Wählen Sie den entsprechenden `Accept`-Header entsprechend den Informationen aus, die Sie in Ihrer Antwort benötigen.

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

## Suchen einer Klasse {#lookup}

Sie können eine bestimmte Klasse nachschlagen, indem Sie die ID der Klasse in den Pfad einer GET-Anfrage aufnehmen.

**API-Format**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, der die Klasse enthält, die Sie abrufen möchten: `global` für eine von Adobe erstellte Klasse oder `tenant` für eine Klasse, die Ihrem Unternehmen gehört. |
| `{CLASS_ID}` | Die `meta:altId` oder URL-kodierte `$id` der Klasse, die Sie suchen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft eine -Klasse anhand ihres im Pfad angegebenen `meta:altId` ab.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

Eine erfolgreiche Antwort gibt die Details der Klasse zurück. Die zurückgegebenen Felder hängen von der `Accept` ab, die in der Anfrage gesendet wird. Experimentieren Sie mit verschiedenen `Accept`-Kopfzeilen, um die Antworten zu vergleichen und festzustellen, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

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

Sie können eine benutzerdefinierte Klasse unter dem `tenant`-Container definieren, indem Sie eine POST-Anfrage stellen.

>[!IMPORTANT]
>
>Beim Erstellen eines Schemas basierend auf einer benutzerdefinierten Klasse, die Sie definieren, können Sie keine Standardfeldgruppen verwenden. Jede Feldergruppe definiert die Klassen, mit denen sie kompatibel sind, in ihrem `meta:intendedToExtend`. Sobald Sie mit der Definition von Feldergruppen beginnen, die mit Ihrer neuen Klasse kompatibel sind (durch Verwendung der `$id` Ihrer neuen Klasse im `meta:intendedToExtend` Feld der Feldergruppe), können Sie diese Feldergruppen jedes Mal wiederverwenden, wenn Sie ein Schema definieren, das die von Ihnen definierte Klasse implementiert. Weitere Informationen finden Sie in den Abschnitten [Erstellen &#x200B;](./field-groups.md#create) Feldergruppen[&#x200B; und &#x200B;](./schemas.md#create)Erstellen von Schemas in den jeweiligen Endpunkthandbüchern.
>
>Wenn Sie planen, Schemas zu verwenden, die auf benutzerdefinierten Klassen im Echtzeit-Kundenprofil basieren, sollten Sie auch beachten, dass Vereinigungsschemas nur auf der Grundlage von Schemas erstellt werden, die dieselbe Klasse aufweisen. Wenn Sie ein benutzerdefiniertes Klassenschema für eine andere Klasse wie [!UICONTROL XDM Individual Profile] oder [!UICONTROL XDM ExperienceEvent] in die Vereinigung einbeziehen möchten, müssen Sie eine Beziehung zu einem anderen Schema herstellen, das diese Klasse verwendet. Weitere Informationen finden Sie im Tutorial [Erstellen einer Beziehung zwischen zwei Schemas in &#x200B;](../tutorials/relationship-api.md) API“.

**API-Format**

```http
POST /tenant/classes
```

**Anfrage**

Die Anfrage zum Erstellen einer Klasse (POST) muss ein `allOf`-Attribut enthalten, das eine `$ref` zu einem von zwei Werten enthält: `https://ns.adobe.com/xdm/data/record` oder `https://ns.adobe.com/xdm/data/time-series`. Diese Werte stellen das Verhalten dar, auf dem die Klasse basiert (Datensatz oder Zeitreihe). Weiterführende Informationen zu Unterschieden zwischen Datensatzdaten und Zeitreihendaten finden Sie im Abschnitt zu Verhaltenstypen in den [Grundlagen der Schemakomposition](../schema/composition.md).

Wenn Sie eine Klasse definieren, können Sie auch Feldergruppen oder benutzerdefinierte Felder in die Klassendefinition aufnehmen. Dies würde dazu führen, dass die hinzugefügten Feldergruppen und Felder in allen Schemata enthalten sind, die die -Klasse implementieren. Folgende Beispielanfrage definiert eine Klasse namens „Eigenschaft“, die Daten zu verschiedenen Eigenschaften erfasst, die von einer Firma besessen und genutzt werden. Sie enthält ein `propertyId`-Feld, das bei jeder Verwendung der Klasse eingeschlossen wird.

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
| `_{TENANT_ID}` | Der `TENANT_ID`-Namespace für Ihre Organisation. Alle von Ihrer Organisation erstellten Ressourcen müssen diese Eigenschaft enthalten, um Kollisionen mit anderen Ressourcen in der [!DNL Schema Registry] zu vermeiden. |
| `allOf` | Eine Liste mit Ressourcen, deren Eigenschaften von der neuen Klasse geerbt werden sollen. Eines der `$ref`-Objekte im Array definiert das Verhalten der Klasse. In diesem Beispiel übernimmt die Klasse das Verhalten „record“. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und eine Payload mit den Details der neu erstellten Klasse zurück, einschließlich `$id`, `meta:altId` und `version`. Diese drei Werte sind schreibgeschützt und werden vom [!DNL Schema Registry] zugewiesen.

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

Wenn Sie eine GET-Anfrage ausführen[&#x200B; um alle Klassen &#x200B;](#list) dem `tenant`-Container aufzulisten, würde diese jetzt die Property-Klasse enthalten. Sie können auch [eine Suchanfrage (GET) ausführen](#lookup) indem Sie die URL-codierte `$id` verwenden, um die neue Klasse direkt anzuzeigen.

## Aktualisieren einer Klasse {#put}

Sie können eine ganze Klasse durch einen PUT-Vorgang ersetzen, wobei die Ressource im Wesentlichen neu geschrieben wird. Beim Aktualisieren einer Klasse über eine PUT POST-Anfrage muss der Hauptteil alle Felder enthalten, die beim [Erstellen einer neuen Klasse](#create) in einer Klassenanfrage erforderlich sind.

>[!NOTE]
>
>Wenn Sie nur einen Teil einer Klasse aktualisieren möchten, anstatt sie vollständig zu ersetzen, finden Sie weitere Informationen im Abschnitt [Aktualisieren eines Teils einer Klasse](#patch).

**API-Format**

```http
PUT /tenant/classes/{CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Die `meta:altId` oder URL-codierte `$id` der Klasse, die Sie umschreiben möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage schreibt eine vorhandene Klasse neu und ändert ihre `description` und die `title` eines ihrer Felder.

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

Sie können einen Teil einer Klasse mithilfe einer PATCH-Anfrage aktualisieren. Der [!DNL Schema Registry] unterstützt alle standardmäßigen JSON-Patch-Vorgänge, einschließlich `add`, `remove` und `replace`. Weitere Informationen zu JSON-Patch-Vorgängen finden Sie im [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Wenn Sie eine gesamte Ressource durch neue Werte ersetzen möchten, anstatt einzelne Felder zu aktualisieren, lesen Sie den Abschnitt über [Ersetzen einer Klasse mithilfe eines PUT-Vorgangs](#put).

**API-Format**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Der URL-codierte `$id`-URI oder `meta:altId` der Klasse, die Sie aktualisieren möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Beispielanfrage aktualisiert die `description` einer vorhandenen Klasse und die `title` eines ihrer Felder.

Der Anfragetext hat die Form eines Arrays, wobei jedes aufgelistete Objekt eine bestimmte Änderung an einem einzelnen Feld darstellt. Jedes Objekt enthält den auszuführenden Vorgang (`op`), in welchem Feld der Vorgang ausgeführt werden soll (`path`) und welche Informationen in diesem Vorgang enthalten sein sollen (`value`).

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

Die Antwort zeigt, dass beide Vorgänge erfolgreich durchgeführt wurden. Die `description` wurde aktualisiert, ebenso wie die `title` des `propertyId`.

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

## Löschen einer Klasse {#delete}

Gelegentlich kann es erforderlich sein, eine Klasse aus der Schemaregistrierung zu entfernen. Dies geschieht, indem eine DELETE-Anfrage mit der im Pfad angegebenen Klassen-ID durchgeführt wird.

**API-Format**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Die URL-codierte `$id`-URI oder `meta:altId` der Klasse, die Sie löschen möchten. |

{style="table-layout:auto"}

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

Sie können den Löschvorgang bestätigen, indem Sie eine [Suchanfrage (GET))](#lookup) für die Klasse ausführen. Sie müssen einen `Accept`-Header in die Anfrage einbeziehen, sollten jedoch einen HTTP-Status 404 (Nicht gefunden) erhalten, da die Klasse aus der Schemaregistrierung entfernt wurde.
