---
keywords: Experience Platform;Startseite;beliebte Themen;API;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Ad-hoc;Tutorial;Tutorial;Erstellen;Schema;Schema
solution: Experience Platform
title: Erstellen eines Ad-hoc-Schemas
description: Unter bestimmten Umständen kann es erforderlich sein, ein (Experience-Datenmodell) XDM-Schema mit Feldern zu erstellen, deren Namespace nur für die Verwendung durch einen einzigen Datensatz vorgesehen ist. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schema werden für die Experience Platform in verschiedenen Workflows zur Datenerfassung verwendet, einschließlich der Erfassung von CSV-Dateien und der Erstellung bestimmter Quell-Verbindungen.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 13%

---


# Erstellen eines Ad-hoc-Schemas

Unter bestimmten Umständen kann es erforderlich sein, ein [!DNL Experience Data Model] (XDM)-Schema mit Feldern zu erstellen, die nur für die Verwendung durch einen einzigen Datensatz benannt werden. Ein solches Schema wird als Ad-hoc-Schema bezeichnet. Ad-hoc-Schema werden in verschiedenen Workflows für [!DNL Experience Platform] verwendet, einschließlich der Erfassung von CSV-Dateien und der Erstellung bestimmter Arten von Quellverbindungen.

Dieses Dokument enthält allgemeine Schritte zum Erstellen eines Ad-hoc-Schemas mit der [Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). Es soll in Verbindung mit anderen [!DNL Experience Platform]-Lehrgängen verwendet werden, bei denen im Rahmen des Workflows ein Ad-hoc-Schema erstellt werden muss. Jedes dieser Dokumente enthält detaillierte Informationen zur ordnungsgemäßen Konfiguration eines Ad-hoc-Schemas für den jeweiligen Verwendungsfall.

## Erste Schritte

Dieses Lernprogramm erfordert ein Arbeitsverständnis mit dem [!DNL Experience Data Model] (XDM) System. Bevor Sie dieses Lernprogramm starten, lesen Sie bitte die folgende XDM-Dokumentation:

- [XDM-System - Übersicht](../home.md): Eine allgemeine Übersicht über XDM und seine Implementierung in  [!DNL Experience Platform].
- [Grundlagen der Zusammensetzung](../schema/composition.md) des Schemas: Eine Übersicht über die Grundkomponenten von XDM-Schemas.

Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte das [Entwicklerhandbuch](../api/getting-started.md), um wichtige Informationen zu erhalten, die Sie kennen müssen, damit Sie erfolgreich Aufrufe an die [!DNL Schema Registry]-API tätigen können. Diese umfassen Ihre `{TENANT_ID}`, das Konzept sogenannter „Container“ und die für Anfragen erforderlichen Kopfzeilen, von denen insbesondere die Accept-Kopfzeile und deren mögliche Werte wichtig sind.

## Erstellen einer Ad-hoc-Klasse

Das Datenverhalten eines XDM-Schemas wird durch seine zugrunde liegende Klasse bestimmt. Der erste Schritt beim Erstellen eines Ad-hoc-Schemas besteht darin, eine Klasse zu erstellen, die auf dem `adhoc`-Verhalten basiert. Senden Sie dazu eine POST-Anfrage an den `/tenant/classes`-Endpunkt.

**API-Format**

```http
POST /tenant/classes
```

**Anfrage**

Die folgende Anforderung erstellt eine neue XDM-Klasse, die von den in der Payload bereitgestellten Attributen konfiguriert wird. Durch Angabe einer `$ref`-Eigenschaft, die auf `https://ns.adobe.com/xdm/data/adhoc` im `allOf`-Array gesetzt ist, übernimmt diese Klasse das `adhoc`-Verhalten. Die Anforderung definiert auch ein `_adhoc`-Objekt, das die benutzerdefinierten Felder für die Klasse enthält.

>[!NOTE]
>
>Die unter `_adhoc` definierten benutzerdefinierten Felder können je nach Anwendungsfall des Ad-hoc-Schemas variieren. Bitte lesen Sie den jeweiligen Arbeitsablauf im entsprechenden Lernprogramm für erforderliche benutzerdefinierte Felder, je nach Anwendungsfall.

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

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neuen Klasse zurück und ersetzt den Namen des Objekts `properties._adhoc` durch eine GUID, die eine systemgenerierte, schreibgeschützte eindeutige Kennung für die Klasse ist. Das `meta:datasetNamespace`-Attribut wird ebenfalls automatisch generiert und in die Antwort aufgenommen.

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

Nachdem Sie eine Ad-hoc-POST erstellt haben, können Sie ein neues Schema erstellen, das diese Klasse implementiert, indem Sie eine Anforderung an den `/tenant/schemas`-Endpunkt senden.

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Mit der folgenden Anforderung wird ein neues Schema erstellt, das einen Verweis (`$ref`) auf das `$id` der zuvor erstellten Ad-hoc-Klasse in ihrer Nutzlast bereitstellt.

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

## Ansicht des vollständigen Ad-hoc-Schemas

>[!NOTE]
>
> Dieser Schritt ist optional. Wenn Sie die Feldstruktur Ihres Ad-hoc-Schemas nicht überprüfen möchten, können Sie am Ende dieses Lernprogramms mit dem Abschnitt [Nächste Schritte](#next-steps) fortfahren.

Nachdem das Ad-hoc-Schema erstellt wurde, können Sie eine Suchanfrage (GET) stellen, um das Schema in seinem erweiterten Formular Ansicht. Dies geschieht mit dem entsprechenden Accept-Header in der GET-Anforderung, wie nachfolgend gezeigt.

**API-Format**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id`-URI oder `meta:altId` des Ad-hoc-Schemas, auf das Sie zugreifen möchten. |

**Anfrage**

Die folgende Anforderung verwendet den Accept-Header `application/vnd.adobe.xed-full+json; version=1`, der das erweiterte Formular des Schemas zurückgibt. Beachten Sie, dass beim Abrufen einer bestimmten Ressource aus dem [!DNL Schema Registry] der Accept-Header der Anforderung eine Hauptversion der betreffenden Ressource enthalten muss.

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

Indem Sie diesem Tutorial folgen, haben Sie erfolgreich ein neues Ad-hoc-Schema erstellt. Wenn Sie als Teil eines anderen Lernprogramms zu diesem Dokument gebracht wurden, können Sie jetzt das `$id` Ihres Ad-hoc-Schemas verwenden, um den Workflow wie gewünscht abzuschließen.

Weitere Informationen zum Arbeiten mit der [!DNL Schema Registry]-API finden Sie im [Entwicklerhandbuch](../api/getting-started.md).