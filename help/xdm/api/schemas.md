---
keywords: Experience Platform;Startseite;beliebte Themen;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schemaregistrierung;Schemaregistrierung;Schema;Schema;Schemata;Erstellen
solution: Experience Platform
title: API-Endpunkt für Schemas
description: Mit dem Endpunkt /schemas in der Schema Registry-API können Sie XDM-Schemas in Ihrer Erlebnisanwendung programmgesteuert verwalten.
topic-legacy: developer guide
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 18%

---

# Endpunkt für Schemas

Ein Schema kann als Entwurf für die Daten betrachtet werden, die Sie in Adobe Experience Platform erfassen möchten. Jedes Schema besteht aus einer Klasse und keiner oder mehr Schemafeldgruppen. Mit dem Endpunkt `/schemas` in der API [!DNL Schema Registry] können Sie Schemas in Ihrer Erlebnisanwendung programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um Links zur zugehörigen Dokumentation zu erhalten, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

## Liste von Schemata abrufen {#list}

Sie können alle Schemas unter dem Container `global` oder `tenant` auflisten, indem Sie eine GET an `/global/schemas` bzw. `/tenant/schemas` anfordern.

>[!NOTE]
>
>When listing resources, the Schema Registry limits result sets to 300 items. In order to return resources beyond this limit, you must use paging parameters. It is also recommended that you use additional query parameters to filter results and reduce the number of resources returned. See the section on [query parameters](./appendix.md#query) in the appendix document for more information.

**API-Format**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, der die Schemas enthält, die Sie abrufen möchten: `global` für von Adoben erstellte Schemata oder `tenant` für Schemas, die Ihrem Unternehmen gehören. |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse. Eine Liste der verfügbaren Parameter finden Sie im Dokument [Anhang](./appendix.md#query) . |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Mit der folgenden Anfrage wird eine Liste von Schemas aus dem `tenant`-Container abgerufen, wobei mithilfe eines `orderby`-Abfrageparameters die Ergebnisse nach ihrem `title`-Attribut sortiert werden.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept`-Kopfzeile ab, die in der Anfrage gesendet wird. Die folgenden `Accept`-Kopfzeilen stehen zur Auflistung von Schemas zur Verfügung:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung jeder Ressource zurück. Dies ist die empfohlene Kopfzeile für die Auflistung von Ressourcen. (Limit: 300) |
| `application/vnd.adobe.xed+json` | Gibt das vollständige JSON-Schema für jede Ressource zurück, wobei das ursprüngliche `$ref` und `allOf` enthalten sind. (Limit: 300) |

{style=&quot;table-layout:auto&quot;}

**Antwort**

In der obigen Anfrage wurde die Kopfzeile `application/vnd.adobe.xed-id+json` `Accept` verwendet. Daher enthält die Antwort nur die Attribute `title`, `$id`, `meta:altId` und `version` für jedes Schema. Using the other `Accept` header (`application/vnd.adobe.xed+json`) returns all attributes of each schema. Wählen Sie je nach den Informationen, die Sie in Ihrer Antwort benötigen, die entsprechende `Accept`-Kopfzeile aus.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
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
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## Nachschlagen eines Schemas {#lookup}

You can look up a specific schema by making a GET request that includes the schema&#39;s ID in the path.

**API-Format**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | The container that houses the schema you want to retrieve: `global` for an Adobe-created schema or `tenant` for a schema owned by your organization. |
| `{SCHEMA_ID}` | The `meta:altId` or URL-encoded `$id` of the schema you want to look up. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Mit der folgenden Anfrage wird ein Schema abgerufen, das durch seinen `meta:altId` -Wert im Pfad angegeben wird.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept`-Kopfzeile ab, die in der Anfrage gesendet wird. Für alle Nachschlageanfragen muss `version` in der `Accept`-Kopfzeile enthalten sein. Die folgenden `Accept`-Header sind verfügbar:

| `Accept`-Kopfzeile | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Roh mit `$ref` und `allOf`, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` und `allOf` aufgelöst, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Roh mit `$ref` und `allOf`, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` und `allOf` aufgelöst, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` und `allOf` aufgelöst, einschließlich Deskriptoren. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Schemas zurück. The fields that are returned depend on the `Accept` header sent in the request. Experimentieren Sie mit verschiedenen `Accept`-Kopfzeilen, um die Antworten zu vergleichen und zu bestimmen, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Erstellen eines Schemas {#create}

Der Prozess der Schemakomposition beginnt mit der Zuweisung einer Klasse. Die Klasse definiert wichtige verhaltensbezogene Aspekte der Daten (Datensatz oder Zeitreihen) sowie die Mindestfelder, die erforderlich sind, um die zu erfassenden Daten zu beschreiben.

>[!NOTE]
>
>The example call below is only a baseline example of how to create a schema in the API, with the minimal composition requirements of a class and no field groups. Vollständige Schritte zum Erstellen eines Schemas in der API, einschließlich der Zuweisung von Feldern mithilfe von Feldergruppen und Datentypen, finden Sie im Tutorial zur Schemaerstellung](../tutorials/create-schema-api.md).[

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die Anfrage muss ein `allOf`-Attribut enthalten, das auf die `$id` einer Klasse verweist. Dieses Attribut definiert die „Basisklasse“, die das Schema implementiert. In diesem Beispiel ist die Basisklasse eine Klasse vom Typ „Eigenschaftsinformationen“, die zuvor erstellt wurde.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `allOf` | Ein Array von Objekten, wobei jedes Objekt auf eine Klasse oder Feldergruppe verweist, deren Felder vom Schema implementiert werden. Jedes Objekt enthält eine einzelne Eigenschaft (`$ref`), deren Wert die `$id` der Klasse oder Feldergruppe darstellt, die das neue Schema implementieren soll. Es muss eine Klasse mit null oder mehr zusätzlichen Feldergruppen bereitgestellt werden. Im obigen Beispiel ist das einzelne Objekt im Array `allOf` die Klasse des Schemas. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und eine Payload mit den Details zum neu erstellten Schema zurück, einschließlich `$id`, `meta:altId` und `version`. These values are read-only and are assigned by the [!DNL Schema Registry].

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Wenn Sie eine GET-Anfrage an [list all schemas](#list) im Mandanten-Container ausführen, würde jetzt das neue Schema enthalten. You can perform a [lookup (GET) request](#lookup) using the URL-encoded `$id` URI to view the new schema directly.

Um einem Schema zusätzliche Felder hinzuzufügen, können Sie einen [PATCH-Vorgang](#patch) ausführen, um den `allOf` - und `meta:extends` -Arrays des Schemas Feldergruppen hinzuzufügen.

## Update a schema {#put}

Sie können ein ganzes Schema durch einen PUT-Vorgang ersetzen und die Ressource im Wesentlichen neu schreiben. Beim Aktualisieren eines Schemas über eine PUT-Anfrage muss der Hauptteil alle Felder einschließen, die beim Erstellen eines neuen Schemas](#create) in einer POST-Anfrage erforderlich sind.[

>[!NOTE]
>
>Wenn Sie nur einen Teil eines Schemas aktualisieren möchten, anstatt es vollständig zu ersetzen, lesen Sie den Abschnitt unter [Aktualisieren eines Teils eines Schemas](#patch).

**API-Format**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der `meta:altId` oder URL-kodierte `$id` des Schemas, das Sie neu schreiben möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage ersetzt ein vorhandenes Schema und ändert dessen Attribute `title`, `description` und `allOf`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Schemas zurück.

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088470592,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Einen Teil eines Schemas aktualisieren {#patch}

Sie können einen Teil eines Schemas mithilfe einer PATCH-Anfrage aktualisieren. [!DNL Schema Registry] unterstützt alle standardmäßigen JSON Patch-Vorgänge, einschließlich `add`, `remove` und `replace`. Weitere Informationen zu JSON Patch finden Sie im [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Wenn Sie eine gesamte Ressource durch neue Werte ersetzen möchten, anstatt einzelne Felder zu aktualisieren, lesen Sie den Abschnitt unter [Ersetzen eines Schemas durch eine PUT-Operation](#put).

Einer der häufigsten PATCH-Vorgänge besteht darin, einem Schema zuvor definierte Feldergruppen hinzuzufügen, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id` -URI oder `meta:altId` des Schemas, das Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

The example request below adds a new field group to a schema by adding that field group&#39;s `$id` value to both the `meta:extends` and `allOf` arrays.

Der Anfragetext hat die Form eines Arrays, wobei jedes aufgelistete Objekt eine bestimmte Änderung an einem einzelnen Feld darstellt. Jedes Objekt enthält den auszuführenden Vorgang (`op`), das Feld, für das der Vorgang ausgeführt werden soll (`path`), und welche Informationen in diesem Vorgang enthalten sein sollen (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**Antwort**

Die Antwort zeigt, dass beide Vorgänge erfolgreich durchgeführt wurden. The field group `$id` has been added to the `meta:extends` array and a reference (`$ref`) to the field group `$id` now appears in the `allOf` array.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Aktivieren eines Schemas zur Verwendung im Echtzeit-Kundenprofil {#union}

Damit ein Schema am [Echtzeit-Kundenprofil](../../profile/home.md) teilnimmt, müssen Sie dem `meta:immutableTags` -Array des Schemas ein `union`-Tag hinzufügen. Dies können Sie erreichen, indem Sie eine PATCH-Anfrage für das betreffende Schema stellen.

>[!IMPORTANT]
>
>Unveränderliche Tags sind Tags, die festgelegt, aber nie entfernt werden sollen.

**API-Format**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id` -URI oder `meta:altId` des Schemas, das aktiviert werden soll. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Beispielanfrage fügt ein `meta:immutableTags` -Array zu einem vorhandenen Schema hinzu, sodass das Array einen einzelnen Zeichenfolgenwert von `union` erhält, um ihn für die Verwendung in Profil zu aktivieren.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**Antwort**

A successful response returns the details of the updated schema, showing that the `meta:immutableTags` array has been added.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

You can now view the union for this schema&#39;s class to confirm that the schema&#39;s fields are represented. Weitere Informationen finden Sie im [Vereinigungsendpunkt-Handbuch](./unions.md) .

## Schema löschen {#delete}

It may occasionally be necessary to remove a schema from the Schema Registry. Dies geschieht durch Ausführen einer DELETE-Anfrage mit der Schema-ID, die im Pfad angegeben ist.

**API-Format**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id` -URI oder `meta:altId` des Schemas, das Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine Nachschlageanfrage (GET) für das Schema ausführen. Sie müssen einen `Accept`-Header in die Anfrage einbeziehen, sollten jedoch einen HTTP-Status 404 (Nicht gefunden) erhalten, da das Schema aus der Schema Registry entfernt wurde.
