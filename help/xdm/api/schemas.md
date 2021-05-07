---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;Schema;Schema;Schemas;Schemas;Erstellen;Erstellen
solution: Experience Platform
title: Schemas-API-Endpunkt
description: Mit dem Endpunkt /Schemas in der Schema Registry API können Sie XDM-Schema in Ihrer Erlebnisanwendung programmgesteuert verwalten.
topic-legacy: developer guide
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 16%

---

# Schemas-Endpunkt

Ein Schema kann man sich als Vorlage für die Daten vorstellen, die Sie in Adobe Experience Platform erfassen möchten. Jedes Schema besteht aus einer Klasse und einer Schema-Feldgruppe von null oder mehr. Mit dem `/schemas`-Endpunkt in der [!DNL Schema Registry]-API können Sie Schema in Ihrer Erlebnisanwendung programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](./getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer Experience Platformen-API benötigt werden.

## Abrufen einer Liste von Schemas {#list}

Sie können alle Schema unter dem Container `global` oder `tenant` durch eine GET an `/global/schemas` bzw. `/tenant/schemas` Liste durchführen.

>[!NOTE]
>
>Bei der Auflistung von Ressourcen wird das Schema Registry-Ergebnis auf 300 Elemente begrenzt. Um Ressourcen über diese Grenze hinaus zurückzugeben, müssen Sie Paging-Parameter verwenden. Es wird außerdem empfohlen, zusätzliche Abfragen zu verwenden, um Ergebnisse zu filtern und die Anzahl der zurückgegebenen Ressourcen zu reduzieren. Weitere Informationen finden Sie im Dokument unter [Abfrage parameters](./appendix.md#query) im Anhang.

**API-Format**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container mit den Schemas, die Sie abrufen möchten: `global` für Adoben erstellte Schema oder `tenant` für Schemas, die Ihrem Unternehmen gehören. |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse. Eine Liste der verfügbaren Parameter finden Sie im Dokument [Anhang](./appendix.md#query). |

**Anfrage**

Mit der folgenden Anforderung wird eine Liste von Schemas aus dem Container `tenant` abgerufen. Dabei wird ein Parameter `orderby` für die Abfrage verwendet, um die Ergebnisse nach dem Attribut `title` zu sortieren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept`-Kopfzeile ab, die in der Anforderung gesendet wird. Die folgenden `Accept`-Kopfzeilen stehen zur Auflistung von Schemas zur Verfügung:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung der einzelnen Ressourcen zurück. Dies ist die empfohlene Kopfzeile für die Auflistung der Ressourcen. (Maximal: 300) |
| `application/vnd.adobe.xed+json` | Gibt für jede Ressource das vollständige JSON-Schema zurück, wobei die ursprünglichen Werte `$ref` und `allOf` enthalten sind. (Maximal: 300) |

**Antwort**

Bei der oben genannten Anforderung wurde die Überschrift `application/vnd.adobe.xed-id+json` `Accept` verwendet. Daher enthält die Antwort nur die Attribute `title`, `$id`, `meta:altId` und `version` für jedes Schema. Mit der anderen `Accept`-Kopfzeile (`application/vnd.adobe.xed+json`) werden alle Attribute jedes Schemas zurückgegeben. Wählen Sie die entsprechende `Accept`-Kopfzeile, je nach den Informationen, die Sie in Ihrer Antwort benötigen.

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
| `{CONTAINER_ID}` | Der Container mit dem Schema, in dem Sie Folgendes abrufen möchten: `global` für ein von der Adobe erstelltes Schema oder `tenant` für ein Schema, das Ihrem Unternehmen gehört. |
| `{SCHEMA_ID}` | Die `meta:altId`- oder URL-kodierte `$id` des Schemas, nach dem Sie suchen möchten. |

**Anfrage**

Die folgende Anforderung ruft ein Schema ab, das durch den Wert `meta:altId` im Pfad angegeben wird.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept`-Kopfzeile ab, die in der Anforderung gesendet wird. Für alle Nachschlageanforderungen muss eine `version` in die `Accept`-Kopfzeile eingefügt werden. Die folgenden `Accept`-Kopfzeilen stehen zur Verfügung:

| `Accept`-Kopfzeile | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | Roh mit `$ref` und `allOf`, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` und `allOf` aufgelöst, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Roh mit `$ref` und `allOf`, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` und `allOf` aufgelöst, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` und `allOf` aufgelöst, einschließlich Deskriptoren. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Schemas zurück. Die zurückgegebenen Felder hängen von der `Accept`-Kopfzeile ab, die in der Anforderung gesendet wird. Experimentieren Sie mit verschiedenen `Accept`-Kopfzeilen, um die Antworten zu vergleichen und festzustellen, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

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
          "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/fieldgroups/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
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
>Der folgende Beispielaufruf ist nur ein Grundbeispiel dafür, wie ein Schema in der API erstellt wird, mit den Mindestanforderungen an die Zusammensetzung einer Klasse und ohne Feldgruppen. Ausführliche Anweisungen zum Erstellen eines Schemas in der API, einschließlich zum Zuweisen von Feldern mit Feldgruppen und Datentypen, finden Sie im Tutorial [Schema-Erstellung](../tutorials/create-schema-api.md).

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
| `allOf` | Ein Array von Objekten, wobei jedes Objekt auf eine Klasse oder Feldgruppe verweist, deren Felder vom Schema implementiert werden. Jedes Objekt enthält eine einzelne Eigenschaft (`$ref`), deren Wert das `$id` der Klasse oder Feldgruppe darstellt, die das neue Schema implementieren wird. Es muss eine Klasse mit null oder mehr zusätzlichen Feldgruppen bereitgestellt werden. Im obigen Beispiel ist das einzelne Objekt im Array `allOf` die Klasse des Schemas. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und eine Payload mit den Details zum neu erstellten Schema zurück, einschließlich `$id`, `meta:altId` und `version`. Diese Werte sind schreibgeschützt und werden durch das [!DNL Schema Registry] zugewiesen.

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

Wenn Sie eine GET für [Liste aller Schema](#list) im Pächter-Container durchführen, wird jetzt das neue Schema einbezogen. Sie können eine [Suchanfrage (GET)](#lookup) mit dem URL-kodierten `$id`-URI ausführen, um das neue Schema direkt Ansicht.

Um einem Schema weitere Felder hinzuzufügen, können Sie einen [PATCH-Vorgang](#patch) ausführen, um den Arrays des Schemas `allOf` und `meta:extends` Feldgruppen hinzuzufügen.

## Schema {#put} aktualisieren

Sie können ein ganzes Schema durch eine PUT ersetzen und die Ressource im Grunde neu schreiben. Beim Aktualisieren eines Schemas über eine PUT-Anforderung muss der Haupttext alle erforderlichen Felder enthalten, wenn [ein neues Schema](#create) in einer POST erstellt wird.

>[!NOTE]
>
>Wenn Sie nur einen Teil eines Schemas aktualisieren möchten, anstatt es vollständig zu ersetzen, lesen Sie den Abschnitt [Aktualisieren eines Teils eines Schemas](#patch).

**API-Format**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId`- oder URL-kodierte `$id` des Schemas, das Sie neu schreiben möchten. |

**Anfrage**

Die folgende Anforderung ersetzt ein vorhandenes Schema und ändert die Attribute `title`, `description` und `allOf`.

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

## Einen Teil eines Schemas {#patch} aktualisieren

Sie können einen Teil eines Schemas mit einer PATCH-Anforderung aktualisieren. [!DNL Schema Registry] unterstützt alle standardmäßigen JSON-Patch-Vorgänge, einschließlich `add`, `remove` und `replace`. Weitere Informationen zum JSON-Patch finden Sie im Handbuch [API-Grundlagen](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Wenn Sie eine gesamte Ressource durch neue Werte ersetzen möchten, anstatt einzelne Felder zu aktualisieren, lesen Sie den Abschnitt unter [Ersetzen eines Schemas mit einem PUT-Vorgang](#put).

Einer der häufigsten PATCH-Vorgänge besteht darin, einem Schema zuvor definierte Feldgruppen hinzuzufügen, wie im folgenden Beispiel gezeigt.

**API-Format**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id`-URI oder `meta:altId` des Schemas, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Beispielanforderung fügt einem Schema eine neue Feldgruppe hinzu, indem der `$id`-Wert dieser Feldgruppe sowohl den Arrays `meta:extends` als auch `allOf` hinzugefügt wird.

Der Anforderungstext besteht aus einem Array, wobei jedes aufgelistete Objekt eine bestimmte Änderung an einem einzelnen Feld darstellt. Jedes Objekt enthält den auszuführenden Vorgang (`op`), für welches Feld der Vorgang durchgeführt werden soll (`path`) und welche Informationen in diesen Vorgang einbezogen werden sollen (`value`).

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
          "value":  "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**Antwort**

Die Antwort zeigt, dass beide Vorgänge erfolgreich durchgeführt wurden. Die Feldgruppe `$id` wurde dem Array `meta:extends` hinzugefügt und im Array `allOf` wird nun ein Verweis (`$ref`) zur Feldgruppe `$id` angezeigt.

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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
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

## Aktivieren eines Schemas zur Verwendung im Echtzeit-Kundenkonto-Profil {#union}

Damit ein Schema am [Echtzeit-Kundenstamm](../../profile/home.md) teilnimmt, müssen Sie dem `meta:immutableTags`-Array des Schemas ein `union`-Tag hinzufügen. Sie können dies erreichen, indem Sie eine PATCH für das betreffende Schema anfordern.

>[!IMPORTANT]
>
>Unveränderliche Tags sind Tags, die festgelegt, aber nie entfernt werden sollen.

**API-Format**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id`-URI oder `meta:altId` des Schemas, das aktiviert werden soll. |

**Anfrage**

In der folgenden Beispielanforderung wird einem vorhandenen Schema ein `meta:immutableTags`-Array hinzugefügt, wobei dem Array ein einzelner Zeichenfolgenwert `union` zugewiesen wird, um ihn für die Verwendung in Profil zu aktivieren.

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

Eine erfolgreiche Antwort gibt die Details des aktualisierten Schemas zurück und zeigt an, dass das Array `meta:immutableTags` hinzugefügt wurde.

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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/e49cbb2eec33618f686b8344b4597ecf"
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

Sie können nun die Vereinigung für die Klasse dieses Schemas zur Bestätigung der Anzeige der Felder des Schemas Ansicht haben. Weitere Informationen finden Sie im Endpunktleitfaden [Vereinigungen](./unions.md).

## Löschen eines Schemas {#delete}

Gelegentlich kann es erforderlich sein, ein Schema aus dem Schema-Register zu entfernen. Dies geschieht durch eine DELETE-Anforderung mit der im Pfad angegebenen Schema-ID.

**API-Format**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die URL-kodierte `$id`-URI oder `meta:altId` des Schemas, das Sie löschen möchten. |

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

Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an das Schema senden. Sie müssen einen `Accept`-Header in die Anforderung einbeziehen, sollten jedoch einen HTTP-Status 404 (Nicht gefunden) erhalten, da das Schema aus der Schema-Registrierung entfernt wurde.
