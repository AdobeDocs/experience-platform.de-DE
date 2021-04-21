---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;Schema;Schema;Schema;Beziehung;Beziehung;Beziehungsdeskriptor;Beziehungsdeskriptor;Referenzidentität;Referenzidentität;
solution: Experience Platform
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe der Schema Registry API
description: Dieses Dokument bietet eine Anleitung zum Definieren einer Eins-zu-Eins-Beziehung zwischen zwei Schemas, die von Ihrer Organisation mithilfe der Schema Registry-API definiert wurden.
topic-legacy: tutorial
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 45%

---

# Definieren einer Beziehung zwischen zwei Schemas mithilfe der API[!DNL Schema Registry]

Die Möglichkeit, Beziehungen zwischen Ihren Kunden und deren Interaktionen mit Ihrer Marke kanalübergreifend zu analysieren, ist ein wichtiger Bestandteil von Adobe Experience Platform. Durch die Definition dieser Beziehungen innerhalb der Struktur Ihrer [!DNL Experience Data Model] (XDM) Schema erhalten Sie komplexe Einblicke in Ihre Kundendaten.

Während Schema-Beziehungen durch die Verwendung des Vereinigung-Schemas und [!DNL Real-time Customer Profile] abgeleitet werden können, gilt dies nur für Schema, die dieselbe Klasse gemeinsam haben. Zur Herstellung einer Beziehung zwischen zwei Schemas, die zu verschiedenen Klassen gehören, muss einem Quell-Schema ein dediziertes Beziehungsfeld hinzugefügt werden, das auf die Identität eines Ziel-Schemas verweist.

Dieses Dokument bietet eine Anleitung zum Definieren einer Eins-zu-Eins-Beziehung zwischen zwei Schemas, die von Ihrem Unternehmen mithilfe von [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) definiert werden.

## Erste Schritte

