---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ressource nachschlagen
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 95%

---


# Ressource nachschlagen

Sie können einzelne Ressourcen nachschlagen, indem Sie eine GET-Anfrage ausführen, die die `$id` (URL-kodierten URI) der Ressource im Anfragepfad enthält.

**API-Format**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, in dem sich die Ressourcen befinden („global“oder „tenant“). |
| `{RESOURCE_TYPE}` | The type of resource to retrieve from the [!DNL Schema Library]. Gültige Typen sind `datatypes`, `mixins`, `schemas` und `classes`. |
| `{RESOURCE_ID}` | Der URL-codierte `$id`-URI oder `meta:altId` der Ressource. |

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

Bei Anfragen zum Nachschlagen von Ressourcen muss in die Accept-Kopfzeile eine `version` aufgenommen werden. Folgende Accept-Kopfzeilen stehen für Nachschlagevorgänge zur Verfügung:

| Accept | Beschreibung |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Roh mit `$ref` und `allOf`, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, verfügt über Titel und Beschreibungen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Roh mit `$ref` und `allOf`, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, keine Titel oder Beschreibungen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` und `allOf` aufgelöst, einschließlich Deskriptoren. |

>[!NOTE]
>
>Wenn Sie nur die `major` Version (1, 2, 3 usw.) angeben, gibt die Registrierung automatisch die neueste `minor` Version (.1, .2, .3 usw.) zurück.

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Ressource zurück. Die zurückgegebenen Felder hängen von der Accept-Kopfzeile ab, die in der Anfrage gesendet wurde. Experimentieren Sie mit verschiedenen Accept-Kopfzeilen, um die Antworten zu vergleichen und zu ermitteln, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

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
