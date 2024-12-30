---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schema Registry;Schema Registry;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Ad hoc;Tutorial;Tutorial;erstellen;Erstellen;Schema;Schema
solution: Experience Platform
title: Erstellen eines Ad-hoc-Schemas
description: Unter bestimmten Umständen kann es erforderlich sein, ein (Experience-Datenmodell) XDM-Schema mit Feldern zu erstellen, deren Namespace nur für die Verwendung durch einen einzigen Datensatz vorgesehen ist. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schemata werden in verschiedenen Datenaufnahme-Workflows für Experience Platform verwendet, einschließlich der Aufnahme von CSV-Dateien und der Erstellung bestimmter Arten von Quellverbindungen.
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 15%

---

# Erstellen eines Ad-hoc-Schemas

Unter bestimmten Umständen kann es erforderlich sein, ein [!DNL Experience Data Model] (XDM)-Schema mit Feldern zu erstellen, die sich in einem Namespace befinden und nur von einem einzigen Datensatz verwendet werden können. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schemata werden in verschiedenen Datenaufnahme-Workflows zur [!DNL Experience Platform] verwendet, einschließlich der Aufnahme von CSV-Dateien und der Erstellung bestimmter Arten von Quellverbindungen.

Dieses Dokument enthält allgemeine Schritte zum Erstellen eines Ad-hoc-Schemas mithilfe der [Schema Registry-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Es sollte zusammen mit anderen [!DNL Experience Platform]-Tutorials verwendet werden, für die ein Ad-hoc-Schema im Rahmen des Workflows erstellt werden muss. Jedes dieser Dokumente enthält detaillierte Informationen dazu, wie Sie ein Ad-hoc-Schema für seinen spezifischen Anwendungsfall ordnungsgemäß konfigurieren.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis des [!DNL Experience Data Model] (XDM)-Systems voraus. Bevor Sie mit diesem Tutorial beginnen, lesen Sie die folgende XDM-Dokumentation:

- [XDM-Systemübersicht](../home.md): Allgemeine Übersicht über XDM und die Implementierung in [!DNL Experience Platform].
- [Grundlagen der Schemakomposition](../schema/composition.md): Ein Überblick über die grundlegenden Komponenten von XDM-Schemata.

Bevor Sie mit diesem Tutorial beginnen, lesen Sie [Entwicklerhandbuch](../api/getting-started.md), um wichtige Informationen zu erhalten, die Sie für die erfolgreiche Durchführung von Aufrufen an die [!DNL Schema Registry]-API benötigen. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.

## Erstellen einer Ad-hoc-Klasse

Das Datenverhalten eines XDM-Schemas wird durch seine zugrunde liegende Klasse bestimmt. Der erste Schritt beim Erstellen eines Ad-hoc-Schemas besteht darin, eine Klasse basierend auf dem `adhoc` zu erstellen. Senden Sie dazu eine POST-Anfrage an den `/tenant/classes`-Endpunkt.

**API-Format**

```http
POST /tenant/classes
```

**Anfrage**

Die folgende Anfrage erstellt eine neue XDM-Klasse, die durch die in der Payload bereitgestellten Attribute konfiguriert wird. Durch Bereitstellung einer `$ref`-Eigenschaft, die im `allOf`-Array auf `https://ns.adobe.com/xdm/data/adhoc` gesetzt ist, erbt diese Klasse das `adhoc`. Die Anfrage definiert auch ein `_adhoc`-Objekt, das die benutzerdefinierten Felder für die Klasse enthält.

>[!NOTE]
>
>Die unter `_adhoc` definierten benutzerdefinierten Felder variieren je nach Anwendungsfall des Ad-hoc-Schemas. Siehe den spezifischen Workflow im entsprechenden Tutorial für erforderliche benutzerdefinierte Felder basierend auf dem Anwendungsfall.

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
| `$ref` | Das Datenverhalten für die neue Klasse. Für Ad-hoc-Klassen muss dieser Wert auf `https://ns.adobe.com/xdm/data/adhoc` festgelegt werden. |
| `properties._adhoc` | Ein -Objekt, das die benutzerdefinierten Felder für die -Klasse enthält, ausgedrückt als Schlüssel-Wert-Paare von Feldnamen und Datentypen. |

{style="table-layout:auto"}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neuen Klasse zurück und ersetzt den Namen des `properties._adhoc`-Objekts durch eine GUID, die eine systemgenerierte, schreibgeschützte eindeutige Kennung für die Klasse ist. Das `meta:datasetNamespace` wird ebenfalls automatisch generiert und in die Antwort aufgenommen.

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
| `$id` | Ein URI, der als schreibgeschützter, systemgenerierter eindeutiger Bezeichner für die neue Ad-hoc-Klasse dient. Dieser Wert wird im nächsten Schritt zum Erstellen eines Ad-hoc-Schemas verwendet. |

{style="table-layout:auto"}

## Erstellen eines Ad-hoc-Schemas

Nachdem Sie eine Ad-hoc-POST erstellt haben, können Sie ein neues Schema erstellen, das diese Klasse implementiert, indem Sie eine Klassenanforderung an den `/tenant/schemas`-Endpunkt senden.

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die folgende Anfrage erstellt ein neues Schema und stellt einen Verweis (`$ref`) auf den `$id` der zuvor erstellten Ad-hoc-Klasse in der Payload bereit.

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

Eine erfolgreiche Antwort gibt die Details des neu erstellten Schemas zurück, einschließlich der systemgenerierten, schreibgeschützten `$id`.

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

## Anzeigen des vollständigen Ad-hoc-Schemas

>[!NOTE]
>
>Dieser Schritt ist optional. Wenn Sie die Feldstruktur Ihres Ad-hoc-Schemas nicht überprüfen möchten, können Sie am Ende dieses Tutorials zum Abschnitt [Nächste Schritte](#next-steps) wechseln.

Nachdem das Ad-hoc-Schema erstellt wurde, können Sie eine Suchanfrage (GET) stellen, um das Schema in seiner erweiterten Form anzuzeigen. Dies geschieht mithilfe des entsprechenden Accept-Headers in der GET-Anfrage, wie unten gezeigt.

**API-Format**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id`-URI oder `meta:altId` des Ad-hoc-Schemas, auf das Sie zugreifen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage verwendet die Accept-Header-`application/vnd.adobe.xed-full+json; version=1`, die die erweiterte Form des Schemas zurückgibt. Beachten Sie, dass beim Abrufen einer bestimmten Ressource aus dem [!DNL Schema Registry] der Accept-Header der Anfrage eine Hauptversion der betreffenden Ressource enthalten muss.

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

Eine erfolgreiche Antwort gibt die Details des Schemas zurück, einschließlich aller unter `properties` verschachtelten Felder.

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

In diesem Tutorial haben Sie erfolgreich ein neues Ad-hoc-Schema erstellt. Wenn Sie im Rahmen eines anderen Tutorials zu diesem Dokument weitergeleitet wurden, können Sie jetzt die `$id` Ihres Ad-hoc-Schemas verwenden, um den Workflow wie angewiesen abzuschließen.

Weiterführende Informationen zum Arbeiten mit der [!DNL Schema Registry]-API finden Sie im [Entwicklerhandbuch](../api/getting-started.md).
