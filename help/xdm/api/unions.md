---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vereinigungen
topic: developer guide
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 1%

---


# Vereinigungen

Vereinigungen (oder Vereinigungen-Ansichten) sind systemgenerierte schreibgeschützte Schema, die die Felder aller Schema, die dieselbe  besitzen (XDM ExperienceEvent oder XDM Individual Profil), Aggregat enthalten und für das [Echtzeit-Profil](../../profile/home.md)des Kunden aktiviert sind.

In diesem Dokument werden wesentliche Konzepte für die Arbeit mit Vereinigungen in der Schema Registry-API beschrieben, einschließlich Beispielaufrufen für verschiedene Vorgänge. Weitere allgemeine Informationen zu Vereinigungen in XDM finden Sie im Abschnitt zu Vereinigungen in den [Grundlagen der Schema-Komposition](../schema/composition.md#union).

## Vereinigung mixins

Die Schema-Registrierung enthält automatisch drei Mixins innerhalb des Vereinigung-Schemas: `identityMap`, `timeSeriesEvents`und `segmentMembership`.

### Identitätskarte

Das Schema einer Vereinigung `identityMap` ist eine Darstellung der bekannten Identitäten innerhalb der zugehörigen DatensatzSchema der Vereinigung. Die Identitätszuordnung trennt Identitäten in verschiedene Arrays, die nach Namensraum geordnet sind. Jede aufgelistete Identität ist selbst ein Objekt, das einen eindeutigen `id` Wert enthält.

See the [Identity Service documentation](../../identity-service/home.md) for more information.

### Zeitreihen-Ereignis

Das `timeSeriesEvents` Array ist eine Liste von Ereignissen aus Zeitreihen, die sich auf die Schema beziehen, die der Vereinigung zugeordnet sind. Wenn Profil-Daten in Datasets exportiert werden, ist dieses Array für jeden Datensatz enthalten. Dies ist in verschiedenen Anwendungsfällen nützlich, z. B. beim maschinellen Lernen, bei dem Modelle zusätzlich zu den Datensatzattributen den gesamten Verhaltensverlauf eines Profils benötigen.

### Segmentmitgliedschaft

Die `segmentMembership` Zuordnung speichert die Ergebnisse der Segmentbewertungen. Wenn Segmentaufträge mit der [Segmentierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)erfolgreich ausgeführt werden, wird die Zuordnung aktualisiert. `segmentMembership` speichert auch alle vorab ausgewerteten Audiencen, die in Platform integriert werden, sodass sie mit anderen Lösungen wie Adobe Audience Manager integriert werden können.

Weitere Informationen finden Sie im Tutorial zum [Erstellen von Segmenten mit APIs](../../segmentation/tutorials/create-a-segment.md) .

## Schema für die Vereinigung-Mitgliedschaft aktivieren

Damit ein Schema in die Ansicht der zusammengeführten Vereinigung aufgenommen werden kann, muss das Tag &quot;Vereinigung&quot;dem `meta:immutableTags` Attribut des Schemas hinzugefügt werden. Dies erfolgt über eine PATCH-Anforderung, um das Schema zu aktualisieren und das `meta:immutableTags` Array mit dem Wert &quot;Vereinigung&quot;hinzuzufügen.

>[!NOTE] Unveränderliche Tags sind Tags, die festgelegt, aber nie entfernt werden sollen.

**API-Format**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{SCHEMA_ID}` | Der URL-kodierte `$id` URI oder `meta:altId` des Schemas, das für die Verwendung in Profil aktiviert werden soll. |

**Anfrage**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Schemas zurück, das jetzt ein `meta:immutableTags` Array mit dem Zeichenfolgenwert &quot;Vereinigung&quot;enthält.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552091263267,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Vereinigungen der Liste

Wenn Sie das Tag &quot;Vereinigung&quot;auf einem Schema festlegen, erstellt und verwaltet die Schema-Registrierung automatisch eine Vereinigung für die Klasse, auf der das Schema basiert. Die `$id` für die Vereinigung ähnelt dem Standard `$id` einer Klasse, wobei der einzige Unterschied darin besteht, dass zwei Unterstriche und das Wort &quot;Vereinigung&quot;(`"__union"`) angehängt werden.

Um eine Liste der verfügbaren Vereinigungen Ansicht, können Sie eine GET-Anforderung an den `/unions` Endpunkt durchführen.

**API-Format**

```http
GET /tenant/unions
```

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) und ein `results` Array im Antworttext zurück. Wenn Vereinigungen definiert wurden, werden die `title`, `$id`, `meta:altId`und `version` für jede Vereinigung als Objekte im Array bereitgestellt. Wenn keine Vereinigungen definiert wurden, wird HTTP-Status 200 (OK) zurückgegeben, aber das `results` Array ist leer.

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## Eine bestimmte Vereinigung nachschlagen

Sie können eine bestimmte Vereinigung durch eine GET-Anforderung, die den `$id` und, je nach Accept-Header, einige oder alle Details der Vereinigung enthält, eine Ansicht durchführen.

>[!NOTE] Vereinigungen-Lookups sind über den `/unions` und- `/schemas` Endpunkt verfügbar, um sie für die Verwendung in Profil-Exporten in einen Datensatz zu aktivieren.

**API-Format**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{UNION_ID}` | Der URL-kodierte `$id` URI der Vereinigung, die Sie suchen möchten. URIs für Schema der Vereinigung werden mit &quot;__Vereinigung&quot;angehängt. |

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Anforderungen für die Suche nach Vereinigungen müssen in den Accept-Header aufgenommen `version` werden.

Die folgenden Accept-Header stehen für die Vereinigung Schema-Suche zur Verfügung:

| Accept | Beschreibung |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Roh mit `$ref` und `allOf`. Umfasst Titel und Beschreibungen. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` Attribute und `allOf` gelöst. Umfasst Titel und Beschreibungen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Ansicht der Vereinigung aller Schema zurück, die die Klasse implementieren, deren `$id` Bereitstellung im Anforderungspfad erfolgte.

Das Antwortformat hängt vom Accept-Header ab, der in der Anforderung gesendet wird. Experimentieren Sie mit verschiedenen Accept-Kopfzeilen, um die Antworten zu vergleichen und festzustellen, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## Liste von Schemas in einer Vereinigung

Um zu sehen, welche Schema zu einer bestimmten Vereinigung gehören, können Sie eine GET-Anforderung mithilfe von Abfrage-Parametern durchführen, um die Schema innerhalb des Mieters zu filtern.

Mithilfe des Parameters `property` &quot;Abfrage&quot;können Sie die Antwort so konfigurieren, dass nur Schema zurückgegeben werden, die ein Feld und ein Feld `meta:immutableTags` `meta:class` gleich der Klasse enthalten, auf deren Vereinigung Sie zugreifen.

**API-Format**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Die `$id` Klasse, auf die Sie zugreifen möchten. |

**Anfrage**

Die folgende Anforderung untersucht alle Schema, die zur XDM Individual Profil-Klasse-Vereinigung gehören.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine gefilterte Liste von Schemas zurück, die nur die  enthalten, die beide Anforderungen erfüllen. Denken Sie daran, dass bei der Verwendung mehrerer Parameter der Abfrage eine UND-Beziehung angenommen wird. Das Format der Antwort hängt vom Accept-Header ab, der in der Anforderung gesendet wird.

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
