---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Definieren einer Beziehung zwischen zwei Schemas mithilfe der Schema Registry API
topic: tutorials
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1504'
ht-degree: 1%

---


# Definieren einer Beziehung zwischen zwei Schemas mithilfe der Schema Registry API


Die Fähigkeit, die Beziehungen zwischen Ihren Kunden und ihre Interaktionen mit Ihrer Marke über verschiedene Kanäle hinweg zu verstehen, ist ein wichtiger Bestandteil der Adobe Experience Platform. Die Definition dieser Beziehungen innerhalb der Struktur Ihrer Experience Data Model (XDM)-Schema ermöglicht Ihnen, komplexe Einblicke in Ihre Kundendaten zu erhalten.

Dieses Dokument bietet eine Anleitung zum Definieren einer Eins-zu-Eins-Beziehung zwischen zwei Schemas, die von Ihrem Unternehmen mithilfe der [Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)definiert werden.

## Erste Schritte

Dieses Lernprogramm erfordert ein funktionierendes Verständnis von Experience Data Model (XDM) und XDM System. Bevor Sie dieses Lernprogramm beginnen, lesen Sie bitte die folgende Dokumentation:

* [XDM-System in Experience Platform](../home.md): Eine Übersicht über XDM und seine Implementierung in Experience Platform.
   * [Grundlagen der Zusammensetzung](../schema/composition.md)des Schemas: Eine Einführung in die Bausteine von XDM-Schemas.
