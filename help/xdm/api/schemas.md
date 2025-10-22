---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schema Registry;Schema Registry;schema;Schemas;Schemas;erstellen
solution: Experience Platform
title: API-Endpunkt für Schemata
description: Mit dem Endpunkt /schemas in der Schema Registry-API können Sie XDM-Schemas in Ihrem Erlebnisprogramm programmgesteuert verwalten.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: dc5ac5427e1eeef47434c3974235a1900d29b085
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 15%

---

# Endpunkt für Schemata

Ein Schema kann als Blueprint für die Daten betrachtet werden, die Sie in Adobe Experience Platform aufnehmen möchten. Jedes Schema besteht aus einer Klasse und keiner oder mehreren Schemafeldgruppen. Mit dem `/schemas`-Endpunkt in der [!DNL Schema Registry]-API können Sie Schemas in Ihrem Erlebnisprogramm programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste von Schemata {#list}

Sie können alle Schemata unter dem `global`- oder `tenant`-Container auflisten, indem Sie eine GET-Anfrage an `/global/schemas` bzw. `/tenant/schemas` stellen.

>[!NOTE]
>
>Beim Auflisten von Ressourcen beschränkt die Schemaregistrierung Ergebnismengen auf 300 Elemente. Um Ressourcen über dieses Limit hinaus zurückzugeben, müssen Sie Paging-Parameter verwenden. Es wird außerdem empfohlen, zusätzliche Abfrageparameter zu verwenden, um Ergebnisse zu filtern und die Anzahl der zurückgegebenen Ressourcen zu reduzieren. Weitere Informationen finden Sie [&#x200B; Abschnitt &#x200B;](./appendix.md#query)Abfrageparameter“ im Anhang.

**API-Format**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, der die Schemata enthält, die Sie abrufen möchten: `global` für von Adobe erstellte Schemata oder `tenant` für Schemata, die Ihrem Unternehmen gehören. |
| `{QUERY_PARAMS}` | Optionale Abfrageparameter zum Filtern der Ergebnisse nach . Eine Liste der verfügbaren Parameter finden [&#x200B; im &#x200B;](./appendix.md#query)-Dokument . |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft eine Liste von Schemata aus dem `tenant`-Container ab und verwendet einen `orderby` Abfrageparameter, um die Ergebnisse nach ihrem `title` Attribut zu sortieren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Format der Antwort hängt von der in der Anfrage gesendeten `Accept`-Kopfzeile ab. Die folgenden `Accept`-Kopfzeilen sind für die Auflistung von Schemata verfügbar:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung jeder Ressource zurück. Dies ist die empfohlene Kopfzeile zum Auflisten von Ressourcen. (Limit: 300) |
| `application/vnd.adobe.xed+json` | Gibt das vollständige JSON-Schema für jede Ressource mit den ursprünglichen `$ref` und `allOf` zurück. (Limit: 300) |

{style="table-layout:auto"}

**Antwort**

Die obige Anfrage verwendete die `application/vnd.adobe.xed-id+json` `Accept`-Kopfzeile. Daher enthält die Antwort für jedes Schema nur die Attribute `title`, `$id`, `meta:altId` und `version`. Bei Verwendung der anderen `Accept`-Kopfzeile (`application/vnd.adobe.xed+json`) werden alle Attribute der einzelnen Schemata zurückgegeben. Wählen Sie den entsprechenden `Accept`-Header entsprechend den Informationen aus, die Sie in Ihrer Antwort benötigen.

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

Sie können ein bestimmtes Schema suchen, indem Sie eine GET-Anfrage stellen, die die ID des Schemas im Pfad enthält.

**API-Format**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, der das abzurufende Schema enthält: `global` für ein von Adobe erstelltes Schema oder `tenant` für ein Schema, das Ihrem Unternehmen gehört. |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodierte `$id` des Schemas, das Sie suchen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft ein Schema ab, das durch seinen `meta:altId` im Pfad angegeben ist.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` und `allOf` aufgelöst wurden, enthält Titel und Beschreibungen. Verworfene Felder werden mit dem `meta:status` Attribut `deprecated` gekennzeichnet. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Schemas zurück. Die zurückgegebenen Felder hängen von der `Accept` ab, die in der Anfrage gesendet wird. Experimentieren Sie mit verschiedenen `Accept`-Kopfzeilen, um die Antworten zu vergleichen und festzustellen, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

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
  "imsOrg": "{ORG_ID}",
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

Der Prozess der Schemakomposition beginnt mit der Zuweisung einer Klasse. Die Klasse definiert wichtige verhaltensbezogene Aspekte der Daten (Eintrag oder Zeitreihen) sowie die Mindestfelder, die erforderlich sind, um die zu erfassenden Daten zu beschreiben.

Anweisungen zum Erstellen eines Schemas ohne Klassen oder Feldergruppen, auch als relationales Schema bezeichnet, finden Sie im Abschnitt [Erstellen eines relationalen &#x200B;](#create-relational-schema)&quot;.

>[!NOTE]
>
>Der folgende Beispielaufruf ist nur ein grundlegendes Beispiel für die Erstellung eines Schemas in der API mit den minimalen Kompositionsanforderungen einer Klasse und ohne Feldergruppen. Eine vollständige Anleitung zum Erstellen eines Schemas in der API, einschließlich der Zuweisung von Feldern mithilfe von Feldergruppen und Datentypen, finden Sie im [Tutorial zur Schemaerstellung](../tutorials/create-schema-api.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `allOf` | Ein Array von Objekten, wobei jedes Objekt auf eine Klasse oder Feldergruppe verweist, deren Felder das Schema implementiert. Jedes Objekt enthält eine einzelne Eigenschaft (`$ref`), deren Wert den `$id` der Klasse oder Feldergruppe darstellt, die das neue Schema implementieren wird. Es muss eine Klasse mit null oder mehr zusätzlichen Feldergruppen bereitgestellt werden. Im obigen Beispiel ist das einzelne Objekt im `allOf`-Array die Klasse des Schemas. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und eine Payload mit den Details zum neu erstellten Schema zurück, einschließlich `$id`, `meta:altId` und `version`. Diese Werte sind schreibgeschützt und werden vom [!DNL Schema Registry] zugewiesen.

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
    "imsOrg": "{ORG_ID}",
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

Wenn Sie eine GET-Anfrage ausführen[&#x200B; um alle Schemata &#x200B;](#list) Mandanten-Container aufzulisten, würde jetzt das neue Schema enthalten. Sie können eine [Suchanfrage (GET) &#x200B;](#lookup), indem Sie den URL-kodierten `$id`-URI verwenden, um das neue Schema direkt anzuzeigen.

Um einem Schema zusätzliche Felder hinzuzufügen, können Sie einen [PATCH-Vorgang](#patch) ausführen, um den `allOf`- und `meta:extends`-Arrays des Schemas Feldergruppen hinzuzufügen.

## Relationales Schema erstellen {#create-relational-schema}

>[!AVAILABILITY]
>
>Data Mirror und relationale Schemata stehen Adobe Journey Optimizer-Lizenzinhabern **Orchestrierte Kampagnen** zur Verfügung. Sie sind auch als **eingeschränkte Version** für Customer Journey Analytics-Benutzer verfügbar, je nach Ihrer Lizenz und der Aktivierung von Funktionen. Wenden Sie sich an den Adobe-Support, um Zugang zu erhalten.

>[!NOTE]
>
>Relationale Schemata wurden in früheren Versionen der Adobe Experience Platform-API-Dokumentation zuvor als modellbasierte Schemata bezeichnet. Die Funktionalität bleibt gleich - nur die Terminologie wurde aus Gründen der Übersichtlichkeit geändert.

Erstellen Sie ein relationales Schema, indem Sie eine POST-Anfrage an den `/schemas`-Endpunkt senden. Relationale Schemata speichern strukturierte Daten im relationalen Stil **ohne** Klassen oder Feldergruppen. Definieren Sie Felder direkt im Schema und identifizieren Sie das Schema mithilfe eines logischen Verhaltens-Tags als relational.

>[!IMPORTANT]
>
>Um ein relationales Schema zu erstellen, setzen Sie `meta:extends` auf `"https://ns.adobe.com/xdm/data/adhoc-v2"`. Dies ist eine **logische Verhaltenskennung** (kein physisches Verhalten oder keine Klasse). Verweisen **nicht** auf Klassen oder Feldergruppen in `allOf` und schließen **nicht** Klassen oder Feldergruppen in `meta:extends` ein.

Erstellen Sie zuerst das Schema mit `POST /tenant/schemas`. Fügen Sie dann die erforderlichen Deskriptoren mit der [Deskriptoren-API (`POST /tenant/descriptors`) hinzu](../api/descriptors.md):

- [Primärer Schlüsseldeskriptor](../api/descriptors.md#primary-key-descriptor): Ein Primärschlüsselfeld muss sich auf der **Stammebene“ befinden** als **markiert**.
- [Versionsdeskriptor](../api/descriptors.md#version-descriptor): **Erforderlich** wenn ein Primärschlüssel vorhanden ist.
- [Beziehungsdeskriptor](../api/descriptors.md#relationship-descriptor): Optional, definiert Joins; Kardinalität wird bei der Aufnahme nicht erzwungen.
- [Zeitstempeldeskriptor](../api/descriptors.md#timestamp-descriptor): Bei Zeitreihenschemata muss der Primärschlüssel ein **zusammengesetzter** Schlüssel sein, der das Zeitstempelfeld enthält.

>[!NOTE]
>
>Im Benutzeroberflächenschema-Editor werden die Versionsdeskriptor- und Zeitstempeldeskriptoren als &quot;[!UICONTROL Version identifier]&quot; bzw. &quot;[!UICONTROL Timestamp identifier]&quot; angezeigt.

>[!CAUTION]
>
>Relationale Schemata sind **nicht kompatibel mit Vereinigungsschemata**. Wenden Sie beim Arbeiten mit relationalen Schemata das `union`-Tag nicht auf `meta:immutableTags` an. Diese Konfiguration ist in der Benutzeroberfläche blockiert, wird aber derzeit nicht von der API blockiert. Weitere Informationen zum Verhalten [&#x200B; Vereinigungsschemas finden &#x200B;](./unions.md) im Handbuch zum Vereinigungsendpunkt .

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

```shell
curl --request POST \
  --url https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
  "title": "marketing.customers",
  "type": "object",
  "description": "Schema of the Marketing Customers table.",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "meta:xdmType": "object"
    }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record"
}
'
```

### Eigenschaften des Anfragetexts

| Eigenschaft | Typ | Beschreibung |
| ------------------------------- | ------ | --------------------------------------------------------- |
| `title` | Zeichenfolge | Anzeigename des Schemas. |
| `description` | String | Kurze Erläuterung des Zwecks des Schemas. |
| `type` | String | Muss für relationale Schemata `"object"` werden. |
| `definitions` | Objekt | Enthält die Objekte auf Stammebene, die Ihre Schemafelder definieren. |
| `definitions.<name>.properties` | Objekt | Feldnamen und Datentypen. |
| `allOf` | Array | Verweist auf die Objektdefinition auf der Stammebene (z. B. `#/definitions/marketing_customers`). |
| `meta:extends` | Array | Muss `"https://ns.adobe.com/xdm/data/adhoc-v2"` enthalten, um das Schema als relational zu identifizieren. |
| `meta:behaviorType` | String | Auf `"record"` festgelegt. Verwenden Sie `"time-series"` nur, wenn aktiviert und geeignet. |

>[!IMPORTANT]
>
>Die Schemaentwicklung für relationale Schemata folgt denselben additiven Regeln wie Standardschemata. Sie können neue Felder mit einer PATCH-Anfrage hinzufügen. Änderungen wie das Umbenennen oder Entfernen von Feldern sind nur zulässig, wenn keine Daten in den Datensatz aufgenommen wurden.

**Antwort**

Bei einer erfolgreichen Anfrage werden **HTTP 201 (Erstellt)** und das erstellte Schema zurückgegeben.

>[!NOTE]
>
>Relationale Schemata erben keine vordefinierten Felder (z. B. id, timestamp oder eventType). Definieren Sie alle erforderlichen Felder explizit in Ihrem Schema.

**Beispielantwort**

```json
{
  "$id": "https://ns.adobe.com/<TENANT_ID>/schemas/<SCHEMA_UUID>",
  "meta:altId": "_<SCHEMA_ALT_ID>",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "marketing.customers",
  "description": "Schema of the Marketing Customers table.",
  "type": "object",
  "definitions": {
    "marketing_customers": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    { "$ref": "#/definitions/marketing_customers" }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record",
  "meta:containerId": "tenant"
}
```

### Eigenschaften des Antworttextes

| Eigenschaft | Typ | Beschreibung |
| ------------------- | ------ | -------------------------- |
| `$id` | Zeichenfolge | Die eindeutige URL des erstellten Schemas. Verwenden Sie in nachfolgenden API-Aufrufen. |
| `meta:altId` | String | Eine alternative Kennung für das Schema. |
| `meta:resourceType` | String | Der Ressourcentyp (immer `"schemas"`). |
| `version` | String | Eine Schemaversion, die bei der Erstellung zugewiesen wurde. |
| `title` | String | Der Anzeigename des Schemas. |
| `description` | String | Eine kurze Erläuterung des Zwecks des Schemas. |
| `type` | String | Der Schematyp. |
| `definitions` | Objekt | Definiert wiederverwendbare Objekte oder Feldergruppen, die im Schema verwendet werden. Dies umfasst normalerweise die Hauptdatenstruktur und wird im `allOf`-Array referenziert, um den Schemastamm zu definieren. |
| `allOf` | Array | Gibt das Stammobjekt des Schemas durch Verweis auf eine oder mehrere Definitionen an (z. B. `#/definitions/marketing_customers`). |
| `meta:extends` | Array | Identifiziert das Schema als relational (`adhoc-v2`). |
| `meta:behaviorType` | String | Verhaltenstyp (`record` oder `time-series`, falls aktiviert). |
| `meta:containerId` | String | Container, in dem das Schema gespeichert ist (z. B. `tenant`). |

Um einem relationalen Schema nach seiner Erstellung Felder hinzuzufügen, stellen Sie eine [PATCH-Anfrage](#patch). Relationale Schemata erben nicht und entwickeln sich nicht automatisch. Strukturelle Änderungen wie das Umbenennen oder Löschen von Feldern sind nur zulässig, wenn keine Daten in den Datensatz aufgenommen wurden. Sobald Daten vorhanden sind **werden nur** additive Änderungen“ (z. B. das Hinzufügen neuer Felder) unterstützt.

Sie können neue Felder auf Stammebene hinzufügen (innerhalb der Stammdefinition oder des `properties`), aber Sie können den Typ der vorhandenen Felder nicht entfernen, umbenennen oder ändern.

>[!CAUTION]
>
>Die Schemaentwicklung wird eingeschränkt, nachdem ein Datensatz mithilfe des Schemas initialisiert wurde. Planen Sie Feldnamen und -typen sorgfältig im Voraus, da Felder nach der Aufnahme von Daten nicht mehr gelöscht oder geändert werden können.

## Schema aktualisieren {#put}

Sie können ein ganzes Schema durch einen PUT-Vorgang ersetzen, indem Sie die Ressource im Wesentlichen neu schreiben. Beim Aktualisieren eines Schemas über eine PUT-Anfrage muss der Hauptteil alle Felder enthalten, die beim [&#x200B; eines neuen Schemas in &#x200B;](#create) POST-Anfrage erforderlich sind.

>[!NOTE]
>
>Wenn Sie nur einen Teil eines Schemas aktualisieren möchten, anstatt es vollständig zu ersetzen, finden Sie weitere Informationen im Abschnitt [Aktualisieren eines Teils eines Schemas](#patch).

**API-Format**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodierte `$id` des Schemas, das Sie umschreiben möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ersetzt ein vorhandenes Schema und ändert dessen `title`-, `description`- und `allOf`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "imsOrg": "{ORG_ID}",
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

## Aktualisieren eines Teils eines Schemas {#patch}

Sie können einen Teil eines Schemas mithilfe einer PATCH-Anfrage aktualisieren. Der [!DNL Schema Registry] unterstützt alle standardmäßigen JSON-Patch-Vorgänge, einschließlich `add`, `remove` und `replace`. Weitere Informationen zu JSON-Patch-Vorgängen finden Sie im [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>Wenn Sie eine gesamte Ressource durch neue Werte ersetzen möchten, anstatt einzelne Felder zu aktualisieren, finden Sie weitere Informationen im Abschnitt zum [&#x200B; eines Schemas mithilfe eines PUT-Vorgangs](#put).

Einer der häufigsten PATCH-Vorgänge besteht darin, wie im folgenden Beispiel gezeigt, zuvor definierte Feldergruppen zu einem Schema hinzuzufügen.

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id`-URI oder `meta:altId` des Schemas, das Sie aktualisieren möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Beispielanfrage fügt eine neue Feldergruppe zu einem Schema hinzu, indem der `$id` dieser Feldergruppe sowohl zum `meta:extends`- als auch zum `allOf`-Array hinzugefügt wird.

Der Anfragetext hat die Form eines Arrays, wobei jedes aufgelistete Objekt eine bestimmte Änderung an einem einzelnen Feld darstellt. Jedes Objekt enthält den auszuführenden Vorgang (`op`), in welchem Feld der Vorgang ausgeführt werden soll (`path`) und welche Informationen in diesem Vorgang enthalten sein sollen (`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Die Antwort zeigt, dass beide Vorgänge erfolgreich durchgeführt wurden. Die Feldergruppe `$id` wurde dem `meta:extends`-Array hinzugefügt und ein Verweis (`$ref`) auf die Feldergruppe `$id` jetzt im `allOf`-Array angezeigt.

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
    "imsOrg": "{ORG_ID}",
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

Damit ein Schema am Echtzeit[Kundenprofil teilnehmen kann, &#x200B;](../../profile/home.md) Sie dem `union`-Array des Schemas ein `meta:immutableTags`-Tag hinzufügen. Sie können dies tun, indem Sie eine PATCH-Anfrage für das betreffende Schema stellen.

>[!IMPORTANT]
>
>Unveränderliche Tags sind Tags, die festgelegt, aber nie entfernt werden sollen.

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id`-URI oder `meta:altId` des Schemas, das Sie aktivieren möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Beispielanfrage fügt einem vorhandenen Schema ein `meta:immutableTags`-Array hinzu, sodass das Array einen einzelnen Zeichenfolgenwert von `union` erhält, um es für die Verwendung im Profil zu aktivieren.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Eine erfolgreiche Antwort gibt die Details des aktualisierten Schemas zurück und zeigt an, dass das `meta:immutableTags`-Array hinzugefügt wurde.

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
    "imsOrg": "{ORG_ID}",
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

Sie können jetzt die Vereinigung für die Klasse dieses Schemas anzeigen, um zu bestätigen, dass die Felder des Schemas dargestellt werden. Weitere Informationen finden Sie [&#x200B; &quot;](./unions.md)-Endpunkthandbuch“.

## Löschen eines Schemas {#delete}

Gelegentlich kann es erforderlich sein, ein Schema aus der Schemaregistrierung zu entfernen. Dies geschieht, indem eine DELETE-Anfrage mit der im Pfad angegebenen Schema-ID durchgeführt wird.

**API-Format**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id`-URI oder `meta:altId` des Schemas, das Sie löschen möchten. |

{style="table-layout:auto"}

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an das Schema stellen. Sie müssen einen `Accept`-Header in die Anfrage einbeziehen, sollten jedoch einen HTTP-Status 404 (Nicht gefunden) erhalten, da das Schema aus der Schemaregistrierung entfernt wurde.
