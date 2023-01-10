---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schemaregistrierung; Schema; Schema; Schemas; Beziehung; Beziehung; Beziehungsdeskriptor; Beziehungsdeskriptor; Referenzidentität; Referenzidentität; Referenzidentität
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe der Schema Registry-API
description: Dieses Dokument bietet eine Anleitung zum Definieren einer Eins-zu-Eins-Beziehung zwischen zwei Schemas, die von Ihrer Organisation mithilfe der Schema Registry-API definiert wurden.
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 32%

---

# Definieren Sie mithilfe der [!DNL Schema Registry] API

Die Möglichkeit, Beziehungen zwischen Ihren Kunden und deren Interaktionen mit Ihrer Marke kanalübergreifend zu analysieren, ist ein wichtiger Bestandteil von Adobe Experience Platform. Definieren dieser Beziehungen innerhalb der Struktur Ihrer [!DNL Experience Data Model] (XDM)-Schemas ermöglichen es Ihnen, komplexe Einblicke in Ihre Kundendaten zu erhalten.

Während Schemabeziehungen durch die Verwendung des Vereinigungsschemas und [!DNL Real-Time Customer Profile], gilt dies nur für Schemas, die dieselbe Klasse teilen. Um eine Beziehung zwischen zwei Schemas herzustellen, die zu verschiedenen Klassen gehören, muss einem Quellschema ein dediziertes Beziehungsfeld hinzugefügt werden, das auf die Identität eines Zielschemas verweist.

