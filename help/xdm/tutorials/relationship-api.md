---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beziehung zwischen zwei Schemas mithilfe der Schemaregistrierungs-API definieren
topic: tutorials
translation-type: tm+mt
source-git-commit: 849142e44c56f2958e794ca6aefaccd5670c28ba
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 49%

---


# Define a relationship between two schemas using the [!DNL Schema Registry] API


Die Fähigkeit, Beziehungen zwischen Ihren Kunden und ihren Interaktionen mit Ihrer Marke über verschiedene Kanäle hinweg zu verstehen, ist ein wichtiger Bestandteil von Adobe Experience Platform. Defining these relationships within the structure of your [!DNL Experience Data Model] (XDM) schemas allows you to gain complex insights into your customer data.

Während Schema-Beziehungen durch die Verwendung des Vereinigung-Schemas abgeleitet werden können, gilt [!DNL Real-time Customer Profile]dies nur für Schema, die dieselbe Klasse gemeinsam haben. Zur Herstellung einer Beziehung zwischen zwei Schemas, die zu verschiedenen Klassen gehören, muss einem Quell-Schema ein dediziertes **Beziehungsfeld** hinzugefügt werden, das auf die Identität eines Ziel-Schemas verweist.

This document provides a tutorial for defining a one-to-one relationship between two schemas defined by your organization using the [!DNL Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Erste Schritte

Dieses Tutorial erfordert ein funktionierendes Verständnis von [!DNL Experience Data Model] (XDM) und [!DNL XDM System]. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und seine Implementierung in [!DNL Experience Platform].
   * [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemas.
* [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Als Vorbereitung für dieses Tutorial sollten Sie im [Entwicklerhandbuch](../api/getting-started.md) die wichtigsten Themen rund um die konkrete Vorgehensweise für Aufrufe der API durchgehen. [!DNL Schema Registry] This includes your `{TENANT_ID}`, the concept of &quot;containers&quot;, and the required headers for making requests (with special attention to the [!DNL Accept] header and its possible values).

## Quell- und Zielschema definieren {#define-schemas}

Wir gehen davon aus, dass Sie die beiden Schemas, die in der Beziehung definiert werden sollen, bereits erstellt haben. This tutorial creates a relationship between members of an organization&#39;s current loyalty program (defined in a &quot;[!DNL Loyalty Members]&quot; schema) and their favorite hotels (defined in a &quot;[!DNL Hotels]&quot; schema).

Schemabeziehungen werden durch ein **Quellschema** mit einem Feld dargestellt, das auf ein anderes Feld innerhalb eines **Zielschemas** verweist. In the steps that follow, &quot;[!DNL Loyalty Members]&quot; will be the source schema, while &quot;[!DNL Hotels]&quot; will act as the destination schema.

>[!IMPORTANT] Um eine Beziehung herzustellen, müssen beide Schema über definierte primäre Identitäten verfügen und für [!DNL Real-time Customer Profile]die sie aktiviert werden. Informationen zum Konfigurieren Ihrer Schema finden Sie im Abschnitt zum [Aktivieren eines Schemas für die Verwendung in Profil](./create-schema-api.md#profile) im Lernprogramm zur Erstellung von Schemas.

Um eine Beziehung zwischen zwei Schemas festzulegen, müssen Sie sich zunächst die `$id`-Werte für beide Schemas verschaffen. If you know the display names (`title`) of the schemas, you can find their `$id` values by making a GET request to the `/tenant/schemas` endpoint in the [!DNL Schema Registry] API.

**API-Format**

```http
GET /tenant/schemas
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>The [!DNL Accept] header `application/vnd.adobe.xed-id+json` returns only the titles, IDs, and versions of the resulting schemas.

**Antwort**

Bei einer erfolgreichen Antwort wird eine Liste der von Ihrer Organisation definierten Schemas zurückgegeben, einschließlich der Werte für `name`, `$id`, `meta:altId` und `version`.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

Notieren Sie sich die `$id`-Werte der beiden Schemas, für die Sie eine Beziehung definieren möchten. Diese Werte werden in späteren Schritten verwendet.

## Definieren eines Referenzfelds für das Quell-Schema

Within the [!DNL Schema Registry], relationship descriptors work similarly to foreign keys in relational database tables: a field in the source schema acts as a reference to the **primary identity** field of a destination schema. Wenn Ihr Quellfeld zu diesem Zweck nicht über ein Schema verfügt, müssen Sie eventuell eine Mischung mit dem neuen Feld erstellen und es dem Schema hinzufügen. This new field must have a `type` value of &quot;[!DNL string]&quot;.

>[!IMPORTANT]
>
>Im Gegensatz zum Ziel-Schema kann das source-Schema seine primäre Identität nicht als Referenzfeld verwenden.

In diesem Lernprogramm enthält das Ziel-Schema &quot;[!DNL Hotels]&quot;ein `email` Feld, das als primäre Identität des Schemas dient und daher auch als Referenzfeld fungiert. Das Quellfeld &quot;[!DNL Loyalty Members]&quot;verfügt jedoch nicht über ein dediziertes Schema, das als Referenz verwendet werden soll, und muss eine neue Mischung erhalten, die dem Schema ein neues Feld hinzufügt: `favoriteHotel`.

>[!NOTE] Wenn Ihr Quellfeld bereits über ein dediziertes Schema verfügt, das Sie als Referenzfeld verwenden möchten, können Sie den Schritt zum [Erstellen eines Referenzdeskriptors](#reference-identity)überspringen.

### Neues Mixin erstellen

Um einem Schema ein neues Feld hinzuzufügen, muss das Feld zunächst in einem Mixin definiert werden. Sie können ein neues Mixin einrichten, indem Sie eine POST-Anfrage an den `/tenant/mixins`-Endpunkt senden.

**API-Format**

```http
POST /tenant/mixins
```

**Anfrage**

Die folgende Anfrage erstellt ein neues Mixin, das ein `favoriteHotel`-Feld unter dem Namespace `_{TENANT_ID}` eines beliebigen Schemas hinzufügt, dem es hinzugefügt wird.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Mixins zurück.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
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
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `$id` | Die schreibgeschützte, vom System erzeugte eindeutige Kennung des neuen Mixins. Erhält die Form eines URI. |

Notieren Sie den `$id`-URI des Mixins, der im nächsten Schritt beim Hinzufügen des Mixins zum Quellschema verwendet werden wird.

### Mixin dem Quellschema hinzufügen

Nachdem Sie ein Mixin erstellt haben, können Sie es dem Quellschema hinzufügen, indem Sie eine PATCH-Anfrage an den `/tenant/schemas/{SCHEMA_ID}`-Endpunkt senden.

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id`-URI oder die `meta:altId` des Quellschemas. |

**Anfrage**

Die folgende Anforderung fügt das &quot;[!DNL Favorite Hotel]&quot; mixin dem &quot;[!DNL Loyalty Members]&quot;-Schema hinzu.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `op` | Der auszuführende PATCH-Vorgang. Diese Anfrage verwendet den `add`-Vorgang. |
| `path` | Der Pfad zum Schemafeld, in dem die neue Ressource hinzugefügt wird. Beim Hinzufügen von Mixins zu Schemas muss der Wert &quot;/allOf/-&quot;lauten. |
| `value.$ref` | Die `$id` des hinzuzufügenden Mixins. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Schemas zurück, das jetzt den `$ref`-Wert des hinzugefügten Mixins unter seinem `allOf`-Array enthält.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{IMS_ORG}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## Referenzidentitätsdeskriptor erstellen {#reference-identity}

Auf Schemafelder muss ein Referenzidentitätsdeskriptor angewendet werden, wenn sie als Referenz aus anderen Schemas in einer Beziehung verwendet werden. Since the `favoriteHotel` field in &quot;[!DNL Loyalty Members]&quot; will refer to the `email` field in &quot;[!DNL Hotels]&quot;, `email` must be given a reference identity descriptor.

Erstellen Sie einen Referenzdeskriptor für das Zielschema, indem Sie eine POST-Anfrage an den `/tenant/descriptors`-Endpunkt senden.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

The following request creates a reference descriptor for the `email` field in the destination schema &quot;[!DNL Hotels]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email"
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu definierenden Deskriptors. Bei Referenzdeskriptoren muss der Wert &quot;xdm:descriptorReferenceIdentity&quot;lauten. |
| `xdm:sourceSchema` | Die `$id`-URL des Zielschemas. |
| `xdm:sourceVersion` | Die Versionsnummer des Zielschemas. |
| `sourceProperty` | Der Pfad zum primären Identitätsfeld des Zielschemas. |
| `xdm:identityNamespace` | Der Identitäts-Namespace des Referenzfelds. Hierbei muss es sich um denselben Namensraum handeln, der beim Definieren des Felds als primäre Identität des Schemas verwendet wird. Weiterführende Informationen dazu finden Sie unter [Übersicht zu Identitäts-Namespaces](../../identity-service/home.md). |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Referenzdeskriptors für das Zielschema zurück.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Beziehungsdeskriptor erstellen {#create-descriptor}

Beziehungsdeskriptoren stellen eine Eins-zu-Eins-Beziehung zwischen einem Quellschema und einem Zielschema her. Nachdem Sie einen Referenz-Deskriptor für das Ziel-Schema definiert haben, können Sie einen neuen Beziehungsdeskriptor erstellen, indem Sie eine POST-Anforderung an den `/tenant/descriptors` Endpunkt senden.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

The following request creates a new relationship descriptor, with &quot;[!DNL Loyalty Members]&quot; as the source schema and &quot;[!DNL Legacy Loyalty Members]&quot; as the destination schema.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/email"
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu erstellenden Deskriptors. The `@type` value for relationship descriptors is &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | Die `$id`-URL des Quellschemas. |
| `xdm:sourceVersion` | Die Versionsnummer des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zum Referenzfeld im Quell-Schema. |
| `xdm:destinationSchema` | Die `$id`-URL des Zielschemas. |
| `xdm:destinationVersion` | Die Versionsnummer des Zielschemas. |
| `xdm:destinationProperty` | Der Pfad zum Referenzfeld im Ziel-Schema. |

### Antwort

Eine erfolgreiche Antwort gibt die Details des neu erstellten Beziehungsdeskriptors zurück.

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## Nächste Schritte

Durch Befolgung dieses Tutorials haben Sie erfolgreich eine Eins-zu-Eins-Beziehung zwischen zwei Schemas erstellt. For more information on working with descriptors using the [!DNL Schema Registry] API, see the [Schema Registry developer guide](../api/descriptors.md). Anweisungen zum Definieren von Schemabeziehungen in der Benutzeroberfläche finden Sie im Tutorial zum [Definieren von Schemabeziehungen mit dem Schema-Editor](relationship-ui.md).
