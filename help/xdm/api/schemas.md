---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Schema erstellen
description: Mit dem Endpunkt /Schemas in der Schema Registry API können Sie XDM-Schema in Ihrer Erlebnisanwendung programmgesteuert verwalten.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 19%

---


# Schemas-Endpunkt

Ein Schema kann man sich als Vorlage für die Daten vorstellen, die Sie in Adobe Experience Platform erfassen möchten. Jedes Schema besteht aus einer Klasse und null oder mehr Mixins. Mit dem `/schemas` Endpunkt in der [!DNL Schema Registry] API können Sie Schema in Ihrer Erlebnisanwendung programmgesteuert verwalten.

## Erste Schritte

The API endpoint used in this guide is part of the [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Bevor Sie fortfahren, lesen Sie bitte die [Anleitung](./getting-started.md) zu den ersten Schritten für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtige Informationen zu den erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer Experience Platformen-API erforderlich sind.

## Retrieve a list of schemas {#list}

Sie können alle Schema unter dem `global` bzw. dem `tenant` Container durch eine GET an `/global/schemas` bzw. `/tenant/schemas`anfordern.

>[!NOTE]
>
>Bei der Auflistung von Ressourcen wird das Schema Registry-Ergebnis auf 300 Elemente begrenzt. Um Ressourcen über diese Grenze hinaus zurückzugeben, müssen Sie Paging-Parameter verwenden. Es wird außerdem empfohlen, zusätzliche Abfragen zu verwenden, um Ergebnisse zu filtern und die Anzahl der zurückgegebenen Ressourcen zu reduzieren. Weitere Informationen finden Sie im Dokument zu den Parametern für die [Abfrage](./appendix.md#query) im Anhang.

**API-Format**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container mit den Schemas, die Sie abrufen möchten: `global` für von der Adobe erstellte Schema oder `tenant` für Schemas im Besitz Ihrer Organisation. |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse. Eine Liste der verfügbaren Parameter finden Sie im Dokument [im](./appendix.md#query) Anhang. |

**Anfrage**

Die folgende Anforderung ruft eine Liste von Schemas aus dem `tenant` Container ab, wobei ein `orderby` Parameter &quot;Abfrage&quot;verwendet wird, um die Ergebnisse nach ihrem `title` Attribut zu sortieren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

The response format depends on the `Accept` header sent in the request. The following `Accept` headers are available for listing schemas:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung der einzelnen Ressourcen zurück. Dies ist die empfohlene Kopfzeile für die Auflistung der Ressourcen. (Maximal: 300) |
| `application/vnd.adobe.xed+json` | Returns full JSON schema for each resource, with original `$ref` and `allOf` included. (Maximal: 300) |

**Antwort**

The request above used the `application/vnd.adobe.xed-id+json` `Accept` header, therefore the response includes only the `title`, `$id`, `meta:altId`, and `version` attributes for each schema. Mit der anderen `Accept` Kopfzeile (`application/vnd.adobe.xed+json`) werden alle Attribute jedes Schemas zurückgegeben. Select the appropriate `Accept` header depending on the information you require in your response.

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

Sie können ein bestimmtes Schema nachschlagen, indem Sie eine GET anfordern, die die ID des Schemas im Pfad enthält.

**API-Format**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container mit dem Schema, in dem Sie Folgendes abrufen möchten: `global` für ein von der Adobe erstelltes Schema oder `tenant` für ein Schema im Besitz Ihrer Organisation. |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodierte `$id` des Schemas, nach dem Sie suchen möchten. |

**Anfrage**

Die folgende Anforderung ruft ein Schema ab, das durch seinen `meta:altId` Wert im Pfad angegeben wird.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

Eine erfolgreiche Antwort gibt die Details des Schemas zurück. The fields that are returned depend on the `Accept` header sent in the request. Experiment with different `Accept` headers to compare the responses and determine which header is best for your use case.

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

## Schema erstellen {#create}

Der Prozess der Schemakomposition beginnt mit der Zuweisung einer Klasse. Die Klasse definiert wichtige verhaltensbezogene Aspekte der Daten (Datensatz oder Zeitreihen) sowie die Mindestfelder, die erforderlich sind, um die zu erfassenden Daten zu beschreiben.

>[!NOTE]
>
>Der folgende Beispielaufruf ist nur ein Grundbeispiel dafür, wie ein Schema in der API erstellt wird, mit den minimalen Kompositionserfordernissen einer Klasse und ohne Mixins. Ausführliche Anweisungen zum Erstellen eines Schemas in der API, einschließlich zum Zuweisen von Feldern mit Mixins und Datentypen, finden Sie im Lernprogramm zur Erstellung von [Schemas](../tutorials/create-schema-api.md).

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
| `allOf` | Ein Array von Objekten, wobei jedes Objekt auf eine Klasse oder Mischung verweist, deren Felder vom Schema implementiert werden. Jedes Objekt enthält eine einzelne Eigenschaft (`$ref`), deren Wert den Wert `$id` der Klasse darstellt oder die vom neuen Schema implementiert wird. Es muss eine Klasse mit null oder mehr zusätzlichen Mixins bereitgestellt werden. Im obigen Beispiel ist das einzelne Objekt im `allOf` Array die Klasse des Schemas. |

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

Performing a GET request to [list all schemas](#list) in the tenant container would now include the new schema. You can perform a [lookup (GET) request](#lookup) using the URL-encoded `$id` URI to view the new schema directly.

Um einem Schema weitere Felder hinzuzufügen, können Sie einen [PATCH-Vorgang](#patch) ausführen, um Mixins zu den Schemas `allOf` und `meta:extends` Arrays hinzuzufügen.

## Schema aktualisieren {#put}

Sie können ein ganzes Schema durch eine PUT ersetzen und die Ressource im Grunde neu schreiben. Beim Aktualisieren eines Schemas über eine PUT-Anforderung muss der Haupttext alle Felder enthalten, die beim [Erstellen eines neuen Schemas](#create) in einer POST-Anforderung erforderlich sind.

>[!NOTE]
>
>If you only want to update part of a schema instead of replacing it entirely, see the section on [updating a portion of a schema](#patch).

**API-Format**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodierte `$id` des Schemas, das Sie neu schreiben möchten. |

**Anfrage**

Die folgende Anforderung ersetzt ein vorhandenes Schema und ändert dessen `title`, `description`und `allOf` Attribute.

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

## Update a portion of a schema {#patch}

Sie können einen Teil eines Schemas mit einer PATCH-Anforderung aktualisieren. Der [!DNL Schema Registry] unterstützt alle standardmäßigen JSON Patch-Vorgänge einschließlich `add`, `remove`und `replace`. Weitere Informationen zum JSON-Patch finden Sie im Handbuch [API-Grundlagen](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>If you want to replace an entire resource with new values instead of updating individual fields, see the section on [replacing a schema using a PUT operation](#put).

Eine der häufigsten PATCH-Vorgänge besteht darin, einem Schema zuvor definierte Mixins hinzuzufügen, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` das zu aktualisierende Schema. |

**Anfrage**

Die folgende Beispielanforderung fügt einem Schema eine neue Mischung hinzu, indem der `$id` Wert dieser Mischung sowohl den `meta:extends` als auch den `allOf` Arrays hinzugefügt wird.

Der Anforderungstext besteht aus einem Array, wobei jedes aufgelistete Objekt eine bestimmte Änderung an einem einzelnen Feld darstellt. Jedes Objekt enthält die auszuführende Operation (`op`), welches Feld für die Operation ausgeführt werden soll (`path`) und welche Informationen in diesen Vorgang einzuschließen sind (`value`).

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

Die Antwort zeigt, dass beide Vorgänge erfolgreich durchgeführt wurden. Das Mixin `$id` wurde dem Array `meta:extends` hinzugefügt und ein Verweis (`$ref`) auf das Mixin `$id` wird jetzt im Array `allOf` angezeigt.

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

## Enable a schema for use in Real-time Customer Profile {#union}

Damit ein Schema an einem [Echtzeit-Customer-Profil](../../profile/home.md)teilnehmen kann, müssen Sie ein `union` -Tag zum `meta:immutableTags` Array des Schemas hinzufügen. Sie können dies erreichen, indem Sie eine PATCH für das betreffende Schema anfordern.

>[!IMPORTANT]
>
>Unveränderliche Tags sind Tags, die festgelegt, aber nie entfernt werden sollen.

**API-Format**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` das Schema, das aktiviert werden soll. |

**Anfrage**

Die folgende Beispielanforderung fügt einem vorhandenen Schema ein `meta:immutableTags` Array hinzu, wobei dem Array ein einzelner Zeichenfolgenwert zugewiesen wird, der es für die Verwendung in Profil aktivieren `union` soll.

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

Eine erfolgreiche Antwort gibt die Details des aktualisierten Schemas zurück und zeigt an, dass das `meta:immutableTags` Array hinzugefügt wurde.

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

Sie können nun die Vereinigung für die Klasse dieses Schemas zur Bestätigung der Anzeige der Felder des Schemas Ansicht haben. See the [unions endpoint guide](./unions.md) for more information.

## Löschen eines Schemas {#delete}

Gelegentlich kann es erforderlich sein, ein Schema aus dem Schema-Register zu entfernen. Dies geschieht durch eine DELETE-Anforderung mit der im Pfad angegebenen Schema-ID.

**API-Format**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` das zu löschende Schema. |

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

Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an das Schema senden. You will need to include an `Accept` header in the request, but should receive an HTTP status 404 (Not Found) because the schema has been removed from the Schema Registry.