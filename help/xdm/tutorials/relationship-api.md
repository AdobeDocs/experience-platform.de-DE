---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beziehung zwischen zwei Schemas mithilfe der Schemaregistrierungs-API definieren
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 84%

---


# Define a relationship between two schemas using the [!DNL Schema Registry] API


Die Fähigkeit, Beziehungen zwischen Ihren Kunden und ihren Interaktionen mit Ihrer Marke über verschiedene Kanäle hinweg zu verstehen, ist ein wichtiger Bestandteil von Adobe Experience Platform. Defining these relationships within the structure of your [!DNL Experience Data Model] (XDM) schemas allows you to gain complex insights into your customer data.

This document provides a tutorial for defining a one-to-one relationship between two schemas defined by your organization using the [!DNL Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Erste Schritte

Dieses Tutorial erfordert ein funktionierendes Verständnis von [!DNL Experience Data Model] (XDM) und [!DNL XDM System]. Bevor Sie mit dieser Anleitung beginnen, lesen Sie folgende Dokumente:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und seine Implementierung in Experience Platform.
   * [Grundlagen der Schemakomposition](../schema/composition.md): Eine Einführung in die Bausteine von XDM-Schemas.
* [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Als Vorbereitung für dieses Tutorial sollten Sie im [Entwicklerhandbuch](../api/getting-started.md) die wichtigsten Themen rund um die konkrete Vorgehensweise für Aufrufe der API durchgehen. [!DNL Schema Registry] Dazu gehören Ihre `{TENANT_ID}`, das Konzept von „Containern“ sowie die erforderlichen Kopfzeilen zum Stellen von Anfragen (mit besonderem Schwerpunkt auf der Accept-Kopfzeile und ihren möglichen Werten).

## Quell- und Zielschema definieren {#define-schemas}

Wir gehen davon aus, dass Sie die beiden Schemas, die in der Beziehung definiert werden sollen, bereits erstellt haben. In diesem Tutorial wird eine Beziehung zwischen Mitgliedern des aktuellen Treueprogramms einer Organisation (definiert in einem Schema namens „Mitglieder im Treueprogramm“) und ihren Lieblingshotels (definiert in einem Schema namens „Hotels“) eingerichtet.

Schemabeziehungen werden durch ein **[!UICONTROL Quellschema]** mit einem Feld dargestellt, das auf ein anderes Feld innerhalb eines **[!UICONTROL Zielschemas]** verweist. In the steps that follow, &quot;[!UICONTROL Loyalty Members]&quot; will be the source schema, while &quot;[!UICONTROL Hotels]&quot; will act as the destination schema.

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
>Die Accept-Kopfzeile `application/vnd.adobe.xed-id+json` gibt nur die Bezeichnungen, Kennungen und Versionen der resultierenden Schemas zurück.

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

## Referenzfelder für beide Schemas definieren

Within the [!DNL Schema Registry], relationship descriptors work similarly to foreign keys in SQL tables: a field in the source schema acts as a reference to a field of a destination schema. Beim Definieren einer Beziehung muss jedes Schema über ein dediziertes Feld verfügen, das als Verweis auf das andere Schema dienen soll.

>[!IMPORTANT]
>
>If the schemas are to be enabled for use in [!DNL Real-time Customer Profile](../../profile/home.md), the reference field for the destination schema must be its **[!UICONTROL primary identity]**. Dieser Aspekt wird im Tutorial später noch ausführlicher erläutert.

Wenn eines der Schemas über kein Feld zu diesem Zweck verfügt, müssen Sie eventuell ein Mixin mit dem neuen Feld erstellen und dem Schema hinzufügen. Dieses neue Feld muss den `type`-Wert „string“ (Zeichenfolge) aufweisen.

Im Rahmen des Tutorials enthält das Zielschema „Hotels“ bereits ein Feld zu diesem Zweck: `hotelId`. Das Quellschema „Mitglieder im Treueprogramm“ hat jedoch kein solches Feld und muss ein neues Mixin erhalten, das ein neues Feld `favoriteHotel` hinzufügt, und zwar unter seinem Namespace `TENANT_ID`.

### Neues Mixin erstellen

Um einem Schema ein neues Feld hinzuzufügen, muss das Feld zunächst in einem Mixin definiert werden. Sie können ein neues Mixin einrichten, indem Sie eine POST-Anfrage an den `/tenant/mixins`-Endpunkt senden.

**API-Format**

```http
POST /tenant/mixins
```

**Anfrage**

Die folgende Anfrage erstellt ein neues Mixin, das ein `favoriteHotel`-Feld unter dem Namespace `TENANT_ID` eines beliebigen Schemas hinzufügt, dem es hinzugefügt wird.

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

Mit der folgenden Anfrage wird das Mixin „Lieblingshotel“ zum Schema „Mitglieder im Treueprogramm“ hinzugefügt.

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
| `path` | Der Pfad zum Schemafeld, in dem die neue Ressource hinzugefügt wird. Beim Hinzufügen von Mixins zu Schemas muss der Wert `/allOf/-`lauten. |
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

## Primäre Identitätsfelder für beide Schemas definieren

>[!NOTE]
>
>This step is only required for schemas that will be enabled for use in [!DNL Real-time Customer Profile](../../profile/home.md). Wenn Sie nicht möchten, dass eines der Schemas Teil einer Vereinigung wird, oder Ihre Schemas bereits über primäre Identitäten verfügen, können Sie den nächsten Schritt zum [Erstellen eines Referenzidentitätsdeskriptors](#create-descriptor) für das Zielschema überspringen.

In order for schemas to be enabled for use in [!DNL Real-time Customer Profile], they must have a primary identity defined. Darüber hinaus muss das Zielschema einer Beziehung seine primäre Identität als Referenzfeld nutzen.

Für dieses Tutorial verfügt das Quellschema bereits über eine definierte primäre Identität, das Zielschema jedoch noch nicht. Sie können ein Schemafeld als primäres Identitätsfeld markieren, indem Sie einen Identitätsdeskriptor erstellen. Senden Sie dazu eine POST-Anfrage an den `/tenant/descriptors`-Endpunkt.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Mit der folgenden Anfrage wird ein neuer Identitätsdeskriptor erstellt, der das `hotelId`-Feld des Zielschemas „Hotels“ als primäres Identitätsfeld festlegt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu erstellenden Deskriptors. Der `@type`-Wert für Identitätsdeskriptoren lautet `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | Der `$id`-Wert des Zielschemas, erhalten im [vorherigen Schritt](#define-schemas). |
| `xdm:sourceVersion` | Die Versionsnummer des Schemas. |
| `sourceProperty` | Der Pfad zum jeweiligen Feld, das als primäre Identität des Schemas dienen wird. Dieser Pfad muss mit einem „/“-Zeichen beginnen und darf nicht auf ein „/“-Zeichen enden. Außerdem müssen alle „properties“-Namespaces ausgeschlossen werden. Die Anfrage oben nutzt zum Beispiel `/_{TENANT_ID}/hotelId` anstelle von `/properties/_{TENANT_ID}/properties/hotelId`. |
| `xdm:namespace` | Der Identitäts-Namespace für das Identitätsfeld. `hotelId` ist in diesem Beispiel ein ECID-Wert; daher wird der Namespace „ECID“ verwendet. Eine Liste der verfügbaren Namespaces finden Sie in der [Übersicht zu Identitäts-Namespaces](../../identity-service/home.md). |
| `xdm:isPrimary` | Eine boolesche Eigenschaft, die darüber bestimmt, ob das Identitätsfeld als primäre Identität für das Schema dienen soll. Da diese Anfrage eine primäre Identität definiert, wird der Wert auf „true“ gesetzt. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Identitätsdeskriptors zurück.

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## Referenzidentitätsdeskriptor erstellen

Auf Schemafelder muss ein Referenzidentitätsdeskriptor angewendet werden, wenn sie als Referenz aus anderen Schemas in einer Beziehung verwendet werden. Da das Feld `favoriteHotel` in „Mitglieder im Treueprogramm“ auf das Feld `hotelId` in „Hotels“ verweisen wird, muss `hotelId` einen Referenzidentitätsdeskriptor erhalten.

Erstellen Sie einen Referenzdeskriptor für das Zielschema, indem Sie eine POST-Anfrage an den `/tenant/descriptors`-Endpunkt senden.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anfrage erstellt einen Referenzdeskriptor für das `hotelId`-Feld im Zielschema „Hotels“.

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
    "xdm:identityNamespace": "ECID"
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `xdm:sourceSchema` | Die `$id`-URL des Zielschemas. |
| `xdm:sourceVersion` | Die Versionsnummer des Zielschemas. |
| `sourceProperty` | Der Pfad zum primären Identitätsfeld des Zielschemas. |
| `xdm:identityNamespace` | Der Identitäts-Namespace des Referenzfelds. `hotelId` ist in diesem Beispiel ein ECID-Wert; daher wird der Namespace „ECID“ verwendet. Eine Liste der verfügbaren Namespaces finden Sie in der [Übersicht zu Identitäts-Namespaces](../../identity-service/home.md). |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Referenzdeskriptors für das Zielschema zurück.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Beziehungsdeskriptor erstellen {#create-descriptor}

Beziehungsdeskriptoren stellen eine Eins-zu-Eins-Beziehung zwischen einem Quellschema und einem Zielschema her. Sie können einen neuen Beziehungsdeskriptor erstellen, indem Sie eine POST-Anfrage an den `/tenant/descriptors`-Endpunkt senden.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Mit der folgenden Anfrage wird ein neuer Beziehungsdeskriptor erstellt, wobei „Mitglieder im Treueprogramm“ als Quellschema und „Alte Mitglieder im Treueprogramm“ als Zielschema dienen.

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
| `@type` | Der Typ des zu erstellenden Deskriptors. Der `@type`-Wert für Beziehungsdeskriptoren lautet `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | Die `$id`-URL des Quellschemas. |
| `xdm:sourceVersion` | Die Versionsnummer des Quellschemas. |
| `sourceProperty`: | Der Pfad zum Referenzfeld im Quellschema. |
| `xdm:destinationSchema` | Die `$id`-URL des Zielschemas. |
| `xdm:destinationVersion` | Die Versionsnummer des Zielschemas. |
| `destinationProperty`: | Der Pfad zum Referenzfeld im Zielschema. |

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

Durch Befolgung dieses Tutorials haben Sie erfolgreich eine Eins-zu-Eins-Beziehung zwischen zwei Schemas erstellt. For more information on working with descriptors using the [!DNL Schema Registry] API, see the [Schema Registry developer guide](../api/getting-started.md). Anweisungen zum Definieren von Schemabeziehungen in der Benutzeroberfläche finden Sie im Tutorial zum [Definieren von Schemabeziehungen mit dem Schema-Editor](relationship-ui.md).