Dieses Lernprogramm erfordert ein Arbeitsverständnis von [!DNL Experience Data Model] (XDM) und [!DNL XDM System]. Bevor Sie mit dem Tutorial beginnen, lesen Sie die folgenden Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und seine Implementierung in  [!DNL Experience Platform].
   * [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemas.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte das [Entwicklerhandbuch](../api/getting-started.md), um wichtige Informationen zu erhalten, die Sie kennen müssen, damit Sie erfolgreich Aufrufe an die [!DNL Schema Registry]-API tätigen können. Dazu gehören Ihre `{TENANT_ID}`, das Konzept der &quot;Container&quot;und die erforderlichen Kopfzeilen für die Anforderung (mit besonderer Aufmerksamkeit für die [!DNL Accept]-Kopfzeile und deren mögliche Werte).

## Quell- und Zielschema definieren {#define-schemas}

Wir gehen davon aus, dass Sie die beiden Schemas, die in der Beziehung definiert werden sollen, bereits erstellt haben. Dieses Lernprogramm erstellt eine Beziehung zwischen Mitgliedern des aktuellen Loyalitätshotels (definiert in einem Schema &quot;[!DNL Loyalty Members]&quot;) und ihren Lieblingshotels (definiert in einem Schema &quot;[!DNL Hotels]&quot;).

Schemabeziehungen werden durch ein **Quellschema** mit einem Feld dargestellt, das auf ein anderes Feld innerhalb eines **Zielschemas** verweist. In den folgenden Schritten ist &quot;[!DNL Loyalty Members]&quot;das Quell-Schema, während &quot;[!DNL Hotels]&quot;als Ziel-Schema fungiert.

>[!IMPORTANT]
>
>Um eine Beziehung herzustellen, müssen beide Schema definierte primäre Identitäten haben und für [!DNL Real-time Customer Profile] aktiviert sein. Informationen zum Konfigurieren Ihrer Schema finden Sie im Abschnitt [Aktivieren eines Schemas zur Verwendung in Profil](./create-schema-api.md#profile) im Lernprogramm zur Erstellung von Schemas.

Um eine Beziehung zwischen zwei Schemas festzulegen, müssen Sie sich zunächst die `$id`-Werte für beide Schemas verschaffen. Wenn Sie die Anzeigenamen (`title`) der Schema kennen, können Sie ihre `$id`-Werte finden, indem Sie eine GET an den `/tenant/schemas`-Endpunkt in der [!DNL Schema Registry]-API anfordern.

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
>Die [!DNL Accept]-Kopfzeile `application/vnd.adobe.xed-id+json` gibt nur die Titel, IDs und Versionen der resultierenden Schema zurück.

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

Innerhalb der [!DNL Schema Registry] funktionieren Beziehungsdeskriptoren ähnlich wie Fremdschlüssel in relationalen Datenbanktabellen: ein Feld im Quell-Schema als Verweis auf das primäre Identitätsfeld eines Schemas dient. Wenn Ihr Quellfeld zu diesem Zweck nicht über ein Schema verfügt, müssen Sie eventuell eine Mischung mit dem neuen Feld erstellen und es dem Schema hinzufügen. Dieses neue Feld muss den Wert `type` von &quot;[!DNL string]&quot;haben.

>[!IMPORTANT]
>
>Im Gegensatz zum Ziel-Schema kann das source-Schema seine primäre Identität nicht als Referenzfeld verwenden.

In diesem Lernprogramm enthält das Zielfeld &quot;[!DNL Hotels]&quot;ein `hotelId`-Schema, das als primäre Identität des Schemas dient und daher auch als Referenzfeld dient. Das Quellfeld &quot;[!DNL Loyalty Members]&quot;verfügt jedoch nicht über ein dediziertes Schema, das als Referenz verwendet werden kann, und muss eine neue Mixin erhalten, die dem Schema ein neues Feld hinzufügt: `favoriteHotel`.

>[!NOTE]
>
>Wenn Ihr Quell-Schema bereits über ein dediziertes Feld verfügt, das Sie als Referenzfeld verwenden möchten, können Sie mit dem Schritt [Erstellen eines Referenzdeskriptors](#reference-identity) fortfahren.

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
| `{SCHEMA_ID}` | Der URL-kodierte `$id`-URI oder `meta:altId` des Quellschemas. |

**Anfrage**

Mit der folgenden Anforderung wird das Mixin &quot;[!DNL Favorite Hotel]&quot;zum Schema &quot;[!DNL Loyalty Members]&quot;hinzugefügt.

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

Auf Schemafelder muss ein Referenzidentitätsdeskriptor angewendet werden, wenn sie als Referenz aus anderen Schemas in einer Beziehung verwendet werden. Da das `favoriteHotel`-Feld in &quot;[!DNL Loyalty Members]&quot;auf das `hotelId`-Feld in &quot;[!DNL Hotels]&quot;verweist, muss `hotelId` ein Referenz-Identitätsdeskriptor erhalten werden.

Erstellen Sie einen Referenzdeskriptor für das Zielschema, indem Sie eine POST-Anfrage an den `/tenant/descriptors`-Endpunkt senden.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anforderung erstellt einen Referenz-Deskriptor für das Feld `hotelId` im Schema &quot;Ziel&quot;[!DNL Hotels]&quot;.

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
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID"
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
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Beziehungsdeskriptor erstellen {#create-descriptor}

Beziehungsdeskriptoren stellen eine Eins-zu-Eins-Beziehung zwischen einem Quellschema und einem Zielschema her. Nachdem Sie einen Referenz-Deskriptor für das Ziel-Schema definiert haben, können Sie einen neuen Beziehungsdeskriptor erstellen, indem Sie eine POST an den `/tenant/descriptors`-Endpunkt anfordern.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Beziehungsdeskriptor mit &quot;[!DNL Loyalty Members]&quot;als Quellcode-Schema und &quot;[!DNL Legacy Loyalty Members]&quot;als Zielziel-Schema erstellt.

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
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu erstellenden Deskriptors. Der `@type`-Wert für Beziehungsdeskriptoren ist &quot;xdm:descriptorOneToOne&quot;. |
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

Durch Befolgung dieses Tutorials haben Sie erfolgreich eine Eins-zu-Eins-Beziehung zwischen zwei Schemas erstellt. Weitere Informationen zum Arbeiten mit Deskriptoren mit der [!DNL Schema Registry]-API finden Sie im [Schema Registry-Entwicklerhandbuch](../api/descriptors.md). Anweisungen zum Definieren von Schemabeziehungen in der Benutzeroberfläche finden Sie im Tutorial zum [Definieren von Schemabeziehungen mit dem Schema-Editor](relationship-ui.md).
