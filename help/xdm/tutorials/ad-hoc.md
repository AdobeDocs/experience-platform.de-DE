---
keywords: Experience Platform;Startseite;beliebte Themen;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schemaregistrierung;Schema Registry;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Tutorial;Tutorial;erstellen;Schema;Schema;Schema
solution: Experience Platform
title: Erstellen eines Ad-hoc-Schemas
description: Unter bestimmten Umständen kann es erforderlich sein, ein (Experience-Datenmodell) XDM-Schema mit Feldern zu erstellen, deren Namespace nur für die Verwendung durch einen einzigen Datensatz vorgesehen ist. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schemas werden in verschiedenen Datenaufnahme-Workflows für Experience Platform verwendet, einschließlich der Aufnahme von CSV-Dateien und der Erstellung bestimmter Arten von Quellverbindungen.
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 16%

---

# Erstellen eines Ad-hoc-Schemas

Unter bestimmten Umständen kann es erforderlich sein, eine [!DNL Experience Data Model] (XDM)-Schema mit Feldern, die nur für die Verwendung durch einen einzigen Datensatz benannt sind. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schemata werden in verschiedenen Datenerfassungs-Workflows für [!DNL Experience Platform], einschließlich der Aufnahme von CSV-Dateien und der Erstellung bestimmter Arten von Quellverbindungen.

Dieses Dokument enthält allgemeine Schritte zum Erstellen eines Ad-hoc-Schemas mit dem [Schema Registry-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Es ist zur Verwendung in Verbindung mit anderen [!DNL Experience Platform] Tutorials, für die im Rahmen ihres Workflows ein Ad-hoc-Schema erstellt werden muss. Jedes dieser Dokumente enthält detaillierte Informationen zur ordnungsgemäßen Konfiguration eines Ad-hoc-Schemas für den jeweiligen Anwendungsfall.

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis von [!DNL Experience Data Model] (XDM)-System. Bevor Sie mit diesem Tutorial beginnen, lesen Sie die folgende XDM-Dokumentation:

- [XDM-System - Übersicht](../home.md): Eine allgemeine Übersicht über XDM und dessen Implementierung in [!DNL Experience Platform].
- [Grundlagen der Schemakomposition](../schema/composition.md): Eine Übersicht über die grundlegenden Komponenten von XDM-Schemas.

Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die [Entwicklerhandbuch](../api/getting-started.md) für wichtige Informationen, die Sie benötigen, um erfolgreich Aufrufe an die [!DNL Schema Registry] API. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.

## Erstellen einer Ad-hoc-Klasse

Das Datenverhalten eines XDM-Schemas wird durch die zugrunde liegende Klasse bestimmt. Der erste Schritt beim Erstellen eines Ad-hoc-Schemas besteht darin, eine Klasse zu erstellen, die auf der `adhoc` Verhalten. Senden Sie dazu eine POST-Anfrage an den `/tenant/classes`-Endpunkt.

**API-Format**

```http
POST /tenant/classes
```

**Anfrage**

Die folgende Anfrage erstellt eine neue XDM-Klasse, die von den in der Payload bereitgestellten Attributen konfiguriert wird. durch Bereitstellung einer `$ref` Eigenschaft auf `https://ns.adobe.com/xdm/data/adhoc` im `allOf` -Array, erbt diese Klasse die `adhoc` Verhalten. Die Anfrage definiert auch eine `_adhoc` -Objekt, das die benutzerdefinierten Felder für die Klasse enthält.

>[!NOTE]
>
>Die benutzerdefinierten Felder, die unter `_adhoc` variieren je nach Anwendungsfall des Ad-hoc-Schemas. Beachten Sie den jeweiligen Workflow im entsprechenden Tutorial für erforderliche benutzerdefinierte Felder basierend auf dem Anwendungsfall.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `$ref` | Das Datenverhalten für die neue Klasse. Für Ad-hoc-Klassen muss dieser Wert auf `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | Ein Objekt, das die benutzerdefinierten Felder für die Klasse enthält, ausgedrückt als Schlüssel-Wert-Paare von Feldnamen und Datentypen. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neuen Klasse zurück und ersetzt die `properties._adhoc` -Objektname mit einer GUID, die eine systemgenerierte, schreibgeschützte eindeutige Kennung für die Klasse ist. Die `meta:datasetNamespace` -Attribut wird auch automatisch generiert und in die Antwort aufgenommen.

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
    "imsOrg": "{ORG_ID}",
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
| `$id` | Ein URI, der als schreibgeschützte, vom System generierte eindeutige Kennung für die neue Ad-hoc-Klasse dient. Dieser Wert wird im nächsten Schritt zum Erstellen eines Ad-hoc-Schemas verwendet. |

{style="table-layout:auto"}

## Erstellen eines Ad-hoc-Schemas

Nachdem Sie eine Ad-hoc-Klasse erstellt haben, können Sie ein neues Schema erstellen, das diese Klasse implementiert, indem Sie eine POST-Anfrage an die `/tenant/schemas` -Endpunkt.

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die folgende Anfrage erstellt ein neues Schema mit einer Referenz (`$ref`) auf `$id` der zuvor erstellten Ad-hoc-Klasse in ihrer Payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Eine erfolgreiche Antwort gibt die Details des neu erstellten Schemas zurück, einschließlich des systemgenerierten schreibgeschützten Schemas `$id`.

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
    "imsOrg": "{ORG_ID}",
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

## Gesamtes Ad-hoc-Schema anzeigen

>[!NOTE]
>
>Dieser Schritt ist optional. Wenn Sie die Feldstruktur Ihres Ad-hoc-Schemas nicht überprüfen möchten, können Sie zum [Nächste Schritte](#next-steps) am Ende dieses Tutorials.

Nachdem das Ad-hoc-Schema erstellt wurde, können Sie eine Nachschlageanfrage (GET) stellen, um das Schema in seiner erweiterten Form anzuzeigen. Dies geschieht mithilfe der entsprechenden Accept-Kopfzeile in der GET-Anfrage, wie unten dargestellt.

**API-Format**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die URL-kodierte `$id` URI oder `meta:altId` des Ad-hoc-Schemas, auf das Sie zugreifen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage verwendet die Accept-Kopfzeile `application/vnd.adobe.xed-full+json; version=1`, das die erweiterte Form des Schemas zurückgibt. Beachten Sie, dass beim Abrufen einer bestimmten Ressource aus dem [!DNL Schema Registry]muss die Accept-Kopfzeile der Anfrage eine Hauptversion der betreffenden Ressource enthalten.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Schemas zurück, einschließlich aller unter verschachtelten Felder `properties`.

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
    "imsOrg": "{ORG_ID}",
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

In diesem Tutorial haben Sie erfolgreich ein neues Ad-hoc-Schema erstellt. Wenn Sie als Teil eines anderen Tutorials zu diesem Dokument gelangt sind, können Sie jetzt die `$id` Ihres Ad-hoc-Schemas verwenden, um den Workflow wie gewünscht abzuschließen.

Weitere Informationen zum Arbeiten mit dem [!DNL Schema Registry] API, siehe [Entwicklerhandbuch](../api/getting-started.md).