Dieses Dokument enthält eine Anleitung zum Definieren einer Eins-zu-Eins-Beziehung zwischen zwei Schemas, die von Ihrer Organisation mithilfe der [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis von [!DNL Experience Data Model] (XDM) und [!DNL XDM System]. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und dessen Implementierung in [!DNL Experience Platform].
   * [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemas.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die [Entwicklerhandbuch](../api/getting-started.md) für wichtige Informationen, die Sie benötigen, um erfolgreich Aufrufe an die [!DNL Schema Registry] API. Dies umfasst Ihre `{TENANT_ID}`, das Konzept der &quot;Container&quot;und die erforderlichen Kopfzeilen für Anfragen (mit besonderem Augenmerk auf die [!DNL Accept] -Kopfzeile und die möglichen Werte).

## Quell- und Zielschemas definieren {#define-schemas}

Wir gehen davon aus, dass Sie die beiden Schemas, die in der Beziehung definiert werden sollen, bereits erstellt haben. In diesem Tutorial wird eine Beziehung zwischen Mitgliedern des aktuellen Treueprogramms einer Organisation (definiert in einem[!DNL Loyalty Members]&quot; schema) und ihren Lieblingshotels (definiert in einem &quot;[!DNL Hotels]&quot; schema).

Schemabeziehungen werden durch ein **Quellschema** mit einem Feld dargestellt, das auf ein anderes Feld innerhalb eines **Zielschemas** verweist. In den folgenden Schritten: &quot;[!DNL Loyalty Members]&quot; wird das Quellschema sein, während &quot;[!DNL Hotels]&quot; dient als Zielschema.

>[!IMPORTANT]
>
>Um eine Beziehung herzustellen, müssen beide Schemas definierte primäre Identitäten aufweisen und für [!DNL Real-Time Customer Profile]. Siehe Abschnitt zu [Aktivieren eines Schemas zur Verwendung in Profil](./create-schema-api.md#profile) im Tutorial zur Erstellung von Schemas , wenn Sie Anleitungen zur entsprechenden Konfiguration Ihrer Schemas benötigen.

Um eine Beziehung zwischen zwei Schemas festzulegen, müssen Sie sich zunächst die `$id`-Werte für beide Schemas verschaffen. Wenn Sie die Anzeigenamen kennen (`title`) der Schemas, können Sie ihre `$id` -Werte, indem Sie eine GET-Anfrage an die `/tenant/schemas` -Endpunkt im [!DNL Schema Registry] API.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>Die [!DNL Accept] header `application/vnd.adobe.xed-id+json` gibt nur die Titel, IDs und Versionen der resultierenden Schemas zurück.

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

## Referenzfeld für das Quellschema definieren

Innerhalb der [!DNL Schema Registry], funktionieren Beziehungsdeskriptoren ähnlich wie Fremdschlüssel in relationalen Datenbanktabellen: Ein Feld im Quellschema dient als Verweis auf das primäre Identitätsfeld eines Zielschemas. Wenn Ihr Quellschema über kein Feld zu diesem Zweck verfügt, müssen Sie möglicherweise eine Schemafeldergruppe mit dem neuen Feld erstellen und zum Schema hinzufügen. Dieses neue Feld muss eine `type` Wert von `string`.

>[!IMPORTANT]
>
>Das Quellschema kann seine primäre Identität nicht als Referenzfeld verwenden.

In diesem Tutorial wurde das Zielschema &quot;[!DNL Hotels]&quot; enthält ein `hotelId` -Feld, das als primäre Identität des Schemas dient. Das Quellschema &quot;[!DNL Loyalty Members]&quot; verfügt nicht über ein dediziertes Feld, das als Verweis auf `hotelId`und daher muss eine benutzerdefinierte Feldergruppe erstellt werden, um dem Schema ein neues Feld hinzuzufügen: `favoriteHotel`.

>[!NOTE]
>
>Wenn Ihr Quellschema bereits über ein dediziertes Feld verfügt, das Sie als Referenzfeld verwenden möchten, können Sie den Schritt zum [Erstellen eines Referenzdeskriptors](#reference-identity).

### Neue Feldergruppe erstellen

Um einem Schema ein neues Feld hinzuzufügen, muss es zunächst in einer Feldergruppe definiert werden. Sie können eine neue Feldergruppe erstellen, indem Sie eine POST-Anfrage an die `/tenant/fieldgroups` -Endpunkt.

**API-Format**

```http
POST /tenant/fieldgroups
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Feldergruppe, die eine `favoriteHotel` Feld unter `_{TENANT_ID}` -Namespace eines beliebigen Schemas, dem es hinzugefügt wird.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
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

Eine erfolgreiche Antwort gibt die Details der neu erstellten Feldergruppe zurück.

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
    "description": "Favorite hotel field group for the Loyalty Members schema.",
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
| `$id` | Die schreibgeschützte, vom System generierte eindeutige Kennung der neuen Feldergruppe. Erhält die Form eines URI. |

{style=&quot;table-layout:auto&quot;}

Notieren Sie die `$id` URI der Feldergruppe, die im nächsten Schritt beim Hinzufügen der Feldergruppe zum Quellschema verwendet wird.

### Hinzufügen der Feldergruppe zum Quellschema

Nachdem Sie eine Feldergruppe erstellt haben, können Sie sie dem Quellschema hinzufügen, indem Sie eine PATCH-Anfrage an die `/tenant/schemas/{SCHEMA_ID}` -Endpunkt.

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id`-URI oder `meta:altId` des Quellschemas. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage fügt die[!DNL Favorite Hotel]&quot; Feldergruppe zu &quot;[!DNL Loyalty Members]&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | Der Pfad zum Schemafeld, in dem die neue Ressource hinzugefügt wird. Beim Hinzufügen von Feldergruppen zu Schemas muss der Wert &quot;/allOf/-&quot;lauten. |
| `value.$ref` | Die `$id` der Feldergruppe, die hinzugefügt werden soll. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Schemas zurück, das jetzt die `$ref` Wert der hinzugefügten Feldergruppe unter `allOf` Array.

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
    "imsOrg": "{ORG_ID}",
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

Auf Schemafelder muss ein Referenzidentitätsdeskriptor angewendet werden, wenn sie als Verweis auf ein anderes Schema in einer Beziehung verwendet werden. Seit `favoriteHotel` -Feld in[!DNL Loyalty Members]&quot; bezieht sich auf die `hotelId` -Feld in[!DNL Hotels]&quot;, `favoriteHotel` muss einen Referenzidentitätsdeskriptor erhalten.

Erstellen Sie einen Referenzdeskriptor für das Quellschema, indem Sie eine POST-Anfrage an die `/tenant/descriptors` -Endpunkt.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anfrage erstellt einen Referenzdeskriptor für die `favoriteHotel` -Feld im Quellschema &quot;[!DNL Loyalty Members]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu definierenden Deskriptors. Für Referenzdeskriptoren muss der Wert `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | Die `$id`-URL des Quellschemas. |
| `xdm:sourceVersion` | Die Versionsnummer des Quellschemas. |
| `sourceProperty` | Der Pfad zum Feld im Quellschema, das verwendet wird, um auf die primäre Identität des Zielschemas zu verweisen. |
| `xdm:identityNamespace` | Der Identitäts-Namespace des Referenzfelds. Dieser Namespace muss mit der primären Identität des Zielschemas übereinstimmen. Weiterführende Informationen dazu finden Sie unter [Übersicht zu Identitäts-Namespaces](../../identity-service/home.md). |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Referenzdeskriptors für das Quellfeld zurück.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Beziehungsdeskriptor erstellen {#create-descriptor}

Beziehungsdeskriptoren stellen eine Eins-zu-Eins-Beziehung zwischen einem Quellschema und einem Zielschema her. Nachdem Sie einen Referenzidentitätsdeskriptor für das entsprechende Feld im Quellschema definiert haben, können Sie einen neuen Beziehungsdeskriptor erstellen, indem Sie eine POST-Anfrage an die `/tenant/descriptors` -Endpunkt.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anfrage erstellt einen neuen Beziehungsdeskriptor mit &quot;[!DNL Loyalty Members]&quot; als Quellschema und &quot;[!DNL Hotels]&quot; als Zielschema.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu erstellenden Deskriptors. Der `@type`-Wert für Beziehungsdeskriptoren lautet `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | Die `$id`-URL des Quellschemas. |
| `xdm:sourceVersion` | Die Versionsnummer des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zum Referenzfeld im Quellschema. |
| `xdm:destinationSchema` | Die `$id`-URL des Zielschemas. |
| `xdm:destinationVersion` | Die Versionsnummer des Zielschemas. |
| `xdm:destinationProperty` | Der Pfad zum primären Identitätsfeld im Zielschema. |

{style=&quot;table-layout:auto&quot;}

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

Durch Befolgung dieses Tutorials haben Sie erfolgreich eine Eins-zu-Eins-Beziehung zwischen zwei Schemas erstellt. Weitere Informationen zum Arbeiten mit Deskriptoren unter Verwendung der [!DNL Schema Registry] API, siehe [Entwicklerhandbuch zur Schema Registry](../api/descriptors.md). Anweisungen zum Definieren von Schemabeziehungen in der Benutzeroberfläche finden Sie im Tutorial zum [Definieren von Schemabeziehungen mit dem Schema-Editor](relationship-ui.md).
