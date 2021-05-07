---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;Vereinigung;Vereinigung;Vereinigungen;Vereinigungen;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Vereinigungen-API-Endpunkt
description: Mit dem Endpunkt /Vereinigungen in der Schema Registry API können Sie XDM-Vereinigung-Schema in Ihrer Experience-Anwendung programmgesteuert verwalten.
topic-legacy: developer guide
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 47%

---

# Vereinigungen-Endpunkt

Vereinigungen (oder Vereinigungen-Ansichten) sind systemgenerierte schreibgeschützte Schema, die die Felder aller Schema Aggregat geben, die dieselbe Klasse ([!DNL XDM ExperienceEvent] oder [!DNL XDM Individual Profile]) teilen und für [[!DNL Real-time Customer Profile]](../../profile/home.md) aktiviert sind.

In diesem Dokument werden wesentliche Konzepte für die Arbeit mit Vereinigungen in der Schema Registry-API beschrieben, einschließlich Beispielaufrufen für verschiedene Vorgänge. Weitere allgemeine Informationen zu Vereinigungen in XDM finden Sie im Abschnitt zu Vereinigungen in den [Grundlagen der Schema-Komposition](../schema/composition.md#union).

## Vereinigung Schema-Felder

Das [!DNL Schema Registry] enthält automatisch drei Schlüsselfelder in einem Vereinigung-Schema: `identityMap`, `timeSeriesEvents` und `segmentMembership`.

### Identitätszuordnung

Die `identityMap` eines Vereinigungs-Schemas ist eine Darstellung der bekannten Identitäten innerhalb der zugehörigen Datensatz-Schemas der Vereinigung. Die Identitätszuordnung teilt Identitäten in verschiedene Arrays auf, die nach Namensraum geordnet sind. Jede aufgelistete Identität ist selbst ein Objekt, das einen eindeutigen `id`-Wert enthält. Weitere Informationen finden Sie in der [Dokumentation für Identity Service](../../identity-service/home.md).

### Zeitreihenereignisse

Das `timeSeriesEvents`-Array ist eine Liste von Ereignissen aus Zeitreihen, die sich auf die Schemas beziehen, die der Vereinigung zugeordnet sind. Wenn Profil-Daten in Datasets exportiert werden, ist dieses Array für jeden Datensatz enthalten. Dies ist in verschiedenen Anwendungsfällen nützlich, z. B. beim Machine Learning, bei dem Modelle zusätzlich zu den Datensatzattributen den gesamten Verhaltensverlauf eines Profils benötigen.

### Segmentzugehörigkeitszuordnung

Die `segmentMembership`-Zuordnung speichert die Ergebnisse der Segmentauswertungen. Wenn Segmentaufträge mit der [Segmentation-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) erfolgreich ausgeführt werden, wird die Zuordnung aktualisiert. `segmentMembership` speichert auch alle vorab ausgewerteten Zielgruppensegmente, die in Platform integriert werden, sodass sie mit anderen Lösungen wie Adobe Audience Manager integriert werden können. Weitere Informationen finden Sie im Tutorial zum [Erstellen von Segmenten mit APIs](../../segmentation/tutorials/create-a-segment.md).

## Abrufen einer Liste von Vereinigungen {#list}

Wenn Sie das `union`-Tag für ein Schema festlegen, fügt das [!DNL Schema Registry] automatisch das Schema zur Vereinigung der Klasse hinzu, auf der das Schema basiert. Wenn für die betreffende Klasse keine Vereinigung vorhanden ist, wird automatisch eine neue Vereinigung erstellt. Die `$id`-Variable für die Vereinigung ähnelt dem Standard `$id` anderer [!DNL Schema Registry]-Ressourcen. Der einzige Unterschied besteht darin, dass zwei Unterstriche und das Wort &quot;Vereinigung&quot;(`__union`) angehängt werden.

Sie können eine Liste der verfügbaren Vereinigungen durch eine GET an den Endpunkt `/tenant/unions` Ansicht haben.

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

Das Antwortformat hängt von der `Accept`-Kopfzeile ab, die in der Anforderung gesendet wird. Die folgenden `Accept`-Kopfzeilen stehen zur Auflistung von Vereinigungen zur Verfügung:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung der einzelnen Ressourcen zurück. Dies ist die empfohlene Kopfzeile für die Auflistung der Ressourcen. (Maximal: 300) |
| `application/vnd.adobe.xed+json` | Gibt für jede Ressource die vollständige JSON-Klasse zurück, wobei die ursprünglichen Werte `$ref` und `allOf` enthalten sind. (Maximal: 300) |

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

## Suchen einer Vereinigung {#lookup}

Sie können eine bestimmte Vereinigung durch eine GET-Anfrage anzeigen, die die `$id` und, je nach Accept-Kopfzeile, einige oder alle Details der Vereinigung beinhaltet.

>[!NOTE]
>
>Vereinigungen-Lookups sind mit dem Endpunkt `/unions` und `/schemas` verfügbar, um sie für die Verwendung in [!DNL Profile]-Exporten in ein Dataset zu aktivieren.

**API-Format**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{UNION_ID}` | Der URL-kodierte `$id`-URI der Vereinigung, die Sie nachschlagen möchten. Bei URIs für Vereinigungs-Schemas wird „__Vereinigung“ angehängt. |

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
| `application/vnd.adobe.xed+json; version=1` | Roh mit `$ref` und `allOf`. Umfasst Titel und Beschreibungen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` Attribute und `allOf` gelöst. Umfasst Titel und Beschreibungen. |

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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/477bb01d7125b015b4feba7bccc2e599"
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
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/477bb01d7125b015b4feba7bccc2e599",
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

Damit ein Schema in die Vereinigung für seine Klasse aufgenommen werden kann, muss dem Attribut `meta:immutableTags` des Schemas ein `union`-Tag hinzugefügt werden. Dies können Sie erreichen, indem Sie eine PATCH auffordern, dem betreffenden Schema ein `meta:immutableTags`-Array mit einem einzelnen Zeichenfolgenwert `union` hinzuzufügen. Ein detailliertes Beispiel finden Sie unter [Schemas endpoint guide](./schemas.md#union).

## Auflisten von Schemas in einer Vereinigung {#list-schemas}

Um zu sehen, welche Schema zu einer bestimmten Vereinigung gehören, können Sie eine GET an den `/tenant/schemas`-Endpunkt senden. Mithilfe des Abfrageparameters `property` können Sie die Antwort so konfigurieren, dass nur Schemas zurückgegeben werden, die ein `meta:immutableTags`-Feld und eine `meta:class` gleich der Klasse enthalten, auf deren Vereinigung Sie zugreifen.

**API-Format**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CLASS_ID}` | Die `$id` der Klasse, deren Schema mit aktivierter Vereinigung Sie Liste haben möchten. |

**Anfrage**

Die folgende Anforderung ruft eine Liste aller Schema ab, die Teil der Vereinigung für die [!DNL XDM Individual Profile]-Klasse sind.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt von der `Accept`-Kopfzeile ab, die in der Anforderung gesendet wird. Die folgenden `Accept`-Kopfzeilen stehen zur Auflistung von Schemas zur Verfügung:

| `Accept`-Kopfzeile | Beschreibung |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Gibt eine kurze Zusammenfassung der einzelnen Ressourcen zurück. Dies ist die empfohlene Kopfzeile für die Auflistung der Ressourcen. (Maximal: 300) |
| `application/vnd.adobe.xed+json` | Gibt für jede Ressource das vollständige JSON-Schema zurück, wobei die ursprünglichen Werte `$ref` und `allOf` enthalten sind. (Maximal: 300) |

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
