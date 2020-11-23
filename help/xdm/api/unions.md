---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;union;Union;unions;Unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Vereinigungen
description: Mit dem Endpunkt /Vereinigungen in der Schema Registry API können Sie XDM-Vereinigung-Schema in Ihrer Experience-Anwendung programmgesteuert verwalten.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 50%

---


# Vereinigungen-Endpunkt

Unions (or union views) are system-generated, read-only schemas that aggregate the fields of all schemas which share the same class ([!DNL XDM ExperienceEvent] or [!DNL XDM Individual Profile]) and are enabled for [[!DNL Real-time Customer Profile]](../../profile/home.md).

In diesem Dokument werden wesentliche Konzepte für die Arbeit mit Vereinigungen in der Schema Registry-API beschrieben, einschließlich Beispielaufrufen für verschiedene Vorgänge. Weitere allgemeine Informationen zu Vereinigungen in XDM finden Sie im Abschnitt zu Vereinigungen in den [Grundlagen der Schema-Komposition](../schema/composition.md#union).

## Vereinigung Schema-Felder

Die Vereinigung enthält [!DNL Schema Registry] automatisch drei Schlüsselfelder in einem Schema: `identityMap`, `timeSeriesEvents`und `segmentMembership`.

### Identitätszuordnung

Die `identityMap` eines Vereinigungs-Schemas ist eine Darstellung der bekannten Identitäten innerhalb der zugehörigen Datensatz-Schemas der Vereinigung. Die Identitätszuordnung teilt Identitäten in verschiedene Arrays auf, die nach Namensraum geordnet sind. Jede aufgelistete Identität ist selbst ein Objekt, das einen eindeutigen `id`-Wert enthält. Weitere Informationen finden Sie in der [Dokumentation für Identity Service](../../identity-service/home.md).

### Zeitreihenereignisse

Das `timeSeriesEvents`-Array ist eine Liste von Ereignissen aus Zeitreihen, die sich auf die Schemas beziehen, die der Vereinigung zugeordnet sind. Wenn Profil-Daten in Datasets exportiert werden, ist dieses Array für jeden Datensatz enthalten. Dies ist in verschiedenen Anwendungsfällen nützlich, z. B. beim Machine Learning, bei dem Modelle zusätzlich zu den Datensatzattributen den gesamten Verhaltensverlauf eines Profils benötigen.

### Segmentzugehörigkeitszuordnung

Die `segmentMembership`-Zuordnung speichert die Ergebnisse der Segmentauswertungen. Wenn Segmentaufträge mit der [Segmentation-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) erfolgreich ausgeführt werden, wird die Zuordnung aktualisiert. `segmentMembership` speichert auch alle vorab ausgewerteten Zielgruppensegmente, die in Platform integriert werden, sodass sie mit anderen Lösungen wie Adobe Audience Manager integriert werden können. Weitere Informationen finden Sie im Tutorial zum [Erstellen von Segmenten mit APIs](../../segmentation/tutorials/create-a-segment.md).

## Retrieve a list of unions {#list}

Wenn Sie das `union` Tag auf einem Schema festlegen, fügt das [!DNL Schema Registry] Schema automatisch der Vereinigung für die Klasse hinzu, auf der das Schema basiert. Wenn für die betreffende Klasse keine Vereinigung vorhanden ist, wird automatisch eine neue Vereinigung erstellt. The `$id` for the union is similar to the standard `$id` of other [!DNL Schema Registry] resources, with the only difference being that is appended by two underscores and the word &quot;union&quot; (`__union`).

Sie können eine Liste der verfügbaren Vereinigungen Ansicht haben, indem Sie eine GET an den `/tenant/unions` Endpunkt anfordern.

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

The response format depends on the `Accept` header sent in the request. The following `Accept` headers are available for listing unions:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung der einzelnen Ressourcen zurück. Dies ist die empfohlene Kopfzeile für die Auflistung der Ressourcen. (Maximal: 300) |
| `application/vnd.adobe.xed+json` | Returns full JSON class for each resource, with original `$ref` and `allOf` included. (Maximal: 300) |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) und ein `results`-Array im Antworttext zurück. Wenn Vereinigungen definiert wurden, werden die Details für jede Vereinigung als Objekte im Array bereitgestellt. Wenn keine Vereinigungen definiert wurden, wird dennoch der HTTP-Status 200 (OK) zurückgegeben, jedoch das `results`-Array ist leer.

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

