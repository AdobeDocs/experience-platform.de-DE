---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Schema erstellen
topic: developer guide
translation-type: tm+mt
source-git-commit: 162316c3b908ffa87d8df4dff72e26ba237993db
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 1%

---


# Schema erstellen

Ein Schema kann als Entwurf für die Daten betrachtet werden, die Sie in Experience Platform erfassen möchten. Jedes Schema besteht aus einer Klasse und null oder mehr Mixins. Das heißt, Sie müssen kein Mixin hinzufügen, um ein Schema zu definieren, aber in den meisten Fällen wird mindestens ein Mixin verwendet.

Der Prozess der Schema-Komposition beginnt mit der Zuweisung einer Klasse. Die Klasse definiert wichtige verhaltensbezogene Aspekte der Daten (Datensatz oder Zeitreihen) sowie die Mindestfelder, die erforderlich sind, um die erfassten Daten zu beschreiben.

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die Anforderung muss ein `allOf` Attribut enthalten, das auf den Wert `$id` einer Klasse verweist. Dieses Attribut definiert die &quot;Basisklasse&quot;, die vom Schema implementiert wird. In diesem Beispiel ist die Basisklasse eine Klasse mit dem Namen &quot;Eigenschaftsinformationen&quot;, die zuvor erstellt wurde.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `allOf > $ref` | Der `$id` Wert der Klasse, die vom neuen Schema implementiert wird. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und eine Nutzlast mit den Details des neu erstellten Schemas zurück, einschließlich der Variablen `$id`, `meta:altId`und `version`. Diese Werte sind schreibgeschützt und werden von der Schema Registry zugewiesen.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

Wenn Sie eine GET-Anforderung zur Liste aller Schema im Pächter-Container ausführen, ist jetzt das Schema Eigenschafteninformationen enthalten. Alternativ können Sie eine GET-Anforderung mit dem URL-kodierten `$id` URI ausführen, um das neue Schema direkt Ansicht. Denken Sie daran, die `version` in den Accept-Header für alle Nachschlageanforderungen einzuschließen.
