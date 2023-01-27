---
title: Hinzufügen bestimmter Felder zu einem Schema mithilfe der Schema Registry-API
description: Erfahren Sie, wie Sie mithilfe der Schema Registry-API einzelne Felder aus bereits vorhandenen Feldergruppen zu einem Experience-Datenmodell (XDM)-Schema hinzufügen.
source-git-commit: 4bcd949e901c11bb933000f7ae76f17134dda496
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# Hinzufügen bestimmter Felder zu einem Schema mithilfe der Schema Registry-API

Experience-Datenmodell (XDM)-Schemas bestehen aus einer Basisklasse, wobei zusätzliche Felder durch die Verwendung von Standardfeldgruppen eingeschlossen werden, die von der Adobe definiert werden, sowie aus benutzerdefinierten Feldergruppen, die von Ihrem Unternehmen definiert werden.

Beim Erstellen eines Schemas können Sie einige Felder aus einer bestimmten Feldergruppe verwenden und gleichzeitig andere Felder aus derselben Gruppe ausschließen, die Sie nicht benötigen. In diesem Tutorial erfahren Sie, wie Sie mithilfe der Schema Registry-API einzelne Felder aus einer Feldergruppe zu einem Schema hinzufügen.

>[!NOTE]
>
>Informationen zum Hinzufügen und Entfernen einzelner Schemafelder in der Adobe Experience Platform-Benutzeroberfläche finden Sie im Handbuch unter [feldbasierte Workflows](../ui/field-based-workflows.md) (derzeit in der Beta-Phase).

## Voraussetzungen

Dieses Tutorial beinhaltet Aufrufe an die [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Bevor Sie beginnen, lesen Sie bitte die [Entwicklerhandbuch](../api/getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Ihrer `{TENANT_ID}`, das Konzept von Containern und die erforderlichen Kopfzeilen für Anfragen.

## Grundlagen zum `meta:refProperty` field

Für ein bestimmtes Schema werden die Klassen- und Feldergruppen, die die Struktur enthalten, unter dem `allOf` Array. Jede Komponente wird als Objekt dargestellt, das eine `$ref` -Eigenschaft, die auf den URI der Komponente verweist `$id`.

Die folgende JSON stellt ein vereinfachtes Schema dar, das eine einzelne Klasse (`experienceevent`) und Feldergruppe (`experienceevent-all`):

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

Für alle Objekte im `allOf` Array, das auf eine Feldergruppe verweist, können Sie ein gleichrangiges `meta:refProperty` -Feld, um anzugeben, welche Felder in der Gruppe in das Schema aufgenommen werden sollen.

>[!NOTE]
>
>Jedes Feld wird mithilfe einer JSON Pointer-Zeichenfolge angegeben, die den Pfad zum Feld innerhalb der entsprechenden Feldergruppe darstellt. Die Zeichenfolge muss mit einem Schrägstrich (`/`) und sollte keine `properties` Namespaces. Beispiel: `/_experience/campaign/message/id`.

Wenn als Zeichenfolge angegeben, `meta:refProperty` kann sich auf ein einzelnes Feld in einer Gruppe beziehen. Andere Felder derselben Gruppe können mit derselben `$ref` Wert in einem anderen Objekt mit einer anderen `meta:refProperty` -Wert.

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

Alternativ: `meta:refProperty` kann als Array bereitgestellt werden, in dem Sie mehrere Felder angeben können, die aus einer bestimmten Gruppe in einer Gruppe einbezogen werden sollen `allOf` Listenelement:

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## Felder mithilfe eines PUT-Vorgangs hinzufügen

Sie können eine PUT-Anfrage verwenden, um ein ganzes Schema neu zu schreiben und die Felder zu konfigurieren, die Sie unter einbeziehen möchten `allOf`.

**API-Format**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodiert `$id` des Schemas, das Sie umschreiben möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert die spezifischen Felder, die aus der Feldergruppe unter der `allOf` Array.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Schemas zurück.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Weitere Informationen zu PUT-Anfragen für Schemas finden Sie im Abschnitt [Endpunktleitfaden für Schemata](../api/schemas.md#put).

## Felder mithilfe eines PATCH-Vorgangs hinzufügen

Sie können eine PATCH-Anfrage verwenden, um einzelne Felder zu einem Schema hinzuzufügen, ohne andere zu überschreiben. Die Schema Registry unterstützt alle standardmäßigen JSON Patch-Vorgänge, einschließlich `add`, `remove`und `replace`. Weitere Informationen zum JSON Patch finden Sie im Abschnitt [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-patch).

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-kodiert `$id` des Schemas, das Sie umschreiben möchten. |

**Anfrage**

Die folgende Anfrage fügt dem Schema ein neues Objekt hinzu `allOf` Array, das die hinzuzufügenden Felder angibt.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Schemas zurück.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>Weitere Informationen zu PATCH-Anfragen für Schemas finden Sie im Abschnitt [Endpunktleitfaden für Schemata](../api/schemas.md#patch).

## Nächste Schritte

In diesem Handbuch wurde die Verwendung von API-Aufrufen zum Hinzufügen einzelner Felder aus einer vorhandenen Feldergruppe zu einem Schema beschrieben. Weitere Informationen zum Ausführen ähnlicher feldbasierter Aufgaben in der Platform-Benutzeroberfläche finden Sie im Handbuch unter [feldbasierte Workflows](../ui/field-based-workflows.md).

Weitere Informationen zu den Funktionen der Schema Registry-API finden Sie im Abschnitt [API-Übersicht](../api/overview.md) für eine vollständige Liste der Endpunkte und Prozesse.
