---
title: Hinzufügen bestimmter Felder zu einem Schema mithilfe der Schema Registry-API
description: Erfahren Sie, wie Sie mithilfe der Schema Registry-API einzelne Felder aus bereits vorhandenen Feldergruppen zu einem Experience-Datenmodell(XDM)-Schema hinzufügen.
source-git-commit: 4bcd949e901c11bb933000f7ae76f17134dda496
workflow-type: ht
source-wordcount: '629'
ht-degree: 100%

---

# Hinzufügen bestimmter Felder zu einem Schema mithilfe der Schema Registry-API

Experience-Datenmodell(XDM)-Schemas bestehen aus einer Basisklasse, wobei zusätzliche Felder durch die Verwendung von Standardfeldgruppen eingeschlossen werden, die von Adobe definiert werden, sowie aus benutzerdefinierten Feldergruppen, die von Ihrem Unternehmen definiert werden.

Beim Erstellen eines Schemas können Sie einige Felder aus einer bestimmten Feldergruppe verwenden und gleichzeitig andere nicht benötigte Felder aus derselben Gruppe ausschließen. In diesem Tutorial erfahren Sie, wie Sie mithilfe der Schema Registry-API einzelne Felder aus einer Feldergruppe zu einem Schema hinzufügen.

>[!NOTE]
>
>Informationen zum Hinzufügen und Entfernen einzelner Schemafelder in der Adobe Experience Platform-Benutzeroberfläche finden Sie im Handbuch zu [feldbasierten Workflows](../ui/field-based-workflows.md) (derzeit in der Beta-Phase).

## Voraussetzungen

Dieses Tutorial beinhaltet Aufrufe an die [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Bevor Sie beginnen, lesen Sie das [Entwicklerhandbuch](../api/getting-started.md). Es enthält wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, u. a. zu Ihrer `{TENANT_ID}`, dem Konzept von Containern und den erforderlichen Headern für Anfragen.

## Grundlegendes zum Feld `meta:refProperty` 

Für ein bestimmtes Schema werden die Klassen- und Feldergruppen, die die Struktur enthalten, unter dem zugehörigen `allOf`-Array referenziert. Jede Komponente wird als Objekt mit einer `$ref`-Eigenschaft dargestellt, die auf den Komponenten-URI `$id` verweist.

Das folgende JSON stellt ein vereinfachtes Schema dar, das eine einzelne Klasse (`experienceevent`) und Feldergruppe (`experienceevent-all`) nutzt:

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

Für alle Objekte im `allOf`-Array, das auf eine Feldergruppe verweist, können Sie ein gleichrangiges Feld `meta:refProperty` hinzufügen, um anzugeben, welche Felder in der Gruppe in das Schema aufgenommen werden sollen.

>[!NOTE]
>
>Jedes Feld wird mithilfe einer JSON Pointer-Zeichenfolge angegeben, die den Pfad zum Feld innerhalb der entsprechenden Feldergruppe darstellt. Die Zeichenfolge muss mit einem Schrägstrich (`/`) beginnen und sollte keine `properties`-Namespaces enthalten. Beispiel: `/_experience/campaign/message/id`.

Wenn als Zeichenfolge angegeben, kann `meta:refProperty` sich auf ein einzelnes Feld in einer Gruppe beziehen. Andere Felder derselben Gruppe können mit demselben `$ref`-Wert in einem anderen Objekt mit anderem `meta:refProperty`-Wert aufgenommen werden.

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

`meta:refProperty` kann auch als Array bereitgestellt werden, sodass Sie mehrere Felder angeben können, die aus einer bestimmten Gruppe innerhalb eines einzelnen `allOf`-Listenelements aufgenommen werden sollen:

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

## Hinzufügen von Feldern mithilfe eines PUT-Vorgangs

Sie können eine PUT-Anfrage verwenden, um ein ganzes Schema neu zu schreiben und die Felder zu konfigurieren, die Sie unter `allOf` einschließen möchten.

**API-Format**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-codierte `$id` des Schemas, das Sie umschreiben möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert die spezifischen Felder aus der Feldergruppe unter dem `allOf`-Array.

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
>Weitere Informationen zu PUT-Anfragen für Schemata finden Sie im [Handbuch zu Schema-Endpunkten](../api/schemas.md#put).

## Hinzufügen von Feldern mithilfe eines PATCH-Vorgangs

Sie können eine PATCH-Anfrage verwenden, um einzelne Felder zu einem Schema hinzuzufügen, ohne andere zu überschreiben. Die Schema Registry-API unterstützt alle standardmäßigen JSON-Patch-Vorgänge, einschließlich `add`, `remove` und `replace`. Weitere Informationen zu JSON-Patch-Vorgängen finden Sie im [API-Grundlagenhandbuch](../../landing/api-fundamentals.md#json-patch).

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Die `meta:altId` oder URL-codierte `$id` des Schemas, das Sie umschreiben möchten. |

**Anfrage**

Die folgende Anfrage fügt dem Schema des `allOf`-Arrays ein neues Objekt hinzu. Dabei werden die hinzuzufügenden Felder angegeben.

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
>Weitere Informationen zu PATCH-Anfragen für Schemata finden Sie im [Handbuch zu Schema-Endpunkten](../api/schemas.md#patch).

## Nächste Schritte

In diesem Handbuch wird die Verwendung von API-Aufrufen zum Hinzufügen einzelner Felder aus einer vorhandenen Feldergruppe zu einem Schema beschrieben. Weitere Informationen zum Ausführen ähnlicher feldbasierter Aufgaben in der Platform-Benutzeroberfläche finden Sie im Handbuch zu [feldbasierten Workflows](../ui/field-based-workflows.md).

Weitere Informationen zu den Funktionen der Schema Registry-API und eine vollständige Liste der Endpunkte und Prozesse finden Sie in der [API-Übersicht](../api/overview.md).