* [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Bevor Sie dieses Tutorial starten, lesen Sie bitte das [Entwicklerhandbuch](../api/getting-started.md) , um wichtige Informationen zu erhalten, die Sie benötigen, um die Schema Registry API erfolgreich aufzurufen. Dazu gehören Ihre `{TENANT_ID}`, das Konzept der &quot;Container&quot; und die erforderlichen Kopfzeilen für Anfragen (mit besonderer Aufmerksamkeit für den Accept-Header und seine möglichen Werte).

## Definieren eines Schemas für Quelle und Ziel {#define-schemas}

Es wird erwartet, dass Sie die beiden Schema, die in der Beziehung definiert werden, bereits erstellt haben. Dieses Lernprogramm vermittelt eine Beziehung zwischen Mitgliedern des aktuellen Loyalität-Programms einer Organisation (definiert in einem Schema &quot;Treuemitglieder&quot;) und ihren Lieblingshotels (definiert in einem Schema &quot;Hotels&quot;).

Schema-Beziehungen werden durch ein **Quell-Schema** mit einem Feld dargestellt, das auf ein anderes Feld innerhalb eines **Ziel-Schemas** verweist. In den folgenden Schritten wird &quot;Treuemitglieder&quot;das Schema der Quelle sein, während &quot;Hotels&quot;als Schema des Zielortes fungieren.

Um eine Beziehung zwischen zwei Schemas zu definieren, müssen Sie zunächst die `$id` Werte für beide Schema erfassen. Wenn Sie die Anzeigenamen (`title`) der Schema kennen, können Sie deren `$id` Werte finden, indem Sie eine GET-Anforderung an den `/tenant/schemas` Endpunkt in der Schema-Registrierungs-API stellen.

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
>Die Kopfzeile &quot;Akzeptieren&quot; `application/vnd.adobe.xed-id+json` gibt nur die Titel, IDs und Versionen der resultierenden Schema zurück.

**Antwort**

Bei einer erfolgreichen Antwort wird eine Liste der von Ihrem Unternehmen definierten Schema zurückgegeben, einschließlich ihrer `name`, `$id`, `meta:altId`und `version`.

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

Notieren Sie die `$id` Werte der beiden Schema, zwischen denen Sie eine Beziehung definieren möchten. Diese Werte werden in späteren Schritten verwendet.

## Definieren von Referenzfeldern für beide Schemas

Innerhalb der Schema Registry funktionieren Beziehungsdeskriptoren ähnlich wie Fremdschlüssel in SQL-Tabellen: Ein Feld im Quell-Schema dient als Verweis auf ein Schema eines Ziels. Beim Definieren einer Beziehung muss jedes Schema über ein dediziertes Feld verfügen, das als Verweis auf das andere Schema verwendet werden soll.

>[!IMPORTANT]
>
>Wenn die Schema für die Verwendung im [Echtzeit-Kundenkonto](../../profile/home.md)aktiviert werden sollen, muss das Referenzfeld für das Ziel-Schema seine **primäre Identität** sein. Dies wird später in diesem Tutorial ausführlicher erläutert.

Wenn eines der Schemas zu diesem Zweck über kein Feld verfügt, müssen Sie eventuell eine Mischung mit dem neuen Feld erstellen und es dem Schema hinzufügen. Dieses neue Feld muss den `type` Wert &quot;string&quot;haben.

Im Rahmen dieses Lernprogramms enthält das Schema &quot;Hotels&quot; bereits ein Feld zu diesem Zweck: `hotelId`. Das Quell-Schema &quot;Loyalty Members&quot; hat jedoch kein solches Feld und muss eine neue Mischung erhalten, die ein neues Feld hinzufügt, `favoriteHotel`unter seinem `TENANT_ID` Namensraum.

### Erstellen eines neuen Mixins

Um einem Schema ein neues Feld hinzuzufügen, muss es zunächst in einem Mixin definiert werden. Sie können eine neue Mischung erstellen, indem Sie eine POST-Anforderung an den `/tenant/mixins` Endpunkt senden.

**API-Format**

```http
POST /tenant/mixins
```

**Anfrage**

Die folgende Anforderung erstellt eine neue Mixin, die ein `favoriteHotel` Feld unter dem `TENANT_ID` Namensraum eines Schemas hinzufügt, dem es hinzugefügt wird.

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
| `$id` | Der schreibgeschützte, vom System erzeugte eindeutige Bezeichner des neuen Mixins. Wird in Form eines URIs ausgeführt. |

Notieren Sie den `$id` URI des Mixins, der im nächsten Schritt beim Hinzufügen des mixins zum source-Schema verwendet werden soll.

### Hinzufügen der Mischung mit dem Quellcode-Schema

Nachdem Sie ein Mixin erstellt haben, können Sie es dem Quellcode-Schema hinzufügen, indem Sie eine PATCH-Anforderung an den `/tenant/schemas/{SCHEMA_ID}` Endpunkt senden.

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` das Quell-Schema. |

**Anfrage**

Mit der folgenden Anfrage wird das Mixin &quot;Favorite Hotel&quot;zum Schema &quot;Loyalty Members&quot;hinzugefügt.

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
| `op` | Der auszuführende PATCH-Vorgang. Diese Anforderung verwendet den `add` Vorgang. |
| `path` | Der Pfad zum Schema, in dem die neue Ressource hinzugefügt wird. Beim Hinzufügen von Mixins zu Schemas muss der Wert `/allOf/-`angegeben werden. |
| `value.$ref` | Die `$id` des hinzuzufügenden Mixins. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Schemas zurück, das jetzt den `$ref` Wert des hinzugefügten mixins unter seinem `allOf` Array enthält.

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

## Definieren Sie primäre Identitätsfelder für beide Schema.

>[!NOTE]
>
>Dieser Schritt ist nur für Schema erforderlich, die für die Verwendung im [Echtzeit-Profil](../../profile/home.md)aktiviert werden. Wenn Sie nicht möchten, dass Schema an einer Vereinigung teilnimmt oder wenn Ihre Schema bereits über primäre Identitäten verfügen, können Sie mit dem nächsten Schritt zur [Erstellung eines Referenz-Identitätsdeskriptors](#create-descriptor) für das Ziel-Schema fortfahren.

Damit Schema für die Verwendung im Echtzeit-Profil aktiviert werden können, muss eine primäre Identität definiert sein. Darüber hinaus muss das Ziel-Schema einer Beziehung seine primäre Identität als Referenzfeld verwenden.

Für diese Übung ist bereits eine primäre Schema-ID definiert, das Ziel-Schema jedoch nicht. Sie können ein Schema-Feld als primäres Identitätsfeld markieren, indem Sie einen Identitätsdeskriptor erstellen. Dies geschieht, indem eine POST-Anforderung an den `/tenant/descriptors` Endpunkt gesendet wird.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Identitätsdeskriptor erstellt, der das `hotelId` Feld des Ziel-Schemas &quot;Hotels&quot;als primäres Identitätsfeld definiert.

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
| `@type` | Der Typ des zu erstellenden Deskriptors. Der `@type` Wert für Identitätsdeskriptoren ist `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | Der `$id` Wert des im [vorherigen Schritt](#define-schemas)erhaltenen Zielwerts. |
| `xdm:sourceVersion` | Die Versionsnummer des Schemas. |
| `sourceProperty` | Der Pfad zum jeweiligen Feld, das als primäre Identität des Schemas dient. Dieser Pfad sollte mit einem &quot;/&quot;beginnen und nicht mit einem &quot;/&quot;enden, während auch alle &quot;properties&quot;-Namensraum ausgeschlossen werden. Die oben aufgeführte Anforderung verwendet zum Beispiel `/_{TENANT_ID}/hotelId` anstelle von `/properties/_{TENANT_ID}/properties/hotelId`. |
| `xdm:namespace` | Der Identitäts-Namensraum für das Identitätsfeld. `hotelId` in diesem Beispiel ein ECID-Wert ist, daher wird der Namensraum &quot;ECID&quot;verwendet. Eine Liste der verfügbaren Namensraum finden Sie in der Übersicht über den [Identitäts-Namensraum](../../identity-service/home.md) . |
| `xdm:isPrimary` | Eine boolesche Eigenschaft, die bestimmt, ob das Identitätsfeld die primäre Identität des Schemas sein soll. Da diese Anforderung eine primäre Identität definiert, wird der Wert auf &quot;true&quot;gesetzt. |

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

## Erstellen eines Referenz-Identitätsdeskriptors

Bei Schema-Feldern muss ein Referenz-Identitätsdeskriptor angewendet werden, wenn sie als Referenz aus anderen Schemas in einer Beziehung verwendet werden. Da das `favoriteHotel` Feld in &quot;Treueanwärter&quot; auf das `hotelId` Feld in &quot;Hotels&quot; verweisen wird, muss eine Referenz-Identitätsbeschreibung angegeben `hotelId` werden.

Erstellen Sie einen Referenz-Deskriptor für das Ziel-Schema, indem Sie eine POST-Anforderung an den `/tenant/descriptors` Endpunkt senden.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anforderung erstellt einen Referenz-Deskriptor für das `hotelId` Feld im Ziel-Schema &quot;Hotels&quot;.

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
| `xdm:sourceSchema` | Die `$id` URL des Ziel-Schemas. |
| `xdm:sourceVersion` | Die Versionsnummer des Ziel-Schemas. |
| `sourceProperty` | Der Pfad zum primären Identitätsfeld des Schemas. |
| `xdm:identityNamespace` | Der Identitäts-Namensraum des Referenzfelds. `hotelId` in diesem Beispiel ein ECID-Wert ist, daher wird der Namensraum &quot;ECID&quot;verwendet. Eine Liste der verfügbaren Namensraum finden Sie in der Übersicht über den [Identitäts-Namensraum](../../identity-service/home.md) . |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Referenz-Deskriptors für das Ziel-Schema zurück.

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

## Erstellen eines Beziehungsdeskriptors {#create-descriptor}

Beziehungsdeskriptoren stellen eine Eins-zu-Eins-Beziehung zwischen einem Quell-Schema und einem Ziel-Schema her. Sie können einen neuen Beziehungsdeskriptor erstellen, indem Sie eine POST-Anforderung an den `/tenant/descriptors` Endpunkt senden.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Beziehungsdeskriptor erstellt, bei dem &quot;Treuemitglieder&quot;als Quell-Schema und &quot;Legacy-Treueanwärter&quot;als Zielland-Schema dienen.

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
| `@type` | Der Typ des zu erstellenden Deskriptors. Der `@type` Wert für Beziehungsdeskriptoren ist `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | Die `$id` URL des Quell-Schemas. |
| `xdm:sourceVersion` | Die Versionsnummer des Quell-Schemas. |
| `sourceProperty`: | Der Pfad zum Referenzfeld im Quell-Schema. |
| `xdm:destinationSchema` | Die `$id` URL des Ziel-Schemas. |
| `xdm:destinationVersion` | Die Versionsnummer des Ziel-Schemas. |
| `destinationProperty`: | Der Pfad zum Referenzfeld im Ziel-Schema. |

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

Indem Sie diesem Tutorial folgen, haben Sie erfolgreich eine 1-zu-1-Beziehung zwischen zwei Schemas erstellt. Weitere Informationen zum Arbeiten mit Deskriptoren mit der Schema Registry API finden Sie im Entwicklerhandbuch für die [Schema-Registrierung](../api/getting-started.md). Anweisungen zum Definieren von Schema-Beziehungen in der Benutzeroberfläche finden Sie im Lernprogramm zum [Definieren von Schema-Beziehungen mit dem Schema-Editor](relationship-ui.md).