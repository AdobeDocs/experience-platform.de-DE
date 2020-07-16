---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Ad-hoc-Schemas
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 14%

---


# Erstellen eines Ad-hoc-Schemas

In specific circumstances, it may be necessary to create an [!DNL Experience Data Model] (XDM) schema with fields that are namespaced for usage only by a single dataset. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc schemas are used in various data ingestion workflows for [!DNL Experience Platform], including ingesting CSV files and creating certain kinds of source connections.

In diesem Dokument werden allgemeine Schritte zum Erstellen eines Ad-hoc-Schemas mithilfe der [Schema Registry-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)beschrieben. Es soll zusammen mit anderen [!DNL Experience Platform] Lernprogrammen verwendet werden, für die im Rahmen des Workflows ein Ad-hoc-Schema erstellt werden muss. Jedes dieser Dokumente enthält detaillierte Informationen zur ordnungsgemäßen Konfiguration eines Ad-hoc-Schemas für den jeweiligen Verwendungsfall.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis des [!DNL Experience Data Model] (XDM-)Systems. Bevor Sie dieses Lernprogramm starten, lesen Sie bitte die folgende XDM-Dokumentation:

- [XDM-System - Übersicht](../home.md): Eine allgemeine Übersicht über XDM und seine Implementierung in [!DNL Experience Platform].
- [Grundlagen der Zusammensetzung](../schema/composition.md)des Schemas: Eine Übersicht über die Grundkomponenten von XDM-Schemas.

Als Vorbereitung für dieses Tutorial sollten Sie im [Entwicklerhandbuch](../api/getting-started.md) die wichtigsten Themen rund um die konkrete Vorgehensweise für Aufrufe der API durchgehen. [!DNL Schema Registry] Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.

## Erstellen einer Ad-hoc-Klasse

Das Datenverhalten eines XDM-Schemas wird durch seine zugrunde liegende Klasse bestimmt. Der erste Schritt beim Erstellen eines Ad-hoc-Schemas besteht darin, eine Klasse zu erstellen, die auf dem `adhoc` Verhalten basiert. Senden Sie dazu eine POST-Anfrage an den `/tenant/classes`-Endpunkt.

**API-Format**

```http
POST /tenant/classes
```

**Anfrage**

Die folgende Anforderung erstellt eine neue XDM-Klasse, die von den in der Payload bereitgestellten Attributen konfiguriert wird. Durch die Bereitstellung einer `$ref` Eigenschaft, die auf `https://ns.adobe.com/xdm/data/adhoc` im `allOf` Array festgelegt ist, übernimmt diese Klasse das `adhoc` Verhalten. Die Anforderung definiert auch ein `_adhoc` Objekt, das die benutzerdefinierten Felder für die Klasse enthält.

>[!NOTE]
>
>Die unter definierten benutzerdefinierten Felder `_adhoc` variieren je nach Anwendungsfall des Ad-hoc-Schemas. Bitte lesen Sie den jeweiligen Arbeitsablauf im entsprechenden Lernprogramm für erforderliche benutzerdefinierte Felder, je nach Anwendungsfall.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `$ref` | Das Datenverhalten für die neue Klasse. Für Ad-hoc-Klassen muss dieser Wert auf `https://ns.adobe.com/xdm/data/adhoc`eingestellt sein. |
| `properties._adhoc` | Ein Objekt, das die benutzerdefinierten Felder für die Klasse enthält, ausgedrückt als Schlüssel-Wert-Paare von Feldnamen und Datentypen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neuen Klasse zurück und ersetzt den Namen des `properties._adhoc` Objekts durch eine GUID, die eine systemgenerierte, schreibgeschützte eindeutige Kennung für die Klasse ist. Das `meta:datasetNamespace` Attribut wird auch automatisch generiert und in die Antwort aufgenommen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `$id` | Ein URI, der als schreibgeschützter, vom System generierter eindeutiger Bezeichner für die neue Ad-hoc-Klasse dient. Dieser Wert wird im nächsten Schritt zum Erstellen eines Ad-hoc-Schemas verwendet. |

## Erstellen eines Ad-hoc-Schemas

Nachdem Sie eine Ad-hoc-Klasse erstellt haben, können Sie ein neues Schema erstellen, das diese Klasse implementiert, indem Sie eine POST-Anforderung an den `/tenant/schemas` Endpunkt senden.

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Mit der folgenden Anforderung wird ein neues Schema erstellt, das einen Verweis (`$ref`) auf die `$id` der zuvor erstellten Ad-hoc-Klasse in ihrer Nutzlast bereitstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Schemas zurück, einschließlich des systemgenerierten schreibgeschützten  `$id`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## Ansicht des vollständigen Ad-hoc-Schemas

>[!NOTE]
>
>Dieser Schritt ist optional. Wenn Sie die Feldstruktur Ihres Ad-hoc-Schemas nicht überprüfen möchten, können Sie am Ende dieses Lernprogramms zum Abschnitt &quot; [Nächste Schritte](#next-steps) &quot;wechseln.

Nachdem das Ad-hoc-Schema erstellt wurde, können Sie eine GET-Anforderung (Lookup) erstellen, um das Schema in seinem erweiterten Formular Ansicht. Dies geschieht mit dem entsprechenden Accept-Header in der GET-Anforderung, wie nachfolgend gezeigt.

**API-Format**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` das Ad-hoc-Schema, auf das Sie zugreifen möchten. |

**Anfrage**

Die folgende Anforderung verwendet den Accept-Header `application/vnd.adobe.xed-full+json; version=1`, der das erweiterte Formular des Schemas zurückgibt. Beachten Sie, dass beim Abrufen einer bestimmten Ressource aus dem [!DNL Schema Registry]Anforderungsheader &quot;Akzeptieren&quot;die Hauptversion der betreffenden Ressource enthalten sein muss.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Bei einer erfolgreichen Antwort werden die Details des Schemas einschließlich aller verschachtelten Felder zurückgegeben `properties`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## Nächste Schritte {#next-steps}

Indem Sie diesem Tutorial folgen, haben Sie erfolgreich ein neues Ad-hoc-Schema erstellt. Wenn Sie als Teil eines anderen Lernprogramms zu diesem Dokument gebracht wurden, können Sie jetzt die `$id` Funktion Ihres Ad-hoc-Schemas verwenden, um den Workflow wie gewünscht abzuschließen.

Weitere Informationen zum Arbeiten mit der [!DNL Schema Registry] API finden Sie im [Entwicklerhandbuch](../api/getting-started.md).