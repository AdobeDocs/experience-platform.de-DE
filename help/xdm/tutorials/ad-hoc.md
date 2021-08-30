---
keywords: Experience Platform;Startseite;beliebte Themen;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schemaregistrierung;Schema Registry;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Tutorial;Tutorial;erstellen;Schema;Schema;Schema
solution: Experience Platform
title: Erstellen eines Ad-hoc-Schemas
description: Unter bestimmten Umständen kann es erforderlich sein, ein (Experience-Datenmodell) XDM-Schema mit Feldern zu erstellen, deren Namespace nur für die Verwendung durch einen einzigen Datensatz vorgesehen ist. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schemata werden in verschiedenen Datenaufnahme-Workflows zur Experience Platform verwendet, einschließlich der Erfassung von CSV-Dateien und der Erstellung bestimmter Arten von Quellverbindungen.
topic-legacy: tutorial
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 13%

---

# Erstellen eines Ad-hoc-Schemas

Unter bestimmten Umständen kann es erforderlich sein, ein [!DNL Experience Data Model] (XDM)-Schema mit Feldern zu erstellen, deren Namespace nur für die Verwendung durch einen einzigen Datensatz vorgesehen ist. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schemata werden in verschiedenen Datenerfassungs-Workflows für [!DNL Experience Platform] verwendet, einschließlich der Aufnahme von CSV-Dateien und der Erstellung bestimmter Arten von Quellverbindungen.

Dieses Dokument enthält allgemeine Schritte zum Erstellen eines Ad-hoc-Schemas mit der [Schema Registry-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Sie ist für die Verwendung in Verbindung mit anderen [!DNL Experience Platform]-Tutorials vorgesehen, für die im Rahmen ihres Workflows ein Ad-hoc-Schema erstellt werden muss. Jedes dieser Dokumente enthält detaillierte Informationen zur ordnungsgemäßen Konfiguration eines Ad-hoc-Schemas für den jeweiligen Anwendungsfall.

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis des [!DNL Experience Data Model] (XDM)-Systems voraus. Bevor Sie mit diesem Tutorial beginnen, lesen Sie die folgende XDM-Dokumentation:

- [XDM-System - Übersicht](../home.md): Eine allgemeine Übersicht über XDM und dessen Implementierung in  [!DNL Experience Platform].
- [Grundlagen der Schemakomposition](../schema/composition.md): Eine Übersicht über die grundlegenden Komponenten von XDM-Schemas.

Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte das [Entwicklerhandbuch](../api/getting-started.md) , um wichtige Informationen zu erhalten, die Sie benötigen, um die [!DNL Schema Registry]-API erfolgreich aufrufen zu können. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.

## Erstellen einer Ad-hoc-Klasse

Das Datenverhalten eines XDM-Schemas wird durch die zugrunde liegende Klasse bestimmt. Der erste Schritt beim Erstellen eines Ad-hoc-Schemas besteht darin, eine Klasse zu erstellen, die auf dem `adhoc`-Verhalten basiert. Senden Sie dazu eine POST-Anfrage an den `/tenant/classes`-Endpunkt.

**API-Format**

```http
POST /tenant/classes
```

**Anfrage**

Die folgende Anfrage erstellt eine neue XDM-Klasse, die von den in der Payload bereitgestellten Attributen konfiguriert wird. Durch die Bereitstellung einer `$ref` -Eigenschaft, die auf `https://ns.adobe.com/xdm/data/adhoc` im `allOf`-Array gesetzt ist, übernimmt diese Klasse das `adhoc`-Verhalten. Die Anfrage definiert auch ein `_adhoc` -Objekt, das die benutzerdefinierten Felder für die Klasse enthält.

>[!NOTE]
>
>Die unter `_adhoc` definierten benutzerdefinierten Felder variieren je nach Anwendungsfall des Ad-hoc-Schemas. Beachten Sie den jeweiligen Workflow im entsprechenden Tutorial für erforderliche benutzerdefinierte Felder basierend auf dem Anwendungsfall.

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
| `$ref` | Das Datenverhalten für die neue Klasse. Bei Ad-hoc-Klassen muss dieser Wert auf `https://ns.adobe.com/xdm/data/adhoc` gesetzt werden. |
| `properties._adhoc` | Ein Objekt, das die benutzerdefinierten Felder für die Klasse enthält, ausgedrückt als Schlüssel-Wert-Paare von Feldnamen und Datentypen. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neuen Klasse zurück und ersetzt den Namen des Objekts `properties._adhoc` durch eine GUID, die eine systemgenerierte, schreibgeschützte eindeutige Kennung für die Klasse ist. Das Attribut `meta:datasetNamespace` wird ebenfalls automatisch generiert und in die Antwort aufgenommen.

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
| `$id` | Ein URI, der als schreibgeschützte, vom System generierte eindeutige Kennung für die neue Ad-hoc-Klasse dient. Dieser Wert wird im nächsten Schritt zum Erstellen eines Ad-hoc-Schemas verwendet. |

{style=&quot;table-layout:auto&quot;}

## Erstellen eines Ad-hoc-Schemas

Nachdem Sie eine Ad-hoc-Klasse erstellt haben, können Sie ein neues Schema erstellen, das diese Klasse implementiert, indem Sie eine POST-Anfrage an den Endpunkt `/tenant/schemas` stellen.

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die folgende Anfrage erstellt ein neues Schema und stellt einen Verweis (`$ref`) auf die `$id` der zuvor erstellten Ad-hoc-Klasse in ihrer Payload bereit.

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

Eine erfolgreiche Antwort gibt die Details des neu erstellten Schemas zurück, einschließlich des systemgenerierten schreibgeschützten `$id`.

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

## Gesamtes Ad-hoc-Schema anzeigen

>[!NOTE]
>
>Dieser Schritt ist optional. Wenn Sie die Feldstruktur Ihres Ad-hoc-Schemas nicht überprüfen möchten, können Sie am Ende dieses Tutorials zum Abschnitt [Nächste Schritte](#next-steps) überspringen.

Nachdem das Ad-hoc-Schema erstellt wurde, können Sie eine Nachschlageanfrage (GET) stellen, um das Schema in seiner erweiterten Form anzuzeigen. Dies geschieht mithilfe der entsprechenden Accept-Kopfzeile in der GET-Anfrage, wie unten dargestellt.

**API-Format**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id` -URI oder `meta:altId` des Ad-hoc-Schemas, auf das Sie zugreifen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage verwendet die Accept-Kopfzeile `application/vnd.adobe.xed-full+json; version=1`, die das erweiterte Formular des Schemas zurückgibt. Beachten Sie, dass beim Abrufen einer bestimmten Ressource aus dem [!DNL Schema Registry] die Accept-Kopfzeile der Anfrage eine Hauptversion der betreffenden Ressource enthalten muss.

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

In diesem Tutorial haben Sie erfolgreich ein neues Ad-hoc-Schema erstellt. Wenn Sie als Teil eines anderen Tutorials zu diesem Dokument gelangt sind, können Sie jetzt das `$id` Ihres Ad-hoc-Schemas verwenden, um den Workflow wie gewünscht abzuschließen.

Weitere Informationen zum Arbeiten mit der [!DNL Schema Registry]-API finden Sie im [Entwicklerhandbuch](../api/getting-started.md).
