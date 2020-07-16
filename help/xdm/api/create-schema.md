---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Schema erstellen
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 88%

---


# Schema erstellen

A schema can be thought of as the blueprint for the data you wish to ingest into [!DNL Experience Platform]. Jedes Schema besteht aus einer Klasse und null oder mehr Mixins. Das heißt, Sie müssen kein Mixin hinzufügen, um ein Schema zu definieren; in den meisten Fällen wird aber mindestens ein Mixin verwendet.

Der Prozess der Schemakomposition beginnt mit der Zuweisung einer Klasse. Die Klasse definiert wichtige verhaltensbezogene Aspekte der Daten (Datensatz oder Zeitreihen) sowie die Mindestfelder, die erforderlich sind, um die zu erfassenden Daten zu beschreiben.

**API-Format**

```http
POST /tenant/schemas
```

**Anfrage**

Die Anfrage muss ein `allOf`-Attribut enthalten, das auf die `$id` einer Klasse verweist. Dieses Attribut definiert die „Basisklasse“, die vom Schema implementiert wird. In diesem Beispiel ist die Basisklasse eine Klasse vom Typ „Eigenschaftsinformationen“, die zuvor erstellt wurde.

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
| `allOf > $ref` | Der `$id`-Wert der Klasse, die vom neuen Schema implementiert wird. |

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und eine Payload mit den Details zum neu erstellten Schema zurück, einschließlich `$id`, `meta:altId` und `version`. These values are read-only and are assigned by the [!DNL Schema Registry].

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

Wenn Sie eine GET-Anfrage zum Auflisten aller Schemas im Mandanten-Container ausführen, wäre jetzt das Schema „Eigenschaftsinformationen“ enthalten. Alternativ können Sie eine GET-Anfrage (Nachschlagen) mit dem URL-kodierten `$id` URI ausführen, um das neue Schema direkt anzuzeigen. Denken Sie daran, bei allen Anfragen zum Nachschlagen die `version` in die Accept-Kopfzeile einzuschließen.