## Look up a union {#lookup}

Sie können eine bestimmte Vereinigung durch eine GET-Anfrage anzeigen, die die `$id` und, je nach Accept-Kopfzeile, einige oder alle Details der Vereinigung beinhaltet.

>[!NOTE]
>
>Union lookups are available using the `/unions` and `/schemas` endpoint to enable them for use in [!DNL Profile] exports into a dataset.

**API-Format**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{UNION_ID}` | The URL-encoded `$id` URI of the union you want to look up. Bei URIs für Vereinigungs-Schemas wird „__Vereinigung“ angehängt. |

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

Anfragen für das Nachschlagen von Vereinigungen erfordern, dass `version` in die Accept-Kopfzeile aufgenommen wird.

Die folgenden Accept-Kopfzeilen stehen für das Nachschlagen von Vereinigungs-Schemas zur Verfügung:

| Accept | Beschreibung |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Roh mit `$ref` und `allOf`. Umfasst Titel und Beschreibungen. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` Attribute und `allOf` gelöst. Umfasst Titel und Beschreibungen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Vereinigungsansicht aller Schemas zurück, die die Klasse implementieren, deren `$id` im Anfragepfad bereitgestellt wurde.

Das Antwortformat hängt von der Accept-Kopfzeile ab, die in der Anfrage gesendet wird. Experimentieren Sie mit verschiedenen Accept-Kopfzeilen, um die Antworten zu vergleichen und zu ermitteln, welche Kopfzeile für Ihren Anwendungsfall am besten geeignet ist.

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

## Aktivieren eines Schemas für die Vereinigungs-Mitgliedschaft {#enable}

Damit ein Schema in die Vereinigung für seine Klasse aufgenommen werden kann, muss ein `union` -Tag zum `meta:immutableTags` Attribut des Schemas hinzugefügt werden. Dies können Sie erreichen, indem Sie eine PATCH-Anforderung zum Hinzufügen eines `meta:immutableTags` Arrays mit einem einzigen Zeichenfolgenwert `union` zum betreffenden Schema stellen. Ein detailliertes Beispiel finden Sie im [Schemas-Endpunkthandbuch](./schemas.md#union) .

## Auflisten von Schemas in einer Vereinigung {#list-schemas}

Um zu sehen, welche Schema zu einer bestimmten Vereinigung gehören, können Sie eine GET zum `/tenant/schemas` Endpunkt durchführen. Mithilfe des Abfrageparameters `property` können Sie die Antwort so konfigurieren, dass nur Schemas zurückgegeben werden, die ein `meta:immutableTags`-Feld und eine `meta:class` gleich der Klasse enthalten, auf deren Vereinigung Sie zugreifen.

**API-Format**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Die `$id` Klasse, deren Schema mit aktivierter Vereinigung Liste werden sollen. |

**Anfrage**

Die folgende Anforderung ruft eine Liste aller Schema ab, die Teil der Vereinigung für die [!DNL XDM Individual Profile] Klasse sind.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

The response format depends on the `Accept` header sent in the request. The following `Accept` headers are available for listing schemas:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung der einzelnen Ressourcen zurück. Dies ist die empfohlene Kopfzeile für die Auflistung der Ressourcen. (Maximal: 300) |
| `application/vnd.adobe.xed+json` | Returns full JSON schema for each resource, with original `$ref` and `allOf` included. (Maximal: 300) |

**Antwort**

Bei einer erfolgreichen Antwort wird eine gefilterte Liste von Schemas zurückgegeben, die nur die zur angegebenen Vereinigung gehörenden, für die die Mitgliedschaft aktiviert wurde. Beachten Sie, dass bei Abfragen mit mehreren Parametern eine UND-Beziehung impliziert wird.

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
