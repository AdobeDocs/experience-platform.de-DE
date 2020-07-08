---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ressourcen suchen
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 2%

---


# Ressourcen suchen

Sie können bestimmte Ressourcen nachschlagen, indem Sie eine GET-Anforderung ausführen, die den `$id` (URL-kodierten URI) der Ressource im Anforderungspfad enthält.

**API-Format**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, in dem sich die Ressourcen befinden (&quot;global&quot;oder &quot;mieter&quot;). |
| `{RESOURCE_TYPE}` | Der Typ der Ressource, die aus der Schema-Bibliothek abgerufen werden soll. Gültige Typen sind `datatypes`, `mixins`, `schemas`und `classes`. |
| `{RESOURCE_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` die Ressource. |

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/mixins/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile-person-details \
  -H 'Accept: application/vnd.adobe.xed+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Ressourcenabfrageanforderungen müssen in den Accept-Header aufgenommen `version` werden. Die folgenden Accept-Header stehen für Suchvorgänge zur Verfügung:

| Accept | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Roh mit `$ref` und `allOf`, hat Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` und `allOf` gelöst, enthält Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Roh mit `$ref` und `allOf`, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` und `allOf` gelöst, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` und `allOf` gelöst, einschließlich Deskriptoren. |

>[!NOTE]
>
>Wenn Sie nur die `major` Version (1, 2, 3 usw.) angeben, gibt die Registrierung automatisch die neueste `minor` Version (.1, .2, .3 usw.) zurück.

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Ressource zurück. Die zurückgegebenen Felder hängen von der Überschrift &quot;Akzeptieren&quot;ab, die in der Anforderung gesendet wird. Experimentieren Sie mit verschiedenen Accept-Kopfzeilen, um die Antworten zu vergleichen und festzustellen, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

```JSON
{
    "$id": "https://ns.adobe.com/xdm/context/profile-person-details",
    "title": "Profile Person Details",
    "type": "object",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Profile person details including naming, gender etc.",
    "definitions": {
        "profile-person-details": {
            "properties": {
                "person": {
                    "title": "Person",
                    "$ref": "https://ns.adobe.com/xdm/context/person",
                    "description": "An individual actor, contact, or owner.",
                    "meta:xdmField": "xdm:person"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
        },
        {
            "$ref": "#/definitions/profile-person-details"
        }
    ],
    "meta:xdmId": "https://ns.adobe.com/xdm/context/profile-person-details",
    "meta:altId": "_xdm.context.profile-person-details",
    "meta:xdmType": "object",
    "meta:status": "experimental",
    "version": "1",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551745787442,
        "repo:lastModifiedDate": 1551745787442
    }
}
```
